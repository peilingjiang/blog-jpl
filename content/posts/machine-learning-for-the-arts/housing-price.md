---
author: "Peiling Jiang"
date: "2019-09-25"
title: Housing Price
tags: ["IMA", "Fall19"]
categories: ["Reading", "Project"]
type: posts
bookToc: true
---

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
