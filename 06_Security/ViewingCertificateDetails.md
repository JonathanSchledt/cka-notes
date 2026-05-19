# Viewing Certificate Details

## Key Commands

```bash
# all certificates, keys in cluster provisioned with kubeadm
cat /etc/kubernetes/manifests/kube-apiserver.yaml

# decodes the kube-apiserver's serving certificate and prints it
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
```
