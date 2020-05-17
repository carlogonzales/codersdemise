
# Setting Timezone in Linux

There are two ways of changing the system timezone in Linux, either you use `timedatectl` or changing the `/etc/localtime` symbolic link and pointing it to you chosen timezone at `/usr/zoneinfo/`

## Solution: Using `timedatectl`

### Step 1
Check the available zones first, which in turn will be provided when we set the timezone you're gonna use for your system.

    timedatectl list-timezones
 
This will show you all available timezone you can set. You can also use `/usr/zoneinfo` for the list but this one's a lot easier than checking each folder for approriate zones.

### Step 2
Now let's set your timezone. In my case I'll use `Asia/Manila` as my timezone.

    timedatectl set-timezone Asia/Manila

### Step 3
Once set, you can now verify if your timezone is currently used by your system. You can run either `date` or `timedatectl`. Running just `timedatectl` defaults to `timedatectl status`, so there's no need to do it the long way.

## Solution 2: Change Symlink of `/etc/localtime`

If you'll check were the `/etc/localtime` is being point to, you'll see it's at `/usr/share/zoneinfo/[TIME_ZONE]`

    readlink -f /etc/localtime

### Step 1
Root holds owner of the file, and has a 777 permission. So first let's remove the symlink

    sudo rm -rf /etc/localtime

### Step 2
Doing the long way to search and confirm for your timezone, and look for it at `/usr/share/zoneinfo`

You can do a recursive search to make it easier

    ls -R /usr/share/zoneinfo

### Step 3
Once you know the timezone to set. Now create a symlink:

    sudo ln -s /usr/share/zoneinfo/Asia/Manila /etc/localtime

### Step 4
Verify if your system is now using your selected timezone:

    date

### REFERENCES

 1. [`timedatectl` Manual](http://man7.org/linux/man-pages/man1/timedatectl.1.html)
 2. [`/etc/localtime` Manual](https://www.freedesktop.org/software/systemd/man/localtime.html)
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI2NzQyMzk3MF19
-->