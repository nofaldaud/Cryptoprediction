# Cryptoprediction
Predicting if the BTC price will go UP or DOWN

The problem is how to predict whether the price of a given cryptocurrency will go up or down in next 1 hour and next 6 hours
given the historical price data.

This can be treated both as a classification problem or a regression problem. I have chosen to treat it as a regression problem and then
assgin the up or down labels based on comparison.

There are several ways to tackle time-series forecasting problems within machine learning. I chose to solve it the following way. I will just mention the major details of my solution.

## Time series prediction methodology
Two commonly used methods to tackle time-series forecasting problems are using periodic windows and the other is shifting the features dataset ahead in time.e.g.

                      time     feature1 feature2    target_variable
                      t-3       45        23            76
                      t-2       23        34            23
                      t-1 	    34        56            57
                      t         67        34            14

now shifting feature space only for t+1 prediction

                      time     feature1 feature2    target_variable
                      t-3       NaN       NaN           Nan
                      t-2       45        23            23
                      t-1       23        34            57
                      t   	    34        56            14
                      t+1       67        34            NaN

Now we have the Values of Features or X to predict y(t+1). I have followed this method.

## Feature Engineering
I have added a couple of statistical features to the original dataset to help increasing the accuracy of prediction.
The sine and cosine functions of the hour values are added to denote the high and low hours during the day
as business tends to do well during some particular hours and not so well during others.

the rolling standard deviation of the closing price is also added as as feature as well as the average price 
during the hour and the difference of opening and closing price.

Also the lagged closing prices are added as features.

## Model selection
I started from logistic regression and then iteratively increased the model complexity considering their corresponding 
accuracy. The state-of-the-art models used in the area of financial and stock market prediction (quite similar to this problem)
are mostly Deep learning methods exploiting artificial neural networks. LSTMs are considered to do particularly well for time series predictions.
However, I am not fluent with Neural networks yet, although I am working on it. So SVM was giving the best results in the models that I tried.

## Results
It can be seen in the graphs that the prediction is offset by an amount of roughly $1000. Best guess, this is due to some normalization
or scaling error. Apart from that the prediction graph is quite similar to the true values which works for this particular problem
because we only have to predict if the price is going to go up to down. The offset does not influence that.

## Miscellaneous:
I have not followed the part 2 of the task because I have not worked with those tools. Although, I know about them and believe that
they are not a big deal to learn to operate. But I just do not have time to do that at the moment.
