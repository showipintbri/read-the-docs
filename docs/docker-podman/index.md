# Docker/Podman
This page is dedicated to all things containers :)

I use docker and podman interchangeably.

## Run a Container
- `-i`: interactive
- `-t`: terminal
- `-v [src]:[dst]`: mounting a storage volume

**Example:** Starting my Zeek(bro) container

```bash
sudo docker run -it -v `pwd`:/pcap broplatform/bro:4.2.0 /bin/bash
```

## List Running Containers
```bash
podman container list
```

## Get Container Details
```bash
podman inspect [container_name]
```

**References:**

- Official Podman Documentation: [https://docs.podman.io/en/latest/index.html](https://docs.podman.io/en/latest/index.html)