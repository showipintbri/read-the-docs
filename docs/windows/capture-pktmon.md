# Packet Capture Using `pktmon`

**NOTE:** Requires elevated privileges (run Command Prompt as Administrator)
```
C:\Users\anthony.efantis>pktmon list
Failed to communicate with the PktMon driver. Access is denied.
```

## Start Capture
```
pktmon start --capture
```

**Example:**
```
C:\WINDOWS\system32>pktmon start --capture

Logger Parameters:
    Logger name:        PktMon
    Logging mode:       Circular
    Log file:           C:\WINDOWS\system32\PktMon.etl
    Max file size:      512 MB
    Memory used:        256 MB

Collected Data:
    Packet counters, packet capture

Capture Type:
    All packets

Monitored Components:
    All

Packet Filters:
     # Name     MAC Address       EtherType Protocol
     - ----     -----------       --------- --------
     1 SenseNdr                             UDP
     2 SenseNdr 01-00-0C-CC-CC-CC
     3 SenseNdr                   ARP
     4 SenseNdr                             TCP
     5 SenseNdr                   LLDP
     6 SenseNdr                             ICMP
     7 SenseNdr                             ICMPv6
     8 SenseNdr                             0x2
     9 SenseNdr                             0x32
    10 SenseNdr                             0x33
    11 SenseNdr                             0x2f
    12 SenseNdr                             0x73
    13 SenseNdr                             FC
```

## Stop Capture
```
pktmon stop
```

**Example:**
```
C:\WINDOWS\system32>pktmon stop
Flushing logs...
Merging metadata...
Log file: C:\WINDOWS\system32\PktMon.etl (No events lost)
```

## Convert \*.etl to \*.pcap
```
pktmon etl2pcap <filename.etl> --out <filename.pcap>
```

**Example:**
```
C:\WINDOWS\system32>pktmon etl2pcap PktMon.etl --out pktmon.pcap
Processing...

Packets total:       8106
Packet drop count:   0
Packets formatted:   8106
Formatted file:      pktmon.pcap
```

## Optional: Choose an Interface to capture from
```
pktmon list
```

**Example:**
```
C:\WINDOWS\system32>pktmon list

Network Adapters:
   Id MAC Address       Name
   -- -----------       ----
  595 38-00-20-09-00-2A Dell Giga Ethernet
   10 D0-00-10-07-00-8A Intel(R) Wi-Fi 6 AX201 160MHz
   11 00-FF-70-07-00-8A TAP-Windows Adapter V9
  241 00-00-50-01-00-41 Virtual Machine
  121 00-00-50-0E-00-EF vEthernet (WSL)
```

### Use the Interface ID in the `start` command
```
pktmon start --capture -c 10
```
