# wer.si

Welcome to the Wersi MK1/EX20 synthesizer knowledge base.

This site provides the necessary tools and information to be able to edit the sounds in your synthesizer.

___

## TL;DR

The editor is a piece of web software that runs on a modern browser in your host computer and communicates to your synthesizer over MIDI. Due to some bugs in the synthesizer's firmware, you'll have to update your synthesizer's firmware before attempting to run the editor.

To get started:

1. Update your synthesizer's firmware. Program your own ([github.com/ijsf/wersi-mk1-ex20-re](https://github.com/ijsf/wersi-mk1-ex20-re)) or order one on [Tindie](https://www.tindie.com/products/uy725ad/wersi-mk1ex20-synthesizer-eeproms/) (availability may be limited).
2. Power on your synthesizer and hook it up to your computer using a MIDI interface.
3. Make sure you have a compatible browser on your computer capable of WebMIDI (e.g. the latest Chrome or Chromium-based browser with default settings should work).
4. Use your web browser to browse to the web editor at [https://ijsf.github.io/wersi-mk1-editor](https://ijsf.github.io/wersi-mk1-editor). Follow the instructions and it should start communicating with your synthesizer.
5. With any luck, you can now start editing your synth sounds.

Please remember that the editor is highly experimental software that contains bugs and does not come with any guarantees. It is open-source software, and any help is much appreciated!
___

This place has been set up to provide a small knowledge base on these synthesizers, including information on:

* Development of a modern open source browser-based editor.
* Firmware documentation and patches.
* People using the MK1 / EX20 synthesizers.

The MK1 series likely faded into obscurity due to various design flaws and issues with the synthesizer itself, such as the notoriously difficult programming interface, uninspired factory presets, absence of editing tools and a lack of focus, further worsened by a halt in development due to a series of manufacturer bankruptcies.

Major efforts in reverse engineering and tracking down original documentation have resulted in the development of this editor, with the sole purpose being to overcome its design flaws and expose as much of the potential sound synthesis capabilities as possible in a modern and convenient way. To revive the purpose of this remarkable and digitally pioneering vintage synthesizer.

The fact that you are on this page likely means that you are one of the few owners of an original Wersi MK1 or EX20 synthesizer. Sit tight, as you will now finally be able to properly use this synthesizer to your heart's content.

## Sound demos

We would very much like to list some sound demos here. Contact me for more information (see below)!

## Editor

Welcome to the long - since 1988 - awaited editor for the Wersi MK1 / EX-20 synthesizers!

The repository at [github.com/ijsf/wersi-mk1-editor](https://github.com/ijsf/wersi-mk1-editor) is currently under active development, and its current state is considered to be *alpha*. This means that setting up the editor will likely require some technical skill, and bugs will be present.

The goal behind this editor is to unlock the Wersi MK1's full sound synthesis potential, by creating a modern and user friendly interface to manipulate its sound synthesis. As such, a large effort has gone into reverse engineering the internal hardware, as well as its MIDI SysEx interface.

For browser compatibility, we recommend the latest version of Chrome or Chromium-based browsers. Compatibility beyond these browsers has not been tested as of yet.

The editor is hosted at [https://ijsf.github.io/wersi-mk1-editor](https://ijsf.github.io/wersi-mk1-editor) and attempts to establish a connection to your synthesizer by using the Web MIDI API.

<img src="https://raw.githubusercontent.com/ijsf/wer.si/master/snapshot5.png">

## Hardware documentation

At first sight, the interface of the MK1 suggests that it is a simple additive synthesizer capable of adding 32 sine harmonics, similar to the registers of an electric organ.

However, the MK1 actually contains an elaborate implementation of *digital wavetable synthesis*, and came fitted with up to *22 CPUs*!

Wavetables are used as basis for sound generation, consist of 64 of 32 samples each and are interpolated and resampled to any note frequency after which they are modulated with complex amplitude and frequency envelopes. Fourier transforms are used to translate between the harmonic sliders on the synth's front panel and the actual sound synthesis modules.

Its main logic consists of two *Motorola 68B09 CPUs* (main + coprocessor) with 32 KiB of program ROM, 16 KiB of voice preset ROM, 16 KiB RAM for user programmable presets, 8 KiB slave RAM (256 bytes for each slave CPU) and 8 KiB work RAM for the master CPU.

More information:

* [fixing firmware bugs from 1987 in 2017 @ bitlog.it](http://bitlog.it/re/fixing-firmware-bugs-from-1987-in-2017/)
* [old school firmware dumping @ bitlog.it](http://bitlog.it/re/old-school-eprom-firmware-dumping/)
* [github.com/ijsf/wersi-mk1-ex20-re](https://github.com/ijsf/wersi-mk1-ex20-re)

#### Sound synthesis

Voice sound synthesis is fully digital (e.g. without VCO or DCO), performed by a *Zilog Z8611 CPU (Z8)* + *NatSemi 0832 DAC* (8-bit), two of which are located on a single *SL-M2* slave sound module. The MK1 synthesizer can be fitted with as much as 10 SL-M2 modules, enabling 20 individual polyphonic voices through a total of 20 CPUs.

#### Envelope modulation

Envelopes for amplitude and frequency modulation can be programmed through a set of predefined envelope modules, each of which can be chained after one another to provide changing ever-changing modulation as time progresses. All envelope calculations are performed by a second *Motorola 68B09 CPU* (coprocessor) and are converted to analog using a *NatSemi 1232 DAC* (12-bit).

#### Analog filters

Each SL-M2 sound module contains an optional analog low-pass filter ("Bright"). Subsequently, all 20 sound module voices are combined and fed through a single *AF-20* or *AF-21* (depending on version) analog filter module, containing a digitally controlled switched capacitor filter (AF-20) or a *SSM2044* analog VCF, mono distortion stage, mono noise stage, stereo phase effect stage ("WersiVoice") and finally a noise-reduction stage ("Dynafex").

Additionally, an optional <strong>DH-10</strong> or <strong>DH-11</strong> filter module mixes reverb, delay and compression into the final audio output.

___

This project is no way affiliated with, authorized, maintained, sponsored or endorsed with Wersi nor any of its affiliates or subsidiaries.

> wersi@ijsf.nl

