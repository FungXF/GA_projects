# Reddit Classification 

## Notebook 1 of 5 - Scraping Data
- There are a total of 5 notebooks
- Due to the processing power required, the modelling is seperated into 3 code notebooks (Notebook 3,4,5)

### Introduction
- Mental health is critically important to everyone, everywhere. All over the world, mental health needs are high but responses are insufficient and inadequate. This issue is prevalent in all countries including first world countries. However, one of the pervasive issues the report covers is stigma. Stigma wears many faces. We most commonly equate it with how we treat one other. However, that represents only part of the issue; personal shame, internalized through an individual’s mental health suffering, is a silent problem. We must normalize talking about mental health and its multitude of conditions because stigma is the chain onto which all mental health conditions link. [WHO Article](https://www.who.int/news-room/commentaries/detail/world-mental-health-day-is-an-opportunity-for-us-to-embrace-our-sense-of-community-and-normalize-mental-health)
- Thus, there are cases where people do not know if they need help or they do know but do not know where to look for help.
- Due to stigmatism, there is a possibility that people try to self-medicate or they go on to social media platforms to write their feelings but did not seek help.
- Thus, this project would bring about the first step in correctly classifying the topics based on NLP.

### Problem Statement
1. Through natural language processing and classification models, How can we classify posts based on the texts used by people who may be depressed or anxious? 

2. How can sentiment analysis be utilized to detect primary and secondary emotions from the posts?

- To correctly classify on anxiety and depression based the subreddit posts in these two topics.
- The vectorizers that will be deployed are CountVectorizer and TfidfVectorizer
- The models used are Logistic Regression, KNearestNeighbors, MultinomialNB, RandomForest and Pycaret.
- The main metrics used for evaluating the performance of the models is accuracy.
- Hugging Face models will also be explored in these notebooks.

### Target Audience
As a Data Science enthusiast and a fellow reddit user who is promoting the usage of NLP for moderators to detect emotions based on redditors's posts by joining as a speaker of World Health Day Convention.

### Datasets
- There are two datasets from two reddit topics, 'Anxiety' and 'depression' which were scrapped using Pushshift API.
- Each dataset has more than 15000 post from each topic
- The duration of the scrap will start with the latest post from 03 Oct 2022 to earlier post.

### Data Scraping Summary
Total 15,242 posts of 'Anxiety' and 15,238 posts of 'depression' were scrapped from subreddit.  
This is a total of 30,480 posts.  
The next notebook (Notebook 2) will be on Base Model, Data Cleaning and EDA.

## Notebook 2 of 5 - Base Model, Data Cleaning and EDA

### Base Model
- For the base model, no preprocessing was done and the `title_text` was directly input into the vectoriser and estimator model.
- Vectoriser: CountVectorizer()
- Estimator: LogisticRegression()

- The Base Model of using CountVectorizer and Logistic Regression has provided a good baseline model of classifying 'Anxiety' and 'Depression' with scores of 88.6% accuracy. 
- However, the train score is 97.1% which is higher than the test score which suggest that it is overfitted.
- It is also observed that the dimensionality is too high where the number of columns is more than the number of rows.

## Pre-Processing
- Regex (To retrive only characters and remove special characters and numbers)  
There is one row that regex is unable to extract the text. This row is dropped.
- Remove duplicated rows  
There are total of 572 duplicated rows which were dropped. This represents a total of 1.88% of data dropped which is acceptable since having duplicated rows does not value add to the training of the model.
- Tokenizing (Via-Vectorization)
- Lemmatizing/Stemming (Via-Vectorization)
- Stop word removal (Via-Vectorization + Custom Words)

## EDA
### Keywords were identified and removed by adding to the custom stop words list.
`custom_stop_words` was created by adding these words 'removed', 'deleted', 'anxiety', 'anxious', 'depression', 'depressed' with the `stop_word = 'english'` within the CountVectorizer/TfidfVectorizer 
- It is observed that the trigram produces the same types of words used in the text. These are not key words in either of the classes. Thus, the custom stop words created fulfills the criteria of removing keywords that can easily fall into the classes.
- Exploring into the length of post which is observed that 96.5% of the post have word count less than 512 words.  
- Both Word Count and Character length have right tailed distributions
- Exploring into the days of post: There is not much difference in the number of post per day for both subreddit topics.

## Notebook 3 of 5 - (Vectorization + Modelling) Part 1 of 2
### Pipeline (Vectorization + Modelling)
Two Vectorizers are selected and this will be used together with the estimators in pipeline 
Pipeline 1 = CountVectorizer() + Estimators (LogReg, kNN, MultinomialNB)  
Pipeline 2 = TfidfVectorizer() + Estimators (LogReg, kNN, MultinomialNB)  
Pipeline 3 = TfidfVectorizer() + RandomForest (In Notebook 4)  
Pipeline 4 = TfidfVectorizer() + Pycaret Model (In Notebook 4)

|Pipeline|Vectorizer|Estimator|Parameters for Vectorizer|Parameters for Estimator|Train|Test
|----|----|----|----|----|----|----|
|Base|CountVectorizer|Logsitic Regression|-|max_iter = 700|0.971|0.886|
|1|CountVectorizer|Logistic Regression|max_df = 0.9, max_features = 5000, min_df = 2, ngram_range: (1,2), stop_words = custom_stop_words, Tokenizer = StemmTokenizer|c=0.1, max_iter = 700|0.930|0.900|
|2|TFIDF|Logistic Regression|max_df = 0.9, max_features = 3000, min_df = 2, ngram_range: (1,1), stop_words = custom_stop_words, Tokenizer = StemmTokenizer|c=1, max_iter = 700|0.924|0.906|

The accuracy of pipeline 2 is higher than pipeline 1.
The difference between the train and test scores are also closer in pipeline 2 than pipeline 1. 

A smaller regularization (c=1) was chosen compared to (c=0.1) which shows that pipeline 2 has a lesser overfit issue. This is confirmed by observing the difference between train value (0.924) versus test value (0.906) in pipeline 2.

It is also shown that both models prefer to use StemmTokenizer. For gridsearch to use the parameter, ngram_range of (1,1), this is a good indicator that the observations in unigram, bigram, trigram word list that the words list in custom_stop_words were in the right direction.


## Notebook 4 of 5 - (Vectorization + Modelling) Part 2 of 2
### Pipeline Vectorization + Modelling 
Pipeline 3 = TfidfVectorizer() + RandomForest  
Pipeline 4 = TfidfVectorizer() + Pycaret Model
Both TfidfVectorizer used the best parameters evaluated from pipeline 2.

- The train score for pipeline 3 is at 87.9% and the test score at 87.2% which the train and test score is much closer than the base model but test score is lower than the base model. 
- Pipeline 3 has the lowest accuracy score than the rest of the models.
- Through the evaluation of the data through Pycaret models after vectorizing, for the finalised model of LogReg has the highest accuracy score of train (0.926)/92.6% and test(0.906)/90.6%. 
- Pycaret (0.906) has higher test score than the base model(0.886) and similar scores to pipeline 2(0.906).


|Pipeline|Vectorizer|Estimator|Parameters for Vectorizer|Parameters for Estimator|Train|Test
|----|----|----|----|----|----|----|
|Base|CountVectorizer|Logsitic Regression|-|max_iter = 700|0.971|0.886|
|3|TFIDF|RandomForest|max_df = 0.9, max_features = 3000, min_df = 2, ngram_range: (1,1), stop_words = custom_stop_words, Tokenizer = StemmTokenizer|max_depth= 4, n_estimators= 200|0.871|0.863|
|Pycaret|TFIDF|Logistic Regression|max_df = 0.9, max_features = 3000, min_df = 2, ngram_range: (1,1), stop_words = custom_stop_words, Tokenizer = StemmTokenizer|c=1, max_iter = 1000|0.926|0.906|

## Notebook 5 of 5 - Hugging Face Models + Evaluation + Conclusion + Limitations + Recommendations/Further Research
### Further Studies on emotions of the subreddit posts
- Other than correctly classifying the post to the topics, further investigation is done to know if there are other emotions when a redditor contributes to the subreddit.
- Two Models were used.
- Model 1: [j-hartmann/emotion-english-distilroberta-base](https://huggingface.co/j-hartmann/emotion-english-distilroberta-base)
- Model 2: [arpanghoshal/EmoRoBERTa](https://huggingface.co/arpanghoshal/EmoRoBERTa?text=I+like+you.+I+love+you)

Note that there are restrictions of the tokenizer in the hugging face models which restricts to a maximum of 512 words per document.
In the word count it was found that there are 96.5% of post with less than 512 words in the dataset.

### Model 1: j-hartmann/emotion-english-distilroberta-base
Human emotions has been classified to [6 basic emotions](https://www.paulekman.com/universal-emotions/). by Paul Ekman.  This model includes 6 basic emotions + neutral which has been trained on a diverse collection of text types. Specifically, they contain emotion labels for texts from Twitter, Reddit, student self-reports, and utterances from TV dialogues.

### Model 2: arpanghoshal/EmoRoBERTa
- The second model uses Dataset labelled from 58,000 Reddit comments with 28 emotions. 
- We want to find out what are their secondary emotions from redditors post 

Using j-hartmann's model it is observed that redditors who post on 'Depression' topics are mostly sad which is mentioned in this article as a [primary symptom](https://www.webmd.com/depression/ss/slideshow-depression-overview)  
On the subreddit 'Anxiety' the highest count of emotion is 'fear' which is corroborated with this article on [anxiety disorder symptoms](https://www.webmd.com/anxiety-panic/guide/anxiety-disorders)

By looking at arpanghoshal's model, the top emotions are largely similar to j-hartmann's model for the with further insights inth how people are feeling when they write their reddit post.

# Evaulation
|Pipeline|Vectorizer|Estimator|Parameters for Vectorizer|Parameters for Estimator|Train|Test
|----|----|----|----|----|----|----|
|Base|CountVectorizer|Logsitic Regression|-|max_iter = 700|0.971|0.886|
|1|CountVectorizer|Logistic Regression|max_df = 0.9, max_features = 5000, min_df = 2, ngram_range: (1,2), stop_words = custom_stop_words, Tokenizer = StemmTokenizer|c=0.1, max_iter = 700|0.930|0.900|
|2|TFIDF|Logistic Regression|max_df = 0.9, max_features = 3000, min_df = 2, ngram_range: (1,1), stop_words = custom_stop_words, Tokenizer = StemmTokenizer|c=1, max_iter = 700|0.924|0.906|
|3|TFIDF|RandomForest|max_df = 0.9, max_features = 3000, min_df = 2, ngram_range: (1,1), stop_words = custom_stop_words, Tokenizer = StemmTokenizer|max_depth= 4, n_estimators= 200|0.871|0.863|
|Pycaret|TFIDF|Logistic Regression|max_df = 0.9, max_features = 3000, min_df = 2, ngram_range: (1,1), stop_words = custom_stop_words, Tokenizer = StemmTokenizer|c=1, max_iter = 1000|0.926|0.906|


Conclusions
1. Through natural language processing and classification models, How can we classify posts based on the texts used by people who may be depressed or anxious? 
- The pipeline 2 TFIDF vectorizer and Logstic Regression is able to accuracy classify the post with a score of 90%.

2. How can sentiment analysis be utilized to detect primary and secondary emotions from the posts?  
- By using the hugging face models, it provides insights based on the 7 emotions model and 28 emotions model by into the underlying feelings behind redditor's posts.

This is a first stop towards predicting or identifying the emotions associated with mood disorder and could be useful in further development to provide support for people with mental health issues.

Limitations
- This study is limited to 15000 post per study which can be further expanded to cover more posts.
- Limited to these two topics and from reddit posts only.
- The period of study is limited to a few months only, this can be expanded to a few years so that we can check if there is seasonality involved.
- The location of the posts are also unknown where there might be different type of usage of languages depending on where they are from.

Recommendations
- Increase the size of study based on longer duration to understand if there is seasonality involved.
- Broden the scope: The 7 and 28 emotions models could be trained on other platforms such as  twitter and facebook.
- Exploring other languages: Even though the data that were scraped only have english text, on other platforms there might be other languages that would be posted. 
- Identify key words: System will be able to pick up certain emotions and provide support
- Dashboard for moderators: Show the top emotions and possibly allow one to pin a response message
- Examine links with suicide ideation: Flag out potential posts that matches these emotions
