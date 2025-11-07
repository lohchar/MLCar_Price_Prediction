# Car Price Prediction Project

## Overview
This repository contains a complete project on predicting car prices. The project follows a structured approach, including data cleaning, exploratory data analysis (EDA), and machine learning model training. The goal is to build and evaluate various regression models to accurately predict the selling price of cars based on their features.
## 1. Data Cleaning & Preprocessing
This stage involved preparing the raw data for analysis and modeling.   
- Imported libraries and loaded dataset to displayed first 5 rows
- Checked missing values per column and percentage where mileage, engine and seats had same count (221) and percentage (2.72). Max power had 215 missing values and 2.65 as a percentage.
- Handled missing values by dropping rows where the target variable (selling_price) was missing and filling in other missing values like mileage with the column's mean. Missing values in max power were filled with mode.
- Removed duplicate rows to ensure numerical columns were correctly formatted.
- Created a new feature for the car's age by subtracting the year from the current year.
- Identified diesel, petrol, LPG and CNG as unique values in fuel column.
- Identified there are no inconsistent values in transmission and standardized column.
- Identified possible outliers in the selling_price using a boxplot which stretch above 4 million, skewing the distribution
- Removed the outliers based on the price range below 10,000 or above 5, 000,000 to improve model performance.
- Standardized Column names to a consistent format of lowercase with underscores.
- Created a new feature, ‘price per kilometer’, to gain a new perspective on the data.
- Ensured the dataset index is properly reset after cleaning and saved the dataset as a new csv file
## 2. Exploratory Data Analysis (EDA)
This section involves data analysis to identify trends and relationships
- Calculated average selling price which is 501378.18
- Identified Diesel to be most common fuel type and LPG as least common
- Visualized price distribution with histogram, which show that most of the car prices are under 1 million. The number of car prices is reducing with the increase in prices forming tail to the right, making it skewed.
- Visualized relationship between car age and selling price using a scatter plot. It confirms that there is a negative relationship, because when car age increases, the selling price decreases.
- Grouped cars to compare average prices across different categories. Diesel had the highest average selling price (620448.48) while LPG had the lowest (200421.05)
- Visualized the relationship between number of cars and transmission type using a bar chart. From the plot, it is clear there more cars using manual transmission compare to those using automatic transmission.
- Identified ‘Maruti Alto 800 CNG LXI Optional’ as the car with the highest mileage in the dataset.
- Analyzed relationships such as the correlation between mileage and selling_price which was -0.12. It indicates the two features have a very weak and slightly negative relationship. The negative correlation shows that higher mileage, lowers the selling price but the effect is not strong.
- Visualized the correlations between all numeric columns where by a perfect negative correlation (-1.00) is identified between car_age and year. A strong positive correlation (0.69) was identified between selling price and max power, making cars with more power to have higher prices. 
- Identified manual cars are cheaper (444,299.1) compared to automatic cars (1,143,215).
- Identified the average selling price for each year of manufacture where 2018 had the highest (825749.55) and 2001 had the lowest (47220.33).
- Visualized trend for selling prices over the years which is downward and stabilizes from around 1982 to early 2000s. The price trend then moves upwards from early 2000s and was sharp increase from around 2010.
- Identified Maruti as the most frequent car brand in the dataset
- Identified diesel and manual as the most common combinations of fuel type and transmission.
## 3. Machine Learning
In this final phase, different regression models were trained to predict car prices.
- Checked the key assumptions of Linear Regression using visualizations to ensure the model's validity. 
- The 1st assumption I checked for was linearity using a scatter plot. From the scatterplot, we can observe that the selling price is reducing as the km driven increase. The plot does not show a clear linear relationship between price and km driven since the points are clustered more towards the left corner rather than a straight line. There are few points away from the main cluster point indicating very few outliers.
- Checked for other assumptions through regression model whereby created a linear regression model, predicted values and calculated the residuals. 
- Checked for Normality of Residuals using a histogram and KDE line that form curve that resembles a bell shape. It appears symmetrical since the highest frequency is at around 0 making both sides even. This indicates the assumption was largely met making the model suitable for the data.
- Checked for Homoscedasticity using a scatter plot and observed that the residuals are not constantly spread. The residuals become more scattered as the selling price increases. It indicates that the higher the predicted selling prices are, the more errors the model has.
- Created and trained a linear regression model to identify coefficient (-0.4366) and the intercept (193868.38). This indicates that km driven, max power and car age have a negative relationship with the selling price. The intercept indicates that 193868.38 is the predicted selling price when the independent variables are at 0 (new car).
- Evaluated the Linear Regression model using R² Score which was 0.6309 and Mean Squared Error (MSE) which was 66988901467.62. The R2 score indicate that the model only accounts for 63% of the factors influencing the selling price of cars and the remaining is for factors not included in the model.
- Created lasso regression and evaluated it using lasso MSE which is 66988901324.86. a smaller MSE indicates that lasso regression performed slightly better than linear regression.
- Applied Ridge Regression to compare its performance with both linear and lasso regressions. Its MSE of 66988893806.15 was the lowest compare to those of linear and lasso. It indicates that Ridge regression performed best due to high correlation of features like engine.
- Used cross-validation to evaluate Regression model where the R2 score of the 5 folds were 0.60765165, 0.63020466, 0.65238393, 0.61232064 and 0.62552924. These scores are relatively close indicating that the model is consistent in predicting the cars selling prices. The mean R2 score is 0.6256, which means the model can account for 62.55% of variance in the cars selling prices. Standard deviation of R2 scores was low, 0.0157, indicating the model is stable.
- Used GridSearchCV to find the best alpha value for Ridge Regression which is 0.01 and the best R2 score for the optimal alpha is 0.6256. The best alpha is low which indicates the Ridge model need little regularization as it is working well with the data.
- Tried polynomial regression on the dataset and it showed improvement where R2 score is 0.7859 and MSE 38849790844.21. The polynomial model can explain 78.6% of the variance in cars selling price which is highest compared to R2 scores of linear, lasso and Ridge regressions. It also has the lowest MSE compared to other models indicating that its predictions are closer to the actual selling prices.
## Conclusion
Polynomial Regression, emerged as the best performing model whereby it captured the non-linear relationships in the data and improved the R² score. This indicates that the relationship between the independent variables and the selling price is better described by a polynomial function rather than a linear one.
