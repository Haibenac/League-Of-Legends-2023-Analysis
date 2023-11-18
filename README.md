# League-Of-Legends-2023-Analysis
This is Project 3 for DSC 80. It was authored by Andrew Peng.

All the data was sourced from a public dataset created by Oracle's Elixer found here: https://oracleselixir.com/tools/downloads.

---

# An Analysis of League of Legends and the Importance of Lanes and Objectives

**Name(s)**: Andrew Peng

**Website Link**: https://haibenac.github.io/League-Of-Legends-2023-Analysis/

### Cleaning and EDA

I begin by cleaning the data. I first decide which columns should be boolean values. I did this by sifting through the data and finding columns that could be determined by trues and falses. 

Afterwards, I removed all columns that I knew I would not be using as it simply cluttered the data and made it harder to read.

The next step was to work only with the big leagues as listed by the League of Legends Wikipedia. This included Brazil, Europe, North America, Japan, Korea, Latin America, China, Vietnam, and the two major international tournaments: The Mid-Season Invitational and Worlds.

Finally, to deal with a small error of different data types, I converted a few columns giving me trouble to strings to ensure that they behaved properly.


<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gameid</th>
      <th>league</th>
      <th>split</th>
      <th>playoffs</th>
      <th>date</th>
      <th>game</th>
      <th>participantid</th>
      <th>side</th>
      <th>position</th>
      <th>playername</th>
      <th>...</th>
      <th>teamkills</th>
      <th>teamdeaths</th>
      <th>firstbloodkill</th>
      <th>firstdragon</th>
      <th>dragons</th>
      <th>opp_dragons</th>
      <th>monsterkills</th>
      <th>monsterkillsownjungle</th>
      <th>monsterkillsenemyjungle</th>
      <th>cspm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9691-9691_game_1</td>
      <td>LPL</td>
      <td>Spring</td>
      <td>False</td>
      <td>1/14/2023 7:23</td>
      <td>1</td>
      <td>1</td>
      <td>Blue</td>
      <td>top</td>
      <td>Xiaolaohu</td>
      <td>...</td>
      <td>6</td>
      <td>16</td>
      <td>False</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>7.9739</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9691-9691_game_1</td>
      <td>LPL</td>
      <td>Spring</td>
      <td>False</td>
      <td>1/14/2023 7:23</td>
      <td>1</td>
      <td>2</td>
      <td>Blue</td>
      <td>jng</td>
      <td>haoye</td>
      <td>...</td>
      <td>6</td>
      <td>16</td>
      <td>False</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>155</td>
      <td>110.0</td>
      <td>6.0</td>
      <td>5.5556</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9691-9691_game_1</td>
      <td>LPL</td>
      <td>Spring</td>
      <td>False</td>
      <td>1/14/2023 7:23</td>
      <td>1</td>
      <td>3</td>
      <td>Blue</td>
      <td>mid</td>
      <td>Care</td>
      <td>...</td>
      <td>6</td>
      <td>16</td>
      <td>False</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>7.9412</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9691-9691_game_1</td>
      <td>LPL</td>
      <td>Spring</td>
      <td>False</td>
      <td>1/14/2023 7:23</td>
      <td>1</td>
      <td>4</td>
      <td>Blue</td>
      <td>bot</td>
      <td>Lwx</td>
      <td>...</td>
      <td>6</td>
      <td>16</td>
      <td>False</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>25</td>
      <td>21.0</td>
      <td>4.0</td>
      <td>11.0131</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9691-9691_game_1</td>
      <td>LPL</td>
      <td>Spring</td>
      <td>False</td>
      <td>1/14/2023 7:23</td>
      <td>1</td>
      <td>5</td>
      <td>Blue</td>
      <td>sup</td>
      <td>Lele</td>
      <td>...</td>
      <td>6</td>
      <td>16</td>
      <td>False</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.3072</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 32 columns</p>
</div>


One of the most important stages of games is the draft where teams can pick and ban champions. While trivial at first, it quickly becomes a complex chess match. Certain champion bans lock teams into playing certain styles and push players out of their comfort zones. Even if a team is "less mechanically skilled," they can still gain an edge in a match by simply banning and picking characters away. 

However, there are certain champions that give a clear edge over others in terms of being selected. Thus, they are normally permanently banned.

The following code creates a new dataframe that concatenates all the bans together by team (as to not quintuple count all banned values) before counting them all together and plotting it in a univariate bar chart.

<bound method BaseFigure.write_html of Figure({
    'data': [{'alignmentgroup': 'True',
              'hovertemplate': 'Champion=%{x}<br>Number of Bans=%{y}<extra></extra>',
              'legendgroup': '',
              'marker': {'color': '#636efa', 'pattern': {'shape': ''}},
              'name': '',
              'offsetgroup': '',
              'orientation': 'v',
              'showlegend': False,
              'textposition': 'auto',
              'type': 'bar',
              'x': array(['Vi', 'Maokai', 'LeBlanc', 'Jayce', 'Jax', 'Sejuani', 'Neeko', 'Annie',
                          'Ashe', 'Tristana', 'Renekton', 'Lucian', 'Elise', 'Rakan', 'Varus',
                          'Caitlyn', 'Xayah', 'Zeri', 'Poppy', "K'Sante"], dtype=object),
              'xaxis': 'x',
              'y': array([1267, 1248, 1165, 1123, 1057, 1043, 911, 900, 888, 860, 827, 786, 773,
                          772, 725, 682, 682, 673, 635, 626], dtype=object),
              'yaxis': 'y'}],
    'layout': {'barmode': 'relative',
               'legend': {'tracegroupgap': 0},
               'template': '...',
               'title': {'text': 'Top 20 Most Banned Champions'},
               'xaxis': {'anchor': 'y', 'domain': [0.0, 1.0], 'tickangle': 45, 'title': {'text': 'Champion'}},
               'yaxis': {'anchor': 'x', 'domain': [0.0, 1.0], 'title': {'text': 'Number of Bans'}}}
})>
