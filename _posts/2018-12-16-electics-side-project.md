---
title:  "Overview of Electics, 2019 Indonesia Presidential Election Analytics - #1"
description: 2019 Presidential Election analytics side project
tags: [30daysofwriting, tech]
---

Here comes my first post of the #30DaysOfWriting challenge.

I have been thinking this whole day to decide what to write on my next post. So here I am going to talk about my ongoing winter project to fill my boring holiday: Electics, 2019 Indonesia Presidential Election analytics. So let me break this thing down into two parts: **Project Goal** and **Components**

## Project Goal
As you might have guessed the name *Electics* comes from the combination of the two words: *Election* and *Analytics*. It is also a pun to *electric*, so I hope this project can electrify both of those stupid supporters from either side (**just kidding**). I chose this particular topic because I think it will be the most talked about topics in 2019. 

Moreover, this would be my starting point to become a data engineer. I am still learning, though. So contact me whenever I did anything wrong while building this project. I will keep you all posted on the progress of the project.

This project will try to identify from a tweet/post/anything whether a person will vote for #1 or #2. From this data we can make a plot/graphical summary of the people's choice, judging from what they post online. 

This can be achieved by collecting realtime data from Twitter, Facebook feeds, and (hopefully) Instagram. I will be focusing on Twitter first (I doubt that the Facebook's developer APIs  is still working, judging from their latest [data breach scandal](https://www.nytimes.com/2018/09/28/technology/facebook-hack-data-breach.html), they might have changed it ). Of course we need NLP, ML, and stuff to do this project. That's why I'll also make a simple data labeler site too to collect labeled data from the crowds. 

## Components

We need four services to make the project:

1. Data crawler (Tweets, posts, comments, etc)
2. Data labeler site
3. Text classification service
4. Analytic dashboard




After writing this I doubt that I will finish this project at the end of the holiday.... 

But duck it right, just go on and let's see what I can do.

Let me breakdown those four services for you (and me, I need it for further reference). The following might not be too technical, the detailed architecture will be updated in the later posts.

#### 1. Data Crawler

I use Golang with *go-twitter* library to fetch filtered realtime tweets. I filtered the tweets based on the location represented by the latitude and longitude values of the location. The library is awesome and easy to use, [go check it out!](https://github.com/dghubble/go-twitter)

I still haven't taken a deep look into the [Facebook Graph API](https://developers.facebook.com/docs/graph-api/). So still nothing to say about the Facbook Feed crawler. 

#### 2. Data Labeler Site

I am going to use [React](https://reactjs.org/) for the data labeling website. But I suck at design so anyone that is reading this post (preferably designer/front-end developer) and willing to help me design the site is very welcomed!

The site will show the data that have been fetched by the crawler and visitors of the site will be asked to fill the label field for the corresponding data. There are three possible labels: **Irrelevant, #1 Voter, #2 Voter**. Pretty simple right?

#### 3. Text Classification Service

Using the labeled data from the data labeler site, (hopefully with enough data) we can make a text classifier that will classify whether the content-writer is the supporter of #1 or #2. I might be using [FastText](https://github.com/facebookresearch/fastText) for the text classification. Any recommendation is welcomed!

#### 4. Analytic Dashboard

After the text classification model is finished and ready to use, we can make a realtime analytic dashboard that uses streaming data and classify it into one of the two classes. From the classification result we can aggregate and make a graphical summary out of it. 


That's it for today, I realize that I still got a lot of work to be done. Huyu
 
See you tomorrow!