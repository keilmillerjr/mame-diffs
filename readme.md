# mame-diffs

by [Keil Miller Jr](http://keilmiller.com)

I did not create these patches. I am simply hosting them all together in one easy package, including binaries that I compiled. Video related patches pertain to Windows. All other patches are operating system agnostic. The guide is oriented towards **Arch Linux** and Mac OS X.

MAME License is [included](LICENSE.md) in this repository, and can be found [here](https://github.com/mamedev/mame/blob/master/LICENSE.md). It must be included with the binary.

## Patch Descriptions

#### d3d8

[by Calamity](http://forum.arcadecontrols.com/index.php/topic,151459.0.html)


> D3D8 fix is added solution for bypassing message "non-power-of-two textures" for old DX8 video cards.
>
> [quote source](http://forum.arcadecontrols.com/index.php/topic,154799.msg1671575.html#msg1671575)


#### d3d9ex

[by Calamity](http://forum.arcadecontrols.com/index.php/topic,151459.0.html)

> Groovy MAME 0.170 under Windows 7 can use Direct Draw, Direct 3-D 9 and Direct 3-D 9 Ex, being the latter the recommended API. Notice that Direct Draw stopped being supported by MAME in version 0.171, whereas Direct 3-D 9 Ex only is supported by Groovy MAME 0.167 onwards.
>
> The advantage of Direct 3-D 9 Ex over Direct 3-D 9 is that, unlike with the latter, there's no need to enable frame delay in order to force the frame latency to the minimum allowed by the driver and therefore avoid the dreaded frame queues present in the ATI video drivers when Direct 3-D is used, which add a lag of 2-3 frames.
>
> [quote source](http://geedorah.com/eiusdemmodi/forum/viewtopic.php?pid=985#p985)


#### groovymame

[by Calamity](http://forum.arcadecontrols.com/index.php/topic,151459.0.html)

#### suppression

[by MKChamp](http://mamestuff.lowtrucks.net/MKChamp/)

The official MAME has "skip_gameinfo" feature built in. It will skip the game info screen. The suppression patch, also known as nonag, will also remove the compatibility/disclaimer warning screen when used with the previously mentioned option. Using a binary with this patch applied is not recommended when reporting bugs or issues.

#### various fixes

[by haynor666](http://forum.arcadecontrols.com/index.php/topic,154799.0.html)

>based on official sources plus extra modifications imported from ARCADE http://arcade.mameworld.info (new derrative based on MAMEUIFX) and no nag patch. Some of those changes created by me.
>
> [quote source](http://forum.arcadecontrols.com/index.php/topic,154799.msg1623604.html#msg1623604)

These modifications are current for the MAME 0.211 patch.

> Video modifications:
>
> - hack for fixing sprites in neogeo driver (at the moment title screen in sengoku2 is a bit broken)
> - removed custom position and size in astrocde and cidelsa drivers (looks very bad on TV/Arcade monitor)
> - restored resolution 256x240 (from 240x240) in remaining games in btime driver as well in scregg driver
> - video fix for Metamorpic Force (proper offsets)
> - small colours fix in nemesis driver (games have now slightly more brighter picture, seems to be more accurate)
> - visible area modifications in in ssv driver (changed Air Blade; Dyna Gear)
> - visible area modifications for many games in neogeo driver (mostly from 320x224 to 304x224 but for four games even to 288x224 - Zed Blade, Goal!Goal!Goal!, Gururin, Zupapa)
> - visible area modification for X-Men,
> - visible area modification Super Contra, Gang Busters, Thunder Cross, Teenage Mutant Hero Turtles, Bells'n'Whistles [not in ARCADE32/64]
> - visible area modification for Battle Rangers, Double Dragon, Double Dragon II, Thunder Strike, China Gate, Garyo Retsuden [not in ARCADE32/64]
> - visible area modification for Express Raider, Exzisus, Liberation, Nova 2001, Rock'n'Rage, Riot City, Wonder Boy 3, Aurail [not in ARCADE32/64]
> - visible area modification for Mad Crasher, Gladiator 1984, Super Cross II, Jungle King, Sea Fighter Poseidon, Xain'n Sleena [not in ARCADE32/64]
> - visible area modification for many games in namcona1 driver [not in ARCADE32/64]
> - visible area modification for many games in system1 driver [not in ARCADE32/64]
> - some video fixes in taito_f3 driver (continue screen in Greed Seeker is now visible, the same goes to intro text in Arabian Nights)
>
> Misc modifications:
>
> - slow rendering fix for namconb1
> - more accurate video timings in Green Beret
> - swapped some IRQ handling in megasys1 driver
>
> [quote source](http://forum.arcadecontrols.com/index.php/topic,154799.msg1623604.html#msg1623604)

## Patching Sequence:

1. GroovyMame
2. Video mode
	* d3d8 *(windows, old video card compatibility)*
	* d3d9ex *(windows vista and later, for less video lag)*
3. Suppression
4. Various Fixes

## Compile

#### Prerequisites

###### Ignore Kernel Update (Arch Linux)

We do not want to loose our patched kernel for 15khz.

1. ```sudo nano /etc/pacman.conf```
2. ```#IgnorePkg =``` to ```IgnorePkg = linux``` *line 25*
3. Save the buffer *(ctrl+o)*.
4. Exit nano *(ctrl+x)*.

###### Update all packages on the system (Arch Linux)

```sudo pacman -Syu```

###### Install unzip package (Arch Linux, already included on Mac OS X)

```sudo pacman -S unzip```

###### Install Dependancies Required to Compile MAME (Arch Linux)

```sudo pacman -S base-devel git sdl2 gconf sdl2_ttf gcc qt5```

###### Install Dependancies Required to Compile MAME (Mac OS X 10.9+)

It is not required to install the complete xcode package for the command line developer tools.

1. ```xcode-select --install```
2. A software update popup window will appear that asks: "The xcode-select command requires the command line developer tools. Would you like to install the tools now?". Click "Install", then agree to the Terms of Service when requested.
3. ```cd ~/```
4. ```curl -O http://libsdl.org/release/SDL2-2.0.9.dmg && hdiutil attach SDL2-2.0.9.dmg``` *2.0.4+ required, take note of disk name from output*
6. ```sudo cp -R SDL2/SDL2.framework /Library/Frameworks/SDL2.framework```
7. ```hdiutil detach /dev/disk1s2``` *use disk name from step 4*

###### Install endlines (Mac OS X and Linux)

I have had issues patching with files within mame source and patches having different line endings. It's best to make sure all line endings are uniform before patching. Must follow *Install Dependancies Required to Compile MAME* section first.

1. ```cd ~/```
2. ```curl -L -o endlines-1.9.2.zip https://github.com/mdolidon/endlines/releases/tag/1.9.2 && unzip endlines-1.9.2.zip```
3. ```cd endlines-1.9.2```
4. ```make```
5. ```make test```
6. ```sudo make install```

#### Download

*substitute version number accordingly*

1. Download MAME Source
	1. ```cd ~/```
	2. ```sudo curl -O -L https://github.com/mamedev/mame/releases/download/mame0211/mame0211s.zip && unzip mame0211s.zip && unzip mame.zip -d mame0211```
	3. ```rm mame.zip```
2. Download Patches
	1. ```cd mame0211```
	2. ```curl -O https://raw.githubusercontent.com/keilmillerjr/mame-diffs/master/mame0211/groovymame_017n.diff```
	3. ```curl -O https://raw.githubusercontent.com/keilmillerjr/mame-diffs/master/mame0211/suppression.diff```
	4. ```curl -O https://raw.githubusercontent.com/keilmillerjr/mame-diffs/master/mame0211/various_fixes.diff```

#### Convert Line Endings to Unix

1. ```cd ~/mame0211```
2. ```endlines check -r *```
3. ```endlines unix -kr *```

#### Apply Patches

1. ```cd ~/mame0211```
2. ```patch -p0 -E < groovymame_017n.diff```
3. ```patch -p0 -E < suppression.diff```
4. ```patch -p0 -E < various_fixes.diff```

#### Warning Errors

If you get ```cc1plus: all warnings being treated as errors``` output while compiling, you can suppress these warning errors.

1. ```cd ~/mame0211```
2. ```nano makefile```
3. Change line 17: ```# NOWERROR``` to: ```NOWERROR```
4. Save the buffer *(ctrl+o)*.
5. Exit nano *(ctrl+x)*.
6. ```make```

#### Compile MAME

1. ```cd ~/mame0211```
2. You can use ```make``` without any flags, or speed things up with the Parrallen Execultion (multi-processing) jobs flag. Each job can take up to 1GB to 1.5GB of RAM. Lower this value if LogicalCores>=RAM.
	1. Linux: ```make -j$(nproc)```
	2. Mac OS X: ```make -j$(sysctl -n hw.logicalcpu)```

## Precompiled Binaries

Precompiled Binaries have the following patches applied:

| Patch         | Linux | Mac OS X |
| --------------| ----- | -------- |
| GroovyMAME    | yes   | no       |
| Suppression   | yes   | yes      |
| Various Fixes | yes   | yes      |

#### Prerequisites

###### Install unzip package

```sudo pacman -S unzip```

#### Download

1. ```cd ~/```
2. ```curl -O https://github.com/keilmillerjr/mame-diffs/blob/master/mame0211/mame64_linux.zip && unzip mame64_linux.zip```

## Contributing

#### Line Endings

Please be sure you use endlines to make sure all patches are converted to unix.

1. ```cd ~/mame-diffs```
2. ```endlines unix -kr *```

#### Compressing Binary

Please be sure that the binary is not mixed up with any other version, and is in the appropriate versioned subdirectory.

###### Prerequisites (Arch Linux)

Install zip package: ```sudo pacman -S zip```

###### Compress Binary

1. ```cd ~/mame0211```
2. ```zip mame64_linux.zip mame64``` *linux/mac*

#### Transfer To USB Disk (linux on virtual operating system install)

This can simplify transfering out of a virtual operating system install. Connect and unmount disk in host operating system. In virtualbox, click on your session and then Settings -> Ports -> USB -> USB Device Filters -> + -> *your usb device*. During an active session, click on the USB symbol and select your usb device.

*substitute device path accordingly*

###### List Available USB Devices

```lsusb```

###### Show Disk Identifiers

```sudo fdisk -l```

###### Create Disk Label

```sudo mkdir /media/usb_drive```

###### Mount Disk
```sudo mount /dev/sdb1 /media/usb_drive```

###### Copy Compressed Binary

1. ```cd ~/mame0211```
2. ```mkdir /media/usb_drive/mame0211```
3. ```cp mame64_linux.zip /media/usb_drive/mame0211/mame64_linux.zip```

###### Unmount Disk
```sudo umount /media/usb_drive```