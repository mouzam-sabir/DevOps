# Networking Commands
---
# DNS Commands

- Display Network Interface
```
ip a
ifconfig
ip addr show
```
- Check domain ip
```
nslookup google.com
```
- Detailed DNS info
```
dig google.com
```
- Check domain IP and Hostname
```
host google.com
```
---
# Networking Information

- Active network connection and listening ports
```
netstat -tun
```
- Same as Netstat but fast
```
ss -tun
```
- Show Routing table
```
route -n
```
- Show MAC Address of Connected devices 
```
arp -a
```
---
# Firewalls

- Show current rules of firewalls
```
iptables -L
```
---
# Network Troubleshooting

- Capture live network traffic
```
tcpdump -i eth0
```
---
# Interface Control
- Network Interface ON
```
ifup eth0
```
- Network Interface OFF
```
ifdown eth0
```
- Check Ethernet setting
```
ethtool eth0
```
- Check hostname
```
hostname
```
---
# Remote Access

- Remote Server login
```
ssh username@ip
```
- Copy file on remote server
```
scp file.txt username@ip:/home/user
```
- Backup files
```
rsync -avz folder/ user@ip:/backup
```
---
# Network Testing

- Test port or creates a netwrok connection
```
nc -l portnumber
```
- Download files from internet
```
wget link
```
- Request Web or API to check repsonse
```
curl link
```
- Look for ports 
```
nmap
```
- Test connectivity of port
```
telnet google.com portnumber
```
- Check netwrok usgae
```
ifstat
```
- Ping + Traceroute
```
mtr google.com
```
---
# Route Management

- Add a new route to network
```
route add -net ip gw ip
```
- Delete a route on the network
```
route delete default gw ip
```
---
# Promiscuous Mode

- Interface will receive all packets
```
ip link set eth0 promisc on
```
- Promiscuos Mode OFF
```
ip link set eth0 promisc off
```
