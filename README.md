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

The project included four major components:

### 1 - User Interface
We developed a Gradio interface to capture user inputs (county, crops and planting year) and display final recommenations from the Crop Planning and Protection Tool. (Section 3.4 of the [ag_planning_tool.ipynb](ag_planning_tool.ipynb) notebook also provdes and option to print the advice to a csv file, demonstrated in an early example [here](crop_advice.csv).)

### 2 - Crop Prediction Models
To develop crop-specific performance predictions based on weather forecasts, we applied machine learning to trained several regression models on 20-years worth of North Carolina  avarage qand seasonal temperatures, avrage and seasonal precipitation, periods of severe, extreme and exceptional drought, crop-specific yields and the production value (dollar value of yield harvested) of each crop per acre. 

To select models that proveded the best model accuracy and peformance, we iterated through several ML models, including Linear Regression, SVR, Decision Tree, Random Forest and Gradient Boost, evaluating each model's performance by crop type using multiple model performance measures (i.e., mean square error, R2 score, explained variance score, mean absolute error) to select the best performing model by crop type (Barley, Bell Peppers, Corn, Cotton, Hay, Oats, Peanuts, Soybeans, Squash, Sweet Potatoes, Tobacco and Wheat). 

(Trained models, their results and the data used to train them are available in the [Resources](./Resources/) folder.)

### 3 - Decision Logic Model
For making determinations on actions farmers should take (i.e., plant, plant with caution or do not plant the selected crop), we developed a function that compares the predicted performance of a selected crop with its respective 20-year average performance and then catagorizes the crop into one of three groups: 
* **Crops to plant** - _crops the tool will eventual recommend for planting given the weather forecast_
* **Crops to plant with caution** - _crops the tool may or may not recommend given the confidence of the prediction and the indivdual farmer's past performance compared to the state average yield_
* **Crops to avoid** - _crops the tool will recommend avoiding given the weather forecast_ \
\
The results are passed to an LLM to develop a justification narrative to support the decision.

### 4 - Recommendation Builder
We again use the LLM to generate a final recommendation. To do this, we enhanced the LLM with RAG capabilities by incorporating a document loading, content chunking and text embedding functions. We use a vectorstore (Chroma DB) for storing and retrieving the resulting embeddings.

We enhanced the LLM with a small sampling of [content](/rag_content/) aquired from USDA and NC Department of Agriculture related to agriculture risk management and distaster assistnace programs for crop producers. 

Once equiped with the addtional RAG content, we developed a recomendation generation function that will accept a dataframe variable containing the crop performance data, the decisions from the decision logic model and associated justifications. The recommendation builder then, using the RAG-enhanced LLM, generates a recommendation narrative along with additional considerations and mitagation information for each crop.

The final recommendations are passed back to the user interface as an output. (Section 3.4 for the [ag_planning_tool.ipynb](ag_planning_tool.ipynb) notebook also enables users to create a download of the recommendtation in CSV format. See an early example here: _[crop_advice](crop_advice.csv)_) 


## INSTRUCTIONS
We have provided instructions for running the code required to use to build and use the tool as well as standalone instructions for running any of the crop prediction models alone. 

### To Run the AG Planning Tool
To use the Ag Planning Tool, 

1) **Clone this repository to your local machine.** 

2) **Select your prefered LLM.**

    As currently configured, the [ag_planning_tool.ipynb](ag_planning_tool.ipynb) notebook  uses a local LLM to enable the Decision Logic and RAG functionality.  configured for using a locally run [Ollama](https://ollama.com/download) server loaded with Ollama's [phi3-mini](https://ollama.com/library/phi3) model. See linked documentation for install and loading instructinos. 
    
    _(Alternatively, users may use a hosted LLM, e.g., OpenAI, Claude, etc. See _Section 0.0 Initial Setup_ to change LLM selection.)_

    To load the Ollama phi3:mini LLM locally
    * Start the Ollama service by running the following command in a CLI: `ollama serve` 
    * To confirm the services is running, open a new terminal and run the following commnand: `ollama list`
    * Pull the latest update to the Ollama phi3 model by running the following:`ollama pull phi3:mini`
   
    To launch phi3:mini LLM
    * Start the Ollama service by running the following command in a CLI: `ollama serve`
    * Minimize the CLI window and allow Ollama service to run in the background while running the code
    * To launch the model, open a new terminal and run the following commnand: `ollama run phi3:mini`


3) **Run _[ag_planning_tool.ipynb](ag_planning_tool.ipynb)_ notebook**

**NOTE**: Documents included in the RAG functionality are locatated in the [rag_content](/rag_content/) folder. See _User Note_ in Section 3.1 to modify file path for source documentents.


### To Run Individual Crop Prediction Models
To run any of the crop prediction models models located in the [Resources](./Resources/) folder run the _[crop_prediction.ipynb](crop_prediction.ipynb)_ notebook.  Example inputs and model runs are provided within the notebook for reference.


## REFERENCES
### Dependencies
For Local LLM Installation
* Ollama _([download page](https://ollama.com/download/windows))_ running [phi3:mini model](https://ollama.com/library/phi3)_

For RAG Development
* LangChain - _See [documentation](https://python.langchain.com/v0.2/docs/introduction)_
* Unstructured - _See [documentation](https://docs.unstructured.io/welcome')_
* OpenAI - _See [documentation](https://platform.openai.com/docs/guides/embeddings)_
* ChromaDB - _See [documentation](https://docs.trychroma.com/getting-started)_

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
tqdm
* tqmd

### Data Providers
* USDA National Agricultural Statistics Service (NASS)
* North Carolina Department of Agriculture
* National Integrated Drought Information System
* NOAA Climate Perdition Center

## CONTRIBUTORS
* Michael Szumski | [GitHub @mikeszumski](https://github.com/mikeszumski/)
* Jamie Bond | [GitHub @JBondAI](https://github.com/jbondAI/) 

## ACKNOWLEGEMENTS
* Project instruction and requirements provided by [The Artificial Intelligence Boot Camp at UNC Charlotte](https://bootcamp.charlotte.edu/artificial-intelligence/)

