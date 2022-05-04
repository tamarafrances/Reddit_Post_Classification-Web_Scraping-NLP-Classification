# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Reddit Post Classification - r/SkincareAddiction and r/MakeupAddiction

<br>

### Background
Reddit is a social media discussion website comprised of subject-specific forums called 'subreddits'.  While Reddit is read-only for site visitors, those with a registered account can posts multiple forms of content, including text posts, images, links, and videos, just to name a few ([source](https://en.wikipedia.org/wiki/Reddit)).

A subreddit is a forum on Reddit focused on a specific topic. Some of the largest subreddits on Reddit have over ten million members. Subreddits may have moderators, FAQ sections, and bots to periodically scan posts and reply to or remove posts when necessary.
<br><br>
### Problem Statement

My goal was to create a classification model to classify a set of subreddit posts into their respective subreddits r/SkincareAddiction or r/MakeupAddiction using selftext (the body of a text post) alone.

Ideally, I would create a model that is better than the baseline using accuracy score as a success metric.

---

### Data Collection

Using the Pushshift API, I built a function that took subreddit and created_utc as inputs and returned a dataframe of 3,500 posts with 70+ features from my two subreddits of interest (r/SkincareAddiction and r/MakeupAddiction). This can be found in the code folder under 'Pulling Data Using Pushshift's API'.

The final dataset amounted to 7,000 rows. The only predictor variable I used in model creation was 'selftext'. The target variable was 'subreddit'.
<br><br>

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**selftext**|*object*|skin_and_makeup.csv - generated using Pushshift API|The body of text in a Reddit text post|
|**subreddit**|*object*|skin_and_makeup.csv - generated using Pushshift API|The sub-forum that a Reddit post belongs to|


<br><br>
### Modeling and Results

#### Model Creation: Iteration 1
The goal was to create a model that beats the baseline model with an accuracy score of 0.509. With default CountVectorizer and model parameters, the accuracy scores were as follows:
* Multinomial Naive Bayes accuracy score :  0.7836
* Logistic Regression accuracy score :  0.7789
* Random Forest Classifier accuracy score :  0.7474

I realized many rows in my dataset had selftext that was removed or deleted, so I dropped those rows from my dataset and re-created the above models using the cleaned data.

#### Model Creation: Iteration 2
The new goal was to create a model that beats the baseline model with an accuracy score of 0.595. With default CountVectorizer and model parameters, the accuracy scores were as follows:
* Multinomial Naive Bayes accuracy score :  0.9418103448275862
* Logistic Regression accuracy score :  0.9213362068965517
* Random Forest Classifier accuracy score :  0.9191810344827587

##### Hyperparameter Tuning
After conducting some hyperparameter tuning using GridSearchCV, the updated scores were as follows:
* Multinomial Naive Bayes accuracy score :  0.9558
* Random Forest Classifier accuracy score :  0.9353
* Logistic Regression accuracy score :  0.9343

More details on the hyperparameter tuning can be found in the code folder under 'Reddit Post Classification - rSkincareAddiction and rMakeupAddiction'.
<br><br>
Ultimately, the **Multinomial Naive Bayes model** with hyperparameter tuning was the best model was a **0.9558 accuracy score**, beating the baseline model's accuracy score of 0.595.

Towards the end of the 'Reddit Post Classification' notebook, I spent some time diving into the model's misclassifications to get a better sense of most common misclassified words and view the specific selftexts that were misclassified.

---
### Next Steps

In future iterations of this project, I would test some models I did not use in this project, like Extra trees Classifier, or ADA Boost. Additionally, I would spend more looking into lemmatization, and spending more time tuning hyperparameters to see if I could add a bit more to the accuracy scores.