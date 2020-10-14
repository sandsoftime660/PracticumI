# Practicum I Course Project
This is an overview of my practicum I course project

## The project attempts to create a real world example of how a fraud model could be implemented. The dataset is from Kaggle and is linked below.

It contains several different notebooks to be run in order. Unfortunate, but I am not able to show the whole project in this readme. So, I will only show certain notebooks. The rest are in the code directory

First, a database was created using MySQL Workbench:

# Creating the database...

![Image of Database](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Database_View.PNG)

#### The motivation for using the database was to show how easily data can be queried from a database, put into a dataframe, and tables for training set distributions can be saved for realtime API usage. Rather than having a project filled with thousands of lines of sql joins and manipulation, having an analytics database (Say, a claims database with large, wide tables that already include all data elements at a claim level) is key to a quick and clean modeling process.

# Insert_Modeling_Dataset.ipynb

## This notebook will take our csv dataset, create a mysql table, and insert

### The dataset used is the Insurance Claims dataset from Kaggle

#### Roshan, Sharma. (2019; July). Insurance Claim, Version 1. Retrieved 8/25/2020 from https://www.kaggle.com/roshansharma/insurance-claim.

# 01 - Data Cleaning.ipynb

## This notebook will begin the data cleaning and exploration. Basically, we look at the dtypes, missing, etc.
Please see the ipynb file for details


### Here is a look at our data:

