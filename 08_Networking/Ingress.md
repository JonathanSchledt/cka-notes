# Ingress

## Concept

Single entry point to route external traffic to internal services based on URL paths or hostnames

Ingress Controller: Deployment of a reverse proxy (e.g. nginx) - not included by default
Ingress Resource: Set of routing rules

pathType:

- Prefix: match URL prefix (most common)
- Exact: full match
- ImplementationSpecific: depends on controller

ingressClassName: which controller handles this Ingress (replaces old `kubernetes.io/ingress.class` annotation)

ssl-redirect: nginx.ingress.kubernetes.io/ssl-redirect: "true"

## Key Commands

```bash
k get ingress

k get ingressclass

k create ingress ingress-test --rule="wear.example.com/=wear-service:80"

k create ingress web --rule="example.com/app*=web-svc:80" --class=nginx
```

## Minimal YAML Example

```yaml
# Ingress Controller Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-ingress-controller
spec:
  replicas: 1
  selector:
    matchLabels:
      name: nginx-ingress
  template:
    metadata:
      labels:
        name: nginx-ingress
    spec:
      containers:
        - name: nginx-ingress-controller
          image: quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.21.0
          args:
            - /nginx-ingress-controller
            - --configmap=$(POD_NAMESPACE)/nginx-configuration
          env:
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: POD_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
          ports:
            - name: http
              containerPort: 80
            - name: https
              containerPort: 443

# Ingress Service
apiVersion: v1
kind: Service
metadata:
  name: nginx-ingress
spec:
  type: NodePort
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
      name: http
    - port: 443
      targetPort: 443
      protocol: TCP
      name: https
  selector:
    name: nginx-ingress

# Service Account
apiVersion: v1
kind: ServiceAccount
metadata:
  name: nginx-ingress-serviceaccount

# Ingress Config Map
kind: ConfigMap
apiVersion: v1
metadata:
  name: nginx-configuration

# Ingress Resource
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-wear-watch
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
spec:
  ingressClassName: nginx
  tls:
    - hosts:
        - example.com
      secretName: example-tls # kubernetes.io/tls secret
  rules:
    - host: example.com
      http:
        paths:
          - path: /wear
            pathType: Prefix
            backend:
              service:
                name: wear-service
                port:
                  number: 80
          - path: /watch
            pathType: Prefix
            backend:
              service:
                name: watch-service
                port:
                  number: 80
```
