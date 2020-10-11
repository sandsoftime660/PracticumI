# Practicum I Course Project
This is an overview of my practicum I course project

## The project attempts to create a real world example of how a fraud model could be implemented. The dataset is from Kaggle and is linked below.

It contains several different notebooks to be run in order. First, a database was created using MySQL Workbench:

# Creating the database...

![Image of Database](https://github.com/sandsoftime660/PracticumI/blob/main/Images/Database_View.PNG)


# Insert_Modeling_Dataset.ipynb


## This notebook will take our csv dataset, create a mysql table, and insert

### The dataset used is the Insurance Claims dataset from Kaggle

#### Roshan, Sharma. (2019; July). Insurance Claim, Version 1. Retrieved 8/25/2020 from https://www.kaggle.com/roshansharma/insurance-claim.


```python
# Setup imports and read csv
import pandas as pd
import numpy as np
import warnings
warnings.filterwarnings('ignore')
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)

path = r"C:\Users\sands\OneDrive\Desktop\MSDS_DATA_PRACTICUM\Data\Modeling"

df = pd.read_csv(path + '\insurance_claims.csv')
print(len(df.columns))
df.head()
```

    39
    




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
      <td>328</td>
      <td>48</td>
      <td>521585</td>
      <td>17-10-2014</td>
      <td>OH</td>
      <td>250/500</td>
      <td>1000</td>
      <td>1406.91</td>
      <td>0</td>
      <td>466132</td>
      <td>MALE</td>
      <td>MD</td>
      <td>craft-repair</td>
      <td>sleeping</td>
      <td>husband</td>
      <td>53300</td>
      <td>0</td>
      <td>25-01-2015</td>
      <td>Single Vehicle Collision</td>
      <td>Side Collision</td>
      <td>Major Damage</td>
      <td>Police</td>
      <td>SC</td>
      <td>Columbus</td>
      <td>9935 4th Drive</td>
      <td>5</td>
      <td>1</td>
      <td>YES</td>
      <td>1</td>
      <td>2</td>
      <td>YES</td>
      <td>71610</td>
      <td>6510</td>
      <td>13020</td>
      <td>52080</td>
      <td>Saab</td>
      <td>92x</td>
      <td>2004</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>1</th>
      <td>228</td>
      <td>42</td>
      <td>342868</td>
      <td>27-06-2006</td>
      <td>IN</td>
      <td>250/500</td>
      <td>2000</td>
      <td>1197.22</td>
      <td>5000000</td>
      <td>468176</td>
      <td>MALE</td>
      <td>MD</td>
      <td>machine-op-inspct</td>
      <td>reading</td>
      <td>other-relative</td>
      <td>0</td>
      <td>0</td>
      <td>21-01-2015</td>
      <td>Vehicle Theft</td>
      <td>?</td>
      <td>Minor Damage</td>
      <td>Police</td>
      <td>VA</td>
      <td>Riverwood</td>
      <td>6608 MLK Hwy</td>
      <td>8</td>
      <td>1</td>
      <td>?</td>
      <td>0</td>
      <td>0</td>
      <td>?</td>
      <td>5070</td>
      <td>780</td>
      <td>780</td>
      <td>3510</td>
      <td>Mercedes</td>
      <td>E400</td>
      <td>2007</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>2</th>
      <td>134</td>
      <td>29</td>
      <td>687698</td>
      <td>06-09-2000</td>
      <td>OH</td>
      <td>100/300</td>
      <td>2000</td>
      <td>1413.14</td>
      <td>5000000</td>
      <td>430632</td>
      <td>FEMALE</td>
      <td>PhD</td>
      <td>sales</td>
      <td>board-games</td>
      <td>own-child</td>
      <td>35100</td>
      <td>0</td>
      <td>22-02-2015</td>
      <td>Multi-vehicle Collision</td>
      <td>Rear Collision</td>
      <td>Minor Damage</td>
      <td>Police</td>
      <td>NY</td>
      <td>Columbus</td>
      <td>7121 Francis Lane</td>
      <td>7</td>
      <td>3</td>
      <td>NO</td>
      <td>2</td>
      <td>3</td>
      <td>NO</td>
      <td>34650</td>
      <td>7700</td>
      <td>3850</td>
      <td>23100</td>
      <td>Dodge</td>
      <td>RAM</td>
      <td>2007</td>
      <td>N</td>
    </tr>
    <tr>
      <th>3</th>
      <td>256</td>
      <td>41</td>
      <td>227811</td>
      <td>25-05-1990</td>
      <td>IL</td>
      <td>250/500</td>
      <td>2000</td>
      <td>1415.74</td>
      <td>6000000</td>
      <td>608117</td>
      <td>FEMALE</td>
      <td>PhD</td>
      <td>armed-forces</td>
      <td>board-games</td>
      <td>unmarried</td>
      <td>48900</td>
      <td>-62400</td>
      <td>10-01-2015</td>
      <td>Single Vehicle Collision</td>
      <td>Front Collision</td>
      <td>Major Damage</td>
      <td>Police</td>
      <td>OH</td>
      <td>Arlington</td>
      <td>6956 Maple Drive</td>
      <td>5</td>
      <td>1</td>
      <td>?</td>
      <td>1</td>
      <td>2</td>
      <td>NO</td>
      <td>63400</td>
      <td>6340</td>
      <td>6340</td>
      <td>50720</td>
      <td>Chevrolet</td>
      <td>Tahoe</td>
      <td>2014</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>4</th>
      <td>228</td>
      <td>44</td>
      <td>367455</td>
      <td>06-06-2014</td>
      <td>IL</td>
      <td>500/1000</td>
      <td>1000</td>
      <td>1583.91</td>
      <td>6000000</td>
      <td>610706</td>
      <td>MALE</td>
      <td>Associate</td>
      <td>sales</td>
      <td>board-games</td>
      <td>unmarried</td>
      <td>66000</td>
      <td>-46000</td>
      <td>17-02-2015</td>
      <td>Vehicle Theft</td>
      <td>?</td>
      <td>Minor Damage</td>
      <td>None</td>
      <td>NY</td>
      <td>Arlington</td>
      <td>3041 3rd Ave</td>
      <td>20</td>
      <td>1</td>
      <td>NO</td>
      <td>0</td>
      <td>1</td>
      <td>NO</td>
      <td>6500</td>
      <td>1300</td>
      <td>650</td>
      <td>4550</td>
      <td>Accura</td>
      <td>RSX</td>
      <td>2009</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Get database username and password
import getpass as gp

user = input("Please enter your database username: ")
print("Please enter your database password: ")
password = gp.getpass()
```

    Please enter your database username: pthielma
    Please enter your database password: 
    ········
    

### This next cell will do two different things:
#### First, we will be splitting off the data into a training, test and validation. The ratios are Train: 80%, Test: 20%
##### The reason for the split here is so that we are not tempted to look at the holdout data during modeling!
#### Second, we will be creating two tables, one for train and test.


```python
# We are using sklearn to split the dataset. We are also stratifying the target so we get a nice distribution in each set
from sklearn.model_selection import train_test_split

X = df.drop(['fraud_reported'], axis=1)
y = df[['fraud_reported']]

# We are creating the training and test dataset here
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.20, random_state=22, stratify = y)
```


```python
# Connecting to mysql database using sqlalchemy. This allows us to insert and retrieve dataframes with ease
# import mysql.connector
from sqlalchemy import create_engine

