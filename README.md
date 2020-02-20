# Utilizing Yelp Cost Estimates for Estimating Neighborhood Affluency
Authors:  

[Jamie McElhiney](https://github.com/jmce619)  
[Julie B](https://github.com/juliebga)  
[Freda Xin](https://github.com/FredaXin)  

___
## Problem Statement
Have you ever driven through an unfamiliar neighborhood and been curious as to how affluent that neighborhood may be? In an unfamiliar neighborhood it may be hard to tell what kind of income bracket the inhabitants may be in and how much they are willing to shell out for their place of residence. We know a one-bedroom condo in a high-end city may be sold for more than a two story detached home in a rural area. Neighborhood is a harsh determining factor in home sale price. If the traditional information of determining neighborhood affluence is missing (e.g. tax returns or unemployment rate), how else can we measure neighborhood wealth?  
For our project, we want to be able to gauge neighborhood affluence using Yelp business data.  A prevalence of luxury shopping stores and high end restaurants mixed with higher commercial activity could be cue for affluent neighborhoods. We will look to uncover valuable information from our data set that will indicate which Yelp features may be key factors in assessing a neighborhood’s affluence. 

(**Place holder; Change later**)
This tool will estimate the affluence of a neighborhood based on the number of $ of businesses and services (according to Yelp) in a given neighborhood. ($, $$, $$$) This tool will expect to get, as an input, a list of zip codes or names of neighborhoods and will estimate the wealth of the locality. While traditional methods typically estimate wealth of a locality based on demographic characteristics (e.g. income or unemployment rate), the novelty of this approach is in its use of big data related to commercial activity and cost of product and services as an indicator for affluency.
___
## Executive Summary

During the data collection process, we used [Yelp Fusion
API](https://www.yelp.com/developers/documentation/v3/get_started) and collected
30,293 Yelp business information in NYC. To measure neighborhoods
afflunency, we used property values, i.e. home prices, and collected data from
the [NYC department of Finance Rolling Sales Data](https://www1.nyc.gov/site/finance/taxes/property-rolling-sales-data.page). This approach makes
intuitive sense, since a neighborhood's property can reveal how affluent the
residents are in that area. In addition, this approach is capable of incorporating
the most up to date real estate information (since NYC Department of Finance
generates data on a rolling basis for the past 12 months); this is an
advantage comparing to the past approaches of using IRS tax return
(which can be out of date and does not offer the current affluency status of a neighborhood).

For our project, we chose NYC as a case study to develop our models: NYC has
a high density of population, high concentration of businesses on Yelp, and high
diversity of types of businesses and neighborhoods, which are desirable when
training models; We also envisioned to generalize our models and to make it
transferrable to other urban areas in the U.S. We took the initial steps toward this
direction in our modeling phase. 

During the EDA process, we investigated Yelp's **$ rating** and found that the
most frequent ratings are $$ for NYC. We further broke this down into the 5
boroughs and found that $ rating are the most common price ratings for Queens,
Brooklyn, and Bronx; whereas $$ signs are the most common price rating for
Manhattan and Staten Island. The fact that Staten Island has a very high percentage
of $$ rating led us to rethink our assumption: is Yelp's $ rating a good
predictor for a neighborhood's affluency status? We then investigated other
features from Yelp's business listings, and found that (business)
**categories** yielded far more illuminating insights about a neighborhood's
affluency status. The features derived from the categories proved to be very
predictive in our models. In addition, we used K-means to generate 80 clusters based on
latitudes and longitudes: those clusters defined our **'neighborhood'**.  

As we stepped into the modeling phase, we developed two different approaches:
first, we used the clusters to generate aggregated data for each cluster and
developed 4 types of classification models: Logistic Regression, KNN,
Tree based models, and PCA. This approach has the advantage of high interpretability since
each observation represents the overall characteristics of the businesses in a given
neighborhood. In addition, this approach was our initial step of generalizing the
models that will be applicable for all urban areas in the U.S.. For the second
approach, we used all individual Yelp businesses as observations (about 20k) and
developed 4 types of classification models: Logistic Regression, KNN, Tree based
models, and Voting Classifier. In short, the first approach is a good and cheap
approach, while the second is fast and cheap. We will use **AUC ROC** as the metric
to eveluate the performance of our models.

![cheap_good_fast](./images/good_fast_cheap.jpg)
 
 [Image source](https://www.dancker.com/blog/good-fast-cheap/)

___
## Data Dictionary: Yelp


| Name | Data Types (Pandas) | Description |
|---|---|---|
|id|object|a unique ID for each business, e.g. E8RJkjfdcwgtyoPMjQ_Olg|
|alias |object|business name alias| 
|name|object|business name|
|image_url|object|URL of photos taken at a given business|
|is_closed|bool|True if the business is currently open, else False|
|url|object|url of business listing on Yelp|
|review_count|int64|Number of reviews|
|categories|object|List of category title and alias pairs associated with this business|
|rating|float64|Rating for this business (value ranges from 1, 1.5, ... 4.5, 5)|
|coordinates|object|Coordinates of this business|
|transactions|object|List of Yelp transactions that the business is registered for, such as pickup, delivery and restaurant_reservation.|
|price|object|Price level of the business. Value is one of \\$, \\$\\$, \\$\\$\\$ and \\$\\$\\$\\$.|
|location|object|Location of this business, including address, city, state, zip code and country.|
|phone|object|phone number of the business|
|display_phone|object|Phone number of the business formatted nicely to be displayed to users. The format is the standard phone number format for the business's country.|
|distance|float64|Distance in meters from the search location. This returns meters regardless of the locale.|


___
## Conclusion
For **modeling option 1**,  the Logistic Regression model outperformed the
ohters. We also explored Principal Component Analysis as a modeling option
for our cluster dataset and uncover interesting business associations that are
predictors of affluent neighborhoods.

Via Logistic Regression, we discovered numerous business types that are predictive of affluence in our NYC-based areas. The top predictors of affluence were french restaurants, cocktail bars and ramen shops. Cafes and Coffee shops also had a strong presence, along with wine and beer bars. This is intuitively sensible, as these types of business would typically be frequented by people with extra expendible income. People who are more affluent would be more able to sustain upscale alcohol establishments (cocktail and wine bars) and cafes.

We also discovered business types that are predictive of the negative class ('not affluent'). The top predictors of 'not affluent' areas are the fraction of pizza restaurants, hot dog shops, donut shops & 1-dollar sign businesses in general. This is intuitively sensible as these types of businesses provide quick and inexpensive food and product options.

As a supplemental analysis, motivated by the unusual size of our data set (many features, few observations), we also explored Principal Component Analysis. We determined that 99% of our feature's variance can be explained by just 56 principal components (relative to the ~260 original features). We closely investigated the two principal components that were most highly correlative with predicting affluence. It was affirming to find that the the most significant features to predict affluence (via the 1st Principal Component) are french/wine related as well as related to higher price points. On the opposite end of the same Principal Component, we again saw familiar busines types - similar to the features obtained via Logistic Regression in our full model comparison process (i.e., 1 dollar sign businesses, pizza, hotdogs and donuts). As mentioned earlier, we are not surprised that these features are negatively associated with affluence, as they are lower-priced and quick food options.

Despite the non-ideal nature of our modeling data set, we are satisfied by our model performance. We were able to attain a ROC AUC that is considerably better than our baseline. We found great insights into the nature of the types of businesses that are prominent (from a percentage perspective) in affluent NYC neighborhoods. Going forward, our client could leverage this type of modeling methodology to assess other cities in similar way, yielding insights into the distinct features that relate to 'affluence' in other cities.

As an alternate, quicker, and more statistical modeling approach, we will also
pursue a Modeling Option 2, where we make predictions based on the entire set of
businesses in NYC.

For **modeling option 2**,  the Voting Classifier outperfomed the others. The
Logstic Regression model was the second best performing model. Since the later
is very interpreterable, we explained the features based on the coefficient.

 Surprisingly, **review_count** is the strongest predictor for the positive class. Based on the coefficient, a one-unit change in review_count causes 'is affluent' to be e^(1.088083) times as likely. The potential reason might be: More review counts indicate higher volumes of costumers, which means the location might have a higher density of population and/or higher traffic.

The second strongest predictor for the positive class is rating: a one-unit change in rating causes 'affluent' to be e^(0.190824) times as likely.

To answer our client's question, i.e. whether the **Yelp $ ratings** can be used
to predict whether the neighborhood is affluent: based on our findings, Although
Yelp's $ rating is among the top 10 predictors, it *alone* cannot be the sole
predictor of a neighborhood's affluency; Combing with other characteristics of a
Yelp business will increase the predicting power.

For option 2, the best performing model is the Voting Classifier. Although the model does not have the optimal AUC ROC score, it can still serve our client's purpose as a fast and cheap estimator for a given neighborhood's affluency.

The advantage of this model is that it does not reply on past U.S census data to calculate the neighborhood's affluency, but rather using an individual Yelp business's characteristics to predict the affluency of the neighborhood where the business is located. Our client can input a single Yelp business information, such as rating, review_counts, and categorical, and get a fast predication of the neighborhood’s affluency status.

In addition, since no geographical features have been used as features to train our models, we assume that the model will be transferable to other urban neighborhoods outside of NYC. The possibility of this generalization will be explored in the future.


___
## Next Steps
Both of our modeling options came with certain assumptions: for option 1 
___

## References
- [Github Link for DSI-NYC (2) students' past
work.](https://github.com/Shaddyjr/predicting_affluence_using_yelp)
- 