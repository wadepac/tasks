## Keepalived

### Master
```
yum -y install keepalived
systemctl enable keepalived
cat << EOF > /etc/keepalived/keepalived.conf
global_defs {
   router_id SRV-1
}

vrrp_instance VI_1 {
    state MASTER
    interface ens192
    virtual_router_id 230
    priority 101
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass P@ssw0rd
    }


   virtual_ipaddress {
       172.20.30.150
    }
}
EOF
systemctl restart keepalived
```
### Backup
```
yum -y install keepalived
systemctl enable keepalived
cat << EOF > /etc/keepalived/keepalived.conf
global_defs {
   router_id SRV-2
}

vrrp_instance VI_1 {
    state BACKUP
    interface ens192
    virtual_router_id 230
    priority 100
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass P@ssw0rd
    }


   virtual_ipaddress {
       172.20.30.150
    }
}
EOF
systemctl restart keepalived
```
