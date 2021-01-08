---
layout: post
title:      "My First NLP Project"
date:       2021-01-08 19:05:30 +0000
permalink:  my_first_nlp_project
---


## Purpose
At this point in my data science journey, I have completed several Exploratory Data Analyses, Regression models of various kinds, and binary classification problems. All of these things are useful skills for a data scientist, but all of them have been performed using entirely numerical data. In the real world, more and more of the data we collect is in the form of text. It’s important that I learn to deal with these types of data sets if I want to have a well rounded understanding of data science as it applies to real world scenarios. 

With this in mind, I chose to pursue a simple Natural Language Processing project to get the basics. In this project I used a selection of ~9000 tweets describing Apple or Google products that have been labeled as positive, negative, or neutral. The dataset is available here. I will be performing one of the most common types of NLP tasks, Sentiment Analysis, and documenting what decisions I had to make as well as why those were the decisions I made. If you are interested in viewing the github repository for this project, including the Jupyter Notebook with my code, you can find that here.

## Getting Familiar
As this dataset is primarily text data, I had to approach it a little differently from my previous projects that were composed primarily of numerical data. To this end, my first step was to open the 'tweets.csv' file in Excel or Sheets to try to get a feel for what kind of preprocessing steps may be required. Scrolling through the file, I saw that there were several questions I would have to answer over the course of my project.

How do I deal with missing data?

Is there a difference between "I can't tell" and "No emotion toward brand or product"?

Do I want to gauge sentiment for specific brands and products or just sentiment overall?

Do neutral tweets matter to my model, and if so do I have an imbalanced data problem?

How do I handle mentions and hashtags?

All of these are questions that must be answered before I can begin building an effective model. I began by working through the first two problems and then setting up the data set for success in answering the remaining questions.

### How do I deal with missing data?
In this data set, there was only one missing data point, which was a tweet with no text. In this instance, I felt comfortable dropping that observation, because it offered no value to our model.

### Is there a difference between "I can't tell" and "No emotion toward brand or product"?
In viewing tweets from both categories, I determined that both categories included tweets that were either purely informational or too vague to classify. I could not tell a difference between them, so I felt safe combining the categories.

### How do I handle mentions and hashtags?
I used a tokenizer that strips twitter mentions from tweets, but I left hashtags because I felt they could provide value to our models.

### Do I want to gauge sentiment for specific brands and products or just sentiment overall?
In my models, I gauge sentiment overall, and as time allows will return to explore sentiment across brands and products.

### Do neutral tweets matter to my model, and if so do I have an imbalanced data problem?
Given that more than half of our observations are marked as neutral, I opted to keep them for my models. I feared that removing those tweets would cause overfitting of our model.

## The Model
For my initial model, I began with a simple Naive-Bayes Multinomial classification. I chose this model because it’s the one I had seen most often, and the implementation is straightforward, allowing me to iterate further once observing the results. 
