# AG PROJECT (Project 3)
This repository shares the source data, examination approach, data analytics script and key findings of an examination of agricultural production and demographics data for the 100 counties in North Carolina.

The data supports an application that assists farm managers in their choice of crop (given rainfall, temperature and drought forecasts), and recommends suitable crop insurance programs.

## EXECUTIVE SUMMARY

### Project Objectives
To examine the impacts of weather events, particularly drought and flooding, on North Carolina agriculture and develop predictions about future impacts of climate change driven events to the sector and automate AI-generated recommendations for risk mitagation and crops resilience


### Summary Findings
* Model selection influenced model performance so each crop type had its own ML model type
* RAG and prompt engineering impacts LLM results; RAG augmentation enhances the value of the recommendations
* Influences beyond weather are important to crop performance; inclusion of additional non-weather features is likely to improve prediction results


## APPROACH

![Approach graphic](/Images/approach_image.png)

Modeling and analysis for this project was conducted in two AI major components parts:

1) _Crop Prediction ML_ - A Crop Prediction model was trained on historical North Carolina temperature, rainfall, crop yield and dollar value of crop per acre.  Several regression models were employed to find optimal quality of prediction for each commodity grown in North Carolina.  the crop prediction function employs trained models and associated quality metrics to return a new prediction and confidence level using forecast rainfall and temperature data.

1) _RAG-Enhanced ML_ - Local LLM model enhanced with USDA and NC Dept of Agriculture risk mangagement strategies, disaster assistance programs and farming best practices.


### 1 - CROP PREDICTION MODEL

* **Models:** iterated through several ML models, including Linear Regression, SVR, Decision Tree,
Random Forest and Gradient Boost, evaluating each model's performance by crop type using multiple model performance measures (i.e., mean square error, R2 score, explained variance score, mean absolute error) to select the best performing model by crop type. 

* **Datasets:** 
    * Crop Data: evaluated USDA crop production data for Barley, Bell Pepper, Corn, Cotton, Hay, Oat Peanut, Soybean, Squash, Sweet Potato, Tobacco and Wheat crops, considering acres planted, yield, production volume, and value per acre

    * Weather Data: evaluated 20 year's worth of NOAA Climate Center data (2000 to 2020) inclusive of seasonal and average temperatures, seasonal and avaerage precipitation and periods and degree of drought conditions.


* **Instructions:** To load and run models [INSTRUCTIONS] 
 
### 2 - RAG-ENHANCED LLM

* **Models** used to determine [ANALYSES included MODELS].
    * Local Large LAnguage Model: ...

    * Embeddings Model: ...


* **Datasets** explored in our modeling and analysis are [what and where]. 

* **Instructions:** To load and run models [INSTRUCTIONS]  



See the associated [presentation]('/UNC_AI_Bootcamp_Project_presented.pdf') file for addional context.

## ADDITIONAL REFERENCE CONTENT
### Python Libraries
Libaries used to conduct these analysis include 
* numpy
* pandas
* matplotlib
* sklearn
* statsmodels
* requests
* json
* os
* datetime

### Data Sources
* USDA National Agricultural Statistics Service (NASS)
* North Carolina Department of Agriculture
* National Integrated Drought Information System
* NOAA Climate Perdition Center


### Project Contributors
* Michael Szumski | [GitHub @mikeszumski](https://github.com/mikeszumski/)
* Jamie Bond | [GitHub @JBondAI](https://github.com/jbondAI/) 

## Other Acknowledgments
* Project instruction and requirements provided by [The Artificial Intelligence Boot Camp at UNC Charlotte](https://bootcamp.charlotte.edu/artificial-intelligence/)

