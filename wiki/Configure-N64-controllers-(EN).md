---
layout: page
title: Configure N64 controllers (EN)
wikiPageName: Configure-N64-controllers-(EN)
menu: wiki
---

Mupen64plus is not auto-configured by recalbox as the other emulators. So you need to do it manually.  
 
_For information : Your **Hotkey** button will be automatically assigned to the emulator exit function._

### A - Add your controller's configuration to the system :   
To configure your controler, you'll need information about it.
Go in [[root acces|Root-access-on-terminal-(EN)]], and use the [[jstest command|Test-your-joystick-with-jstest-(EN)]] :

`jstest /dev/input/js0`

In my case, I get : 

```
Joystick (Broadcom Bluetooth Wireless  Joystick                        ) has 6 axes (X, Y, Z, Rz, Hat0X, Hat0Y)
and 12 buttons (Trigger, ThumbBtn, ThumbBtn2, TopBtn, TopBtn2, PinkieBtn, BaseBtn, BaseBtn2, BaseBtn3, BaseBtn4, BaseBtn5, BaseBtn6).
```

Once the controller's name and each button identified, you need to edit this file `/usr/share/mupen64plus/InputAutoCfg.ini`

Use this command :

`nano  /usr/share/mupen64plus/InputAutoCfg.ini`

Now, to the end of the file, add the configuration's informations, like this :   

_This template is an example, with informations about my controller (controller's name, button number etc...). You need to adapt it with your own controller's informations._   

```
[Broadcom Bluetooth Wireless  Joystick                        ]
plugged = True
plugin = 2
mouse = False
AnalogDeadzone = 4096,4096
AnalogPeak = 32768,32768
DPad R = hat(0 Right)
DPad L = hat(0 Left)
DPad D = hat(0 Down)
DPad U = hat(0 Up)
Start = button(9)
Z Trig = button(7)
B Button = button(2)
A Button = button(1)
C Button R = axis(3+)
C Button L = axis(3-)
C Button D = axis(2+)
C Button U = axis(2-)
R Trig = button(5)
L Trig = button(4)
Mempak switch = button(6)
Rumblepak switch = 
X Axis = axis(0-,0+)
Y Axis = axis(1-,1+)
```

Once your configuration ok, do `Ctrl+x` to exit nano, accept to overwrite the file with `y` and press `Enter` to exit.   
You can now start a N64 game, and test your configuration.   

Your configuration is ok, you love it ?? Great ^^   
But, there is a "problem". When you update your recalbox, all these configuration files are updated too.   
So, they will be reset.   
If don't want to do that after each update, do a backup of your `InputAutoCfg.ini` file.   
You can also add your configuration to recalbox. You need to go to [this issue](https://github.com/digitalLumberjack/recalbox-os/issues/437), and post your own configuration as comment.   
Then we'll add it to the system in a next recalbox's update. (not needed anymore because a configgen is integrated since recalbox version 4.0.0)

### B - Add special commands   
Mupen64plus doesn't support buttons combinations, as retroarch emulators, to start a special commands.   
But you can affect unused buttons to a specific command, as _save/load a savestate, switch savestate slots,_ etc...   

To do that, in a first time, you need to identify all unused buttons in your configuration.   
So, as seen before, go in [[root acces|Root-access-on-terminal-(EN)]] and use [[jstest command|Test-your-joystick-with-jstest-(EN)]], then note the code number of your unused buttons.   

Now, ever in root acces, edit your `mupen64plus.cfg` file with this command :   

`nano /recalbox/configs/mupen64/mupen64plus.cfg`   

Then go in the section called `[CoreEvents]`. The useful part, is this one :   
```
# Joystick event string for stopping the emulator
Joy Mapping Stop = ""
# Joystick event string for switching between fullscreen/windowed modes
Joy Mapping Fullscreen = ""
# Joystick event string for saving the emulator state
Joy Mapping Save State = ""
# Joystick event string for loading the emulator state
Joy Mapping Load State = ""
# Joystick event string for advancing the save state slot
Joy Mapping Increment Slot = ""
# Joystick event string for taking a screenshot
Joy Mapping Screenshot = ""
# Joystick event string for pausing the emulator
Joy Mapping Pause = ""
# Joystick event string for muting/unmuting the sound
Joy Mapping Mute = ""
# Joystick event string for increasing the volume
Joy Mapping Increase Volume = ""
# Joystick event string for decreasing the volume
Joy Mapping Decrease Volume = ""
# Joystick event string for fast-forward
Joy Mapping Fast Forward = ""
# Joystick event string for pressing the game shark button
Joy Mapping Gameshark = ""
```
Something to keep in mind, is than Mupen64plus, identify `player 1` as `J0`, `player 2` as `J1` etc...   
So, for example, if you want to add button number 10, of the player 1, to _"save savestates"_ command, you need to edit your file like this :   
`Joy Mapping Save State = "J0B10"`  
 
And if you want to add button 5, of the player 2, to  _"load savestates"_ command, you'll edit your file like this :   
`Joy Mapping Load State = "J1B5"`   

Once your configuration ok, do `Ctrl+x` to exit nano, accept to overwrite the file with `y` and press `Enter` to exit.  