<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>months_as_customer</th>
      <th>age</th>
      <th>policy_number</th>
      <th>policy_bind_date</th>
      <th>policy_state</th>
      <th>policy_csl</th>
      <th>policy_deductable</th>
      <th>policy_annual_premium</th>
      <th>umbrella_limit</th>
      <th>insured_zip</th>
      <th>insured_sex</th>
      <th>insured_education_level</th>
      <th>insured_occupation</th>
      <th>insured_hobbies</th>
      <th>insured_relationship</th>
      <th>capital-gains</th>
      <th>capital-loss</th>
      <th>incident_date</th>
      <th>incident_type</th>
      <th>collision_type</th>
      <th>incident_severity</th>
      <th>authorities_contacted</th>
      <th>incident_state</th>
      <th>incident_city</th>
      <th>incident_location</th>
      <th>incident_hour_of_the_day</th>
      <th>number_of_vehicles_involved</th>
      <th>property_damage</th>
      <th>bodily_injuries</th>
      <th>witnesses</th>
      <th>police_report_available</th>
      <th>total_claim_amount</th>
      <th>injury_claim</th>
      <th>property_claim</th>
      <th>vehicle_claim</th>
      <th>auto_make</th>
      <th>auto_model</th>
      <th>auto_year</th>
      <th>fraud_reported</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>235</td>
      <td>39</td>
      <td>651861</td>
      <td>07-01-2011</td>
      <td>IL</td>
      <td>100/300</td>
      <td>500</td>
      <td>1046.58</td>
      <td>4000000</td>
      <td>434982</td>
      <td>MALE</td>
      <td>MD</td>
      <td>tech-support</td>
      <td>exercise</td>
      <td>wife</td>
      <td>0</td>
      <td>-31700</td>
      <td>24-01-2015</td>
      <td>Vehicle Theft</td>
      <td>?</td>
      <td>Trivial Damage</td>
      <td>None</td>
      <td>NY</td>
      <td>Hillsdale</td>
      <td>6193 1st Hwy</td>
      <td>1</td>
      <td>1</td>
      <td>?</td>
      <td>2</td>
      <td>1</td>
      <td>NO</td>
      <td>4950</td>
      <td>450</td>
      <td>900</td>
      <td>3600</td>
      <td>Chevrolet</td>
      <td>Silverado</td>
      <td>2010</td>
      <td>N</td>
    </tr>
    <tr>
      <th>1</th>
      <td>35</td>
      <td>35</td>
      <td>930032</td>
      <td>10-09-2002</td>
      <td>IL</td>
      <td>100/300</td>
      <td>2000</td>
      <td>1117.42</td>
      <td>0</td>
      <td>446158</td>
      <td>FEMALE</td>
      <td>PhD</td>
      <td>protective-serv</td>
      <td>kayaking</td>
      <td>not-in-family</td>
      <td>0</td>
      <td>-51900</td>
      <td>14-02-2015</td>
      <td>Multi-vehicle Collision</td>
      <td>Side Collision</td>
      <td>Minor Damage</td>
      <td>Fire</td>
      <td>NC</td>
      <td>Hillsdale</td>
      <td>7909 Andromedia Hwy</td>
      <td>23</td>
      <td>3</td>
      <td>NO</td>
      <td>2</td>
      <td>2</td>
      <td>NO</td>
      <td>53190</td>
      <td>5910</td>
      <td>11820</td>
      <td>35460</td>
      <td>Volkswagen</td>
      <td>Jetta</td>
      <td>1996</td>
      <td>N</td>
    </tr>
    <tr>
      <th>2</th>
      <td>50</td>
      <td>44</td>
      <td>525862</td>
      <td>18-10-2000</td>
      <td>OH</td>
      <td>250/500</td>
      <td>2000</td>
      <td>1188.51</td>
      <td>0</td>
      <td>447469</td>
      <td>MALE</td>
      <td>College</td>
      <td>handlers-cleaners</td>
      <td>bungie-jumping</td>
      <td>unmarried</td>
      <td>0</td>
      <td>-65800</td>
      <td>08-01-2015</td>
      <td>Multi-vehicle Collision</td>
      <td>Front Collision</td>
      <td>Total Loss</td>
      <td>Police</td>
      <td>NY</td>
      <td>Northbend</td>
      <td>4710 Lincoln Hwy</td>
      <td>15</td>
      <td>3</td>
      <td>?</td>
      <td>1</td>
      <td>2</td>
      <td>NO</td>
      <td>61100</td>
      <td>6110</td>
      <td>12220</td>
      <td>42770</td>
      <td>Dodge</td>
      <td>Neon</td>
      <td>2008</td>
      <td>N</td>
    </tr>
    <tr>
      <th>3</th>
      <td>456</td>
      <td>62</td>
      <td>669800</td>
      <td>24-06-2009</td>
      <td>OH</td>
      <td>250/500</td>
      <td>1000</td>
      <td>1395.77</td>
      <td>0</td>
      <td>611651</td>
      <td>FEMALE</td>
      <td>MD</td>
      <td>protective-serv</td>
      <td>chess</td>
      <td>own-child</td>
      <td>82600</td>
      <td>-49500</td>
      <td>07-02-2015</td>
      <td>Multi-vehicle Collision</td>
      <td>Side Collision</td>
      <td>Major Damage</td>
      <td>Other</td>
      <td>PA</td>
      <td>Hillsdale</td>
      <td>5352 Lincoln Drive</td>
      <td>13</td>
      <td>3</td>
      <td>?</td>
      <td>1</td>
      <td>3</td>
      <td>NO</td>
      <td>66480</td>
      <td>5540</td>
      <td>11080</td>
      <td>49860</td>
      <td>Saab</td>
      <td>92x</td>
      <td>2012</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>4</th>
      <td>150</td>
      <td>30</td>
      <td>354481</td>
      <td>17-11-2004</td>
      <td>IN</td>
      <td>100/300</td>
      <td>1000</td>
      <td>1342.02</td>
      <td>0</td>
      <td>608425</td>
      <td>MALE</td>
      <td>MD</td>
      <td>prof-specialty</td>
      <td>polo</td>
      <td>own-child</td>
      <td>0</td>
      <td>0</td>
      <td>28-02-2015</td>
      <td>Parked Car</td>
      <td>?</td>
      <td>Trivial Damage</td>
      <td>None</td>
      <td>VA</td>
      <td>Arlington</td>
      <td>6317 Best St</td>
      <td>8</td>
      <td>1</td>
      <td>YES</td>
      <td>0</td>
      <td>2</td>
      <td>NO</td>
      <td>4500</td>
      <td>450</td>
      <td>450</td>
      <td>3600</td>
      <td>Saab</td>
      <td>93</td>
      <td>1999</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>

Afterwards, we pickled the file to save the pandas dtypes

### This notebook was basic checking data types and missing values. Missing values were kept since there are times when having a missing value may be predictive (Zip missing, for example).

# 02 - Feature Engineering.ipynb

## The purpose of this notebook is to engineer some of the features to be used in the model.
### Some things done here may include binning, banding, dummy, normalization, etc

### We treated this dataset with a no-look approach. Often, it is too time consuming or impractical to look at each feature. I personally have not tried this approach before. However with some datasets (say, 15,000 features wide), it is impossible to look at each features distribution. Therefore, we are attempting a programmatic approach for experimentation.

