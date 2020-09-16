---
author: "Peiling Jiang"
date: "2020-09-09"
title: Reality Composer Cont.
type: posts
bookToc: true
---

This week, we try to use Reality Composer to design and prototype for experiences in day-to-day activities.

## RRR

**RRR stands for re-buy, refill, and repair.** With AR and object detection, users can interact with the daily objects on-site and finish purpose-driven activities within the following friendly 2D interface.

### Scenario

Shopping is fun, while shopping groceries can be frustrating (even online with mobile apps), partially because of the **goal point** (e.g. you know you need to buy something, you want to buy something) and **action point** (e.g. you actually buy all the things in a long shopping list) are separated by the current 2D interface. This is true for all three R scenarios, where you either need to refill daily necessities or report for repairs for equipment. However, as AR gets access to real-world objects, it connects goals and actions and helps the users easily finish the process on the spot.

### Interface

![Possible Interactions](/new-realities/rc-cont/status.webp)

The interaction can be divided into two parts: augmented and normal. The **augmented labels** tell the user the purchasing (or other) states of the objects and act as **_entry points_** for further interactions. They can be divided into 4 stages: **Recently bought** labels and **Bought a while ago** labels tell you when you bought the item and you can quickly re-buy with a click, **Not recognized** labels enable you to search and add the item into the database so that you can interact with it as the recorded ones, **Just bought** labels tell you how long you need to wait for an item you just ordered. The text is extremely simplified for a comfort AR experience.

### Prototype

{{< video src="/new-realities/rc-cont/prototype.mp4" width="40%" >}}

The draft video shows a simple mockup of the experience. This prototype uses both image anchor and object anchor.

## Screen Extended

**This experience runs on AR glasses instead of a mobile device.**

Screen Extended provides an external display area, virtually, for the monitor to help users concentrate on the main task while accessing more content privately. With AR glasses (e.g. Apple Glasses,) users will be able to view the content seamlessly and interact with it using mouse or pointer, as the AR content has been integrated into the original OS.

One of the main challenges for real-world development would be the detection of the screen area. Here I can just use a screenshot as the image anchor, but any change made to the screen could break the setup. It might require _marking points_ around the monitor or displaying characteristic content around the screen to help detection.

### Prototype

{{< video src="/new-realities/rc-cont/prototype-2.mp4" >}}

The draft video shows a simple mockup of the experience. This prototype uses image anchor.

## References

1. [Augmented Reality Design Guidelines](https://designguidelines.withgoogle.com/ar-design/)
2. [Creating Great AR Experiences](https://developer.apple.com/videos/play/wwdc2018/805/)
3. [AR Cut & Paste](https://github.com/cyrildiagne/ar-cutpaste) by Cyril Diagne / [Demo](https://twitter.com/cyrildiagne/status/1256916982764646402?s=20)
