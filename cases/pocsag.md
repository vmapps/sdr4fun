# POCSAG decoding

POCSAG decoding is the process of taking a radio signal used by pagers and turning it back into the original bits and text messages that were sent.

## Introduction

POCSAG (Post Office Code Standardisation Advisory Group) is a digital paging protocol used to send short messages (numeric or text) over radio.
​
It uses simple frequency shift keying (**FSK**): one audio/radio frequency represents a binary 0 and another represents a 1, at bit rates of 512, 1200, or 2400 bits per second.

When a pager transmission happens, the over‑the‑air bit stream has a defined structure:

- A preamble: at least 576 bits of alternating 0 and 1 (…010101…), used for clock and receiver synchronization and for “waking up” pagers
- Then batches of data: each batch starts with a special 32‑bit sync codeword (frame sync), followed by 16 other 32‑bit codewords which are either addresses or message data
- Each 32‑bit codeword contains:
  - 21 bits of actual information (address or message bits)
  - 10 bits of error‑correcting code (BCH code)
  - 1 parity bit

Pagers are logically grouped into 8 “frames”, and each pager only listens to its assigned frame to save power.

## Decoding POCSAG

POCSAG decoding typically involves these steps:

1. Receive and demodulate the signal

- A radio receiver (scanner, SDR, etc.) is tuned to the pager frequency and outputs baseband audio of the FSK signal
- Software then looks at that audio and converts the two tones into a stream of 0/1 bits at the correct baud rate

2. Find preamble and sync

- The decoder searches the bit stream for the long 010101… preamble and then for the fixed sync codeword (0x7CD215D8)
- Once found, it can align to 32‑bit codeword boundaries and batch/frame structure

3. Error checking and correction

- For each 32‑bit codeword, the BCH and parity bits are used to detect and correct bit errors caused by noise or weak signal

4. Interpret address vs data codewords

- An address codeword contains the pager’s address (“cap code”) and a few “function bits” telling if following messages are numeric or alphanumeric.
- Data codewords carry the actual message bits, which can be: Numeric (often BCD digits), or Alphanumeric (7‑bit ASCII, with bits sent least‑significant‑bit first and sometimes crossing codeword boundaries)

5. Reassemble and display the message

- The decoder chains multiple data codewords for one address until another address, sync, or idle pattern appears
- For alphanumeric messages, it groups bits into 7‑bit characters (after bit‑order fixing) and converts them to readable text

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*muRcITz49LHYI-OT)

_(source: medium .com)_

### Quick tutorial

- run `gqrx` software defined radio
- search for active frequency for POCSAG traffic (depends on countries)
- stream output to `localhost`using `UDP`
- run `netcat` to forward UDP traffic to `sox` then ` multimon-ng` decoder

  ```
  ncat -l -u -p 7355 \
      | sox --type raw -esigned-integer --bits 16 --rate 48000 - --type raw -esigned-integer --bits 16 --rate 22050 - \
      | multimon-ng -n -t raw -p -a POCSAG512 -a POCSAG1200 -a POCSAG2400 -a FLEX -a FLEX_NEXT -f auto --timestamp /dev/stdin
  ```

### See also

- [POCSAG](https://www.sigidwiki.com/wiki/POCSAG)
- [RTL-SDR Tutorial: POCSAG Pager Decoding](https://www.rtl-sdr.com/rtl-sdr-tutorial-pocsag-pager-decoding/)
- [Decoding POCSAG using Gqrx & RTL-SDR](https://radiohackers.com/decoding-pocsag-using-gqrx-rtl-sdr-4f4e4fe1c10b)
