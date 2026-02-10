# AM decoding

AM decoding with SDR involves using a software-defined radio to receive and process amplitude-modulated signals, extracting the original audio information from radio broadcasts.

## Introduction

Amplitude modulation (AM) encodes audio onto a carrier wave by varying its amplitude while keeping frequency constant. A typical AM signal looks like a high-frequency carrier with the audio waveform "riding" on its peaks, often visualized in SDR software as a spectrogram or IQ plot.

## Decoding AM

To decode, SDR software tunes to the AM frequency, applies a demodulator (like envelope detection), and outputs audio. Steps include: tune receiver, apply AM demod block (e.g., in GNU Radio or SDR#), filter noise, and downsample for playback at rates like 8 kHz. The result is clear audio from stations like medium-wave broadcasts.

![](https://web.stanford.edu/class/ee26n/Assignments/graphics/AB_310.8.png)

_(source: stanford.edu)_

## Quick tutorial

- run `gqrx` software defined radio
- set center frequency to one around `388 MHz` or any other AM band
- select `AM` decoding mode

## See also

- [Amplitude Modulation (AM)](<https://www.sigidwiki.com/wiki/Amplitude_Modulation_(AM)>) at sigidwiki.com
- [RTL-SDR for AM on GNU Radio](https://jeremyclark.ca/wp/telecom/rtl-sdr-for-am-on-gnu-radio/)
- [How to Demodulate an AM/FM Signal Using Software](https://eureka.patsnap.com/article/how-to-demodulate-an-amfm-signal-using-software-sdr-example)
