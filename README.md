# Practicum I Course Project
This is an overview of my practicum I course project

## The project attempts to create a real world example of how a fraud model could be implemented. The dataset is from Kaggle and is linked below.

It contains several different notebooks to be run in order. Unfortunate, but I am not able to show the whole project in this readme. So, I will only show certain notebooks. The rest are in the code directory

First, a database was created using MySQL Workbench:

# Creating the database...

![Image of Database](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Database_View.PNG)

# Insert_Modeling_Dataset.ipynb

## This notebook will take our csv dataset, create a mysql table, and insert

### The dataset used is the Insurance Claims dataset from Kaggle

#### Roshan, Sharma. (2019; July). Insurance Claim, Version 1. Retrieved 8/25/2020 from https://www.kaggle.com/roshansharma/insurance-claim.

# 01 - Data Cleaning.ipynb

## This notebook will begin the data cleaning and exploration. Basically, we look at the dtypes, missing, etc.
Please see the ipynb file for details

```python
# Retrieve modeling dataset from the database
# Connecting to mysql database using sqlalchemy. This allows us to insert and retrieve dataframes with ease

# import mysql.connector
from sqlalchemy import create_engine

# Using an f string to input the user and password
connstring = f'mysql+mysqlconnector://{user}:{password}@127.0.0.1:3306/claims'
# Engine is a factory for connection. The connection does not happen here
engine = create_engine(connstring, echo=False)
# Connection happens here. Be sure to close
dbConnection    = engine.connect()
# Reading the table into a dataframe
df = pd.read_sql("select * from claims.train_dataset", dbConnection);
# Closing the connection
dbConnection.close()

df.head()
```

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

Afterwards, we will pickle the file to save the pandas dtypes

# 02 - Feature Engineering.ipynb

## The purpose of this notebook is to engineer some of the features to be used in the model.
### Some things done here may include binning, banding, dummy, normalization, etc


### We are treating this dataset with a no-look approach. Often, it is too time consuming or impractical to look at each feature. I personally have not tried this approach before. However with some datasets (say, 15,000 features wide), it is impossible to look at each features distribution. Therefore, we are attempting a programmatic approach for experimentation



# 02.1 - Test Dataset Prep.ipynb

## This notebook will apply transformations to the test dataset. 

Please view the ipynb file for a walkthrough

# 03 - Modeling-Final.ipynb

