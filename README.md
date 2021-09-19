
# Project 3: Reddit Classification for r/drizzy and r/kanye Comments
by Nati Marcus

## Problem Statement
As two of the most popular hip-hop artists of the past decade (or longer), Kanye and Drake have sparked debate over which artist is better, and if either is the best ever. Although Kanye fans might laugh at the idea that Drake may be the better artist and vice versa, the two fan bases might not be that different. In this study, I will be analyzing reddit comments on the Kanye subreddit (r/kanye) and the Drake subreddit (r/drizzy) to see if fans can be properly classified as Kanye fans or Drake fans. Using classification accuracy score, I will evaluate how well I can properly classify the comments in comparison to the baseline accuracy of 51%.

## Data Overview
Using Pushshift's Reddit API, I collected 21,300 observations from r/drizzy and 22,300 observations from r/kanye. These comments were then combined into a single dataset (with 43,600 observations) with four main columns: `body` (comment itself), `author` (username of commentor), `created_utc` (time stamp of reddit comment post), and `subreddit` (r/drizzy or r/kanye).

## Preprocessing
After merging the dataset, I utilized Regex's tokenizer to create tokens for each of the reddit comments. Then I used WordNetLemmatizer to create lemmas from the tokens. I filted out non-text lemmas that included empty space or emojis. I also cleaned tokens to remove tokens that contained numbers and tokens that contained more than two consecutive letter repeats. Lastly, I assigned a 1 to the subreddit column where the value was "Drake" and a 0 to the subreddit column where the value was "Kanye."


## Data Dictionary
|**Feature**|**Type**|**Dataset**|**Description**|
|----|----|----|----|
|**body**|*object*|Combined r/drizzy & r/kanye DataFrame|Text of subreddit comments from r/drizzy and r/kanye.|
|**author**|*object*|Combined r/drizzy & r/kanye DataFrame|Username of user that commented in either r/drizzy or r/kanye.|
|**created_utc**|*int*|Combined r/drizzy & r/kanye DataFrame|Unix time of when the comment was posted to either r/drizzy or r/kanye.|
|**subreddit**|int|Combined r/drizzy & r/kanye DataFrame|1 if comment was posted in r/drizzy and 0 if comment was posted in r/kanye.|
|**tokens**|object|Combined r/drizzy & r/kanye DataFrame|A list of Regex tokens from each comment.|
|**lemmas**|object|Combined r/drizzy & r/kanye DataFrame|A string of lemmas for each comment.|

## Analysis Overview
The modeling process was split into two main focuses: models with CountVectorization and models with TfidfVectorization. Within each of those focuses, four models were constructed: Random Forest, Support Vector Classifier (SVC), AdaBoost, and Naive Bayes. Various iterations of each model were conducted to test different hyperparameters. All models besides for AdaBoost were around 70%-71% accurate, with AdaBoost models being around 65% accurate.

## Conclusions and Recommendations
All of the models performed between 15%-20% better than the baseline score of 51%. The best model for the CountVectorized section was the Random Forest model. The best model for the TfidfVectorized section was the SVC model. While the models constructed performed better than the baseline, there is still room for significant improvement. The next step would be to dive deeper into the words being selected in the CountVectorizer and TfidfVectorizer to fine tune the models.
