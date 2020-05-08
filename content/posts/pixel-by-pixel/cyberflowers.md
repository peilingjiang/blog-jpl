---
author: "Peiling Jiang"
date: "2020-05-02"
title: Cyberflowers
type: posts
bookToc: true
---

<iframe style="width: 720px; height: 810px; overflow: hidden;" scrolling="no" frameborder="0" src="https://editor.p5js.org/peilingjiang/embed/b6SH4VwL1"></iframe>

<br>

## Art of Typography

Typography is the art and technique of arranging type to make written language legible, readable, and appealing when displayed. Grew up and living in the digital era, we have built a common sense and intuitively perceive those shapes, composed of curvatures, lines, and solid surfaces, as meaningful pieces. This perception, emerging only in the recent hundreds of years, is so strong, just like our centrality of social cognition of faces, forces us to form meanings around even arbitrary graphics (like <a href="https://twitter.com/simplife_plus/status/1257805754121117696" target="_blank">this</a> (twitter) recent example during social distancing), however, can also be easily **destroyed** as far as I'm concerned. Different coloring, margin, sizes, or even a tiny change to the familiarized radian and stroke length, can easily make us lose the conformity of it being text and rather stimuli our imagination. *(For the following canvases, please click on the canvas to switch text.)*

<br>
<iframe style="width: 720px; height: 320px; overflow: hidden;" scrolling="no" frameborder="0" src="https://editor.p5js.org/peilingjiang/embed/ixM4XnkKR"></iframe>

*Swipe the cursor from left to right to see the formation.*

<br>

With simple and repeated revolving, I created a new form of text art that I'd like to call **Cyberflowers** - made of digital typography and grew from the digital texts in the cyberspace. Here you can see how individual letters gradually *break* their shape-based meaning and become blooming cyberflowers while the curves and lines become cyber-petals and cyber-stamens.

Thanks to p5's nature of interactivity, I can play with the composition of those flowers. By changing the relative position of the starting letter, the formed flowers can be totally different given the same letter, number, or punctuation.

<br>
<iframe style="width: 720px; height: 720px; overflow: hidden;" scrolling="no" frameborder="0" src="https://editor.p5js.org/peilingjiang/embed/hFP05DMUk"></iframe>

*Move the cursor around to change the composition.*

<br>

You can see the composition of cyberflowers that I finally decided for each character at the left bottom corner or browse through them below. The compositions were regulated with the vertical and horizontal offsets of the char, the turning angle each time (which will finally affect the number of cyber-petals), and the size of each petal. These data were recorded into a `.json` file (as follows) that were packed with the scripts.

```
{
    "en": {
        "A": [[   0,   -1], 11,   4],
        "a": [[   0,   -1], 11,   4],
        "B": [[   0, -1.6], 11, 3.5],
        "b": [[   0,    3], 12, 3.5],
        "C": [[ 0.7,    0], 12,   4],
        "c": [[0.65,    0], 12,   4],
        ...
    }
}
```

One thing I almost forgot to mention is the actual typography I was using for all the cyberflowers here, also one of the most famous of all time, **Times**. In spite of its great name, the font is aesthetically out-of-time and has been put on the "Never Use" lists for graphic designers. I can't agree more with this fact, while proudly used it as a proof-of-concept manner - If Times works, who doesn't? On the other hand, honestly, the font has advantages that outstand itself from those popular and boring ones. With the serifs directly modified and inherited from English calligraphy, it features soft curves as well as powerful and solid straight lines and sharp corners. Both of which add various flavors into the graphic and give us more power to create different shapes when we don't have to perceive them as characters. Here's the final works:

<br>
<iframe style="width: 720px; height: 320px; overflow: hidden;" scrolling="no" frameborder="0" src="https://editor.p5js.org/peilingjiang/embed/-CYsUUWxC"></iframe>

*Click on the canvas to change to different chars.*

<br>

## Letters, Words, Lines

Then I tried to push this arbitrary imagination further, from a single character, to words and lines. **Every word is a seed of an idea.** And seeds of thoughts with distinct emotion, arousal, attitude, and meaning would grow into different flowers of affects *(n. emotion or desire, especially as influencing behavior or action)*.

I built a Chrome extension based on the art to help people find positive or negative sentiments on the web **(for fun)**, with the help of ml5.js sentiment library.

![Screenshot 1](/pixel-by-pixel/cyberflowers/screenshot_1.png)
![Screenshot 2](/pixel-by-pixel/cyberflowers/screenshot_2.png)
![Screenshot 3](/pixel-by-pixel/cyberflowers/screenshot_3.png)
![Screenshot 4](/pixel-by-pixel/cyberflowers/screenshot_4.png)

The sizes of cyberflowers, shades of their colors, and blooming speeds are all based on the sentiment scores of the content around the picked letter.

### How to use it?

Please go to the GitHub repository page to download the source file of the package, unzip it, and load into your Chrome. (You'll need to go to `chrome://extensions`, turn on *Developer mode*, and choose *Load unpacked*.)

You can either click on the character and sow a new cyberflower rooted on it, or select a section of text and move your cursor over it to quickly sow many. After that, you could also click on "Pick Cyberflowers" to save the picture of the flowers.

![Demo](/pixel-by-pixel/cyberflowers/demo_1.gif)

The current version (0.3.5) of the extension has been submitted to Chrome Extension Store for review and would be published if no issues found.

## Future Works

1. Apply the concept to other languages - Katakana, Hiragana, Chinese characters, and more.
2. Distinguish different cyberflowers by their shapes instead of color, as those with sharper outline and scarer looks should be different from those with soft outline and an appealing look in terms of sentiment and emotion representation.
3. Instead of using a *sentiment* model, try *emotion* models as they'll have more dimensions and represent the original content more accurate.

## References

1. Prior works - Peiling Jiang's [accordion book design for A Clockwork Orange](https://blog.jpl.design/posts/typography/a-clockwork-orange/)
2. [Typography - Wikipedia](https://en.wikipedia.org/wiki/Typography)
3. [Nombre Redondo](https://www.marinavictoria.space/nombre-redondo) by Marina Victoria (after presentation)

## Technical References

1. [Determine the position index of a character within an HTML element when clicked - Stack Overflow](https://stackoverflow.com/questions/8105824/determine-the-position-index-of-a-character-within-an-html-element-when-clicked)
2. [Get Position of text inside a HTML element - Stack Overflow](https://stackoverflow.com/questions/30061542/get-position-of-text-inside-a-html-element)
3. [Sentiment - ml5.js](https://learn.ml5js.org/docs/#/reference/sentiment)
4. [Getting Started Tutorial - Chrome Extension](https://developer.chrome.com/extensions/getstarted)

## Links

1. [GitHub Repository](https://github.com/peilingjiang/cyberflowers) for the extension
2. [GitHub Repository](https://github.com/peilingjiang/ima-courses/tree/master/s20-pixel/final_cyberflowers) for the example p5.js sketches
3. [Embedded p5.js sketch](https://editor.p5js.org/peilingjiang/present/b6SH4VwL1) (Matrix)
4. [Embedded p5.js sketch](https://editor.p5js.org/peilingjiang/present/ixM4XnkKR) (Formation)
5. [Embedded p5.js sketch](https://editor.p5js.org/peilingjiang/present/hFP05DMUk) (Composition)
6. [Embedded p5.js sketch](https://editor.p5js.org/peilingjiang/present/-CYsUUWxC) (Groups)