# Introduction

Reddit is a social news website where users with common interests discuss and share content in subreddits which are divided by topics. The website is the sixth most visited website in the U.S.  and has about 300 million monthly active users.

Natural language processing is the study of human language and its purpose is to train computers to analyze it and extract data from it.

The purpose of this project is to use NLP to build a model to rebuilt two subreddits: Conspiracy and Climate Skeptics, which are fairly similar.

# Problem Statement

The conspiracy and climate skeptics subreddits were accidentaly deleted. Thankfully, we had 1000 posts from each subreddit archived, which is enough to build a model and train it to be able to classify posts into either subreddit using the post's title. The stakeholders here are Reddit, and the 840k conspiracy subscribers and 11k climate skeptics subscribers.

# Executive Summary

### Cleaning
Since we built our dataframe ourselves there were no missing values here. The purpose of this section was to reformat the titles in order to get a better model. The titles here were made all lower case, so that the same two words wouldn't be counted as different depending on capitalization, also i got rid of special characters, punctuation and numbers, and the titles were also lemmatized. 
Stemming and Lemmatizing are two techniques that reduce words. While stemming replaces words with their roots, often one that doesn't have any meaning, Lemmatizing is less harsh and will always return a word that exists in the dictionary.

### EDA
In our exploratory data analysis we were looking for trends in the subreddits. The most frequent words and bigrams were explored. Also we wanted to check the total word count in each subreddits and the number of common words.

### Modeling
The baseline model was predicting the majority class (in this case conspiracy), where we would end up with 50.7% accuracy.

6 models were implemented in total using 2 vectorizers and 3 modeling techniques using pipelines.

Count Vectorizer tokenizes the titles then counts the number of times each word appears in a document, where each word is as meaningful as the other.
TF-IDF vectorizer is used to extract features from titles and then the words are assigned a value between 0 and 1 based on how many times the words appear in the dataset, so more frequent words are assigned less meaning.

We use both these vectorizing techniques to transform the datasets, and then we apply either Logistic Regression, Multinomial Naive Bayes or Random Tree Classifier to solve the classification problem.

All combinations were tried with Grid Search with multiple possible values for each parameter, with the best perfoming being TF-IDF vectorizer with Logistic Regression with a test set accuracy score of 0.91

# Evaluation

The metric we used to evaluate models was accuracy, since we don't prefer any subreddit over the other, we want to reconstruct both with as many right posts as possible.

Evaluating each model the best one was logistic regression. The metrics we could use to evaluate it with ended up being:
Accuracy = 91.5%; Sensitivity = 96.6%; Specificity = 87.5%; and Precision = 88.1%. 

While looking at bigrams frequently occuring in False Negatives (posts that were originally from climate skeptics but were predicted as being from conspiracy), one notable trend we notice is that all posts with the "climate change" bigram were classified as being from climate skeptics. While the newly reconstructed conspiracy subreddit contains no posts with either "global warming" or "climate change" in their titles.

# Conclusion

We were ultimately successful in rebuilding the 2 subreddits, with a 91% accuracy. It would be interesting to build a model for posts that contain 'climate change' or 'global warming' in their titles and identify the source of those posts in particular.