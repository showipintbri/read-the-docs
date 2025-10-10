# Cisco Catalyst 9500

## Firmware Upgrade

### Check the existing install method:
```
show version | i System image
```

If output show's filename ending in *.bin == **BUNDLE**
If output show's filename "packages.conf" == **INSTALL**

```
show install summary
```

If output show's details == **INSTALL**
If output show's "Bundle" == **BUNDLE**

### Verify
Verify the `boot` commands in the config are correct:

  - `packages.conf` == INSTALL
  - `*.bin` == BUNDLE

If using INSTALL do not change or modify the `boot` commands or the `packages.conf` file.


### Remove unused firmware files
This makes more room available on the storage of the device as firmware images are quite large.

```
install remove inactive
```

### Copy firmware file to device
Use, `scp` or any other available method.


### Verify the firmware hashes

```
verify /md5 flash:<filename.bin>
```

Ensure the hash of the file and the reported hashes match.

### Install
```
install add file flash:<filename.bin> activate commit
```
This command will:
  - Unpack the `*.bin` image
  - Update the `packages.conf` file
  - Commit the new packages

### After reboot, Verify
Use the same verification commands in step 1: `show version`, `show install summary`