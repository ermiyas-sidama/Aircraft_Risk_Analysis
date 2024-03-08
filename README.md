# Aviation Risk Analysis Project

## Introduction

In the US court systems, the average compensation for a life lost in a general aviation accident is $5.2 million dollars, the highest in the world!1
This project presents analysis of past aviation accidents based on how the aircraft was built. Our team reviews and processes the data to generate insights for Jelly Co. and ultimately provides airplane purchasing reccomendations.

1([Article](https://www.keystonelaw.com/keynotes/how-is-compensation-calculated-after-an-aviation-accident)) written by Healy-Pratt and Hanna in 2021 

![image](https://storage.googleapis.com/mcp_acc_236blog/uploads/2014/11/018067-vroeg-II1.jpg)

Photo by ([Andres Bolkenbaas](https://blog.klm.com/6-tips-for-creative-aviation-photography/))

## Business Problem
Jelly Co. is expanding it's business to new industries. They asked our team to look into the data for airplane accidents1 within the US in the last twenty-odd years. 
The company wants to know:
  - Which airplane feature helps assess the lowest possible risk to the company?
  - Which airplane manufacturer should be purchased and operated for a commercial enterprise?
  - Which airplane manufacturer should be purchased and operated for a private enterprise?

Here we are using the ([definition](https://www.faa.gov/faq/what-constitutes-post-accident-test-what-definition-accident#:~:text=The%20FAA%20and%20the%20National,any%20person%20suffers%20death%20or)) of accident: "an occurrence associated with the operation of an aircraft which takes place between the time any person boards the aircraft with the intention of flight and all such persons have disembarked, AND in which any person suffers death or serious injury or in which the aircraft receives substantial damage"

## Data and Resource Used
For this project a ([dataset](https://www.kaggle.com/datasets/khsamaha/aviation-accident-database-synopses)) was taken from the National Transportation Safety Board that includes:

  - Aviation accident data from 1962 to 2023
  - Civil aviation accidents
  - Selected incidents in the United States and international waters

In this project:
  - Python 3 is used to clean up data, to impute , to make analysis, and visualizations.
  - Tableau is used to make our dashboard.
## Methods
The method applied to solve our business problem is simply by following data science procedures. The first step is data cleaning.
Data cleaning includes:

  - Removing duplicates in this dataset, there were 1390 records duplicated.
  - Dropping some columns which are not relevant to our business problems.
  - Some imputation technique is also used.

After cleaning the data the master ([dataset](https://github.com/ermiyas-sidama/Aircraft_Risk_Analysis/blob/main/data/Aviation_Data_Cleaned.csv)) was created and used to make an analysis using Python and Tableau.
## Data Analysis Result
Our analysis shows that:

      - Aircraft engine number is correlated to total accident record.
      - Aircraft with a single engine has the highest accident record.
      - Aircraft with recprocating type of engine has the highest accident.
      - The most accidents occurred during the landing phase of flight.
## Airplanes with a minimum of 2 engines had the least amount of accidents

![image](https://github.com/ermiyas-sidama/Aircraft_Risk_Analysis/assets/160514617/4dcf86d3-0460-448b-912f-56d55f7f2e04)

## Airplanes with the recprocating type of engine had the most amount of accidents

![image](https://github.com/ermiyas-sidama/Aircraft_Risk_Analysis/assets/160514617/857f30f2-f43c-4e0f-9301-0a6dbf02bfd7)

## The most accidents occurred during the landing phase of flight

![image](https://github.com/ermiyas-sidama/Aircraft_Risk_Analysis/assets/160514617/90768e02-b564-459f-94de-6f1004228c62)


## Reccomendations
### For Commercial Airplanes
Aircraft with the least amount of accidents had 3 or more engines and their engine type is not reciprocating and had no landing accident record we set this as a minimum requirement. 
Based on this requirement we checked ([top aircraft manufacturers](https://www.aerotime.aero/articles/top-10-largest-aircraft-manufacturers-in-the-world)) (i.e., Boeing and Airbus) that essentially dominate the commercial airline industry and perform risk analysis and we 
foundout that Airbus industries has less amount of accident record. As a result we recommended the following model for commercial airlines.
  - Make: Airbus
  - Number of Engines: 4.0

### For Private Airplanes
We did the same analysis for private airlines and recommended the following model. Here are the ([top 10 private airplanes](https://www.aerotime.aero/articles/top-10-most-popular-private-jet-models-of-2023))

  - Make: Make: Gulfstream Aerospace
  - Number of Engines: 2.0
### Purchasing Recommendation For Both Airplanes:
  - Advanced landing assistance features

## Future Investigations

- Understand Jelly Co.’s aircraft selection requirements (e.g., passenger capacity and minimum mileage) to provide model recommendations
- Request financial data to conduct financial metric analysis to recommend the most cost effective airplane model 
- Follow up with Jelly for any additional analysis to support the successful launch of the commercial and private/business airlines

## For More Information
Please review our full analysis in jupyter notebook ([Aircraft_Purchasing_Decision_Analysis](https://github.com/ermiyas-sidama/Aircraft_Risk_Analysis/blob/main/Aircraft_Purchasing_Decision_Analysis.ipynb))
And also refer to our 
- ([Presentation](https://docs.google.com/presentation/d/1jL-KFUmxIiucP_slylAH3MVa7dCOrDrfDK0MjUmDY54/edit#slide=id.p)) 
- Tableau Dash board ([Tableau Private Airline](https://public.tableau.com/app/profile/sangwon.shim/viz/AircraftManufacturerSelectionDashboardforPrivateAirline/AircraftSelection-Private?publish=yes))
                   ([Tableau Commercial Airlines](https://public.tableau.com/app/profile/sangwon.shim/viz/AircraftManufacturerSelectionDashboardforCommercialAirline/AircraftSelection-Commercial?publish=yes))
  
## Repository Structure
```
|— README.md
|— Aircraft_Purchasing_Decision_Analysis.ipynb
|— .gitignore
|— Data
|— Presentation_slide.pdf
```




















