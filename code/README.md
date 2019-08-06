# Tutorial (how to configure and flash)

This firmware will work out of the box, no edits required, with your Smash Box, and flashing it is very easy. Here's what you'll need:

1. Arduino IDE (compatible with Windows, Mac, and Linux): https://www.arduino.cc/en/Main/Software
2. Smash Box Designer and Firmware Updater: https://cdn.shopify.com/s/files/1/0166/4408/files/Smash_Box_Designer_Beta_4.03.zip?44
3. Nicohood Library: https://github.com/NicoHood/Nintendo/archive/master.zip

Before anything else, make sure you have installed the Arduino IDE and unzipped the Smash Box Designer .zip into an easy-to-find directory. The Nicohood library does not need to be unzipped.

## Smash Box Drivers and Setup:

1. Go to the directory you unzipped the Smash Box Designer software to, and open the Documentation and Drivers directory.
   * If you have a gen 1 or alpha Smash Box, you need to install the CH340 drivers.exe
   * If you have a gen 2 Smash Box, install the Teensy drivers.exe.
   * If the driver installer says that you don't need to install drivers, great, just close the window and move on.
2. Plug in your Smash Box to your PC using the included USB cable. Let Windows install drivers if it hasn't already.
3. Find the COM port that your Smash Box is plugged into.
   * An easy way to do this is to unplug your Smash Box, open up the Smash Box Firmware Updater, and note the COM ports listed in the "Ignore COM Ports" box. Close the Firmware Updater, plug your Smash Box back in, and open it again. Whichever port wasn't there before is the port your Smash Box is plugged into.
4. To be safe, if you haven't configured your Smash Box before, install the Gen2 Hotfix and then use the Firmware Updater (being sure to select the correct COM port both times).
5. Open up the Smash Box Designer software and go to the Options tab. Click the button that says "Set to Program Mode". You may hear the Windows sound for a device being unplugged and replugged. Your Smash Box is now ready for flashing!

## Steps:

1. Download the DIYB0XX.ino file from this repo (located in code/DIYB0XX) and open it in the Arduino IDE. If it asks you to create a DIYB0XX directory, say "Yes" to that.
2. Install the Nicohood library (required to build the code)
   * Sketch > Include Library > click Add .ZIP Library. Then find and select the Nintendo-master.zip file you downloaded earlier.
3. Tools > Board > click "Arduino/Genuino Mega or Mega 2560".
4. Tools > Processor > click "ATmega2560".
5. Tools > Port > select the COM port that your Smash Box is plugged into. If the port listed does not say "Arduino/Genuino Mega or Mega2560" or something similar after it, you probably haven't set your Smash Box to Program Mode, so make sure you do that before continuing.
6. In the greenish-blue top menu bar, select and click the right-arrow icon.
7. If all goes well, a lot of things should start happening in the terminal at the bottom of the Arduino IDE. After a short while (<30 seconds, usually), it should say "Done uploading" right above the terminal. Once it does, you can unplug your new "SmashB0XX" and go to town!

## Notes:

* This version of DIYB0XX uses Smash Ultimate as the default mode. To use Melee mode, hold down B while plugging in. To use PM mode, hold X while plugging in.
* If you would like to use WASD instead of right pinky for Up, put two slashes in front of line 76 and delete the two slashes in front of line 78 (in DIYB0XX.ino).
  * If you want to do this, I also suggest remapping Y or R to right pinky (since your right pinky will have nothing to do otherwise). For Y, change the number in line 64 to 45. For R, change the number in line 68 to 45.

## Restoring your Smash Box to the original firmware:

This is pretty easy to do. All you have to do is plug in your Smash Box, open up the Firmware Updater from the Smash Box Designer folder, and run it. That should restore your Smash Box to its original firmware, and you can go back to using Smash Box Designer to configure it yourself.

# Crane's README:

#### This program was originally made by simple. The edits I have made are listed below, and I have received the permission of its creator and other editors to add it to this repo.

This code utilizes Nicohood's Nintendo library.

As of July 4th 2019 : I rewrote the entire program from scratch to increase efficiency, increase readability, to make adding new profiles easier, to improve the Smash Ultimate mode

This is code designed with 16 mhz Arduinos in mind such as the Arduino Mega 2560, Arduino Micro, Arduino Nano, etc. A version of this code is available with native USB joystick support and nunchuk support for controllers using the 32u4 chip such as my Arduino Micro based GCCPCB. You can probably use it on a Micro/Leonardo/Pro Micro DIY, but do so at your own risk.

Heres a link to it : https://github.com/Crane1195/GCCPCB/tree/master/code

## SOCD Options
You can choose between 2ip, 2ip with no reactivation, and neutral to resolve simultaneous opposite cardinal direction (SOCD) inputs. This applies to both the control and c stick.

#### 2ip works like this:
* Press left. Character moves left.
* While still pressing left, press right. Character moves right.
* While still pressing left, stop pressing right. Character moves left again.

#### 2ip with no reactivation (The method the B0XX uses) works like this:
* Press left. Character moves left.
* While still pressing left, press right. Character moves right.
* While still pressing left, stop pressing right. Character will not move.

#### Neutral works like this:
* Press left. Character moves left.
* While still pressing left, press right. Character stops moving.
* While still pressing left, stop pressing right. Character moves left again.

## Game profiles
Currently there are 3 game profiles. Melee, Ultimate, and PM.
* One of these modes loads when the controller is plugged in while holding no buttons, by default this is Melee.
* Another mode loads when the controller is plugged in while holding B, by default this is Ultimate.
* The third mode loads when the controller is plugged in while holding X, by default this is PM.

You can choose the SOCD method for each profile separately.

You can change which is loaded with no button press at line 59 (and its SOCD at line 60), and which are loaded with button presses starting at line 113. You can change the button required by changing whats inside the parenthesis of `if (digitalRead(**) == LOW)` as well as the game / SOCD like before.

More profiles can be added easily. Just add another game in the enum game declaration at line 23, add another block for picking a mode via a button press like lines 113-117, and everywhere you see a if(currentGame == XXXXX), you will need to add a code block like it for the new game mode. From there you can edit the coords for that mode.

## DPAD Toggle Button / Switch
Normally the DPAD is enabled by holding Mod1 and Mod2 and pressing C-Up/down/left/right. If instead you would rather have a switch or a button do this, follow these steps.
* Uncomment line 84, and change XX to whatever pin you have your switch / button plugged into.
* Uncomment line 109, this sets that pin to the correct mode.
* Uncomment line 148, this sets a boolean to true if the button is pressed or the switch is closed.
* Comment out line 523, this is the normal way DPAD is enabled.
* Uncomment line 524, this enables the DPAD code when the button is pressed or switch is closed.

## Contact info

Let me know if you have any issues with the code, or any suggestions for the Ultimate/PM modes, as they are less concrete.

Discord : @Crane#1195
