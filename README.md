# Predicting Brazil's retail trade sales time series in R
In this work, i'll analyze the retail trade sales in brazil from **2012** to **2022** and choose the best fit model to predict 2023 sales.
####
#### 1. Taking a look at the time series
![alt text](images/image1.jpeg)
######
Analyzing the plot of the series, we can easily visualize that it has a seasonality (S = 12). Then we can try a SARIMA $$(p,d,q)(P,D,Q)_{S}$$ model in this case.
######
#### 2. Testing the equality of variances with the Levene's test
Even though the series seems to have a constant variance, we still should do the Levene's test to check the variance equality through the series.
- **$$H_{0}: \theta_{1}^{2}=\theta_{2}^{2}=...=\theta_{k}^{2}$$,**
- **$$H_{1}: \theta_{i}^{2}\neq\theta_{j}^{2}$$ for at least one pair $$(i,j)$$.**
######
Testing the hypothesis for $$k=2$$ (dividing the series in half), it resulted in a p-value of **$$0.6758$$**. It means that we didn't find evidences that the variances of the two groups are different from each other.
######
#### 3. Analyzing the ACF and PACF plots
![alt text](images/image2.jpeg)
![alt text](images/image3.jpeg)
######
#### 4. Trying to figure out the parameters.
######
To get rid of the seasonality peaks we can take one difference of the seasonality part (D = 1).
######
![alt text](images/image4.jpeg)
######
The resulted plot is indicating to us that the series is non-stationary. A simple differencing, d = 1, may estabilise the series.
######
![alt text](images/image5.jpeg)
######
Now with the series stabilised, let's take a look on the resulted ACF and PACF plottings.
######
![alt text](images/image6.jpeg)
![alt text](images/image7.jpeg)
######
The plottings are indicating to us that we may choose one of the models below:
- SARIMA $$(0,1,0)(1,1,0)_{12}$$,
- SARIMA $$(0,1,0)(0,1,1)_{12}$$,
- SARIMA $$(0,1,0)(1,1,1)_{12}$$,
- SARIMA $$(1,1,1)(1,1,0)_{12}$$,
- SARIMA $$(1,1,1)(0,1,0)_{12}$$,
- SARIMA $$(1,1,1)(1,1,0)_{12}$$.
######
Talking about the models selected, since both ACF and PACF are truncated in lag 12, we should test models with P = 1 only, Q = 1 only and one with the combination of both P = 1 and Q = 1. The models with p = 1 and q = 1 are in the list just because it's complex to really identify them, so we are testing to see if they can have better results than the models with p = 0 and q = 0.
######
#### 5. Choosing the model.
######
