# Automatidata---Generous-Tipper-Binary-Classification-Model


## Introduction 

This project aims to develop a classifier to predict wheather a rider would give high gratuities based on a variety of factors (High gratuity classified as a tip amount of over %20 of the taxi fare) The goal is to determine what features are most influential in separating low tippers form high tippers. Based on the model, riders from VeriFone Inc were deemed to have an overwhelming high correlation with generous tips, followed by pickup and dropoff location. The best performing model was a XGB classifier which achieved a recall of 0.78 and F1 Score of 0.74. 

## Business Understanding 

The project aims to understand the determining factors for high rider gratuity. Having a complete understanding of these factors can allow drivers to more easily identify customers who are likely to be generous tippers. It can also help identify the peak locations where riders often give high tips. 

## Data understanding 
The project uses a dataset called 2017_Yellow_Taxi_Trip_Data.csv. The data is gathered by the New York City Taxi & Commission. In order to shorten runtimes, a sample of 408 thousand rows was drawn from the 113 million rows from the original dataset. Features include pickup/dropoff times and locations, fare_amount and more. 

## Data Dictionary 
| Column name             | Description                                                       |
|-------------------------|-------------------------------------------------------------------|
| ID                      | Trip identification number                                        |
| VendorID                | A code indicating the TPEP provider that provided the record.     <br> 1 = Creative Mobile Technologies, LLC <br> 2 = VeriFone Inc. |
| tpep_pickup_datetime    | The date and time when the meter was engaged.                    |
| tpep_dropoff_datetime   | The date and time when the meter was disengaged.                 |
| Passenger_count         | The number of passengers in the vehicle.                         <br> This is a driver-entered value. |
| Trip_distance           | The elapsed trip distance in miles reported by the taximeter.    |
| PULocationID            | TLC Taxi Zone in which the taximeter was engaged.                |
| DOLocationID            | TLC Taxi Zone in which the taximeter was disengaged.             |
| RateCodeID              | The final rate code in effect at the end of the trip.            <br> 1 = Standard rate <br> 2 = JFK <br> 3 = Newark <br> 4 = Nassau or Westchester <br> 5 = Negotiated fare <br> 6 = Group ride |
| Store_and_fwd_flag      | This flag indicates whether the trip record was held in vehicle memory before being sent to the vendor, aka “store and forward,” because the vehicle did not have a connection to the server. <br> Y = store and forward trip <br> N = not a store and forward trip |
| Payment_type            | A numeric code signifying how the passenger paid for the trip.  <br> 1 = Credit card <br> 2 = Cash <br> 3 = No charge <br> 4 = Dispute <br> 5 = Unknown <br> 6 = Voided trip |
| Fare_amount             | The time-and-distance fare calculated by the meter.             |
| Extra                   | Miscellaneous extras and surcharges.                             <br> Currently, this only includes the $0.50 and $1 rush hour and overnight charges. |
| MTA_tax                 | $0.50 MTA tax that is automatically triggered based on the metered rate in use. |
| Improvement_surcharge   | $0.30 improvement surcharge assessed trips at the flag drop. The improvement surcharge began being levied in 2015. |
| Tip_amount              | Tip amount – This field is automatically populated for credit card tips. Cash tips are not included. |
| Tolls_amount            | Total amount of all tolls paid in trip.                         |
| Total_amount            | The total amount charged to passengers. Does not include cash tips. |


## Modeling and Evaluation 
A total of three classifiers were developed through gridsearch optimisation: RandomForest, Logistic Regression and XGB to predict whether certain trips would result in a generous tip. 

Prior to the model, a number of pre-processing steps and data transofrmations were applied to the original dataset. Pre-processing included checking for null values, duplicates, validating and standardising data. Transformations included engineering a generous tip boolean column by calculating the tip amount as a percentage to the fare amount. Pickup and dropoff locations were also one-hot encoded, along with splitting the time the ride took place into 4 time frames: am rush, daytime, pm rush and nighttime. 

Gridsearch was utilised with cross validation degree of 4 to find optimal parameters for each model. 

### Performance

| Model                               | Precision | Recall   | F1       | Accuracy |
|-------------------------------------|-----------|----------|----------|----------|
| XGB Test Scores                    | 0.695243  | 0.782203 | 0.736164 | 0.704880 |
| XGB Train Scores                   | 0.698655  | 0.770535 | 0.732753 | 0.704225 |
| Logistic Regression Test Scores    | 0.694397  | 0.763535 | 0.727327 | 0.698657 |
| Logistic Regression Train Scores   | 0.699666  | 0.753578 | 0.725545 | 0.700049 |
| RF test scores                     | 0.677704  | 0.764157 | 0.718339 | 0.684573 |
| RF Train scores                    | 0.683952  | 0.746733 | 0.713824 | 0.685064 |


XGB performed the best with an F1 score of 0.736. 

![d602ce6a-2022-486e-9b15-2207bdedc7c7](https://github.com/felix553/Automatidata---Generous-Tipper-Binary-Classification-Model/assets/81670336/dec7cc11-d113-4626-a5f6-214c92c16179)

However, observing the confusion matrix suggests that the model performance is still not very strong, with 551 false negatives. This could raise issues of taxi drivers declining certain trips in hopes of other trips that are more likely to result in generous tips when the rider was going to tip generously to begin with. 


The feature importances are as follows: 
![9361ff95-55fd-476b-81b7-d69831df346c](https://github.com/felix553/Automatidata---Generous-Tipper-Binary-Classification-Model/assets/81670336/3f289d1e-9b07-4bc6-a9ed-b583a0518dbd)


## Conclusion 
The model performs mediocrely at predicting generous tippers. More features may need to be engineered to gain a more accurate picture of factors contributing to a high tip. 





