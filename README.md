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

![Text length](graphs/text_length.png)

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

We first compare the accuracy of the diffent models to select a few that we will imporve furhter.

![Models Accuracy](graphs/accruracy_base.png)

![Models Accuracy with half the Dataset](graphs/accruracy_base_half.png)

![Models Accuracy difference](graphs/accuracy_comp.png)

Note: Bagging and Radnom Forest need bigger amounts of data for tuning more paramaters (multiple models/Trees) so have the biggest loss with reduced dataset.

## Cross validation and Hyperparameter Tuning
We will implement cross validation and Hyperparameter tuning for selected base models which already show promissing results (hight accuracy and consistent confussion matrix) so:  
**KNN**  

![K-Nearest-Neightbour](graphs/hp_cv_knn.png)

As we can see KNN with K = 7 produces the best results. Even better then the Base KNN Clasifier because of Cross-Valdiation.  

**Random Forest**   

![Random Forest](graphs/rf_accuracy.png)

Grid search produces best results because it has overview over all options and Random Search dosent find the good Options in this instance so the Result is lower than the base Classifier.

Grid Search:

| Hyperparameter    | Best Value    |
|-------------------|---------------|
| criterion         | gini          |
| max_depth         | None          |
| min_samples_leaf  | 1             |
| max_samples_split | 30            |
| n_estimators      | 100           |


Radom Search:  

| Hyperparameter    | Best Value    |
|-------------------|---------------|
| max_features      | log2          |
| max_depth         | None          |
| n_estimators      | 50            |

The main diffence is in the number of Estimators choosen so the lower score makes sense because with a lower amount of trees the Forest cant capture as many relations in the data.

**Bagging**  

![Bagging](graphs/bc_accuracy.png)


### Advanced Machine learning

We tried two approaches:

- **Mixing KNN, BaggingClassifier and RandomForest.** We prepared the data with the TF-IDF vectorizer. Gave 70% to RandomForest, 20% to BaggingClassifier and 10% to KNN.

- **Deep Neuronal Network**. We prepared the data with Tokenizer(max_words), texts_to_sequences and pad_sequences and we also prepared the target column with to_categorical.

Also, when splitting the data with train_test_split we used stratify=df_balanced["label"] to keep into account the imbalance between classes.

We tried multiple approaches without getting good results and lots of overfitting until we realized that the problem was focused on the labels with not that much data so we decided to use the amplified HuggingFace dataset and that's when we started getting nice results, especially with the neural network.

Also, this is the classes distribution of the large dataset so we decided to downsize labels 0 and 1 to 60000.

![Text length Large Dataset](graphs/text_length_large_ds.png)

Now, we didn't get quite good results for the Mixing models as it was not capable of predictin the minority classes. This is the code we used:

![Mixing models code](graphs/mm_code.png)

And for the Neural Network we decided to use this structure:

![Structure Neural Network](graphs/nn_model.png)

And got this result:

![Neural Network Results](graphs/nn_results.png)

And the learning and loss curves:

![Neural Network Graphs](graphs/nn_graph_results.png)






