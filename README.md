## Exploring Depression Markers Over Progression of the Disease: A Machine Learning Approach Using Twitter Data
A Machine learning based research study which aims at examining and monitoring the various depression markers by analyzing the tweets of various self-declared depression patients on Twitter

## TABLE OF CONTENTS

* [Objective](#objective)
* [Data](#data)
* [Tools](#tools)
* [Techniques](#techniques)
* [Implementation](#implementation)
* [Results](#results)
* [References](#references)

## OBJECTIVE
Depression as a mental illness has been a great concern worldwide, with more than 264 million individuals affected. In the USA, nearly 17.3 million people suffer from depression with higher incidence among women and younger individuals. Despite the availability of effective treatments, depression goes undiagnosed and untreated in several cases. Also, there have been less emphasis on studying the progression of symptoms indicated by the patients before and after the on-set of conditions.

This study proposes a novel approach involving temporal analysis of tweets to identify progression of depression markers 90 days before and after the date of diagnosis.
The primary objectives in the study are:

- Constructing topic modeling of the tweets to understand the progression of symptoms before and after the on-set of depression
- Using Machine Learning algorithms to predict the probability of depression in a user given the set of tweets
- Formulate & distinguish linguistic characteristics displayed by patients with depression against a control group cohert

## DATA
In order to conduct a thorough topic modeling it was key to begin with a solid dataset in hand both in terms of quality and quantity. Preparing the data can be divided into following steps

#### 1. Data Extraction
Sourcing historic data from twitter was enabled by using the python library GetOldTweets3 - https://pypi.org/project/GetOldTweets3/. In order to target the depressed users on twitter, we used the keywords like 'diagnosed with depression', 'I have depression' to narrow our search results. It was also key to us to obtain the diagnosis date of such users. So, we further tuned our results by introducing keywords like 'diagnosed today', 'diagnosed yesterday', etc. With these filtering conditions in place, we obtained a list of 500 self-declared depressed users.

#### 2. Data preparation
We structured from the extracted content to obtain the data elements of interest, like username, tweet time, hashtags, date of diagnosis, etc. After carefully validating each of the tweets, tweeting frequency, we chose a subset of 230 depressed users for our study. 

Using GetOldTweets3 we pulled the historic tweets for the chosen 230 users in the time period of 2018-2019. We also constructed a datasheet containing username, tweets, date of diagnosis, time of tweet, number of tweets per user

#### 3. User profiling
In order to create a portfolio of the chosen users, we used Microsoft Azure FaceClient API to analyze the profile picture of the users to determine the age and gender of the users. To achieve more precision in creating user portfolios, we implemented a Multimodal, Multilingual, and Multi-attribute system ([M3 Inference] https://github.com/euagendas/m3inference))  designed to create demographic information of users from their text. 

#### 4. Data cleaning
We cleaned the tweets (text data) removing stopwords from the texts. We further fine-tuned by lematizing and stemming the text content. 

## TOOLS
- Python (pandas, seaborn, nltk, gensim, spacy, GetOldTweets3, azure-cognitiveservices, corextopic, scikit-learn, sklearn)
- MS Excel, SPSS, STATA, Tableau

## TECHNIQUES

| TASK | TECHNIQUES  | TOOLS USED | 
| --------- | -------------| ---------------|
| Data Collection | Tweet Extraction using GetOldTweets | [got](https://pypi.org/project/GetOldTweets3/) | 
| Data preparation | Data preparation, Exploratory Data Analysis | MS Excel, Pandas | 
| Data processing | Processing & cleaning text data using stopwords removal, lematization, stemming | nltk, gensim, spacy |
| Statistical Analysis | Wilcox-signed rank tests, c-logit | SPSS, STATA |
| Exploratory Data Analysis | Data visualization | matplotlib, seaborn, MS Excel, Tableau, Wordcloud |
| Text Analytics | Topic Modeling & Linguistics, Sentiment analysis | tfidf, LDA, Anchor word Corex, LIWC, Vader | 
| Supervised learning | Implementing Machine learning models in python | Naive-Bayes, Logistic Regression, Support Vector Machine |
| Other tasks | Image Analysis | Microsoft Azure FaceClient |
| Environments & Platforms | Microsoft Azure, Google Colab, Twitter, Jupyter Notebook |

## IMPLEMENTATION

## RESULTS

## REFERENCES
