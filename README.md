# Bash on Android

A makefile that patches & cross-compiles bash 4.4 beta to Android (on
ARM, but it's configurable). Bash itself is kept pristine w/o
behavioral modifications.

## Prerequisites

* Androis NDK (tested w/ r10e)
* Linux (tested on Fedora 23)
* GNU Make

## Compile

	$ git clone ...
	$ mkdir tmp && cd tmp

	$ wget ftp://ftp.gnu.org/gnu/bash/bash-4.4-beta.tar.gz
	$ tar xfz bash-4.4-beta.tar.gz

The arm target:

	$ bash-on-android/bash-on-android compile

This presumes that the NDK was installed in
`/opt/s/android-ndk-r10e`. If not, set the correct path via a command
line override:

	$ bash-on-android/bash-on-android compile NDK=my/android-ndk/installation

If the cross-compilation succeeds, `build-arm-bash-4.4-beta/bash`
appears:

	$ file build-arm-bash-4.4-beta/bash
	build-arm-bash-4.4-beta/bash: ELF 32-bit LSB executable, ARM, EABI5 version 1 (SYSV), statically linked, not stripped

## Installation

	$ adb push build-arm-bash-4.4-beta/bash /data/bin

Don't put it in `/sdcard`; the 1st partition of the card is usually
formatted w/ FAT32 & your ROM may mount it w/o execute access.

## License

MIT.
