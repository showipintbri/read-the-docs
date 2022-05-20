# TCPReplay

## Basic Usage



# Troubleshooting

## Unsupported DLT Type
Using the command **`tcpreplay -i [interface] [filename.pcap]`** to replay a *.pcap and getting alot of Warnings on the screen:
```bash
Warning: Unable to process unsupported DLT Type: Ethernet (0x1)
Warning: Unable to process unsupported DLT Type: Ethernet (0x1)
Warning: Unable to process unsupported DLT Type: Ethernet (0x1)
Warning: Unable to process unsupported DLT Type: Ethernet (0x1)
Warning: Unable to process unsupported DLT Type: Ethernet (0x1)
Warning: Unable to process unsupported DLT Type: Ethernet (0x1)
Warning: Unable to process unsupported DLT Type: Ethernet (0x1)
...etc...
```

While the file I was using openned fine in Wireshark and parsed perfected using tcpdump, it was generating warnings in TCPReplay and I wanted to understand why so I could more reliably replay predicatable traffic.

The frames and packets it was flagging with a Warning we all STP, RSTP, ARP and EIGRP. This was a Full-PCAP from a CTF event and contained all protocols. Filtering out those protocols (sans EIGRP IIRC) was the solution.

### Solution
Preparse the PCAPs excluding all non-IP traffic. To do this I used tcpdump:
```bash
tcpdump -r [in-filename] -w [out-filename] 'ip'
```

Tcpdump will read a *.pcap file, filter all traffic leaving only IP traffic and writing it to a new file. Now, using TCPReplay I could replay the new files without issue or Warning.

### Reference
- [https://sourceforge.net/p/tcpreplay/mailman/tcpreplay-users/?viewmonth=202204&style=flat](https://sourceforge.net/p/tcpreplay/mailman/tcpreplay-users/?viewmonth=202204&style=flat)

# Links/References
- **Homepage:** [http://tcpreplay.appneta.com/](http://tcpreplay.appneta.com/)
- **GitHub:** [https://github.com/appneta/tcpreplay](https://github.com/appneta/tcpreplay)