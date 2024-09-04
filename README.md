# King County House Price Predictions Using Regression Models
![Screenshot 2024-05-05 165544](https://github.com/DoreenMolly/House_Prices_Modeling/assets/155205164/75fa76de-6c1b-4ebf-a713-cdf68fc53953)


## 1.0 Business Understanding

### 1.1 Business Overview

The real estate industry thrives on a foundation of accurate property valuations and market analysis. In dynamic markets characterized by fierce competition, real estate agents require reliable tools to determine optimal listing prices, attract buyers quickly, and maximize profits for their sellers. The real estate market is highly competitive. Pricing homes accurately is essential for attracting buyers, maximizing profits for sellers, and ensuring timely sales. Traditionally, agents may rely heavily on recent comparable sales and their own experience, which can introduce subjectivity and potential for pricing errors. Additionally, limited availability of housing inventory, particularly in desirable neighborhoods or regions with high demand, can lead to increased buyer competition and inflated prices.

### 1.2 Problem Statement

The real estate market in the King County region faces challenges in accurately pricing homes, understanding the factors driving property values, and providing targeted renovation advice to homeowners. Traditional valuation methods may lack precision and fail to account for the diverse range of features influencing home prices. Consequently, real estate agents may struggle to offer accurate pricing estimates and relevant advice to clients, leading to suboptimal outcomes for both buyers and sellers.

### 1.3 Objectives

#### 1.3.1 General Objective

This project aims to develop data-driven models to support real estate agents in the King County region with accurate property pricing and targeted insights for client consultations.

#### 1.3.2 Specific Objectives

- To examine the features that have the most significant impact on home prices for effective marketing and negotiation strategies.

- To develop models using the King County Housing dataset to predict home prices based on various features.

     -  To create a regression model for house price prediction: Provide price predictions for potential listings based on key property characteristics.

     -  To create a classification model for price range prediction: Establish realistic price ranges for properties based on their features, enhancing agents' negotiation strategies.

- To provide actionable insights to real estate agents to assist them in pricing homes accurately, understanding factors influencing property values, and advising homeowners on targeted renovations




### 1.4 Challenges

- Traditionally, agents may rely heavily on recent comparable sales and their own experience, which can introduce subjectivity and potential for pricing errors.

- Inventory Shortages: Limited availability of housing inventory, particularly in desirable neighborhoods or regions with high demand, can lead to increased buyer competition and inflated prices. This shortage may also result in longer wait times for buyers to find suitable properties.

- Client Expectations: Meeting the diverse needs and preferences of clients, including first-time homebuyers, investors, and downsizing retirees, requires housing agents to have a deep understanding of market trends, property features, and financing options.



## 2.0 Data Overview & Methodology


- Dataset - King County House Sales dataset (kc_house_data.csv).

- Methodology – Quantitative Statistical Analysis and Predictive Modeling

### 2.1 Columns Used and Their Relevance

- id: Unique identifier for each house sale record. May not be directly used for modeling, but essential for data cleaning and reference.

- date: Date of the house sale. Useful for time-based analysis, filtering by timeframe, or creating features related to seasonality.

- price: The target variable – the outcome we aim to predict.

- bedrooms: Number of bedrooms, essential for accommodating buyer needs.

- bathrooms: Number of bathrooms, impacting convenience and value.

- sqft_living: Square footage of interior living space, a major price driver.

- sqft_lot: Square footage of the land parcel, affecting lot size and potential use.

- floors: Number of floors in the house, a possible indicator of layout and space.

- waterfront: Binary variable indicating whether the property has waterfront access, a highly desirable feature in the region.

- view: Rated view quality of the property, a potential value-adding aspect.

- condition: Overall condition of the house, likely affecting price and renovation needs.

- grade: Overall grade assigned to the housing unit based on King County grading system. Understanding the details of this grading system is crucial.

- sqft_above: Square footage of the house excluding the basement.

- sqft_basement: Square footage of the basement, if present.

- yr_built: Year the house was originally built, indicating age.

- yr_renovated: Year of the last renovation, if applicable. Influences condition and potential for further updates.

- zipcode: Geographic location, potentially related to market dynamics and neighborhood desirability.

- lat: Latitude coordinate, useful for mapping or finer-grained location analysis.

- long: Longitude coordinate, used in conjunction with latitude.

- sqft_living15: Living space of homes in the neighborhood (15 nearest neighbors). Can provide insight into local market comparisons.

- sqft_lot15: Lot size of homes in the neighborhood (15 nearest neighbors).



## 3.0 Data Preparation

Issue	Resolution

- Correct Data Types	Converted 'date' column to datetime format and 'sqft_basement' to float using the pd.to_datetime() and pd.to_numeric() functions with appropriate format and error handling.

Missing Values	
- Removed rows with missing values in specified columns and replaced missing or zero values in 'yr_renovated' with 'yr_built' values using boolean masking and the fillna() method.

Add New Columns	
- Added new columns including 'year_sold', 'month_sold', 'house_age', 'renovation_age', and 'season' by extracting year and month from 'date' column, calculating house age, years since renovation, and season based on month sold.

Drop Unnecessary Columns

- Dropped 'id', 'zipcode', and 'date' columns from the dataset using the drop() method with the appropriate axis parameter.

Check for Outliers

- Created box plots for specified numerical columns to visualize the distribution of data and identify outliers.

Identified outliers that represent legitimate data points and decided not to remove them to avoid introducing bias and maintain the model's generalizability.

![boxplots](https://github.com/DoreenMolly/House_Prices_Modeling/assets/155205164/68f92ac8-d6db-40d0-88f1-15bea05dfa21)


3.1 Exploratory Data Analysis – (Univariate Analysis)


![image](https://github.com/DoreenMolly/House_Prices_Modeling/assets/162351617/40db0298-9b39-449e-afba-ac21447eca61)


### 3.2 Exploratory Data Analysis – Price (IV) and Independent Variables (Bivariate Analysis)

![price vs all variables](https://github.com/DoreenMolly/House_Prices_Modeling/assets/155205164/4a86afc7-7e1f-49a2-8692-63979556fa4d)


- Positive correlations are observed between price and square footage, bedrooms, bathrooms, lot size, floors, and basement square footage, indicating that more extensive features tend to increase house prices. 

- While some scatter plots reveal transparent linear relationships between variables, others show no discernible pattern, indicating variations in correlation strength across different pairs of variables.

- Outliers are present in the data, representing data points significantly deviating from the overall trend, and clusters of points suggest subgroups within the data, highlighting the need for further analysis or modeling to understand underlying patterns.

### 3.3 Exploratory Data Analysis – Correlations between all Variables (Bivariate Analysis)


![C  MATRIX HEAT MAP](https://github.com/DoreenMolly/House_Prices_Modeling/assets/155205164/c29fde81-60fe-4575-8f9b-311705b7bb25)


- The correlation coefficients range from -1 to 1, where values near 1 indicate strong positive correlation, close to -1 indicate strong negative correlation, and around 0 suggest little to no correlation. 

- Sqft_living and price have the highest positive correlation (0.71), implying that the living space correlates with the price of the property. 

- The grade variable strongly correlates with both sqft_living and sqft_above, suggesting that higher-graded houses tend to have larger living spaces and more above-ground square footage.

## 3.4. Exploratory Data Analysis – Price Vs Longitude and Latitude (Multivariate Analysis)

- Spatial Clusters: Areas around 47.5, -122, 2 and 47.7, -122.1 exhibit clusters of higher-priced real estate (indicated by red dots). These locations likely correspond to desirable neighborhoods or central districts with elevated property values.

  ![lat and log vs prices heatmap](https://github.com/DoreenMolly/House_Prices_Modeling/assets/155205164/8fd4a21d-5090-4e11-9c0b-8634d6471f66)


- Geographical Variation: As latitude and longitude change, real estate prices fluctuate significantly. Understanding these spatial patterns can inform decisions related to property investment, urban planning, and market analysis.

## 4.0. Modeling Overview

- The data preprocessing phase involved feature engineering and encoding categorical variables. 

- Outliers were identified and removed based on scatterplot analysis during Exploratory Data Analysis.

-  Correlation matrix and Variance Inflation Factors were utilized to detect multicollinearity among features, followed by data transformation and scaling to normalize distributions and ensure equal contribution of all features during model training.

- Simple linear regression, multiple linear regression, random forest, and XGBoost were iteratively employed, with adjustments made to enhance model accuracy through various iterations.

Price Prediction

![price models](https://github.com/DoreenMolly/House_Prices_Modeling/assets/155205164/03a90e49-6835-4e00-bf86-47d553a6b38c)

Price Range Prediction

![price range](https://github.com/DoreenMolly/House_Prices_Modeling/assets/155205164/ded551b9-a6e0-46b5-b068-3323df0abe05)

## 5.0. Deployment
- XGBoost Price Prediction Model: Achieved exceptional performance in explaining the variability in the target variable, indicating superior predictive accuracy.

-  Efficient Model Evaluation: Demonstrated robustness through low error metrics, indicating minimal overfitting and strong generalization capability.
![xgboost](https://github.com/DoreenMolly/House_Prices_Modeling/assets/155205164/c2b72819-9cd7-45af-8204-8cabb50b4b8e)

-  XGBoost Price Range Prediction Model: Similarly excelled in predicting categorical price ranges, signifying robust classification performance.
![xgboost 2](https://github.com/DoreenMolly/House_Prices_Modeling/assets/155205164/256c6a79-b5f8-4c55-8e70-f0904db0a6bc)

- Visualizations: Observing scatterplots and histograms revealed a linear distribution of prices vs. predicted prices and random residuals, validating the models’ accuracy and reliability.


## 6.0. Conclusion
- Accurate Pricing Guidance: Achieved high model accuracy (R-squared > 0.800), empowering agents with precise pricing predictions for effective listing strategies and client communication.

-  Key Feature Identification: Identified 'sqft_living', 'grade', and 'view' as pivotal factors influencing home prices, enabling tailored marketing and negotiation strategies to highlight property attributes.

-  Enhanced Marketing Strategies: Equipped agents to craft compelling listing descriptions and showcase amenities that resonate with buyers, leveraging insights to attract premium prices.

-  Strategic Renovation Recommendations: Provided data-driven guidance on cost-effective renovations that maximize property value, empowering agents to advise clients on strategic improvements.

- Empowering Data-Driven Decisions: Overall, equipped real estate professionals with actionable insights into housing market dynamics, enabling data-driven decisions that optimize pricing strategies and enhance client satisfaction.

## 7.0. Recommendations
- Action	Responsibility	Evaluation

    - Foster Collaboration	Data science & real estate	Schedule bi-weekly meetings from May 1st, 2024. Assess impact on model refinement.

- Continuous Model Refinement	Data science & analytics
	- Implement monthly refinement sprints starting May 1st, 2024. Evaluate accuracy improvements.

- Invest in Advanced Analytics Tools	IT & executive leadership	

    - Allocate resources by July 1st, 2024. Measure adoption and efficiency gains.

## 8.0 Next Steps
- Dynamic Data Pipeline: 
Develop automated pipeline for real-time data retrieval & preprocessing.
Ensure models stay current for accurate insights.

- Interactive Consumer Dashboard: 
Design user-friendly dashboard for easy access to pricing predictions & market insights.
Enhance user engagement & decision-making with intuitive visualizations.

- Time-Sensitive Data Research: 
Conduct research for up-to-date housing data, including market trends & economic indicators. 
Anticipate future changes in the real estate landscape & adjust models accordingly for continued relevance & reliability.





