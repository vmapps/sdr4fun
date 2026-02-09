# FM decoding

FM decoding with SDR means taking a radio signal whose frequency is wiggled by audio (frequency modulation, FM) and using software on a computer to turn that back into sound, instead of using analog radio circuitry.

## Introduction

In FM, the transmitter keeps the signal strength roughly constant but shifts the carrier frequency up and down according to the audio waveform.

An SDR (software-defined radio) stick or board converts the radio-frequency signal into digital samples (often complex I/Q samples) and sends them to your PC.

Your SDR software then does in software what a classic FM radio did with hardware: tuning, filtering, FM demodulation, and audio output.

A simple mental picture: your SDR grabs a chunk of spectrum around specific frequency, then your software “zooms in” on that station, strips away the carrier, measures how fast the signal’s phase/frequency is changing, and converts those variations into audio samples you can send to the sound card.

## Quick tutorial

- run `gqrx` software defined radio
- set center frequency to one from `87,5 MHz - 108 MHz`range
- select `WFM / WBFM / FM` decoding mode

another method could be :

- launch `rtl_fm` and redirect output to audio player

  `rtl_fm -f 96.9M -M wfm -s 180k -E deemp  | play -r 180k -t raw -e s -b 16 -c 1 -V1 - lowpass 16k`

## See also

- [Listening to FM using RTL-SDR and GQRX](https://payatu.com/blog/listening-to-fm-using-rtl-sdr-and-gqrx/)
- [Decoding FM radio Signals using SDR](https://www.hackster.io/thabiso/decoding-fm-radio-signals-using-software-defined-radio-36fa46)
- [RTL-SDR FM Receiver using GNU Radio](https://wiki.gnuradio.org/index.php?title=RTL-SDR_FM_Receiver)
