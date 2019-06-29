## TMDB Movie Revenue Prediction

<img src="images/movies.jpg?raw=true"/>


**Project description and overview:** In this TMDB Box Office Prediction project, we aimed at predicting the revenue for movies using some attributes of movies. We tried several techniques including random forest, text mining, extreme gradient boosting, clustering, neural network, and SVM. Finally, we learned that xgboost with text mining is the best one. 
We found that the most important variables that influence a movie’s revenue are budget, popularity, number of casts & crews and sentiments in a movie overview description. In conclusion part, we recommended several ways for movie producers to generate higher revenue.

### 1. Statement of the problem or question(s) being addressed

Nowadays where movies made nearly $12 billion in 2018, the film industry is more popular than ever. But what movies make the most money at the box office? How much does a director matter? Or the budget? Or the genres? These are the questions we would like to answer.
For this project, we studied metadata on over 7,000 past films and applied EDA and predictive analysis. Some of our variables are numeric, and some are texts. 
The goal of our project is to find out the important factors that would influence a movie’s revenue, and build a predictive model to forecast a movie’s revenue. The error measure we used is rmsle. Generally speaking, smaller rmsle means smaller error and better accuracy. With the help of our analysis, the production companies will be able to enhance a movie’s revenue by making adjustments to relevant factors, such as release data, and control the risk of producing movies.


### 2. Modeling techniques selected 

In our analysis, we applied many analytical techniques such as text mining, clustering and neural network, and decided to use sentiment analysis with extreme gradient boosting in our final moel. Below are a full list of model techniques we experimented:
- Text Mining (Sentiment analysis)
- Random Forest
- Advanced Decision Tree(Extreme Gradient Boosting)
- Clustering
- Neural Network
- SVM


### 3. Exploratoray Data Analysis and Feature Engineering

We have a combination of numerical data and text data. We first looked at the dirstributions of numeric variables in relation to target variable "Revenue". And then we analyzed the categorical data and one hot encoded them in order to input to xgboost model. Then, we performed text mining on text data such as movie overviews and keywords, and used sentiment analysis and tokenization to extract key information as new variables. 

Below are exploratary on some selected variables.

**Revenue**: Only a small number of movies has high revenue, whereas the majority doesn’t. The distribution of revenue is greatly positive skew. Due to the large range of revenue, we decided to do the log to revenue for a clearer distribution.    

<img src="images/movies-1.PNG?raw=true"/>

**Year and revenue**: Looking at the average revenue from 1921, we can find that the revenue for the film industry has been soaring. The industry is increasingly growing at a fast pace.  
<img src="images/movies-2.PNG?raw=true"/>


**Numeric Data Heatmap** The following heatmap indicates that budget has the highest correlation with revenue. And popularity is the second one.
<img src="images/movies-3.PNG?raw=false"/>
  
  
**Genres/producing company and revenue**: The most popular genres of movies are Drama, Comedy, Thriller, and Action. The top three movie producing companies are Warner Bros, Universal Pictures, and Paramount Pictures.
For genres, even though Adventure, Animation, Family, and Fantasy are not the most popular genres, their revenue is much higher than other types(first and second pictures). For producing companies, Walt Disney has much higher revenue than others (third one).
<img src="images/movies-4.PNG?raw=true"/>


**Overview and revenue**:
In our dataset, the overview of each movie conveys important information about a  movie’ content. We looked forward to finding out if the emotion in these movies, as well as the frequency of a word has impact on movies’ revenue. For this purpose, sentiment analysis can be a good choice to help us discover and extract meaningful patterns and relationships from text. To be more specific, firstly, we counted the overview length in words and in sentences separately. Then, we used "nrc" lexicon to count the number of words that show certain sentiment, such as positive, negative, anger, etc., and tried "afinn" lexicon to scores the sentiment of each overview. Besides, we created and prepared a corpus which contained all the meaningful words in the overviews of train and test data, and found out the words appeared most frequently.


The first two charts shows the relationship between revenue and the sentiment score of the overview. The last six charts shows the relationship between the revenue and the number of words with certain emotion. From these bar charts, a conclusion can be got that the overviews of movies with high revenue tend to include less sentimental words. The emotion of their overview is relatively neutral.

<img src="images/movies-5.PNG?raw=true"/>
<img src="images/movies-6.PNG?raw=true"/>


