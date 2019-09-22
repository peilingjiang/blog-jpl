---
author: "Peiling Jiang"
date: "2019-09-22"
title: Violinist
tags: ["IMA", "Fall19"]
categories: ["Project"]
type: docs
bookToc: true
---

# Violinist

> UPDATE: The name of the project has changed to **Guitarist**!

_Violinist_ enables user to play violin (or potentially any type of instrument) by just posing as they are playing it. This simple have-a-try project is based on p5.js, ml5.js, and poseNet, and help us understand the basic use of poseNet and p5.serialControl. Here's the [link](https://editor.p5js.org/peilingjiang/full/eguZUH4Xb) to p5 web app (p5.serialControl and Arduino required).

## poseNet() in p5.js

The goal is to have the webcam and p5 web app be able to distinguish the **relaxing**, **prepared**, and **playing** status with poseNet(). And a few points we noticed when tackling the challenge are as follows.

### Eliminate Noise

Raw poseNet() output is quite noisy with more than 10 digits after the decimal point and the value changing 60 times a second. As a result, the keypoints drawn are shaking all the time and unusable for us as our calculation will be based on the position of those dots. Thus we set `noiseDelta = 6`, and if the horizontal or vertical position changes between frames are smaller than the value is will be regarded as noise. Moreover, we use the same strategy for minimizing the noise of angle changing, by setting `sensitivity = 12` (degrees).

<img src="/machine-learning-arts/violinist/noise.gif" alt="Comparison between raw points and noise-eliminated points" width="100%" >

### Correct Pose

PoseNet() is good at abstracting the skeleton and keypoints from the body, but we didn't find a direct way to label specific poses (e.g. running, playing violin) based on it - which might require another machine learning library. And we don't want the speaker to beep once the bow angle changes. We then set a series of standard semi-transparent key points to help user match their pose to the _performing pose_. Once the pose matched, the hint areas will dim. However, this is also the constrain of the project, and if `playPose()` is based on the label or name of the pose, it would be much better.

### Mirror Effects

All the `VIDEO` assets drawn in p5.js sketch are flipped horizontally, unlike a natural mirror. These feature caused a huge problem for us since it's really confusing when the figure on the screen acts the opposite way of you and you need to match your pose to the preset one. We first flip the displayed video while this will not affect the data poseNet is reading.
```
push();
// Move image by the width of image to the left
translate(video.width, 0);
// Then scale it by -1 in the x-axis to flip the image
scale(-1, 1);
image(video, 0, 0, width, height);
pop();
```
Then we setup a `Point` class and store all keypoints into one array. When drawing the points, renderer will only get data from `getX()` and `getY()`, and the calculation and rendering will be separated.
```
class Point {
  constructor(x, y, ind, part) {
    this.x = x;
    this.y = y;
    this.px = x;
    this.py = y;
    ...
  }
...
  getX() {
    // Return mirrored x
    return (width - this.x);
  }

  getY() {
    return this.y;
  }
...
}
```

## Physical Computing

We want the buzzer to beep at different rate as the user play faster or slower. To do that, we map the velocity of angle changing to `delay(x)` - the faster the user is playing, the bigger the `vel`, and the smaller the value of `x`. (Please turn down the volume before playing the video.)

<br>

{{< video src="/machine-learning-arts/violinist/final.mp4" width="100%" >}}

<br>

## Future Works

1. Due to time and the scale of the project, we didn't have enough time to further tuning the tone of buzzer. But it'll be the first to-do on the list. Moreover, instead of playing just one note, a sequence of notes can be programmed to beep to create a real song. And mp3 shield can be used to make the sound better.

2. As mentioned in **Correct Pose** section, we need to train the model to recognize the specific poses, _performing_ in this case, in a more "elegant" way.
