# Display the List of Block Devices in Linux (e.g. Hard Disk, CD-ROM, Flash Drive)

When you want to find out the list of block devices in your computer, you can use `lsblk`.

### Sample Usage

#### List block devices

```bash
lsblk
```

#### List all block devices

```bash
lsblk
```

#### List all SCSI devices

_Please take note of the capital 'S'_

```bash
lsblk -S
```

#### Specifically list column

You can get all the available columns by running `lsblk -h`.

```bash
lsblk -o NAME,TYPE,MODEL
```

#### References

- [What is a block device](http://unix.stackexchange.com/questions/259193/what-is-a-block-device#answer-259197)
- [Using the lsblk Command](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-sysinfo-filesystems.html) 
- [LSBLK Man Page](http://man7.org/linux/man-pages/man8/lsblk.8.html)
