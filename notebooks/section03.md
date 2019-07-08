# Section 3: Recommender System

### Time Taken 56 Minutes

**Answer 1**: I would explore collaborative filtering methods to solve this problem. Reason being, this method allows using products as features to users, hence making it easy to identify products to recommend to similar users. My preferred model in this case would be *k*-Nearest Neighbors as it intuitively predicts the most similar *k* products. The pros and cons of this model are:

| Pros | Cons|
|------| -----|
| Non-parametric making it easy to retrain with more Interactions| Predictions are computationally expensive and take longer time to make |
| Easily interpretable and quantifiable by examining cosine similarity | The users x products matrix will be very sparse |
| Transferable from store to store as additional columns and rows can be appended | Feature scaling is necessary to make products comparable |

**Answer 2**: Given a matrix factorization model, I would address sub-issues in the following manner:

- To avoid over-fitting, I would separate out the Interaction table into Train (60%), Validation (20%) and Test (20%) sets. Then I would use regularization on latent factors on the validation set to ensure that my results are not over fitting. After identifying the optimal regularization penalty, I would evaluate it's performance on the test set.

- For outliers, I would use Principal Component Analysis (PCA) to reduce dimensionality as a means to identify outliers. The maximum variance calculated for each component would help detect values that lay further away from the IQR.

- The cold start problem can be solved by feeding the features of shoppers and products into a classification algorithm to predict a favorable outcome, i.e. sale, or not.

- I would propose starting with a simple linear regression model that uses ratings and the shoppers and products attributes with a response variable of purchase count. This model has the advantages of interpretability and ability to tackle earlier mentioned issues of outliers and cold start.

**Answer 3**: In order to make recommendations efficient, I would adopt the same strategy as section 2 where products can be filtered primarily on `Type` and `Size`. Additionally, I would factor in the time period between `Click Process` and `Purchase Process` dates to ensure that the customer is looking for similar items in a given timespan. Based on filtered values, I would rank relevance on further product and shopper attributes.
