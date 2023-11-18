# League-Of-Legends-2023-Analysis
This is Project 3 for DSC 80. It was authored by Andrew Peng.

All the data was sourced from a public dataset created by Oracle's Elixer found here: https://oracleselixir.com/tools/downloads.

---

# An Analysis of League of Legends and the Importance of Lanes and Objectives

**Name(s)**: Andrew Peng

**Website Link**: https://haibenac.github.io/League-Of-Legends-2023-Analysis/
---
### Introduction
This dataset holds a multitude of information regarding the 2023 professional League of Legends scene, holding much data from professional matches and how each match developed in gold differential, minion kills, victories, teams, and players. Each row also has access to a variety of statistics for each individual player, all ready for analysis.

This dataset initially came with 129,048 rows and 93 columns.

Some of the important columns were

-League: Determined with region the match was played in.

-Side: Gave information on what side of the map the team played on.

-Position: Informed whether or no the statistic belonged to a certain role or the team as a whole.

-Champion: The character a given player played during that match.

-bans 1-5: All bans that a team made through one match.

-game length: The length of the game in seconds.

-kills: The number of kills a player gets in one match.

-deaths: The number of deaths a player gets in one match.

-assists: The number of assists a player gets in one match.

-cspm: The number of minion kills per minute a player reached in one match.


### Cleaning and EDA

I begin by cleaning the data. I first decide which columns should be boolean values. I did this by sifting through the data and finding columns that could be determined by trues and falses. 

Afterward, I removed all columns that I knew I would not be using as it simply cluttered the data and made it harder to read.

The next step was to work only with the big leagues as listed by the League of Legends Wikipedia. This included Brazil, Europe, North America, Japan, Korea, Latin America, China, Vietnam, and the two major international tournaments: The Mid-Season Invitational and Worlds.

Finally, to deal with a small error of different data types, I converted a few columns giving me trouble to strings to ensure that they behaved properly.

| gameid           | league   | split   | playoffs   | date           |   game |   participantid | side   | position   | playername   | teamname        | champion   | ban1   | ban2   | ban3   | ban4    | ban5   |   gamelength | result   |   kills |   deaths |   assists |   teamkills |   teamdeaths | firstbloodkill   |   firstdragon |   dragons |   opp_dragons |   monsterkills |   monsterkillsownjungle |   monsterkillsenemyjungle |    cspm |
|:-----------------|:---------|:--------|:-----------|:---------------|-------:|----------------:|:-------|:-----------|:-------------|:----------------|:-----------|:-------|:-------|:-------|:--------|:-------|-------------:|:---------|--------:|---------:|----------:|------------:|-------------:|:-----------------|--------------:|----------:|--------------:|---------------:|------------------------:|--------------------------:|--------:|
| 9691-9691_game_1 | LPL      | Spring  | False      | 1/14/2023 7:23 |      1 |               1 | Blue   | top        | Xiaolaohu    | FunPlus Phoenix | K'Sante    | Lucian | Varus  | Syndra | LeBlanc | Viktor |         1836 | False    |       1 |        4 |         1 |           6 |           16 | False            |           nan |       nan |           nan |              0 |                       0 |                         0 |  7.9739 |
| 9691-9691_game_1 | LPL      | Spring  | False      | 1/14/2023 7:23 |      1 |               2 | Blue   | jng        | haoye        | FunPlus Phoenix | Vi         | Lucian | Varus  | Syndra | LeBlanc | Viktor |         1836 | False    |       2 |        3 |         4 |           6 |           16 | False            |           nan |       nan |           nan |            155 |                     110 |                         6 |  5.5556 |
| 9691-9691_game_1 | LPL      | Spring  | False      | 1/14/2023 7:23 |      1 |               3 | Blue   | mid        | Care         | FunPlus Phoenix | Akali      | Lucian | Varus  | Syndra | LeBlanc | Viktor |         1836 | False    |       1 |        2 |         4 |           6 |           16 | False            |           nan |       nan |           nan |              0 |                       0 |                         0 |  7.9412 |
| 9691-9691_game_1 | LPL      | Spring  | False      | 1/14/2023 7:23 |      1 |               4 | Blue   | bot        | Lwx          | FunPlus Phoenix | Caitlyn    | Lucian | Varus  | Syndra | LeBlanc | Viktor |         1836 | False    |       1 |        2 |         3 |           6 |           16 | False            |           nan |       nan |           nan |             25 |                      21 |                         4 | 11.0131 |
| 9691-9691_game_1 | LPL      | Spring  | False      | 1/14/2023 7:23 |      1 |               5 | Blue   | sup        | Lele         | FunPlus Phoenix | Lux        | Lucian | Varus  | Syndra | LeBlanc | Viktor |         1836 | False    |       1 |        5 |         3 |           6 |           16 | False            |           nan |       nan |           nan |              0 |                       0 |                         0 |  1.3072 |


