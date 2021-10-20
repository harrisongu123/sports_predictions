# Betting Against Vegas

## Author: Harrison Gu

## Overview

As the sports betting industry is gaining steam, we are interested in selling NBA spread picks to sports bettors via subcription to our service. We will use regression models to predict outcomes of NBA games. Our goal is to make a prediction on the spreads (point differential) of each game, and use that information to bet against the Vegas spread. Because Vegas typically takes a 10% rake for each bet, we have to be able to beat Vegas 52.5% of the time in order to be profitable.

## The Data

Our data was collected via scraping, using Beautiful Soup, basketball-reference.com and sportsbookreviewonline.com. We used data from all regular season games from 2011-2020, which includes 11,656 games. The NBA game has changed dramatically since the early 2000s, in that 3 point shooting has become a much more critcal part of the game. In order to train an accurate model for today's game, we made the decision to not include games from the 2000s.


## Modeling

For our first round of modeling, we casted a wide net, running 8 different machine learning regression baseline models. From there, we chose the 3 best performing models, determined by lowest RMSE while keeping training and testing RMSEs as close as possible. These models were linear regression, random forest, and gradient boost. From there, we tuned each model using gridsearch to determine optimal parameters. All 3 of our optimized models topped out at 61.5%-62.5% accuracy against the Vegas spread. We believe that this could be due to the true randomness of sports in general. 

Additionally, we also ran a neural networks regression model, and tuned parameters using Talos. Again, the model topped out around 62.3%.

In an effort to increase our prediction accuracy, we tried to create ensemble models. Our method was to only make predictions when all 4 of the regression models agreed on the same side of the bet. This increased our accuracy to 69.1%, and included 62.28% of games. While this is a dramatic increase in accuracy, we would like to be able to make predictions on a higher percentage of games. Diving futher, we found that when only 3 models agreed with each other, the accuracy was between 51.8%-54.1% depending on which model disagreed. Because of the 52.5% threshold to be profitable, we cannot use predictions when the random forest disagrees with the others, as those predictions are only 51.8% accurate. However, when linear regression, gradient boost, or neural networks disagree, the predictions are still useable. This increases the percentage of useable predictions to 81.5% of all games!



## Analysis

The next trend that we explored was the absolute difference between our predicted spreads and Vegas' spread. We found that the bigger the discrepency, the more accurate our model was. This pattern will help us rank our picks based on how confident we are in them, which is important to bettors, as it allows them to size their bets appropriately. Interestingly, when our model is more than 10 points away from the Vegas spread (0.5% of games), it predicts games at >90% accuracy.

We believe that this could be due to Vegas' business model. Their goal is to set a line such that exactly 50% of bettors take each side, and just collect the 10% juice with 0 risk. If the public opinion differs from the "true" spread, Vegas will move their line away from their original prediction, closer to the public average. When the public opinon is vastly different from the "true" spread, our model will we able to pick the correct side more frequently. 


## Final Outcome

Our final model will be able to make useful predictions on 81.5% of games, at a weighted average accuracy of 65.2% of games. For the remaining 18.5% of games, we will refrain from making any predictions. This yields an expected value of 0.239, meaning for every $1 bet using our model, the bettor is expected to make ~$0.24. Based on our research, the average sports bettor bets $216 per month. This means that our model gives the average sports bettor $51.84 of value per month. Because our target audience are serious bettors, we will price our montly subscription at $50/month. 