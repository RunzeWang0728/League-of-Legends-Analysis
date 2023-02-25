

# Is RNG Xiaohu the "Tiger King of the Spring" in LPL? :thinking:
![cat GIF](https://media.tenor.com/Jh6tYjm6dOAAAAAC/xiaohu-rng-lpl.gif)


**Name(s)**: Runze Wang, Xuecheng Xu

# Introduction
## Background Information
![alt text](https://i.imgur.com/hZnnBki.jpg)

Xiaohu is one of the most prominent League of Legends Player around the world, especially in LPL league. His ID, Xiaohu, stands for "Little Tiger" in English. 

There is a saying in LPL that Xiaohu is the "Tiger King of the Spring" because his unforgettable performances in Spring split in LPL carried the team from elimination.

## Central Question
In this League of Legends Analysis, we would testify this claim:

***Is RNG Xiaohu the "Tiger King of the Spring" in LPL?*** 

Is this just a saying or it is a fact supported by data? :thinking:
## Approach


### **How to decide the performance of Xiaohu and other players?**

The first crucial decision is to find an approach to decide the performance of Xiaohu and other players. We use damage per gold deriving from damage per miniute (dpm) over gold per miniute (gpm). Damage per gold is the most optimal benchmark for a player. If the player utilizes the resources for damage output effectively, damage per gold would be higher. Vice versa.

The data we use is the csv file for match data in 2022 from [OE public Match Data](https://drive.google.com/drive/u/1/folders/1gLSw0RLjBbtaNy0dgnGQDAZOHIgCe-HH) with 149232 rows × 123 columns initially. After cleaning the data, the dataframe has 47 rows and 5 columns **(split, side, champion, dpm_per_gpm_avg,	xiaohu_dpm_per_gpm_avg)**
1. **split** : The time period of the collected data . The split contains Spring split and Summer split, where we need to use performance in Summer split to compare with spring split.
2. **side** : The side of the collected data. The side contains Red side and Blue side, where the same player could perform differently on different side, even if it is the same champion.
3. **champion** : The champions Xiaohu and other players use.
4. **dpm_per_gpm_avg** : The average damage per gold for other mid-lane players in LPL. This data is used to compared with damage per gold of XIaohu for hypothesis test.
5. **xiaohu_dpm_per_gpm_avg** : The average damage per gold for Xiaohu in LPL.

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
      <th>...</th>
      <th>opp_csat15</th>
      <th>golddiffat15</th>
      <th>xpdiffat15</th>
      <th>csdiffat15</th>
      <th>killsat15</th>
      <th>assistsat15</th>
      <th>deathsat15</th>
      <th>opp_killsat15</th>
      <th>opp_assistsat15</th>
      <th>opp_deathsat15</th>
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
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
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
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
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
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
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
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
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
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 123 columns</p>
</div>


Secondly, we identify the column we need to proceed the calculation, which is ['year','split','teamname','playername','position','side','champion','earned gpm','dpm']

Then, we narrow the data by the column we need, including in Spring and Summer Split, playername, position, side, champion, gold per miniute(earned gpm), damage per miniute (dpm)



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


Since, Xiaohu is a mid laner in 2022 so we are only looking at the stats of mid lane players for comparison and calculation.



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


Then, we calculate the damage per gold (dpm_per_gpm) by dpm/gpm for other players in LPL.




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



Also, Calculate the dpg for Xiaohu!

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


Calculate the data for Xiaohu's dpg for different splits, sides, and champions 




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


Calculate the dpg for other players just like what we did to Xiaohu.



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



Calculate the dpg for other players for different splits, sides, and champions 



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




Lastly, We merge the two dataframes of the dpg for different splits, sides, and champions for other players and Xiaohu (shown below). 
The NaN in Xiaohu's dpg column represents that Xiaohu did not use this champion in 2022

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




# Hypothesis Testing


**Null: Xiaohu have a better performnace in Spring split than Summer split 
according to the gap between his DPG with and other players' DPG in average**

**Alt: Xiaohu have a worse or equal performance in Spring split than Summer split
according to the gap between his DPG with and other players' DPG in average**

Since our data contains direction (i.e. we think Xiaohu's performance in Summer split is better), 
therefore, we adopt sample mean to hypothesis testing

For illustration purpose, sp_mean is the mean of the gap between Xiaohu's DPG with and other players' DPG in average in Spring split
 and su_mean is the mean of the gap between Xiaohu's DPG with and other players' DPG in average in Spring split.

The test statistics we use is the difference between sp_mean and su_mean. This will be the observed data for the simulation. (这里要解释为啥这个test statistics是好的。。。)

After simulation, we get the p-value = 0.49615

The p-value=0.49615, which is greater than 0.05, therefore, we fail to reject the null hypothesis.
Hence, we are unable to state that Xiaohu have a better performnace in Summer than Spring

## Thank you for reading through this analysis! We firmly believe that Xiaohu will prove himself even more in future tournaments. Royal Never Give Up!

![cat GIF](https://media.tenor.com/0tfISiQDwoIAAAAC/xiaohu-lpl.gif)
