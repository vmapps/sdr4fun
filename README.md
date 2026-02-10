# sdr4fun

Sharing various stuff on Software-Defined Radio :

- [Introduction](#introduction)
- [Hardware](#hardware)
- [Software](#software)
- [WebSDR](#websdr)
- [Tools](#tools)
- [Use-cases](#use-cases)
- [Scripts](#scripts)
- [Resources](#resources)
- [References](#references)

## Introduction

[Software-defined radio](https://en.wikipedia.org/wiki/Software-defined_radio) also named SDR, is a radio communication system where components that conventionally have been implemented in analog hardware (e.g. mixers, filters, amplifiers, modulators/demodulators, detectors, etc.) are instead implemented by means of software on a computer or embedded system (source: Wikipedia).

> **Important note**
>
> Listening and decoding communications is generally allowed, but recording or sharing communications, or trying to break encryption, may be restricted by local law in your country.

## Hardware

An SDR (software defined radio) hardware device is the physical radio front end that converts real-world radio waves into digital samples (and back), so that almost all signal processing can be done in software.

SDR hardware typically includes:

- RF front end (tuner, low-noise amplifiers, filters) to select and condition a band of frequencies
- High‑speed ADCs (and often DACs) that digitize incoming RF (and synthesize outgoing RF) as raw I/Q samples
- A programmable processing section such as FPGA, DSP, SoC, or a USB/ethernet interface to stream samples to a host computer for software processing

In short, “SDR hardware” is the configurable radio front-end plus converters and processing/IO that replace most traditional fixed-function RF circuitry (mixers, demodulators, etc.) with a flexible, software-controlled platform.

There are a few hardware devices you could use to start playing with SDR:

| Vendor                                                             | Device        | Frequencies         |
| ------------------------------------------------------------------ | ------------- | ------------------- |
| Generic                                                            | DVB-T tuner   | 24 Mhz - 1.766 Ghz  |
| [RTL-SDR Blog](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/) | RTL-SDR v3/v4 | 500 kHz – 1.766 GHz |
| [Nooelec](https://www.nooelec.com/store/)                          | NESDR SMArt   | 100 kHz - 1.750 GHz |
| [Great Scott Gadgets](https://greatscottgadgets.com/hackrf/one/)   | HackRF One    | 1 MHz - 6 GHz       |

Note that frequency range depends on device architecture and some bands could require specific sampling mode.

## Software

SDR software refers to the programs and applications used in Software-Defined Radio (SDR) systems. These replace traditional hardware components like mixers, filters, and modulators with software running on general-purpose computers or embedded processors.

SDR software processes radio signals digitally after an analog-to-digital converter captures RF input, enabling flexible tuning, demodulation, and protocol support without hardware changes. It handles tasks like filtering, frequency modulation, and signal enhancement for applications from amateur radio to 5G testing.

SDR software typically includes:

- Switching frequencies, modes (e.g., FM, SSB, digital), or standards via software updates
- Hardware pairing with SDR devices featuring FPGAs, DSPs, or sound cards as the RF front end
- Spectrum monitoring, prototyping wireless systems, and real-time analysis in labs or field tests

There are a few software applications you could use to start playing with SDR:

| Author            | Software                                                           | Platforms                  |
| ----------------- | ------------------------------------------------------------------ | -------------------------- |
| Charles J. Cliffe | [CubicSDR](https://github.com/cjcliffe/CubicSDR)                   | Windows, Linux, MacOS      |
| Alexandru Csete   | [Gqrx](https://github.com/gqrx-sdr/gqrx)                           | Windows, Linux, MacOS      |
| Edouard Griffiths | [SDR Angel](https://github.com/f4exb/sdrangel)                     | Windows, Linux, MacOS      |
| SDR-radio.com     | [SDR Console](https://www.sdr-radio.com/Console)                   | Windows                    |
| Alexandre Rouma   | [SDR++](https://github.com/AlexandreRouma/SDRPlusPlus) (SDR Sharp) | Windows, Linux, MacOS, BSD |
| Airspy            | [SDR#](https://airspy.com/download/) (SDR Plus Plus)               | Windows                    |

## WebSDR

A WebSDR is a software-defined radio receiver that is connected to the internet and can be tuned and listened to by many users at the same time via a web browser. In practice, it means someone hosts a radio and antenna at their location, and you control that receiver remotely from your computer or phone.

There are various benefits to adopt WebSDR :

- No hardware/software required : You can listen to shortwave, amateur bands, and other signals without buying a radio, antenna, or SDR dongle yourself, which is ideal for beginners or people in apartments
- Global access : You can use receivers located all over the world, so you can hear stations and propagation conditions that are impossible to receive from your own location
- Better reception than at home : Many servers use good antennas and low-noise locations, so reception quality can exceed that of a typical urban home setup
- Learning and experimentation: WebSDR lets you see whole bands on a waterfall display, explore different modes (AM, FM, SSB, CW, digital), and learn about SDR concepts without needing to install software or drivers
- Convenience and portability : Everything runs in a browser, so it works from almost any device and OS with just an internet connection, with no complex setup

Thanks to the amateur radio club ETGD at the University of Twente, you can listen to and control a short-wave receiver with their [Wide-band WebSDR](http://websdr.ewi.utwente.nl:8901/). Launched in 2008, it is the very first WebSDR site ever.

## Tools

There are a few software add-ons you could also use to start playing with SDR:

- [direwolf](https://github.com/wb2osz/direwolf) : Decoded Information from Radio Emissions for Windows Or Linux Fans
- [dsd](https://github.com/szechyjs/dsd) : decoder for several digital voice formats
- [dump1090](https://github.com/antirez/dump1090) : Mode S decoder specifically designed for RTLSDR devices
- [multimon-ng](https://github.com/EliasOenal/multimon-ng) : decoder for multiple protocols
- [rtl-sdr](https://osmocom.org/projects/rtl-sdr/wiki) : RTL drivers and utils
- [rtl_433](https://github.com/merbanan/rtl_433) : generic data receiverfor 433/868/325/345/915 MHz bands
- [Qtmm AFSK1200 Decoder](https://sourceforge.net/projects/qtmm/)

## Use Cases

There are a few use-cases you could consider to start playing with SDR:

- Airband traffic
- [AM radios](cases/am.md)
- [ADS-B tracking](cases/ads-b.md)
- [APRS decoding](cases/aprs.md)
- [FM radios](cases/fm.md)
- HAM radio
- ISS Radio & TV
- LPD433 decoding
- NOAA-APT 15/18/19
- Numbers stations
- OTH Radar monitoring
- [PMR446 decoding](cases/pmr446.md)
- POCSAG decoding

## Scripts

Some scripts to use for SDR.

**Scanning Airband**

```
GAIN=50
SQUELCH=-20
FREQ=118M:137M:25k
RATE=12k

rtl_fm -M am -f ${FREQ} -s ${RATE} -g ${GAIN} -l ${SQUELCH} \
 | play --volume ${VOLUME} --rate ${RATE} --type raw --encoding s --bits 16 --channels 1 -V3 -
```

**Listening to FM station**

```
FREQ=105.5M
PPM=-36
GAIN=50
SQUELCH=0

rtl_fm -g ${GAIN} -f ${FREQ}M -M fm -s 180k -E deemp -p ${PPM} -l ${SQUELCH} \
 | play --rate 180k --type raw --encoding s --bits 16 --channels 1 -V2 - lowpass 16k
```

**Decoding PMR flows**

```
PORT=7355

ncat -l -u -p ${PORT} \
 | dsd -i - -o pa:1
```

**Decoding POCSAG flows**

```
PORT=7355

ncat -l -u -p ${PORT} \
 | sox --type raw -esigned-integer --bits 16 --rate 48000 - --type raw -esigned-integer --bits 16 --rate 22050 - \
 | multimon-ng -n -t raw -p -a POCSAG512 -a POCSAG1200 -a POCSAG2400 -a FLEX -a FLEX_NEXT -f auto --timestamp /dev/stdin
```

## Resources

There are a few web resources helpful when you would start playing with SDR:

- [Priyom.org](https://priyom.org/) : international group of radio enthusiasts seeking out mysterious stations
- [Signal Identification Guide](https://www.sigidwiki.com/wiki/Signal_Identification_Guide) : wiki to help identifying radio signals through sounds samples and waterfall images
- [WebSDR.org](http://websdr.org/) : project providing web access to worldwide SDR receivers covering complete shortwave spectrum

## References

Please find below some links to useful Wikipedia articles on various topics related to SDR:

- [Airband](https://en.wikipedia.org/wiki/Airband)
- [ALS162 time signal
  ](https://en.wikipedia.org/wiki/ALS162_time_signal)
- [AM broadcasting](https://en.wikipedia.org/wiki/AM_broadcasting)
- [Amateur Radio](https://en.wikipedia.org/wiki/Amateur_radio) (HAM)
- [Amateur Radio on the International Space Station](https://en.wikipedia.org/wiki/Amateur_Radio_on_the_International_Space_Station) (ARISS)
- [Automatic Dependent Surveillance Broadcast](https://en.wikipedia.org/wiki/Automatic_Dependent_Surveillance%E2%80%93Broadcast) (ADS-B)
- [Automatic Packet Reporting System](https://en.wikipedia.org/wiki/Automatic_Packet_Reporting_System) (APRS)
- [Automatic picture transmission
  ](https://en.wikipedia.org/wiki/Automatic_picture_transmission) (APT)
- [Duga radar](https://en.wikipedia.org/wiki/Duga_radar) (aka _Russian Woodpecker_)
- [Earth–Moon–Earth communication](https://en.wikipedia.org/wiki/Earth%E2%80%93Moon%E2%80%93Earth_communication) (Moon bouncing)
- [FM broadcasting](https://en.wikipedia.org/wiki/FM_broadcasting)
- [GRAVES System](<https://en.wikipedia.org/wiki/GRAVES_(system)>)
- [Low Power Device 433 MHz](https://en.wikipedia.org/wiki/LPD433) (LPD433)
- [Meteor burst communications](https://en.wikipedia.org/wiki/Meteor_burst_communications) (Meteor Scatter)
- [Numbers station](https://en.wikipedia.org/wiki/Numbers_station)
- [Over-the-horizon radar](https://en.wikipedia.org/wiki/Over-the-horizon_radar) (OTH radar)
- [Private Mobile Radio, 446 MHz](https://en.wikipedia.org/wiki/PMR446) (PMR446)
- [Radio-paging code No. 1](https://en.wikipedia.org/wiki/POCSAG) (POCSAG)
- [UVB-76](https://en.wikipedia.org/wiki/UVB-76) (aka _The Buzzer_)
- [VHF omnidirectional range](https://en.wikipedia.org/wiki/VHF_omnidirectional_range)
