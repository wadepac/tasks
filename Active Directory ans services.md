## Base

```
Rename-Computer -NewName
New-NetIPAddress –IPAddress 192.168.1.10 -DefaultGateway 192.168.1.1 -PrefixLength 24 -InterfaceIndex (Get-NetAdapter).InterfaceIndex
Set-DNSClientServerAddress –InterfaceIndex (Get-NetAdapter).InterfaceIndex –ServerAddresses 192.168.1.10
```

## Install and configure AD

```
Install-WindowsFeature -name AD-Domain-Services -IncludeManagementTools
Install-ADDSForest -DomainName ad.contoso.com -DomainNetBIOSName AD -InstallDNS
```

## Install and configure DHCP

```
Install-WindowsFeature -name DHCP -IncludeAllSubFeature
Add-DhcpServerv4Scope -Name “NY Branch1 192.168.113.0” -StartRange 192.168.113.50 -EndRange 192.168.113.250 -SubnetMask 255.255.255.0
Set-DhcpServerv4OptionValue -ScopeID 192.168.113.0 -DnsDomain woshub.com -DnsServer 192.168.13.4 -Router 192.168.113.1
```

## Configure DNS

Forward lookup zone

```
Add-DnsServerPrimaryZone -Name contoso.local -ReplicationScope "Forest" –PassThru
```

Reverse lookup zone
```
Add-DnsServerPrimaryZone -NetworkId "192.168.1.0/24" -ReplicationScope Domain
```

Create A with PTR
```
Add-DnsServerResourceRecordA -Name rds1 -IPv4Address 192.168.1.30 -ZoneName contoso.local  –CreatePtr
```
Delete A
```
Remove-DnsServerResourceRecord -ZoneName contoso.local -RRType A -Name rds1 –Force
```

Create A with PTR from file
```
Import-CSV "C:\PS\NewDnsRecords.txt" | %{
Add-DNSServerResourceRecordA -ZoneName contoso.local -Name $_."HostName" -IPv4Address $_."IPAddress" –CreatePtr
}
```
