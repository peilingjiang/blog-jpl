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

When we *move*, a lot more is happening than what can be explicitly observed: signals coming out of the brain, and converted into electrical inputs muscle can understand and execute. The signal that we can record on our skin is **Electromyography (EMG)**. According to former research, EMG data can be collected and analyzed for the identification of certain movements. For example, [AlterEgo](https://www.media.mit.edu/projects/alterego/overview/) (A. Kapur et al.) can translate indiscernible silent speech to words with machine learning of collected data.

But the concept and technology haven't been applied to the identification and interpretation of *body movements* yet. With the project **Handy**, I'll collect EMG data of different hand and finger gestures, use machine learning model to learn and identify different movements, and explore possible use scenarios.

Data will be collected and interacted with OpenBCI [Cyton](https://docs.openbci.com/docs/02Cyton/CytonLanding) Board and [sticky electrodes](https://shop.openbci.com/collections/frontpage/products/skintact-f301-pediatric-foam-solid-gel-electrodes-30-pack?variant=29467659395). I setup the board and tried with one channel (one muscle) on:

![Early board testing](/machine-learning-arts/handy/curve.png)

We can tell clearly when did I use the muscle and when did I idle. After the technical development phrase, the ultimate goal of the project would be researching and developing HCI for this new EMG-based interface.

### TODO

Here are several (technical) questions I'll answer during the first stages of the project:

1. How to collect meaningful data through electrodes and the broad? In other words, how to determine the quantity of electrodes needed, and set the *universal ground*?
2. What are the best places (on wrist and hand) to place electrodes? And make sure of the cross-session consistency?
3. How to preprocess data into understandable formats machine learning models can use?
4. How to live stream data from the board to browser or other applications?

More TODOs and future works related to HCI to be updated.

## Development

### Electrodes

One Cyton board can read and send up to 4 channels of EMG data, which means 4 different muscle groups. After learning about hand and arm muscle groups, I decided to use *two* channels for early stage development and simple gestures, and all 4 channels for final implementation and more complex and detailed movement detection. The electrodes will be attached to the upper limb and hand as follows (might be adjusted in the future):

![2 Channels Implementation](/machine-learning-arts/handy/upper-limb-2.png)
2 Channels *(Photos from Wikipedia)*
![4 Channels Implementation](/machine-learning-arts/handy/upper-limb-4.png)
4 Channels

## References

1. [Electromyography - Wikipedia](https://en.wikipedia.org/wiki/Electromyography)
2. [Muscles of the Upper Limb - Wikipedia](https://en.wikipedia.org/wiki/Category:Muscles_of_the_upper_limb)
3. [Arm - Wiki](https://en.wikipedia.org/wiki/Arm), [Upper Limb - Wiki](https://en.wikipedia.org/wiki/Upper_limb)
4. [AlterEgo - MIT Media Lab](https://www.media.mit.edu/projects/alterego/overview/), [Paper](https://dl.acm.org/citation.cfm?id=3172977)
5. [OpenBCI](https://openbci.com)

## Technical References

1. [Setting up for EMG - OpenBCI Doc](https://docs.openbci.com/docs/01GettingStarted/02-Biosensing-Setups/EMGSetup)
2. [Python signal filter test by J77M](https://github.com/J77M/openbciGui_filter_test/blob/master/fft_data.ipynb)
