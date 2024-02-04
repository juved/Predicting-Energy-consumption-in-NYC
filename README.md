## Predicting-Energy-consumption-in-NYC

Predicting Energy consumption in NYC
A Data-Driven Approach to Sustainable Urban Living

## Business Understanding:
This project centers on the analysis and prediction of energy consumption in buildings across New York City, with a focus on driving positive outcomes for various stakeholders. The intended audience includes urban planners, environmentalists, the New York State Government, real estate investors, and policymakers. The goal is to provide insights that can influence energy-efficient building practices, shape policies supporting sustainable living, and contribute to cost savings for individuals and businesses. By predicting energy efficiency trends, the project aims to guide strategic decisions that not only optimize resource usage and reduce environmental impact but also support economic development and enhance the overall resilience of the community.

<img width="562" alt="Screenshot 2024-02-04 at 4 20 39 PM" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/cbc35a70-7297-4f56-b11d-8c33848cd938">


## Data Understanding

This project leverages two key datasets: The NYC Building Energy for Local Law 84 (2023-Present), providing information on energy usage for buildings exceeding 50,000 square feet, including details such as year built, address, and occupancy. Additionally, the Primary Land Use Tax Lot Output (PLUTO™) data file offers comprehensive land use and geographic data, featuring columns like address, number of buildings, number of floors, etc. The selection of these datasets are based on their extensive information content, with PLUTO™ comprising over 800,000 rows and 92 columns, and the NYC dataset containing 30,000 rows and 254 columns. Directly sourced from official websites, these datasets encompass diverse features, including building energy consumption, water usage, land use, zoning, building characteristics, and geographic information. Our study stands out for its unique approach to integrating these datasets, potentially offering valuable insights into the field of urban energy efficiency analysis.

<img width="575" alt="Screenshot 2024-02-04 at 7 43 14 PM" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/7bf19457-1ca4-4d14-98b1-0f9989ffa9e5">


Figure 1: 

## Data Preparation

The project required  extensive data preparation, including cleaning, merging datasets, and addressing missing values. The data, stored in CSV format, poses challenges such as large dataset size and diverse data types. I used visual tools like bar charts, scatter plots, and heatmaps to make the data easier to understand. Table merging: Each dataset was evaluated separately, involving a thorough understanding of the data, text and column normalization, and identification of key columns for merging. The 'Address' column was identified as a potential key. The address field in both datasets was standardized by removing characters like '-' and '/', and it was converted to lowercase. The datasets were then merged using this column, resulting in a merged dataset, df_a_m, with a shape of (9723, 346).

Data cleaning: Subsequently, duplicates are removed based on the 'property id' column, and the 'postal codes' column is cleaned by selecting only the first 5 digits. Some entries in metric columns were mistakenly considered as object/characters, even though they were clearly numeric. Therefore, we converted these numeric values to make them easier to understand and interpret.


## Data Engineering and Feature Selection:

Target column: we choose …. And the distribution 


Features: 
As seen in Figure 1 , we noticed that many features had a skewed distribution, concentrating in low numbers with a "long tail" towards high values. To tackle this, we applied a Logarithm transformation to reduce skewness and normalize the dataset's distribution. This transformation specifically focused on columns we identified as having this issue. Additionally, we used QQ plots to visually inspect whether the columns exhibited a normal distribution after the log transformation.

The merged dataset encompasses numerous columns directly linked to energy consumption. In constructing our initial model, priority was given to columns providing information about building size, year built, neighbourhood, occupancy, etc.



Figure 2: <img width="546" alt="Screenshot 2024-02-04 at 7 45 33 PM" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/c64a07d7-b48e-44a8-a62d-83a095c0b414">


## Modelling

I use site energy use (kbtu) as target. The analysis use Regression Analysis for predicting energy consumption. The model used for this project are: 
Linear Regression
Random Forest Regressor
Decision Trees Regressor
Gradient Descent XGboost


## Evaluation

<img width="546" alt="Screenshot 2024-02-04 at 7 46 19 PM" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/d98792f5-06b3-485b-8b20-82185f1cc003">

For this first baseline model for the selected features below, the Linear Regression was so far the best model with the highest cross validation. 
Features=  'borough_x', 'lotarea', 'bldgarea', 'numbldgs', 'numfloors','unitstotal','assessland',
                                 'postal code','largest property use type - gross floor area (ft²)',
                                  'year built', 'construction status', 'number of buildings', 'occupancy',
                                 'property gfa - self-reported (ft²)',  'water use (all water sources) (kgal)',
                                 'total (location-based) ghg emissions (metric tons co2e)'    ]
                                 
Best Model  === Linear Regression MODEL SUMMARY==
Mean Squared Error for Energy Efficiency model: 0.03378337559569033
R-Squared 0.968041818682259
Mean MSE:-cross val  2745772250922531.5
Model accuracy 0.9674890593752579

Test Set evaluation :

Mean Squared Error Test: 0.07912565150192472
R-squared Test:: 0.9344066990308929
model score: 0.9344066990308929


#Next Steps:
Investigating the futures 

