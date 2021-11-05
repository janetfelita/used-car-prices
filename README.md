![Untitled-1](https://user-images.githubusercontent.com/78501809/140493534-cf09a9e7-f323-4db3-9e06-4cac4c2d66b3.png)


# Used Car Prices Predictions with Linear Regression

* **Data**: [CarDekho's used car dataset](https://www.kaggle.com/saisaathvik/used-cars-dataset-from-cardekhocom)
* **Objective**: build a model to predict the resale value of used cars in India based on their specifications.
* **Method**: linear regression
* **Tool(s)**: R
* **Full preview**: [click here](https://rpubs.com/janetfelita/used_car_regression)

## Workflow
1. **Import dataset and libraries**: tidyverse, inspectdf, magicfor, ggpubr, GGally, ggplot2, MLmetrics, fastDummies, car, caret, vtreat, lmtest, pastecs.
2. **Check for duplicates and missing values:** no duplicates, ~50% of the total rows contains missing values for price.
3. **Handling missing values:** imputing missing values with the average price based on the car's name. Using `max_power`, and `engine` if the car's name isn't available.
4. **Removing outliers**: by looking at the descriptive statistics summary
5. **Removing highly correlated variables**: using `ggcorr()`
6. **Check for price distribution:** right-skewed, fixed by transforming the numbers to their natural log value to be distributed evenly.
7. **Splitting train and test data:** 80:20, variables turned into dummy variables.
8. **Build first model:** with all predictors. _Result_: 0.912 multiple R-squared and 0.9118 Adjusted R-squared with 55 predictors.
9. **Build second model:** with `designTreatmentsZ()`. _Results_: 0.863 R-squared and 0.8629 Adj. R-squared with 14 predictors.
10. **Build third model:** removing insignificant predictors from the second model. _Results_: 0.8629 R-squared and 0.8628 Adj. R-squared with 12 predictors.
11. **Prediction results:** compared between the first and third model. 
<p align="center"><img width="461" alt="Screenshot 2021-11-05 163235" src="https://user-images.githubusercontent.com/78501809/140489514-1fa1992b-83c4-4db2-a588-4932d6bd5647.png"></p>

12. **Regression assumptions**:
* Linearity: not linear. Model could predict better in the mid-range, but when the model is predicting higher values, the error is larger in the negative side since the model tends to under-predict the value.
*  Residuals normality: normally distributed.
*  Homoscedasticity: using `bptest()`, assumptions not fulfilled.
*  No-Multicollinearity: `fuel_type` Diesel and Petrol and `engine` has high VIF.
13. **Model improvement**: remove more outliers, remove fuel_type Diesel and `engine`.
<p align="center"><img width="524" alt="Screenshot 2021-11-05 164013" src="https://user-images.githubusercontent.com/78501809/140490671-97f72173-3619-4804-b345-4cdf3e0b424e.png"></p>

## Conclusion
* Improved model still doesn't fulfill the linearity and homoscesdasticity assumptions.
* In this dataset, the `selling_price` relies heavily on the brand of the model but there's no data for the model type. This model could do better with more data such as the type of the car because a car's resale value is seen more based on the brand and the type of the car because the same type of a car by different brands could have a different resale value.
* The `selling_price` is very skewed to the right. From tens of thousands of data, 75% of them are actually priced between INR 34,000 - 799,250. With the median value of 530,000 and maximum value of 39,500,000 is too huge of a gap and it couldn’t just be removed since it's 25% of the data.
* 50% of the data were actually missing values. Another method to impute those missing values should be tried to generate a better result.
