---
created: 20211114192757596
desc: ''
id: zmtf1tif64cs1wflhiange0
title: Tidal Cycles
updated: 1652817950110
---
   
Topics::  [music](../unsorted/music.md)   
   
   
---   
   
### Install Haskell   
   
<[https://www.haskell.org/platform/linux.html#linux-ubuntu>](https://www.haskell.org/platform/linux.html#linux-ubuntu>)   
   
    sudo apt-get install haskell-platform   
   
check if its installed using `ghci`   
   
Also run   
   
```
sudo apt update
# for safe measure
sudo apt install build-essential cabal-install git jackd2
```
   
   
### Install SuperCollider   
   
Using this handy script: <[https://github.com/lvm/build-supercollider>](https://github.com/lvm/build-supercollider>)   
   
    git clone [https://github.com/lvm/build-supercollider](https://github.com/lvm/build-supercollider)   
    cd build-supercollider   
    sh build-supercollider.sh   
    sh build-sc3-plugins.sh   
   
Run this inside SuperCollider   
   
    Quarks.checkForUpdates({Quarks.install("SuperDirt", "v1.7.2"); thisProcess.recompile()})   
   
Inside a new file:   
   
    SuperDirt.start;   
    s.makeGui;   
   
Start recording for sounds from the `s.makeGui` window   
   
`Shift + Return` to run   
   
### Install Tidal Cycles   
   
    cabal update   
    cabal install tidal --lib   
   
### Choose a text-editor   
   
Let's go with <[https://atom.io/>](https://atom.io/>)   
   
Once installed: Packages \> TidalCycles \> Boot TidalCycles   
   
### Useful links   
   
<[https://tidalcycles.org/docs/getting-started/linux_install>](https://tidalcycles.org/docs/getting-started/linux_install>)   
   
   
---   
   
    SuperDirt.start;   
    s.makeGui;   
   
    MIDIClient.init;   
    ~midi = MIDIOut.newByName("Midi Through", "Midi Through Port-0");   
    ~dirt.soundLibrary.addMIDI(\midi, ~midi);