One of the most important stages of games is the draft where teams can pick and ban champions. While trivial at first, it quickly becomes a complex chess match. Certain champion bans lock teams into playing certain styles and push players out of their comfort zones. Even if a team is "less mechanically skilled," they can still gain an edge in a match by simply banning and picking characters away. 

However, there are certain champions that give a clear edge over others in terms of being selected. Thus, they are normally permanently banned.

The following code creates a new dataframe that concatenates all the bans together by team (as to not quintuple count all banned values) before counting them all together and plotting it in a univariate bar chart.

<iframe src="assets/Chart1.html" width=800 height=600 frameBorder=0></iframe>

These are the twenty most banned champions during the 2023 League of Legends season. From this, we can clearly see that the most banned champions are Vi, Maokai, Elise, Neeko, Rakan, and few others. A large majority of these are engage champions: Characters that specialize in creating opportunities for team fights with dashes and crowd control.

Now, I shift my focus to see what kinds of champions are selected after many of the most powerful engage champions are banned away.

Here, I focus on players rather than teams to see exactly what champion is picked. I use the 'champion' column and filter it to show the first 20 most picked champions before plotting it in a bar chart.

<iframe src="assets/Chart2.html" width=800 height=600 frameBorder=0></iframe>

From this graph, we can see characters that are known to be stronger in solo duels or champions that are good at engaging and initiating team fights, making them net positives for the teams that select them.

The most interesting thing is the heavy focus on solo-kill champions--characters that are stronger in one versus one engagements. This could be likely due to the size of the map of Summoner's Rift, making solo characters much more effective in creating a small advantage and bullying their own lanes to begin stacking small edges on top of each other. 

As a very poor League of Legends player myself, I wanted to see the true power of holding and controlling neutral objectives in League of Legends. In this case, the most common neutral map objective are dragons. Killing four of them by one team grants a soul which results in an absurd boost in team strength. In theory, this should make controlling the dragon pit (and in turn killing them before the enemy) very important to winning the game.

As both teams can kill dragons, I decided to use the difference in dragon kills to show the potential difference in win rate that even a singular dragon can make.

<iframe src="assets/Chart3.html" width=800 height=600 frameBorder=0></iframe>

The importance of dragons in this game as objectives is painstakingly obvious as, the more dragons a team has in comparison to another, the higher the chance of victory. League of Legends is not only a mico-skilled game, but also a macro-based game where map control of objectives is very important, as seen by this chart.

Surprisingly, the highest jump in win rate came from having a one dragon edge over your opponent, resulting in a 19% increase in win rate, much larger than any other dragon increment.

The early game normally decides the rest of the game as the team that can get ahead usually snowballs an advantage and becomes an unstoppable force, picking up kills and bounties, controlling objectives, and gaining map control. However, as the game progresses, more and more players reach full builds and begin focusing less on their individual lanes. Instead, they begin to focus more on the map, controlling territory, and team fights. 

In the next graph, I decided to test this hypothesis to see if there was a negative correlation between the length of a game and creep score per minute--the most impactful way of making gold.

<iframe src="assets/Chart4.html" width=800 height=600 frameBorder=0></iframe>

As the game drags on, the importance of maintaining a high creep score becomes less and less important as the objectives on the map becomes increasingly more important to the team and securing victory. Players begin to stop focusing as much on their lanes and instead begin to roam and win team fights. Thus, as expected, there is a clear negative correlation in this bivariate analysis.

Normally, people talk about a "gap" between regions, saying that the LPL (China's League) and the LCK (Korea's league) are light years ahead of their competition. Thus, I created a pivot table that showed the relationship of kills by each league based on position.

