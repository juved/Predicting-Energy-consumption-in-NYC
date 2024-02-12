## Predicting-Energy-consumption-in-NYC

Predicting Energy consumption in NYC
A Data-Driven Approach to Sustainable Urban Living

## Business Understanding:
This initiative revolves around the comprehensive analysis and prediction of energy consumption in New York City buildings, aligning closely with broader business motivations and objectives. The project aims to deliver valuable outcomes for a diverse range of stakeholders, including urban planners, environmentalists, the New York State Government, real estate investors, and policymakers.

Our primary business objectives are to offer useful insights that directly impact energy-efficient building practices, influence the creation of policies supporting sustainable living, and lead to cost savings for individuals and businesses. By utilizing advanced machine learning models to predict energy efficiency trends, our project aims to guide decisions that optimize resource usage, reduce environmental impact, and support economic development. Ultimately, we want to contribute to the overall resilience of the community.

<img width="562" alt="Screenshot 2024-02-04 at 4 20 39 PM" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/cbc35a70-7297-4f56-b11d-8c33848cd938">

## This Project’s Technical Objectives:

In this project, our primary goal is to assess the ability to predict total energy consumption in buildings using only indirect factors, such as building size, occupancy, and other related parameters. By employing advanced machine learning models, we aim to understand how well these non-direct energy measures can serve as reliable predictors for overall energy usage. Initially, bigger buildings, taller buildings, and higher occupancy all show positive correlations. But the question arises: how well can we predict these factors?

Our secondary objective is to identify buildings that deviate significantly from our predictions. Buildings consuming more energy than anticipated may be considered inefficient, prompting the exploration of recommendations for energy reduction. On the other hand, identifying buildings that consume less energy than predicted provides an opportunity for further study. Analyzing these energy-efficient buildings can yield insights into practices that contribute to lower consumption, ultimately allowing us to develop targeted recommendations for broader energy efficiency improvements.


## Data Understanding

This project leverages two key datasets: The NYC Building Energy for Local Law 84 (2023-Present), providing information on energy usage for buildings exceeding 50,000 square feet, including details such as year built, address, and occupancy. Additionally, the Primary Land Use Tax Lot Output (PLUTO™) data file offers comprehensive land use and geographic data, featuring columns like address, number of buildings, number of floors, etc. The selection of these datasets are based on their extensive information content, with PLUTO™ comprising over 800,000 rows and 92 columns, and the NYC dataset containing 30,000 rows and 254 columns. Directly sourced from official websites, these datasets encompass diverse features, including building energy consumption, water usage, land use, zoning, building characteristics, and geographic information. Our study stands out for its unique approach to integrating these datasets, potentially offering valuable insights into the field of urban energy efficiency analysis.


## Data Preparation

<img width="575" alt="Screenshot 2024-02-04 at 7 43 14 PM" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/7bf19457-1ca4-4d14-98b1-0f9989ffa9e5">

Figure 1: 

The project required  extensive data preparation, including cleaning, merging datasets, and addressing missing values. The data, stored in CSV format, poses challenges such as large dataset size and diverse data types. I used visual tools like bar charts, scatter plots, and heatmaps to make the data easier to understand. Table merging: Each dataset was evaluated separately, involving a thorough understanding of the data, text and column normalization, and identification of key columns for merging. The 'Address' column was identified as a potential key. The address field in both datasets was standardized by removing characters like '-' and '/', and it was converted to lowercase. The datasets were then merged using this column, resulting in a merged dataset, df_a_m, with a shape of (9723, 346).

Data cleaning: Subsequently, duplicates are removed based on the 'property id' column, and the 'postal codes' column is cleaned by selecting only the first 5 digits. Some entries in metric columns were mistakenly considered as object/characters, even though they were clearly numeric. Therefore, we converted these numeric values to make them easier to understand and interpret.


## Data Engineering and Feature Selection:



