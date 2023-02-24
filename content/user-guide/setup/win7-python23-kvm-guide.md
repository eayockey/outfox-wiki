---
title: Setup Python2 & KVM (Win7)
description: Guide for setting up a Python 2 (SuperNOVA / SuperNOVA2) system and a KVM switch on Windows 7
weight: 4
---

This is a guide for how to get Outfox running on a Python 2 (SuperNOVA / SuperNOVA2) cabinet, enabling pad and cabinet inputs, sound, and lights.

---
# Materials
## List of materials for the Python 2
###### Note that a 32-bit Outfox build is currently required to load the Python23IO input driver.
* DDR Python 2 cabinet (Used: Betson DDR SuperNOVA2)
* PC (Used: Dell Optiplex 780)
* Dedicated graphics card (Optional but recommended) (Used: Geforce GT 740)
* Windows 7 (Used: Windows 7 x64 SP 1; x32 should also work)
* Outfox 32-bit (Used: OutFox 0.4.18.1 LTS 32-bit)
* 2x USB-A extenders (Used: [OKRAY 6' USB Extender](https://www.amazon.com/dp/B076HHK8Y6))
* 1x 3.5mm (AUX audio) male to stereo RCA males cable (may be unnecessary if using KVM)

## List of materials for a network connection
###### Connecting SuperNOVA 2 to a network will greatly speed up its boot sequence, as it will otherwise look for a network for a few minutes before timing out. Connecting your PC to a network will make it much easier to load simfiles and remotely work on it, which is especially important if it's mounted in your cab.
* Network switch (Used: [TP-LINK TL-SF1005D](https://www.amazon.com/dp/B000FNFSPY))
* 3x ethernet cables (Used: 1x 12" cable, 2x 5' cables)
* Wi-fi to LAN adapter (Optional, if you want wi-fi) (Used: [IOGEAR GWU627](https://www.amazon.com/gp/product/B004UAKCS6/))

## List of materials for the KVM
###### A KVM will allow you to switch between the stock game and your PC with a button press. A KVM with two USBs per connection may be required (many condense the inputs to a single USB on the output).
* KVM switch (Used: [Rosewill KVM RKV-4UC](https://www.amazon.com/dp/B004B0H5R6))
* 2x more USB-A extenders
* 2x 3.5mm (AUX audio) female to stereo RCA males cables (depends on KVM)
* 1x 3.5mm (AUX audio) female to female coupler/adapter (depends on KVM)

---
# Setup
## Outfox Python2 Setup
#### Configure the cabinet:
1. Turn off the arcade machine and remove its power plug
   
   ###### The Betson components may hold a charge even if powered off if the plug is still attached. Best to unplug it to be safe.
2. Connect the PC to the USBs from the Playstation 2
   1. Open the Python 2 case in the back, center, 2nd shelf of the cabinet
   2. Disconnect the 2 USBs from the front of the Playstation 2 (they are connected to the board and a ground)
   3. Connect your 2x USB-A extenders to the cables you disconnected
   4. Connect the other end of your 2x USB-A extenders to your PC
   5. Ensure all of the other connections are still intact in the Python 2 and on the Playstation 2 (the PS2 video cable especially likes to detach itself), then replace the Python 2 case lid
3. Connect the PC to the VGA cable from the cabinet
   1. Disconnect the VGA cable from the left side of the Python 2 case
   2. Connect the VGA cable to your PC
4. Connect the PC to the amplifier
   1. Connect your 3.5mm-Male-to-stereo-RCA-male cable to the PC audio out
   2. Connect the other end of the cable to the Amplifier line 1 in ports on the left side (the amplifier is in the back, center, top shelf)
#### Configure the Windows 7 PC:
1. Install [libusbK](https://sourceforge.net/projects/libusbk/) (Used: libusbK 3.1.0.0; libusb-win32 may also work)
2. Install & run [Zadig](https://zadig.akeo.ie/) (Used: Zadig 2.7)
   1. Choose the Python 2 IO device (likely 'Unknown Device #1')
   2. Rename the device to something you'll recognize later, such as "Python 2 USB IO"
   3. Select the lib driver (libusbK in this guide)
   4. Install the driver and wait for it to complete
3. Run Outfox x32 at least once to create a `Save` folder, then exit
4. Configure [Preferences.ini](https://outfox.wiki/user-guide/config/preferences/) in your `Outfox\Save` directory:
   * `ArcadeOptionsNavigation=1` *Uses the machine buttons without up/down to navigate menus*
   * `DisplayAspectRatio=1.333333` *Uses a 4:3 aspect ratio to fit the stock monitor*
   * `DisplayHeight=600` *800x600 for Trisync monitors. Yours may need 640x480 or something else.*
   * `DisplayWidth=800` *800x600 for Trisync monitors. Yours may need 640x480 or something else.*
   * `InputDrivers=Python23IO,legacy,minisdl` *'legacy' enables keyboard input*
   * `LastSeenMemory=` *Best to clear this if you've used a 64-bit Outfox before*
   * `Python23IO_HDXB_DEV_ID=3` *Default; may be optional*
   * `Python23IO_HDXB_PORT=` *Default (blank); may be optional*
   * `Python23IO_Mode=SDP2IO`
   * `Python23IO_P2IO_EXTIO=1` *Default*
   * `UseOldJoystickMapping=0`
   * `UsingArcadePads=1`
5. Configure BIOS to start PC on receiving power (optional)
###### The method for this varies by PC manufacturer. Boot into BIOS and look for 'Power Management' or 'AC power' options.
6. Increase the USB polling rate (optional)
   * Work in progress. Check [HackMyCab](https://www.hackmycab.com/?portfolio=usb-polling) for instructions for a JPAC (3rd party DDR extio device).
7. Run Outfox!
---
## Network Setup
###### Recommended. SuperNOVA2 will wait for a few minutes on boot before timing out if you do not connect it to a network.
1. Either provide an ethernet cable or use a wi-fi to ethernet adapter (and configure it to receive a wi-fi signal)
2. Plug your internet source (direct line or cable from your wi-fi to ethernet device) into port 1 on your switch
3. Connect an ethernet cable between another port on the switch and the port on the left side of the Python 2
4. Connect another ethernet cable between another port on the switch and the ethernet port on the PC
---
## Python2 KVM Setup
It may be best to pick a KVM that takes 2 USB inputs and delivers 2 USB outputs per device due to the Playstation 2 in the Python 2 expecting 2 USB inputs. You'll also need a KVM that switches between audio sources. The item linked above in the materials does both.
1. Turn off the arcade machine and remove its power plug
   ###### The Betson components may hold a charge even if powered off if the plug is still attached. Best to unplug it to be safe.
2. Connect the USBs to the Python 2
   1. Open the Python 2 case in the back, center, 2nd shelf of the cabinet
   2. If you haven't already, disconnect the 2 USBs from the front of the Playstation 2 (they are connected to the board and a ground)
   3. If you haven't already, connect your 2x USB-A extenders to the cables you disconnected
   4. Connect the other end of your 2x USB-A extenders to the KVM USB inputs
   5. Find which set of KVM outputs is #1. You'll this for the stock SuperNOVA / SuperNOVA2 game
      ###### The official game should use input 1 because it may crashloop if it doesn't detect USB inputs soon after boot.
   6. Connect the KVM #1 USB outputs to the Playstation 2 in the Python 2
   7. Ensure all of the other connections are still intact in the Python 2 and on the Playstation 2 (the PS2 video cable especially likes to detach itself), then replace the Python 2 case lid
3. Connect the USBs to the PC
   1. Connect the KVM #2 USB outputs to 2 open USB ports on the PC
4. Connect the VGA to the Python 2
   1. Connect the KVM #1 VGA input to the VGA output on the left side of the Python 2
5. Connect the VGA to the PC
   1. Connect the KVM #2 VGA input to VGA output on the PC
6. Connect the audio to the Python 2
   1. Connect the KVM #1 audio input to the Line 1 audio output on the Python 2
   2. Depending on your KVM connections, you may need 1 or more adapters. The recommended KVM provides a 3.5mm male input and the stock amplifier provides a stereo RCA female output, so either a 3.5mm female to RCA stereo male cable or a 3.5mm female/female coupler and 3.5mm male to RCA stereo male adapter/cable would be necessary
7. Connect the audio to the PC
   1. Connect the KVM #1 audio input to the audio output on the PC
8. Connect the audio to the Amplifier
   1. Connect the KVM #1 audio output to the Line 1 audio input on the amplifier (back of machine, left side, center, top shelf)

### Running the KVM
* SuperNOVA1&2 will need its USB inputs during its boot sequence or it will crashloop.
* Switching away from SuperNOVA1&2 after booting or during gameplay will give a pad input error that can be cleared by entering and exiting the test menu.
* Outfox will need the Python 2 USB inputs during startup or it will not activate Python 2 support (no inputs or lights).
* Switching away from Outfox will cause it to crash. This is being addressed in a future update.
* Therefore the current best solution is to create and run a BAT file that will monitor Outfox's status and restart it if it is hung. 
   * The following BAT script will start Outfox and then check every 3 seconds to see if it's not responding. If it isn't, it will restart it:
   ```
   echo off
   Title Outfox restart watchdog
   set OutfoxLocation="C:\Games\OutFox 0.4.18 LTS Win32\Program\OutFox.exe"
   :OutfoxStart
   start "" %OutfoxLocation%
   :OutfoxStartLoop
   tasklist /fi "ImageName eq OutFox.exe" /fo csv 2>NUL | find /I "OutFox.exe">NUL
   timeout 1 > NUL
   if "%ERRORLEVEL%"=="0" goto OutfoxHungLoop
   goto OutfoxStartLoop
   :OutfoxHungLoop
   taskkill /im "OutFox.exe" /fi "STATUS eq NOT RESPONDING" /f >nul && goto OutfoxStart
   timeout 3 > NUL
   goto OutfoxHungLoop
   ```
   * Create this file, and name it something like `OutfoxRestartWatchdog.bat`.
   * You probably want it to run when the PC boots. If so, place the BAT file in your User's AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup folder (Start Menu > Run > `"%appdata%\Microsoft\Windows\Start Menu\Programs\Startup"`).
#### Starting up the machine
* Turn on the machine and set the KVM to input #1 if it isn't already
* Wait until you begin to see DDR diagnostic info.
* From here it's safe to switch the KVM to your PC if you like.
##### Switching to PC
* Outfox is likely not responding or not running.
* If the above BAT file hasn't restarted the program, close all error popups.
* If Outfox still isn't running, start it manually.
##### Switching to SuperNOVA
* You'll arrive at an I/O error screen that advises you to push the Test button.
* Push the test button.
* Exit the test menu.
