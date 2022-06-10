# systemctl


```bash
systemctl start [unit]
systemctl status [unit]
systemctl stop [unit]
systemctl reload [unit]
systemctl restart [unit]

systemctl enable [unit]
systemctl disable [unit]
systemctl list-units [unit]
systemctl list-sockets [unit]
systemctl list-unit-files [pattern]
```

## Example *.service files
Service files are typically found in: `/etc/systemd/system/[service_name].service`
Service can only have 1 `ExecStart` statement.

```bash
[Unit]
Description=cloudflared
After=network.target

[Service]
TimeoutStartSec=0
Type=notify
ExecStart=/usr/bin/cloudflared --no-autoupdate tunnel run --token x0x0x0x0x0x0x0x0x0x
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```


### Show/List All Services
```bash
systemctl list-units --all *.service
```


### Show Details about a Single Service
```bash
systemctl status [service_name]
```


### **References:**
