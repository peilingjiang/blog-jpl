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

For the second question, I played with two different scenarios: one smaller object ~~traveling~~ trying to travel through another one, and the collision of objects with curved surfaces. I recorded the simulation with different collision type settings of the objects - Box, Capsule, Sphere, while it seems none of them works perfectly for complex objects, as they don't treat the models as they originally are, but simplistic bounding geometries assumably for better performance.

![Question 2 GIF](/new-realities/ar-assets/2.gif)
![Question 2 GIF](/new-realities/ar-assets/3.gif)

## Two

For the forth week, we practiced texturing and simple APP interactivity with ARKit. I used the cover of Imagine Dragon's [Evolve](https://en.wikipedia.org/wiki/Evolve_(Imagine_Dragons_album)) as the base color and modified the metallicity and roughness of the surface to reflect the genre and style of the music. Some mud and dirts textures were also added on top of the base ones.

![Texture Process](/new-realities/ar-assets/texture.gif)

{{< video src="/new-realities/ar-assets/ar4-mp4.mp4" width="40%" >}}
