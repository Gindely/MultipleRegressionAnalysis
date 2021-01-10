# Predictors on the Productivity of Hits in 2017 Major League Baseball
Hits in MLB Prediction Project
## Table of contents
* [A Multiple Regression Analysis of Batting Average and Hits](#A-Multiple-Regression-Analysis-of-Batting-Average-and-Hits)
* [A Simple Regression Model](#A-Simple-Regression-Model)
* [Matrix Methods](#Matrix-Methods)
* [Model Selection](#Model-Selection)
* [Cross Validation](#Cross-Validation)

## A Multiple Regression Analysis of Batting Average and Hits
### Introduction
The topic of this subject matter is on the starting lineup for all teams in the 2017 MLB season. I’ve been a baseball fan, specifically of the Yankees, since around 10 years old. I would watch the games with my family and we would cause so much commotion that my mother would think something bad had happened. I became such a giant fan of the Yankees throughout the years that I even got season tickets. Admittingly, I started to grow tired of baseball after that year, maybe it was all the travelling to the Bronx that I had to do, but in recent years my interest has started to slowly grow back. Therefore, for this analysis I’m interested in seeing how specific variables affect hits.
### Data Source
I was able to pull up the statistic for the starting lineup for 2017 of all Major League Baseball Teams on the following website:
https://www.baseball-reference.com/leagues/MLB/2017.shtml

### Variables
There are a total of 246 observations in this dataset. For this analysis the dependent variable is the total number of hits for each player and the independent variables are batting average, age, strikeouts, and at bats.

Hits: When the batter safely reaches first base after hitting the ball in fair territory

Batting Average: Number of hits divided by at bats

Age: Age of the batter

Strikeouts: Occurs when the batter racks up 3 strikes for failure to hit the ball into fair territory

Walks: occurs when a batter receives four pitches outside the strike zone and is in turn awarded first base

![Dataview](./img/dataview.png)

## A Simple Regression Model
### Scatterplot
![Scatterplot](./img/scatterplot.png)

## Analysis of Scatterplot
I don’t see obvious curvature in my data. We can see a bit of heteroscedasticity towards the bottom of the scatterplot. The pink line illustrates the vertical cut in the data. It could be that these players didn’t play a full season due to an injury or they might have just had a very bad year. No real leverage or outliers exist in this scatterplot. The two points that are separated by the pink line fall in line with the rest of the data and aren’t dramatically far away from the rest of the data points.

## The Linear Regression Model

Yx= &beta;<sub>o</sub> + &beta;<sub>1</sub>x + &epsilon;

(a)	Yx = subpopulation average, which is normally distributed, of hits that share the same batting average.

(b)	E(Yx) = the expected value of the random variable, Hits, conditional on knowing the batting average. For example, it is the expected value of the subpopulation average of hits given all the players with 0.250 batting average. 

(c)	V(Yx) = the variance of the random variable hits given the players with a batting average of 0.250.

## SAS Output for the Fitted Model
![Singleanalysis](./img/singleanalysis.png) ![Fitplot](./img/fitplot.png) <br />
At a given count of x, say in my case is a batting average of 0.250, we can picture a vertical line down that count, illustrated in green. That vertical line intersects the 2 dotted lines. The y coordinates of those intersections, illustrated by the purple dots, define the endpoints for the 95% prediction interval for the number of hits of the 247th (the next observation) player. As the vertical line passes through the shaded band, given by the pink slanted lines, it defines the 95% confidence interval for the subpopulation expected value of hits given a batting average of 0.250. Where the vertical line intersects the  line, the red dot, it gives us the point prediction of the number of hits of the 247th player with a batting average of 0.250.

## Analysis of Output
 a. The t-test
    i. We are testing if the population slope for hits and batting average is equal to       zero. 
           h<sub>o = &beta;<sub>1 =0
           h<sub>o = &beta;<sub>1 =! 0
 
    ii. 	Test statistic: t-stat =  (b<sub>1- &beta;<sub>1)/(s/√SSx)  =  (760.15209-0)/59.89739=12.69

Rejection Region: |12.69| > 1.970, &alpha;=0.05
	 t-critcal value with 2 d.f. = 1.970

Conclusion :	null hypothesis is rejected because the |t-stat| = |53.19| greater than the t-critical value of 1.970


**fixed acidity:** The predominant fixed acids found in wines are tartaric, malic, citric, and succinic. Wines produced from cool climate grapes are high in acidity and thus taste sour. These high-acid wines can be treated to reduce the acidity.
<br>

## Models Used
Linear Regression: Baseline Model
<br>
KNN
<br>
Random Forest

## Methodology
1. *Data Understanding and Data Cleaning:* Lengths and types of the variables were determined and data was checked for missing values. The dataset consists of all numeric variables. The dataset doesn't contain missing values.

2. *Exploratory Analysis:* Created visualizations to explore the target variable and examine the potential existance of outliers or corrupt data. Further visualized the relationship between the target and the feature variables and relationships between features.<br />

First, I examined the target variable, quality. The average of wines in this dataset are rated 5 or 6 and target variable is normally distributed.
![Targetviz](./img/targetplot.png) <br />

Second, a distribution plot and a box plot was created to examine the distribution of each feature and the interaction between feature and target respectively. 
![Featplot](./img/featplot.png) <br />

Lastly, a heatmap was created to further examine the degree of correlation between varibles.
![Heatmap](./img/heatmap.png) <br />

The highest positively correlated variables are:
* citric acid and fixed acidity
* density and fixed acidity
* alcohol and quality <br />

The highest negatively correlated variables are:
* citric acid and volatile acidity
* pH and fixed acidity
* pH and citric acidity
* denisty and alcohol <br />

3. *Feature Selection and Feature Engineering:* In order to access which features to use for the linear regression model, I reviewed the p-values for each feature in order to determine with features showed staistical significance. I applied backward elimination in order to select the best features for the model. The variance inflation factor shows that mulicollinearity does not exist in the model selected. For the random forest model, I applied binning to quality. Wines of quality 3-4 were considered as low, 5-6 were considered medium, and 7-8 were considered high quality. <br>
![Selfeatures](./img/selfeatures.png) ![Vif](./img/vif.png) <br />

4. *Model Building and Evaluation:* Established a baseline model and developed two additional models to see if I could improve upon the baseline. For each model a train-test split of 70%-30% was used. Each models were then fitted. <br />

### Baseline Model: Linear Regression
![Regressionplot](./img/regressionplot.png) <br />
  *MSE:* .39 <br>
  *R-squared:* 38% <br />
### KNN
![Knn](./img/knn.png) <br />
  *MSE:* .44 <br>
  *Accuracy:* 67% <br />
### Random Forest
![Randomforest](./img/randomforest.png) ![Distplotrf](./img/distplotrf.png) <br />
  *MSE:* .18 <br>
  *Accuracy:* 82% <br />

5. *Scoring the Dataset:* Evaluated the performance of each model based on MSE and R-squared/Accuracy. The model with lowest MSE and highest R-squared or Accuracy was selected for quality prediction.

## Model Results and Selection
**Random Forest gave the best prediction of quality with MSE of .18 and Accuracy of 82%.**
The distribution plot for the choosen model shows that the predicted values are very close to the actual values with a bit of an overestimation in the prediction of wines of "medium" quality and a slight underestimation in "low" and "high" quality wines. <br />
<br>
The plot below demostrates the level of importance of each feature on the quality of wine. The feature with the highest influence on quality is alcohol. <br>
![featimp](./img/featimp.png)<br />
