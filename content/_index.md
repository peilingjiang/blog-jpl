---
title: Home
type: docs
bookToc: false
---

<div id="homeCanvas"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.1.9/p5.min.js"></script>
<script type="text/javascript">
  let logo

  function setup() {
    logo = loadImage('jpl-logo.svg')
    let c = createCanvas(800, 570, WEBGL)
    c.parent('homeCanvas')
    noStroke()
    imageMode(CENTER)
    angleMode(DEGREES)
  }

  function draw() {
    background(255)
    scale(0.8)
    rotateX((height / 2 - mouseY) * 0.03)
    rotateY((mouseX - width / 2) * 0.01)
    rotateZ((mouseX - width / 2) * 0.003)
    image(logo, 0, 0)
  }
</script>

**JPL is 江沛嶺, and 江沛嶺 is Peiling Jiang.** Peiling is a media arts and design student at NYU Tisch School of the Arts. With a background of product design, he's practices include computational design, HCI, user research, and creative coding.

🙆‍♂️ More information will be updated soon. Love Qingqing.