| position   |    CBLOL |      LCK |      LCS |      LEC |      LJL |      LLA |      LPL |      PCS |      VCS |
|:-----------|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|
| bot        | 4.58471  | 3.75565  | 4.13447  | 4.32578  | 4.28488  | 4.52604  | 4.13311  | 4.25427  | 4.72492  |
| jng        | 2.18802  | 2.01643  | 2.21402  | 2.51568  | 2.0407   | 2.53906  | 2.40066  | 2.29522  | 2.46926  |
| mid        | 3.21281  | 2.70739  | 3.34848  | 3.57666  | 3.4031   | 3.55208  | 3.3      | 3.35495  | 3.18932  |
| sup        | 0.766529 | 0.613963 | 0.664773 | 0.764808 | 0.757752 | 0.697917 | 0.701987 | 0.648464 | 0.796117 |
| top        | 2.91116  | 2.06057  | 2.3428   | 2.72125  | 2.28682  | 2.26823  | 2.26954  | 2.40444  | 2.47896  |

Interestingly enough, the smaller regions (CBLOL, LLA, VCS) have a much higher average number of kills per position while the best regions (LCK, LPL) have lower average kills. This could imply that stronger regions tend to take fewer fights and instead probe enemies while waiting for an advantage instead of diving and engaging in coin-flip fights.

Interestingly enough, supports in the "weaker regions" tended to have higher kills on average, perhaps indicating lost gold that could've gone to the ADC.

---
### Assessment of Missingness

In the dataset under analysis, there are no columns categorized as NMAR, as the data originates from structured and regulated esports matches overseen by RIOT Games. Unlike survey data, where respondents decide whether to answer specific questions, esports match data is inherently complete in terms of player participation.

While there is missing data, it is MAR (not NMAR). Instances of missing values can be attributed two a few main reasons.

One scenario involves the absence of numerous advanced statistics, such as turret plates, opp_turretplates, and inhibitors, predominantly observed in matches associated with the LPL league. This pattern suggests that the non-availability of certain metrics is not random but rather associated with specific leagues or tournaments.

The second involves team versus individual stats. For example, it it a team stat to show the total number of objectives taken (towers, dragons, barons). Thus, the individual statistic for those columns is listed as NaN.

An example of a column that contained many missing values was the column "monsterkillsownjungle" which was a statistic that was only tracked in LPL (China) games or when LPL teams faced each other in international tournaments. 

Thus, I conducted a 10,000 permutation test that involved using the distribution of "monsterkillsownjungle" dependant on the league the data was sourced from. 

The Null Hypothesis: "Monsterkillsownjungle" is MCAR and is not associated with the "region" column.

The Alternative Hypothesis: "Monsterkillsownjungle" is MAR and is very much so associated with the "region" column.

| side   |   junglekill_missing = False |   junglekill_missing = True |
|:-------|-----------------------------:|----------------------------:|
| Blue   |                          0.5 |                         0.5 |
| Red    |                          0.5 |                         0.5 |

<iframe src="assets/Chart5.html" width=800 height=600 frameBorder=0></iframe>

We observe an extremely significant p-value of 0.0, meaning that we will reject the null. Monster kills in a team's own jungle is MAR when comparing it to the region column.

However, "monsterkillsownjungle" is not dependent on all columns. As an example, I tested it against the team's side to prove that it was highly improbable that "monsterkillsownjungle" was associated with team side. To test this, I once again did another 10,000 permutation test to compare the TVDs of the observed TVD along with the simulated TVDs. 


The Null Hypothesis: "Monsterkillsownjungle" is MCAR in relation to the column "team" and is not associated with it.
The Alternative hypothesis:  

The Alternative Hypothesis: "Monsterkillsownjungle" is MAR and is associated with the "team" column.

<iframe src="assets/Chart6.html" width=800 height=600 frameBorder=0></iframe>

With a significantly large p-value of 1.0, we fail to reject the null. Monster kills in a team's own jungle is MCAR when comparing it to the side (blue or red) column.

---
### Hypothesis Testing

For my hypothesis, I wanted to see Which role “carried” (does the best) in their team more often: ADCs (Bot lanes) or Mid laners? To determine this, I decided that success and "carrying" would be determined by whichever role had the highest KDA ((kills + assists) / deaths). The higher the number, the more impactful they were, and the higher the share of teamfights that specific role impacted. To do this, I first filtered my dataframe to create a new row (kda) where every player that had the role 'mid' or 'bot' had a new 'kda' statistic. Then, I pushed the mean of the KDAs of both roles and took a .diff() using 'Mid' - 'ADC.' Finally, using my observation, I compared it to a 10,000 permutation test of randomized Mid and ADC KDAs and compared the observed value to the difference of the means of the simulated statistics. 

