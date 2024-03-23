#### Objective

The task here is to perform A/B testing to determine if putting a gate at level 40 (test) instead of 30 (control) leads to significant differences between the following:

- the number of rounds played by a player during the first 14 days after installation
- retention of the player 1 day after installing
- retention of the player 7 days after installing

#### Overview of A/B Testing

A/B testing, also known as split testing, is a statistical method used in marketing, product development, and user experience design to compare two or more versions of a webpage, email, app feature, or other digital assets. The goal of A/B testing is to identify which version performs better in terms of predefined key performance indicators (KPIs), such as click-through rates, conversion rates, or user engagement metrics. These KPIs will be what is called the "target variable".

In an A/B test, users are randomly divided into two or more groups, with each group exposed to a different version of the asset being tested. One group, known as the control group (Group A), is shown the current version, while the other group, known as the test group (Group B), is shown a modified version. 

Depending on the data and target variable, different statiscial tests will be used to determine if the observed differences in both control and test groups are statistically significant. In other words, whether different versions of a product leads to an improvement in predefined KPIs.


#### DataSet 
The dataset used here for is from the following Kaggle URL :

https://www.kaggle.com/code/yufengsui/datacamp-project-mobile-games-a-b-testing/input

Variables are as follows:


| Column          | Description                                                                                          |
|-----------------|------------------------------------------------------------------------------------------------------|
| userid          | A unique number that identifies each player.                                                          |
| version         | Whether the player was put in the control group (gate_30 - a gate at level 30) or the group with the moved gate (gate_40 - a gate at level 40). |
| sum_gamerounds  | The number of game rounds played by the player during the first 14 days after installing.                |
| retention_1     | Did the player come back and play 1 day after installing?                                             |
| retention_7     | Did the player come back and play 7 days after installing?  



#### A/B Tests and Results

The null hypothesis here is that there is no difference between Groups A and B ie, any observed differences are not statistically significant.

##### Variable: sum_gamerounds

To perform a test for the number of rounds played by a player during the first 14 days after installation, we examine the variable "sum_gamerounds". This variable is continuous, and we use the following to determine which test should be used, which then gives us the p-value to compare against.

First, check if the distributions of "sum_gamerounds" split into groups A and B are normal using Shapiro test. 

If both groups A and B have  normal distributions:
- check if variances are homogeneous using Levene test. 
    - If both have homogeneous variances: use t-test
    - else, not homogeneous:  use Welch test
Else:
- use Mann Whitney U test

For this dataset and the target variable "sum_gamerounds", a Mann Whitney U test was used, with a p-value of 0.0509 > 0.05. The null hypothesis is not rejected and we conclude that there is no significant impact on the number of rounds played by a player during the first 14 days after installation by placing a gate at level 40 instead of 30.

##### Variable: retention_1 and retention_7

To perform a test for retention rates 1 and 7 days after installation of the update, we examine the variable "retention_1" and "retention_7". Since these are now categorical variables, different tests from the above have to be used. Here, a chi-squared test or Fisher's exact test will be considered, depending on the expected cell frequencies of the contingency table.

If expected cell frequencies of all cells >5:
- use chi-squared test
Else:
- use Fisher's exact test

For both target variables, expected cell frequencies meet the criteria for a chi-squared test, so this test was performed for both "retention_1" and "retention_7". Results are as follows:
- p-value for "retention_1" is 0.07501 > 0.05, we do not reject the null hypothesis and conclude that there is no significant impact on player retention one day after installation of an update, which places a gate at level 40 instead of 30.
- p-value for "retention_7" is 0.001639 < 0.05, we reject the null hypothesis and conclude that there is a significant impact on player retention seven days after installation of an update, which places a gate at level 40 instead of 30. 



