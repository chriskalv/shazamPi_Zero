# shazamPi
A python-based implementation of recording capability and Shazam track analysis on a Raspberry Pi Zero 2.


Functionality:

1. After booting up, the shazamPi device shows a blue LED on the microphone board, in order to indicate that it is operational.
2. On pushing the button on the microphone board, the Pi checks whether is is connected to the internet or not.
   - Not connected: It records a 12s audio clip and stores it on the microSD card (red LED is shown)
   - Connected: It analyzes all previously recorded tracks, moves them from a 'new recordings' directory to a 'old recordings' directory, writes a log file, saves it to the device and sends it via eMail (green LED progress bar is shown).
3. After recording/analysis, the device reverts back to the "waiting for button push" status, indicated by the blue LED.

Hardware:

  - Raspberry Pi Zero 2
  - Wavehare UPS (C) HAT (1000 mAh)
  - Seeed Respeaker 2-Mic HAT
 
 
 Installation:
 
  - Flash piOS auf microSD 
  - sudo apt-get update && sudo apt-get upgrade
  - Installiere Respeaker Karte: https://wiki.seeedstudio.com/ReSpeaker_2_Mics_Pi_HAT_Raspberry/
  - Installiere LED libraries etc.
  - Fortwährender Settings restore für den Soundkartenmixer nach reboot: https://dev.to/luisabianca/fix-alsactl-store-that-does-not-save-alsamixer-settings-130i
  - Installiere Shazam Library: https://github.com/dotX12/ShazamIO
  - shazam.py in bash autostart packen
  - Verringere pi Zero Stromverbrauch: https://www.cnx-software.com/2021/12/09/raspberry-pi-zero-2-w-power-consumption/
