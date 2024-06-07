# Bank Marketing Campaign Analysis

## Project 4 - University of Minnesota - Data Visualization and Analytics Bootcamp

### Contributors:
    Aliyu Muraina
    David Kogge
    Eriel Kadambi
    Indu Bandi

## Project Overview

The Bank Marketing Campaign Analysis project aims to analyze the effectiveness of a bank marketing campaign using classification models. The goal is to analyze and predict the customer responses to a bank's marketing campaigns and help the bank to optimize marketing strategies, improve customer targeting, and enhance campaign effectiveness based on these insights.

## DataSet Overview

The [bank marketing campaign dataset](https://archive.ics.uci.edu/dataset/222/bank+marketing) used in this project is obtained from UCI Machine Learning Repository, The dataset downloaded from the website has four datasets:
There are four datasets: 
1) bank-additional-full.csv - with all examples (41188) and 20 inputs, ordered by date (from May 2008 to November 2010), very close to the data analyzed in [Moro et al., 2014]
2) bank-additional.csv  - with 10% of the examples (4119), randomly selected from 1), and 20 inputs.
3) bank-full.csv - with all examples and 17 inputs, ordered by date (older version of this dataset with less inputs). 
4) bank.csv - with 10% of the examples and 17 inputs, randomly selected from 3 (older version of this dataset with less inputs). 

This project is modelled using the [bank-additional-full.csv](Resources/bank-additional-full.csv) file from the Resources folder and has 41,188 records with the following features:

### Bank Client Data:
        age: Age of the client
        job: Type of job
        marital: Marital status
        education: Education level
        default credit: Has credit in default?
        housing: Has housing loan?
        loan: Has personal loan?
### Contact Data:
        contact: Contact communication type
        day_of_week: Last contact day of the week
        month: Last contact month of year
        duration: last contact duration, in seconds
### Campaign Data:
        campaign: Number of contacts performed during this campaign and for this client
        pdays: Number of days that passed by after the client was last contacted from a previous campaign
        previous: Number of contacts performed before this campaign for this client
        poutcome: Outcome of the previous marketing campaign
### Economic Indicators:
        emp.var.rate: Employment variation rate (quarterly)
        cons.price.idx: Consumer price index (monthly)
        cons.conf.idx: Consumer confidence index (monthly)
        euribor3m: 3-month Euribor rate
        nr.employed: Number of employees
### Target Variable:
        y: Has the client subscribed to a term deposit?


## Data Preprocessing

## Data Visualization

## Model Building and Analysis
The first Tensorflow Sequential model was created using the Relu activation and 2 layers with 5 neurons each that provided the baseline accuracy of 91.2%.  

<img width="536" alt="bank_marketing_results" src="https://github.com/DKogge/project4/assets/152900988/5ab86f45-3204-4a34-9833-1b0602701f19">

#### *Please see the notebook located in the Data folder.

## Model Optimizations
A Keras Tuner auto optimization model was run to see if a more optimal model could be obtained.  The options for the model were Relu Tanh and Sigmoid for the activations with the option of up to 6 layers and up to 10 neurons per layer.  The result was a Sigmoid activation with 5 layers.  When the testing data was run the accuracy did improve but only slightly to 91.3%

<img width="542" alt="auto_opt_result" src="https://github.com/DKogge/project4/assets/152900988/0bd8b635-f8df-4d23-80f9-e2b18d7312e2">
 
We then went back to the features and removed the 4 columns of data that related to the economic indicators and reran the Tensorflow Sequential model with the Relu activation and 2 layers of 5 neurons.  This version improved the model to 91.5%.

<img width="514" alt="dropped_columns_results" src="https://github.com/DKogge/project4/assets/152900988/e4b22017-c430-4f23-8674-8c9492ab7f17">
 
We also tried a Random Forest model and the results of that were also 91% accuracy.

<img width="404" alt="random_forest_results" src="https://github.com/DKogge/project4/assets/152900988/8eaa72dd-57fd-4ea3-8a5b-282aafcc91fd">

 
#### *Please see the model_performace_log.xlsx for the full details and Optimization folder for the corresponding notebooks.

## Limitations and Next Steps
Ran into issues with the max processing limit in the free version of Colab, several model runs had the connection broken 4+ hours into the run. Would recommend the paid version and more resources dedicated to future model research.

Noticed an imbalance in the testing dataset with a higher number of non-responders (9124) compared to responders (1173) in random forest classification model.


## Conclusion

The machine learning models we generated were able to predict results with 91% accuracy.  While not perfect, we felt this was a excellent tool for this bank to use for their future marketing campaigns.

## Sources and References

1. Dataset Source: https://archive.ics.uci.edu/dataset/222/bank+marketing
2. Keras Tuner - https://www.tensorflow.org/tutorials/keras/keras_tuner
3. Google Colab - https://research.google.com/colaboratory/faq.html

