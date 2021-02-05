---
layout: post
title: Discord Total Gameplay Duration
published: false
---

```
import pandas as pd
snippet =
df = pd.read_json(snippet)
games = pd.read_json('https://gist.githubusercontent.com/Cynosphere/c1e77f77f0e565ddaac2822977961e76/raw/52d1f2d31be7168a0486a3a355e06a2d751bdc44/gameslist.json')
games = games.rename(columns={"id": "application_id"})
games_short = games[['application_id','name','description']]
merge_df = pd.merge(df, games_short, how='left', on=['application_id'])
merge_df = merge_df.sort_values(['total_duration'],ascending = (False)).reset_index(drop=True)
merge_df['duration_in_hours'] = merge_df['total_duration']/3600
final_df = merge_df[['name','description','duration_in_hours','last_played_at']]
final_df['short_description'] = final_df['description'].str.slice(0,100) + '...'
final_df['duration_in_hours'] = final_df['duration_in_hours'].round(decimals=1)
final_df = final_df.drop(columns=['description'])
df = final_df[['name', 'short_description', 'duration_in_hours', 'last_played_at']]
final_df.to_csv('discord_duration_data.csv',index=False)
print(final_df.to_markdown())

```

|    | name                                         |   duration_in_hours | last_played_at                   | short_description                                                                                       |
|---:|:---------------------------------------------|--------------------:|:---------------------------------|:--------------------------------------------------------------------------------------------------------|
|  0 | Overwatch                                    |              1290   | 2020-11-21 05:50:47.351000+00:00 | A stylish sci-fi, team-based, first-person shooter from Blizzard in which players can choose from a ... |
|  1 | Slay the Spire                               |               233.4 | 2020-11-19 20:31:26.977000+00:00 | nan                                                                                                     |
|  2 | Hades                                        |                67.2 | 2020-11-21 02:26:20.200000+00:00 | nan                                                                                                     |
|  3 | Dota 2                                       |                22.4 | 2019-05-27 03:00:15.826000+00:00 | The official free-to-play sequel to the Warcraft III custom scenario that originally popularized the... |
|  4 | The Witcher 3: Wild Hunt                     |                18   | 2020-04-12 04:40:24.415000+00:00 | CD Projekt RED's third Witcher combines the series' non-linear storytelling with a sprawling open wo... |
|  5 | Hearthstone                                  |                14.5 | 2020-06-12 06:05:53.873000+00:00 | A Free-to-Play collectible card game by Blizzard Entertainment set in the Warcraft universe....         |
|  6 | Ori and the Blind Forest: Definitive Edition |                12.5 | 2019-07-21 22:01:32.687000+00:00 | nan                                                                                                     |
|  7 | Slime Rancher                                |                12.4 | 2018-12-09 06:38:09.141000+00:00 | A vividly coloured and light-hearted game about building a ranch of slime creatures on another plane... |
|  8 | Path of Exile                                |                12.1 | 2019-01-03 21:24:11.839000+00:00 | Path of Exile is a free-to-play PC online action Role-Playing Game set in a dark fantasy world....      |
|  9 | Overcooked! 2                                |                 9.5 | 2020-03-27 23:51:29.808000+00:00 | Overcooked! returns in this multiplatform sequel now with online play....                               |
| 10 | Stardew Valley                               |                 8.2 | 2020-03-27 23:01:33.459000+00:00 | An open-ended country-life RPG in which players can manage their own farm and interact with the surr... |
| 11 | The Elder Scrolls V: Skyrim                  |                 6   | 2018-10-16 03:27:08.041000+00:00 | The fifth installment in Bethesda's Elder Scrolls franchise is set in the eponymous province of Skyr... |
| 12 | nan                                          |                 3.5 | 2019-01-03 22:09:29.043000+00:00 | nan                                                                                                     |
| 13 | The Jackbox Party Pack 3                     |                 2.3 | 2020-11-05 01:19:35.899000+00:00 | Brainstorm t-shirts, deceive your friends, and survive a night with a deadly trivia host in the thir... |
| 14 | Ashen                                        |                 1.7 | 2019-01-07 03:42:48.916000+00:00 | nan                                                                                                     |
| 15 | Don't Starve Together                        |                 1.5 | 2018-12-18 03:57:29.214000+00:00 | Don't Starve Together is the standalone multiplayer expansion of the uncompromising survival game Do... |
| 16 | Terraria                                     |                 1.4 | 2019-08-18 23:07:22.854000+00:00 | The first major 2D entry into the world of "open world" sandbox action-adventure games, Terraria is ... |
| 17 | Black Desert Online                          |                 1.4 | 2019-01-27 04:32:42.751000+00:00 | A sandbox action MMORPG....                                                                             |
| 18 | BioShock™ Remastered                         |                 0.6 | 2018-10-14 01:10:37.372000+00:00 | nan                                                                                                     |
| 19 | BioShock 2                                   |                 0.2 | 2018-11-30 03:39:18.544000+00:00 | Ten years after the events of the first game, Subject Delta is awoken and must unravel the mystery b... |
