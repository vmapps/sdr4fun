# AIS decoding

AIS decoding is the process of taking the raw radio signal from ships’ AIS transmissions and turning it into human‑readable information like vessel name, position, speed, and course.

### Introduction

AIS (Automatic Identification System) is a safety system where ships automatically broadcast their identity, GPS position, speed, and course over VHF radio so other ships and shore stations can track them and avoid collisions.

These broadcasts are short digital messages sent on specific marine VHF channels (around 162 MHz) using a modulation called GMSK at 9 600 bits per second.

### Decoding AIS

An AIS receiver captures the raw audio/data signal and a decoder then interprets the bits according to the AIS standard message format.

The decoder extracts fields such as MMSI (unique ship ID), latitude/longitude, speed over ground, course over ground, heading, ship type, and status, and outputs them as readable text or NMEA sentences that chartplotters and software can use.

### Decoding setup

Hardware: a **161.975 MHz (AIS 1)** and/or **162.025 MHz** capable receiver, commonly a cheap USB RTL‑SDR dongle plus an antenna tuned near **162 MHz**.

Software: a decoder like **AIS-catcher** or similar, which demodulates the signal, parses the AIS messages, and can feed them to a map display showing ships around you in real time.

### After decoding

For each ship you usually see its MMSI, callsign, position, and speed, updated frequently.

Many online services (e.g., radar‑style maps) are built from thousands of hobbyists doing AIS decoding at home and sharing their local ship data.

![](https://www.aisfriends.com/images/static/aiscatcher/AIS%20Catcher%20Live%20Map.png)

_(screenshot from aisfriends.com)_

### Quick tutorial

- launch `AIS-catcher` in interactive mode

  `./AIS-catcher -N 8100`

- connect with your browser to see live traffic

  `http://localhost:8100`

### See also

- [Automatic Identification System (AIS)](https://www.sigidwiki.com/wiki/AIS) at sigidwiki.com
- [AIS Catcher community](https://www.aiscatcher.org/l)
- [AIS Friends network](https://www.aisfriends.com/)
- [Maritime Mobile Service Identity (MMSI)](https://en.wikipedia.org/wiki/Maritime_Mobile_Service_Identity)
