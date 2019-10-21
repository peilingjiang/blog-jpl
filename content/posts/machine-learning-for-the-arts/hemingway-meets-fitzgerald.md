---
author: "Peiling Jiang"
date: "2019-10-19"
title: Hemingway Meets Fitzgerald
tags: ["IMA", "Fall19"]
categories: ["Project"]
type: posts
bookToc: true
---

## What would they write?

Hemingway and Fitzgerald are two of my favorite writers. The tiny project I did for this week, ***Hemingway Meets Fitzgerald***, is based on an assumption that could never happen:

What if Ernest Hemingway (1899-1961) and F. Scott Fitzgerald (1896-1940) could *write together*? How could their writing style affect each other and tell a story that has never been told before?

What's more, Fitzgerald is known for his descriptive language while Hemingway habitually used the word "and" in place of commas to convey immediacy and simplicity, with a writing style shaped "in reaction to [his] experience of world war." I was wondering how new sentences could be constructed this this mixed writing style.

### Data

I found two world famous novels for each writer: *The Old Man and The Sea* and *The Sun Also Rises*, *The Great Gatsby* and *The Beautiful and Damned*. The plain txt files that can be directly preprocessed and fed into model were downloaded from [Project Gutenberg](https://www.gutenberg.org/) website.

## CharRNN

The first problem I had when exploring this week's topic is the built-in [CharRNN](https://learn.ml5js.org/docs/#/reference/charrnn) library of ml5: the examples were not working on the p5 web editor. And error kept bumping up even before I downloaded the file and setup a local server. And the on-site text RNN training is not available yet. So I had to train my own model first outside of the friendly environment of ml5 first, which would also be my first time doing machine learning without p5 and ml5.

### Ubuntu

I found the documentation for vanilla CharRNN which then pointed me to a later faster version called TorchRNN, with dependencies of `torch` and `nn`. Since it's recommended to train a model in Linux environment, I installed Ubuntu and tried to follow the instructions. However, tons of errors occurred and I had to uninstall and reinstall torch, LuaJIT or LuaRocks again and again... while the problems just evolved to newer ones. I had to stop for a final project for another class.

### torchRNN

Fortunately, a detailed and beginner-friendly documentation for running the model on MacOS by amazing Jeff Thompson was linked on the torch-rnn page. I could follow the instructions can then train the model on Mac directly. Although there were still several errors around the package and system versions, the community forum helped me went through all of them.

Finally, with the line:

```terminal
th train.lua -input_h5 data/h-m-f.h5 -input_json data/h-m-f.json
```

The training started. With the default setting, there were 50 Epochs and the whole training took around 1 hour (with no GPU acceleration). Disappointingly, the loss couldn't go lower than around `1.4`. And the outcome of the model is also unreadable (which was also because the `temperature` was set to `1` which means noisy and creative output):

```
_L! MrGDA. Nossiginging to drip," I said to him, out of cigorally to go and thing was an afternoonle of Myrt me after him,
God, sixters," I said.
"No worked," said Riveralpom.
"Don't he name," Bill said we cramp lose the house--all.
The water. So he was his stars and sitting to
Brett seemed his bag
```
(Lines manually broke)

I went through the options and started training with several customizations:

```terminal
time th train.lua -input_h5 data/h-m-f.h5 -input_json data/h-m-f.json -gpu -1 -batch_size 4 -seq_length 50 -print_every 100 -checkpoint_every 5000 -max_epochs 30
```

The time was tripled. And creative writings look kind of better:

```
He bulls and a time that the man was a good week as the posts of the fish. There was no longer in the street and see the houses of the trees and the man between the taxi to the bar. They were started and started to his time with a street of his grandfather and the great transity and the count was a
```

However, one thing I didn't notice is that there's no direct way mentioned in the tutorial to export and save the trained model. All I got is a `checkpoint` json file to be called by `th sample.lua -checkpoint cv/checkpoint_180000.t7 -length 300 -gpu -1 -temperature 0.2` within the `torch-rnn` project. Everything looked like to be restarted.

### ml5

Finally, I found the models<sup>5</sup> written in Python using Tensorflow by Cristóbal. It is 100 times easier to setup. Using NYU's HPC resources, I was also able to train my models much faster.

```
73846/73850 (epoch 49), train_loss = 1.254, time/batch = 0.032
73847/73850 (epoch 49), train_loss = 1.277, time/batch = 0.032
73848/73850 (epoch 49), train_loss = 1.281, time/batch = 0.032
73849/73850 (epoch 49), train_loss = 1.274, time/batch = 0.032
```

Although the loss is still above one, I can finally get the p5 sketch working. The interface has three major sections: **Hemingway wrote**, **Fitzgerald wrote**, and **\*They* might write**, starting with the assigned word. The first two sections are based on my previous work of `Trie` model for an [assignment](https://py.mit.edu/spring19/labs/lab5) last semester about autocomplete. Actually, the model introduced in this lab assignment was the first thing came into my mind when I learned about RNN. Unfortunately, the code was written in Python and by the time I resolved all ml5 and model training problems, I have no time to look into the way to call it from JavaScript.

{{< hint warning >}}
In-progress.
{{< /hint>}}

> The code of the project is now on [GitHub](https://github.com/peilingjiang/ima-courses/tree/master/f19-ml-art/hemingway-meets-fitzgerald).<br>
> I couldn't upload the sketch to p5 web editor since it refuses accepting some files in the model folder.<br>
> UPDATE: The project is now deployed with Netlify with this [LINK](https://h-meets-f.netlify.com).

## Future Works

1. Instead of printing out sentences, with machine learning on [handwriting](http://blog.otoro.net/2017/01/01/recurrent-neural-network-artist/), I might be able to display the paragraph written by each author in their own handwriting, and the mixed writing sample with the mixed handwriting style.

2. Instead of having just two beloved writers, users might be able to choose from a group of them and mix as they like.

3. Train the model with modified options and try to get better results.

## References

1. [karpathy/char-rnn](https://github.com/karpathy/char-rnn)
2. [jsjohnson/torch-rnn](https://github.com/jcjohnson/torch-rnn)
3. [Getting started with Torch](http://torch.ch/docs/getting-started.html#_)
4. [Torch-rnn: Mac Install](http://www.jeffreythompson.org/blog/2016/03/25/torch-rnn-mac-install/)
5. [ml5js/training-charRNN](https://github.com/ml5js/training-charRNN)
6. [Generating Text with a LSTM Neural Network - Ellen Nickles](https://ellennickles.site/blog/2018/10/13/week-6-generating-text-with-a-lstm-neural-network)
7. [ysh329/deep-learning-model-convertor](https://github.com/ysh329/deep-learning-model-convertor)
