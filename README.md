shazamPi
========================


A mobile device to record, analyze and identify music on the go, similar to the famous "**Shazam**" app for smartphones. 

It is supposed to be a gadget, which can be taken to places, where carrying a phone with you does not really make sense (like festivals, for example), but you still want to be able to identify tracks that are being played.

The code is entirely python-based and the device is fairly easy to build.

## Hardware
+ [Raspberry Pi Zero 2](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/)
+ [Seeed ReSpeaker 2-Mics Pi HAT](https://wiki.seeedstudio.com/ReSpeaker_2_Mics_Pi_HAT/)
+ [Waveshare Uninterruptable Power Supply HAT (C) - 1000 mAh](https://www.waveshare.com/wiki/UPS_HAT_(C))

<br></br>

| Close-up of the assembled device   | Red means recording   |
| ------------- | -------------|
| [![](https://i.imgur.com/bUT98Rx.jpg?raw=true)](https://i.imgur.com/bUT98Rx.jpg)   |   [![](https://i.imgur.com/pAnGlDO.jpg?raw=true)](https://i.imgur.com/pAnGlDO.jpg)   |

<br></br>

## Functionality

1. On **booting up** the device by switching on the power supply:
   + Power-saving measures are activated.
   + The shazampi.py script is started. 
   + Once everything is operational, a blue LED on the ReSpeaker board lights up, signaling the device is _'ready to be used'_.

2. On **pushing the button** on the ReSpeaker board, the device checks for an internet connection.
   + If there is no internet connection (= the user is away from home):
      - An audio clip is recorded while a red LED illuminates (as seen on the picture above). 
      - After recording, the new file is stored on the microSD card.
      - Once finished, the device reverts back to the _'ready to be used'_ status (blue LED).
   + If there is an internet connection (= the user is home):
      - All previously recorded clips are analyzed for artist and track name data, while green LEDs illuminate.
      - All analysis results are stored in a log file and sent via eMail. 
      - All analyzed clips are moved to a seperate directory on the microSD card, so they won't be analyzed a second time. 
      - Once finished, the devices reverts back to the _'ready to be used'_ status (blue LED).

## Setup
1. Flash [Pi OS](https://www.raspberrypi.com/software/) onto the microSD card (SSH enabled), assemble the hardware and make the device connect to your WiFi.
2. `sudo apt-get update -y && sudo apt-get upgrade -y`
3. Install Seeed ReSpeaker 2-Mics Pi HAT with these [Instructions](https://wiki.seeedstudio.com/ReSpeaker_2_Mics_Pi_HAT_Raspberry/) and manage settings:
   - Adjust the left/right input db gain to an appropriate level, depending on the desired usage environment (loud music = low/no db gain needed)
   - Restore your `alsamixer` configuration automatically after reboot. How this is done is described [here](https://dev.to/luisabianca/fix-alsactl-store-that-does-not-save-alsamixer-settings-130i).
4. Install shazam library with these [Instructions](https://github.com/dotX12/ShazamIO).
5. Reduce power consumption of your device with these [Instructions](https://www.cnx-software.com/2021/12/09/raspberry-pi-zero-2-w-power-consumption/):
   - Disable HDMI input/output
   - Disable bluetooth
   - Disable Pi board LED
   - Throttle CPU
6. Copy the `shazampi.py` file to your device and edit the script as well as your folder structure:
   - Create directories for new recordings, old recording and logs
   - Edit global settings at the top of `shazampi.py` to your needs
   - Make sure to edit permissions of files/folders, so the script can read, write and execute adequately (`sudo chmod 777 -R` your shazampi folder)
   - Make the `shazampi.py` autostart on bootup

## Case
A 3D-printed case is in the works and will be linked here in the future.
