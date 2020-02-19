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
___
## Next Steps
___

## References
- [Github Link for DSI-NYC (2) students' past
work.](https://github.com/Shaddyjr/predicting_affluence_using_yelp)
- 