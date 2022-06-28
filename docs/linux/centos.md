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

## Hostname
See current hostname: `hostname`

**Edit:** `vi /etc/hostname`

Validate with: `hostnamectl`

A restart is often required or logout of your current SSH session and log back in.


## Firewall

**Add Port/Protocol Permanently:**
```bash
firewall-cmd --add-port=xxxx/tcp --permanent 
```

**NOTE: YOU MUST RESTART THE SERVICE FOR CHANGES TO TAKE EFFECT!!!**
```bash
systemctl restart firewalld.service
```

```bash
[root@hostname ~]# firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: ens192
  sources:
  services: cockpit dhcpv6-client snmp ssh
  ports: 9200/tcp
  protocols:
  forward: no
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

```
