# TwitterBotDetection 
Implementation of a GCN for Twitter Bot Detection. Unique from existing scholarship, this methodology includes the use of user meta information in the graph network, as well as a distinction of relationships (tweets) between the users and bots. Through the use of different graph aggregation algorithms, we will be able to distinguish between users and bots via node classification.

## Overview
The following sequence of Jupyter Notebooks serve as the methodology for our research procedure.

1. `FeatureEngineeringStratifiedSampling.ipynb`
- Due to the sheer size of our datasets, we were required to import our datasets into MongoDB and query from the 9 tweet json files from the database.
- We utilised a disproportionate stratified sampling methodology to obtain a sample of bot and human accounts.
- We engaged in a series of Feature Engineering and Feature Learning steps by incorporating domain knowledge.
**Note**
This `FeatureEngineeringStratifiedSampling.ipynb` notebook is a script that allows us to create a single user and graph CSV from a single tweet dataset
As a team, we were assigned with the respective tweets datasets and queried them into 9 separate files.

2. `Feature_Selection.ipynb`
- There were a total of 9 tweet files within the dataset containing tweet, retweet and post information between users
- After sampling from each of those tweet files, and engaging in Feature Engineering, we collated the relevant CSVs and aggregated them in `Feature_Selection.ipynb`
- In addition to this, we utilised Feature Selection to select useful features (wrt the model) and did Exploratory Data Analysis to come to a concerted decision on whether to retain the features.

3. `Model Training.ipynb`
- After identifying the top 10 useful features, we were able to utilise them in training our models for Baseline GCN, Graphsage and GAT
- Classical Machine Learning methods were also used to train on the same dataset to allow for a meaningful comparison at the end of the study

4. `Explainable.ipynb`
- After training the models, we were able to identify the false positives and false negatives and we attempted to cluster the bots to decipher the reasons why they were misclassified

5. ``
- A list of common words that should have been stop words but are not included in the library

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