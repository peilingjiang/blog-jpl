---
author: "Peiling Jiang"
date: "2020-09-13"
title: RAWGraphs
type: posts
bookToc: false
---

Learning and play with RAWGraphs, an open web tool to create custom vector-based visualizations on top of the [d3.js](https://github.com/d3/d3) library.

## Scatter Plot

This visualization answers the question **How the housing prices correlate with the location in the city of Beijing?** I firstly used the dataset for a machine learning course [assignment](/posts/f19/machine-learning-for-the-arts/more/housing-price) around a year ago. Besides the LAT and LNG value from the dataset, after downloading the `.svg` file from RAWGraphs website, I also added another layer - the map of Beijing - to the plot to make the visualization more meaningful and easier to understand.

{{< photo src="/info-design/raw/1.webp" alt="Visualization 1" width="70%" >}}

## Beeswarm Plot

This plot tells **How many space missions each country has conducted and how much did them cost?** Each ellipse represents a mission and the radius correlates with the cost of it. However, this graph might be misleading on the *frequency* of the missions as larger swarm height doesn't necessarily mean more missions during the period.

{{< photo src="/info-design/raw/2.webp" alt="Visualization 2" width="70%" >}}

## Parallel Coordinates

Unlike the former plots, this plot explains, or at least tries to illustrate, a concept instead of a knowledge, answering the question **How might a credit card fraud detecting system work?** Each dimension represents a value that machine learning system takes and considers when classifying an incoming transaction (e.g. total amount, time). Due to confidentiality issues, publisher of the dataset didn't disclose the actual original catagories of data. However, visual animals have already found the enough useful information. (The original dataset has 28 dimensions and I only randomly picked part of them due to space constrains.)

![Visualization 3](/info-design/raw/3.svg)

## References

1. [RAWGraphs](https://github.com/densitydesign/raw) (GitHub)
2. [d3.js](https://github.com/d3/d3) (GitHub)
3. [Kaggle](https://www.kaggle.com/) (Owned by Alphabet Inc.)
    - [Housing price in Beijing](https://www.kaggle.com/ruiqurm/lianjia)
    - [All Space Missions from 1957](https://www.kaggle.com/agirlcoding/all-space-missions-from-1957)
    - [Credit Card Fraud Detection](https://www.kaggle.com/mlg-ulb/creditcardfraud)

*This page contains WebP images that are not supported by browsers including Safari 13.*