# Using an f string to input the user and password
connstring = f'mysql+mysqlconnector://{user}:{password}@127.0.0.1:3306/claims'
engine = create_engine(connstring, echo=False)

# Saving the datasets
X_train['fraud_reported'] = y_train
X_test['fraud_reported'] = y_test
df.to_sql(name='full_modeling_dataset', con=engine, if_exists = 'append', index=False)
X_train.to_sql(name='train_dataset', con=engine, if_exists = 'append', index=False)
X_test.to_sql(name='test_dataset', con=engine, if_exists = 'append', index=False)
```

### Now that the data is stored in the database, we will continue to next notebook


# 01 - Data Cleaning.ipynb

## This notebook will begin the data cleaning and exploration


```python
# Initial imports...
import pandas as pd
import numpy as np
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
```


```python
# Get database username and password
import getpass as gp

user = input("Please enter your database username: ")
print("Please enter your database password: ")
password = gp.getpass()
```

    Please enter your database username: pthielma
    Please enter your database password: 
    ········
    


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




```python
# First thing to note is that there are ? for some of the values, lets set these to nan type
df.replace('?', np.nan, inplace=True)
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
      <td>NaN</td>
      <td>Trivial Damage</td>
      <td>None</td>
      <td>NY</td>
      <td>Hillsdale</td>
      <td>6193 1st Hwy</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
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
      <td>NaN</td>
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
      <td>NaN</td>
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
      <td>NaN</td>
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




```python
# Quick list of columns that have null values
df.columns[df.isna().any()].tolist()
```




    ['collision_type', 'property_damage', 'police_report_available']




```python
# Since these are all categorical, we will replace the nulls back with the string ? values for visualization. 
# This will also make it easier later since we don't need to convert test/valid data. 
df.replace(np.nan, '?', inplace=True)
```

### Not too many missing values in this dataset! Lets look at the distribution of these missing for the three columns


```python
# Collision type
import plotly.express as px
import plotly.io as pio
from IPython.display import Image
fig = px.histogram(df, x="collision_type")
# fig.show()

Image(pio.to_image(fig, format='png'))
```



