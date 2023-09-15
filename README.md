# *Medical Cost Analysis*

The main goal of this project is to estimate the potential cost of health insurance for individuals using various factors.

▶Exploratory Data Analysis

In this section of the code, the data was analyzed and meaningful conclusions were drawn from the data.
</br>
Data visualization techniques were used whenever possible during the analysis.

⊿Dataset Import and First Look:
</br>
Health insurance data was read from a CSV file and assigned to a variable named data.
</br>
To preserve the data, the data was copied into a copy called df.
</br>
The first few lines of data were displayed with df.head().
</br>
Basic statistical information was examined with df.describe() to obtain a general idea about the data.

⊿Data Visualization:
</br>
Body Mass Index (BMI) distribution was visualized by drawing a histogram.
</br>
The relationship was tried to be understood by examining the health costs of "smokers" with a dot plot.
</br>
Visualize the relationship by comparing the number of "Region" and "Smokers" with a grouped bar chart.
</br>
The relationship between "Gender" and "BMI" was evaluated with a box plot.
</br>
Relationships such as "Age-BMI", "Child-BMI", "BMI-Cost" were visualized and examined with other graphs.

⊿Outlier Review:
</br>
Outliers of the “BMI” data were represented by a boxplot.
</br>
Calculations to detect outliers were performed using the IQR method.

▶Data Preprocessing

In this section of the code, various preprocessing steps were applied to organize the dataset and make it suitable for model training.
</br>
The processes in this section include data preparation steps such as converting the data into numerical format, coding categorical variables, and dividing the data into training-test sets.

⊿Label Encoding:
</br>
The label coding method was used to convert categorical data into numerical values ​​in the “sex” and “smoker” columns.
</br>
"sex" column: Coded as Female (0) and Male (1).
</br>
"Smoker" column: Coded as Non-Smoker (0) and Smoker (1).

⊿One-Hot Encoding:
</br>
Because the “Region” column is categorical, one-hot coding was used to code each region as a separate column.
</br>
With the "drop='first'" parameter, a region column is dropped because other columns already carry this information.
</br>
New hardcoded "region" columns: "region_1", "region_2", "region_3".

⊿Data Partitioning and Scaling:
</br>
The data were divided into dependent variables ("charges") and independent variables ("sex", "smoker", "age", "bmi", "children", "region_1", "region_2", "region_3").
</br>
The data was divided into training and testing sets (80% training, 20% testing).
</br>
Data were scaled by standardization. This made each feature equally effective.

⊿Visualizing Data Distribution:
</br>
The distribution of training and test data scaled with two separate histograms was compared.
</br>
The distribution of scaled training data is visualized in the first graph.
</br>
The distribution of scaled test data is visualized in the second graph.

▶Model Selection

This piece of code was used to create and evaluate different regression models.

⊿Creating Models:
</br>
We add different models and their names to the models list, which is a list.
</br>
Models: Linear Regression, Ridge Regression, Lasso Regression, Decision Tree and Random Forest Regression.

⊿Evaluation of Models with Cross Validation:
</br>
We evaluate the cross-validation results for each model with the help of a loop.
</br>
With the cross_val_predict function, the model generates predictions by cross-validating on the scaled training data.
</br>
We evaluate the performance of the models by calculating the root mean square error (RMSE) between the generated predictions and the actual values.
</br>
We save these results in a dictionary called cv_rmse_scores.

⊿Visualization of Performance:
</br>
We draw a bar graph to compare the cross-validation results of the created models.
</br>
In the chart, the names of the models are shown on the x-axis, and the RMSE values ​​are shown on the y-axis.

⊿Printing Model Performance Results:
</br>
We compare cross-validation results of all models by printing them.

⊿Choosing the Best Model:
</br>
We choose the model with the lowest RMSE value with the Min function.
</br>
We print the name of the best model and the lowest RMSE value of this model.

▶Hyperparameter Optimization

This piece of code performs hyperparameter optimization to determine the best hyperparameters for the Random Forest Regressor model and achieve better performance with these parameters.

⊿Determination of Model and Parameters:
</br>
The "Random Forest Regressor" model is created.
</br>
A dictionary named param_grid is created, in which the possible values ​​of the hyperparameters of the model are specified. Experiments will be made on these values.

⊿Grid Search:
</br>
Different combinations of parameters are experimented on using GridSearchCV.
</br>
5-fold cross validation is performed with cv=5.
</br>
Scoring is done by minimizing the negative of the error square with scoring='neg_mean_squared_error'.
</br>
Prints the best parameters and the best RMSE score obtained with those parameters.

⊿Visualization of Parameter Combinations:
</br>
First, it visualizes the RMSE scores of the “n_estimators” and “max_length” parameters with a heat map.
</br>
Secondly, it visualizes the RMSE scores of the "max_length" and "n_estimators" parameters with another heat map.

⊿Visualization of the "max_features" Parameter:
</br>
It visualizes the RMSE scores obtained according to different values ​​of the "max_features" parameter with a bar chart.
</br>
Prints the corresponding RMSE value above each bar.

▶Model Evaluation

This piece of code calculates metrics such as MSE, MAE, and R-squared to evaluate the performance of the trained Random Forest Regressor model and prints the results.
</br>
These metrics are used to understand how well the model works.

⊿Predictions of the Model:
</br>
With grid_search.best_estimator_, predictions are made based on test data using the best model found as a result of hyperparameter optimization.
</br>
These predictions are stored in the y_pred_rf variable.

⊿MSE (Mean Square Error) Calculation:
</br>
MSE, which is the average value of the squared differences between the actual values ​​and the predicted values, is calculated.
</br>
A lower MSE value indicates how close the estimates are to the actual values.

⊿MAE (Mean Absolute Error) Calculation:
</br>
MAE, which is the average value of the absolute differences between actual values ​​and predicted values, is calculated.
</br>
A lower MAE value indicates how close the predictions are to the actual values.

⊿R-square (Coefficient of Determination) Calculation:
</br>
R-squared is calculated, which calculates the ratio of variance between actual values ​​and predicted values.
</br>
An R-squared value approaching 1 indicates how well the prediction model explains the actual data.
