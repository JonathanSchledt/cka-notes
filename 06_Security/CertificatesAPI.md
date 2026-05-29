# Certificates API

## Concept

Certificate signing requests are send to the Kubernets Certificates API:

1. Create CertificateSigningRequestObject
2. Review Requests
3. Approve Requests
4. Share Certs to Users

Controller-Manager is responsible for all certificate related operations

## Key Commands

```bash
# crete key
openssl genrsa -out jane.key 2048

# create certificate signing request
openssl req -new -key jane.key -subj "/CN=jane" -out jane.csr

# encode to base64
cat jane.csr | base64 -w 0

k get csr

k certificate approve jane

# show certificate after approval
k get csr jane -o yaml

echo "LS0...Qo=" | base64 --decode
```

## Minimal YAML Example

```yaml
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  creationTimestamp: "2026-02-03T11:45:00Z"
  name: jane-csr
  uid: 9c1a8c5e-3b9a-4f9e-8b4d-1a2f3c4d5e6f
spec:
  signerName: kubernetes.io/kube-apiserver-client
  expirationSeconds: 600 #seconds
  usages:
    - client auth
  request:
    LS0tLS1CRUdJTiBDRVJUSUZJQ0FURSBSRVFVRVNULS0tLS0KTUlJQ1dEQ0NBVUFDQVFBd0
    V6RVJNQThHQTFVRUF3d0libVYzTFhWelpYSXdnZ0VpTUEwR0NTcUdTSWIzRFFFQgpBUVVB
    QTRJQkR3QXdnZ0VLQW9JQkFRRE8wV0pXK0RYc0FKU0lyanBObzV2UklCcGxuemcrNnhjOS
    tVVndrS2kwCkxmQzI3dCsxZUVuT041TXVxOTloZXZtTUVPbnJ
```
