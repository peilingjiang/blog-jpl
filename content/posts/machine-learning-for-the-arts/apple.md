---
author: "Peiling Jiang"
date: "2019-09-15"
title: aPPle!
tags: ["IMA", "Fall19"]
categories: ["Project"]
type: docs
bookToc: true
---

# aPPle!

🍎🥮🐟🍊🍳🍞🍗🍔🍟🥔🍚🥘💣

**aPPle!** is a webcam game powered by p5.js and ml5.js. In the game, various kinds of food will fly into the screen and the player need to choose only healthy food, that helps to lose weight, to eat. The player also need to dodge bombs flying into the screen from time to time. Office chair with wheels is recommended to use for playing. Here's a [quick link](https://editor.p5js.org/peilingjiang/full/043oUt7_c) to play on p5 web editor.

# Game

The idea comes from my struggle of keeping a diet. There're so many kinds of food that potentially contain a great many of calories and we need to distinguish them from the healthy ones.

The screen is divided into three sections: Left, Center, and Right. And the food can be eaten by the user when flying to the middle of each section.

<img src="/machine-learning-arts/apple/game_intro.png" alt="Game Introduction" width="100%" >

## Winning conditions

The player need to eat enough healthy food to win the game while avoid eating junk or high carbohydrate food. Different food has different "bonus" or "penalty". Since it's a game helping me losing weight (itself involves a lot of workout when playing), the bonus will take off numbers of a preset goal and the player will win when the number is zero.

Food          | Bonus (-)               | Food        | Penalty (+)
--------------|-------------------------|-------------|--------------
🍎 Apple      | -20, trigger BoostShoot |🥘 Hotpot   | +20
🥮 Mooncake    | -10                     |🍗 Chicken  | +10
🐟 Fish       | -10                     |🥔 Potato   | +10
🍊 Tangerine  | -5                      |🍔 Burger   | +5
🍳 Egg        | -5                      |🍟 Fries    | +5
🍞 Bread      | -5                      |🍚 Rice     | +5

Also, the player need to dodge the bomb flying into the screen. The setting increases the hardness and playfulness (and workout) of the game.

{{< video src="/machine-learning-arts/apple/apple_game.mp4" width="100%" >}}

## Constrains

Teachable Machine is the technology behind the scene. However, this interface is incapable of training models that could recognize the position of a particular thing, in this case, my mouth. So I have to set a **eating area** at the middle of the screen and set 3 different body position labels. A more real game should detect the real-time position of the mouth and whether or not it's opening solely, and calculate the "collision" of the opening area and the food.

# Teachable Machine

## Labels

The model used in the project is trained with Teachable Machine interface. There are **7** different labels in total for the machine to learn recognize:

- Left position with mouth closed
- Left position with mouth open
- Center position with mouth closed
- center position with mouth open
- Right position with mouth closed
- Right position with mouth open
- Player in the picture

Mouth can be either open or close for 3 different body positions, and one more for no player in the frame (dodge). To make the model robust, I tried to include photos of me in different clothes, and also called my roommates to open and close their mouth in front of my webcam.

## Training

{{< figure src="/machine-learning-arts/apple/train_outcome.png" alt="Train Interface" width="100%" >}}

In the end, each label has around 500 picture to train and the training process takes around 10 minutes. While body in different positions might be easy for the machine to learn, the opening and closing of the mouth, in other words, the most important part of the whole gaming experience, seemed hard for it to distinguish as the first version. I had to reduce the influencing factors that could have confused the model: making the background white and clean, stopping calling other people to be recorded, putting my head at the same height for all positions, and opening my mouth as big as possible during the recording - since machine learning models will always find "the closest label," it shall be helpful to make different scenarios as unlike to each other as possible. The performance of the model then improved a lot.

{{< video src="/machine-learning-arts/apple/train_process.mp4" width="100%" >}}
{{< video src="/machine-learning-arts/apple/model_test.mp4" width="100%" >}}

 However, having all different 7 labels is solely because the model trained with teachable machine can't locate the mouth. While *Train models on poses* has an interface with positioned eyes, nose and ears, but there's no way to directly gain data from it.

# Future Works

This is my first p5.js project and my first game design. And it's still a beta. There're still a lot can be done but due to time and the scale of this weekly assignment that cannot be finished within the weekend. The future works include:

1. Better sound effects and background music.
2. Multiplayer system, and potential connection with the course Collective Play - two players play a same game on two computers sharing one food space.
3. As mentioned in the constrains, current machine learning model is incapable of finding the position of the mouth thus I have to set 3 body positions and an eating area. The ideal gaming experience would be the user could decide and eat the food wherever on the screen by moving the mouth around.

> Media on this page is blurred due to privacy concerns.