![Image of Database](https://github.com/sandsoftime660/PracticumI/blob/main/Images/output_8_0.png)





```python
# Property Damage
fig = px.histogram(df, x="property_damage")
# fig.show()
Image(pio.to_image(fig, format='png'))
```




![Image of Database](https://github.com/sandsoftime660/PracticumI/blob/main/Images/output_9_0.png)




```python
# Police Report Available
fig = px.histogram(df, x="police_report_available")
# fig.show()
Image(pio.to_image(fig, format='png'))
```




![Image of Database](https://github.com/sandsoftime660/PracticumI/blob/main/Images/output_10_0.png)



### Since there are quite a few nulls, the decision has been made to leave these as values. Sometimes, the absence of something can also be predictive

#### Now, we will explore the data types of the columns and convert them if neccesary. We will also drop columns that are irrelevant


```python
df.drop(['policy_number', 'insured_zip', 'policy_bind_date', 'incident_date','incident_city','incident_location'], axis=1, inplace=True)

df.head()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>months_as_customer</th>
      <th>age</th>
      <th>policy_state</th>
      <th>policy_csl</th>
      <th>policy_deductable</th>
      <th>policy_annual_premium</th>
      <th>umbrella_limit</th>
      <th>insured_sex</th>
      <th>insured_education_level</th>
      <th>insured_occupation</th>
      <th>insured_hobbies</th>
      <th>insured_relationship</th>
      <th>capital-gains</th>
      <th>capital-loss</th>
      <th>incident_type</th>
      <th>collision_type</th>
      <th>incident_severity</th>
      <th>authorities_contacted</th>
      <th>incident_state</th>
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
      <td>IL</td>
      <td>100/300</td>
      <td>500</td>
      <td>1046.58</td>
      <td>4000000</td>
      <td>MALE</td>
      <td>MD</td>
      <td>tech-support</td>
      <td>exercise</td>
      <td>wife</td>
      <td>0</td>
      <td>-31700</td>
      <td>Vehicle Theft</td>
      <td>?</td>
      <td>Trivial Damage</td>
      <td>None</td>
      <td>NY</td>
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
      <td>IL</td>
      <td>100/300</td>
      <td>2000</td>
      <td>1117.42</td>
      <td>0</td>
      <td>FEMALE</td>
      <td>PhD</td>
      <td>protective-serv</td>
      <td>kayaking</td>
      <td>not-in-family</td>
      <td>0</td>
      <td>-51900</td>
      <td>Multi-vehicle Collision</td>
      <td>Side Collision</td>
      <td>Minor Damage</td>
      <td>Fire</td>
      <td>NC</td>
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
      <td>OH</td>
      <td>250/500</td>
      <td>2000</td>
      <td>1188.51</td>
      <td>0</td>
      <td>MALE</td>
      <td>College</td>
      <td>handlers-cleaners</td>
      <td>bungie-jumping</td>
      <td>unmarried</td>
      <td>0</td>
      <td>-65800</td>
      <td>Multi-vehicle Collision</td>
      <td>Front Collision</td>
      <td>Total Loss</td>
      <td>Police</td>
      <td>NY</td>
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
      <td>OH</td>
      <td>250/500</td>
      <td>1000</td>
      <td>1395.77</td>
      <td>0</td>
      <td>FEMALE</td>
      <td>MD</td>
      <td>protective-serv</td>
      <td>chess</td>
      <td>own-child</td>
      <td>82600</td>
      <td>-49500</td>
      <td>Multi-vehicle Collision</td>
      <td>Side Collision</td>
      <td>Major Damage</td>
      <td>Other</td>
      <td>PA</td>
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
      <td>IN</td>
      <td>100/300</td>
      <td>1000</td>
      <td>1342.02</td>
      <td>0</td>
      <td>MALE</td>
      <td>MD</td>
      <td>prof-specialty</td>
      <td>polo</td>
      <td>own-child</td>
      <td>0</td>
      <td>0</td>
      <td>Parked Car</td>
      <td>?</td>
      <td>Trivial Damage</td>
      <td>None</td>
      <td>VA</td>
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




```python
# Looking at our datatypes. This will help us to determine which need dummies
df.dtypes
```




    months_as_customer               int64
    age                              int64
    policy_state                    object
    policy_csl                      object
    policy_deductable                int64
    policy_annual_premium          float64
    umbrella_limit                   int64
    insured_sex                     object
    insured_education_level         object
    insured_occupation              object
    insured_hobbies                 object
    insured_relationship            object
    capital-gains                    int64
    capital-loss                     int64
    incident_type                   object
    collision_type                  object
    incident_severity               object
    authorities_contacted           object
    incident_state                  object
    incident_hour_of_the_day         int64
    number_of_vehicles_involved      int64
    property_damage                 object
    bodily_injuries                  int64
    witnesses                        int64
    police_report_available         object
    total_claim_amount               int64
    injury_claim                     int64
    property_claim                   int64
    vehicle_claim                    int64
    auto_make                       object
    auto_model                      object
    auto_year                        int64
    fraud_reported                  object
    dtype: object




```python
# Choosing to pickle here since it will save our dtypes
import pickle
path = r'C:\Users\sands\OneDrive\Desktop\MSDS_DATA_PRACTICUM\Data\Modeling'
df.to_pickle(path + '\clean_data.pkl')


# We are also storing the column names here for later
cols = list(df.columns)

with open(path + '\original_columns.pkl', 'wb') as file:
    pickle.dump(cols, file)
```

## The data is fairly clean at this point. We will move into feature engineering in the next notebook
