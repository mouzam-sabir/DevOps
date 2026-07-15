# IP TABLES
---
- Check Service
```
systemctl status service-name
```
- View firewall rules
```
iptables -L
```
- View Rules with numbers
```
iptables -L --line-numbers
```
- Basic Rule Command
```
iptables -A INPUT/OUTPUT -p/-s ip-address/port-name-with-number -j ACCEPT/DROP
```
Example: Allow HTTP Traffic
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
# NOTE:
- (-A) FOR APPEND
- (-p) For Port number
- (-s) For IP address
---
- Set default Policy (All Incoming traffic block)
```
iptables -P INPUT DROP 
```
- Delete a Rule
```
iptables -D INPUT rule-number
```
- Flush All Rules
```
iptavles -F
```
- Save rULES
```
Iiptables-save > firewall.rules
```
