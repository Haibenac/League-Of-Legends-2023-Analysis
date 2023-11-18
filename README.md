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