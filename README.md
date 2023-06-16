# Legue of Legends 2022 Data Prediction Model

by Redwan Ali (r1ali@ucsd.edu) and Nicholas Azpeitia (nazpeitia@ucsd.edu)

---

## Problem Identification

Prediction Problem: The prediction problem will determine whether a team will win or lose a game based on the gold difference and kills at 15 minutes into a League of Legends game.

Type: Classification

Response Variable: The response variable is the outcome of the game, specifically whether the team wins or loses.

Metric: The metric we chose to evaluate the model is be accuracy. Accuracy measures the proportion of correctly predicted outcomes (win or lose) over the total number of predictions. It is a suitable metric for this classification problem as we're interested in the overall correctness of the predictions.

Justification: The gold difference and kills at 15 minutes can provide valuable information about a team's performance and advantage in the early game. By considering these factors, we can make a reasonable prediction about the outcome of the game at an early stage. Accuracy is a commonly used metric for classification problems where the classes are relatively balanced. In this case, since we don't have information about the class distribution, accuracy provides a straightforward evaluation of the model's performance in predicting the game outcome. At the time of prediction, we would only have access to the gold difference and kills at 15 minutes. Other features or information that may become available later in the game, such as the overall game duration or additional events, should not be used for training the model or making predictions.

---

## Baseline Model

For our baseline model, we utilized a random forest classifier to predict which team will win based on the features 'killsat15' and 'golddiffat15'. These features are quantitative, representing numerical values. We didn't perform any explicit encoding in the given code, since our League of Leagends Competive data from 2022 already contains numerical values for these features.

The performance of our model has an accuracy of approximately 65%. Additionally, the precision, recall, and F1-scores for both classes ('0' and '1') are quite similar, indicating a balanced performance across the classes. We believe our model is good as it's prediction is better than 50%, but it can still be improved upon.

---

## Final Model

For the final prediction model, in addition to the original features 'killsat15' and 'golddiffat15', we added interaction and polynomial features using the PolynomialFeatures transformer. This way we can capture potential nonlinear relationships and interactions between the existing features. By including interaction terms, we can account for complementary effects between 'killsat15' and 'golddiffat15', which could be influential in determining the game outcome. These added features provide a more flexible representation of the data generating process and improves the model's performance in capturing complex patterns.

The modeling algorithm we chose in this case is the Gradient Boosting Classifier, which is known for its ability to handle complex relationships and perform well in various prediction tasks. We used hyperparameter tuning using RandomizedSearchCV to find the best combination of hyperparameters. The ones that performed the best are a learning rate of 0.01, 100 estimators, and a maximum depth of 3.

The final model's performance demonstrates improvement over the baseline model. The final model achieves an accuracy of approximately 73.3%, which is higher than the baseline model's accuracy of 65%. The precision, recall, and F1-scores for both classes are also improved compared to the baseline. This improvement can be attributed to the inclusion of interaction and polynomial features, as well as the optimized hyperparameters of the Gradient Boosting Classifier. Overall, the final model better captures the complexities in the data generating process, leading to more accurate predictions and a more balanced performance across classes.

---

## Fairness Analysis

In order to perform a fairness analysis, we chose group X to represent matches that had a significant gold difference at 15 minutes, specifically with a threshold of 3000 gold difference. Group Y represents matches with a gold difference at 15 minutes that is not considered significant (less than or equal to 3000 gold difference).

The evaluation metric we chose for this analysis is precision, which measures the proportion of correctly predicted positive instances (matches won) out of all instances predicted as positive.

Our null hypothesis is that our model is fair, meaning its precision for matches with a large gold difference at 15 minutes is roughly the same as matches without a significant gold difference. The alternative hypothesis states is that our model is unfair, indicating that its precision for matches with a large gold difference at 15 minutes is significantly different from matches without a significant gold difference.

To test these hypotheses, we performed a permutation test. The observed difference in precision between Group X and Group Y is calculated. Then, the labels are shuffled and new precisions are calculated for each group, creating permuted differences. This process is repeated 1000 times to create a distribution of permuted differences. The p-value is calculated as the proportion of permuted differences that are as extreme as or more extreme than the observed difference.

The resulting p-value is approximately 0.001, which is lower than the significance level of 0.05. Therefore, we reject the null hypothesis and conclude that there is a statistically significant difference in the model's performance for matches with a high gold difference and those without. However, it's important to note that statistical tests alone cannot provide definitive conclusions, as we are limited by the nature of observational data and statistical inference.
