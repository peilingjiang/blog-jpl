---
author: "Peiling Jiang"
date: "2019-11-18"
title: Handy
tags: ["IMA", "Fall19", "Final"]
categories: ["Project"]
type: posts
bookToc: true
---

A wearable interface interpreting hand movements to computer interactions.

## Proposal

When we *move*, a lot more is happening than what can be explicitly observed: signals coming out of the brain, and converted into electrical inputs muscle can understand and execute. The signal that we can record on our skin is Electromyography (EMG). According to former research, EMG data can be collected and analyzed for the identification of certain movements. For example, [AlterEgo](https://www.media.mit.edu/projects/alterego/overview/) can translate indiscernible silent speech to words with machine learning of collected data.

But the concept and technology haven't been applied to the identification and interpretation of *body movements* yet. With the project **Handy**, I'll collect EMG data of different hand and finger gestures, use machine learning model to learn and identify different movements, and explore possible use scenarios.

Data will be collected and interacted with OpenBCI [Cyton](https://docs.openbci.com/docs/02Cyton/CytonLanding) Board and electrodes. After the technical development phrase, the ultimate goal of the project would be researching and developing HCI for this new EMG-based interface.

### TODO

Here are several (technical) questions I'll answer during the first stages of the project:

1. How to collect meaningful data through electrodes and the broad? In other words, how to determine the quantity of electrodes needed, and set the *universal ground*?
2. What are the best places (on wrist and hand) to place electrodes? And make sure of the cross-session consistency?
3. How to preprocess data into understandable formats machine learning models can use?
4. How to live stream data from the board to browser or other applications?

More TODOs and future works related to HCI to be updated.

## References

1. [Electromyography - wikipedia](https://en.wikipedia.org/wiki/Electromyography)
2. [AlterEgo - MIT Media Lab](https://www.media.mit.edu/projects/alterego/overview/)
3. [OpenBCI](https://openbci.com)
