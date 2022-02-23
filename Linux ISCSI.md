Install targetcli
```
yum install targetcli
systemctl start target
systemctl enable target
firewall-cmd --permanent --add-port=3260/tcp
firewall-cmd --reload
```

Configure targetcli

```
# targetcli
/> ls
o- /........................................[...]
  o- backstores.............................[...]
  | o- block.................[Storage Objects: 0]
  | o- fileio................[Storage Objects: 0]
  | o- pscsi.................[Storage Objects: 0]
  | o- ramdisk...............[Storage Objects: 0]
  o- iscsi...........................[Targets: 0]
  o- loopback........................[Targets: 0]
/> iscsi/
/iscsi> create
 ```
