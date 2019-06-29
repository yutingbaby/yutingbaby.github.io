## TMDB Movie Revenue Prediction

<img src="images/movies.jpg?raw=true"/>


**Project description:** In this TMDB Box Office Prediction project, We aimed at predicting the revenue for movies using some attributes of movies. We tried several techniques including random forest, text mining, extreme gradient boosting, clustering, neural network, and SVM. Finally, we learned that xgboost with text mining is the best one. 
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


### 3. Exploratoray Data Analysis and Models

In our dataset, the overview of each movie conveys important information about a  movie’ content. We looked forward to finding out if the emotion in these movies, as well as the frequency of a word has impact on movies’ revenue. For this purpose, sentiment analysis can be a good choice to help us discover and extract meaningful patterns and relationships from text. To be more specific, firstly, we counted the overview length in words and in sentences separately. Then, we used "nrc" lexicon to count the number of words that show certain sentiment, such as positive, negative, anger, etc., and tried "afinn" lexicon to scores the sentiment of each overview. Besides, we created and prepared a corpus which contained all the meaningful words in the overviews of train and test data, and found out the words appeared most frequently.


### 4. Provide a basis for further data collection through surveys or experiments

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
