# Minimum Viable Product
## Disney Movie Marathon: What are we watching next?

The goal of this project is to create a recommendation system to make a movie recommendation based on the favorite Disney movies of two different users.

To do this, I am using movie summaries from [_Disney A to Z_](https://d23.com/disney-a-to-z/)&mdash;which generally include a brief plot overview, award highlights, character names, and actor credits (longer than 100 words, on average)&mdash;for every movie produced and released by Walt Disney Productions. The data consist of over 2100 movies, spanning films released during the 1920s (Walt Disney's _Alice Comedies_) through early 2020 (Pixar's _Onward_).



To begin building a classification model, I create baseline models with just the acceleration, braking, and speeding scores as features, using KNN, logistic regression, decision tree, and Random Forest. The KNN, decision tree, and Random Forest models (all have F2 > 0.91) perform marginally better than the logistic regression model (F2 ~ 0.85), so I have dropped the logit model from further consideration.

In expanding and refining these three models (KNN, decision tree, Random Forest), I have added all drive specific features (scores for acceleration, braking, turning, weaving, drifting, speeding, and following), as well as a dummy variable for day- vs. night-time driving. For each of these models, I run GridSearchCV over:
- KNN: _k_ from 3 to 100, with a step size of 2
- DT: _max_depth_ from 5 to 20; _min_samples_split_ from 2 to 10; _min_samples_leaf_ from 1 to 5; _criterion_ as entropy or gini
- RF: _max_depth_ from 5 to 20; _criterion_ as entropy or gini; _max_features_ as auto, sqrt, or log2

The figure below shows the ROC curve (based on the validation set) for the best estimator for each model type. Note, the _x_- and _y_-axes are formatted to show the upper left corner of the typical ROC curve; in this project, the AUC is large (approaching 1) for all three models, so to see the slight differences between the model, we need to zoom into this part of the plot.

<p float="left" align="center">
  <img src="roc_curves_base.png" width="500" />
</p>

These results show that the Random Forest model (AUC = 0.988, F2 = 0.983) performs very well on the validation set; I have dropped the KNN and decision tree models from further consideration. As a next step, I plan to test a gradient boosted tree model (e.g., XGBoost) to compare with the Random Forest model.
