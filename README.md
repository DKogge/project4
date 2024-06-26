# Bank Marketing Campaign Analysis

## Project 4 - University of Minnesota - Data Visualization and Analytics Bootcamp

### Contributors:
    Aliyu Muraina
    David Kogge
    Eriel Kabambi
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

![image](https://github.com/DKogge/project4/assets/153557880/be261b2d-d348-4bb0-b1ae-519079a3ac53)

1.	Retrieve the data from the UCI Machine Learning Repository.
2.	Upload the data to GitHub repository.
3.	Read the data from the CSV file on GitHub for cleaning and validation using Spark SQL as our primary tool for data extraction. 
4.	In the transformation process we:
    a.	Filled all missing values by 0
    b.	Rename the default column to default credit

5.  Convert the PySpark DataFrame to a Pandas DataFrame
6.  Save the DataFrame as a CSV for visualization
7.	Determine the number of unique values in each column
8.	Checking the value of different columns to replace it with Other in order to normalize our data frame.
9.	Convert our categorical data to numeric using ‘ pd.get_dummies’

## Data Visualization
In the visualization process using Tableau, a key column was renamed from 'Y', representing the target variable, to 'Subscribed'. One of the visualization ideas involved analyzing the relationship between customers' age distribution and job status in relation to their subscription status. The following insights were derived from the bar chart visualization:

### Job Status and Subscription:
##### Admin Employees: 
The bar chart clearly indicates that employees in administrative roles have a higher subscription rate compared to other job categories.
##### Unknown Job Status: 
Conversely, individuals with an unknown job status exhibit the lowest subscription rates.
####Age Distribution and Subscription:
The analysis reveals that the age group with the highest subscription rates falls between 30 to 40 years old, particularly among those employed in administrative positions.
These insights suggest that targeted marketing efforts focusing on individuals aged 30-40 in administrative roles could potentially enhance subscription rates.
![Screenshot 2024-06-09 at 20 18 19](https://github.com/DKogge/project4/assets/79320352/7190dd9c-f6db-496b-ac9e-b0b8d87674ff)
These insights suggest that targeted marketing efforts focusing on individuals aged 30-40 in administrative roles could potentially enhance subscription rates.

Another analysis focused on the subscription outcomes segmented by education level, specifically comparing those who subscribed to those who did not. The key findings from this analysis are:

#### Subscription Outcomes by Education:
##### University Degree Holders: The analysis shows that individuals with a university degree constitute the largest group among both subscribed and non-subscribed customers.
#### Implications:
This suggests that the majority of the campaign efforts have primarily reached out to individuals with university degrees.
<img width="1049" alt="Screenshot 2024-06-06 at 21 10 54" src="https://github.com/DKogge/project4/assets/79320352/cc33d91c-fa28-4c48-8139-bad3bc702194">

These findings indicate that while university graduates are the main target of the campaigns, further strategies may be needed to convert more of them from non-subscribed to subscribed customers.

To gain more concrete insights from the dataset, further analysis was performed on the Campaign Success Rate, Monthly Calls and Subscriptions, and Best Days to Call. The results of this analysis revealed the following key insights:
#### Campaign Success Rate:
The majority of subscriptions come from individuals who were called only once.
#### Best Days to Call:
The optimal days for calling, leading to the highest subscription rates, are Tuesdays vwith 11.8% and Thursdays with 12.1% .
#### Best Month for Calls:
The month of May emerged as the most successful month for securing subscriptions.
![Screenshot 2024-06-06 at 20 37 53](https://github.com/DKogge/project4/assets/79320352/57da2e34-2dcd-4aa4-8ef6-19a8932ab944)
These findings suggest that the most effective strategy for maximizing subscriptions involves targeting potential customers with a single call, particularly on Wednesdays and Thursdays, with a focus on the month of May.
#### https://public.tableau.com/views/Bank_Marketing_17176507235630/OutreachingEmployees?:language=en-GB&publish=yes&:sid=&:display_count=n&:origin=viz_share_link


## Model Building and Analysis
The first Tensorflow Sequential model (bank_marketing) was created using the Relu activation and 2 layers with 5 neurons each that provided the baseline accuracy of 91.2%.  

<img width="536" alt="bank_marketing_results" src="https://github.com/DKogge/project4/assets/152900988/5ab86f45-3204-4a34-9833-1b0602701f19">

#### *Please see the notebook located in the Data folder.

## Model Optimizations
A Keras Tuner auto optimization model was run to see if a more optimal model could be obtained.  The options for the model were Relu Tanh and Sigmoid for the activations with the option of up to 6 layers and up to 10 neurons per layer (bank_marketing_auto_opt1).  The result was a Sigmoid activation with 5 layers.  When the testing data was run the accuracy did improve but only slightly to 91.3%

<img width="542" alt="auto_opt_result" src="https://github.com/DKogge/project4/assets/152900988/0bd8b635-f8df-4d23-80f9-e2b18d7312e2">
 
We then went back to the features and removed the 4 columns of data that related to the economic indicators and reran the Tensorflow Sequential model with the Relu activation and 2 layers of 5 neurons (bank_marketing_dropped_end_columns).  This version improved the model to 91.5%.

<img width="514" alt="dropped_columns_results" src="https://github.com/DKogge/project4/assets/152900988/e4b22017-c430-4f23-8674-8c9492ab7f17">
 
We also tried a Random Forest model (bank_marketing_random_forest) and the results of that were also 91% accuracy.

<img width="404" alt="random_forest_results" src="https://github.com/DKogge/project4/assets/152900988/8eaa72dd-57fd-4ea3-8a5b-282aafcc91fd">

Several other optimizations were attempted, we ran a 2nd auto optimization with fewer resources (bank_marketing_auto_opt2), we edited the age column to bins by decade (age_bins), we grouped the unknown and illiterate education categories together as "other"(edu_optimize), we looked at only the top 5 professions moving all the rest to "other"(employed_2k) all of these models returned results below 91.5%.  The model that got the best results was using all the actual jobs and moving the unknown, student and unemployed groups into the "other" category (employed_only).  This gave a 91.6% return using the testing data.

<img width="536" alt="employed_only_results" src="https://github.com/DKogge/project4/assets/152900988/cd7452d1-418c-473e-8c94-3b0bc2de6186">

 
#### *Please see the model_performace_log.xlsx for the full details and Optimization folder for the corresponding notebooks. Snapshot shown below
![model_performace_log_snapshot](Images/Model_Optimizations_Summary.png)

## Limitations and Next Steps
Ran into issues with the max processing limit in the free version of Colab, several model runs had the connection broken 4+ hours into the run. Would recommend the paid version and more resources dedicated to future model research.

Noticed an imbalance in the testing dataset with a higher number of non-responders (9124) compared to responders (1173) in random forest classification model.


## Conclusion

The machine learning models we generated were able to predict results with 91% accuracy.  While not perfect, we felt this was a excellent tool for this bank to use for their future marketing campaigns.

## Sources and References

1. Dataset Source: https://archive.ics.uci.edu/dataset/222/bank+marketing
2. Keras Tuner - https://www.tensorflow.org/tutorials/keras/keras_tuner
3. Google Colab - https://research.google.com/colaboratory/faq.html

