# Predicting Subreddits Using NLP: r/Fantasy vs. r/scifi
### Uriel Eckmann

![Scifi Fantasy Venn Diagram](./assets/SciFi_Fantasy_Venn.png)

## Problem Statement

Reddit's moderators are going on strike! After years of having to read through countless posts, the moderators have expressed feeling overwhelmed and are considering going on strike unless something is done to help them get through all the posts. Additionally, the reddit servers are beginning to become overloaded. Given the amount of crossposts that occur on a day to day basis, the servers can't maintain so many subreddits! 

Luckily, our company has recently come up with a solution for both of these problems. Our goal is to utilize Natural Language Processing to eliminate redundant subreddits while simultaneously predicting if a post actually belongs in the subreddit when submitted. We'll begin by eliminating the r/geekdom subreddit which is filled with crossposts from [r/scifi](https://www.reddit.com/r/scifi/) and [r/fantasy](https://www.reddit.com/r/fantasy/). From now on, anything posted in the r/geekdom subreddit will automatically be sorted into either r/scifi or r/fantasy through utilizing our classification model. The success of this model will be measured in it's accuracy to classify posts. If we can successfully build an accurate model, our model can then be implemented in these 2 subreddits to help moderators by automating the process by which posts are checked to ensure that they actually belong in that subreddit. Once we have built a successful model, our process can then be repeated for any number of other subreddits, streamlining the entire site, saving time for the mods, saving money on servers, and keeping users happy.

## Executive Summary
Our goal here is to create an accurate model that will predict if a written post belongs in the scifi or fantasy subreddit. The success of our model will be determined by it's accuracy.
### _Workflow_
#### _Data Collection_
The data for this project was collected using reddit's pushshift [API](https://api.pushshift.io/reddit/search/submission). This was a difficult experience, as much of the data had to be cleaned for a variety of reasons - posts wer removed from the subreddit for not following subreddit rules, deleted posts, or posts with no actual text content. Once all of the data was collected and cleaned, it was then stored as a CSV to be used in this notebook.
#### _NLP_
Because we were using text data, the data had to be converted into a format that would be usable by our model. This meant that the text itself had to be tokenized, lemmatized, and in some cases, fixed up a bit. Once the text data was cleaned, it then had to be transformed into a format that would be interpretable by a computer. We used the CountVectorizer and the TFIDFVectorizer to transform all the text into a dataframe that considered each word as a statistic as opposed to a word.
#### _Data Exploration_
After transforming our data, we were able to look at all the particular words that were most relevant to our two subreddits. While Science Fiction and Fantasy do overlap in many areas, it was quite clear that there were some important differences between the two, most importantly, the fact that r/fantasy appeared to be more reading and book focused, while r/scifi was more TV and Movies focused. 
#### _Observations_
After building several models from our data to predict the subreddit, we actually saw some success in our models. Our most successful model was the Logistic Regression Model, but it is worth noting that this particular model was overfit. Most of the models performed relatively well, and certainly did better than the baseline.

#### _Issues_
Using NLP for the first time was stressful and a handful. Learning to utilize Lemmatizing and Tokenizing was very difficult, and it did not help that lemmatizing did not alway produce the results I hoped for. While doing each did ultimately make the models better, it could still be frustrating working with them. Another critical issue was timing - running these models through a Pipeline took far too much time and often caused more frustration. It's possible that if I were to go back, I might Vectorize the text before fitting it to the model, or using RandomSearch instead of GridSearch.

## Data Dictionary

|Column Name|Data Type|Description|
|---|---|---|
|title |object|Title given to the post|
|selftext |object|Main body of the post|
|subreddit |object|Which subreddit the post was from, our target|
|created_utc |int|Date and time this was posted in Epoch time|
|author |object|The username of the redditor|
|num_comments |int|The number of comments made on the post|
|score |int|The number of upvotes the post received|
|is_self |bool|Checks that the post is a text|
|timestamp |object|The date of the post in yyyy/mm/dd form|


## Conclusion 

Our model performed relatively well! Considering that if we compare our model's accuracy to the baseline's accuracy, we have relative success in that regard. It should be noted that our model is overfit, and as such, will need some work, we can definitively say that this problem can be fixed. Given that this was our first iteration, This is a success.

Reddit can inform the moderators that they will soon be implementing automated models that will help the moderators determine if a post is fine. Additionally, r/geekdom will soon be discontinued, freeing up much needed space on the servers. Looking to the future, Reddit will be able to implement these models soon and will vastly improve their user experience. 

## Recommendations

As stated earlier, the work is not yet done. This model still needs improvement, and no model will ever be perfect. One thing to consider is that there are a few steps that should be taken:
1. Continue building models with more data. As more data is collected, the models will each improve.
2. Consider using other classification models. There are plenty of other models that were not used in this first iteration. As such, models such as KNN, LASSO Classifiers, and others would be useful to try.
3. In that regard, Boosting current models is another great suggestion, that will improve the current models. 
4. Another option would be for these models to be used in an ensemble. Utilizing the "Wisdom of the Crowd" is a great way to ensure a model that will predict as best as possible. 
5. Finally, since no model will be perfect, one thing to consider is that we have a threshold of 0.5 in regards to the probability of a post that will determine which subreddit it goes to. We can use the probabilities to determine that certain posts are not necessarily going to be classified correctly, and need to be submitted to the moderators. Using a range from 0.4 - 0.6 will cut down on 80% of the posts needing review, and will ensure that earlier iterations of the model can be used, while minimizing the error. 

## References
- [Reddit API](https://api.pushshift.io/reddit/search/submission)
- [Reddit](https://reddit.com/)
- [r/fantasy](https://www.reddit.com/r/fantasy/)
- [r/scifi](https://www.reddit.com/r/scifi/)
- [Stop Words](https://towardsdatascience.com/stop-words-in-nlp-5b248dadad47#:~:text=What%20are%20stop%20words%3F,at%2C%20which%2C%20and%20on.)
- [tokenizing](https://docs.python.org/3/library/tokenize.html)
- [Lemmatizing](https://nlp.stanford.edu/IR-book/html/htmledition/stemming-and-lemmatization-1.html)
- [CountVectorization](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html)
- [Matplotlibrary Tick Parameters](https://dfrieds.com/data-visualizations/style-plots-python-matplotlib.html#:~:text=For%20the%20methods%20title%20%2C%20xlabel,smaller%20fonts%20than%20axes%20labels.)