# Enable SSH on Raspbian OS without Desktop UI (Headless)

## Step 1
Whichever storage you're using for your Raspbian OS either SD Card, SSD, or HDD; remove it from your board and mount the storage to your computer. Look for the _**boot**_ partition and push an empty file with a filename **ssh**

## Step 2
Put your storage back in the board and start your Raspberry Pi.

## Step 3
Connect to your Raspberry Pi with SSH
`ssh [USERNAME]@[YOUR PI IP OR DOMAIN HERE]`

*Note: The default username and password for Raspbian is `pi` for username and `raspberry` as password.*

### REFERENCES
[Raspberry Pi Documentation: SSH Remote Access](https://www.raspberrypi.org/documentation/remote-access/ssh/)
[Raspberry Pi Documentation: Linux User Management](https://www.raspberrypi.org/documentation/linux/usage/users.md)
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODE4NDk5ODg4LC00MDY0ODE1MThdfQ==
-->