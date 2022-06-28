# SELinux
Security-Enhanced Linux

```bash
[root@hostname ~]# getenforce
Enforcing
[root@hostname ~]# setenforce 0
[root@hostname ~]# getenforce
Permissive
[root@hostname ~]#
```

```
semanage port -a -t http_port_t -p tcp 9200
```
