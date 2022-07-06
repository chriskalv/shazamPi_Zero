shazamPi
========================

A device to record and analyze tracks with a Raspberry Pi Zero 2. Entirely python-based.

[![](https://i.imgur.com/pyAoYx3.jpg?raw=true)](https://i.imgur.com/pyAoYx3.jpg)


## Hardware
+ [Raspberry Pi Zero 2](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/)
+ [Waveshare Uninterruptable Power Supply HAT (C) - 1000 mAh](https://www.waveshare.com/wiki/UPS_HAT_(C))
+ [Seeed ReSpeaker 2-Mics Pi HAT](https://wiki.seeedstudio.com/ReSpeaker_2_Mics_Pi_HAT/)

## Functionality
1. After booting up, the shazamPi device shows a blue LED on the microphone board, in order to indicate that it is operational.
2. On pushing the button on the microphone board, the Pi checks whether is is connected to the internet or not.
   - Not connected: It records a 12s audio clip and stores it on the microSD card (red LED is shown)
   - Connected: It analyzes all previously recorded tracks, moves them from a 'new recordings' directory to a 'old recordings' directory, writes a log file, saves it to the device and sends it via eMail (green LED progress bar is shown).
3. After recording/analysis, the device reverts back to the "waiting for button push" status, indicated by the blue LED.

## Setup
1. Flash piOS auf microSD 
2. sudo apt-get update && sudo apt-get upgrade
3. Installiere Respeaker Karte: https://wiki.seeedstudio.com/ReSpeaker_2_Mics_Pi_HAT_Raspberry/
4. Installiere LED libraries etc.
5. Fortwährender Settings restore für den Soundkartenmixer nach reboot: https://dev.to/luisabianca/fix-alsactl-store-that-does-not-save-alsamixer-settings-130i
6. Installiere Shazam Library: https://github.com/dotX12/ShazamIO
7. shazam.py in bash autostart packen
8. Verringere pi Zero Stromverbrauch: https://www.cnx-software.com/2021/12/09/raspberry-pi-zero-2-w-power-consumption/

