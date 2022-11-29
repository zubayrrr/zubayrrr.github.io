---
created: 1658105133263
desc: ''
id: hbogjgnkmj9ecp1s0s3xkrd
title: Vcv Rack
updated: 1658209425905
---
   
Topics::  [music](../unsorted/music.md)   
   
   
---   
   
## Lets learn VCV Rack   
   
It is an Eurorack Synthesizer   
   
   
A modular synth lets you make sound using analogue electronics   
   
You use continuous signal, not digital.   
   
It is basically an analogue computer for sound.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1658195351/wiki/kgxqrt4sva2aecff4qlq.png)
   
   
## VCO   
   
**Voltage Controlled Oscillator**   
   
   
- Sounds start with an oscillator (VCO) that can produce different waveforms with different sonic qualities   
- We use electrical signals to represent sounds and control effects   
  in a modular synthesizer.   
   
- An oscillator generates a repeating signal that corresponds to a   
  sound.   
   
- An electrical signal that is used to control a module is called a   
  **Control Voltage** (CV).   
   
- It can produce Analogue or Digital waveform.   
- It has frequency (pitch) control.   
- It has pulse width knob for square wave.   
- Type of waves VCO can make:   
  - Sine   
  - Triangle   
  - Sawtooth   
  - Square   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1658195402/wiki/nqsqivtxdyqhniaosbts.png)   
   
Here, we have **patch**, a VCO's SIN output in the AUDIO's left input.   
   
What colored light's indication mean:   
   
   
- **red** = negative voltage,   
- **green** = positive voltage,   
- **yellow** = going positive and negative,   
- **black** = zero voltage   
   
## Patching Rules   
   
   
- Patch lead must go between an output and an inp   
- Each input can only be connected to one output   
- Each output can be connected to multiple inputs   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1658195376/wiki/erlpgzewwnuuuaub3efo.png)   
   
   
- Set the audio encoding parameters. If the sound stutters increase the block size until the stutter stop   
   
   
- Frequency is measured in Hertz (Hz) – the number of times the signal does a complete oscillation in 1 second   
- Useful frequencies for sounds are about 20Hz – 20kHz   
- Frequency corresponds to the pitch of a note   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1658195519/wiki/qwd0jvr4tlnndqifzr0i.png)   
   
Adding a **VCA** to the mix   
   
## VCA   
   
Voltage Controlled Amplifier. In this context, an amplifier can change the level of a signal while keeping the same proportionate shape (and sound)   
   
**Chaining signals through modules**   
   
   
- We can chain the oscillator output signal through other modules (e.g. VCA) to further modify its sound   
- A core concept in modular synthesizers to chain a signal through modules   
- Each module in the chain can add a different modification to the signal   
- You can add as many links in the chain as you wan to achieve the sound you like   
- You can also split and combine signals to create chains that follow multiple paths   
   
## Oscilloscope   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1658196175/wiki/ftswuqzpnfp4si7sxg11.png)   
   
Patch the VCA output to IN 1. The scope shows the waveform of the electrical signal on the IN 1. Adjust the TIME knob and play around with different type of waves.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1658196388/wiki/cu0he6cpn3hp3ct33wqp.png)   
   
   
- Waveform amplitude is the loudness of the corresponding sound (Control on the VCA)   
- Waveform frequency is the pitch of the corresponding sound   
- Waveform shape is the tonal quality of the corresponding sound (roughly: the more angular, the harsher the sound)   
   
## CV   
   
**Control Voltage**   
   
Another core concept in [music.modular synth](../unsorted/music.modular%20synth.md).   
   
We can use Control Voltages (CVs) to automatically control parameters in modules   
What if we used electrical signals instead of manually turning the knobs to control the waves and their behaviour. We can use these electrical signals to automate.   
   
This type of signal is called **Control Voltage**.   
   
To generate CVs we can use:   
   
   
- Sequencer   
- Input device (could also be mod wheel, pads, key velocity etc. etc.)   
   
## SEQ 3   
   
Sequencer   
   
We can generate CVs from a sequencer.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1658199602/wiki/rokxxtvjhilnxjczjfhe.png)   
   
CV 1 from SEQ 3 to V/OCT of the VCO, Randomize SEQ 3   
   
## V/OCT   
   
1 Volt = 1 Octave change in pitch   
   
**Volt per Octave**   
   
   
- The V/OCT CV input to the oscillator will change the pitch by 1 octave for each volt at that input   
  – Equivalent to halving or doubling the frequency   
  – To move one semitone use 1/12th of a volt   
   
- `+ve` voltages go up, `-ve` voltages go down   
- Change is relative to the frequency set with the manual knobs   
   
   
- We can even chain CV signals through modules   
  – e.g. through a VCA to change the intensity of a CV   
   
- GATE is positive when a note is played   
- CV is V/OCT for the pitch of the last note   
   
## FM   
   
**Frequency Modulation** is added (FM) to the output, which is a small change in frequency controlled by a CV. Creates vibratos, slurs and zaps.   
   
## LFO   
   
**Low Frequency Oscillator**   
   
Is another important module. It should really be called a VCLFO, but I guess synth geeks like TLAs.   
   
   
- Essential functions are the same as the oscillator we already know, except it operates at lower frequencies.   
- Use it for vibrato or other repeating effects.   
- LFO SQR (square wave) outputs can also be used as “Clocks” to deliver regular pulses to modules that need pulse-inputs.   
- It has output modes: positive (UNI) and positive and negative (BI) voltage ranges.   
- `RESET` resets oscillator to the starting position (0 Volts).   
   
## ADSR   
   
An Envelope Generator, commonly **Attack-Decay-Sustain-Release** (ADSR) module.   
   
   
- ADSR is an engineer’s model of how the loudness of a musical note changes as it is played   
- Value of the ADSR parameters can be set by control knobs and CVs.   
- Normally you connect the GATE input to a GATE output from a sequencer or keyboard.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1658202139/wiki/urgnljzn4u8vfhhyhkhc.png)   
   
## Notes   
   
   
- Use a smooth analogue CV to vary the volume of a sound. Creates “natural” decay of notes and vibrato effects.   
- Add Pulse Width Modulation (PWM) to the oscillator square wave controlled by the CV. Creates “phasing” type sounds   
   
## Resources   
   
   
- [Intro to Eurorack (ft. VCV Rack)](https://youtube.com/playlist?list=PLcaEIjiwaCmTpG7i5Gm5jro0M6kXtl-zt)