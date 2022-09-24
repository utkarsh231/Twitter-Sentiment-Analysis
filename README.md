# Twitter-Sentiment-Analysis

## Problem Statement

This project aims to perform different text cleaning techniques to extract relevant 
information from the Tweets. Given a message and an entity, the task is to judge the 
message's sentiment about the topic. 


## Dataset

[Dataset Link on Kaggle](https://www.kaggle.com/datasets/jp797498e/twitter-entity-sentiment-analysis) 

- The dataset contains 74682 rows and 4 columns. 
- I have renamed the dataset’s column to {0:’Tweet_ID’, 1:’Topic’, 
2:’Sentiment’, 3:’Tweet’} to get a better sense of the data. 
- As the name suggests ‘Tweet_ID’ feature contains the tweet’s ID. 
The ‘Topic’ feature gives the topic of the tweet. 
The ‘Tweet’ feature contains the tweet’s contents. 
- The target feature ‘Sentiment’ has four classes namely ‘Positive’, ‘Negative’, 
‘Neutral’, and ‘Irrelevant’

![1_2IEsNGad_0k1cfUaKA6TJA](https://user-images.githubusercontent.com/57147530/192115276-f1231081-0139-4ce8-bf8b-089d98f65595.png)

## EDA

0.9% of the ‘Tweet’ feature contained null values. So we have dropped the null 
values. 
The features had correct data types. So there is no need to change them. 
![1_3KAt86Mjmfof86i4cfUJtw](https://user-images.githubusercontent.com/57147530/192115293-2560da51-29c6-48ef-b488-6e3c002c69be.png)

Distinct values in the ‘Topic’ feature are
![1_TMyETlh-yk3FkGVuIXY1Pw](https://user-images.githubusercontent.com/57147530/192115289-1b307ceb-a9d8-4e38-87a9-c9c2cc732926.png)


Next, we will try to analyze the distribution of tokens in each tweet. To do this, a new 
feature named ‘Tweet_word_count’ has been created which contains the total number 
of tokens/words in each tweet. 

![1_SoOXwZsKXzYCdCSaLtJcKg](https://user-images.githubusercontent.com/57147530/192115343-bcb331b8-0c54-4980-906b-9359d14a1a2f.png)

From the above plots, it can be observed that the mean number of tokens is around 23 
in each tweet. The boxplot shows that there are some extreme outliers and the 
histogram shows that the data is positively skewed. 

After removing whitespaces, the graph is:

![image](https://user-images.githubusercontent.com/57147530/192115399-ecebbd19-5eb8-432e-bcf0-795e5800ecd7.png)


# DATA PREPROCESSING

In this section, the main task is to clean the ‘Tweet’ feature in order to extract 
important information from it using regular expressions. 

 ### Removing Usernames
 
 User mentions start with ‘@’. We will replace all the words that start with the ‘@’ symbol followed by alphanumeric characters until whitespace with whitespace.
 
### Removing Hashtags

Tweets contain ‘#’ to better classify the content. We will replace the hashtags with whitespaces. 

### Removing Contractions

“Don’t” or “could’ve” are examples of contractions. Such contractions will be 
replaced with the whole word. Eg: “Don’t” will become “Do not” and “could’ve” will 
become “could have”. 

### Removing Hyperlinks

Hyperlinks or URLs starting with ‘http’ followed by alphanumeric characters will be 
removed from the text. 



## WORDCLOUD


![1_YhObDbqOkgWlRhuSVnSNVA](https://user-images.githubusercontent.com/57147530/192115464-e409653d-42fc-4114-a84f-ee34e7f5b36f.png)

# MODEL BUILDING 

In this part, we will first separate the dependent and independent features and then 
perform a train-test-split to generate training and validation sets. 

Output => Train (51797, 4) (51797, ) 
 Test (22199, 4) (22199, ) 

TF-IDF vector has been used to generate the Bag of Words from the cleaned tweets. 
TF-IDF score is higher for terms that occur quite often in a document but are not 
present in most of the other documents. Similarly, the score is lower for terms that 
occur frequently in most of the documents. 
Output (Shape after creating bag of words using TF-IDF): ((51797, 7670), 
(22199,7670)) 

## MODEL SCORES 
### Model 1: Multinomial Naive Bayes

-Accuracy score: 0.6447137258435065 
-Weighted F1 score: 0.6339980772017713 

### Model 2: Logistic Regression

Accuracy score: 0.6965629082391098 
Weighted F1 score: 0.6930624787458346 

### Model 3: Decision Tree

Accuracy score: 0.7626019190053606 
Weighted F1 score: 0.7622672223768574 

### Model 4: Random Forest

Accuracy score: 0.857741339699864 
Weighted F1 score: 0.8577394763372356
