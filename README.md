# Frequency Response

## What is this?

To measure the audio response of any transmitter, you can generate an audio file, transmit it, receive it, record it and compare the spectrograms between the original and the recorded audio. Adjusting filters, equalisers, gain and other transceiver settings will result in the spectrogram changing.

This branch implements a website that updates when a new recording is created. It does so by creating a spectrogram for each recording, then generating a new index.html page and uploading the page and the matching images.

Every day it removes images that are older than 24 hours and updates the website.

The website is [hosted by an AWS S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) and the [aws-cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) is used to synchronise the data.

This is implemented on a Raspberry Pi 2B, and uses a Yaesu FT-857d connected to a Diamond X300N antenna for receive. The sound card is a generic external USB card connected between the pi and the radio, sampling at 48 kHz.

Some example spectrograms can be found on the [project page](https://projects.vk6flab.com/projects/rtl-sdr-projects/frequency-response).

## Software

This collection of [bash](https://tiswww.case.edu/php/chet/bash/bashtop.html) scripts relies heavily on [SoX](http://sox.sourceforge.net/) which is a cross-platform (Windows, Linux, MacOS X, etc.) command line utility that can convert various formats of computer audio files in to other formats. It also has the ability to generate spectrograms.

The scripts generate a spectrogram every minute for any audio files that don't yet have a spectrogram. If a spectrogram is created, it sets a flag to generate a new index.html file. Every five minutes the flag is checked and if it exists, it generates a new index.html file, ignoring audio files with no data. When it completes, it sets a flag to tell the aws_upload script to upload the new files.

Every day a script is run to delete all audio and spectrograms that are older than 24 hours. It then sets the flag to create a new index.html file.

## Usage

- create a /home/pi/bin directory
- clone this branch into that directory
- make a /home/pi/audio directory
- setup your radio to have squelch on, so there is silence between each transmission, I use TSQ on my radio
- configure an [AWS S3 bucket as a website](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)
- update the user crontab with the supplied crontab (use crontab -e)

## Prerequisites

- bash
- SoX
- aws-cli

## Author

Onno (VK6FLAB) [cq@vk6flab.com](mailto:cq@vk6flab.com)
