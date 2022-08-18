# Packet Capture Using `netsh`

**NOTE:** Requires elevated privileges.
```
C:\Users\tony.e>netsh trace start capture=yes tracefile=C:\Users\tony.e\Desktop\netsh.etl
The requested operation requires elevation (Run as administrator).
```


## Start Capture
```
netsh trace start capture=yes tracefile=C:\Users\tony.e\Desktop\netsh.etl
```

**Example:**
```
C:\WINDOWS\system32>netsh trace start capture=yes tracefile=C:\Users\tony.e\Desktop\netsh.etl

Trace configuration:
-------------------------------------------------------------------
Status:             Running
Trace File:         C:\Users\tony.e\Desktop\netsh.etl
Append:             Off
Circular:           On
Max Size:           512 MB
Report:             Off
```

## Stop Capture
```
netsh trace stop
```

**Example:**
```
C:\WINDOWS\system32>netsh trace stop
Merging traces ... done
Generating data collection ... done
The trace file and additional troubleshooting information have been compiled as "C:\Users\tony.e\Desktop\netsh.cab".
File location = C:\Users\tony.e\Desktop\netsh.etl
Tracing session was successfully stopped.
```

## Convert \*.etl to \*.pcap
Download CLI conversion utility: [https://github.com/microsoft/etl2pcapng/releases](https://github.com/microsoft/etl2pcapng/releases)

Run utility via Windows Command Prompt:
```
etl2pcapng <infile> <outfile>
```

**Example:**
```
C:\Users\tony.e\Downloads\etl2pcapng\x64>etl2pcapng.exe C:\Users\tony.e\Desktop\netsh.etl C:\Users\tony.e\Desktop\netsh.pcap
IF: medium=eth                  ID=0    IfIndex=3       VlanID=0
IF: medium=wifi                 ID=1    IfIndex=4
IF: medium=eth                  ID=2    IfIndex=53      VlanID=0
Converted 1024 frames
```

