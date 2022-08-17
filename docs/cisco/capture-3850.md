# Packet Capture: Cisco 3850
- License: Requires IPBASE or IPSERVICES.
- Capture filters are not supported.
- Layer 2 and Layer 3 EtherChannels are not supported.
- MAC Access Control List (ACL) is only used for non-IP packets such as ARP. It is not supported on a Layer 3 port or Switch Virtual Interface (SVI).
- During a Wireshark packet capture, hardware forwarding happens concurrently.
- Switch CPU generated packets can be captured and must use the control-plane as the source interface.
- It is not possible to capture rewrite information. Egress captures do not show and changes to the packet performed by the Cisco Catalyst 3850 Series Switch.

## Configure
```
monitor capture [name] interface [interface name: Gi0/0/1] [direction:in|out|both]
monitor capture [name] match ipv4 [source ip/xx] [dest ip/xx]
monitor capture [name] match ipv4 any any
monitor capture [name] file location [location: flash:mypcap.pcap]
monitor capture [name] buffer size 100     # This is in Megabytes
```

## Start the Capture
```
monitor capture [name] start
```

## Show Capture Status
```
show monitor capture [name]
```

## View Capture (ASCII Only)
```
show monitor capture file flash:[name].pcap
```

## View Capture (Embedded `tshark`)
```
show monitor capture file flash:[name].pcap detailed
```

## View Capture (hex dump)
```
show monitor capture [name] buffer dump
```

## Stop the Capture
```
monitor capture [name] start
```

## Export PCAP to Workstation
```
monitor capture [name] export tftp://[workstation_ip]/[name].pcap
```

## Verify Capture Configs
```
show monitor capture [name] parameter
```


## Reference:
- [https://www.cisco.com/c/en/us/support/docs/switches/catalyst-3850-series-switches/117639-configure-wireshark-00.html](https://www.cisco.com/c/en/us/support/docs/switches/catalyst-3850-series-switches/117639-configure-wireshark-00.html)
