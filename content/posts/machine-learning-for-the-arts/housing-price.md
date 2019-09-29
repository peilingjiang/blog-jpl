---
author: "Peiling Jiang"
date: "2019-09-25"
title: Housing Price
tags: ["IMA", "Fall19"]
categories: ["Reading", "Project"]
type: posts
bookToc: true
---

> This page is a composite of Assignment 4a and 4b.

# The Dataset

After a long time wandering in Kaggle and OpenML, I finally decided to choose the dataset of [Housing price in Beijing](https://www.kaggle.com/ruiqurm/lianjia) (Housing price of Beijing from 2011 to 2017, fetching from Lianjia.com.) from Kaggle as the data I'm to collect, wrangle and build on for this week's assignment.

My interests and curiosity of housing price might be arisen by Ekene Ijeoma's *Wage Islands: Immigrants* project - a sculpture to visualize where low-wage immigrant workers can afford to rent in NYC.

## File

The original dataset is formatted in .csv file with 318852 rows (data points) and 26 columns (variables). According to the author, Qichen Qiu, it includes URL, ID, Lng, Lat, Community ID, Trade Time, DOM (days on market), Followers, Total Price, Price, Square, Living Room Num, Drawing Room Num, Kitchen Num, Bathroom Num, Building Type (1-4), Construction time, Renovation Condition (1-4), Building Structure (1-6), Ladder Ratio, Elevator, Property Rights for Five Years, Subway, District, Community Average Price.

I was confused by some variables at first since they are only displayed as a number instead of a clear definition. And the author elaborates some of them as below:

- Lng: and Lat coordinates, using the BD09 protocol. *Basically the location.*
- buildingType: Tower (1), bungalow (2)，combination of plate and tower (3), plate (4).
- renovationCondition: Other (1), rough (2), Simplicity (3), hardcover (4).
- buildingStructure: Unknown (1), mixed (2), brick and wood (3), brick and concrete (4), steel (5) and steel-concrete composite (6).
- ladderRatio: the proportion between number of residents on the same floor and number of elevator of ladder. It describes how many ladders a resident has on average.
- elevator: Have (1), not have (0).
- fiveYearsProperty: (1) if the owner have the property for less than 5 years. It's related to China's housing purchase policy.
- district: Dongcheng (1), Fengtai (2), Tongzhou (3), Daxin (4), Fangshan (5), Changping (6), Chaoyang (7), Haidian (8), Shijinshan (9), Xicheng (10), Pinggu (11), Mentougou (12), Shunyi (13).

All the data are last updated a year ago (2018) and reflect the housing prices from 2011 to 2017. Since there's a URL linked to China's largest house trading platform, I assume all these data were captured from that website.

One good thing about this dataset worth mentioning is that it provides different accuracy of some variables. For example, floor. Except recording the exact floor number of the house, the dataset also use 低 (Low), 中 (Middle), 高 (High) to help simplify the classification of this particular variable. And if our prediction is not every floor sensitive, we can just use the blurred data for the training. However, the Chinese characters also cause some problems.

## Why?

The first thing I noticed is that there are a great many of variables that could affect the price of a house. And this data can be used to learn how the housing price in Beijing is affected by construction time or the number of bathroom. Moreover, since the dataset is collected cumulatively through 7 years, it could also be used to decode the pattern of how house price is ~~changing~~ growing, and predict how it will change in the future.

## Problems

With Lng and Lat, and district number, the location is kind of clearly reflected in the data - In terms of a city like Beijing, location of the property might be the most important thing related to the price. However, 3 administrative districts are missing in this data collection. Also, due to the source of the data is a Chinese website, there's a lot of errors and garbled text in original data and I have to set encoding to GB2312 to have those text correctly displayed, while still with a lot of error.

When a data is missing, sometimes it says "nan", while others might say "未知" (unknown). I think this could also potentially confuse the machine during the training. The documentation of the dataset is also not very good, with some important description missing that I had to search in the discussion section.

## Clean

I tried several ways to prepare a cleaner dataset for the further use.

1. I split *floor*, which consists of both a character indicating the height level of the house, and the exact floor number, into two different columns: *floor class* and *floor num*. And replaced 底低中高顶 - Bottom, Low, Middle, High, Top with 1, 2, 3, 4, and 5.

2. I replaced all missing data, whether it says "nan" or "unknown" with *0*.

3. I deleted URL, ID, Community ID which wouldn't affect housing prices.

A [link](https://docs.google.com/spreadsheets/d/1Rhy7pZuvPnyn_DEmitKEgD26wNl-BPten5hMqHuPlA0/edit?usp=sharing) to cleaned small dataset is here *(NYU login required)*.

***

# The Neural Network

Then I tried an in-progress feature of ml5.js: `ml5.neuralNetwork()`.

## Titanic Dataset

First, I played with examples given in class - a model based on [Titanic Survival Dataset](https://www.openml.org/d/40945), with the following steps:

1. Clean the raw data and replace all missing data. Delete unrelated data including name, sibsp, parch, etc.
2. Try different ways of data representation:
  - Use "lived"/"died" instead of 0/1 for *survived* parameter;
  - Use "first"/"second"/"third" instead of 1/2/3 for *pclass* (passenger class) parameter.

### Variable Types

When fed into p5 web editor, the model can still be trained and predict as before. While the outcomes are different: when using numbers as labels, all the output are numbers and need to be translated by an extra piece of code to be more readable. Surprisingly, string-based labels also help the model work better with a **smaller loss**: (Epochs = 20)

survived | pclass | Average loss
---------|--------|--------------
Number   | Number | 0.531
Number   | String | 0.530
String   | Number | 0.528
String   | String | 0.485
(Losses vary between sessions and numbers above are averages of 3 trials.)

> Q: Why *loss* would vary between different sessions?

Then another question came into my mind: we were asked to clean the data by making all floating numbers integers, will this also affect the performance of the model training and the prediction? I looked into this by changing *fare* values between raw floating numbers and rounded integers. And here's the results: (Epochs = 20)

*fare* Number | loss_1 | loss_2 | loss_3
--------------|--------|--------|--------
Integer       | 0.528  | 0.529  | 0.529
Float         | 0.528  | 0.529  | 0.528

As a result, integers don't really help the training perform better. However, all results above might only be true for the very specific algorithm that ml5.neuralNetwork is using.

### Idle Columns

To further test the feature, I added an extra column that will not be used by the model nor mentioned in `inputs` in the code, and the training couldn't finish with a TypeError always occurred after Epoch 19 (the last Epoch but one).

    TypeError: Cannot convert undefined or null to object

### Hyperparameters

All the experiments above are based on default settings of ml5.neuralNetwork. But we can also modify those based on our interests.

```js
let nnOptions = {
  activationHidden: 'sigmoid', // 'relu', 'tanh'
  learningRate: 0.25,
  hiddenUnits: 16,
  modelLoss:  'categoricalCrossentropy', // 'meanSquaredError'
};

let trainingOptions = {
  epochs: 32,
  batchSize: 64
};
```

#### activationHidden

> Reference: [Activation Functions in Neural Networks](https://towardsdatascience.com/activation-functions-neural-networks-1cbd9f8d91d6)

<img src="/machine-learning-arts/housing-price/sigmoid_relu_tanh.png" alt="Training performances of Sigmoid, ReLu, and tanH" width="100%">
<caption>Training Performance when using **Sigmoid**, **ReLu**, and **tanH**</caption>

While the default activation function is $\sigma$ (sigmoid), which ranges from 0 to 1 - perfect when need to predict something with a confidence, there're also many other functions to choose from.

- ReLu: range $[0, \infty)$

$$f(x)=\cases{
  0 &x $\lt$ 0\cr
  x &x $\geqslant$ 0}$$

The training became much faster when I set `activationHidden: 'relu'` with a smaller loss of around 0.44. (While the loss of Sigmoid-based training is around 0.49.)

- tanH: range $(-1, 1)$

$$f(x)=tanh(x)=\frac{2}{1+e^{-2}}-1$$

I feel the training is even faster with tanH as activation function. The loss is around 0.47.

#### learningRate

**Learning rate**, together with **hidden units** and **batch size**, should affect the performance of each time the learning algorithm working through the entire training dataset. And the more epochs the training has, the more opportunities the training dataset will have to update the internal model parameters thus will have better results. (Epochs = 15, Size of Training Set = 1308)

Test     | learningRate | batchSize | hiddenUnits | loss_1 | loss_2    | loss_3       | Average | $\sigma$
---------|--------------|-----------|-------------|--------|-----------|--------------|---------|---------
**lR1**  | 0.25         | 64        | 16          | 0.491  | 0.493     | 0.493        | 0.4923  | 0.00115
lR2      | 0.0001       | 64        | 16          | 0.783  | 0.666     | 0.762        | 0.737   | 0.06238
lR3      | 1            | 64        | 16          | 0.474  | 0.480     | 0.482        | 0.4787  | 0.00416
lR4      | 5            | 64        | 16          | 0.514  | **5.519** | 0.586        | 2.2063  | 2.86908
**bS1**  | 0.25         | 1 *       | 16          | 0.442  | 0.444     | 0.445        | 0.4437  | 0.00153
bS2      | 0.25         | 128 **    | 16          | 0.502  | 0.509     | 0.500        | 0.5037  | 0.00473
bS3      | 0.25         | 1308 ***  | 16          | 0.617  | 0.626     | 0.629        | 0.624   | 0.00624
**hU1**  | 0.25         | 64        | 2           | 0.500  | 0.498     | 0.523        | 0.507   | 0.01389
hU2      | 0.25         | 64        | 64          | 0.523  | 0.522     | 0.537        | 0.5273  | 0.00839
hU3      | 0.25         | 64        | 1000        | **5.519** | **5.519** | **5.599** | 7.2123  | 2.93294

\* **Stochastic Gradient Descent** - Takes much longer time for each epoch to complete. (Bathes per epoch = 1308)<br>
\** **Mini-Batch Gradient Descent** (Bathes per epoch = 10)<br>
\*** **Batch Gradient Descent** - Very fast. (Bathes per epoch = 1)

As a result, the default settings (lR1) of ml5.neuralNetwork has the most stable training output. Also, smaller batch sizes will help improve the output loss by trading training time.

#### epochs

Intuitively, the more epochs the training model has, the better the output will be. And it was proved through the experiments recorded below. (Use default settings for learning rate, batch size and hidden units.)

epochs    | loss_1 | loss_2 | loss_3 | Average | $\sigma$
----------|--------|--------|--------|---------|----------
1         | 0.628  | 0.644  | 0.654  | 0.642   | 0.01311
5         | 0.535  | 0.537  | 0.531  | 0.5343  | 0.00305
10        | 0.500  | 0.505  | 0.503  | 0.5027  | 0.00251
20        | 0.486  | 0.487  | 0.489  | 0.4873  | 0.00153
50        | 0.475  | 0.475  | 0.472  | 0.474   | 0.00173
100       | 0.463  | 0.456  | 0.453  | 0.4573  | 0.00513

#### modelLoss

> Reference:<br>
> [Usage of loss functions - Keras Documentation](https://keras.io/losses/)<br>
> [Why You Should Use Cross-Entropy Error ...](https://jamesmccaffrey.wordpress.com/2013/11/05/why-you-should-use-cross-entropy-error-instead-of-classification-error-or-mean-squared-error-for-neural-network-classifier-training/)<br>
> [Why is the Cross Entropy method preferred over Mean Squared Error?](https://stackoverflow.com/questions/36515202/why-is-the-cross-entropy-method-preferred-over-mean-squared-error-in-what-cases)

According to the reference, Cross-Entropy Error is preferred for **classification** (this case), while Mean Squared Error is one of the best choices for **regression**. In the previous sections, I played with the labels of the same meanings while in different data types: string or integer. And would it be affected by modelLoss parameter with `'categoricalCrossentropy'` or `'meanSquaredError'`? (Epochs = 15)

modelLoss   | survived/pclass/sex | loss_1 | loss_2 | loss_3 | Average | $\sigma$
------------|---------------------|--------|--------|--------|---------|----------
categorical | Number              | 0.495  | 0.493  | 0.499  | 0.4957  | 0.00306
meanSquared | Number              | 0.493  | 0.493  | 0.495  | 0.4937  | 0.00115
categorical | String              | 0.495  | 0.492  | 0.497  | 0.4947  | 0.00252
meanSquared | String              | 0.489  | 0.496  | 0.495  | 0.4933  | 0.00379

We can see that either model loss type doesn't really make a huge difference in terms of average performance here, and the advantage of either error model isn't shown through the data. However, Cross-Entropy Error makes string data perform more stable and Mean Squared Error makes number data perform more stable.

## House Price in Beijing

Then I tried to train my own model with `ml5.neuralNetwork()`. The data is much more complex with more columns of parameters and more rows of datasets.

### Wrangling

According to the results from Titanic exercise, I made following changes to my dataset from last data wrangling practice ([Link](https://docs.google.com/spreadsheets/d/1ICIMnDOVvNj4btbWYJqoXScIlphX4v0LEgRNpQvYjmI/edit?usp=sharing) to the final version for training. *(NYU login required)*):

- Delete all idle columns and make it as simple as possible. Output: totalPrice. Inputs: tradeTime, square, livingRoom, kitchen, bathRoom, floorClass, constructionTime, elevator, fiveYearsProperty, subway, district, and communityAverage.
```js
let nnOptions = {
      modelLoss:  'meanSquaredError',

      dataUrl: 'house_price_clean_small_2.csv',
      inputs: ['tradeTime', 'square',
      'livingRoom', 'kitchen', 'bathRoom',
      'floorClass', 'constructionTime',
      'elevator', 'fiveYearsProperty', 'subway',
      'district', 'communityAverage'],
      outputs: ['totalPrice'],
      task: 'regression', // Different from the Titanic example
      debug: true
};
```
- Since it'll be a linear prediction - the price number of a house, I'll use `"meanSquaredError"` for the modelLoss type. Thus all data should be transferred to numerical type. For example, 1 for *Yes*, and 0 for *No*. However, for *district* number, which doesn't represent the housing prices in a linear way (Houses in District 1 are not necessarily cheaper than those in District 7), so I still keep it as strings of names of the districts.
- Dates are all formatted as numbers without any punctuation. For example, Aug. 9th, 2016 are formatted as *20160809*.
- Instead of using 0 for missing data in the former practice, I choose to use the method introduced in Titanic tutorial - to calculate the average and then pick random numbers within one standard deviation of the average for the missing data.

Here's the first rows of the final .csv file:

```csv
totalPrice,tradeTime,square,livingRoom,kitchen,bathRoom,floorClass,constructionTime,elevator,fiveYearsProperty,subway,district,communityAverage
415,20160809,131,2,1,1,4,2005,1,0,1,Chaoyang,56021
575,20160728,132.38,2,1,2,4,2004,1,1,0,Chaoyang,71539
1030,20161211,198,3,1,3,3,2005,1,0,0,Chaoyang,48160
297.5,20160930,134,3,1,1,1,2008,1,0,0,Changping,51238
392,20160828,81,2,1,1,3,1960,0,1,1,Dongcheng,62588
```

### Training

Fortunately, although several annoying red alerts popped at first, none of them were unreasonable and I was able to solve them quickly. The biggest problems came out of the difference between the task of `"classification"` and `"regression"`. First, I need to look up the *preview* version of ml5.js, and figured out "regression" is the task label that I would use. And when `gotResults()`, I need to print out `results.outputs.value` instead of `results[0].label`.

```js
function gotResults(err, results) {
  if (err) {
    console.error(err);
  } else {
    console.log(results);
    select('#result').html(`prediction: ${results.outputs.value.toFixed(3)}`);
  }
}
```

Here's the [**link**](https://editor.p5js.org/peilingjiang/sketches/3i8abog1P) to the p5 web editor of the project.

### Results

The model seems working well for most of times, and sometimes making reasonable predictions for test inputs. It's performance, however, is quite unstable. Sometimes the learning curve (loss) drops dramatically at the beginning, while sometimes it stays the same for the whole time.

<img src="/machine-learning-arts/housing-price/learning_curves.jpg" alt="Learning Curves" width="100%">
<caption>Learning Curves of 50/20/30/30 epochs.</caption>

And they are all making very different predictions. The top two (50 and 20 epochs) predict the price to be 570 and 470, while the bottom two (30 epochs) predict the price to be 810 and 27, which is the most outrageous one.

Then I tried to set `learningRate = 0.05` for smaller changes during each epoch, and `hiddenUnits = 32`, and the performance and predictions became much more stable. The final prediction of the price of the virtual house mentioned above should be around 700-800.

However, the model also acts very weirdly sometimes.

As far as I'm concerned, it wouldn't work when I tried to upload and feed larger datasets. I tried with a very small dataset of 2000 rows (compared to original 318852 rows) and the model could run. However, when I tried with even 4000 or 5000 rows, the model started to fail and outputted **NaN** for loss, while still "unconsciously" ran to the last epoch and started predicting - NaNs.

      Epoch: 0 - loss: NaN
      Epoch: 1 - loss: NaN
      Epoch: 2 - loss: NaN
      Epoch: 3 - loss: NaN
      ...

# Ideas

> In addition to documenting your exercise, reflect on your experience using a new feature of an open source library. One of the big challenges of designing a higher level library for machine learning is finding the right balance between hiding the lower level details and allowing for flexibility / customization. Thinking about the difference between programming all the elements of the model and working with the ml5.neuralNetwork() function, how did this balance sit with you? Is the code easy for you to follow? Do you understand what the library is doing? What are some roadblocks you anticipate for using the library with your own data? Do you have any ideas for improvements or modifications to the ml5.js library?

With a programming background of python, I used to include many smaller, more specific libraries in the code, unlike larger, and one-for-all libraries like p5.js and ml5.js. For me, to make the library easier to use, with more built-in capabilities, must also sacrifice the customizability and flexibility. For example, I have no idea how ml5.neuralNetwork can be trained with an article or a group of pictures, instead of .json or .csv files. This might also because of the lack of documentation at this stage. `ml5.neuralNetwork()` help us a lot by hiding inner components carefully, and we only need to adjust Hyperparameters that would directly affect the training performance: activation function, learning rate, hidden units, and error type, instead of starting with programming a perceptron.

Currently, all the training need to be done during the `setup()`, and would it be possible to have users interactively input data for training from the p5 canvas, and start training afterwards?