From an initial point of view, many people (myself included) believe that ADC players (bottom lane) tend to carry the most. They, for one, must control the dragon pit with absurd amounts of damage. In return, they stay relatively weak in terms of survivability. In pure 5v5 teamfights, the team that protects their ADC for the longest usually wins due to the sheer damage output that an ADC player is capable of outputting. It is why they always run with a support player for much of the early game.

The Null Hypothesis: Neither role does better than one another. Instead, they are near equal in terms of damage output and have similar KDAs.

The Alternative Hypothesis: ADC players play a much more important role and tend to get much more kills and assists than mid laners. Thus, they have a higher KDA than their counterpart.

|       | gameid                | league   | split   | playoffs   | date             |   game |   participantid | side   | position   | playername     | teamname                      | champion     | ban1         | ban2         | ban3         | ban4         | ban5         |   gamelength | result   |   kills |   deaths |   assists |   teamkills |   teamdeaths | firstbloodkill   |   firstdragon |   dragons |   opp_dragons |   monsterkills |   monsterkillsownjungle |   monsterkillsenemyjungle |    cspm |       kda |
|------:|:----------------------|:---------|:--------|:-----------|:-----------------|-------:|----------------:|:-------|:-----------|:---------------|:------------------------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|-------------:|:---------|--------:|---------:|----------:|------------:|-------------:|:-----------------|--------------:|----------:|--------------:|---------------:|------------------------:|--------------------------:|--------:|----------:|
|     2 | 9691-9691_game_1      | LPL      | Spring  | False      | 1/14/2023 7:23   |      1 |               3 | Blue   | mid        | Care           | FunPlus Phoenix               | Akali        | Lucian       | Varus        | Syndra       | LeBlanc      | Viktor       |         1836 | False    |       1 |        2 |         4 |           6 |           16 | False            |           nan |       nan |           nan |              0 |                       0 |                         0 |  7.9412 |  2.5      |
|     3 | 9691-9691_game_1      | LPL      | Spring  | False      | 1/14/2023 7:23   |      1 |               4 | Blue   | bot        | Lwx            | FunPlus Phoenix               | Caitlyn      | Lucian       | Varus        | Syndra       | LeBlanc      | Viktor       |         1836 | False    |       1 |        2 |         3 |           6 |           16 | False            |           nan |       nan |           nan |             25 |                      21 |                         4 | 11.0131 |  2        |
|     7 | 9691-9691_game_1      | LPL      | Spring  | False      | 1/14/2023 7:23   |      1 |               8 | Red    | mid        | Shanks         | Team WE                       | Azir         | Zeri         | Ryze         | Yuumi        | Ahri         | Fiora        |         1836 | True     |       8 |        1 |         4 |          16 |            6 | True             |           nan |       nan |           nan |             12 |                       4 |                         8 |  8.8562 | 12        |
|     8 | 9691-9691_game_1      | LPL      | Spring  | False      | 1/14/2023 7:23   |      1 |               9 | Red    | bot        | Hope           | Team WE                       | Kalista      | Zeri         | Ryze         | Yuumi        | Ahri         | Fiora        |         1836 | True     |       7 |        3 |         5 |          16 |            6 | False            |           nan |       nan |           nan |             24 |                      16 |                         4 | 10.1961 |  4        |
|    14 | 9691-9691_game_2      | LPL      | Spring  | False      | 1/14/2023 8:15   |      2 |               3 | Blue   | mid        | Shanks         | Team WE                       | Sylas        | Galio        | Fiora        | Ryze         | Syndra       | K'Sante      |         1779 | False    |       2 |        4 |         1 |           4 |           17 | False            |           nan |       nan |           nan |              0 |                       0 |                         0 |  8.1619 |  0.75     |

With a significance level of 0.05, the resulting p-value of 0.0 is far from it. Thus, we can reject the null hypothesis.

This is the difference between mid KDA subtracted by bot KDA. Because the value returned from the observed statistic is very small, it is safe to assume that, in our observed stat, the ADC does better than the mid player, boasting a .43 higher KDA on average.

Based on the permutated data, this value is significantly significant because the p-value is incredibly low with no simulated datasets being more extreme than the observed test statistic, showing that we can safely reject the null hypothesis. ADC players do carry better than mid laners. In this case, carry is defined as having a higher KDA.

