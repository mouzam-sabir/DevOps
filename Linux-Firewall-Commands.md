# Firewall Commands
---
- Enable Firewall
```
sudo ufw enable
```
- Disable Firewall
```
sudo ufw disable
```
- Check firewall status
```
sudo ufw status
```
- Allow a Port using port number
```
sudo ufw allow 80
```
- Allow a Port using name
```
sudo ufw allow http
```
- Deny a Port
```
sudo ufw deny 80
```
- Delete a rule
```
sudo ufw delete allow 80
```
- List of rules
```
sudo ufw status numbererd
```
- Allow traffic from Specific IP address
```
sudo ufw allow from 192.168.1.1 
```
- Deny traffic from Specific IP address
```
sudo ufw deny from 192.168.1.1
```
- Allow IP range using subnet
```
sudo ufw allow from 192.168.1.1./24
```
- Allow Port Range
```
sudo ufw allow 6000:6007/tcp
```
- Allow from Application profiles name
```
sudo ufw allow 'mouzam'
```
- Reset Firewall
```
sudo ufw reset
```
- Control Login
```
sudo ufw logging on
sudo ufw logging off
```
- Rate limiting
```
sudo ufw limit ssh
```
- Allow outgoing traffic by default
```
sudo ufw default allow outgoing
```
- Deny outgoing traffic by default
```
sudo ufw default deny outgoing
```
- Check Firewall logs
```
sudo tail -f /var/log/ufw.log
```
--- 
# Set Rules

- Add new rule in Firewall
```
iptables -A INPUT -s ip -j ACCEPT
```
- Delete a Firewall rule
```
iptables -D INPUUT -s ip -j ACCEPT
```
- Block All incoming traffic by default
```
iptables -P INPUT DROP
```
- Remove all firewall rules
```
iptables -F INPUT
```
