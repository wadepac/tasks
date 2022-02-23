## IP Forwarding

```
echo "net.ipv4.ip_forward=1" > /etc/sysctl.conf
```

## Firewalld
List interfaces
```
firewall-cmd --list-interfaces
```
Allow all traffic
```
firewall-cmd --zone=external --add-rich-rule='rule family="ipv4" source address="0.0.0.0/0" accept'
firewall-cmd --zone=internal --add-rich-rule='rule family="ipv4" source address="0.0.0.0/0" accept'
firewall-cmd --runtime-to-permanent
```
