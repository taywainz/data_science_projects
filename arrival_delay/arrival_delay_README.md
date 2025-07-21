# Arrival Delay Model
`python` `scikit-learn` `regression task`

## Introduction
This project focuses on creating a model to predict how delayed a flight may arrive. When traveling, typically the traveler
is more concerned how delayed their flight will arrive opposed to how delayed their flight will depart. The datasets used are
from [Kaggle's 2015 Flight Delays and Cancellation](https://www.kaggle.com/datasets/usdot/flight-delays), and this project
utilizes the IATA codes, airlines, distances, days of week, origin and destination airports. After testing was conducted, it was
quickly realized that these are not effective features in predicting arrival delays. A correlation matrix revealed which features
would improve this model's accuracy, and the results improved astronomically!

## Classes and Algorithms Used
To determine the arrival delay, the following `scikit-learn` classes and algorithms from were used:
* `train_test_split`
* `cross_val_score`
* `make_pipeline`
* `SimpleImputer`
* `StandardScaler`
* `OneHotEncoder`
* `ColumnTransformer`
* `LinearRegression`
* `mean_squared_error`
* `r2_score`
* `mean_absolute_error`

## Project Workflow
#### Step 1: Data Exporation
* Analyzed datasets and merged accordingly
* Handled null values within target attribute
#### Step 2: Separate and Split Data
* Isolated target attribute from selected features
* Separated categorical and numerical features
* Converted data types of categorical features
* Split data by allocating 80% towards training and 20% towards testing
#### Step 3: Preprocessing
* Created categorical and numerical pipelines
* Inserted pipelines within a column transformer
* Fit and transformed the training features to the column transformer
#### Step 4: Create and Train Model
* Instantiated a Linear Regression model
* Examined the RMSE and cross validation scores for the training data
#### Step 5: Fit and Test Model
* Fit model to training data
* Model predictions against transformed test features
* RMSE, R<sup>2</sup>, MAE

## Final Evaluations
The results from the linear regression model:
> ```python
> # Results during training
> Cross_val_scores: [0.01235849 0.01220675 0.01205523]
> RMSE: 39.05
>
> # Results during testing
> RMSE: 38.9
> R2: 0.012
> MAE: 21.08
> ```
These results were not ideal. To make a model that would accurately predict arrival delays, I realized I would have to use those "delay" columns that had information
a normal person would not have access to. To confirm what features I should use instead, I ran a **correlation matrix**. To no surprise, departure delay was the most important
feature followed by airline delay and late aircraft delay.</br>
</br>
I used these new, more important features from my correlation matrix and trained a linear regression model using them. The final results using the testing data is
shown below:
> ```python
> RMSE: 12.89
> R2: 0.89
> MAE: 9.06
> ```

## Conclusion
The results that were from the features selected using a correlation matrix were much better than those selected at a whim. The most significant improvement was evident
within the R<sup>2</sup> value, increasing from 1.2% to 89%!</br>
</br>
During my debugging process, I ran into a few errors. Those consisted of:
* Issues with column 'DAY_OF_WEEK'. I initially had this as a categorical feature, but when testing my model. I got an error since some categories within this column did not show up within the training set. Since this feature could really go either way, I decided to change it to a numeric datatype and included it within the numeric pipeline.
* Categorical features being different datatypes. This caused issues within the column transformer. I converted all of the categorical features to a string datatype.
</br>
I like to share areas I struggled in to hopefully save others time debugging if creating a similar model. I was also optimistic that I could select regular, well-known
information that the general public would know as my features. As shown above, those features performed poorly. Within my conclusion in my code, I quickly realized I
needed to conduct some feature engineering to select the best features instead. After all, the general public may not have access to this information, but the general
public also isn't creating machine learning models. :smile: 
