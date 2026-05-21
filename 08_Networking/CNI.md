# Container Network Interface

## Concept

IP Adress Mangement (IPAM) -> Responsibility of CNI Plugin

## Key Commands

```bash
# where the container runtime finds the plugin
/opt/cni/bin

# which plugin to use and how to use it is configured in
/etc/cni/net.d

cat /etc/cni/net.d/10-bridge.conf
```

```json
{
	"cniVersion": "0.2.0",
	"name": "mynet",
	"type": "bridge",
	"bridge": "cni0",
	"isGateway": true,
	"ipMasq": true,
	"ipam": {
		"type": "host-local",
		"subnet": "10.22.0.0/16",
		"routes": [
			{
				"dst": "0.0.0.0/0"
			}
		]
	}
}
```
