# Juniper
My collection of Juniper stuff that I commonly forget.

## Default Configuration
```
[edit]
user@switch# load factory-default
[edit]
user@switch# delete system commit factory-settings
[edit]
user@switch# commit
```

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
- `set interfaces vlan unit 30 family inet address 10.30.30.254/24`
- `set vlans v30-Engineering l3-interface vlan.30`


## Switchport: Access
```
set interfaces [interface] unit 0 family ethernet-switching port-mode access
set interfaces [interface] unit 0 family ethernet-switching vlan members [vlan-name]
```
**Example:**
- `set interfaces ge-0/0/47 description "Access: Engineering Desk-002"`
- `set interfaces ge-0/0/47 unit 0 family ethernet-switching port-mode access`
- `set interfaces ge-0/0/47 unit 0 family ethernet-switching vlan members v30-Engineering`

## Switchport: Trunk
```
set interfaces [interface] unit 0 family ethernet-switching port-mode trunk
set interfaces [interface] unit 0 family ethernet-switching vlan members [vlan-name]
```
**Example:**
- `set interfaces ge-0/0/1 description "Trunk: To Engineering Dept."`
- `set interfaces ge-0/0/1 unit 0 family ethernet-switching port-mode trunk`
- `set interfaces ge-0/0/1 unit 0 family ethernet-switching vlan members v30-Engineering`


## Interface Range
```
set interfaces interface-range [range-name] member-range [start-int] to [end-int]
```
**Example:**
- `set interfaces interface-range v30-Eng-Dept member-range ge-0/0/12 to ge-0/0/46`
- `set interfaces interface-range v30-Eng-Dept description "Access: Engineering Department"`
- `set interfaces interface-range v30-Eng-Dep unit 0 family ethernet-switching port-mode access`
- `set interfaces interface-range v30-Eng-Dep unit 0 family ethernet-switching vlan members v30-Engineering`


## Static Route
```
set routing-options static route [prefix/mask] next-hop [nh-address]
```
**Example:** `set routing-options static route 0.0.0.0/0 next-hop 10.30.30.1`


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

