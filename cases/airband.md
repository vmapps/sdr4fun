# Airband

Airband listening is the hobby of tuning into the VHF radio frequencies used for civil aviation, mainly to hear communications between pilots and air traffic control.

## Introduction

The civil aviation **airband** is the VHF range from about **118 to 137 MHz**, used mostly for voice AM communications :

- Routine ATC like clearances, hand‑offs between tower, ground, approach/departure, and traffic information
- Airline operations between aircraft and company dispatch or ground staff, usually in the upper part of the band (**128–137 MHz**)
- Automated broadcasts like ATIS, giving weather and runway information for nearby airports
- Sometimes special-use traffic like firefighting aircraft, balloons, etc

Military aircraft typically use a separate UHF AM band roughly **220–400 MHz**, which is distinct from the civil airband.

A scanner or radio that covers **118–137** MHz in **AM** mode, or a RTL‑SDR USB dongle and SDR software could be used to listen to airband communications. An antenna tuned for around **120–130 MHz**; even a simple quarter‑wave ground‑plane or an “airband” whip placed high and in the clear greatly improves reception.

![](https://i.ytimg.com/vi/yIuU8ROYGVE/maxresdefault.jpg)

_(source: youtube.com)_

## Quick tutorial

- run `gqrx` software defined radio
- set center frequency to one from `118 MHz - 137 MHz` range
- select `AM` decoding mode

another method could be :

- launch `rtl_fm` and redirect output to audio player

  ```
  GAIN=20
  SQUELCH=-150
  RATE=48k
  VOLUME=50
  FREQ=131M:134M:33k

  rtl_fm -M am -g ${GAIN} -s ${RATE} -l ${SQUELCH} -f ${FREQ} \
    | play --volume ${VOLUME} --rate ${RATE} --type raw --encoding s --bits 16 --channels 1 -V3 -
  ```

## Legal considerations

Laws differ by country: in some places, merely listening to airband without a license is an offense; in others (like the UK), listening to navigation/weather-related transmissions is allowed but rebroadcasting or using the information operationally can be restricted.

Transmitting on airband without proper authorization is illegal and potentially dangerous everywhere; this hobby is strictly receive‑only.

## See also

- [RTL-SDR for VHF Air Band AM on GNU Radio](https://jeremyclark.ca/wp/telecom/rtl-sdr-for-vhf-air-band-am-on-gnu-radio/)
- [Live ATC](https://www.liveatc.net/)
- [Listening to air band voices](https://edwardstark.website/listening-to-air-band-voices/)
- [Listening to Air Traffic control using SDR Radio](https://www.youtube.com/watch?v=yIuU8ROYGVE)
