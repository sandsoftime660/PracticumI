# PracticumI
This is an overview of my practicum I course project.

It contains several different notebooks to be run in order. First, a database was created using MySQL Workbench:

# Creating the database...


# This notebook will take our csv dataset, create a mysql table, and insert

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


