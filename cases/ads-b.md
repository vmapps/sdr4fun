# ADS-B decoding

ADS‑B decoding is the process of receiving and translating the digital radio signals that aircraft broadcast into readable information like position, altitude, speed, and callsign.

### Introduction

ADS‑B means Automatic Dependent Surveillance‑Broadcast, a surveillance technology used in aviation so aircraft can be tracked without traditional radar.

Each equipped aircraft regularly broadcasts short digital messages that include its GPS‑derived position, altitude, velocity, and identity on a specific frequency (usually **1090 MHz**).

### Decoding ADS-B

In the air, ADS‑B messages are transmitted as a stream of radio pulses (pulse‑position modulation) at **1090 MHz**, not as audio tones like APRS.

Decoding means capturing those RF pulses with a receiver, turning them into bits, and then interpreting the bits as fields such as latitude/longitude, barometric altitude, ground speed, vertical rate, and emergency status.

### Decoding setup

Hardware: a **1090 MHz**‑capable receiver, commonly a cheap USB RTL‑SDR dongle plus an antenna tuned near **1090 MHz**.

Software: a decoder like **dump1090** or similar, which demodulates the signal, parses the ADS‑B messages, and can feed them to a map display showing aircraft around you in real time.

### After decoding

For each aircraft you usually see its hex address, callsign or flight number, position, altitude, heading/track, and speed, updated roughly once per second.

Many online services (e.g., radar‑style maps) are built from thousands of hobbyists doing ADS‑B decoding at home and sharing their local aircraft data.

![](https://www.rtl-sdr.com/wp-content/uploads/2013/04/dump1090.png)
_(screenshot from rtl-sdr.com)_

### Quick tutorial

- launch `dump1090` in interactive mode

  `./dump1090 --interactive --net`

- connect with your browser to see live traffic

  `http://localhost:8080`

### See also

- [ADS-B Exchange community](https://www.adsbexchange.com/)
- [ADS-B using dump1090 for the Raspberry Pi](https://www.satsignal.eu/raspberry-pi/dump1090.html)
