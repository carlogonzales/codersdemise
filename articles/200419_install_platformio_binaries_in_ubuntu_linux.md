
# Install PlatformIO Binaries in Ubuntu Linux

## Step 1 (Optional)
Before doing this step, make sure you already have installed Python's `distutils` . To do this, run the command below:

    sudo apt-get install python3-distutils

## Step 2
Get and run the installer:

    python3 -c "$(curl -fsSL https://raw.githubusercontent.com/platformio/platformio/develop/scripts/get-platformio.py)"

## Step 3
Create symbolic links to `/usr/local/bin`

    sudo ln -s ~/.platformio/penv/bin/platformio /usr/local/bin/platformio
    sudo ln -s ~/.platformio/penv/bin/pio /usr/local/bin/pio
    sudo ln -s ~/.platformio/penv/bin/piodebuggdb /usr/local/bin/piodebuggdb

*Note: After this, you can now use PlatformIO plugin in Clion without hiccups*

### References

1. [PlatformIO Utility Installation](https://docs.platformio.org/en/latest/core/installation.html)
---
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE0NzAyNTk0N119
-->