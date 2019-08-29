# AndieGraph-AIDE
A(ndroid)IDE compatible structure for AndieGraph

This repository is a clone of dgmltn/AndieGraph but restructured.
This clone might also contain improvements with the purpose to upstream them.

Features created within this clone:
- Setting contrast colors better so that it is possible to make fades.
- Multi-touch to enable pressing multiple keys at once.
- Audio from linkport
- Rewrite of screenlock to enable faster refresh for potential greyscale graphics


Notes about the audio from linkport:
This audio feature has a very naive implementation that sends a changed hi/low value to the speaker for as long time as it was since the previous "out" operation had a different value.
This works quite fine for anything that is supposed to be about pure notes. However anything that is not based on just one tone at a time will lead to very awkward noise.
The emulator works in 20ms batches and the idea is to try and build audio streams for those 20ms at a time instead. This would generate a slight delay but could probably produce higher quality of the audio.

How to build:
This repository was originally made to be built with AIDE and the AIDE-NDK addon.
However since the AIDE-NDK addon hasn't had an update in quite a while, there is no support for the aaudio API.
To get this working I've found another ndk that is possible to run in termux.

Using termux I have downloaded this:
https://github.com/Lzhiyong/termux-ndk unpacked and then set the following environment variable.
export NDK="your path"
export PATH=$PATH:$NDK

I did have a problem with the ndk-build script that was fixed by keeping the library path.
android-ndk-r17/build/ndk-build
133c133
< export LD_LIBRARY_PATH=$ANDROID_NDK_ROOT/prebuilt/$HOST_TAG/lib
---
> export LD_LIBRARY_PATH=$ANDROID_NDK_ROOT/prebuilt/$HOST_TAG/lib:$LD_LIBRARY_PATH


In short I've been placing my jni directory somewhere and run ndk-build. This results in the needed libs in ../libs, these have then been copied to the projects libs directory before just building with AIDE.
Maybe AIDE shall be replaced with https://github.com/SDRausty/buildAPKs but I haven't really understood how that works yet.
