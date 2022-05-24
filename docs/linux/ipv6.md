# IPv6

## Ubuntu: Netplan
Create a new config file. Highest one takes precendence.
```bash
touch /etc/netplan/99-ipv6.yaml

-------------------------------
network:
  ethernets:
    ens160:
      dhcp6: true
      accept-ra: true     # Host will use SLAAC to configure its address and gateway
      addresses: ['fd10::10/64'] #ULA address for my site
      nameservers:
          addresses: ['2606:4700:4700::1111'] #Cloudflare DNS
  version: 2

```
