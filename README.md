# 128b/130b to 5b/6b Encoding with CRC Error Detection

This project implements a simple digital data transmission system using Arduino.  
The system starts with a 130-bit data frame, divides it into 5-bit blocks, converts each block into a 6-bit encoded symbol using a 5b/6b lookup table, transmits the encoded data bit by bit, and then decodes it back at the receiver side.

A second version of the project also adds CRC-based error detection to identify corrupted bits during transmission.

---

## Project Overview

The goal of this project is to simulate and implement a basic line-coding and error-detection mechanism.

The system performs the following steps:

1. Generate a 130-bit data frame.
2. Transmit the original frame from the first transmitter to the first receiver.
3. Split the received 130-bit frame into 26 blocks of 5 bits.
4. Encode each 5-bit block into a 6-bit codeword using a predefined 5b/6b mapping table.
5. Transmit the 156-bit encoded frame.
6. Decode each received 6-bit block back into its original 5-bit value.
7. Compare the decoded data with the original data.
8. In the CRC version, detect transmission errors using CRC-8.

---

## Why 5b/6b Encoding?

5b/6b encoding maps every 5-bit input value to a 6-bit output code.  
This adds controlled redundancy to the transmitted data and can help improve signal reliability, synchronization, and DC balance in digital communication systems.

In this project:

- Input frame size: `130 bits`
- Number of 5-bit blocks: `26`
- Encoded block size: `6 bits`
- Encoded frame size: `26 × 6 = 156 bits`

---

## Repository Contents

| File | Description |
|---|---|
| `Encoding.ino` | Main Arduino implementation for 130-bit transmission, 5b/6b encoding, second transmission, decoding, and error checking |
| `Encoding-error-detect.ino` | Extended version of the project with CRC-8 error detection |
| `Document-report.pdf` | Full project report and explanation |

---

## Main Features

- Random 130-bit data generation
- Two-stage bit-by-bit transmission
- 5b/6b encoding using a lookup table
- 6b/5b decoding at the receiver side
- LED display of received 6-bit encoded blocks
- Serial Monitor output for debugging and observation
- Error comparison between original and decoded data
- CRC-8 based error detection in the extended version
- Simulated bit flipping to test error detection

---

## Encoding Process

The encoder takes every 5-bit block and uses it as an index in a predefined 5b/6b table.

Example flow:

```text
130-bit input frame
        |
        v
Split into 26 blocks of 5 bits
        |
        v
Map each 5-bit block to a 6-bit codeword
        |
        v
156-bit encoded frame
```

Each 5-bit value has a corresponding 6-bit encoded value stored in the `ENCODE_5B6B` lookup table.

---

## Error Detection

The `Encoding-error-detect.ino` version uses CRC-8 to detect transmission errors.

CRC is calculated before transmission and checked again after reception.  
If the received CRC does not match the CRC calculated from the received data, the program reports a CRC mismatch.

This version also intentionally flips bits during transmission to demonstrate that the CRC mechanism can detect corrupted data.

---

## Arduino Pin Configuration

The project uses digital pins for transmission, reception, and LED output.

| Purpose | Pins |
|---|---|
| LED output pins | `2, 3, 4, 5, 6, 7` |
| First transmitter pin | `8` |
| First receiver pin | `9` |
| Second transmitter pin | `10` |
| Second receiver pin | `11` |

The LEDs are used to display the current 6-bit encoded block during decoding.

---

## How to Run

1. Open the project in the Arduino IDE.
2. Select the desired file:
   - `Encoding.ino` for the basic encoding/decoding version.
   - `Encoding-error-detect.ino` for the CRC error-detection version.
3. Connect the required TX/RX pins according to the circuit setup.
4. Upload the code to the Arduino board.
5. Open the Serial Monitor.
6. Set the baud rate to `9600`.
7. Observe the transmission, encoding, decoding, and error-checking logs.

---

## Program Output

The Serial Monitor shows:

- Generated original data
- Sent and received bits
- 5-bit to 6-bit encoding results
- Received encoded blocks
- Decoded 5-bit blocks
- Mismatch reports
- CRC mismatch reports in the error-detection version
- Final transmission status

Example output messages include:

```text
Starting first transmission
Encoding received data into 5B/6B format
Starting second transmission
Decoding received data
Checking decode errors
SUCCESS: All bits transmitted and decoded correctly
```

---

## Team Members

- Mohammadfarhan Bahrami
- Pouyan Shamsedin
- Mohammad Shafiezade

---

## Project Purpose

This project was developed as a practical implementation of digital encoding and error-detection concepts.  
It demonstrates how binary data can be encoded, transmitted, decoded, and checked for errors using Arduino-based hardware simulation.
