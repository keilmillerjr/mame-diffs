# mame-diffs

by [Keil Miller Jr](http://keilmiller.com)

I did not create these patches. I am simply hosting them all together in one easy package, including binaries that I compiled. MAME License is [included](LICENSE.md) in this repository, and can be found [here](https://github.com/mamedev/mame/blob/master/LICENSE.md). It must be included with the binary.

## Patch Descriptions

#### d3d8

[Description](http://forum.arcadecontrols.com/index.php/topic,154799.msg1671575.html#msg1671575)

> D3D8 fix is added solution for bypassing message "non-power-of-two textures" for old DX8 video cards.

[Patch Source](http://forum.arcadecontrols.com/index.php/topic,151459.0.html) by Calamity

#### d3d9ex

[Support and Advantages](http://geedorah.com/eiusdemmodi/forum/viewtopic.php?pid=985#p985)
> Groovy MAME 0.170 under Windows 7 can use Direct Draw, Direct 3-D 9 and Direct 3-D 9 Ex, being the latter the recommended API. Notice that Direct Draw stopped being supported by MAME in version 0.171, whereas Direct 3-D 9 Ex only is supported by Groovy MAME 0.167 onwards.
>
> The advantage of Direct 3-D 9 Ex over Direct 3-D 9 is that, unlike with the latter, there's no need to enable frame delay in order to force the frame latency to the minimum allowed by the driver and therefore avoid the dreaded frame queues present in the ATI video drivers when Direct 3-D is used, which add a lag of 2-3 frames.

[Patch Source](http://forum.arcadecontrols.com/index.php/topic,151459.0.html) by Calamity

#### groovymame

[Patch Source](http://forum.arcadecontrols.com/index.php/topic,151459.0.html) by Calamity

#### suppression

The official MAME has "skip_gameinfo" feature built in. It will skip the game info screen. The suppression patch, also known as nonag, will also remove the compatibility/disclaimer warning screen when used with the previously mentioned option. Using a binary with this patch applied is not recommended when reporting bugs or issues.

[Patch Source](http://mamestuff.lowtrucks.net/MKChamp/) by MKChamp

#### various fixes

>based on official sources plus extra modifications imported from ARCADE http://arcade.mameworld.info (new derrative based on MAMEUIFX) and no nag patch. Some of those changes created by me.

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

[Patch Source](http://forum.arcadecontrols.com/index.php/topic,154799.0.html) by haynor666

## Patching Sequence:

1. GroovyMame
2. Video mode
	* d3d8 *(old video card compatibility)*
	* d3d9ex *(windows vista and later, for less video lag)*
3. Suppression
4. Various Fixes

## Applying Patches Using Linux (Arch)

#### Prerequisites

###### Ignore Kernel Update

We do not want to loose our patched kernel for 15khz.

1. ```sudo nano /etc/pacman.conf```
2. ```#IgnorePkg =``` to ```IgnorePkg = linux``` *line 25*
3. Save the buffer *(ctrl+o)*.
4. Exit nano *(ctrl+x)*.

###### Update all packages on the system

```sudo pacman -Syu```

###### Install unzip package

```sudo pacman -S unzip```

###### Install Dependancies Requiered to Compile MAME

```sudo pacman -S base-devel git sdl2 gconf sdl2_ttf gcc qt5```

#### Create New Directory

1. ```cd ~```
2. ```mkdir dev```

#### Download & Unzip MAME Source and Patches

1. ```cd ~/dev```
2. ```curl -O https://github.com/mamedev/mame/archive/mame0211.zip && unzip mame0211.zip```
3. ```curl -o mame-diffs.zip https://github.com/keilmillerjr/mame-diffs/archive/master.zip && unzip mame-diffs.zip```

#### Apply Patches

1. ```cd ~/dev/mame-mame0211```
2. ``` patch -p0 < ~/dev/mame-diffs-master/mame0211/groovymame_017m.diff```
3. ```patch -p0 < ~/dev/mame-diffs-master/mame0211/suppression.diff```
4. ```patch -p0 < ~/dev/mame-diffs-master/mame0211/various_fixes.diff```

#### Compile MAME

1. ```cd ~/dev/mame-mame0211```
2. ```make```

## Line returns

Patches were converted to unix line returns using dos2unix. This section of the guide is only for my personal reference, or anyone willing to fork and help contribute to the project.

#### To install on Mac OS X using Homebrew:

1. ```brew update```
2. ```brew install dos2unix```

#### Mac (\r) to Unix (\n)

```mac2unix -n file.mac.txt file.unix.txt```

#### Windows (\r\n) to Unix (\n)

```dos2unix -n file.windows.txt file.unix.txt```