# Packet Captures: ASA

## Start a Capture
```
enable
capture [name] interface [int_name] match ip [src_host] [src_subnet_mask] [dst_host] [dst_subnet_mask]

Example:
capture testcapture interface inside match ip 192.168.100.99 255.255.255.255 8.8.8.8 255.255.255.255
```

## Stop a Capture
```
no capture [name] interface [int_name]
```

## Show the Captured Packets
Only shows ASCII output.
```
show capture [name]
```

## Clear the Capture Buffer
This removes the captured data but keeps the 'capture configs' in place incase you need to re-run them using the same name.
```
clear capture [name]

clear capture /all #Clears the buffers for all captures
```

## Download the Capture

From a workstation navigate to: `https://<ip_of_asa>/admin/capture/<capture_name>/pcap` or from the ASA:
```
copy /pcap capture:<capture-name> tftp://<server-ip-address>
```
