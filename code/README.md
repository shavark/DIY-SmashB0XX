# Tutorial (how to configure and flash)

This firmware will work out of the box, no edits required, with your Smash Box, and flashing it is very easy. Here's what you'll need:

1. Arduino IDE (compatible with Windows, Mac, and Linux): https://www.arduino.cc/en/Main/Software
2. Smash Box Designer and Firmware Updater: https://cdn.shopify.com/s/files/1/0166/4408/files/Smash_Box_Designer_Beta_4.03.zip?44
3. Nicohood Library: https://github.com/NicoHood/Nintendo/archive/master.zip

## Smash Box Drivers and Setup:

1. Go to the directory you unzipped the Smash Box Designer software to, and open the Documentation and Drivers directory. If you have a gen 1 or alpha Smash Box, you need to install the CH340 drivers .exe; if you have a gen 2 Smash Box, install the Teensy drivers .exe. If the driver installer says that you don't need to install drivers, great, just close the window and move on.
2. Plug in your Smash Box to your PC using the included USB cable. Let Windows install drivers if it hasn't already.
3. Find the COM port that your Smash Box is plugged into. An easy way to do this is to unplug your Smash Box, open up the Smash Box Firmware Updater, and note the COM ports listed in the "Ignore COM Ports" box. Close the Firmware Updater, plug your Smash Box back in, and open it again. Whichever port wasn't there before is the port your Smash Box is plugged into.
4. To be safe, if you haven't configured your Smash Box before, install the Gen2 Hotfix and then use the Firmware Updater (being sure to select the correct COM port both times).
5. Open up the Smash Box Designer software and go to the Options tab. Click the button that says "Set to Program Mode". You may hear the Windows sound for a device being unplugged and replugged. Your Smash Box is now ready for flashing!

### Steps:

1. Before anything else, make sure you have installed the Arduino IDE and unzipped the Smash Box Designer .zip into an easy-to-find directory. The Nicohood library does not need to be unzipped.
2. Download the DIYB0XX.ino file from this repo (located in code/DIYB0XX) and open it in the Arduino IDE. If it asks you to create a DIYB0XX directory, say "Yes" to that.
3. In the Tools dropdown of the Arduino IDE, hover over Board and then select and click "Arduino/Genuino Mega or Mega 2560" from the dropdown.
4. In the Tools dropdown again, hover over Processor and select and click "ATmega2560" from the dropdown.
5. In the Tools dropdown again, hover over Port and select the COM port that your Smash Box is plugged into. If the port listed does not say "Arduino/Genuino Mega or Mega2560" or something similar after it, you probably haven't set your Smash Box to Program Mode, so make sure you do that before continuing.
6. In the greenish-blue top menu bar, select and click the right-arrow icon.
7. If all goes well, a lot of things should start happening in the terminal at the bottom of the Arduino IDE. After a short while (<30 seconds, usually), it should say "Done uploading" right above the terminal. Once it does, you can unplug your new "SmashB0XX" and go to town!

## Notes:

* This version of DIYB0XX uses Smash Ultimate as the default mode. To use Melee mode, hold down B while plugging in. To use PM mode, hold X while plugging in.
* If you would like to use WASD instead of right pinky for Up, put two slashes in front of line 76 and delete the two slashes in front of line 78. If you want to do this, I also suggest remapping Y or R to right pinky (since your right pinky will have nothing to do otherwise). For Y, change the number in line 64 to 45. For R, change the number in line 68 to 45.

# Crane's README:

#### This program was originally made by simple. The edits I have made are listed below, and I have received the permission of its creator and other editors to add it to this repo.

This utilizes the Nicohood Library. This were originally made by simple to make a Smashbox. Snapple and then Danny modified this code to work with the B0XX's two modifiers and to try and abide by the parameters set in the B0XX manifesto.

I then modified aspects of that code to make it function in Project M, Smash 4, and Smash Ultimate, as well as having 2ip as a SOCD option.

Hexadecimal has added 2ip with no reactivation as a SOCD method.

# My Edits
## 2ip or 2ip with no reactivation or Neutral SOCD
I have edited the left/right simultaneous opposite cardinal directions (SOCD) method so you now have the option to pick from 2ip or neutral. Hexadecimal added 2ip with no reactivation which is the method the B0XX uses.

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

## Choose your SOCD
You can choose your horizontal SOCD method for each game profile.

To do so, change the value to the right of the equal sign on line 92 for Melee, 129 for Ultimate, and 134 for PM to Neutral, TwoIP, or TwoIPNoReactivate. I do not advise changing these though, as the default settings match the B0XX.

## I have combined my Melee, Project M, and Smash4/Ultimate edits, so you don't have to keep swapping profiles.
 *  To launch in Melee mode, just plug in normally.
 *  To launch in Smash4/Ultimate mode, hold B while plugging in.
 *  To launch in Project M mode, hold X while plugging in.

 Be sure to do a button check before starting a set, to confirm you are in the right mode.

#### To confirm you are in the right mode:
 * Enable tap jump.
 * If mod1+up makes you jump, or if mod1+down+B makes you neutral B, you are in the wrong mode. Check both of these.

## Edits made for the Project M mode
 *  Tilts, firefox angles, shield drop angles (Axe method), and wavedash angles all fixed.
 *  Fixed bug where left and down were not working on SSS and menus.

## Edits made for the Smash4/Ultimate mode
 * Mods + cardinals, tilts, triggers(shields), and most firefox angles edited.
 * Mod1/2 + cardinal has slow run/walking speed. Mod1 + cardinal gives perfect speed to ledgerun in smash4.
 * Tilts now work with mod1.
 * Triggers now give the analog value needed to shield. LRAStart now works too because of this.
 * FFox angles (B0XX method, c stick) now almost work properly. Mod1+diagonal+cright/left do not work in Smash4, but do in Ultimate.
 * C stickless firefox angles function now.

All the names above are the Discord names of users in the 20XX Discord, where the original code was shared.
