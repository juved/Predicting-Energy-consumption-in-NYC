## Predicting-Energy-consumption-in-NYC

Predicting Energy consumption in NYC
A Data-Driven Approach to Sustainable Urban Living

## Business Understanding:
This project revolves around the comprehensive analysis and prediction of energy consumption in New York City buildings, aligning closely with broader business motivations and objectives. The project aims to deliver valuable outcomes for a diverse range of stakeholders, including urban planners, environmentalists, the New York State Government, real estate investors, and policymakers.

Our primary business objectives are to offer useful insights that directly impact energy-efficient building practices, influence the creation of policies supporting sustainable living, and lead to cost savings for individuals and businesses. By utilizing advanced machine learning models to predict energy efficiency trends, our project aims to guide decisions that optimize resource usage, reduce environmental impact, and support economic development. Ultimately, we want to contribute to the overall resilience of the community.

The alignment of business motivations with model objectives ensures that the predictions and insights from our models have practical implications, supporting broader goals such as promoting sustainability, informing policy decisions, and creating a resilient and energy-efficient urban environment.

<img width="562" alt="Screenshot 2024-02-04 at 4 20 39 PM" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/cbc35a70-7297-4f56-b11d-8c33848cd938">

## This Project’s Technical Objectives:

In this project, our primary goal is to assess the ability to predict total energy consumption in buildings using only indirect factors, such as building size, occupancy, and other related parameters. By employing advanced machine learning models, we aim to understand how well these non-direct energy measures can serve as reliable predictors for overall energy usage. Initially, bigger buildings, taller buildings, and higher occupancy all show positive correlations. But the question arises: how well can we predict these factors?

Our secondary objective is to identify buildings that deviate significantly from our predictions. Buildings consuming more energy than anticipated may be considered inefficient, prompting the exploration of recommendations for energy reduction. On the other hand, identifying buildings that consume less energy than predicted provides an opportunity for further study. Analyzing these energy-efficient buildings can yield insights into practices that contribute to lower consumption, ultimately allowing us to develop targeted recommendations for broader energy efficiency improvements

## Data Understanding

This project leverages two key datasets: The NYC Building Energy for Local Law 84 (2023-Present), providing information on energy usage for buildings exceeding 50,000 square feet, including details such as year built, address, and occupancy. Additionally, the Primary Land Use Tax Lot Output (PLUTO™) data file offers comprehensive land use and geographic data, featuring columns like address, number of buildings, number of floors, etc. The selection of these datasets are based on their extensive information content, with PLUTO™ comprising over 800,000 rows and 92 columns, and the NYC dataset containing 30,000 rows and 254 columns. Directly sourced from official websites, these datasets encompass diverse features, including building energy consumption, water usage, land use, zoning, building characteristics, and geographic information. Our study stands out for its unique approach to integrating these datasets, potentially offering valuable insights into the field of urban energy efficiency analysis.

Exploring df1, it contains only 10 out of 92 columns with complete information. It has 28 columns of type object and 64 of type float or integer. Key columns of interest include borough, block, zipcode, address, building areas, land use, lot area, commercial area, residential area, building class, etc. A subset dataset, exp_df1, has been created for further exploration, revealing opportunities for data normalization such as converting strings to lowercase, particularly in the address column. Understanding the features and addressing the huge amount of zeros in columns like building area, commercial area, and residential area are essential steps.

df2 contains 233 columns with data type ‘object’ and 19 with data type float or integer. Key columns of interest include Property Id, Year Ending, NYC Borough, block and lot, City, Postal Code, Address 1, Primary Property Type, etc. Certain columns have missing values, and a value count has been conducted to explore each column.

<img width="575" alt="Screenshot 2024-02-04 at 7 43 14 PM" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/7bf19457-1ca4-4d14-98b1-0f9989ffa9e5">

Figure 1: 



## Data Engineering and Feature Selection:

The project required extensive data preparation, involving tasks such as cleaning, merging datasets, and addressing missing values. The df_a_m dataset, stored in CSV format, posed challenges due to its large size and diverse data types, with dimensions of (9723, 346). The 'property id' column was used to eliminate duplicates, and data cleaning included the removal of entries based on this column and the cleaning of 'postal codes' by selecting only the first 5 digits. Some entries in metric columns were erroneously considered as objects/characters, leading to their conversion to numeric values for clarity. Visual tools like bar charts, scatter plots, and heatmaps were employed to enhance data understanding. A subset of the dataset, using features not related directly to energy consumption with site energy us as target, was created.

Features: As we will see below, many features exhibited a skewed distribution, concentrating in low numbers with a "long tail" toward high values. To address this, we applied a Logarithm transformation to reduce skewness and normalize the dataset's distribution. This transformation specifically targeted columns identified as having this issue. Additionally, QQ plots were used to visually inspect whether the columns exhibited a normal distribution after the log transformation.

The steps mentioned above are crucial for solving the problem at hand. They ensure data integrity, reduce biases, and enhance interpretability in the context of result interpretation.


