# Cisco Forensics
Collection of tools, links, techniques and resources to perform forensics on a Cisco Device.

## Core Dump

**You'll Need:**
- Console Cable
- Network Cable
- TFTP Server / FTP Server Software \([https://pjo2.github.io/tftpd64/]\)(https://pjo2.github.io/tftpd64/)

Using a laptop or computer connect to the device with both a **console cable** *and* a regular ethernet cable. You will issue commands and capture logs from the console while the network cable will be used to off-load the core dumps and memory dumps off the device and onto a TFTP server.

### Step 1: Capture The Core Dump
Log into the device via the console cable and issue the `write core [ip.add.re.ss]` command using the IP of your workstation as the destination device.

Getting a Core Dump from a Cisco3560CX took: [##]hours and [##] minutes

```
Switch>
Switch> enable
Switch#
Switch# write core xx.xx.xx.1
Base name of core files to write [Switch-core]?
writing uncompressed tftp://xx.xx.xx.1/Switch-corecoredump
!!!!!!!!!!!!!!!!!!!! [...OMITTED...]

```



**References:** 

- Creating Core Dumps: [https://www.cisco.com/c/en/us/support/docs/ios-nx-os-software/ios-software-releases-122-mainline/12687-appA.html](https://www.cisco.com/c/en/us/support/docs/ios-nx-os-software/ios-software-releases-122-mainline/12687-appA.html)
- Didier Stevens: NAFT - [https://blog.didierstevens.com/programs/network-appliance-forensic-toolkit/](https://blog.didierstevens.com/programs/network-appliance-forensic-toolkit/)
- SANS: Cisco Router Forensics - [https://www.sans.org/blog/cisco-router-forensics/](https://www.sans.org/blog/cisco-router-forensics/)