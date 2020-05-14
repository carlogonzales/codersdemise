
# Raspberry Pi Camera Error: `Failed to create component 'vc.ril.camera'`

Hardware & Software Info:
- 5MP Camera Board
- Raspbian 10 (Buster)
- Python 3

When using a Python library `PiCamera` and this error below occured:

    mmal: mmal_vc_component_create: failed to create component 'vc.ril.camera' (1:ENOMEM)
    mmal: mmal_component_create_core: could not create component 'vc.ril.camera' (1)
    Traceback (most recent call last):
      File "/usr/lib/python3/dist-packages/picamera/camera.py", line 456, in _init_camera
        self._camera = mo.MMALCamera()
      File "/usr/lib/python3/dist-packages/picamera/mmalobj.py", line 2279, in __init__
        super(MMALCamera, self).__init__()
      File "/usr/lib/python3/dist-packages/picamera/mmalobj.py", line 633, in __init__
        prefix="Failed to create MMAL component %s" % self.component_type)
      File "/usr/lib/python3/dist-packages/picamera/exc.py", line 184, in mmal_check
        raise PiCameraMMALError(status, prefix)
    picamera.exc.PiCameraMMALError: Failed to create MMAL component b'vc.ril.camera': Out of memory
    
    During handling of the above exception, another exception occurred:
    
    Traceback (most recent call last):
      File "cam.py", line 4, in <module>
        camera = PiCamera()
      File "/usr/lib/python3/dist-packages/picamera/camera.py", line 431, in __init__
        self._init_camera(camera_num, stereo_mode, stereo_decimate)
      File "/usr/lib/python3/dist-packages/picamera/camera.py", line 460, in _init_camera
        "Camera is not enabled. Try running 'sudo raspi-config' "
    picamera.exc.PiCameraError: Camera is not enabled. Try running 'sudo raspi-config' and ensure that the camera has been enabled.

There are two possible issue that which can cause this error to appear.

1. Your FFC (Flexible Flat Cable) connection to your camera or your board is loose. 
2. You haven't enabled your camera yet.

## Solution: Tighten your loose FFC on your camera and board

Yes, as it says. It won't be that hard to follow right. :D 

## Solution: Enable camera access

### Step 1
Open your terminal and execute:

    sudo raspi-config

Once executed and you have provided your password, you'll be greeted by this screen:

    ┌──────────────────────────────┤ Raspberry Pi Software Configuration Tool (raspi-config) ├───────────────────────────────┐
    │                                                                                                                        │
    │                  1 Change User Password Change password for the 'pi' user                                              │
    │                  2 Network Options      Configure network settings                                                     │
    │                  3 Boot Options         Configure options for start-up                                                 │
    │                  4 Localisation Options Set up language and regional settings to match your location                   │
    │                  5 Interfacing Options  Configure connections to peripherals                                           │
    │                  6 Overclock            Configure overclocking for your Pi                                             │
    │                  7 Advanced Options     Configure advanced settings                                                    │
    │                  8 Update               Update this tool to the latest version                                         │
    │                  9 About raspi-config   Information about this configuration tool                                      │
    │                                                                                                                        │
    │                                                                                                                        │
    │                                                                                                                        │
    │                                                                                                                        │
    │                                   <Select>                                   <Finish>                                  │
    │                                                                                                                        │
    └────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘

Select `5 Interfacing Options`

### Step 2
Once you have selected `5 Interfacing Options`, this screen will show:

    ┌──────────────────────────────┤ Raspberry Pi Software Configuration Tool (raspi-config) ├───────────────────────────────┐
    │                                                                                                                        │
    │                    P1 Camera      Enable/Disable connection to the Raspberry Pi Camera                                 │
    │                    P2 SSH         Enable/Disable remote command line access to your Pi using SSH                       │
    │                    P3 VNC         Enable/Disable graphical remote access to your Pi using RealVNC                      │
    │                    P4 SPI         Enable/Disable automatic loading of SPI kernel module                                │
    │                    P5 I2C         Enable/Disable automatic loading of I2C kernel module                                │
    │                    P6 Serial      Enable/Disable shell and kernel messages on the serial connection                    │
    │                    P7 1-Wire      Enable/Disable one-wire interface                                                    │
    │                    P8 Remote GPIO Enable/Disable remote access to GPIO pins                                            │
    │                                                                                                                        │
    │                                                                                                                        │
    │                                                                                                                        │
    │                                                                                                                        │
    │                                                                                                                        │
    │                                   <Select>                                   <Back>                                    │
    │                                                                                                                        │
    └────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
Select `P1 Camera` and proceed with  the instructions of enabling your camera. After it, go back on the main menu and select `<Finish>`. You'll be prompted to restart your board. Go on and restart, then proceed to the next step to test your camera.

### Step 3
Execute the command below and see if your board can detect your camera:

    vcgencmd get_camera
You should get this output `supported=1 detected=1` if not, tighten your FFC on your cam and board.

To test if the camera is working, execute the command below:

    raspistill -v -o test.jpg

Once executed, on the same directory you're in, you should see a file named `test.jpg` open it and you should see the captured image from your cam.

### References

1. [Raspbian Docs:`vcgencmd`](https://www.raspberrypi.org/documentation/raspbian/applications/vcgencmd.md)
2. [Raspbian Docs: Camera](https://www.raspberrypi.org/documentation/configuration/camera.md)

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjE3NzQxNjk5XX0=
-->