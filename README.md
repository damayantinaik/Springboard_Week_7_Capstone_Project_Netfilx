# Predicting Netflix Movies rating

## 1. Introduction

![](https://github.com/damayantinaik/Springboard_Week_7_Capstone_Project_Netfilx/blob/main/Report/Netflix_image.jpg)

Netflix, a subscription-based streaming service offers online streaming of films and television series. Starting in 1997 in USA,  now it makes the service available in most of the parts  of the world.   It is well known for its efficient recommendation engines providing users choice. The engines work behind the scenes and provide user’s choice related contents. The engines use Content-based filtering algorithm, collaborative filtering algorithm or both.

User rating(review) plays an important role in recommendation system. The users (called subscribers/viewers/member) rate movies based on various features of  a movie like genre, actor, director, title, language, country, duration, production company etc. History of users choice on different types of movies also helps to predict the rating of the unseen movie. 

## 2. Problem statement
Different predictive models will be developed to predict movies users’ rating and the best one will be selected based on the R2-score (co-efficient of determination) i.e how close the actual ratings are close to the predicted values. 

## 3. Data:
 
The data was collected from Kaggle and IMDB website. The links are 
* https://www.kaggle.com/shivamb/netflix-shows
* https://www.imdb.com/interfaces/


 ## 4. Data Cleaning/wrangling

Both datasets lists movies along with other features as columns. However, based on my requirement, I selected features those required for the predictive model building. To achieve this, I did data wrangling and the following were carried out: 
  
**Problem-1:** Kaggle dataset listed both movies and TV shows. 
**Solution:** I separated out the TV shows and only kept the movies for further data processing and model building.  

**Problem-2:** The IMDB dataset has listed titles and original titles both for movies. 
**Solution:** I dropped the ‘title’ column preserving only the ‘original_title’.

**Problem-3:** The duration time was including both numbers and unit(minute). 
**Solution:** Minute was deleted and only numerical value was kept.

**Problem-5:** IMDB and Kaggle dataset both contains some columns (date_published, metascore, usa_gross_income, worlwide_gross_income, budget, reviews_from_critics) which seems to be not useful for predictive model building. 
**Solution:** These columns were deleted from respective datasets.

**Problem-6:** After the conversion of the date_added column to date, the year was extracted. The output obtained was float instead of integer. 
**Solution:** To find out the reason, further investigation was carried out which shows that this is happening due to the presence of the null values in time stamp. To handle this, the null values were  filled with 0, then converted those to integer.

Finally rows with Null values are removed to prepare the dataset for EDA( Exploratory Data Analysis). 

The jupyter notebook for data import and data wrangling can be obtained at 
https://github.com/damayantinaik/Springboard_Week_7_Capstone_Project_Netfilx/blob/main/Capstone_Project_Netflix_Data_Wrangling_submission4.ipynb

## 5. Exploratory Data Analysis (EDA)
       
Detail investigations into each column of both datasets were carried out and following conclusions were drawn:
•	Both datasets show USA ranked Number One in movie production, while India ranked Second followed by United Kingdom in Third place.
 The jupyter notebook containing the EDA can be found at: https://github.com/damayantinaik/Springboard_Week_7_Capstone_Project_Netfilx/blob/main/Netflix_EDA_submission2.ipynb

## 6. Feature Engineering
As the IMDB dataset was very large as compared to Kaggle dataset, before feature engineering, I formed two new datasets out of it. Movies, which were found only in IMDB dataset, but not in Kaggle were separated out and used for building the predictive model, whereas movies common to both are used for testing the model. 
Feature engineering was carried out on both training and testing datasets as follows: 
1. Dummie variables for all the categorical columns: genre, language, actors, directors, writers, production company were created. For genre and language, the dummies for all the unique values were carried out, because it listed few varieties (<300),  however for rest of the columns, dummies for top 200 values in each column were obtained.
1. Standard scaling was carried out for numerical columns:  duration_min, votes, reviews from users to keep them in similar range.  As their distribution  follow normal distribution, standard scaling was preferred among all other types of scaling.
1. Few numerical columns had very high outliers, which were not mistakenly entered. However, as it might bias the ML (Machine Learning) model, hence, to avoid this, imputation was carried out, assigning  95th percentile value of the respective column to the outliers.
1. Finally, all the dummies columns were added to the respective main datasets and original categorical columns were dropped.

## 7. ML models
To predict the movies rating, different regression models: Simple Linear Regression, Lasso Regression, Ridge Regression, Random Forest Regressor, Gradient Boosting Regressor were developed. 
•	The Simple Linear regression model performance was poor, however it improved significantly when regularization was applied. Among Lasso and Ridge, the later one  performed better with r2_score (test set): 0.42. 
•	To have better performance, ensemble model Random Forest Regressor was developed. The highest r2_score obtained with this was 0.44. 
•	To obtain more higher model performance, Gradient Boosting Regressor was developed. The highest r2_score obtained with this was 0.507 and this was the best model among all the models.    
To improve the models’ performance, PCA (Principal Component Analysis) was applied on the data and models were trained again. However, though it helped Logistic Regression to improve its performance and run time, it couldn’t improve performance of both ensemble models. 
Best model: Gradient Boosting Regressor was saved for deployment and tested on unseen data. 

![]()


Below is a table listing the best features, hyperparameters, and metrics of the best model:
![]()

The final Gradient Boostimng model with r2_score : 0.51 was applied on the unseen movies to determine their ratings. The model performance was very close to train dataset with r2_score: 0.51.

The model optimization without and with PCA have been discussed in three separate jupyter notebooks Part-1, Part-II Part-III and available in Github following links:
•	Part-I
•	https://github.com/damayantinaik/Springboard_Week_7_Capstone_Project_Netfilx/blob/main/Netflix_data_model_development_Part_II.ipynb 
•	https://github.com/damayantinaik/Springboard_Week_7_Capstone_Project_Netfilx/blob/main/Netflix_data_model_development_PCAall_Part_III.ipynb
8. Future Recommendations:
In this project, all the possible ML predictive models: Simple linear Regression, Lasso Regression, Ridge Regression, Random Forest Regressor, Gardient Boosting Regressor have been applied to obtain the best model performance with maximum possible hyperparameter tuning. However, the model performance is not very good. I think, the model performance can be improved with addition of  more features like quality of music, quality of picture, actors ranking, users age, chorography etc. Hence, in future,  data on these should also be collected for analysis and ML model building . 

## 9. Acknowledgement
 I am grateful to Python developer community for providing many rich, versatile libraries to carry out all types of Data analysis and ML model building. I thank my mentor Yadunath Gupta for all his thoughtful guidance which helped me to dig deep into the project objective and solution, also  his constant encouragement to include advance pythonic way to write the code. Also, I like to thank springboard supporting staffs  for their  constant encouragement and my best services to gain knowledge in Data science.


