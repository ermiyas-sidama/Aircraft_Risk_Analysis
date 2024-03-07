# Aviation Risk Analysis Project
## Project Overview
In the US court systems, the average compensation for a life lost in a general aviation accident is $5.2 million dollars, the highest in the world!1
This project presents analysis of past aviation accidents based on how the aircraft was built. Our team reviews and processes the data to generate insights for Jelly Co. and ultimately provides airplane purchasing reccomendations.
1Article written by Healy-Pratt and Hanna in 2021 ![image](https://storage.googleapis.com/mcp_acc_236blog/uploads/2014/11/018067-vroeg-II1.jpg)
Photo by Andres Bolkenbaas on
## Business Problem
Jelly Co. is expanding it's business to new industries. They asked our team to look into the data for airplane accidents1 within the US in the last twenty-odd years. The company wants to know:

```
  1.Which airplane feature helps assess the lowest possible risk to the company?
  2.Which airplane manufacturer should be purchased and operated for a commercial enterprise?
  3.Which airplane manufacturer should be purchased and operated for a private enterprise?
```
Here we are using the definition of accident: "an occurrence associated with the operation of an aircraft which takes place between the time any person boards the aircraft with the intention of flight and all such persons have disembarked, AND in which any person suffers death or serious injury or in which the aircraft receives substantial damage"

## Data Understanding
For this project a dataset was taken from the National Transportation Safety Board that includes:

```
  1.Aviation accident data from 1962 to 2023
  2.Civil aviation accidents
  3.Selected incidents in the United States and international waters
```
## Data Preparation
The dataset contains 90348 records and 31 columns. Let's explore the dataset.
  ```python
## Import necessary python libraries

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline 

## Read the dataset using pandas library

df = pd.read_csv("data/Aviation_Data.csv", low_memory=False)

## Display information for the first 5 events

pd.set_option('display.max_columns', None)

df.head()
```
## Data Cleaning
Overall steps for this section:
```
  1.Checking for duplicates and dropping them if there are
  2.Filter the raw data
```
Checking for dupliactes
  ```python
## Print the number of duplicates in the dataset

print(df.duplicated().sum())
```
 ```python
## Drop the number of duplicates in the dataset

unique_df = df.drop_duplicates(ignore_index=False)


## Verify duplicates were dropped by printing the number of duplicates in the dataset

print(unique_df.duplicated().sum())
```
Filter out the rows where the values in the Aircraft.Category and Purpose.of.flight columns are not in the specified lists Aircraft_categories and Flight_purpose.

Justifications for filtering raw data:

  * Jelly Co. company is interested in Accidents over Incidents because Incidents is concerned with the operation of the aircraft whereas Accidents is concerned with the operation of the aircraft as well as the safety of the passengers as defined by the Federal Aviation 
  * Administration and the National Transportation Safety Board.
  * Our company is interested in flights within the United States.
  * Our company is interested in the data after the new safety regulations were set in place by TSA in November 2001.
  * Our company is interested in purchasing only airplanes.
  * Our company is interested in Purpose of flight data that is related to commercial and private airplanes.
 ```python
## Filter dataset for Investigation Type, Country, Event Date, Aircraft category, and Purpose of flight


Aircraft_categories = ['Helicopter', 'Glider', 'Balloon', 'Gyrocraft', 'Weight-Shift', 'Powered Parachute', 
                       'Ultralight', 'WSFT', 'Powered-Lift', 'Blimp', 'ULTR', 'Rocket']
Flight_purpose = ['Instructional', 'Aerial Application', 'Positioning', 'Ferry', 'Aerial Observation', 
                  'Flight Test', 'Skydiving', 'External Load', 'Banner Tow', 'Air Race show', 'Air Race/show', 
                  'Glider Tow', 'Firefighting', 'Air Drop', 'ASHO']

unique_df = unique_df.loc[(unique_df['Investigation.Type'] == 'Accident') 
                    & (unique_df['Country'] == 'United States')
                    & (unique_df['Event.Date'] > '2001-11-01')
                    & (unique_df['Aircraft.Category'] != (unique_df['Aircraft.Category'].isin(Aircraft_categories)))
                    & (unique_df['Purpose.of.flight'] != (unique_df['Purpose.of.flight'].isin(Flight_purpose)))
                    ]

```
 ```python
## Look at columns relevant to business problem and clean if necessary

unique_df['Make'].value_counts()
```
Remove missing values from the Make column
 ```python
unique_df = unique_df.dropna(subset=['Make'])
```
Further clean this data by standardizing the capitalization of the string objects in each element of the Make column.
 ```python
unique_df['Make'] = unique_df['Make'].str.title()
unique_df['Make'].value_counts()
```
 ```python
## Continue to clean data in Make Column

unique_df['Make'].replace(to_replace = ['Saab-Scania', 'Saab'], value = 'Saab-Scania Ab (Saab)', inplace = True)
unique_df['Make'].replace(to_replace = ['Embraer'], value = 'Embraer S A', inplace = True)
unique_df['Make'].replace(to_replace = ['Airbus'], value = 'Airbus Industrie', inplace = True)
unique_df['Make'].replace(to_replace = ['Bombardier', 'Bombardier, Inc.'], value = 'Bombardier Inc', inplace = True)
unique_df['Make'].replace(to_replace = ['Mcdonnell Douglas', 'Douglas', 'Mcdonnell Douglas Corporation'], value = 'Mcdonnell Douglas Aircraft Co', inplace = True)
unique_df['Make'].replace(to_replace = ['Beechcraft'], value = 'Beech', inplace = True)
unique_df['Make'].replace(to_replace = ['Gulfstream'], value = 'Gulfstream Aerospace', inplace = True)
unique_df['Make'].replace(to_replace = ['Embraer-Empresa Brasileira De'], value = 'Embraer S A', inplace = True)
unique_df['Purpose.of.flight'].replace(to_replace = ['PUBS'], value = 'Public Aircraft - State', inplace = True)
unique_df['Purpose.of.flight'].replace(to_replace = ['PUBL'], value = 'Public Aircraft - Local', inplace = True)
```
 ```python
## Choose which columns to keep in order to answer the business question

unique_df.info()
```
Give reasoning for dropping columns
 ```python
## Drop the columns that aren't relevant to the business question

dropped_columns = ['Injury.Severity', 'Registration.Number', 'Amateur.Built', 'FAR.Description', 
                   'Schedule', 'Air.carrier', 'Weather.Condition', 'Report.Status', 'Publication.Date', 
                   'Total.Fatal.Injuries', 'Total.Serious.Injuries', 'Total.Minor.Injuries', 'Total.Uninjured', 
                   'Latitude', 'Longitude', 'Airport.Code', 'Airport.Name']

for column in dropped_columns:
    unique_df = unique_df.drop(column, axis=1)
    
unique_df.head()
```
## Data Visualization
Create visuals that compare:
  * The number of engines to the total accident count
  * The engine type to the total accident count
  * The broad phase of flight to the total accident count
Reiterate title aka takeaway
 ```python
unique_df['Number.of.Engines'].value_counts().sort_index()

## Plotting data

fig, ax = plt.subplots(figsize=(10,5))

x = unique_df['Number.of.Engines'].value_counts().index
y = unique_df['Number.of.Engines'].value_counts().values

ax.bar(x,y)
ax.set_title('Airplanes with a Minimum of 2 Engines had the Least Amount of Accidents')
ax.set_xlabel('Number of Engines')
ax.set_ylabel('Total Accident Count');
```
Reiterate title aka takeaway
 ```python
fig, ax = plt.subplots(figsize=(15,5))
x = unique_df['Engine.Type'].value_counts().index
y = unique_df['Engine.Type'].value_counts().values
ax.bar(x,y)
ax.set_title('Airplanes with the Reciprocating Type of Engine had the Most Amount of Accidents')
ax.set_xlabel('Engine Type')

ax.set_ylabel('Total Accident Count');
```
Reiterate title aka takeaway
 ```python
fig, ax = plt.subplots(figsize=(17,5))

x = unique_df['Broad.phase.of.flight'].value_counts().index
y = unique_df['Broad.phase.of.flight'].value_counts().values

ax.bar(x,y)
ax.set_title('The Most Accidents Occurred During the Landing Phase of Flight')
ax.set_xlabel('Broad Phase of Flight')
ax.set_ylabel('Total Accident Count');
```
## Data Analysis
### Commmercial Airlines
Analyze data for commcercial airplanes that have the least amount of accidents.

   * We chose 2.0 engines as per the data in the bar graph "Airplanes with a minimum of 3 engines had the least amount of accidents".

   * We focused on data from Boeing and Airbus because they are among the top 10 largest commercial aircraft manufacturers according to the article written by Rosita Mickeviciute in 2023.
 ```python
filtered_public_df = unique_df.loc[(unique_df['Number.of.Engines'] > 2.0)
           & (unique_df['Engine.Type'] != 'Reciprocating')
           & (unique_df['Purpose.of.flight'] != 'Personal')
           & (unique_df['Purpose.of.flight'] != 'Business')
           & (unique_df['Purpose.of.flight'] != 'Other Work Use')
           & (unique_df['Purpose.of.flight'] != 'Executive/corporate')
           & (unique_df['Broad.phase.of.flight'] != 'Landing')
           ]
```
 ```python
final_public_df = filtered_public_df.loc[(filtered_public_df['Make'] == 'Boeing')
                       |(filtered_public_df['Make'] == 'Airbus Industrie')
                        ]
```
 ```python
final_public_df[['Make', 'Number.of.Engines']].value_counts().head(50)
```
### Private Airlines

Analyze data for private airplanes that have the least amount of accidents.

   * Investigate if there is a correalation between number of engines and engine type

   * We chose 1.0 engine as per the data in the bar graph "Airplanes with the Reciprocating type of engine had the most amount of accidents" and the data from "Num_of_engines_and_Engine_type".

   * We focused on data from Beech, Cessna, Bombardier Inc, and Gulfstream Aerospace because they are among the top 10 largest private aircraft manufacturers according to the [article] https://www.aerotime.aero/articles/top-10-most-popular-private-jet-models-of-2023 written by Rosita Mickeviciute in 2023.
Make a comment about Beech being under another company.

Num_of_engines_and_Engine_type = unique_df[['Number.of.Engines', 'Engine.Type']].value_counts()
Num_of_engines_and_Engine_type
 ```python
## Airplanes that used Reciproating engine types and ran on single engines 
## had the most amount of accidents
```
 ```python
filtered_private_df = unique_df.loc[(unique_df['Number.of.Engines'] > 1.0)
           & (unique_df['Engine.Type'] != 'Reciprocating')
           & (unique_df['Purpose.of.flight'] != 'Public Aircraft')
           & (unique_df['Purpose.of.flight'] != 'Public Aircraft - Federal')
           & (unique_df['Purpose.of.flight'] != 'Public Aircraft - State')
           & (unique_df['Purpose.of.flight'] != 'Public Aircraft - Local')
           & (unique_df['Broad.phase.of.flight'] != 'Landing')
           ]
```
 ```python
final_private_df = filtered_private_df.loc[(filtered_private_df['Make'] == 'Cessna')
                       |(filtered_private_df['Make'] == 'Bombardier Inc')
                       |(filtered_private_df['Make'] == 'Gulfstream Aerospace')
                        ]

## bring back Beech
```
 ```python
final_private_df[['Make', 'Number.of.Engines']].value_counts()
```
## Reccomendations
### For Commercial Airplanes
```
  1. Make: Airbus
  2. Number of Engines: 4.0
```
### For Private Airplanes
```
  1. Make: Make: Gulfstream Aerospace
  2. Number of Engines: 2.0
```




















