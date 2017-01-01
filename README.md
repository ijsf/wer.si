# wer.si

Welcome to the strange world of Wersi MK1 / EX20 synthesizers.

Known as a notoriously difficult and impractical digital synthesizer originally manufactured in the 1980's by West-German manufacturer Wersi, only hardcore button bashing and deep programming would unlock some of its unique and remarkable digital wavetable sound.

Until today.

___

This place has been set up to provide a small knowledge base on these synthesizers, including information on:

* Development of a modern open source browser-based editor.
* Firmware documentation and patches.
* People using the MK1 / EX20 synthesizers.

The MK1 series likely faded into obscurity due to various design flaws and issues with the synthesizer itself, such as the notoriously difficult programming interface, uninspired factory presets, absence of editing tools and a lack of focus, further worsened by a halt in development due to a series of manufacturer bankruptcies.

Major efforts in reverse engineering and tracking down original documentation have resulted in the development of this editor, with the sole purpose being to overcome its design flaws and expose as much of the potential sound synthesis capabilities as possible in a modern and convenient way. To revive the purpose of this remarkable and digitally pioneering vintage synthesizer.

The fact that you are on this page likely means that you are one of the few owners of an original Wersi MK1 or EX20 synthesizer. Sit tight, as you will now finally be able to properly use this synthesizer to your heart's content.

## Editor

A modern browser-based editor is currently under development and test, and will soon be released as an open source project.

<img src="https://pbs.twimg.com/media/CvZI_mvWEAAGYRq.jpg:large" height="400px">

## Firmware

Up-to-date information on firmware development can be found at:

[github.com/ijsf/wersi-mk1-ex20-re](https://github.com/ijsf/wersi-mk1-ex20-re)

More information:

* [old school firmware dumping @ bitlog.it](http://bitlog.it/re/old-school-eprom-firmware-dumping/)

## Hardware documentation

At first sight, the interface of the MK1 suggests that it is a simple additive synthesizer capable of adding 32 sine harmonics, similar to the registers of an electric organ.

However, the MK1 actually contains an elaborate implementation of *digital wavetable synthesis*, and came fitted with up to *22 CPUs*!

Wavetables are used as basis for sound generation, consist of 64 of 32 samples each and are interpolated and resampled to any note frequency after which they are modulated with complex amplitude and frequency envelopes. Fourier transforms are used to translate between the harmonic sliders on the synth's front panel and the actual sound synthesis modules.

Its main logic consists of two *Motorola 68B09 CPUs* (main + coprocessor) with 32 KiB of program ROM, 16 KiB of voice preset ROM, 16 KiB RAM for user programmable presets, 8 KiB slave RAM (256 bytes for each slave CPU) and 8 KiB work RAM for the master CPU.

#### Sound synthesis

Voice sound synthesis is fully digital (e.g. without VCO or DCO), performed by a *Zilog Z8611 CPU (Z8)* + *NatSemi 0832 DAC* (8-bit), two of which are located on a single *SL-M2* slave sound module. The MK1 synthesizer can be fitted with as much as 10 SL-M2 modules, enabling 20 individual polyphonic voices through a total of 20 CPUs.

#### Envelope modulation

Envelopes for amplitude and frequency modulation can be programmed through a set of predefined envelope modules, each of which can be chained after one another to provide changing ever-changing modulation as time progresses. All envelope calculations are performed by a second *Motorola 68B09 CPU* (coprocessor) and are converted to analog using a *NatSemi 1232 DAC* (12-bit).

#### Analog filters

Each SL-M2 sound module contains an optional analog low-pass filter ("Bright"). Subsequently, all 20 sound module voices are combined and fed through a single *AF-20* or *AF-21* (depending on version) analog filter module, containing a digitally controlled switched capacitor filter (AF-20) or a *SSM2044* analog VCF, mono distortion stage, mono noise stage, stereo phase effect stage ("WersiVoice") and finally a noise-reduction stage ("Dynafex").

Additionally, an optional <strong>DH-10</strong> or <strong>DH-11</strong> filter module mixes reverb, delay and compression into the final audio output.

___

This project is no way affiliated with, authorized, maintained, sponsored or endorsed with Wersi nor any of its affiliates or subsidiaries.

> ijsf@wer.si
