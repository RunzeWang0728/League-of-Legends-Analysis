

# Is RNG Xiaohu the "Tiger King of the Spring" in LPL? &#x1F914;
![cat GIF](https://media.tenor.com/Jh6tYjm6dOAAAAAC/xiaohu-rng-lpl.gif)


**Name(s)**: Runze Wang, Xuecheng Xu


# Introduction
## Background Information
![alt text](https://i.imgur.com/hZnnBki.jpg)

Xiaohu is one of the most prominent League of Legends Player around the world who work for the RNG, Royal Never Give up, for many years in LPL League. His ID, Xiaohu, stands for "Little Tiger" in English. He has won the intercontinental championship three times, and won it in different positions, mid and top. In the LPL, he has always been one of the best mid laners and has brought us wonderful games. However, on the other hand, many audiences call him the King of the Spring in LPL, which means that Xiaohu is the one who can carry the team only in the spring split, but when it comes to the summer split and the World Championship, his performance isn't as good as he used to be in Spring Split.

## Main Question
In this League of Legends Analysis, we would testify this claim:

***Is RNG Xiaohu the "Tiger King of the Spring" in LPL?*** 

Is this just a saying or it is a fact supported by data? &#x1F914;
## Approach


### **How to measure the performance of Xiaohu and other players?**

We measure a player's performance in the game through DPG, which is the ratio of the damage done per minute of the game to the gold gained per minute. On the one hand, as a mid laner, most of the time, he undertakes the task of causing damage in the team. The team will provide resources to the middle and bottom lanes so that they can buy better equipment in a shorter period of time to surpass their opponents. Calculating DPG is to understand the ability of the player to convert the resources given by the team into damage to the opponent in the game.

DPG(dpm_per_gpm) = dpm/earned gpm

League of Legends is a 5V5 team game, sometimes winning or losing the game does not depend on the performance of a certain player, so even if the raw data includes the data of whether the game was won, we did not include it as a measure of whether a player won performance variables; in addition, the KDA statistic for mid and bottom lane players seems to be a very convincing statistic to represent the player's performance in the game. However, we believe that KDA can only reflect the performance of the player's kills and assists. In the game, some champions can get assists or kills more easily through the mechanism of their skills. Therefore, when choosing different champions, the KDA data is not a good indicator of the player's performance.

The data we use is the csv file for match data in 2022 from [OE public Match Data](https://drive.google.com/drive/u/1/folders/1gLSw0RLjBbtaNy0dgnGQDAZOHIgCe-HH) with 149232 rows × 123 columns initially. After cleaning the data, the dataframe has 47 rows and 5 columns **(split, side, champion, dpm_per_gpm_avg,	xiaohu_dpm_per_gpm_avg)**
1. **split** : The time period of the collected data . The split contains Spring split and Summer split, where we need to use performance in Summer split to compare with spring split.
2. **side** : The side of the collected data. The side contains Red side and Blue side, where the same player could perform differently on different side, even if it is the same champion.
3. **champion** : The champions Xiaohu and other players use.
4. **dpm_per_gpm_avg** : The average damage per gold for other mid-lane players in LPL. This data is used to compared with damage per gold of Xiaohu for hypothesis test.
5. **xiaohu_dpm_per_gpm_avg** : The average damage per gold for Xiaohu in LPL.

In order to better understand Xiaohu's performance, we need to compare him horizontally with other players in the same position. Therefore, we filter out the game data of all mid lane positions.

# Cleaning and EDA

Firstly, after we load the raw data from csv file as dataframe, we firstly extract the data for LPL league by only looking for players in "LPL" in "League" column.


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gameid</th>
      <th>datacompleteness</th>
      <th>url</th>
      <th>league</th>
      <th>year</th>
      <th>split</th>
      <th>playoffs</th>
      <th>date</th>
      <th>game</th>
      <th>patch</th>
      <th>participantid</th>
      <th>side</th>
      <th>position</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8401-8401_game_1</td>
      <td>partial</td>
      <td>https://lpl.qq.com/es/stats.shtml?bmid=8401</td>
      <td>LPL</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 09:24:26</td>
      <td>1</td>
      <td>12.01</td>
      <td>1</td>
      <td>Blue</td>
      <td>top</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8401-8401_game_1</td>
      <td>partial</td>
      <td>https://lpl.qq.com/es/stats.shtml?bmid=8401</td>
      <td>LPL</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 09:24:26</td>
      <td>1</td>
      <td>12.01</td>
      <td>2</td>
      <td>Blue</td>
      <td>jng</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8401-8401_game_1</td>
      <td>partial</td>
      <td>https://lpl.qq.com/es/stats.shtml?bmid=8401</td>
      <td>LPL</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 09:24:26</td>
      <td>1</td>
      <td>12.01</td>
      <td>3</td>
      <td>Blue</td>
      <td>mid</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8401-8401_game_1</td>
      <td>partial</td>
      <td>https://lpl.qq.com/es/stats.shtml?bmid=8401</td>
      <td>LPL</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 09:24:26</td>
      <td>1</td>
      <td>12.01</td>
      <td>4</td>
      <td>Blue</td>
      <td>bot</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8401-8401_game_1</td>
      <td>partial</td>
      <td>https://lpl.qq.com/es/stats.shtml?bmid=8401</td>
      <td>LPL</td>
      <td>2022</td>
      <td>Spring</td>
      <td>0</td>
      <td>2022-01-10 09:24:26</td>
      <td>1</td>
      <td>12.01</td>
      <td>5</td>
      <td>Blue</td>
      <td>sup</td>
    </tr>
  </tbody>
</table>
</div>



In order to analyze Xiaohu's performance more conveniently and clearly, we extracted the following columns:

**year**: Year of the game\
**split**: LPL Spring or Summer Split\
**teamname**: The team the player plays for\
**playername**: player name\
**position**: Positions in a League of Legends team\
**side**: The red or blue side of the League of Legends game\
**champion**: The champion used\
**earned gpm**: Gold gained per minute of the game\
**dpm**: The damage caused to the enemy per minute of the game

Then, we narrow the data by the column we need, including in Spring and Summer Split, playername, position, side, champion, gold per miniute(earned gpm), damage per miniute (dpm).



<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>split</th>
      <th>teamname</th>
      <th>playername</th>
      <th>position</th>
      <th>side</th>
      <th>champion</th>
      <th>earned gpm</th>
      <th>dpm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>shanji</td>
      <td>top</td>
      <td>Blue</td>
      <td>Gwen</td>
      <td>266.5055</td>
      <td>491.7802</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>Aki</td>
      <td>jng</td>
      <td>Blue</td>
      <td>Jarvan IV</td>
      <td>262.9011</td>
      <td>194.5495</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>Creme</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Syndra</td>
      <td>301.8901</td>
      <td>552.8352</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>Able</td>
      <td>bot</td>
      <td>Blue</td>
      <td>Jinx</td>
      <td>339.2527</td>
      <td>422.7692</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>COLD</td>
      <td>sup</td>
      <td>Blue</td>
      <td>Nautilus</td>
      <td>155.5165</td>
      <td>100.0440</td>
    </tr>
  </tbody>
</table>
</div>


In order to better understand Xiaohu's performance, we need to compare him horizontally with other players in the same position. Therefore, we filter out the game data of all mid lane positions.



<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>split</th>
      <th>teamname</th>
      <th>playername</th>
      <th>position</th>
      <th>side</th>
      <th>champion</th>
      <th>earned gpm</th>
      <th>dpm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>Creme</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Syndra</td>
      <td>301.8901</td>
      <td>552.8352</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022</td>
      <td>Spring</td>
      <td>ThunderTalk Gaming</td>
      <td>Captain</td>
      <td>mid</td>
      <td>Red</td>
      <td>Vex</td>
      <td>223.7802</td>
      <td>239.0769</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>Creme</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>448.8366</td>
      <td>732.7978</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2022</td>
      <td>Spring</td>
      <td>ThunderTalk Gaming</td>
      <td>Captain</td>
      <td>mid</td>
      <td>Red</td>
      <td>Twisted Fate</td>
      <td>279.7230</td>
      <td>377.0360</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2022</td>
      <td>Spring</td>
      <td>FunPlus Phoenix</td>
      <td>Gori</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>303.1696</td>
      <td>504.2472</td>
    </tr>
  </tbody>
</table>
</div>


Then, we calculate the damage per gold (dpm_per_gpm), known as **DPG**, by dpm/gpm for all the players in LPL.




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>split</th>
      <th>teamname</th>
      <th>playername</th>
      <th>position</th>
      <th>side</th>
      <th>champion</th>
      <th>earned gpm</th>
      <th>dpm</th>
      <th>dpm_per_gpm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>Creme</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Syndra</td>
      <td>301.8901</td>
      <td>552.8352</td>
      <td>1.831247</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022</td>
      <td>Spring</td>
      <td>ThunderTalk Gaming</td>
      <td>Captain</td>
      <td>mid</td>
      <td>Red</td>
      <td>Vex</td>
      <td>223.7802</td>
      <td>239.0769</td>
      <td>1.068356</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>Creme</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>448.8366</td>
      <td>732.7978</td>
      <td>1.632661</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2022</td>
      <td>Spring</td>
      <td>ThunderTalk Gaming</td>
      <td>Captain</td>
      <td>mid</td>
      <td>Red</td>
      <td>Twisted Fate</td>
      <td>279.7230</td>
      <td>377.0360</td>
      <td>1.347891</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2022</td>
      <td>Spring</td>
      <td>FunPlus Phoenix</td>
      <td>Gori</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>303.1696</td>
      <td>504.2472</td>
      <td>1.663251</td>
    </tr>
  </tbody>
</table>
</div>

<iframe src="assets/tf.html" width=800 height=600 frameBorder=0></iframe>

Side is also a variable that needs to be count. When different champions are on different sides, due to the differences in the terrain of the red and blue sides, the method of using the champion is also different. As you can see above, for the champion, "Twisted Fate", the distribution of DPG are different. It showcase that the champion select in different side will create a different situation for players. Therefore we will recognize the same champion on different sides as different situations.

We will separate the data of Xiaohu from other LPL mid laners. By comparing the average DPG of different heroes used by Xiaohu on different sides with other LPL mid laners to understand Xiaohu's performance in each game.

Note: the average DPG of different champion and side data is in the columns called "dpm_per_gpm_avg".

Here is the **DPG** for Xiaohu!

<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>split</th>
      <th>teamname</th>
      <th>playername</th>
      <th>position</th>
      <th>side</th>
      <th>champion</th>
      <th>earned gpm</th>
      <th>dpm</th>
      <th>dpm_per_gpm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Royal Never Give Up</td>
      <td>Xiaohu</td>
      <td>mid</td>
      <td>Red</td>
      <td>Viktor</td>
      <td>290.5547</td>
      <td>574.4532</td>
      <td>1.977091</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Royal Never Give Up</td>
      <td>Xiaohu</td>
      <td>mid</td>
      <td>Red</td>
      <td>Zoe</td>
      <td>289.3791</td>
      <td>607.1863</td>
      <td>2.098238</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Royal Never Give Up</td>
      <td>Xiaohu</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Syndra</td>
      <td>281.4000</td>
      <td>473.5579</td>
      <td>1.682864</td>
    </tr>
    <tr>
      <th>44</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Royal Never Give Up</td>
      <td>Xiaohu</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Twisted Fate</td>
      <td>321.1839</td>
      <td>352.9597</td>
      <td>1.098933</td>
    </tr>
    <tr>
      <th>46</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Royal Never Give Up</td>
      <td>Xiaohu</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Twisted Fate</td>
      <td>319.4188</td>
      <td>573.9379</td>
      <td>1.796819</td>
    </tr>
  </tbody>
</table>
</div>

Calculate the data for Xiaohu's **DPG**(dpm_per_gpm_avg) for different splits, sides, and champions.

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>split</th>
      <th>side</th>
      <th>champion</th>
      <th>xiaohu_dpm_per_gpm_avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Ahri</td>
      <td>1.749823</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>2.393276</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Galio</td>
      <td>1.428157</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>LeBlanc</td>
      <td>1.901784</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Lucian</td>
      <td>2.223384</td>
    </tr>
  </tbody>
</table>
</div>


And here is the **DPG** for other players.

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>split</th>
      <th>teamname</th>
      <th>playername</th>
      <th>position</th>
      <th>side</th>
      <th>champion</th>
      <th>earned gpm</th>
      <th>dpm</th>
      <th>dpm_per_gpm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>Creme</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Syndra</td>
      <td>301.8901</td>
      <td>552.8352</td>
      <td>1.831247</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022</td>
      <td>Spring</td>
      <td>ThunderTalk Gaming</td>
      <td>Captain</td>
      <td>mid</td>
      <td>Red</td>
      <td>Vex</td>
      <td>223.7802</td>
      <td>239.0769</td>
      <td>1.068356</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2022</td>
      <td>Spring</td>
      <td>Oh My God</td>
      <td>Creme</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>448.8366</td>
      <td>732.7978</td>
      <td>1.632661</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2022</td>
      <td>Spring</td>
      <td>ThunderTalk Gaming</td>
      <td>Captain</td>
      <td>mid</td>
      <td>Red</td>
      <td>Twisted Fate</td>
      <td>279.7230</td>
      <td>377.0360</td>
      <td>1.347891</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2022</td>
      <td>Spring</td>
      <td>FunPlus Phoenix</td>
      <td>Gori</td>
      <td>mid</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>303.1696</td>
      <td>504.2472</td>
      <td>1.663251</td>
    </tr>
  </tbody>
</table>
</div>

Calculate the **DPG**(dpm_per_gpm_avg) for other players for different splits, sides, and champions.

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>split</th>
      <th>side</th>
      <th>champion</th>
      <th>dpm_per_gpm_avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Ahri</td>
      <td>1.971737</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Akali</td>
      <td>1.699806</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Annie</td>
      <td>2.045827</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Azir</td>
      <td>2.171837</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>2.139534</td>
    </tr>
  </tbody>
</table>
</div>

We merge the dataframes of other players with Xiaohu's dataframe to easily and clearly observe the difference between Xiaohu's average DPG and other players under different champions and sides. The Nan value contained in Xiaohu's average DPG means that Xiaohu did not choose the champion in the blue or red side of the split.

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>split</th>
      <th>side</th>
      <th>champion</th>
      <th>dpm_per_gpm_avg</th>
      <th>xiaohu_dpm_per_gpm_avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Ahri</td>
      <td>1.971737</td>
      <td>1.749823</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Akali</td>
      <td>1.699806</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Annie</td>
      <td>2.045827</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Azir</td>
      <td>2.171837</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>2.139534</td>
      <td>2.393276</td>
    </tr>
  </tbody>
</table>
</div>

# Assessment of Missingness

The League of Legends game data we use includes the game data of any game in LPL. Also, there is no data missingness in the initial data we used. Therefore, the missingness of data is not related to the collection of data itself. The data missingness in the above table comes from Xiaohu's champion selection and the side he is on. The missingness come from the champion he did not choose when he is in a certain split and a certain side, which is a random process. Hence, we recognize the missingness is **Missing at Random(MAR)** or **Missing Completely at Random(MCAR)** instead of **Not Missing at Random(NMAR)**.

In order to determine whether the missing value of Xiaohu is independent under different side and different champion selections so that we can measure the missingness is **Missing at Random(MAR)** or **Missing Completely at Random(MCAR)**, we need to use permutation and TVD to distinguish. By creating a new column, "xiaohu_missing", it indicates whether Xiaohu's data is missing compared to other players in this row. Finally, observe the difference between the two distribution by creating a pivot table and calculating TVD. Choosing the variable 'split' as the standard to distinguish if the missing is dependent or independent.

(Look at the distribution of coli when colx is missing and look at the distribution of coli when colx is not missing. Comparing null and non-null 'xiaohu_dpm_per_gpm_avg' distributions for 'split')

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>split</th>
      <th>side</th>
      <th>champion</th>
      <th>dpm_per_gpm_avg</th>
      <th>xiaohu_dpm_per_gpm_avg</th>
      <th>xiaohu_missing</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Ahri</td>
      <td>1.971737</td>
      <td>1.749823</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Akali</td>
      <td>1.699806</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Annie</td>
      <td>2.045827</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Azir</td>
      <td>2.171837</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>2.139534</td>
      <td>2.393276</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>

<iframe src="assets/addf.html" width=800 height=600 frameBorder=0></iframe>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>xiaohu_missing = False</th>
      <th>xiaohu_missing = True</th>
    </tr>
    <tr>
      <th>split</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Spring</th>
      <td>0.567568</td>
      <td>0.448276</td>
    </tr>
    <tr>
      <th>Summer</th>
      <td>0.432432</td>
      <td>0.551724</td>
    </tr>
  </tbody>
</table>
</div>

**test statistic**: TVD result, also known as the observed TVD
According to the table above, we can find the observed TVD is equal to 0.11929170549860202.

Use the permutation method to shuffle the values in the split, and then use multiple simulations to observe whether the distribution of 'split' when xiaohu data is missing is the same as the distribution of 'split' when xiaohu data under the change of the split value is not missing.

**Null hypothesis**: the distribution of 'split' when xiaohu data is missing is the same as the distribution of 'split' when xiaohu data under the change of the split value is not missing.\
**Alternative hypothesis**: the distribution of 'split' when xiaohu data is missing is different to the distribution of 'split' when xiaohu data under the change of the split value is not missing.\
**Significant level**: α = 0.05.

<iframe src="assets/tvdg.html" width=800 height=600 frameBorder=0></iframe>

(The p_value is equal to 0.2975.)\
The p_value create by observed TVD and empirical TVD, the 'split' distribution difference according to Xiaohu's data missingness, is close to 0.3, which is larger than the significant level, α = 0.05, we set. We fail to reject the null hypothesis which states that the distribution of 'split' when xiaohu data is missing is the same as the distribution of 'split' when xiaohu data under the change of the split value is not missing. Hence, the distribution of the them are indepentdent and the missingness of Xiaohu's data are Missing Completely at Random(MCAR).

### Imputation

As we have been prove that the missingness of Xiaohu's data are Missing Completely at Random(MCAR). Hence, we can impute the data by **probabilistic imputation**, which randomly select the Xiaohu's data that are not missing and impute them into the missing rows in the column. Moreover, we are comparing the Xiaohu's performance gap between Spring Split and Summer Split. The imputation process need to seperate them as 2 different part.

#### Spring Data
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>split</th>
      <th>side</th>
      <th>champion</th>
      <th>dpm_per_gpm_avg</th>
      <th>xiaohu_dpm_per_gpm_avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Ahri</td>
      <td>1.971737</td>
      <td>1.749823</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Akali</td>
      <td>1.699806</td>
      <td>0.644327</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Annie</td>
      <td>2.045827</td>
      <td>1.428157</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Azir</td>
      <td>2.171837</td>
      <td>1.470425</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Spring</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>2.139534</td>
      <td>2.393276</td>
    </tr>
  </tbody>
</table>
</div>

#### Summer Data
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>split</th>
      <th>side</th>
      <th>champion</th>
      <th>dpm_per_gpm_avg</th>
      <th>xiaohu_dpm_per_gpm_avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Summer</td>
      <td>Blue</td>
      <td>Ahri</td>
      <td>2.018176</td>
      <td>2.190875</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Summer</td>
      <td>Blue</td>
      <td>Akali</td>
      <td>2.051743</td>
      <td>2.199335</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Summer</td>
      <td>Blue</td>
      <td>Azir</td>
      <td>2.431485</td>
      <td>1.445139</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Summer</td>
      <td>Blue</td>
      <td>Brand</td>
      <td>2.709100</td>
      <td>1.171316</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Summer</td>
      <td>Blue</td>
      <td>Corki</td>
      <td>2.326786</td>
      <td>2.155207</td>
    </tr>
  </tbody>
</table>
</div>

Now, we have finish the imputation and seperate the data as the **spring_data** and **summer_data**, which represent the Spring Split, the average DPG for each champion select and side, and the Summer Split, the average DPG for each champion select and side. Both of them are finished the imputation by probabilistic imputation.

# Hypothesis Testing


**Null hypothesis**: Xiaohu have a better performnace in Spring split than Summer split according to the gap between his DPG with and other players' DPG in average.\
**Alternative hypothesis**: Xiaohu have a worse or equal performance in Spring split than Summer split according to the gap between his DPG with and other players' DPG in average.\
**test statistic**: the mean of the gap between Spring Split and Summer Split.\
**significant level**: α = 0.05.

**Note**: the 'gap' here means the mean of average DPG gap between Xiaohu's and other players for each champion select and side. We calculate the gap by using Xiaohu's average DPG minus other players' average DPG to see their performance gap for each champion select and side. We state that his performance gap between Spring split and Summer split is measure by the mean of 'gap' in Spring minus the mean of 'gap' in Summer.

**mean of gap = mean of Xiaohu's average DPG in different side and champion - mean of other players' average DPG in different side and champion**
 
The **mean of gap in spring** is equal to -0.07835090260952164.\
The **mean of gap in summer** is equal to -0.016971950490046725.

**Test statistic = mean of gap in spring - mean of gap in summer = -0.06137895211947492**

Finally we simulate the empirical result by randomly select the data from Xiaohu's data and caclulate the mean gap between him and other players multiple times.

<iframe src="assets/pfg.html" width=800 height=600 frameBorder=0></iframe>

(the **p value** is equal to 0.50155)

The p value generate by the test statistic and the empirical distribution are close to 0.5, which is larger than the significant level, α = 0.05. We fail to reject the null hypothesis which states that Xiaohu have a better performnace in Spring split than Summer split according to the gap between his DPG with and other players' DPG in average. Hence we can't state that Xiaohu have a better performance in Spring Split than Summer Split.

### The justification of the test statistic

The test statistic we choose to doing the camprison between Xiaohu's performance in Spring Split and Summer Split is called the average DPG in each situation. The situation here is seperate by the side he is on and the champion he choose in one game; The DPG come from the ratio of damage he cause to the opponent per miniutes to the gold he earn per miniutes, which can showcase his performance of transfering the resource he gain to the damage he cause. As we all konw, League of legend is a 5V5 game which means that the win or loose of the game are not depend on one player. Therefore, the win rate can only be used when we are measure the team performance. Moreover, although the KDA seems to be a nice choice for judge one players performance, as we mention above, different champion's mechanism may cause the advantage of get the kills or gain the assistent, which can't not illustrate the performance of one player. The 'gap' between Xiaohu and other players here is the mean of average DPG in different situation. The test statistic we made is the mean of the gap in Spring split minus the mean of the gap in Summer split, which can provide a more convinced result to see if Xiaohu is able to do a better performance or not in Spring Split.

## Thank you for reading through this analysis! We firmly believe that Xiaohu will prove himself even more in future tournaments. Royal Never Give Up!

![cat GIF](https://media.tenor.com/0tfISiQDwoIAAAAC/xiaohu-lpl.gif)
