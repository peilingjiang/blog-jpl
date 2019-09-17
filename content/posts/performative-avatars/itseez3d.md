---
author: "Peiling Jiang"
date: "2019-09-16"
title: itSeez3D
tags: ["IMA", "Fall19"]
categories: ["Reading"]
type: docs
bookToc: true
---

# itSeez3D

<img src="/performative-avatar/itseez3d/scan_spin.gif" alt="An animation of the scanned model spinning" width="100%" >

This week I scanned my whole body with itSeez3D app and Occipital’s Structure Sensor for capturing color and structure information. The app did a decent job for well capturing overall information including my height (a little taller) and body shape; and details from the words on my t-shirt to acne on my face.

<img src="/performative-avatar/itseez3d/full_body_blur.png" alt="Full body model" width="100%">

My partner held the iPad and scanned me for 3 times while the first trail was a total failure and we didn't keep it. The second scan (left two models above) went fine with some flaws occurred: for example, the texture of the top of the head didn't match the mesh well. I'll elaborate it below. For the third scan I tried to smile while the final facial expression turned out weird.

## Things Work Well

<img src="/performative-avatar/itseez3d/body.png" alt="Full body model" width="100%">

The model looks not bad especially when people know it's created by a tiny accessible scanner attached to an iPad. The **color** is accurate, the **ratio and dimension** preserved correctly, and the **texture and shape** were captured well.

## Things Don't Work Well

### Internal surfaces

{{< figure src="/performative-avatar/itseez3d/texture_mesh.png" alt="Picture shows inner surfaces details" width="100%" >}}

Although during the scan you could feel that you did scan both outer and "internal" surfaces - that are not facing the outside, through the gaps. For example, inner thigh and inner arm. However, these parts were still not captured well and in the picture above both texture and mesh of inner arm are broken.

### Edges

<img src="/performative-avatar/itseez3d/head_top.png" alt="The head top details" width="100%">

_Edge_ means both the edge parts of the body - head, hands, feet, etc., and the edges of the mesh. And the software is not good at meshing both. For head, although we've put the iPad as high as possible, the texture still looks twisted and squeezed. What's more, it will fill all the holes by capping them with a flat surface, including the gap between my t-shirt sleeves and my arm, and the bottom of the shoes.

### Structure details

<img src="/performative-avatar/itseez3d/detail_ear.png" alt="The ear details" width="100%">

The detailed structures are also not very well preserved. My ears, figures and hair are either simplified with a lot of details lost, or merged together.

## Conclusion

The Structure Sensor scan works well with color, meshing and texture details since it's also helped by the iPad camera; however, is not very good at internal surfaces (faces that are noting facing outside), edges, and structure details (figures, hair, etc.) The app will re-mesh the scanned model and tends to close every opening to create a closed body.

## Questions
1. When we talk about Avatar ownership, what are we talking about: Appearance, Identity, or Money?<br>
Avatar is capable to reflect our appearance, execute our identity, and monetize celebrities' fame. But what do people actually care about when they "fight for" non-statutory rights (in most places) of their digital representatives? Is it **appearance**? An app recently caught a lot of attention in China, not only because with it people can easily replace actors' faces with their own and act in as many movies as they want (like deep fake), but also because of it's domineering user agreement - that most of people wouldn't ever read. The original version of the agreement (that had been rewritten) granted the company the complete right of usage of image data users uploaded. However, after the thing had arisen the attention of the whole society, many people still use it and post "their" works to social media, before the company took any action. Is it **identity**? Or is it **Money**?
2. Should family members be eligible to make decisions of the after-demise usage of our Avatars when -<br>
The Avatar is a 3D scanned model that can be programmed to do things?<br>
The Avatar is so real that could pass "visual Turing test"?<br>
The Avatar is formed with real biological information including our figure print and medical history?<br>
The Avatar has memory of our past behaviors?

## Related Readings

Avatars & Ethics/Ownership

1. [Athletes & Video Games: Balancing Publicity Rights and the First
Amendment](https://www.forbes.com/sites/oliverherzfeld/2016/09/22/athletes-in-video-games-balancing-publicity-rights-and-the-first-amendment/#6d88e19455b3)
2. [College Football Video Games Are Done. Here’s Why.](https://www.motherjones.com/politics/2013/09/ncaa-football-video-ea-sports-lawsuit/)
3. [Hollywood’s Post-Biological Future: Where Actors Can Perform After
Death](https://www.vice.com/en_us/article/539a5z/hollywoods-post-biological-future-where-actors-can-perform-after-death)
4. [‘Rogue One: A Star Wars Story’ — A New Hope (For Deceased Actors)](https://www.forbes.com/sites/legalentertainment/2016/12/22/rogue-one-a-star-wars-story-a-new-hope-for-deceased-actors/#21a69246af36)
5. [Avatar Acts: Why Online Realities Need Regulation](https://www.scientificamerican.com/article/avatar-acts/)

> Some media on this page is blurred due to privacy concerns. <br>
> Models scanned by Keru Wang.
