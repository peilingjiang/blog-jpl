---
author: "Peiling Jiang"
date: "2019-09-09"
title: ImageNet
type: posts
bookToc: true
---

The first thing that amazed me was that the project of ImageNet took full advantage of WordNet and benefited from Mechanical Turk. In this way, the data is so organized by synonym sets and, sounds crazy, human-annotated. The data can be looked up easily through treemap visualization.

While each syntex, as claimed, has more than 1000 images on average to be illustrated, I still found some weak portions. With only 138 picture for _People_ section, a lot of subdivisions, including business people and lobby boy, have no photos. The same is for _Misc_ section. The main reason, as far as I'm concerned, is privacy. In ImageNet's Introduction page, a whole section started with **Does ImageNet own the images? Can I download the images?** explains one, all photos here in the ImageNet are originally public available, and two, ImageNet only provides links and thumbnails to the actual photos for most people, like a search engine. However, there might still be potential privacy and copyright concerns. Although all the pictures are uploaded to the public space, most people might not be prepare to have their photos been used for research purposes, and been classified to be search and view easily. Given the fact that most people never read those user agreements, their consent to the photos been reused or shared, when they uploaded the photos to this services, is also doubted. ImageNet seems to have found a "perfect" way to avoid this concern coming into being, and intentionally gave up the magic power in some sensitive sections.

To many debating over whether citizens should sacrifice their privacy to support technology development have taken place around. Privacy is a major part of our social identity thus plays an important role of our modern humanity. Yet there's no clue that technology and humanity are naturally opposite. We see lots of technology boosted the formation of humanity we define today, and many of them were particularly developed to protect our privacy and identity. One possible reason might be that we haven't found the most proper way to do AI. Back to the solution itself, we shall all agree that the current solution is working and descent, yet unsatisfying. Are we only capable to analyze pixel and color? And will never understand how the world is observed and the view of it is established? I doubt that.

# Try-on Sessions

<img src="/machine-learning-arts/imagenet/screenshots.png" alt="Webcam Screenshots" width="100%">
<caption>Cropped screenshots of webcam image classification. Fist line (1-5): Glass Cup, Closet, Boxes, Battery, DSLR Lens. Second line (6-10): Bird on Screen, Board, Mouse, Sunglasses, Pen.</caption>

I tried several things with a focus on the following scenarios:

- Transparent (1)
- Group of things (2-3)
- Hard for human (4-5)
- On screen (6)
- With people (7-9)
- Tiny target (10)

## Results

Original         | Prediction
-----------------|--------------------------------------
Glass Cup        | beaker, paintbrush
Closet           | wardrobe, closet, press
Boxes            | comics
Battery          | revolver, six-gun, six-shooter
DSLR Lens        | hand blower, blow dryer, hair dryer
Bird on Screen   | laptop, laptop computer
Board            | remote control
Mouse            | cellular telephone, mouse
Sunglasses       | sunglasses, dark glasses, shades
Pen              | syringe