#### This notebook took a capping approach to the numeric outliers. By calculating the mean and standard deviation, finding the low and high values that were 3 std away, capping values were set. If a value fell outside of this capped value, we used the capped value instead.

![Image of capping](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Cutoff_Chart.PNG)

#### Below is an image of what those values looked like

![Image of capping](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Capping_Values.PNG)

#### Encoding was used for categorical values. Target, polynomial, and several others were tried. The final choice was for target encoding. I found the target encoding to not be as predictive, however.

![Image of dummy](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Dummy.png)

#### FeatureTools was used to create more features to model. This was to highlight the capabilities of the tool. While it works well for a single dataframe, applying this to a relational database would assist an analyst not familiar with the data and how it is related. The choice to use one hot encoding created over 6000+ features. I was torn with the predictors >> data points, so went with target encoding.

![Image of featuretools](https://github.com/sandsoftime660/PracticumI/blob/main/Images/FeatureTools.png)

# 02.1 - Test Dataset Prep.ipynb

## This notebook applied the training transformations to the test dataset. 

#### The reason for this seperate notebook was to highlight the importance of keeping any training dataset distribution information out of the feature engineering. 

Please view the ipynb file for a walkthrough

# 03 - Modeling-Final.ipynb

## Now, on to the fun stuff

### The approach here was almost pure machine learning with very little 'data look'. Techniques such as TPOT, gridsearch, and auto feature reduction really gave this the machine driven vibe. Ultimately, I would like to turn this project into a continuous learning model. With that in mind, an algorithmic decision approach was implemented.

#### Our data was split 80/20. We only had 1000 rows of data so a validation dataset was not included in the analysis. Our target was not terribly imbalanced:

![Image of target](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Target.PNG)

#### TPOT was used for the inital analysis. I had not used it before, but automation was the goal here.

![Image of tpotcode](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Tpot_Code.PNG)

#### Oversampling was done once we found our optimal pipeline:

![Image of oversample](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Oversample.PNG)

I tried SMOTE, SVMSMOTE, and ADASYN. I ended up using SVMSMOTE.

#### I attempted to use Dask with TPOT. It worked well for awhile, but would always crash. Here is a view of dask at work (while it was):

![Image of dasktpot](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Dask_TPOT.PNG)

### The Final Model chosen was a GradientBoostingClassifier with SelectKBest feature selection. TPOT really helped defining what type of model to use. 

A neural network actually performed very well on this dataset. However, explaining the prediction was difficult and there were only a few features in the final model.

![Image of model](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Final_Model.PNG)

##### After TPOT ran, I was able to narrow down a pipeline. I ran TPOT on the original dataset, then bootstrapped, then ran grid search to find more optimal parameters.

10 features were selected for the final model. Parsimonious was a goal, but leaving enough features in to be able to give context to the prediction required a balance. 

### Feature importance was done via permutation due to decision tree placing more importance on high cardinality features:

![Image of model](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Feature_Importance.PNG)

### The goal was to set a cutoff for the predicted probabilites to increase precision (reducing false positives). However, the final model proved difficult in this regard. Recall and accuracy dropped considerably with no precision gain.

Future recommendations are to spend time defining two seperate models. One for prediction and one for explainability.

![Image of precision_recall](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Precision_Recall.PNG)

## Model Evaluation

### Model evaluation was done via lift chart and auc curve. 

#### The auc curve showed excellent predictive power. Stair stepping was expected, but results were incredibly smooth

![Image of auc](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Auc_Curve.PNG)

#### The lift chart showed great seperation between the classes. Expected volatility in the lower probabilities, but this was not the case. 

![Image of lift](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Lift_Chart.PNG)

#### The confusion matrix:

This looks great for accuracy and recall. As mentioned, precision suffered. There were other model types that increased precision to ~ 80%. However, these models proved difficult to explain. 

![Image of confusion](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Confusion_Matrix.PNG)

#### Accuracy, Recall, and Precision:

![Image of accuracy](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Accuracy.PNG)

## Explaining the Prediction

### This was possibly the most important aspect of the project. Being able to explain to an adjuster why a claim was fraudulent provided the most gain for the business side. 

ELI5 was used to explain the predictions and put them in context to the adjuster. An example of a prediction is below:

![Image of explain](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Explain_Prediction.PNG)

#### The contributing features can be compared to the mean of the target for that value and put into context, as shown below

![Image of reason](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Reason_Message2.PNG)

## This wraps up the analysis! 
