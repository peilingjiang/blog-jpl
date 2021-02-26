---
title: Home
type: docs
bookToc: false
---

<div id="homeCanvas"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.2.0/p5.min.js" integrity="sha512-b/htz6gIyFi3dwSoZ0Uv3cuv3Ony7EeKkacgrcVg8CMzu90n777qveu0PBcbZUA7TzyENGtU+qZRuFAkfqgyoQ==" crossorigin="anonymous"></script>
<script type="text/javascript">
  let logo
  function preload() {
    logo = loadImage('jpl-logo.svg')
  }
  function setup() {
    let c = createCanvas(800, 570, WEBGL)
    c.parent('homeCanvas')
    noStroke()
    imageMode(CENTER)
    angleMode(DEGREES)
  }
  function draw() {
    clear()
    scale(0.8)
    rotateX((height / 2 - mouseY) * 0.03)
    rotateY((mouseX - width / 2) * 0.01)
    rotateZ((mouseX - width / 2) * 0.003)
    image(logo, 0, 0)
  }
</script>

**JPL is 江沛嶺, and 江沛嶺 is Peiling Jiang.** Peiling studies Interactive Media Arts and Psychology at NYU Tisch School of the Arts and College of Arts and Sciences. With a background of product design, his practices include computational design, human-computer interaction, and computational cognitive modeling.

More information will be updated soon.
