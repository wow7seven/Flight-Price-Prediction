Predict The Flight Ticket Price

# **1. Abstract:**

The paper reports my work and experience in predicting the flight ticket price using various features.The database i used can be found [**here**](https://docs.google.com/spreadsheets/d/1duJy_VZoxnF_1jydxndbFDo1ubc-sX6W/edit#gid=1005231314) or [Dataset.xlsx](https://docs.google.com/spreadsheets/d/1duJy_VZoxnF_1jydxndbFDo1ubc-sX6W/edit#gid=1005231314).I train various models and compare and analyze which i summarize in my report.

# **2. Introduction:**

Flight price prediction is quite an interesting and challenging problem and it also affects our lives.Predictions hardly depend on single variables and so is it in our case.Our dataset consists of eleven columns.Every feature is essential while predicting the price for example, increase in total number of stops increases our price to a great extent.Below is real time example of same airline same day flight with different number of stops and price almost doubles.

![](media/9f3736dcf4c3ecb14b4b1104a65f46b3.png)

![](media/187172a2e7546511fec0df18188bcba1.png)

# **3. Methodology:**

## **A.Overview**

I used 5 models namely,

1.  Decision Tree Regressor
2.  Linear Regressor
3.  Random Forest Regressor
4.  AdaboostRegressor
5.  Light Gradient Boosting Machine(LGBM) Regressor

## **B.Preprocessing**

The key to enhance accuracy for all models was to do rigorous and useful preprocessing.I did preprocessing for all the features and in fact changed the number of features.I will explain preprocessing for all the features below.This was essential to get a significantly better score.

Firstly deleting null values and resetting the index.**Date of journey** is an important feature and to further increase its usability I replaced it with **weekday** (monday==0), **date** and **month** columns.The idea being prices are higher on weekends and lower on weekdays, using seasonal trends thus using date and month would give help our model more compared to just date of journey.

Then I convert **Departure time** and **Arrival time** into the military hour system, i.e. 17:30 is 1730 hours =1730 and duration in total time in minutes, i.e. 2h 50 m = 170.

Label encoding remaining features namely Airline, Source, Destination,Route,Total Stop and Additional info.

However for **Total Stops** I label encoded it manually for 2 reasons since I wanted a single entry of total stops =4 to be encoded with the same number that of total stops =3.

Similarly for **Airline** i categorize Multiple carriers Premium economy, Jet Airways Business, Vistara Premium Economy and trujet into “Others” as they compromised only 0.2% of our data.

Finally i train my models using 3 types of data :

Type 1 -\> Data obtained after preprocessing shown above.

Type 2-\> Scaled data obtained after preprocessing shown above.

Type 3-\> Manually min-max scale only departure time,arrival time and duration of the data obtained after preprocessing shown above.

# **4. Implementation of classification algorithms:**

## **A. Decision Tree Regressor**

Decision tree regressor builds models in the form of a tree structure with decision nodes and leaf nodes. It runs very fast and gives a fair idea on how tree based regressors would work.The accuracies were:

|                | Type 1  | Type 2 | Type 3  |
|----------------|---------|--------|---------|
| Train Accuracy | 99.61   | 99.61  | 99.61   |
| Test Accuracy  | 83.16   | 83.06  | 83.5    |

## **B. Linear Regressor**

Linear Regression model makes a linear equation using all the features(variables) to predict the output variable which in our case is price.This also runs fast it is generally good for predicting 2 class classification and we see it performs badly for our model.

|                | Type 1  | Type 2 | Type 3  |
|----------------|---------|--------|---------|
| Train Accuracy | 43.74   | 43.74  | 43.74   |
| Test Accuracy  | 43.72   | 43.72  | 43.72   |

## **C. Random Forest Regressor**

Random Forest Classifiers use boosting ensemble methods to train by using various decision trees and finally combine the prediction from each tree to give the final result.

|                | Type 1  | Type 2 | Type 3  |
|----------------|---------|--------|---------|
| Train Accuracy | 97.88   | 97.89  | 97.93   |
| Test Accuracy  | 90.83   | 90.96  | 90.92   |

## **D. Adaboost Regressor**

Adaboost helps you combine multiple weak classifiers(one level decision tree) into a single strong one.It puts more weight on difficult to classify instances and less on those already handled well.

|                | Type 1  | Type 2 | Type 3  |
|----------------|---------|--------|---------|
| Train Accuracy | 24.25   | 44.12  | 31.86   |
| Test Accuracy  | 22.86   | 39.02  | 28.38   |

## **E. LGBM**

Is another tree based regressor which uses decision trees that are made level by level.It is fast and performs really well and is the best model in our case after tuning the parameters.

|                | Type 1  | Type 2 | Type 3  |
|----------------|---------|--------|---------|
| Train Accuracy | 91.19   | 91.37  | 91.09   |
| Test Accuracy  | 87.72   | 87.29  | 87.31   |

# **5.Note**

Since there are only 10 features dimensionality reduction or feature selection is not a good idea however i tried dimensionality reduction using PCA and feature selection using SFS both unsurprisingly reduce accuracies of all the models and SFS consumed a lot of time hence Dimensionality reduction and SFS were avoided.

# **6.Results and Analysis**

In general tree based models performed much better with the top two models being Random Forest Regressor and Light Gradient Boosting Machine (LGBM) Regressor.To further enhance the accuracies of these models and tune the parameters to get the best results.

For Random Forest I varied n_estimators and max_depth.

For LGBM I varied n_estimators, max_depth and learning_rate

![](media/af2bd149da8cd98a73aeceb63ff9bbba.png) ![](media/20374305d381ec0214dc6b8d6a89a2bb.png)

Hence our best model is **LGBM** parameters with **92.37%(Type 1)** accuracy and Random forest is second best with **90.81%(Type 2)** accuracy.Both consume less time and have good accuracies but LGBM is slightly better and in my opinion the best model for Flight Price Prediction.
