# Project 3 - Reddit NLP
---


## Goal
  To see if there is a difference in the U.S and U.K legal systems, using the subreddits LegalAdvise and LegalAdviseUK.
  

## Data Used
- LemBothCom.csv

- stemBothCom.csv

- CleanBothCom.csv

Data Dictionary

| Variable                     | Definition                           |
|------------------------------|--------------------------------------|
| body                         | The text for the comment.            |
| created_utc                  | Epoch timestamp for the comment.     |
| subreddit                    | The subreddit the comment came from. |

## Gathering & Cleaning Data
    
  The data was gathered from the subreddits LegalAdvise and LegalAdvise UK. The pushshift api was used to collect comments from both subreddits. After collecting 5000 comments from both subreddits the process of cleaning the data was started, so the comments could be used in a model. 
  
  The biggest process in cleaning was to remove all moderator comments. Those comments were for making sure the subreddit stayed on topic and no rules were violated. Most of the moderated comments were automated and were removed from the data set. Any comment that had a post that was marked as removed or deleted was also taken out of the dataset.
  
  The whole dataset was put through a lemmatization and stemming process using sklearn. The dataset was put through each process individually and saved. I ended up with three different datasets, the original, lemmatized, and stemmed dataset. I wanted to test what effect each type of transformation would have on model accuracy.
  
## Regression Models

  I used a count vectorizer to transform my data into a sparse matrix. This allowed me to use the data to create a model. There were many models used with the data such as, logistic regression, decision trees, naïve bayes,  extra trees classifier, random forest classifier. I used gridsearch to try and find the best parameters. 
  
  A recurring theme with the models was they were all extremely overfit. Lowering the max features when using count vectorizer reduced how overfit the model was, but it also reduced accuracy. The max feature count of 4000 was the spot where you would lose more on accuracy than gain from a reduction to overfitting. Using english stop words while count vectorizing also reduced the overfit of the data. Using the stemmed transformation of the dataset also reduced overfitting. 
  
  The model that had the lowest overfit with a higher accuracy was naïve bayes. Other models were getting upper 90's on percent accuracy on the train data, but were only getting in the mid 70's for accuracy on test data. Naïve Bayes with just the default parameters was getting mid 80's for percent accuracy on tests and the mid 70's for percent accuracy on test data. After adjusting the alpha in the naïve bayes model to .2 I was able to get an 83% accuracy with the train data and a 77% accuracy on the test data.
  
## Model Metrics

  The model had an overall accuracy of 77% on test data, but the model was more efficient in predicting a comment coming from LegalAdvise as opposed to LegalAdviseUK. The model accurately predicted 90% of the comments that came from LegalAdvise, but correctly predicted 64% of comments that came from LegaAdviseUK. I believe this can be mostly explained by looking at the coefficients for each word. 

  The words that influenced a comment being predicted LegalAdvise had many words that were specific to the U.S. Words that were region spesifi like a city or a state, and words that were U.S. institutions, such as F.B.I. and D.E.A. The words that had the biggest impact on a LegalAdviseUK comment, had very few if any words that defined something that was specific to the U.K. This absence made it hard for the model to correctly predict a LegalAdviseUK comment.

## Conclusion
  The model had very few legal terms that were the top influencers on the model. The model was deciding on other factors when determining its prediction. This leads me to believe that how legal problems are solved are very similar. 

