# Networking Cluster Nodes

## Key Commands

```bash
# show network interfaces (NICs)
ip link

# show IP addresses assigned to interfaces
ip addr

# assign IP address to interface eth0
ip addr add 192.168.1.10/24 dev eth0

# show routing table
ip route

# add static route via gateway 192.168.2.1
ip route add 192.168.1.0/24 via 192.168.2.1

# show ARP cache (IP <-> MAC mappings)
arp

#older command to show/manipulate routing table
route

# show listening TCP ports and owning processes
netstat -plnt

# check if IP forwarding/routing is enabled
cat /proc/sys/net/ipv4/ip_forward
```
