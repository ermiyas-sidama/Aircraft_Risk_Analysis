# Aviation Risk Analysis Project
## Project Overview
In the US court systems, the average compensation for a life lost in a general aviation accident is $5.2 million dollars, the highest in the world!1
This project presents analysis of past aviation accidents based on how the aircraft was built. Our team reviews and processes the data to generate insights for Jelly Co. and ultimately provides airplane purchasing reccomendations.
1Article written by Healy-Pratt and Hanna in 2021
https://storage.googleapis.com/mcp_acc_236blog/uploads/2014/11/018067-vroeg-II1.jpg
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
  2.filter
```
Checking for dupliactes
  ```python
## Print the number of duplicates in the dataset

print(df.duplicated().sum())
```
## Drop the number of duplicates in the dataset

unique_df = df.drop_duplicates(ignore_index=False)


## Verify duplicates were dropped by printing the number of duplicates in the dataset

print(unique_df.duplicated().sum())






