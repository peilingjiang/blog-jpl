---
author: "Peiling Jiang"
date: "2019-12-01"
title: Infinite Goldfish
tags: ["IMA", "Fall19", "Final"]
categories: ["Project"]
type: posts
bookToc: true
---

By Carol (Keru) Wang and Peiling Jiang.

{{< figure src="/world-in-box/main.jpg" alt="Headline Photo" width="100%" >}}

**Infinite Goldfish (actually Betta)** is an installation which finds meaningful words through letters interpreted from a Betta's positions in an aquarium. [GitHub](https://github.com/peilingjiang/infinite-goldfish)

## What is it?

*Infinite Goldfish* is an installation in which a goldfish "types" an “infinitely” long string of letters by unconsciously swimming in an aquarium. It intends to raise the question of whether meaning does exist by demonstrating an absurd practice of looking for meaning in randomness.

Through Raspberry Pi and Pi camera, a top view of the fish tank is taken and uploaded to a cloud drive for further process every minute. Using Blob Detection, the position of the fish in the aquarium is found and mapped to a specific English letter. The generated string is then passed to a piece of C code, which would create files marking out and counting the meaningful words that appeared in the text.

## Philosophical Content

*Infinite Goldfish* is inspired by *Infinite Monkey Theorem* and *Eternal Recurrence Theory*: one states that “a monkey hitting keys at random on a typewriter keyboard for an infinite amount of time will almost surely type any given text, such as the complete works of William Shakespeare”; the other argues that “the universe and all existence and energy has been recurring, and will continue to recur, in a self-similar form an infinite number of times across infinite time or space”.

For us, the philosophy behind both concepts discusses the meaning of existence from the aspect of probability: when looking at existence in the stream of infinite time, does it still hold value when it is merely resulted in randomness? Or can a form of being still be considered meaningful when things are predestined to continue repeating the same pattern recurrently?

We hope by demonstrating an absurd practice of looking for meaning in randomness, the artwork can state our insight into the relationship between meaning and being.

Relating the unconscious swimming of a goldfish to text generation and seeking true words in that, the work can be considered as an exaggerated practice of pareidolia: a common psychological phenomenon that causes people to see patterns in a random stimulus, such as seeing a face from clouds. For us, it is a metaphor of what most people are doing everyday: paying great effort to reason and conclude the causal relationship behind things, even though it could be completely irrelevant.

## Technical Report

### Image Taking & Uploading

Raspberry Pi and Pi camera are used for taking and uploading images, together with Google Drive API.

### Image Processing

We thought about using DenseCap for the fish location detection, for it can recognize the fish and return the coordination of its bounding box. However, after doing some further research, we found that it is completely unnecessary and overheavy. In our final implementation, the location of the fish is calculated using a blob detection algorithm, which would find the red pixel group - the color of Betta - in the image. The position is then mapped to a English letters based on its coordination.

![Division Explanation](/world-in-box/division.png)
Check photos | [1](/world-in-box/division-01.png) | [2](/world-in-box/division-02.png) | [3](/world-in-box/division-03.png)

We divide the area into `n = 26x26` subdivisions, and randomly place alphabet letters in them. Each letter will occupy 26 blocks. The method is implemented to minimize the influences of original positions the letters occur in alphabet, and Betta's preferences of locations in the tank.

### Word detection

We insert a dictionary of 25,322 popular words into a *tire tree* data structure, and the following word detection process is based on that tree.

## Reflection

For now, the setup of the fish tank and the Pi camera has two significant problems:

1. The reflection of the fish could disturb the fish location detection, and this issue cannot be solved by simply chopping the image for the top-view perspective’s influence.

2. The heater in the fish tank would interfere with the detection as well and is not aesthetically desirable.

Also, the installation itself is not a closed system for now: the generated text needs to be collected and fed to the C code for word detection by us, and the created files need to be printed manually. Therefore, the demonstration effect is not desirable for now, since all the audience can look at is just a fish tank with a Pi camera hanging over it.

In the future, besides solving the setup problems mentioned above, we wish to make this work a closed system that could tell the audience which letter is being generated, what is the current text, and what is the current detected words in real-time.

## References

1. [DenseCap: Fully Convolutional Localization Networks for Dense Captioning](https://cs.stanford.edu/people/karpathy/densecap/)
2. [DenseCap - GitHub](https://github.com/jcjohnson/densecap)
3. [Google Drive API v3](https://developers.google.com/drive/api/v3/about-sdk)
4. [Computer Vision: Blob Detection - Processing Tutorial](https://www.youtube.com/watch?v=ce-2l2wRqO8)
5. [Fish Tank - MAD](http://www.i-mad.com/post-art/fish-tank/)
6. [Operant conditioning chamber](https://en.wikipedia.org/wiki/Operant_conditioning_chamber)
7. [Infinite Monkey Theorem](https://en.wikipedia.org/wiki/Infinite_monkey_theorem)
8. [Eternal Recurrence Theory](https://en.wikipedia.org/wiki/Eternal_return)
9. [Dictionary (25,322 words)](https://github.com/dolph/dictionary)
