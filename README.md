
# Project Problem and Hypothesis

More than one-third (36.5%) of  the U.S. adult population suffer from obesity. The estimated annual medical cost of obesity in the U.S. was $147 billion in 2008. (source: CDC)

#### Goal:

The goal of this project is to use the Food Environment Atlas data to try to predict obesity rates in U.S. counties. Through visualization and analysis, identify what factors are the most important in driving obesity rates up. 

#### Hypothesis:

Counties with a high share of the population receiving food assistance (SNAP, free lunch for students program) as well as low access to healthy, affordable food and fitness facilities will have higher rates of obesity. 

# Proposed Methods and Models

The response variable, adult obesity rate by county in 2010, is represented as a percent variable, which is a continuous number. For this reason, multiple linear regression will be used.

Alternatively, obesity rates can be bucketed into bins to predict the obesity rank by county. In this case, logistic regression or random forests should be used to assign a rank (class) to each county. 

**Feature selection:**

In order to identify the most important variables to be included in the model, the following methods can be used:

1. Random Forests. The importance scores form RF will separate the least important variables from the top predictors.
2. Lasso. This method will yield features that do not predict the outcome and can be excluded.
3. Principal Component Analysis. This method could be used to convert correlated features into a set of uncorrelated predictors.

# Dataset

United States Department of Agriculture published Food Environment Atlas data that is composed of a range of 211 variables in three major categories:

1. **Food Choices** - describes access of U.S. population by county to healthy, affordable food (e.g.  ‘access and proximity to a grocery store’)
2. **Health and Wellbeing** - describes diabetes, obesity rates, and food insecurity
3. **Community Characteristics** - demographic composition (by age and race), income and poverty characteristics, county status (metro/non-metro), availability of recreation and fitness facilities 

The data set is available in the Excel format with each category variables aggregated on the respective worksheet (see categories below). The data will be combined into one file using FIPS codes (State and county Federal information processing standards) included in each worksheet. 

Category| Number of Variables
---|---|---
Access and Proximity to Grocery Store | 10
Food Assistance | 52
Food Prices and Taxes | 8
Health and Physical Activity | 16
Local Foods | 46
Restaurant Availability and Expenditures | 16
Socioeconomic Characteristics | 15
State Food Insecurity | 12
Store Availability | 36

Each row in the data set contains food environment indicators for one of the U.S. counties. These data were collected by USDA from a variety of sources and cover varying years and geographic levels. For some indicators, the data were not available at a county level. In these cases, the State and regional level data were used. The indicators in the dataset come in several types: count, percent, % change, count per 1,000 pop, dollars/capita, classification, ratio, acres, sqft, etc. Obesity rates in the data set are available for 2010. 

Source: Economic Research Service (ERS), U.S. Department of Agriculture (USDA). Food Environment Atlas.

The data dictionary and documentation can be found [here](https://github.com/elenabohenick/obesity_analysis/blob/master/Variable_List.xlsx) and [here](https://github.com/elenabohenick/obesity_analysis/blob/master/documentation.pdf)

# Domain knowledge

As obesity in America is one of the major health issues among both adults and children and obesity rates keep growing, there have been a number of studies performed to tackle this problem. 

Obesity is medically defined as having a body mass index (BMI), a measure of height to weight, that is over 30 points. 

Poverty rates, density of fast food restaurants, low access to a grocery store (i.e. over a mile away from the consumer’s home) have been shown to increase obesity rates. While access to recreation and fitness facilities as well as access to fresh foods can reduce obesity rates. 

# Project Concerns

Large number of variables and relatively small number of records (~3,150) increase the risk of overfitting. 

#### _Covariance:_

Variables in each category are subject to covariance since they describe similar subjects. Besides, many variables can be characterized as related to poverty levels. Thus, variables are also subject to covariance across categories. 

#### _Causality:_

There is a question of cause and effect between obesity rates and diabetes. For this reason I will not be including variables describing diabetes rates into my model.

#### _Year when the data was collected:_

Some variables are from 2012, while the obesity rates, the value I am trying to predict, are from 2010. Thus, future data cannot be used in the model. 

#### _Data at different levels of granularity:_

Not all variables are available at a county level. Those that are available at a state-only level showcase the same value for each county in the state. This might affect the predicting power of variables. 

#### _Data not included in the data set that would be interesting to look at:_

Obesity rates across different racial groups would be interesting to look at with the hypothesis being that different factors might have higher importance for obesity rates for one racial group over the other. It would also be interesting to compare factor importance by looking at the data broken down by gender. 

## Outcomes

I will narrow down the number of features my model uses to around 10 or less since the assumption is that many of the features are highly correlated. 

I am hoping to find relationships between a number of food environment factors and obesity rates. Ideally, using on the optimal set of meaningful factors, my model’s mean absolute error should be as low as possible. I can use MAE from a multiple linear regression model that takes all available variables as a baseline. 
