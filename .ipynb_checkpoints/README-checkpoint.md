# Starbucks Offer Spending Prediction Model

For a more detailed writeup, please my blog post at https://medium.com/@jordan.nish/starbucks-promotion-strategy-308fdf31c36f

## Install
This project was made in Python 3 and requires the following libraries:
- Pandas
- Numpy
- Matplolib
- Scikit-learn

## Introduction
This data set contains simulated data that mimics customer behavior on the Starbucks rewards mobile app. 
Once every few days, Starbucks sends out an offer to users of the mobile app. 
An offer can be merely an advertisement for a drink or an actual offer such as a discount or BOGO (buy one get one free). 
Some users might not receive any offer during certain weeks.

We are given transactional data showing user purchases made on the app including the timestamp of purchase and the amount of money spent on a purchase. This transactional data also has a record for each offer that a user receives as well as a record for when a user actually views the offer. There are also records for when a user completes an offer.

The task is to combine transaction, demographic and offer data to determine which demographic groups respond best to which offer type. 

To do this, I will create a model that will predict the expected spending by a customer after receiving and viewing an offer.

## Data Sets
The data provided is contained in three files:

portfolio.json - containing offer ids and meta data about each offer (duration, type, etc.)
profile.json - demographic data for each customer
transcript.json - records for transactions, offers received, offers viewed, and offers completed
Here is an explanation of each variable in the files:

### portfolio.json

- id (string) - offer id
- offer_type (string) - type of offer ie BOGO, discount, informational
- difficulty (int) - minimum required spend to complete an offer
- reward (int) - reward given for completing an offer
- duration (int) - time for offer to be open, in days
- channels (list of strings)

### profile.json

- age (int) - age of the customer
- became_member_on (int) - date when customer created an app account
- gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)
- id (str) - customer id
- income (float) - customer's income

### transcript.json

- event (str) - record description (ie transaction, offer received, offer viewed, etc.)
- person (str) - customer id
- time (int) - time in hours since start of test. The data begins at time t=0
- value - (dict of strings) - either an offer id or transaction amount depending on the record

## Files

- clean_portfolio.csv: portfolio dataset after cleaning
- clean_profile.csv: profile dataset after cleaning
- clean_transcript.csv: transcript dataset after cleaning
- merged_data.csv: The top three datasets merged by person and offer_id
- master_df.csv: Data for each received offer and the amount spent from when the offer was viewed and when it ended
- xgb_model.sav: pickled model 



## Results
The model that performed best was XGBRegressor. It achieved a root mean squared error of $49.84, and a mean absolute error of $21.21.

The function **which_coupon** takes in customer demographic data, as well as how many days they have been a member and how many offers they have previously viewed, and produces a graph of the customers predicted spending. It returns a dataframe with the same information.
This can be used to select the best coupon for each customer. 

## Licensing and Acknowledgements
Data was provided by Udacity. 
