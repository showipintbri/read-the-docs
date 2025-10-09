# Juniper
My collection of Juniper stuff that I commonly forget.

## Default Configuration
```
switch# load factory-default
switch# delete system commit
switch# commit
```
**NOTE:** You might need to set a `root-authentication` before issuing the final commit.

**Reference:** 

- [https://www.juniper.net/documentation/us/en/software/junos/cli/topics/topic-map/junos-factory-default.html](https://www.juniper.net/documentation/us/en/software/junos/cli/topics/topic-map/junos-factory-default.html)


## Create VLAN
```
set vlans [name] vlan-id [##]
```
**Example:** `set vlans v30-Engineering vlan-id 30`


## Create VLAN Interface (L3)
```
set interfaces vlan unit [##] family inet address [address/mask]]
set vlans [name] l3-interface vlan.[##]
```
**Example:** 
```
set interfaces vlan unit 30 family inet address 10.30.30.254/24
set vlans v30-Engineering l3-interface vlan.30
```


## Switchport: Access
```
set interfaces [interface] unit 0 family ethernet-switching port-mode access
set interfaces [interface] unit 0 family ethernet-switching vlan members [vlan-name]
```
**Example:**
```
set interfaces ge-0/0/47 description "Access: Engineering Desk-002"
set interfaces ge-0/0/47 unit 0 family ethernet-switching port-mode access
set interfaces ge-0/0/47 unit 0 family ethernet-switching vlan members v30-Engineering
```

## Switchport: Trunk
```
set interfaces [interface] unit 0 family ethernet-switching port-mode trunk
set interfaces [interface] unit 0 family ethernet-switching vlan members [vlan-name]
```
**Example:**
```
set interfaces ge-0/0/1 description "Trunk: To Engineering Dept."
set interfaces ge-0/0/1 unit 0 family ethernet-switching port-mode trunk
set interfaces ge-0/0/1 unit 0 family ethernet-switching vlan members v30-Engineering
```

## Interface Range
```
set interfaces interface-range [range-name] member-range [start-int] to [end-int]
```
**Example:**
```
set interfaces interface-range v30-Eng-Dept member-range ge-0/0/12 to ge-0/0/46`
set interfaces interface-range v30-Eng-Dept description "Access: Engineering Department"`
set interfaces interface-range v30-Eng-Dep unit 0 family ethernet-switching port-mode access`
set interfaces interface-range v30-Eng-Dep unit 0 family ethernet-switching vlan members v30-Engineering`
```

## Static Route
```
set routing-options static route [prefix/mask] next-hop [nh-address]
```
**Example:** 
```
set routing-options static route 0.0.0.0/0 next-hop 10.30.30.1`
```

## Change `root` Password
```
set system root-authentication plain-text-password
New password: [input-password] <enter>
Retype new password: [input-password] <enter>
```


## New User
```
set system login user admin class super-user
set system login user admin authentication plain-text-password <enter>
New password: [input-password] <enter>
Retype new password: [input-password] <enter>
```


## SSH Access
```
set system services ssh
```

## Reboot/Restart
```
request system reboot
```

## Shutdown
```
request system power-off
or (? Whats the difference ?)
request system halt
```

## AAA - RADIUS Authentication
```
# This is required for the RADIUS users to assume this profile
set system login user remote class super-user 

# 'local' doesn't need to be specified. If it can't reach RADIUS it will fall back to local users
set system services ssh authentication-order radius 

set system radius-server [SERVER_IP] secret [clear_text_key]
set system radius-server [SERVER_IP] timeout 15
set system radius-server [SERVER_IP] source-address [your_src_ip]

set system radius-options enhanced-accounting
```
  
I also, like to add: `set system services ssh root-login deny` to prevent **root** user from logging in remotely, forcing this to be a console only credential, incase an on-site rescue is needed.

## IKEv2 IPSEC Site-to-Site Tunnel
```
# -------------------------
# IKE Phase 1 (IKEv2)
# -------------------------
set security ike proposal IKEV2-PROP authentication-method pre-shared-keys
set security ike proposal IKEV2-PROP dh-group group14
set security ike proposal IKEV2-PROP encryption-algorithm aes-256-gcm
set security ike proposal IKEV2-PROP lifetime-seconds 28800
set security ike proposal IKEV2-PROP authentication-algorithm hmac-sha-256-128

set security ike policy IKEV2-POL mode main
set security ike policy IKEV2-POL proposals IKEV2-PROP
set security ike policy IKEV2-POL pre-shared-key ascii-text "SuperSecret123"

set security ike gateway GW-TO-SRXB ike-policy IKEV2-POL
set security ike gateway GW-TO-SRXB address 203.0.113.2
set security ike gateway GW-TO-SRXB external-interface ge-0/0/0.0
set security ike gateway GW-TO-SRXB version v2-only
set security ike gateway GW-TO-SRXB local-identity inet 198.51.100.1
set security ike gateway GW-TO-SRXB remote-identity inet 203.0.113.2
set security ike gateway GW-TO-SRXB dead-peer-detection interval 10 retry 3

# -------------------------
# IPsec Phase 2
# -------------------------
set security ipsec proposal IPSEC-PROP protocol esp
set security ipsec proposal IPSEC-PROP authentication-algorithm hmac-sha-256-128
set security ipsec proposal IPSEC-PROP encryption-algorithm aes-256-gcm
set security ipsec proposal IPSEC-PROP lifetime-seconds 3600

set security ipsec policy IPSEC-POL perfect-forward-secrecy keys group14
set security ipsec policy IPSEC-POL proposals IPSEC-PROP

# -------------------------
# VPN Binding
# -------------------------
set security ipsec vpn VPN-TO-SRXB ike gateway GW-TO-SRXB
set security ipsec vpn VPN-TO-SRXB ike ipsec-policy IPSEC-POL
set security ipsec vpn VPN-TO-SRXB bind-interface st0.0
set security ipsec vpn VPN-TO-SRXB vpn-monitor optimized
set security ipsec vpn VPN-TO-SRXB establish-tunnels immediately

# -------------------------
# st0 interface
# -------------------------
set interfaces st0 unit 0 family inet address 169.254.10.1/30
set security zones security-zone vpn-zone interfaces st0.0

# -------------------------
# Security zones & policies
# -------------------------
set security zones security-zone trust interfaces ge-0/0/1.0
set security zones security-zone untrust interfaces ge-0/0/0.0

set security policies from-zone trust to-zone vpn-zone policy trust-to-vpn match source-address any destination-address any application any
set security policies from-zone trust to-zone vpn-zone policy trust-to-vpn then permit

set security policies from-zone vpn-zone to-zone trust policy vpn-to-trust match source-address any destination-address any application any
set security policies from-zone vpn-zone to-zone trust policy vpn-to-trust then permit

# -------------------------
# Routing
# -------------------------
set routing-options static route 10.2.2.0/24 next-hop st0.0

```

