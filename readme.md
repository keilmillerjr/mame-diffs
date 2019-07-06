# mame-diffs

I did not create these patches. I am simply hosting them all together in one easy package, including binaries that I compiled.

## Applying Patches

Patches are applied in this order:

1. GroovyMame
2. Video mode
	* d3d8 (windows XP 32-bit) 
	* d3d9ex (windows 7+ for less video lag)
3. Suppression
4. Various Fixes

## Line returns

Patches are converted to unix line returns using dos2unix.

#### To install on Mac OS X using Homebrew:

1. ```$ brew update```
2. ```brew install dos2unix```

#### Mac (\r) to Unix (\n)

mac2unix -n file.mac.txt file.unix.txt

#### Windows (\r\n) to Unix (\n)

dos2unix -n file.windows.txt file.unix.txt