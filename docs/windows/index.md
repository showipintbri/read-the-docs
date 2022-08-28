# Windows

## For Loop w/ Range of Numbers
Step from 1 to 450 in steps of 1.
```
FOR /L %i IN (1,1,450) DO curl http://hostname.fqdn/%i -o NUL: -s && TIMEOUT /T 1 /NOBREAK
```

## WSL2 Error
To fix the error:
```
Logon failure: the user has not been granted the requested logon type at this computer.                                                                                                       
Press any key to continue... 
```

As Administrator run in Powershell:
```
Get-Service vmcompute | Restart-Service
```

Then start your WSL2 VM again.

## WSL2 Folder Location
`\\wsl$\[wsl_vm-name]\home` maps to the `/home/` folder inside the VM.
