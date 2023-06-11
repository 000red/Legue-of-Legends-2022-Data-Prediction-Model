# Legue of Legends 2022 Data Prediction Model


## Problem Identification

Prediction Problem: The prediction problem is to determine whether a team will win or lose a game based on the gold difference and kills at 15 minutes.

Type: Classification

Response Variable: The response variable is the outcome of the game, specifically whether the team wins or loses.

Metric: The metric chosen to evaluate the model could be accuracy. Accuracy measures the proportion of correctly predicted outcomes (win or lose) over the total number of predictions. It is a suitable metric for this classification problem as we are interested in the overall correctness of the predictions.

Justification: The gold difference and kills at 15 minutes can provide valuable information about a team's performance and advantage in the early game. By considering these factors, we can make a reasonable prediction about the outcome of the game at an early stage. Accuracy is a commonly used metric for classification problems where the classes are relatively balanced. In this case, since we don't have information about the class distribution, accuracy provides a straightforward evaluation of the model's performance in predicting the game outcome. At the time of prediction, we would only have access to the gold difference and kills at 15 minutes. Other features or information that may become available later in the game, such as the overall game duration or additional events, should not be used for training the model or making predictions.
