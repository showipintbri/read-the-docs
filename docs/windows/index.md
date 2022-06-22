# Windows

## For Loop w/ Range of Numbers
Step from 1 to 450 in steps of 1.
```
FOR /L %i IN (1,1,450) DO curl http://hostname.fqdn/%i -o NUL: -s && TIMEOUT /T 1 /NOBREAK
```

