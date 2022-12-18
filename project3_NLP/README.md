# Project 3  - Natural Language Processing

Reddit has decided to change their business model by becoming the

world\'s top conversation platform.

Reddit now want to display organic conversations from its members, but
also any publicly available conversation on the internet, and classified
it under one of its existing subrredits.

They have hired us to run a \"stage 0 testing\" to evaluate whether such
an algorithm would even be effective based sources from reddit itself,
let alone importing from other sources.

**The aim of our project is to create and train a model that can
correctly classify a corpus into its correct subreddit**

We want to be mindful about sentiment analysis and will create a
sentiment filter category that future reddit users will be able to use
to filter for each post.

**We have decided to work on Starbucks and DunkinDonuts subreddits**

![1664586209724](image/README/1664586209724.png)

![1664586223900](image/README/1664586223900.png)

**Notebook structure and plan**

We have structured the project on **3+1 notebooks**:

1. Data gathering
2. EDA, preprocessing
3. Modeling and recommendations
4. --Appendices, attempt at puttin the model on streamlit--

### `1.Gathering data`

Was done using reddit API, scrapping over 6000 posts for each
subreddit ; After aggregating, we cleanse the data to prepare
the EDA: lower case, removing emojis, removing empty / low infrmation
posts

### `2.EDA`

The EDA section aims at understanding what are our posts made of: what
are the most occuring words, the length of our posts.

We also looked at the impact of removing stop words on the most occuring
words, as well as lemmatizing to trim the text even further. We explored
the impact of lemmatizing + CountVectorizer applied on the corpus vs
lemmatizing + TF-IDF. **We could not conclude and decided to test both
options on the modelling phase**

Starbucks and Dunkin donuts are quite similar in top 50 top words with a
striking difference: Starbucks tends to talk more about \"work\" topics

Distribution of posts length in subreddits

![1664586247727](image/README/1664586247727.png)

![1664586270163](image/README/1664586270163.png)

### `3.Modeling`

After lemmatizing the corpus, we evaluated 7 models:

1. Baseline score (tf-idf mNB) non-tuned by GridSearch
2. Random forests (tfidv)
3. Random forests(cvec)
4. NaiveBayes (tfidf)
5. NaiveBayes (cvec)
6. Logistic Regression (tfidf)
7. Logistic Regression (cvec)

We gathered the following classificatons metrics: **Accuracy (the most
important one)**, precision, recall, F1-score and ROC-AUC
We were able to generate the following recap table and see the
superiority of LogisticRegression model to achieve this task

![1664616049154](image/README/1664616049154.png)

Our best model AUC-ROC Curve:

![1664586297133](image/README/1664586297133.png)

### `Conclusion`

We have a solid classifier to identify between 2 posts `<br>`{=html}
**However,** being able to accurately classify a post coming from
anywhere on the internet into the right subreddit will prove way more
difficult:

**Problems that we may encounter could be of different nature**. For
example, which level of aggregation should a post be classified into?
(example: Dunkin? Starbucks? or \"Coffee?).

What if a post on Russia\'s war on Ukraine ends up classified in a
random subreddit? We should probably consider an option for
users to re-classify posts

This project is not realistic given the quantity of data to scrape and
aggregate. But we could start such a project if we identify 1 partner that would be ok to let us aggregate their content into our platform. This would ensure some data quality and would
narrow the scope of work.

### `Recommendations`

We can use Logistic Regression as our weapon of choice to allocate
subreddits with satisfying accuracy.  We can add on
Sentiment Analysis feature to ease the navigation inside a subreddit for
HR \| marketing business development teams

### `Next steps`

To improve our modeling performance we could consider the following
steps:

**Gathering more data** - fine tune model and enable time-series
analysis

**Text-pre-processing steps**

- Removing Contractions
- Removing special characters

**Improving on our models training** ( Gridsearch/ vectorizers etc...)

**Testing other models**

- SVM
- KNN
- Boosting
- ExtraTrees
