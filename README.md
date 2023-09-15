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
"Random Forest Regressor" modeli oluşturulur.
param_grid adlı bir sözlük oluşturulur, bu sözlük içinde modelin hiperparametrelerinin olası değerleri belirtilir. Bu değerler üzerinde deneme yapılacaktır.

⊿Grid Search:
</br>
GridSearchCV kullanılarak parametrelerin farklı kombinasyonları üzerinde deneme yapılır.
cv=5 ile 5 katlı çapraz doğrulama yapılır.
scoring='neg_mean_squared_error' ile hata karesinin negatifini en aza indirgeyerek skorlama yapılır.
En iyi parametreleri ve bu parametrelerle elde edilen en iyi RMSE skorunu yazdırır.

⊿Visualization of Parameter Combinations:
</br>
İlk olarak, "n_estimators" ve "max_depth" parametrelerinin RMSE skorlarını bir ısı haritasıyla görselleştirir.
İkinci olarak, "max_depth" ve "n_estimators" parametrelerinin RMSE skorlarını başka bir ısı haritasıyla görselleştirir.

⊿Visualization of the "max_features" Parameter:
</br>
"max_features" parametresinin farklı değerlerine göre elde edilen RMSE skorlarını çubuk grafiği ile görselleştirir.
Her çubuğun üstüne ilgili RMSE değeri yazdırır.

▶Model Evaluation

This piece of code calculates metrics such as MSE, MAE, and R-squared to evaluate the performance of the trained Random Forest Regressor model and prints the results.
</br>
These metrics are used to understand how well the model works.

⊿Predictions of the Model:
</br>
grid_search.best_estimator_ ile hiperparametre optimizasyonu sonucunda bulunan en iyi modeli kullanarak test verileri üzerinde tahminler yapılır.
Bu tahminler y_pred_rf değişkeninde saklanır.

⊿MSE (Mean Square Error) Calculation:
</br>
Gerçek değerlerle tahmin edilen değerler arasındaki karesel farkların ortalama değeri olan MSE hesaplanır.
Daha düşük MSE değeri, tahminlerin gerçek değerlere ne kadar yakın olduğunu gösterir.

⊿MAE (Mean Absolute Error) Calculation:
</br>
Gerçek değerlerle tahmin edilen değerler arasındaki mutlak farkların ortalama değeri olan MAE hesaplanır.
Daha düşük MAE değeri, tahminlerin gerçek değerlere ne kadar yakın olduğunu gösterir.

⊿R-square (Coefficient of Determination) Calculation:
</br>
Gerçek değerlerle tahmin edilen değerler arasındaki varyans oranını hesaplayan R-kare hesaplanır.
1'e yaklaşan R-kare değeri, tahmin modelinin gerçek verileri ne kadar iyi açıkladığını gösterir.
