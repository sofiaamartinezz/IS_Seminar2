# Emotion Classification in Tweets

**Authors**: Sofía Martínez Pastor and Milan Ehret

This project aims to classify emotions in tweets using **Machine Learning** techniques. The provided dataset contains tweets labeled with one of six emotions: 0 - sadness, 1 - joy, 2 -love , 3 - anger, 4 - fear, 5 - surprise.

### Objectives

- **Emotion Classification in Text**: Train and evaluate classification models capable of detecting the emotions present in the tweets.
- **Implementation of Multiple Models**: Compare the performance of different classification algorithms.
- **Hyperparameter Tuning**: Fine-tune the models' hyperparameters to improve performance.

### Task 1 - Data preparation and exploration

We started by exploring the data.

![Emotions distribution](graphs/data_distribution.png)

We have some imbalance on the emotions. This can affect model performance, as models might be biased towards the most frequent classes. So it can be much more useful to evaluate additional metrics like F1-score or the confusion matrix to get a more complete view of how the model is classifying emotions, especially for underrepresented classes.

![Text length](graphs/data_distribution.png)

 The length of the text can affect the vectorization process. And, as we can see in the graph, most texts cluster around the 50-75 character range, with a gradual decline in frequency for longer texts. So we used TF-IDF to normalize this by down-weighting terms that appear very frequently across all documents. This normalization helps prevent overly frequent terms from dominating the model, giving better feature representations. So our texts now look like this:

 ![Text vectorized](graphs/tf_idf_vectorizer.png)


### Models Implemented

The project includes several classification models, including:

- **KNN (K-Nearest Neighbors)**
- **SVM (Support Vector Machine)**
- **Decision Trees**
- **Random Forest**
- **Bagging**
- **Gradient Boosting**


