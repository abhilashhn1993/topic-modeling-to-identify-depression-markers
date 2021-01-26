## Exploring Depression Markers Over Progression of the Disease: A Machine Learning Approach Using Twitter Data
A Machine learning based research study which aims at examining and monitoring the various depression markers by analyzing the tweets of various self-declared depression patients on Twitter

## TABLE OF CONTENTS

* [Objective](#objective)
* [Data](#data)
* [Tools](#tools)
* [Techniques](#techniques)
* [Implementation](#implementation)
* [Results](#results)
* [Conclusion](#conclusion)
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

Code can be found [here](https://github.com/abhilashhn1993/topic-modeling-to-identify-depression-markers/blob/master/Code/TweetExtraction.ipynb)

#### 2. Data preparation
We structured from the extracted content to obtain the data elements of interest, like username, tweet time, hashtags, date of diagnosis, etc. After carefully validating each of the tweets, tweeting frequency, we chose a subset of 230 depressed users for our study. 

Using GetOldTweets3 we pulled the historic tweets for the chosen 230 users in the time period of 2018-2019. We also constructed a datasheet containing username, tweets, date of diagnosis, time of tweet, number of tweets per user

#### 3. User profiling
In order to create a portfolio of the chosen users, we used Microsoft Azure FaceClient API to analyze the profile picture of the users to determine the age and gender of the users. To achieve more precision in creating user portfolios, we implemented a Multimodal, Multilingual, and Multi-attribute system: [M3 Inference](https://github.com/euagendas/m3inference), designed to create user profiling revealing the gender and Age of the chosen users.

Code for both techniques can be found here:
-[Azure Face Client](https://github.com/abhilashhn1993/topic-modeling-to-identify-depression-markers/blob/master/Code/AgenGenderProfiling.ipynb) 
-[M3 Inference](https://github.com/abhilashhn1993/topic-modeling-to-identify-depression-markers/blob/master/Code/AgenGenderM3Model.ipynb)
 
#### 4. Control Group
To study the variation of depression characteristics with a control group cohert it was important to choose a random set of non-depressed users exhibiting similar user profile (similar age and gender values)to create a match-pair with each of the depressed users in our sample space. With that intent, a random cohert of 230 users similar age and gender characteristics were chosen and their historical twitter data is scraped.

#### 5. Data cleaning
All the words in the tweets were transformed into lower cases, and @mentions, special characters, emoji and URLs were removed. We fine tuned the tweets (text data) by removing stopwords from the texts. We further fine-tuned by lematizing and stemming the text content. This allowed us to uncover the topics underlying the tweets indicating the various characteristics of depression.

Code can be found [here](https://github.com/abhilashhn1993/topic-modeling-to-identify-depression-markers/blob/master/Code/TweetCleaner.ipynb)

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
| Text Analytics | Topic Modeling & Linguistics, Sentiment analysis | tfidf, LDA, Anchor CorEx, LIWC, Vader | 
| Supervised learning | Implementing Machine learning models in python | Naive-Bayes, Logistic Regression, Support Vector Machine |
| Other tasks | Image Analysis | Microsoft Azure FaceClient |
| Environments & Platforms | Microsoft Azure, Google Colab, Twitter, Jupyter Notebook |

## IMPLEMENTATION
The Primary goal of focus was to compare the social media disclosures by the depressed users before and after the date of clinical diagnosis. To perform the temporal analysis of social disclosures prior to and after clinical diagnosis of depression, a machine learning technique for text mining known as topic modelling was employed to uncover hidden topics in the text data.

Although there are several probabilistic generative models like Latent Dirchlet Allocation (LDA) are available, a relatively new approach - Correlation Explanation (CorEx) was implemented. CorEx was implemented on the dataset with different number of topics (n = 10, 20, 30, 40, 50). The specification of the number of topics is important to identify the appropriate latent topics underlying the tweets. The distribution of total correlations for each topic was computed to see how much correlation each additional topic contained. This was iteratively done to find the optimal number of topics. 

Following the above analysis the 7 topics (given in the table below) were chosen with a careful assessment of anchor words in each of these categories to build an Anchor word driven version (A semi-supervised approach) of the CorEx algorithm.

| SL NO | TOPIC | TOP ANCHOR WORDS |
| ----- | ----- | ---------------- |
| 1 | Causes | assault, trauma, torture, war, abuse |
| 2 | Physical Symptoms | pain, ache, insomnia, headache | 
| 3 | Mental Symptoms | sad, panic, anxious, lonely, depress | 
| 4 | Swear words | shit, f*#k, ass, damn | 
| 5 | Treatment | doctor, therapy, treat, pills, drug, meds, prozac | 
| 6 | Coping & Support Mechanisms | exercise, gym, motivate, meditate, diet, heal | 
| 7 | Lifestyle | art, music, play, write, sketch, paint, holiday |

To assess the extent of association every tweet with the discovered themes from the topic modeling was done by examining the Total Correlation (TC score) scores provided by the CorEx for each of the tweets. This score indicates the strength of the association of a tweet to a particular topic. These TC-scores were aggregated on day level and corresponding z-scores were computed for the whole pre and post diagnosis period of 90 days. This would reveal the progression of each of the topics in both before and aftermath of the onset of depression. A conditional logistic regression (in STATA) was used to compute the odds of a user tweeting about a specific theme in both pre and post diagnosis period. 

These results also helped to carefully assess the differences between depressed and control group users. 

Code can be found [here](https://github.com/abhilashhn1993/topic-modeling-to-identify-depression-markers/blob/master/Code/AnchorCorexTopicModeling.ipynb)

The secodary goal was to design a classifier to predict whether a subject is depressed or not based on their tweets. Binary classifier using the TC scores of each of the 7 themes extracted as the principal features were implemented along with the age and gender features of the subjects (depressed and control group combined). Three classification algorithms: Logistic Regression, Naive-Bayes algorithm, Support Vector Machine with a linear kernel were used with a 10-fold cross validation to model the features in the dataset. The performance of classification models was assessed using five metrics: accuracy, precision (number of true positives over the sum of number of true positives and false positives), recall, F1 measure and ROC curves.

Code can be found [here](https://github.com/abhilashhn1993/topic-modeling-to-identify-depression-markers/blob/master/Code/Final_Classifier.ipynb)

## RESULTS
The topic modeling revealed the insights into the trends pertaining to the themes in the period prior to and after the depression diagnosis. Some of the key insights uncovered are:
- Depressed users engaged in discourses about causes much more in the post-diagnosis period as compared to prediagnosis phase
- Once clinically diagnosed, users seem to reflect on the causes of depression and share this information on social media 
- When it comes to physical symptoms, the discussion about physical symptoms decreases after the diagnosis and disclosure
- Depressed users shared content about their anti-depression medications, side effects, clinic visits, counselling, therapy sessions and treatment plans post diagnosis

#### Performance metrics of classifiers
| Metric | SVM | Logistic Regression | Naive-Bayes | 
| ------ | --- | ------------------- | ----------- |
| Accuracy | 90.93 | 90.58 | 79.71 |
| Recall | 92.61 | 90.61 | 79.8 |
| Precision | 90.2 | 90.63 | 80.1 |
| AUC ROC | NA | 0.91 | 0.8 |
| F1-score | 91.21 | 90.85 | 79.67 |

ROC curve for the models are given below

![Capture](https://user-images.githubusercontent.com/9445072/105903878-125af600-5fe6-11eb-9439-08071bf6e24c.JPG)

## CONCLUSION
This study focused on demonstrating the progression of various symptoms and characteristics displayed by depressed individuals on Social Media using Machine Learning and Text Mining approach. In addition to using Machine Learning algorithms to detect symptoms of depression among users, the text mining gave a more comprehensive information about how the depressed individuals carry themselves on Social Media thus enabling a mechanism to continuosly monitor such patients. These findings can be used to target such patients for clinical intervention.

## REFERENCES
- Andalibi, N., Ozturk, P., & Forte, A. (2015). Depression-related Imagery on Instagram. Proceedings of the 18th ACM Conference Companion on Computer Supported Cooperative Work & Social Computing, 231–234.
- Birnbaum, M. L., Ernala, S. K., Rizvi, A. F., De Choudhury, M., & Kane, J. M. (2017). A Collaborative Approach to Identifying Social Media Markers of Schizophrenia by Employing Machine Learning and Clinical Appraisals. Journal of Medical Internet Research, 19(8), e289.
- Blei, D. M., Ng, A. Y., & Jordan, M. I. (2003). Latent Dirichlet Allocation. Journal of Machine Learning Research: JMLR, 3(Jan), 993–1022
- Burdisso, S. G., Errecalde, M., & Montes-y-Gómez, M. (2019). A text classification framework for simple and effective early depression detection over social media streams. Expert Systems with Applications, 133, 182–197
- Cheung, C., Lee, Z. W. Y., & Chan, T. K. H. (2015). Self-disclosure in social networking sites. Internet Research. https://www.emerald.com/insight/content/doi/10.1108/IntR-09-2013-0192/full/html
- Cohen, S., Klein, D. N., & O’Leary, K. D. (2007). The role of separation/divorce in relapse into and recovery from major depression. Journal of Social and Personal Relationships, 24(6), 855–873.
- Cooney, G., Dwan, K., & Mead, G. (2014). Exercise for depression [Review of Exercise for depression]. JAMA: The Journal of the American Medical Association, 311(23), 2432–2433. cochranelibrary.com
- Gallagher, R. J., Reing, K., Kale, D., & Ver Steeg, G. (2017). Anchored Correlation Explanation: Topic Modeling with Minimal Domain Knowledge. Transactions of the Association for Computational Linguistics, 5, 529–542
- Greenglass, E., Fiksenbaum, L., & Eaton, J. (2006). The relationship between coping, social support, functional disability and depression in the elderly. Anxiety, Stress, and Coping, 19(1), 15–31. Gruda, D., & Hasan, S. (2019). Feeling anxious? Perceiving anxiety in tweets using machine learning. Computers in Human Behavior, 98, 245–255

## CREDITS 
This project was done in collaboration with one of my peers in academics and check out some of his works - https://github.com/skotak2
