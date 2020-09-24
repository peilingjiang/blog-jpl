---
author: "Peiling Jiang"
date: "2020-09-24"
title: AR Assets
type: posts
bookToc: true
---

## One

For the first step of modeling for AR experiences, I started with several simple models to answer two questions:

1. Does it work with open meshes (mesh surfaces) or only solid bodies?
2. Does physical simulation, especially collision, apply to the models themselves, or to their bounding boxes?

For the first question, I modeled a single sheet of individual mesh surfaces connecting to each other only by vertices. After trying various ways to export the model the import to Reality Converter, it still failed to read the model correctly as originally in the modeling software.

![Question 1 Image](/new-realities/ar-assets/1.webp)

For the second question, I played with two different scenarios: one smaller object ~~traveling~~ trying to travel through another one, and the collision of objects with curved surfaces. I recorded the simulation with different collision type settings of the objects - Box, Capsule, Sphere, while it seems none of them works perfectly for complex objects, as they don't treat the models as they originally are, but simplistic bounding geometries for assumably for better performance.

![Question 2 GIF](/new-realities/ar-assets/2.gif)
![Question 2 GIF](/new-realities/ar-assets/3.gif)
