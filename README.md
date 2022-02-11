# Frequency Response

## What is this?

To measure the audio response of your transmitter, you can generate an audio file, transmit it, receive it, record it and compare the spectrograms between the original and the recorded audio. Adjusting filters, equalisers, gain and other transceiver settings will result in the spectrogram changing.

Note that I'm using a Raspberry Pi, an RTLSDR dongle, an antenna, a Yaesu FT-857d and a dummy load. This is **NOT** required. See below for details.

Some examples can be found on the [project page](https://projects.vk6flab.com/projects/rtl-sdr-projects/frequency-response).

## Hardware

The transmit hardware is a Yaesu FT-857d connected to a dummy load, using 5 Watts FM.

The receive hardware is a [Raspberry Pi](https://www.raspberrypi.org/) connected to an [RTL SDR v3 dongle](https://www.rtl-sdr.com/rtl-sdr-blog-v-3-dongles-user-guide/) with a telecopic rabbit ear antenna (that came with the dongle).

## Alternative Hardware

This project will work just as well using alternative hardware. Although I'm using the specified hardware, the aim is to get an audio file to play on a transmitter and to record it off air from a receiver. If you have digital modes like FT8 or WSPR working, you're most of the way there.

You can even use simpler tools than that. For example, you can play the audio file with your mobile phone into the microphone of your radio and record it off air with your computer, or a handheld recorder.

## Software

This collection of tools relies heavily on [SoX](http://sox.sourceforge.net/) which is a cross-platform (Windows, Linux, MacOS X, etc.) command line utility that can convert various formats of computer audio files in to other formats. It also has the ability to generate spectrograms.

The audio is received by a dongle using [rtl_fm](http://kmkeen.com/rtl-demod-guide/).

## Usage

- Generate the audio sweep files using `make_sweep`.
- Pick a transmitter frequency that both the transmitter and receiver can tune to. Pay attention to the bandplan in your country!
- Start recording with `record-fm` - example: `record-fm 146.450M 55`
- Transmit audio with `auto_cq` - example: `auto_cq fm.double-sweep.48k.wav`
- Adjust your transmitter gain or any other setting you want to explore: TX filter, Clarifier, VOX-gain, etc.
- Experiment with receive settings, RX filter, etc.
- Stop `auto_cq` using Ctrl-C.
- Stop `record-fm` using Ctrl-C.
- Create spectrograms using `spectrogram` - example: `spectrogram *.wav`
- Compare the pictures.

## Prerequisites

- sox
- rtl_fm (optional)

## Author

Onno (VK6FLAB) [cq@vk6flab.com](mailto:cq@vk6flab.com)
