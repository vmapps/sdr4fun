# sdr4fun

Sharing various stuff on Software-Defined Radio :

- [Introduction](#introduction)
- [Hardware](#hardware)
- [Software](#software)
- [Tools](#tools)
- [Use-cases](#use-cases)
- [Scripts](#scripts)
- [Resources](#resources)
- [References](#references)

## Introduction

> _[Software-defined radio](https://en.wikipedia.org/wiki/Software-defined_radio) also named SDR is a radio communication system where components that conventionally have been implemented in analog hardware (e.g. mixers, filters, amplifiers, modulators/demodulators, detectors, etc.) are instead implemented by means of software on a computer or embedded system (source: Wikipedia)._

## Hardware

There are a few hardware devices you could use to start playing with SDR:

| Vendor                                                             | Device        | Frequencies         |
| ------------------------------------------------------------------ | ------------- | ------------------- |
| Generic                                                            | DVB-T tuner   | 24 Mhz - 1.766 Ghz  |
| [RTL-SDR Blog](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/) | RTL-SDR v3/v4 | 500 kHz – 1.766 GHz |
| [Nooelec](https://www.nooelec.com/store/)                          | NESDR SMArt   | 100 kHz - 1.750 GHz |
| [Great Scott Gadgets](https://greatscottgadgets.com/hackrf/one/)   | HackRF One    | 1 MHz - 6 GHz       |

Note that frequency range depends on device architecture and some bands could require specific sampling mode.

## Software

There are a few software applications you could use to start playing with SDR:

| Author            | Software                                                           | Platforms                  |
| ----------------- | ------------------------------------------------------------------ | -------------------------- |
| Charles J. Cliffe | [CubicSDR](https://github.com/cjcliffe/CubicSDR)                   | Windows, Linux, MacOS      |
| Alexandru Csete   | [Gqrx](https://github.com/gqrx-sdr/gqrx)                           | Windows, Linux, MacOS      |
| Edouard Griffiths | [SDR Angel](https://github.com/f4exb/sdrangel)                     | Windows, Linux, MacOS      |
| SDR-radio.com     | [SDR Console](https://www.sdr-radio.com/Console)                   | Windows                    |
| Alexandre Rouma   | [SDR++](https://github.com/AlexandreRouma/SDRPlusPlus) (SDR Sharp) | Windows, Linux, MacOS, BSD |
| Airspy            | [SDR#](https://airspy.com/download/) (SDR Plus Plus)               | Windows                    |

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

### Airband traffic

### AM radios

### ADS-B tracking

### APRS decoding

- APRS (Automatic Packet Reporting System) is a digital system used mainly by radio amateurs to send real‑time information such as GPS position, short text messages, and weather data.

- These data are sent as short packets over VHF/UHF (for example around **144.800 Mhz in Europe** or **144.390 MHz** in many regions) and can be shown on maps or lists of stations.

- On the air, APRS packets are audio tones (**AFSK1200**) that sound like fast modem noises; a modem (TNC or software) converts those tones into digital bits.

- APRS decoding is the process where software takes that bitstream (AX.25 frames), checks it, and extracts fields such as callsign, path (digipeaters used), latitude/longitude, altitude, speed, and free‑text messages.

- A radio tuned to the APRS frequency outputs audio, which you feed into a sound card or dedicated modem connected to a computer or microcontroller.

- Software tools such as **Direwolf** or **MultiPSK** demodulate and decode the APRS packets into text, then APRS programs (e.g., mapping software) display stations on a map or list and can log or forward them to Internet APRS servers.

- See also:
  - https://www.aprs.org/
  - https://aprs.fi/

### What you see after decoding

- A decoded APRS line usually shows the sender callsign, SSID (like -9 for mobile), digipeater path, timestamp, coordinates, and optional data like course, speed, or sensor values in a compact text format. [reddit](https://www.reddit.com/r/APRS/comments/kz50w8/how_to_decode_aprs_messages/)
- Mapping software uses the coordinates and symbol codes to draw icons (cars, balloons, weather stations, etc.) with tracks showing their movement over time. [en.wikipedia](https://en.wikipedia.org/wiki/Automatic_Packet_Reporting_System)

If you tell me what hardware or software you have (for example SDR, handheld radio, Raspberry Pi), I can outline concrete steps for you to start decoding APRS yourself.

### FM radios

### HAM radio

### ISS Radio & TV

### LPD433 decoding

### NOAA-APT 15/18/19

### Numbers stations

### OTH Radar monitoring

### PMR446 decoding

### POCSAG decoding

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

- [Priyom.org](https://priyom.org/)
- [Signal Identification Guide](https://www.sigidwiki.com/wiki/Signal_Identification_Guide)
- ...

## References

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
