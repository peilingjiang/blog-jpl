---
author: "Peiling Jiang"
date: "2019-10-07"
title: knowSound( )
tags: ["IMA", "Fall19"]
categories: ["Project"]
type: posts
bookToc: true
---

{{< hint warning >}}
IN PROGRESS
{{< /hint>}}

I'm planning to train a sound classification model for ml5 among a group of CV models. I've found a relatively small (around 1000-2000 pieces of sound effects files) yet well labeled dataset of sound effects: [Adobe Audition Sound Effects](https://offers.adobe.com/en/na/audition/offers/audition_dlc/AdobeAuditionDLCSFX.html). The dataset, or the sound effects library, is high quality while open-sourced and royalty-free. All the files were well named thus perfectly labeled for the training, here're several examples:

```
>>> Animal
Animal Dog Bark 08.wav
>>> Crash
Crash Car Crushing 01.wav
>>> Horror
Horror Wood Crackle 02.wav
>>> Sports
Sports Boxing Gloves Hit 03.wav
```

For every category, the most files were named by "Category" + "Object" + "event", which is perfect for multi-layer training. I'll start looking for more references and writing the code this week.

## References
1. [Sound Classification using Deep Learning](https://medium.com/@mikesmales/sound-classification-using-deep-learning-8bc2aa1990b7)
2. [Using Deep Learning for Sound Classification: an In-depth Analysis](https://analyticsindiamag.com/using-deep-learning-for-sound-classification-an-in-depth-analysis/)
3. [Enhanced Environmental Sound Classification with a CNN](https://medium.com/ai%C2%B3-theory-practice-business/enhanced-environmental-sound-classification-with-a-cnn-1ca388748bc9)
4. [A Quick Introduction to the “Pandas” Python Library](https://towardsdatascience.com/a-quick-introduction-to-the-pandas-python-library-f1b678f34673)
