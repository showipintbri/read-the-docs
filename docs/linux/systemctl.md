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

### Show/List All Services
```bash
systemctl list-units --all *.service
```


### Show Details about a Single Service
```bash
systemctl status [service_name]
```


### **References:**
