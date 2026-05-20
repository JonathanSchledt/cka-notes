# Gateway API

## Concept

Successor to Ingress - Layer 4 and Layer 7 Routing

GatewayClass: Defines the controller implementation (like IngressClass)
Gateway: Configures listeners (ports, protocols) - managed by infra admins
HTTPRoute: Routing rules attached to a Gateway - managed by app developers

Other Route types: TLSRoute, TCPRoute, UDPRoute, GRPCRoute

## Key Commands

```bash
k get gatewayclass

k get gateway

k get httproute
```

## Minimal YAML Example

```yaml
# Gateway Class
apiVersion: gateway.networking.k8s.io/v1
kind: GatewayClass
metadata:
  name: example-class
spec:
  controllerName: example.com/gateway-controller

#Gateway
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: example-gateway
spec:
  gatewayClassName: example-class
  listeners:
    - name: http
      protocol: HTTP
      port: 80

# HTTP Route
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: example-httproute
spec:
  parentRefs:
    - name: example-gateway
  hostnames:
    - "www.example.com"
  rules:
    - matches:
        - path:
            type: PathPrefix
            value: /login
      backendRefs:
        - name: example-svc
          port: 8080
```
