# AG PROJECT (Project 3)
This repository shares the code, source data, approach and key findings for an examination of weather conditions on the yield of agricultural crops in North Carolina and the design of a **Crop Planning and Protection Tool** that take in weather forecast information, predicts future crop yields and supplies advice to farmers on whether to plant the crop and how to mitgate financial risks.

## SUMMARY FINDINGS
Data evaluation and model development revealed the following:
* Prediction performance for each specific crop was influenced by model selection; each crop required a different ML model type to achieve best model accuracy scoring
* RAG and prompt engineering impacted the quality of the performance of the LLM-generated advice;  augmentating the LLM with agricultural materials from USDA and NC Department of Agriculture yielded better crop-specific advice and enhanced the value of mitgation recommendations
* Better crop performance predictions require additonal modeling features beyond weather 

See the associated [presentation]('/UNC_AI_Bootcamp_Project_presented.pdf') file for addional context.

## APPROACH

![Approach graphic](/Images/approach_image.png)

The project included four major components :

### 1 - User Interface
 We developed a Gradio interface to capture user inputs (county, crops and planting year) and display final recommenations from the Crop Planning and Protection Tool. (Section 3.4 of the [Ag Planning Tool code](ag_planning_tool.ipynb) also provdes and option to print the advice to a csv file, demonstrated in an early example [here](crop_advice.csv).)

### 2 - Crop Prediction Models
 To develop crop-specific performance predictions based on weather forecasts, we applied machine learning to trained several regression models on 20-years worth of North Carolina  avarage qand seasonal temperatures, avrage and seasonal precipitation, periods of severe, extreme and exceptional drought, crop-specific yields and the production value (dollar value of yield harvested) of each crop per acre. 

To select models that proveded the best model accuracy and peformance, we iterated through several ML models, including Linear Regression, SVR, Decision Tree, Random Forest and Gradient Boost, evaluating each model's performance by crop type using multiple model performance measures (i.e., mean square error, R2 score, explained variance score, mean absolute error) to select the best performing model by crop type (Barley, Bell Pepper, Corn, Cotton, Hay, Oat Peanut, Soybean, Squash, Sweet Potato, Tobacco and Wheat). 

(Trained Models, their results and the data used to train them are available in the [Resources](./Resources/) folder.)

### 3 - Decision Logic Model
For making determinations on actions farmers should take (i.e., plant, plant with caution or do not plant the selected crop), we developed a function that   .

(The code for the decision logic is included in section 2 of the [Ag Planning Tool code](ag_planning_tool.ipynb) also provdes and option to print the advice to a csv file, demonstrated in an early example [here](crop_advice.csv).)


### 4 - Recommendation Builder

## INSTRUCTIONS
We have provided several type of instructions for using this repository: Using the Crop Planning and Protection Tool, from running the code used to build the tool and running any of the crop prediction models that support the tool. 

### To Use the Tool
To use the tool ...

### To Run the Ag Planning Tool Code
To run the code ....

### To Run Models
To run any of the crop prediction models models located in the [Resources](./Resources/) folder ...


## ADDITIONAL REFERENCE CONTENT
### Dependencies

* For Local LLM Installation
    * Ollama _([dowload]('https://ollama.com/download/windows'))_ running 'phi3:mini' model _([documentation]('https://ollama.com/library/phi3'))_

* For RAG Development
    * LangChain - See [documentation]('https://python.langchain.com/v0.2/docs/introduction')
    
    ] [documentation] ('https://python.langchain.com/v0.2/docs/introduction/'). 
    * Unstructured - See [documentation]('https://docs.unstructured.io/welcome').
    * OpenAI - See  [documentation]('https://platform.openai.com/docs/guides/embeddings/'). 
    * ChromaDB - See [documentation]('https://docs.trychroma.com/getting-started').


### Libraries
bs4
 * BeautifulSoup

gradio
* gr

python
* ollama
* openai
* os
* nltk
* numpy
* nltk
* pandas
* pickle 
* re
* warnings
* time

langchain
* chains
* llms
* prompts

sklearn
* preprocessing
* linear_model
* svm
* tree
* ensemble


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

