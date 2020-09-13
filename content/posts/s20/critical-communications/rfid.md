---
author: "Peiling Jiang"
date: "2020-04-05"
title: RFID
type: posts
bookToc: true
---

**Week One Assignment** / Research a communications protocol of your choice.

## RFID: Explained

![RFID Chip](/critical-communications/rfid_chip.jpg)

**Radio-frequency identification** (RFID) uses *electromagnetic* fields to automatically identify and track tags attached to objects. An RFID tag consists of:

- A radio transponder
- A radio receiver and transmitter

When triggered by an electromagnetic interrogation pulse from a nearby RFID reader device, the tag transmits digital data, usually an identifying inventory number, back to the reader.

### Tags

RFID tags consist of three parts:

- **Micro chip**: an integrated circuit which stores and processes information and modulates and demodulates radio-frequency signals
- **Antenna**: receive and transmit the signal
- Substrate

There're two types of RFID tags:

1. **Passive tags** (including battery-assisted passive tags) are powered by energy from the RFID reader's interrogating radio waves.<br>
*Smaller / Cheaper / Needs a 1000 times stronger power than active tags for signal transmission*

2. **Active tags** are powered by a battery and thus can be read at a greater range from the RFID reader - up to hundreds of meters.

Unlike a barcode, the tag doesn't need to be within the line of sight of the reader, so it may be embedded in the tracked object. RFID is one method of automatic identification and data capture (AIDC).

### Readers

1. **Passive Reader Active Tag (PRAT) system**<br>
Passive reader and active tags (battery operated, transmit only). Reception range: 0-600m.

2. **Active Reader Passive Tag (ARPT) system**<br>
Active reader transmits interrogator signals and also receives authentication replies from passive tags.

3. **Active Reader Active Tag (ARAT) system**<br>
Active tags awoken with an interrogator signal from the active reader.

### Frequencies

$$f = \frac{c}{λ}$$

| Band                                             | Regulations         | Range     | Data Speed       | Cost (2006) USD |
|--------------------------------------------------|---------------------|-----------|------------------|-----------------|
| 120 – 150kHz (LF)                                | Unregulated         | 10cm      | Low              | 1               |
| 13.56MHz (HF)                                    | ISM band worldwide  | 10cm - 1m | Low to Moderate  | 0.5 - 5         |
| 433MHz (UHF)                                     | Short range devices | 1 - 100m  | Moderate         | 5               |
| 865 – 868MHz (EU) 902 – 928MHz (N America) (UHF) | ISM band            | 1 - 12m   | Moderate to High | 0.15 (Passive)  |
| 2450 – 5800MHz (Microwave)                       | ISM band            | 1 - 2m    | High             | 25 (Active)     |
| 3.1 – 10GHz (Microwave)                          | Ultra wide band     | 1 - 200m  | High             | 5               |

## History

**1945**<br>
Léon Theremin invented a *listening device* for the Soviet Union which retransmitted incident radio waves with the added audio information. Even though this device was a covert listening device, rather than an identification tag, it is considered to be *a predecessor of RFID* because it was **passive**, being **energized** and **activated by waves** from an outside source.

**1948**<br>
**Identification friend or foe transponder** was routinely used by the allies and Germany in World War II to identify aircraft as friend or foe.

**1973**<br>
*Mario Cardullo*'s device, patented on January 23, 1973, was the **first true ancestor of modern RFID**, as it was a passive radio transponder with memory. The initial device was **passive** and **powered by the interrogating signal**. It has a transponder with 16 bit memory.

**1983**<br>
The first patent to be associated with the abbreviation RFID was granted to *Charles Walton*.

## Uses

The tag can be read if passed near a reader, even if it is covered by the object or not visible. RFID tags can be read hundreds at a time while bar codes can only be read one at a time using current devices.

Common scenarios:
- Access management
- Tracking of goods
- Tracking of people or animals
- Toll collection and contactless payment
- Machine readable travel documents
- Airport baggage tracking
- Timing sporting events
- ...

In China, RFID are used in the new generation ID card, railway automatic train identification system, package tracking, etc. China is also leading the design of antenna and chip design.

In 2010 three factors drove a significant increase in RFID usage:
- Decreased cost of equipment and tags
- Increased performance to a reliability of 99.9%
- Stable international standard around UHF passive RFID

## Problems

1. **Data Flooding** A large amount of data may be generated that is not useful for managing inventory or other applications.

2. **Global Standardization** The frequencies used for UHF RFID in the USA are as of 2007 incompatible with those of Europe or China. Furthermore, no emerging standard has yet become as universal as the barcode.

3. **Security** Tags, which are world-readable, pose a risk to both personal location privacy and corporate/military security.

4. **Health** Microchip–induced tumors have been noted during animal trials.

## References

1. [Radio-frequency identification - Wikipedia](https://en.wikipedia.org/wiki/Radio-frequency_identification)
2. [RFID in China - EE Times](https://www.eetimes.com/rfid-in-china/)
3. [RFID: How businesses use chip technology](https://job-wizards.com/en/rfid-how-businesses-use-chip-technology/) (Cover)
