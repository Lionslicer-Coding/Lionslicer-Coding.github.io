---
layout: post
title:      "Predicting Match Outcomes in Dota 2: Part One"
date:       2021-01-18 17:11:12 -0500
permalink:  predicting_match_outcomes_in_dota_2_part_one
---


## Introduction

This is part one of a series of posts detailing my project to build a model that predicts the outcomes of DotA 2 matches. You can view the GitHub repository for this project [here](https://github.com/Lionslicer-Coding/Dota2Project).

* Part One: Obtaining Data (You are here)
* [Part Two: Scrubbing and Exploration](https://lionslicer-coding.github.io/projecting_dota_2_match_outcomes_part_two)
* Part Three: Modeling and Interpretation

For the better part of two decades, online multiplayer video games have been accruing massive player bases and forming competitive environments within them. These games span many different genres, and range in complexity from simple enough for children to master, to complex enough to require thousands of hours of playtime to develop high level skills.

One such game is Dota 2, created by Valve Software. Launched in 2012, this Multiplayer Online Battle Arena (MOBA) game has maintained a strong following all the way to the present day, where there are at least 400,000 players online at any point in time. Given the stability of the player base, it's not surprising that it also enjoys a strong competitive scene, creating myriad opportunities for individuals to generate income from the game. It has also generated an appetite for strong predictive tools that allow for more confident analysis and betting predictions.
As someone very familiar with DotA 2, and with knowledge of data science techniques, I have decided to attempt to build a model that will successfully project match outcomes. 

## Getting started

Before I can even think about models, I need to decide what data is necessary and how to obtain that data. Luckily, the DotA community offers several solutions for gathering data. Below I will describe three of these solutions, the Steam API, OpenDota API, and the Stratz API. I'll cover pros and cons of each and explain why I made the choice I did. 

### Steam API

Once upon a time, the Steam API was the only option available. As far as raw data is concerned, it is still the king for DotA 2 data. One reason for this is the moderately high request limit. The Steam API allows users with an API key to send 100,000 requests per day. This means that with proper calls you can accumulate a lot of data very quickly. The problem with this data is that it tends to be fairly raw, which is why services like OpenDota and Stratz exist in the first place. The Steam API provides very basic information about matches, while also providing access to replays. The other services parse through DotA 2 matches and their replays to provide more meaningful data output to those requesting match data, including data from throughout the match instead of just data from the beginning and end. 

The Steam API is fairly straightforward to use, and it's easy to find resources around the internet from others that have used it. The documentation from Valve itself is adequate for most needs, but not perfect. 

### OpenDota

The OpenDota API is an open source project funded in part by the very well respected OpenAI. It offers more advanced data than the Steam API in combination with a wealth of easy to understand resources for developers and hobbyists. The free access is restricted to 50,000 calls per month and 60 calls per minute, but you can get an API key that will grant you greater access for a charge of $.01 per 100 calls. This also removes your monthly call limit and raises the calls per minute limit to 1200. That effectively gives you 1.7 million calls per day! For this project I sent ~34,000 requests and paid less than $4 for the entirety of my data. 

OpenDota also provides an excellent graphical explorer tool to use for crafting your queries. Once you've input what you want to pull, the explore will return matches, also giving you the option to retrieve the json file of results, or the link to use for that request to the API in your code. I cannot describe how useful this tool is for someone still getting the hang of using APIs. The API also seems very stable. Of the 34,000 requests I sent, I got one bad response. I'm still not convinced it wasn't user error!

The final and perhaps largest benefit of the OpenDota API is the access to its community. The OpenDota discord is very active and full of people willing to help with any issues you encounter or questions you might have. I was able to acquire several nuggets of domain knowledge just by posting in the help channel and waiting a few minutes, and most of that knowledge didn't show up anywhere else I looked. It's worth noting that some of this knowledge came directly from the user Stratz_Ken, who is also the point of contact for the Stratz API. 

The OpenDota API has many many things it does well, but there are also some quirks that I found somewhat frustrating. The biggest headache was in using the publicMatches endpoint of the API. This endpoint returns a selection of 100 matches selected from balanced game modes over the previous 72 hours. On paper, this sounds like the most efficient way to gather recent matches with minimal calls, but in practice I found difficulties. The endpoint refreshes sporadically, so if you are sending thousands of requests on short delays as I was, you end up being flooded by duplicates. In my original pull, I sent 10,000 requests, expecting to get roughly 600,000 unique matches based on some smaller test pulls I had done. Instead I got just over 32,000 unique matches. If you have time to put a significant delay between your requests, you should be able to increase your yield, but I didn't see a difference by adding a .7 second delay between requests. 

### Stratz API

The Stratz API is another community API that offers advanced statistics, including lanes and roles for different players, which it gathers from parsing replays. The API is straightforward to use and Stratz_Ken is very responsive to help requests. 

I did not spend a ton of time researching the efficacy of the API, as I was interested in only pregame information and the request limits for Stratz API are the most strict of the three options. With an API key you are restricted to only 500 requests per hour. The options and available data are impressive, I just needed to be able to pull data more quickly. 

## The Verdict

Ultimately I decided to use the OpenDota API for my data gathering. It offered the most generous pull limits while also giving me the best options for support. It also offered the most flexible options for scaling my project as well as expanding the scope later down the road. 

In the next post, I will discuss my process for scrubbing and exploring the data obtained from the OpenDota API. 
