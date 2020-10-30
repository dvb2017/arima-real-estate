# Module 4 Final Project


## Introduction

**Business Case**  The business care here is quite simple.  A real estate investor would like to know the top five zip codes to invest based on the provided data.  This is left intentionally vague, giving us a few potential questions to answer.
- What criteria should I use to evaluate the investments?
- What quantitative targets should be used to evaluate the models?
- What are the five best zip codes for investment?


## Table of Contents

- presentation.pdf - a pdf file containing the powerpoint slides
- student.ipynb - Jupyter Notebook containing notated code
- README.md - this file, serving as a directory
- zillow_data.csv - the main dataset used here
- census_1996.csv - another dataset used here
- census_2018.csv - another dataset used here
- name_abbr.csv - another dataset used here
- charts - a folder containing all of the charts generated 

## The Dataset

The dataset here is fairly simple.  It includes housing prices for a large number of zip codes in the United States over a period of 22 years.  Along with each entry is the associated city, state, and size ranking.  The only real data of interest for our analysis will be the zip codes and time series housing prices, which is presented originally in wide format.  This just means that all of the date entries are on the same line, making the dataset 'wide'.

## The Cleaning

There were two separate and distinct steps here. The first was to narrow down the list of zip codes so that the modeling wouldn't be too time intensive.  I chose to do this by calculating the ROI from the beginning to the end of the time series for each zip code.  I then sorted these and selected the top 3% of zip codes to further examine.  These are the regions I would take a closer look at with the modeling as they seem to represent the best investments from a high level perspective.  The second step was to put the data in long form rather than wide form.  What this means is that each time series entry gets its own row.  I also created a dictionary that served as a list of lists with each zip code corresponding to its time series data so that they could be modeled separately.  For the long form data I set the index to correspond with the time series dates.  

## The Modeling

The first step I took here was to find the ARIMA parameters that best fit the remaining data.  In order to find this, I averaged the dataset for each date and ran a grid search model with varying parameters in order to find the lowest AIC value.  The Akaike Information Criterion gives us a score representing the prediction error. It takes into account both underfitting and overfitting so that both can be avoided.  Once I had found the model that best fit the average data, I ran each of the remaining zip codes through the model separately.  Once I had done this and put the information into a dataframe, I was able to rank each one according to its predicted ROI 5 years out.  I took the top 10 values here and tested each of these to make sure they were running at their optimal parameters, much like with the overall dataset.  At this point I was able to calculate the risk adjusted return for each of the top five values and rank them, giving my final result.  

## Conclusion/Results

Once this was all complete I was able to answer each of the three questions originally posed.  

- What criteria should I use to evaluate the investments?  
The answer here comes down to personal preference more so than any answer presented in the data.  I took a look at some reasonable investment standards and simply applied those.  For example, I chose to look at a time period of 5 years since that is a fairly standard investment time period, and it was short enough that a prediction would be more accurate and useful than ten or twenty years.  The evaluation metric I chose for this time period was risk-adjusted ROI.  This is because I wanted to provide investment advice that would give an optimal return while still controlling for downside risk.  

- What quantitative targets should be used to evaluate the models?   
In order to evaluate the models I again used fairly standard criteria.  While narrowing down optimal parameters I looked at the AIC score in order to make sure I was choosing a model that minimized overfitting and underfitting.  After optimal parameters had been selected, I also took MSE into consideration.  This was more indirect though, the error appeared in my investment analysis since it is considered when calculating the risk-adjusted return on investment.  
- What are the five best zip codes for investment?  
In the end, the five best zip codes that I would recommend are:
1. 90057
2. 11959
3. 94063
4. 95133
5. 95128




## Citation

1. https://www.census.gov/data/datasets/time-series/demo/popest/2010s-state-total.html
2. https://www.zillow.com/research/data/
3. https://www2.census.gov/programs-surveys/popest/tables/1990-2000/state/totals/st-99-03.txt
4. https://worldpopulationreview.com/states/state-abbreviations
