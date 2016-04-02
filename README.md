# PrudentialLifeInsurance

DATA SCIENCE PROJECT


Kaggle Competition: Prudential Life Insurance Assessment
Website: https://www.kaggle.com/c/prudential-life-insurance-assessment
Fecha: Noviembre 2015 – Febrero 2016
	Autor: MSc. Oswaldo F. Domejean
Email: ofigue@gmail.com
Lugar: La Paz – BOLIVIA
Code: . . .


Business understanding

From the competition description link: https://www.kaggle.com/c/prudential-life-insurance-assessment

Prudential, one of the largest issuers of life insurance in the USA, It has a life insurance application process antiquated, customers provide extensive information to identify risk classification and eligibility, including scheduling medical exams, a process that takes an average of 30 days. Prudential wants to make it quicker and less labor intensive for new and existing customers to get a quote while maintaining privacy boundaries.

By developing a predictive model that accurately classifies risk using a more automated approach, you can greatly impact public perception of the industry. The results will help Prudential better understand the predictive power of the data points in the existing assessment, enabling us to significantly streamline the process.

Data 

In the competition site where data is described and downloaded: https://www.kaggle.com/c/prudential-life-insurance-assessment/data, there is a description of every one of the features from the training and testing dataset, important to mention that the features are encoded.

Data exploration 

Data exploration had been done beginning with the analysis of each one of the variables distribution both individually and in relation to the target variable called “Responde”, then the analysis went by analyzing two and three variables and also in relation with the target. Some graphics had been done with a lot of variable combinations. 


It had been found that there is neither duplicates rows nor constant variables. It had been identified that there are some variables very low or high variations, however those variables had been kept because they could be predictive together with other variables.

In the case of NAs processing, it had been decided to replace them with median, which at the model predicting stage it incremented the accuracy. There had been an analysis of the correlation between variables, an element that came up was that only when the variables with NAs had been changed with the mean, it had been found that around eight very correlated variables prone to be eliminated.

It had also been done a correlation analysis between categorical variables and in relation with the target variable, for that it had been used the Chi-squared statistic. After identifying the set of variables to use, the target variable had been changed to factor with eight levels (i.e. 1 -8), but the result predictions with GBM and XGBOOST were as low as fliping a coin, something that drew attention.

Then in the Kaggle competition Forum people began to say that the target variable represent the concept of risk and that it is an ordinal variable, it meant that it is better to keep it numerical because the variable order is relevant, that is what it had been done. One consideration with the used metric i.e. Quadratic Weighted Kappa, the penalty level when the prediction differs from the actual value is greater than using other metrics, therefore it make sense that the target variable were continuous.

An interesting element that came up was the fact that the result of any of the predictions using the target variable as continuous gave an numerical result in the predictions varying between, for example, -1 to 9, and processing the result using cuts that convert to a discrete variable between 1 to 8 gave a very good predicted result.


Feature engineering

The feature engineering process began with getting rid of highly correlated variables that were removed. The concept of analysis and creation of new variables came up, in all cases, on the basis of a natural grouping of these variables like Employment or Medical History, etc.

A new variable with the multiplication of BMI and Age was created which proved to be highly predictive. Another variable that proved to be predictive was the row-wise sum of the variables Medical_Keyword_1-48, which are kind of dummy variables. With these variables it had been calculated the standard deviation which also proved to be very predictive, but in the case of the calculation of the mean didn’t prove to be predictive.

There was a trial and error in the process of creating new variables, for example, the row-wise mean of the variables related to employment and Insurance proved to be very predictive.

In this case a process related to the process of transforming Product_Info_2 to dummy variables did not work.

There had been created a lot of other variables using mean, standard deviation, median, etc., which did not prove to be relevant variables for Random forest and GBM 


Models and Evaluation

It had been used XGBoost with the mlR package, which proved to be very good at the time of the predictions, but there was a very hard work identifying right parameters.

It had been also used the lm and glm which did not work in the expected way. Then it had been used an ensembling of those three mentioned models, but because of the fact that mlR model was very powerful did not work using the other two weak models. 

What happened was that mlR XGBoost model was very powerful, in terms of predictive power, so it was very far from lm or glm models that is why the ensembling did not work as expected because the power of ensembling is precisely the combination of weak models, which was not the case in this competition.


Conclusion

The highlight of this competition was that the use of ML models with the dataset considering a number of variables originally of factor type, which did not prove to get higher level of accuracy, but when those variables were transformed to ordinal numerical which made a big difference. The use of linear models also drew attention because the predicted values had to be adjusted by cuts in the discrete range of values 1 to 8.


