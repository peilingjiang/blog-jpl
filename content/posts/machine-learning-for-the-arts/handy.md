---
author: "Peiling Jiang"
date: "2019-11-18"
title: Handy
tags: ["IMA", "Fall19", "Final"]
categories: ["Project"]
type: posts
bookToc: true
---

Handy is a wearable interface interpreting tangible interaction to intangible experiences.

## Proposal

When we *move*, a lot more is happening than what can be explicitly observed: signals coming out of the brain, and converted into electrical inputs muscle can understand and execute. The signal that we can record on our skin is **Electromyography (EMG)**. According to former research, EMG data can be collected and analyzed for the identification of certain movements. For example, [AlterEgo](https://www.media.mit.edu/projects/alterego/overview/) (A. Kapur et al.) can translate indiscernible silent speech to words with machine learning of collected data.

But the concept and technology haven't been applied to the identification and interpretation of *body movements* yet. With the project **Handy**, I'll collect EMG data of different hand and finger gestures, use machine learning model to learn and identify different movements, and explore possible use scenarios.

Data will be collected and interacted with OpenBCI [Cyton](https://docs.openbci.com/docs/02Cyton/CytonLanding) Board and [sticky electrodes](https://shop.openbci.com/collections/frontpage/products/skintact-f301-pediatric-foam-solid-gel-electrodes-30-pack?variant=29467659395). I setup the board and tried with one channel (one muscle) on:

![Early board testing](/machine-learning-arts/handy/curve.png)

We can tell clearly when did I use the muscle and when did I idle. After the technical development phrase, the ultimate goal of the project would be researching and developing HCI for this new EMG-based interface.

### TODO

Here are several (technical) questions I'll answer during the first stages of the project:

1. How to collect meaningful data through electrodes and the broad? In other words, how to determine the quantity of electrodes needed, and set the *universal ground*? *- (2019.12.11) I use 4 electrodes for this stage's experiments. It's partially because it's all the electrodes I have, but also because for the interactions I determined to explore for the stage - scroll and zoom, 4 electrodes are totally enough. The universal ground should be placed at somewhere near the other electrodes while there're supposed to be as less muscle as possible.*

2. What are the best places (on wrist and hand) to place electrodes? And make sure of the cross-session consistency? *- Explored below.*
3. How to preprocess data into understandable formats machine learning models can use? *- (2019.12.11) The data will firstly be received by a Node server, simply processed, and emitted to the client, where not the value of data points, but other index will be calculated and sent into the machine learning model.*
4. How to live stream data from the board to browser or other applications? *- I use Node.js for current web-based applications. Will be likely to switch to Python for other scenarios and possibilities.*

More TODOs and future works related to HCI to be updated.

## Development

### Electrodes

One Cyton board can read and send up to 4 channels of EMG data, which means 4 different muscle groups. After learning about hand and arm muscle groups, I decided to use *two* channels for early stage development and simple gestures, and all 4 channels for final implementation and more complex and detailed movement detection. The electrodes will be attached to the upper limb and hand as follows:

{{< expand >}}

![2 Channel Implementation](/machine-learning-arts/handy/upper-limb-2.png)
2 Channels *(Base photos from Wikipedia)*
![4 Channel Implementation](/machine-learning-arts/handy/upper-limb-4.png)
4 Channels

{{< /expand >}}

After several trials of data collecting and testing, I finally adjust the electrode placement as the following, for the designated interactions for this stage - **scroll up/down** and **zoom in/out**:

{{< figure src="/machine-learning-arts/handy/electrode-placement.png" alt="Electrode Placement" width="100%" >}}

Channel one and two will mainly be used to *scroll*, and three and four will mainly be used to *zoom*.

### Signal Processing

The models were trained with `ml5.neuralNetwork`.

The sampling rate of the OpenBCI Cyton board is around 200Hz (which is much higher than the default 60Hz p5.js `draw()`) so I'm getting a lot of data each second for every channel.

I firstly tried to send the data directly to ml5.neuralNetwork, however, the training performed very poorly (see the left figure below) no matter how I adjusted training options like learning rate and epochs. Then I plotted out the signals I received and understood the reason: even though the signal plot is relatively easy for us to identify the "active" parts from the "idle" ones, the data points are really close to each other, jumping back and forth, making it hard for machine learning models to distinguish (see the figure below the loss curves.)

![Training Performance](/machine-learning-arts/handy/training_performance.jpg)

![Clean Signal Curve](/machine-learning-arts/handy/curve-clean.jpg)
<caption>Preprocessed sign received from Cyton</caption>

![Analyzed Signal Curve](/machine-learning-arts/handy/curve-closer.svg)
<caption>Data points in the same place of adjacent periodic signal chunks</caption>

Then I realized the "active" part of the signal has "destroyed periods" - the signal no longer repeat as it normally does, with a larger amplitude. Thus, instead of sending the absolute value of the data into the model, I sent the following three values:

- the delta (absolute value) of the point and its predecessor
- the delta (absolute value) of the point and the point 12 points ahead of it
- the standard deviation of the the point with 11 points ahead of it (*f* = 12)

And the training results and predictions works drastically better than before (see the right figure above.)

Due to the time limitation, I didn't have enough time to apply appropriate DSP (digital signal processing) filters to the signal streamed from the board. But this could help the machine learning model perform much better on the signal recognizing and gesture classification. Also, the OpenBCI GUI (normally for quick plotting and connection checking, based on Processing!) applies the filters automatically and provides options of re-streaming out the filtered data. But I haven't figured out the proper way to establish connection with it before the deadline of the project.

{{< vimeo 379383886 >}}

## The Interface

For the first stage of development, I tried to accomplish the following three interactions with the interface (all requiring `categorization` as the task for the models.)

![Interactions](/machine-learning-arts/handy/interface.png)

The third interaction that intends to create a "number board" inside the palm hasn't been achieved, it's unstable even when recognizing "1" and "9" - which are the furthest two numbers on a board - alone. I'll keep working on it and see if the result will improve if after applying the filter or with other methods. I also modularized the system so that each model only needs to handle very simple and specific tasks, and it's easy to extend the applications by training new models and adding them into the pipeline.

{{< figure src="/machine-learning-arts/handy/model-structure.png" alt="Model Structure" width="100%" >}}

## Future Works

1. Look into high-pass filters that would help make the signal cleaner and easier for the model to learn.
2. Complete the demo of the visualized data collection tool.
3. Explore possibilities in terms of HCI (human-computer interaction) and industrial design of the interface and device.
4. Lose weight to get better EMG signals.

## References

1. [Electromyography - Wikipedia](https://en.wikipedia.org/wiki/Electromyography)
2. [Muscles of the Upper Limb - Wikipedia](https://en.wikipedia.org/wiki/Category:Muscles_of_the_upper_limb)
3. [Arm - Wiki](https://en.wikipedia.org/wiki/Arm), [Upper Limb - Wiki](https://en.wikipedia.org/wiki/Upper_limb)
4. [AlterEgo - MIT Media Lab](https://www.media.mit.edu/projects/alterego/overview/), [Paper](https://dl.acm.org/citation.cfm?id=3172977)
5. [OpenBCI](https://openbci.com)
6. [Techniques of EMG signal analysis: detection, processing, classification and applications](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1455479/)
7. [EMG Signal Classification for Human Computer Interaction A Review](https://www.researchgate.net/publication/215677997_EMG_Signal_Classification_for_Human_Computer_Interaction_A_Review) (Table 1: Summary of major methods used for EMG classification in the field of HCI)
8. [A new means of HCI: EMG-MOUSE](https://ieeexplore.ieee.org/document/1398280)

## Technical References

1. [Setting up for EMG - OpenBCI Doc](https://docs.openbci.com/docs/01GettingStarted/02-Biosensing-Setups/EMGSetup)
2. [Python signal filter test by J77M](https://github.com/J77M/openbciGui_filter_test/blob/master/fft_data.ipynb)
3. [OpenBCI/OpenBCI_NodeJS_Cyton - GitHub](https://github.com/OpenBCI/OpenBCI_NodeJS_Cyton)
4. [OpenBCI/OpenBCI_NodeJS - GitHub](https://github.com/OpenBCI/OpenBCI_NodeJS)
