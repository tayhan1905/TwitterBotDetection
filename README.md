# TwitterBotDetection 
Implementation of a GCN for Twitter Bot Detection. Unique from existing scholarship, this methodology includes the use of user meta information in the graph network, as well as a distinction of relationships (tweets) between the users and bots. Through the use of different graph aggregation algorithms, we will be able to distinguish between users and bots via node classification.

# Disclaimer
Due to the large volume of source and intermediary files, please download only these csv:
- `users.csv`
- `graph.csv`
- `label.csv`
- `bot_clusters_ids.csv` 

and run the following notebook to see the EDA, feature selection, model training and evaluation / analysis:
- `Step2_Feature_Selection.ipynb` (Part 1 has been commented out as the intermediary files, `users.csv` and `graph.csv`, have been provided)
- `Step5_Model_Training_Evaluation.ipynb`

The other notebooks are used to generate intermediary files and may not be runnable as they involve the use of MongoDB for querying of the original Twibot-22 dataset.

## Overview
The following sequence of Jupyter Notebooks serve as the methodology for our research procedure.

1. `Step1_Feature_Engeering.ipynb` (**We have ran this file to generate `user_0.csv to user_8.csv` and `graph_0.csv to graph_8.csv`, NO NEED TO RUN AGAIN**)
- Due to the sheer size of our datasets, we were required to import our datasets into MongoDB and query from the 9 tweet json files from the database.
- We utilised a disproportionate stratified sampling methodology to obtain a sample of bot and human accounts.
- We engaged in a series of Feature Engineering and Feature Learning steps by incorporating domain knowledge.
**Note**
This `Step1_Feature_Engeering.ipynb` notebook is a script that allows us to create a single user and graph CSV from a single tweet dataset
As a team, we were assigned with the respective tweets datasets and queried them into 9 separate files.

2. `Step2_Feature_Selection.ipynb` (**Run this file using `user_0.csv to user_8.csv` and `graph_0.csv to graph_8.csv` to see the output**)
- There were a total of 9 tweet files within the dataset containing tweet, retweet and post information between users
- After sampling from each of those tweet files, and engaging in Feature Engineering, we collated the relevant CSVs and aggregated them in `Feature_Selection.ipynb`
- In addition to this, we utilised Feature Selection to select useful features (wrt the model) and did Exploratory Data Analysis to come to a concerted decision on whether to retain the features.

3. `Step3_Bot_Clusters.ipynb` (**Cannot run this file as it requires querying from MongoDB**)
- Group bots into 5 clusters (save the `bot_clusters_ids.csv`) and obtained their tweets (generate a `cluster_<cluster_number>_<tweet_file_number>.txt`).
**Note**
This `Step3_Bot_Clusters.ipynb` notebook is a script that allows us to get the sampled bots and their tweets from all the 9 different tweet files from Twibot-22 through MongoDB

4. `Step4_Cluster_TFIDF` (**Uses the output files from `Step3_Bot_Clusters.ipynb`, DO NOT RUN, Open to see results**)
- Combined 9 sets of `cluster_<cluster_number>_<tweet_file_number>.txt` per clusters
- Retrieves top 30 important words from each bot cluster using TF-IDF and identify the type of bots in each cluster based on topic

5. `Step5_Model_Training_Evaluation.ipynb` (**Run this file using `users.csv`, `graph.csv`, `label.csv`, `bot_clusters_ids.csv`**)
- After identifying the top 10 useful features, we were able to utilise them in training our models for Baseline GCN, Graphsage and GAT
- Classical Machine Learning methods were also used to train on the same dataset to allow for a meaningful comparison at the end of the study
- After training the models, we were able to identify the false negatives (bots misclassified as humans) and we attempted to cluster the bots to decipher the reasons why they were misclassified
- We also run the model on 3 subset of features: all features, top 10 important features and the other features to observe if feature selection plays a part in the performance of our model

The following are the files we will be running in our ipynb (accessed via https://drive.google.com/drive/folders/1M2hYVr6cQhMAGIussXcbCtSjEUzWh1wM?usp=sharing)
1. `user_0.csv to user_8.csv`
- The csv contains sampled users and their extracted and original features from the Twibot-22 dataset
2. `graph_0.csv to graph_8.csv`
- The csv contains the source_user_id, target_user_id and the tweet from each of the 9 tweet JSON from the Twibot-22 dataset
3. `users.csv`
- Combined `user_0.csv to user_8.csv` that is used for feature selection and model training
4. `graph.csv`
- Combined `graph_0.csv to graph_8.csv` using aggregation that is used building our graph structure for GNN models
5. `label.csv`
- The label (human or bot) for each user_id
6. `cluster_stopwords.txt`
- A list of common words that should have been stop words but are not included in the library
7. `bot_clusters_ids.csv`
- Matches source_user_id that are bots to their corresponding bot cluster (0 to 4)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Requirements
-`numpy`

-`pandas`

-`matplotlib`

-`sklearn`

-`seaborn`

-`torch`

-`pymongo`

-`csv`

-`xgboost`

-`google.colab `