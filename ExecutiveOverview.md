# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 1: Standardized Testing, Statistical Summaries and Inference

## Executive Summary

### Overview

The subreddit posts dataset was pulled from two subreddits using the publically avaialable API. The subreddits selected for this project sit within the same domain and therefore have a lof of overlapping content making classification based on the text in a given post more challenging. Our goal is accuratley classify which subreddit a post belongs too by pre-processing the post text using Natural Language Processing techniques and then applying a classification model to the cleaned/processed text data. This predictive algorithm could be useful for moderators of a given subreddit who would like to flag posts that do not belong in their thread. 

### Problem Statement

This technical report steps through the workflow of building a predictive model to accuratley predict which subreddit a post belongs in. Multiple classification models (Naive-bayes Multinomial, Naive-bayes Bernoulli, Logistic Regression, Decision Tree's and Random Forests) are evaluated in order to select a production model with the least amount of error (e.g. bias) that generalizes well to the data (e.g. low variance b/w test and train scores). 

Throughout the report we'll seek to identify trends in the text data that answers relevant questions moderators of a subreddit would have wuch as which keywords appear most frequently in a given subreddit or which features/keywords provide the most predictive power in determining whether a post should be flagged for review. The goal of this analysis is to save reddit moderators time and energy, so they can apply that effort in more constructive and creative ways for their communities. 


### Contents of this README

- Executive Summary
- Data-set Description
- Primary Findings and Insights
- Conclusions and Recommendations
- Next Steps

---

### Data-set Overview

#### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|subreddit|int64|cleaned.csv|Binary classification of which subreddit a post belongs too (1 = IOTA, 0 = IOTAmarkets)|
|selftext|string|cleaned.csv|The descriptive text that is added to a post that comes just below the title of that post|
|title|string|cleaned.csv|The title of the post|

#### Provided Data

For this project, I've used the following datasets as source data for my model. This is a cleaned version of the data that was collected from both subreddits and combined into a single file:

- [Cleaned Reddit Text Data](./data/cleaned.csv)

You can see the original sources of of the data are the two subreddits found: [here](https://www.reddit.com/r/Iota/) and [here](https://www.reddit.com/r/IOTAmarkets/)


#### Primary Findings & Insights

I selected the logistic regression model as my production model given it's performance above all other models as well as it's interpretability. When analyzing text data, it is important to know which features/keywords provide more predictive power than others. A close runner up was the Random Forests algorithm but in the end I was able to optimize better for bias and variability in the logistic regression mode. 

The production regression model scored 96.3% on the training data & 92.2% on the test data.


Through exploratory analysis of the model coefficients it is clear that the features with the largest predictive power are: 
- Binance, price, buy, MIOTA, http, really, Bitcoin, just, 10, It, So, Btc, com, think, wallet, exchange, Crypto, market  


#### Conclusion & Recommendations

It would be valuable to implement this model for any r/IOTA reddit moderator who would like to implement a better flag warning system to notify them if posts in their thread are off topic (and belong on r/IOTAmarkets). In this scenario any post would be flagged if it was classified as a 0 and belonged on IOTAmarkets. The predictive model achieves >90% accuracy and can be trusted to save some time and only flag the posts that really seem off topic. 

#### Next Steps

Moving onto the next phase of this analysis would require additional time. In order to further refine the data, it would be necissary to gather more data from each subreddit, either further back in time or layering in comments as well. I would also likely fine tune and further optimize the model to minimize False Negatives (e.g. maximize Sensitivity) to ensure we are properly flagging all posts that do not belong on our page. It is preferrable to incorrectly classify a legitimate post and then review it vs. not flagging invalid posts altogether. Additionally I would compare our classifacation models performance to other powerful classification alogrithms (e.g. SVMs) to better understand the tradeoff of a black box algorithm vs. accuracy performance. 