### 4. Predictive Model and Result

**Result and What we learn from Xgboost**:
In order to fit the xgb model, we converted categorical variables to numeric variables before we started. After that, we tried to fit the xgb model with arbitrary parameters. Then, in order to find out the relatively best parameters, we try the grid search. But the results of grid search are not better than before. We think there might be some over-fitting problems. 
There are two reasons we considered to the overfitting problem, the irrelevant sentiment related variables and the redundant trees in the model. For the first reason, we tried to drop some of sentiment related variables to see if the accuracy of the model could be better. The results showed that adding these variables have positive influence on model's accuracy. So in the final model, these variables will be kept. As for the second reason, we reduced the number of rounds(the number of trees) in the model, and our results became better, which means that the overfitting problem partially caused by the number of rounds.
Another way to enhance the accuracy of the xgboost model is to convert categorical variables to separate dummy variables, instead of numeric variables. Therefore, more features of the categorical variables can be saved in the model.

**Result and what we learned from clustering**:
After the clustering, we predicted and combined the result. We reduced the RMSLE to 2.235. However, we compared the “clustering then predict” total RMSLE with “no clustering” result, and found the “no clustering” performed better! Therefore, it is not the clustering that improved our model, but the dummy we did help the model. 
From this exercise, we learned that dummy categorical variables are useful. Originally, we used as.numeric to change our categorical variables to numeric variables. However, dummy is more accurate than simply treating them as numerics. Treating them as numeric make them look like there is a linear relationship between different factors while there is no this kind relationship between them at all. Using dummy can better represent categorical variables.
We also reflect on why clustering does not help our model. Movies probably are more complicated that they should be grouped into more than 2 categories. Grouping them into 2 groups is not enough, but grouping them into more groups will reduce our train dataset and leads to low accuracy. As a result, we decided not to adopt clustering in our final model. 

Other models we experimented include random forest, SVM and etc. 

**Model Accuray Table**:
<img src="images/movies-7.PNG?raw=true"/>
  
### 5. Conclusion and Recommendations from the Analysis
Our final model used both Text Mining and xgboost. It has the lowest error rate with rmsle equals to 2.18. We run a variable importance plot based on the xgboost model as shown below to understand what factors influence movie revenue.
<img src="images/movies-8.PNG?raw=true"/>

Based on our final xgboost model variable importance plot, below are some of our findings and recommendations.
Findings and Recommendations for movie producers:

- A few of the most important variables for predicting a movie’s revenue are: **budget, number of casts and number of crews**. These variables suggest that a movie with bigger budget is more likely to have a higher revenue as number of casts and number of crews all indicate size of the budget. 
- The second most important variable for predicting a movie’s revenue is **popularity**. This could be meaningful for movie producers with small budget as it indicates that even if a movie doesn’t have a high production budget, it can achieve high revenue if the movie has a high popularity before it is released. Therefore, we recommend movie producers with low budget to wisely allocate their resources to marketing to increase popularity and exposure among consumers. They can even leverage low-cast or even free marketing tools such as social media to increase movie publicity. 
- We also see that **Overview Length and its sentiment** such as p1 (the number of positive words) is another important indicator for movie revenue. We suggest movie producers to write detailed overview with proper amount of positive words(0-6) to attract consumers to movies. 
- As for **Runtime**, too long(>200 min) or too short(<50 min)  movies are not attractive to audience. The best runtime of a movie is between 100 minutes and 150 minutes.
- **Belong_to_collections**: Movies belongs to a collection are more likely to have higher revenue because they already have a large audience base.
- **Drama**: drama is the most common type of movies. So, it has great influence on the model results, even though it is not the most profitable movie genre. 

### Insights and Recommendations for investors:
- As we can see from the plot, the third most important variable that indicates movie revenue is **year**. As the year gets closer and closer to nowadays, the movie revenue goes higher and higher. This suggests that the movie industry is getting more and more popular and profitable. People loves watching movies as entertainment. We suggest investors to continue to invest in movies industry to support better movie production.
- **Budget** is the most important factor that can influence revenue. However, for those low-budget movies, a good overview, proper length of runtime, as well as the marketing campaigns before the movie is on can all help them to improve their revenue.

For presentation deck, please see [Click Here For Project Result Presentation Deck](/pdf/MoviePrediction.pdf).
