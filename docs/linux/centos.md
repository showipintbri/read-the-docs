# Centos

## Static IP Address
**Edit:** `/etc/sysconfig/network-scripts/ifcfg-[interface_name]`

```bash
TYPE=Ethernet

BOOTPROTO=static
NAME=eno2
UUID=a6a9b6a7-5215-4cf1-9f74-3d03559674a9
DEVICE=eno2
ONBOOT=yes

IPADDR=10.13.65.246
NETMASK=255.255.255.0
GATEWAY=10.13.65.1
DNS1=1.1.1.1
DNS2=8.8.8.8
```

After Editing the file restart networking: 
```
sudo systemctl restart network
```