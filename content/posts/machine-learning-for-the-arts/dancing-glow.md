---
author: "Peiling Jiang"
date: "2019-10-07"
title: Dancing Glow
tags: ["IMA", "Fall19"]
categories: ["Project"]
type: posts
bookToc: true
---

{{< video src="/machine-learning-arts/dancing-glow/dancing-glow-working.mp4" width="100%" >}}

This week I tried real-time data collection and multiple, different types of inputs and output with the new Neural Network feature of ml5.js. **Dancing Glow**, as a result, is a visual project in which lines following the body will change to different colors according to body positions as trained. Here's the [**LINK**](https://editor.p5js.org/peilingjiang/sketches/hg8ecxUTS) to the p5 web editor.

## Train

### Data Collection

I set up and used two models in this project - one is `'regression'` model that trains the program to predict the **color** of any given poses; another one is `'classification'` model that trains the program to distinguish *normal poses* to *emit pose*, when posing which the glowing colors will emit to the surroundings. To collect data for both models, the user need to add data with either a color array as target output, or a label of `"Emit"` or `"Not Emit"`. Moreover, to collect data more efficiently, while data is collected to color regression model, the same pose information is also passed into the classification model as "Not Emit" label.

```js
//  Add a training example
function addExample_1() {
    // Add to brain_1 as color input
    // Add to brain_2 as Not Emit category
    if (poses.length > 0) {
        let poseInput = get_body_data(poses);
        let target = bodyColor;
        // Add data for regression training
        // Input 26, Output 3
        brain_1.addData(poseInput, [target[0], target[1], target[2]]);
        // Add data for categorization training
        // Input 26, Output 1
        brain_2.addData(poseInput, ["Not Emit"]);
    }
}

function addExample_2() {
    // Add to brain_2 as Emit category
    if (poses.length > 0) {
        let poseInput = get_body_data(poses);

        brain_2.addData(poseInput, ["Emit"]);
    }
}
```

### Mouth Switch

Another interesting thing, which you might have noticed, is that I open and close my mouth as the switch of data collection. We all know about the 3..2..1.. countdown, which is decent and boring. Here instead I use face-api.js (a built-in library of ml5.js) to track the points of my mouth and calculate the distances of several signature points to get to know whether I'm opening my mouth or not, thus if to collect the pose data.

```
poseNet = ml5.poseNet(video, modelReady);
// This sets up an event that fills the global variable "poses"
// with an array every time new poses are detected
poseNet.on("pose", function (results) {
    poses = results;
});

// face-api.js
// No need to create faceBrain here
const faceOptions = {
    withLandmarks: true,
    withExpressions: false,
    withDescriptors: false
};
faceStatusLabel = 2;
faceapi = ml5.faceApi(video, faceOptions, faceReady);
```

Here poseNet is for tracking poses as inputs for machine learning, and faceAPI is solely for mouth opening and closing. The problem is that face-api.js is really heavy and slows down the frame rate significantly once it's running. To save computing resources, instead of letting it recursively call `faceapi.detect(gotFaces)`, I move it to `draw()` and will only be executed when the user choose a color or emit class to collect data.

### Classification

However, the classification model is not working, getting weird predictions in which one label's confidence is always 1 and another one's is *undefined*.

    Array(2)
    0: {label: "Emit", confidence: 1}
    1: {label: "Not Emit", confidence: undefined}
    tensor: t {kept: false, isDisposedInternal: false, shape: Array(2), dtype: "float32", size: 1, …}
    length: 2
    __proto__: Array(0)

## Interface

<img src="/machine-learning-arts/dancing-glow/full.png" alt="The Interface of Dancing Glow" width="100%">

The interface for user to collect data and train the model is another focus of the project. It's designed for users to easily select data target (for color regression or emit classification), adjust color, add more classes of data (user can add up to 8 colors), and get informed of the status behind the scene.

<img src="/machine-learning-arts/dancing-glow/colors.png" alt="The Interface of Dancing Glow - Selections" width="100%">

At the top of the interface are *add color class button* for adding more color classes, *add data for emit class button*, *add data for color class button*, and *train! button*. Since the project involves multiple library and the training of more than one model, I added a section of status feedback for users to know about the progress more easily. Below the video are status reports of the loading of libraries and training of the model - *grey* means not start yet, *yellow* means in-progress, and *green* means finished.

## Feature Works

1. Fix the bug of `'classification'` model. As mentioned before, the classification brain is not working and currently I don't know if it's a bug from ml5 or my own code.

2. A better output visualization, and interface design.
