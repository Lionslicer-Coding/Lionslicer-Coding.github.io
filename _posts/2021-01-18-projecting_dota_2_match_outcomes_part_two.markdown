---
layout: post
title:      "Projecting Dota 2 Match Outcomes: Part Two"
date:       2021-01-19 01:32:45 +0000
permalink:  projecting_dota_2_match_outcomes_part_two
---


## Introduction
This is part two of a series of posts detailing my project to build a model that predicts the outcomes of DotA 2 matches. You can view the GitHub repository for this project [here](https://github.com/Lionslicer-Coding/Dota2Project).

* [Part One: Obtaining Data](https://lionslicer-coding.github.io/predicting_match_outcomes_in_dota_2_part_one)
* Part Two: Scrubbing and Exploration (You are here)
* Part Three: Modeling and Interpretation

Now that we've obtained our data using the OpenDota API, it's time for us to work it into a format we can use for modeling and do some exploration as we ask questions about our data. In our OSEMN process, this will cover Scrubbing and Exploration. 

### Scrubbing
The data we obtained contains everything we need to make a minimum viable product, but the formatting is inconvenient for exploration and modeling. Before moving on, the data will need to be reformatted. The features in our data are as follows:

* match_id 
* match_seq_num 
* radiant_win 
* start_time 
* duration 
* avg_mmr 
* num_mmr 
* lobby_type 
* game_mode 
* avg_rank_tier 
* num_rank_tier 
* cluster
* radiant_team 
* dire_team 

Many of these features will be removed before we model but we know that we will want the avg_mmr feature. This feature gives us an indicator of the skill level of players in a match. Anyone that has played a meaningful amount of Dota 2 understands that heroes have different win rates at different skill levels. IO, for example, has a 48% win rate in the lowest skill bracket, but a 52% win rate in the highest skill bracket. Pudge, meanwhile, has a 52% win rate in lowest skill bracket but craters to 46% in the highest skill bracket! It's very important that we consider skill in our predictions, and to choose a model that can pick up on these interactions.

The other features we are keeping are the teams, though we will need to reformat them. From the API, the teams are stored as a string containing a list of numbers that correlate to each hero. The way we address this is by splitting each team into a list, and then using those lists to one-hot encode each hero, but with consideration for which team they are on. This effectively creates a sparse table containing columns for each hero on dire side and additional columns for each hero on radiant. The hope is that formatting this way will allow our models to pick up on interactions such as counter picks (picking Puck as a counter to Pangolier, or Earthshaker to counter a Phantom Lancer). An alternative that was considered was placing all teams in the same colummns, which would effectively double our observations and cut our features in half. We chose not to go this route because it would not allow for interactions of counter picks.

The function for this appears below:

```
def add_hero_cols(df, column_name) :
    """Builds and appends a sparse data table at the end of a dataframe of Dota 2 Matches.
    
    Keyword Arguments:
    df -- Pandas Dataframe containing match data
    column_name -- the column of the team you are wishing to append
    
    Libraries needed: Pandas, json, requests, time
    """
    heroes = requests.get('https://api.opendota.com/api/constants/heroes')
    heroes = heroes.json()
    
    temp_df = df[column_name].str.split(pat = ',')
    hero_dict = {}
    
    for hero in heroes :
        heroes['{}'.format(hero)]['localized_name'].replace(' ', '_')
        hero_dict['{}_{}'.format( heroes['{}'.format(hero)]['localized_name'], column_name)] = []
    
    for team in temp_df :
        for hero in heroes :
            if hero in team :
                hero_dict['{}_{}'.format(heroes['{}'.format(hero)]['localized_name'], column_name)].append(1)
            else :
                hero_dict['{}_{}'.format(heroes['{}'.format(hero)]['localized_name'], column_name)].append(0)
    
    for hero in hero_dict :
        df[hero] = hero_dict[hero]
        
    df.drop(['{}'.format(column_name)], axis=1, inplace=True)
    
    return df
		```
The last thing to note about our final data set is that it's slightly unbalanced class-wise. We have a data set that features roughly 60% Radiant wins, and 40% Dire wins. This isn't a terrible imbalance and don't believe it will show any significant impact on our models.

### Exploration

Generally before modeling we would want to answer several questions about our data set and attempt to find meaningful answers. For this project, we really only explored the representation of each hero in our data set. This section will be expanded in the future once a more thorough exploration has been completed. For now, it's worth noting that we had one hero clearly represented the most, beating out the second most represented by more than 10% and appearing in a little more than one in every four games; Pudge!

In part three, we will explore our models and how they performed, and also take a look at feature importance to get an idea of what specific factors an individual or organization might need to consider most before making decisions on each match.

