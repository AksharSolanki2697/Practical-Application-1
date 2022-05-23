# Practical Application 1


## Context

Imagine driving through town and a coupon is delivered to your cell phone for a restaraunt near where you are driving. Would you accept that coupon and take a short detour to the restaraunt? Would you accept the coupon but use it on a sunbsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaraunt? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? Would weather impact the rate of acceptance? What about the time of day?

Obviously, proximity to the business is a factor on whether the coupon is delivered to the driver or not, but what are the factors that determine whether a driver accepts the coupon once it is delivered to them? How would you determine whether a driver is likely to accept a coupon?

## Overview

The goal of this project is to use what you know about visualizations and probability distributions to distinguish between customers who accepted a driving coupon versus those that did not.

## Data

This data comes to us from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios including the destination, current time, weather, passenger, etc., and then ask the person whether he will accept the coupon if he is the driver. Answers that the user will drive there ‘right away’ or ‘later before the coupon expires’ are labeled as ‘Y = 1’ and answers ‘no, I do not want the coupon’ are labeled as ‘Y = 0’.  There are five different types of coupons -- less expensive restaurants (under \\$20), coffee houses, carry out & take away, bar, and more expensive restaurants (\\$20 - \\$50). 

### Data Description

The attributes of this data set include:
1. User attributes
    -  Gender: male, female
    -  Age: below 21, 21 to 25, 26 to 30, etc.
    -  Marital Status: single, married partner, unmarried partner, or widowed
    -  Number of children: 0, 1, or more than 1
    -  Education: high school, bachelors degree, associates degree, or graduate degree
    -  Occupation: architecture & engineering, business & financial, etc.
    -  Annual income: less than \\$12500, \\$12500 - \\$24999, \\$25000 - \\$37499, etc.
    -  Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -  Number of times that he/she buys takeaway food: 0, less than 1, 1 to 3, 4 to 8 or greater
    than 8
    -  Number of times that he/she goes to a coffee house: 0, less than 1, 1 to 3, 4 to 8 or
    greater than 8
    -  Number of times that he/she eats at a restaurant with average expense less than \\$20 per
    person: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -  Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    

2. Contextual attributes
    - Driving destination: home, work, or no urgent destination
    - Location of user, coupon and destination: we provide a map to show the geographical
    location of the user, destination, and the venue, and we mark the distance between each
    two places with time of driving. The user can see whether the venue is in the same
    direction as the destination.
    - Weather: sunny, rainy, or snowy
    - Temperature: 30F, 55F, or 80F
    - Time: 10AM, 2PM, or 6PM
    - Passenger: alone, partner, kid(s), or friend(s)


3. Coupon attributes
    - time before it expires: 2 hours or one day



### Data Exploration and Cleaning

1. Using the pandas .info() and .describe() function to get an overview of the data. 
2. Looking for unique values in every column in the dataframe. This helps in finding NaN stored as a string which is difficult for isna() function in pandas to detect.
3. Found that column toCoupon_GEQ5min had only one unique value and no missing value. Therefore, since all records have the same information, it doesnot add any new information that we already know. Therefore I decided to drop the column.
4. Finding NULL attributes: car column had 99% missing data and therefore have dropped the column since it didnot add any information to the data.
5. Found out that Columns Bar, CoffeeHouse, CarryAway, RestauranceLessThan20, Restaurant20To50 have nan values. 
6. In all, these 5 columns consist of less than 5% (4.14%) of the data and that is why I decided to drop all rows that have any NaN field. Losing ~4% of data is not an ideal way and we can try to reduce this further. If we delete those rows that have all these columns as NaN then, we wouldnt delete much data and would also retain alot of the information. Therefore, this means that we will lose only 0.33% of the data which is acceptable. 
7. Therefore in the analysis above, since all the columns were string values, we can either store an empty string in place of the NaN or remove the rows. If these columns were real number, we could have assumed a mean for the NaN field but in this case, it is beneficial to remove the rows completely that have all the mentioned columns as null.

### Insights

1. 56.93% of the total observations chose to accept the coupon
