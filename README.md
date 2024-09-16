# trading-strategies

Data: 

      NYU_USD_JPY_2016.csv

      NYU_XAU_USD_20142015.csv
      
Trading Strategy:

Momentum strategy with two protection.

First, we calculate the rolling 7-days asset return R, and we will take beta=R exposures to this asset. 
R is updated hourly, which means we rebalance hours.

Because the underlying assets are quite volatile sometimes, we use two ways to create protection for our strategy. 
The first one is using Flow. For XAU, we will take beta = -(current Flow – Threshold) exposures to the underlying asset. 
The Threshold for XAU is 1.7 and for JPY is 1.4. 
So, when there is significant more long position than short position, we will cut our exposure to prevent unexpected unwinding and vice versa.

For the second protection, we utilized the idea from neural network active function: tanh. 
It will help us to compress our position into [-1,1]. 
As a result, when our signal’s values are too high or low, we will cap our exposure’s absolute value to 1. 
Also, even when the raw absolute value is higher than 0.5, we will increase our exposure slowly. 
You can regard this as the conservative investment. But it can help this strategy endure wider spread by reducing rebalanced exposure.
