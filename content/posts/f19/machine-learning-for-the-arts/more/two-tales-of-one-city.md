---
author: "Peiling Jiang"
date: "2019-10-27"
title: Two Tales of One City
type: posts
bookToc: true
---

It was the best of times, it was the worst of times, it was the age of wisdom, it was the age of foolishness, it was the epoch of belief, it was the epoch of incredulity, it was the season of Light, it was the season of Darkness, it was the spring of hope, it was the winter of despair, we had everything before us, we had nothing before us, we were all going direct to Heaven, we were all going direct the other way—in short, the period was so far like the present period, that some of its noisiest authorities insisted on its being received, for good or for evil, in the superlative degree of comparison only. (*A Tale of Two Cities*, Charles Dickens)

## Two Tales

The conflict of two different systems has never been as prominent and breathtaking as the ongoing Hong Kong incident. Outside of the city once regarded as one of the most important economic centers in the world, however, two extremely distinct tales covering the story can be found on the borderless Internet. Press from the western world states it as a prodemocracy protest against communist China, fight for freedom, and the enforcement Hong Kong police is applying to peaceful protesters is illegal and improper. Press from China states it as a riot backed up by western countries, and police is respectful for protecting Hong Kong people from the violent thug.

I'm curious how meta narrative over the press can form and constrain the reports into one stream of information. And in this project, I'll train different models based on different sets of news from "western world" and China, and if any, see how contradictory and bias both of them could be - when learning just from one information source.

## Data Collecting

### Crawler

The data collection process for this project took **99.999%** of the time. I didn't realize how difficult it could be to gain a reasonable amount of news reports for machine learning to learn, until I started to collect them.

Firstly, I tried to write a *web crawler* to download text from official websites of major press ~~of fake news~~ like CNN and BBC with [Selenium WebDriver](https://www.seleniumhq.org/projects/webdriver/). Since every website has its own page and html rules, I need to adjust my code ([GitHub](https://github.com/peilingjiang/ima-courses/blob/master/f19-ml-art/two-tales-of-one-city/data-collection/main.py)) for each situation to get content from them. After hours of debugging, the code could work in the list view and download `title` and `url` of articles, but when it comes to the `content`, websites plays very well of avoiding anyone to read even directly from `html` tags. I had to give up collecting the body part, but train the model only with titles of the articles.

### API

Although my own code works fine getting titles from the websites, the process actually relies on a web driver opening websites locally and reading content from the html file. It's really slow and taking too much computing and connection resources. Then I finally realized that those press should have web APIs for people to use. The answer is YES and NO. CNN has its own content [API](http://developer.cnn.com/) but you need to apply first, and the project is terribly maintained. Many others don't have, or I couldn't find clear documentations.

Finally, I found [NewsAPI](https://newsapi.org/) that could easily fetch `title` and even `content` (for paid users) from news resources. I set it up and it ran very fast. However, three very annoying facts made me have to re-start again and try to find another API:

- Its support of Chinese sourced press is still beta and problematic.
- The free developer account can only get 100 results.
- There's a limit of length of text returned for free accounts, and sometimes the result might not be complete.

Finally-ly, I found Microsoft Azure News API. And wrote four files with it ([Code](https://github.com/peilingjiang/ima-courses/blob/master/f19-ml-art/two-tales-of-one-city/data-collection/api.py)): `zh_name.txt` (1.7MB), `zh_description.txt` (8.9MB), `en_name.txt` (4.1MB), and `en_description.txt` (15.8MB). These files are also available on [GitHub](https://github.com/peilingjiang/ima-courses/tree/master/f19-ml-art/two-tales-of-one-city/data-collection/results).

## Training

I need to train 4 models in total: 2 for title writing, and 2 for description writing.

The training of the models were rather painless and fast. The loss of all four models went down to nearly 0 after several thousands of batches. However, there's some problems of training-charRNN: when you continuously train different models and don't delete or move out models generated from the previous training, the model saved will only always represent the result of the first training, even they are named differently by the name of input file. That's why when I trained one file after another, all I got was the same result (either both Chinese or English):

<img src="/machine-learning-arts/two-tales-of-one-city/process_1.png" alt="Screenshot of the Project in Progress" width="100%" style="opacity:0.75;filter:alpha(opacity=75);">
<caption>Screenshot of the Project in Progress</caption>

You can see both descriptions are in English and both titles are in Chinese, it's simply because I trained both `title` writing models on my own laptop - started with `zh` file, and trained both `description` writing models on NYU HPC - started with `en` file. Is it a bug of training-charRNN ([#18](https://github.com/ml5js/training-charRNN/issues/18))?

I'll then have to retrain the models - which takes hours.

## Deploy

The project is now on [GitHub](https://github.com/peilingjiang/ima-courses/tree/master/f19-ml-art/two-tales-of-one-city) and a live demo is hosted through [Netlify](https://two-tales.netlify.com).

<img src="/machine-learning-arts/two-tales-of-one-city/final_screen_1.png" alt="Final 1" width="100%">

<img src="/machine-learning-arts/two-tales-of-one-city/final_screen_2.png" alt="Final 2" width="100%">

The *windows* can be dragged around, like real *windows*, making it more like real web browser interface. Though I didn't have time make the UI details perfect. (It's also because of the style of the project I chose to have.) Every time you click on either of the windows, the "desktop" background image will change (based on image URLs gained through NewsAPI).

## Future Works

1. Now the two models show how binary narrative could affect people's point of view of one fact. More interactively, what if the program could rephrase one same piece of words input by the user - to two different narratives, based on two models. This could disclose how facts could be reproduced into stories, that aren't necessarily fake, but serve the speakers' interests. This might beyond the capability of LSTM models but I'm curious if other machine learning models can make it happen.

2. To make the project more understandable for people only understand English or Chinese, I'll try to use Google Translate API to translate the text into one selected language.

3. ~~Refresh button on each window.~~

4. Think about how CharRNN works with languages other than English. How does it perform with Chinese training text?

## References

1. [Hong Kong - Wikipedia](https://en.wikipedia.org/wiki/Hong_Kong)
2. [A Tale of Two Cities - Wikipedia](https://en.wikipedia.org/wiki/A_Tale_of_Two_Cities)
3. [Selenium WebDriver](https://www.seleniumhq.org/projects/webdriver/)
4. [News API](https://newsapi.org/)
5. [mattlisiv/newsapi-python](https://github.com/mattlisiv/newsapi-python)
6. [Azure News API](https://docs.microsoft.com/en-us/azure/cognitive-services/bing-news-search/news-sdk-python-quickstart)
7. [Create a Cognitive Services resource using the Azure portal](https://docs.microsoft.com/en-us/azure/cognitive-services/cognitive-services-apis-create-account?tabs=singleservice%2Cwindows)
8. [Perform a news search with the Bing News Search SDK for Python](https://docs.microsoft.com/en-us/azure/cognitive-services/bing-news-search/news-sdk-python-quickstart)