Features: 
As seen in Figure 1, we noticed that many features had a skewed distribution, concentrating in low numbers with a "long tail" towards high values. To tackle this, we applied a Logarithm transformation to reduce skewness and normalize the dataset's distribution. This transformation specifically focused on columns we identified as having this issue. Additionally, we used QQ plots to visually inspect whether the columns exhibited a normal distribution after the log transformation.

The merged dataset encompasses numerous columns directly linked to energy consumption. In constructing our initial model, priority was given to columns providing information about building size, year built, neighbourhood, occupancy, etc.



Figure 2: <img width="546" alt="Screenshot 2024-02-04 at 7 45 33 PM" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/c64a07d7-b48e-44a8-a62d-83a095c0b414">

## Meaningful Zeros
In our dataset, the concept of meaningful zeros plays a crucial role in understanding various Features. Meaningful zeros refer to instances where a data point or feature holds a value of zero, and this zero has significant implications for the interpretation of the data. For example, in the 'unitsres' column, a value of zero indicates that there are no residential units in the tax lot, providing valuable information about the absence of housing in those instances. Similarly, in the 'occupancy' column, a zero signifies that a certain percentage of Gross Floor Area (GFA) is unoccupied and non-operational, shedding light on the vacant areas. The 'easements' column, with a meaningful zero, suggests that a tax lot has no easements. Additionally, in the 'resarea' column, a zero value implies the absence of common residential areas in the building. Recognizing and analyzing these meaningful zeros enhance our understanding of the dataset, allowing for more accurate interpretations and informed decision-making in subsequent analyses.

## Modelling

I use site energy use (kbtu) as target. The analysis use Regression Analysis for predicting energy consumption. The models used for this project are: 
Linear Regression
Random Forest Regressor
Decision Trees Regressor
Gradient Descent XGboost


## Evaluation

Based on the Random Forest Regressor MODEL SUMMARY, the mean squared error for the RF model is 0.0879, with an R-squared value of 0.6166. Additionally, the mean MSE during cross-validation is 0.2973, with a cross-validated R-squared of 0.6152. This analysis underscores the model's performance in predicting energy consumption, where the R-squared values indicate a reasonably good fit between the predicted and actual values. 
For this first baseline model for the selected features below, the Linear Regression was so far the best model with the highest cross-validation.

fig. 3:
<img width="645" alt="image" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/e15d087d-9ac2-4398-b954-d0e764d00413">

In fig.3, we display the actual versus predicted energy consumption. The red dots represent buildings with actual energy consumption at least 10% higher than predicted, suggesting a need for improvement in their energy infrastructure. The green dots represent buildings with actual energy consumption 10% lower than predicted, offering insights into potential energy efficiency enhancements. For the majority of buildings, the actual values fall within 10% of the logarithmically transformed predicted energy consumption values. Our model explains 61.5% of the variance in log energy consumption.


Building with highest overuse of energy compared to predictions fig.4 :
['820 boynton avenue']
![image](https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/18841328-729f-484b-b740-534c0a115d40)

Building the most significant underutilization of energy compared to predictions fig.5:
['528 west 162nd street']
![image](https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/1ebeb6ea-b957-43f5-b647-ab0973c3a7c7)

## Next Steps:

- Incorporate More Direct Features: Expand the model's feature set by including more direct features related to energy consumption. Incorporating additional energy-related parameters could enhance the model's predictive power and provide deeper insights into energy efficiency trends.

- Develop Property-Specific Models: Explore the development of separate predictive models tailored to different types of property use, such as multi-family housing, hospitals, hotels, etc. Customizing models based on property types can better capture the nuanced factors influencing energy consumption in diverse building types.

- Investigate Deviating Buildings: Investigate buildings that exhibit significant deviations from predicted energy consumption levels. Identifying common parameters among these buildings can shed light on underlying factors contributing to energy inefficiency or efficiency. This analysis could inform targeted strategies for energy reduction and optimization.



