shazamPi Zero
========================


A mobile device to record, analyze and identify music on the go, similar to the famous "**Shazam**" app for smartphones. 

It is supposed to be a gadget, which can be taken to places, where carrying a phone with you does not really make sense (like festivals, for example), but you still want to be able to identify tracks that are being played.

The code is entirely python-based and the device is fairly easy to build. There is not even any soldering required if you have the pre-soldered **WH** model of the Pi Zero.

## Hardware
+ [Raspberry Pi Zero 2 W/WH](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/)
+ [Seeed ReSpeaker 2-Mics Pi HAT](https://wiki.seeedstudio.com/ReSpeaker_2_Mics_Pi_HAT/)
+ [Waveshare Uninterruptable Power Supply HAT (C) - 1000 mAh](https://www.waveshare.com/wiki/UPS_HAT_(C))
+ [MicroSD Card](https://www.westerndigital.com/products/memory-cards/sandisk-extreme-uhs-i-microsd#SDSQXAF-032G-GN6MA) (pretty much any will do)

<br></br>

| Close-up of the assembled device   | Red means recording   |
| :-------------: | :-------------: |
| [![](https://i.imgur.com/bUT98Rx.jpg?raw=true)](https://i.imgur.com/bUT98Rx.jpg)   |   [![](https://i.imgur.com/pAnGlDO.jpg?raw=true)](https://i.imgur.com/pAnGlDO.jpg)   |
| **Finished device inside 3D-printed case & fanny pack**   |   **Blue means ready**   |
|  [![](https://i.imgur.com/hYEt4os.png?raw=true)](https://i.imgur.com/hYEt4os.png)   |   [![](https://i.imgur.com/lvmLCtV.png?raw=true)](https://i.imgur.com/lvmLCtV.png)   |

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
2. `sudo apt-get update && sudo apt-get upgrade -y`
3. Install Seeed ReSpeaker 2-Mics Pi HAT with these [Instructions](https://wiki.seeedstudio.com/ReSpeaker_2_Mics_Pi_HAT_Raspberry/) and manage settings:
   - Adjust the left/right input db gain to an appropriate level, depending on the desired usage environment (loud music = low/no db gain needed)
   - Restore your `alsamixer` configuration automatically after reboot. How this is done is described [here](https://dev.to/luisabianca/fix-alsactl-store-that-does-not-save-alsamixer-settings-130i).
4. Install shazam library with these [Instructions](https://github.com/dotX12/ShazamIO).
5. Copy the `shazampi.py` file to your device (I used `/var/shazampi/`) and edit the script as well as your folder structure:
   - Create directories for new recordings, old recording and logs in your shazampi folder.
   - Edit global settings at the top of `shazampi.py` to your needs.
   - Make sure to edit permissions of your newly created files and folders, so the script can read, write and execute adequately without printing errors (`sudo chmod 777 -R /<insertyourshazampifolderhere>/` will do).
6. Copy the `apa102.py` library for the LED control of the ReSpeaker HAT into the same directory as your `shazampi.py` file. 
7. Reduce power consumption of your device with these [Instructions](https://www.cnx-software.com/2021/12/09/raspberry-pi-zero-2-w-power-consumption/):
   - Disable HDMI input/output
   - Disable bluetooth
   - Disable Pi board LED
   - Throttle CPU
8. Make `shazampi.py` autostart on bootup. If you do not know how, take a look [here](https://www.dexterindustries.com/howto/run-a-program-on-your-raspberry-pi-at-startup/).


## Case
The 3D-printed case for this device, which was integrated into a fanny pack (as you can see on the pictures), was created by a friend of mine. As soon as he uploads the model to Thingiverse, I will link it here.
