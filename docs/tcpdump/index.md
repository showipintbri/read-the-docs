# TCPdump

## Filters
Filters are written in BPF (Berkley Packet Filter).

### CDP, VTP, PAgP, DTP, RSTP
```
'ether dst 01:00:0c:cc:cc:cd'
```

### EIGRP
```
'ether dst 01:00:5e:00:00:0a'
'host 224.0.0.10'
```

### Spanning-Tree
```
'stp'
```

### VLANs / 802.1q
```
vlan
```

# Troubleshooting

## Continuous capture failing to write to new file
```bash
sudo tcpdump -i ens160 -C 100 -w web_traffic.pcap
```

When tcpdump writes continuous files it appends a number to the file name.

If you wanted to continuously capture traffic and write it to disks in approximately 100MB files using the base filename `full_capture.pcap`. Once the first ~100MB is written, tcpdump will create a new file with the name: `full_capture.pcap1`. This will continue, increasing the numeric value appended to the end.

The conflict with the apparmor policy happens because apparmor will only allow tcpdump to write files with extensions: `.pcap` or `.cap` (in any combination of upper- and lowercase).

The problem is this section of the apparmor policy: **`/etc/apparmor.d/usr.bin.tcpdump`**

```bash title="/etc/apparmor.d/usr.bin.tcpdump"
  # for -r, -F and -w
  /**.[pP][cC][aA][pP] rw,
  /**.[cC][aA][pP] rw,
```

We can modify the policy to allow the continuous writing of files by adding the below lines or modifying the existing lines from the config section above:

```bash title="/etc/apparmor.d/usr.bin.tcpdump"
  # for -r, -F and -w
  /**.[pP][cC][aA][pP][0-9]*  rw,
  /**.[cC][aA][pP][0-9]*  rw,
```

### Solution
My solution isn't to disable apparmor, but instead to modify the apparmor policy so tcpdump can do what it needs and apparmor can continue to do what it does.

### Commands
1. Check the apparmor status: **`sudo aa-status`**
2. Check the logs: **`cat /var/log/syslog | grep -i denied`**
```bash
Apr 26 20:58:00 cnmfpcap kernel: [ 2169.229999] audit: type=1400 audit(1651006680.331:31): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web-traffic" pid=1905 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=109 ouid=109
Apr 26 20:58:54 cnmfpcap kernel: [ 2223.096608] audit: type=1400 audit(1651006734.198:32): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web-traffic" pid=1923 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=109 ouid=109
Apr 26 21:00:02 cnmfpcap kernel: [ 2291.315473] audit: type=1400 audit(1651006802.421:33): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web-traffic" pid=1933 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=109 ouid=109
Apr 26 21:01:55 cnmfpcap kernel: [ 2404.315427] audit: type=1400 audit(1651006915.426:34): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web-traffic" pid=1953 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=1000 ouid=1000
Apr 26 21:02:29 cnmfpcap kernel: [ 2438.316675] audit: type=1400 audit(1651006949.432:35): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web_traffic" pid=1960 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=1000 ouid=1000
Apr 26 21:02:40 cnmfpcap kernel: [ 2448.918463] audit: type=1400 audit(1651006960.032:36): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web_traffic" pid=1963 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=0 ouid=0
Apr 26 21:04:15 cnmfpcap kernel: [ 2544.397543] audit: type=1400 audit(1651007055.516:37): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web_traffic" pid=1996 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=109 ouid=109
Apr 26 21:04:23 cnmfpcap kernel: [ 2552.557682] audit: type=1400 audit(1651007063.676:38): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web_traffic" pid=1999 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=1000 ouid=1000
Apr 26 21:05:29 cnmfpcap kernel: [ 2618.028858] audit: type=1400 audit(1651007129.151:39): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web_traffic" pid=2018 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=109 ouid=109
Apr 26 21:05:35 cnmfpcap kernel: [ 2624.785708] audit: type=1400 audit(1651007135.907:40): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web_traffic" pid=2021 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=1000 ouid=1000
Apr 26 21:06:04 cnmfpcap kernel: [ 2653.751938] audit: type=1400 audit(1651007164.877:41): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web_traffic" pid=2025 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=109 ouid=109
Apr 26 22:31:05 cnmfpcap kernel: [ 7753.978615] audit: type=1400 audit(1651012265.324:42): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web_traffic.pcap1" pid=2042 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=109 ouid=109
Apr 27 09:52:34 cnmfpcap kernel: [48641.533480] audit: type=1400 audit(1651053154.580:43): apparmor="DENIED" operation="mknod" profile="tcpdump" name="/mnt/pcap/web_traffic.pcap1" pid=3078 comm="tcpdump" requested_mask="c" denied_mask="c" fsuid=109 ouid=109
```
3. Disable the tcpdump apparmor policy: 
**`sudo apparmor_parser -R /etc/apparmor.d/usr.bin.tcpdump`**
4. Modify the apparmor policy: **`/etc/apparmor.d/usr.bin.tcpdump`**
```bash
  # for -r, -F and -w
  /**.[pP][cC][aA][pP][0-9]*  rw,
  /**.[cC][aA][pP][0-9]*  rw,
```
5. Test/Verify tcpdump can write/create new files. 
(**NOTE:** The policy is not activated yet. We just want to make sure it works while it's still off)
6. Re-enable the tcpdump apparmor policy: 
**`sudo apparmor_parser /etc/apparmor.d/usr.bin.tcpdump`**
7. Test/Verify tcpdump can write/create new files past the initial base filename given when the command was invoked.

### Reference
- [https://www.xmodulo.com/disable-particular-apparmor-profile-ubuntu.html](https://www.xmodulo.com/disable-particular-apparmor-profile-ubuntu.html)