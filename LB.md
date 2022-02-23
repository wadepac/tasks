## Keepalived

### Master
```
yum -y install keepalived
systemctl enable keepalived
cat << EOF > /etc/keepalived/keepalived.conf
global_defs {
   router_id uMASTER
}

vrrp_instance VI_1 {
    state MASTER
    interface agge
    virtual_router_id 230
    priority 101                        # PAY ATTENTION ON PRIORITY!!
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass SecPassWord              #changepass if need
    }


   virtual_ipaddress {
       173.0.146.251/32 dev agge label agge:0
    }
}
```
### Backup
