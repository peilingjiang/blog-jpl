---
bookCollapseSection: true
author: "Peiling Jiang"
date: "2020-09-09"
title: Starry Night
type: posts
bookToc: true
---

For my first AR project, I tried to bring the starry sky into my room, as during the pandemic,  we have fewer chances to go outside and stargaze. Unlike famous [Night Sky](https://apps.apple.com/us/app/night-sky/id475772902) and [SkyView](https://apps.apple.com/us/app/skyview/id404990064) that depict the sky in a scientific and realistic way, I tried to make the experience simple, cute, and relaxing.

## Process

Ideally, the user will be able to see the sparkling stars unfold lying in the bed and pointing the phone to the ceiling. However, problems came up and the final result is not as expected in a various of ways.

### Modeling

I was able to model the star with Grasshopper in Rhino, and convert the file into `.usdz` format with [Reality Converter](https://developer.apple.com/news/?id=01132020a) so that it can be imported into Reality Composer. However, I failed to find a way to keep the luminous textures attached when exporting and importing the file. As a result, the star objects can only reflect the ambient lights with a strange metallic surface style.

![Properties](/new-realities/starry-night/properties.png)

### Behavior

Although the stars will be above to the ceiling at first, I added another interactive layer where they'll turn into meteor shower and drop down when the user hit them.

![Behavior](/new-realities/starry-night/behavior.png)

Unlike most AR applications where the users interact with objects placed on the table or on the floor, the stars are "floating" above and with no support beneath in the "development setting." To make this possible in the "realities," I had to give up **Dynamic** motion type as well as inherent *Add Force* action that could have made later interactions more vivid and engaging.

### AR

Without LiDAR Scanner, the AR experience on my phone is highly light-sensitive, so I have to keep the lights on and bright. In addition, I have to point the phone down to the bed or floor to "scan" and find the base anchor before moving it upwards, as Reality Composer doesn't provide a "top-down" setting. Not to speak of the white and plain ceiling that makes it almost impossible for the cameras to find the references. As a result, the overall experience is shaky and unreliable.

## Demo

{{< video src="/new-realities/starry-night/demo.mp4" >}}