Figure 2: <img width="546" alt="Screenshot 2024-02-04 at 7 45 33 PM" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/c64a07d7-b48e-44a8-a62d-83a095c0b414">

## Meaningful Zeros
In our dataset, the concept of meaningful zeros plays a crucial role in understanding various Features. Meaningful zeros refer to instances where a data point or feature holds a value of zero, and this zero has significant implications for the interpretation of the data. For example, in the 'unitsres' column, a value of zero indicates that there are no residential units in the tax lot, providing valuable information about the absence of housing in those instances. Similarly, in the 'occupancy' column, a zero signifies that a certain percentage of Gross Floor Area (GFA) is unoccupied and non-operational, shedding light on the vacant areas. The 'easements' column, with a meaningful zero, suggests that a tax lot has no easements. Additionally, in the 'resarea' column, a zero value implies the absence of common residential areas in the building. Recognizing and analyzing these meaningful zeros enhance our understanding of the dataset, allowing for more accurate interpretations and informed decision-making in subsequent analyses.

## Modelling

I use site energy use (kbtu) as target. The analysis use Regression Analysis for predicting energy consumption. The models used for this project are: 
- Linear Regression
- Random Forest Regressor
- Gradient Descent XGboost


## Evaluation
<img width="493" alt="image" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/151a4435-94c4-4bcd-9756-34cf7160e40e">

The Random Forest Regressor model distinguishes itself as the top performer among the assessed models.
It archeive the lowest Mean Squared Error (MSE) of 0.0879, signifying superior predictive accuracy compared to alternative models. The R-squared value of 0.6166 indicates that the model explains a substantial portion of the variance in the target variable. The model's robustness is further affirmed by the mean MSE during cross-validation, registering at 0.2973. A consistent performance across different folds is demonstrated by the Cross-validated R-squared of 0.6152.

Therefore, the Random Forest Regressor emerges as the preferred choice for predicting energy consumption in this context. With the selected : 'lotarea,' 'bldgarea,' 'numfloors,' 'unitstotal,' 'assessland,' 'largest property use type - gross floor area (ft²),' 'year built,' 'construction status,' 'number of buildings,' 'occupancy,' 'property gfa - self-reported (ft²),' 'postal code,' 'landuse,' 'comarea,' 'resarea,' 'bldgdepth,' 'lottype,' 'bsmtcode,' 'builtfar,' 'residfar,' 'commfar,' 'facilfar' to make accurate predictions.

fig. 3:
<img width="641" alt="image" src="https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/1bb8b788-b1fd-458f-b02f-3ffd9455000c">


In fig.3, we display the actual versus predicted energy consumption. The red dots represent buildings with actual energy consumption at least 10% higher than predicted, suggesting a need for improvement in their energy infrastructure. The green dots represent buildings with actual energy consumption 10% lower than predicted, offering insights into potential energy efficiency enhancements. For the majority of buildings, the actual values fall within 10% of the logarithmically transformed predicted energy consumption values. Our model explains 61.5% of the variance in log energy consumption.


Building with highest overuse of energy compared to predictions fig.4 :
['820 boynton avenue']
![image](https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/18841328-729f-484b-b740-534c0a115d40)

Building the most significant underutilization of energy compared to predictions fig.5:
['528 west 162nd street']
![image](https://github.com/juved/Predicting-Energy-consumption-in-NYC/assets/34844790/1ebeb6ea-b957-43f5-b647-ab0973c3a7c7)

## Conclusion
Considering these achievements, the Random Forest Regressor is strongly recommended for predicting energy consumption in this context. Aligning with the broader business objectives and motivations outlined earlier, the model's exceptional performance offers valuable insights for promoting sustainability, informing policy decisions, and contributing to the overall resilience of the community. The features selected for this model, including 'lotarea,' 'bldgarea,' 'numfloors,' and others, have proven to be instrumental in achieving these significant outcomes.
## Next Steps:

- Incorporate More Direct Features: Expand the model's feature set by including more direct features related to energy consumption. Incorporating additional energy-related parameters could enhance the model's predictive power and provide deeper insights into energy efficiency trends.

- Develop Property-Specific Models: Explore the development of separate predictive models tailored to different types of property use, such as multi-family housing, hospitals, hotels, etc. Customizing models based on property types can better capture the nuanced factors influencing energy consumption in diverse building types.

- Investigate Deviating Buildings: Investigate buildings that exhibit significant deviations from predicted energy consumption levels. Identifying common parameters among these buildings can shed light on underlying factors contributing to energy inefficiency or efficiency. This analysis could inform targeted strategies for energy reduction and optimization.


## Datasets URL :
https://data.cityofnewyork.us/Environment/NYC-Building-Energy-and-Water-Data-Disclosure-for-/5zyy-y8am/about_data / https://www.nyc.gov/site/planning/data-maps/open-data/dwn-pluto-mappluto.page

## Repo Structure:
├── Data
├── Images
├── Notebooks
│   ├── 
│   ├── 
├── .gitignore
├── Final.ipynb
├── LICENSE
├── README.md
