---
layout: page
title: Easy Arcade on Recalbox (EN)
wikiPageName: Easy-Arcade-on-Recalbox-(EN)
menu: wiki
---

## Introduction (recalbox 3.3.0b17)

This page is dedicated to beginners for helping them to easily play arcade games on the recalbox.

Arcade has long been the most complicated of emulations due to its very own nature : arcade machines don't all use the same hardware, so they all have to be emulated independently.  
Imagine you want to play 5 different arcade games, you could have to use 5 different hardware emulators, whereas playing 5 different SNES games will only need the one and only SNES emulator.

That's why MAME has been invented : MAME is kind of a meta-emulator, it brings all the different emulated hardwares of arcade machines into one system, making it simpler for the user to play arcade games without any knowledge of the underlying arcade machine on wich the games are launched. It is no small feat and this is why MAME is so complicated to use.


### General MAME Principles

There are only two main principles to know to get a good grasp of how to use MAMEon your recalbox : Romsets and BIOS/driver files

### Romsets

A romset is a set of all the different game roms emulated by a MAME version.  
A romset contains parent game roms wich are roms corresponding to the 'main' version of a game and clone game roms which are 'alternative' versions of a parent rom. As you can guess, in most cases we will discard all clone roms and only used the main (or parent) ones.

Most of the code used to make those game roms playable is included in the MAME emulator. Sadly this means that there is a strong and close relationship between a MAME version and the game roms versions : When MAME releases a new version, game roms may need to be updated to fit to the new emulator version.

To keep it simple : if you use a certain MAME emulator, say version 0.78, you also have to get your hands on and use the 0.78 version of the romset. Some games from another romset may work with your version but **the only way to be sure that the most games are working is to use only a MAME version in conjunction with the romset of the same version**.

For recent versions (such as the one used by fba_librero, see below) there are less and less modifications of game roms, so it is sometime possible to use an older set and still have most of the games playable.

### BIOS / Drivers
Some of the game roms from a romset may additionaly need BIOS files, the most well known case beeing neogeo games. Let's use that as an example :  
If you want to use neogeo games, you'll have to copy the needed bios/driver file (in that case neogeo.zip) in the same folder as the game. That's all !

Off course if you use different subfolders for your games (genre subfolders or hardware type subfolders for instance) you'll have to copy the BIOS file in every folder containing games which may need it. **Given that they are pretty small sized, it's better to copy them all in each of your subfolders**.

Where do i find the BIOS files do you say ? Well it's very simple : they are included in your romset !
So if a game doesn't launch and goes back right away to the Emulation Station screen, just try to find the relevant BIOS file and copy it in the game folder.


## Arcade Emulation on Recalbox

As the [[Advanced Arcade on recalbox|Advanced-Arcade-on-Recalbox-(EN)]] wiki page for recalbox explains to us there are several arcade emulators included in recalbox.  
Just using two of them will be enough for running the majority of games on your Raspberry Pi.

Those two systems are :

* Mame
  * _mame/romset version :_ 0.78
  * _roms folder :_ mame

* FBA_libretro
  * FBA is kind of an alternative version of MAME (emulating less arcade machines), but it follows exactly the same principles which I just explained
  * _mame/romset version :_ 0.167
  * _roms folder :_ fba_libretro

Now some games will only work on Recalbox with Mame and some others only with FBA_libretro.

As a guideline, please use the [BestArcade4Recalbox](https://docs.google.com/spreadsheets/d/1F5tBguhRxpj1AQcnDWF6AVSx4av_Gm3cDQedQB7IECk/edit?usp=sharing) document to get the correct emulator to use for each game


## Let's configure your recalbox !

First download the full romsets for both emulators : romset 0.78 for mame and romset 0.167 for fba_libretro (alternativelly 0.161 should work fine).  
If you can't find the required versions of the romsets, you can download a higher version then clean it by following the instructions on https://github.com/recalbox/recalbox-os/wiki/Check-your-roms-version-with-clrmamepro-%28EN%29

You may rather download each game one by one because full romsets are quite large, but it's usually not easy to find individual roms and to be sure that they are in the right version.
Full romsets are the only way to avoid headaches !

You're now just a few steps away from playing some awesome arcade games on your recalbox.

### Copy of Bios/drivers

First we aref going to copy BIOS/drivers files from our romsets. Contraty to other systems, these files must not be copied into the bios folder but to the roms folder.
 
* Get these BIOS/Drivers files from your MAME 0.78 romset and copy them into the mame roms folder :
_acpsx.zip, cpzn1.zip, cpzn2.zip, cvs.zip, decocass.zip, konamigx.zip, megaplay.zip, megatech.zip, neogeo.zip, nss.zip, pgm.zip, playch10.zip, skns.zip, stvbios.zip, taitofx1.zip, tps.zip_

* Copy these BIOS/Drivers files from your FBA_libretro 0.167 or 0.161 romset and copy them into the fba_libretro roms folder, I only needed two of them : _neogeo.zip_ and _pgm.zip_


###Copy games

* Now check the [BestArcade4Recalbox](https://docs.google.com/spreadsheets/d/1F5tBguhRxpj1AQcnDWF6AVSx4av_Gm3cDQedQB7IECk/edit?usp=sharing) document and locate which system is the best for the game you want to play :
  * if it's in the mame tab, copy the game rom file from your complete 0.78 romset to the mame roms folders
  * if it's in the fba_libretro tab, copy the game from your complete 0.167 romset (or 0.161 or any other close to that) into the fba_libretro rom folders
  * if it's in the 'not found or not working' tab, well guess what ?

* PLAY ! (or not)


## Further Tricks

* If you want to hide your BIOS  files in Emulation Station, edit their metadata with the select menu 
(not working anymore in 4.0.0 for the moment : just rename them with a .ZIP extension (putting the zip extension in caps) and remove .ZIP use for the related arcade system in es_system.cfg)

* Remember, if you want to use subfolders in your roms folders, just make a copy of BIOS/drivers files into every subfolder and then move your game into the subfolder

* Read [[Advanced Arcade on Recalbox | Advanced Arcade on Recalbox (EN)]]
