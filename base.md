## IP
```
echo "input interface, ip/mask, dns and gateway"read ip_elem
ip_param=($ip_elem)
nmcli connection modify ${ip_param[0]} conn.autoconnect yes conn.interface-name ${ip_param[0]} ipv4.method manual ipv4.addresses ${ip_param[1]} ipv4.dns ${ip_param[2]} ipv4.gateway ${ip_param[3]}
```

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
