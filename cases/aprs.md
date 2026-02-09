# APRS decoding

APRS decoding means taking the radio “beeps” of APRS signals and turning them back into readable data like position, messages, and telemetry.

### Introduction

APRS (Automatic Packet Reporting System) is a digital system used mainly by radio amateurs to send real‑time information such as GPS position, short text messages, and weather data.

These data are sent as short packets over VHF/UHF (for example around **144.800 Mhz in Europe** or **144.390 MHz** in many regions) and can be shown on maps or lists of stations.

### Decoding APRS

On the air, APRS packets are audio tones (**AFSK1200**) that sound like fast modem noises; a modem (TNC or software) converts those tones into digital bits.

APRS decoding is the process where software takes that bitstream (AX.25 frames), checks it, and extracts fields such as callsign, path (digipeaters used), latitude/longitude, altitude, speed, and free‑text messages.

### Decoding chain

A radio tuned to the APRS frequency outputs audio, which you feed into a sound card or dedicated modem connected to a computer or microcontroller.

Software tools such as **Direwolf** or **MultiPSK** demodulate and decode the APRS packets into text, then APRS programs (e.g., mapping software) display stations on a map or list and can log or forward them to Internet APRS servers.

### After decoding

A decoded APRS line usually shows the sender callsign, SSID (like -9 for mobile), digipeater path, timestamp, coordinates, and optional data like course, speed, or sensor values in a compact text format.

Mapping software uses the coordinates and symbol codes to draw icons (cars, balloons, weather stations, etc.) with tracks showing their movement over time.

### Quick tutorial

- run `gqrx` software defined radio
- set frequency to `144.800 Mhz`
- in `Tools` menu, chosse `AFSK1200 Decoder``
- APRS decoded packets will be displayed in new window

### See also

- [Automatic Packet Reporting System](https://www.aprs.org/)
- [Aprs.fi web service](https://aprs.fi/)
