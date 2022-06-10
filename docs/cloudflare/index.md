# Cloudflare Zero-Trust

## cloudflared
Cloudflared (cloud-flare-dee) is a light weight multi-purpose daemon.

It can be invoked manually or through scripting/service files to manage tunnels. You can run many instances of cloudflared at once if needed. For example, I run one instance acting as a DNS to DNS over HTTPS proxy and another instance as a tunnel to reach the webserver on that box which is listening on localhost.

### Example cloudflared service file for DNS to DNS over HTTPS Proxy
```
[Unit]
Description=DNS over HTTPS (DoH) proxy client
Wants=network-online.target nss-lookup.target
Before=nss-lookup.target

[Service]
AmbientCapabilities=CAP_NET_BIND_SERVICE
CapabilityBoundingSet=CAP_NET_BIND_SERVICE
TimeoutStartSec=0
Type=notify
ExecStart=/usr/bin/cloudflared --no-autoupdate proxy-dns --address "localhost" --port 5053 --upstream "https://x0x0x0x0x.cloudflare-gateway.com/dns-query" --bootstrap "https://1.1.1.1/dns-query", "https://1.0.0.1/dns-query"
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```
