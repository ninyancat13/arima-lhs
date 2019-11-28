# arima-lsd
Replication of a study by Kandanamond (2013) using factorial design and Latin Square Design. 

Two simulations were conducted under the ARIMA model: ARMA (stationary) and the IMA (non-stationary). In the literature by Kandanamond (2013), once the dataset for both ARMA and IMA are obtained, the SVM and ANN methods along with the other AR and MA settings are applied to obtain the MAPEs (Mean Absolute Percentage Error).

## Recreated Experimental Results:
### Stationary:
The MAPEs recorded in the literature were duplicated for the purposes of the current study (with inversed MAPE values) and ANOVA was applied. After running the ANOVA, there is evidence to suggest that there exists a significant interaction effect between phi, theta and the method (ANN or SVM). Below are the ANOVA table output and the Main Effects Plot for stationary. The ANOVA table is identical to that shown in the literature for the stationary process.

<b>The literature failed to look at the assumptions of ANOVA.</b> Shapiro-Wilk test of normality of residuals shows that p = 0.1781 which is larger than 0.05. Thus, the assumption of normality of residuals has been met. Levene's Test of homogeneity of variance indicates that at 5% level of significance there is insufficient evidence (F(7,32) = 1.6237, P = 0.1645) to conclude that assumption of homogeneity of variance has been met. Thus all assumptions have been satisfied for the stationary case.

### Non-Stationary:
However, for the non-stationary data, the ANOVA table does not match that shown in the literature. There exists a significant interaction effect between theta and the method (ANN or SVM) when looking at the MAPEs.

Shapiro-Wilk test of normality of residuals shows that p = 0.008475 which is less than 0.05. Thus, the assumption of normality of residuals has not been met. Levene's Test of homogeneity of variance indicates that at 5% level of significance there is sufficient evidence (F(3,16) = 5.52, P = 0.008498) to conclude that the assumption of homogeneity of variance has been met.
The non-stationary data failed the Shapiro Wilk’s Test but passed the Levene Test when MAPE was inversed. However, this was not the case when the inverse was removed. Without inversed MAPEs, the dataset passed Shapiro Wilk’s Test but failed to pass the Levene’s Test (as shown in the Appendix). Other transformations such as square root, log, square, were also trialed but did not satisfy all assumptions. Thus it will be necessary to trial non-parametric model on the non-stationary data.

## Simulating using ARMA & IMA Models:
### Stationary:
ARMA model was used to simulate time series data based on random phi and theta values ranging from -0.9 to 0.9 as shown in the plot below. 51 values were simulated at one time, then the first 50 values were used to train the SVM model to predict the 51st value. MAPE was then calculated using the equation: |(actual - pred)/actual|. This model training was repeated 50 times using 50 sets of ARMA simulated values. The mean of the 50 MAPEs was then derived. This whole process was then repeated to produce 100 MAPE values in the end.

### Non-Stationary:
The process is identical to that discussed for Stationary but now only theta (from -0.9 to 0.9) is used to simulate the values using IMA. As can be seen, the majority of the differences between predicted MAPE values and actual values centre around 0, when using the Krigging model to produce new MAPE values for the stationary process. Thus the current model is not bad at predicting MAPE values - although note that there are also quite a few bad predictions.As can be seen, the majority of the differences between predicted MAPE values and actual values centre around 0, when using the Krigging model to produce new MAPE values for non-stationary process. However there is some skew to the left which may indicate that a transformation is necessary and it also exposes the fact that many of the predicted values are smaller than the actual value of the MAPEs.

## Optimality Criterion (LHS):
### Overall Methodology:
Firstly we generated the design for the Phi (AR) and Theta (MA) parameters using the maximin LHS criterion. We generated 100 pairs of phi and theta and simulated 100 sequences of time series data. Each sequence used to train the SVM to predict the last value in the sequence. This process was repeated 50 times (for each sequence out of the 100) to obtain the average of the SVM’s prediction MAPEs. We resulted in having 100 data points for both stationary and non-stationary processes. The non-stationary only required the theta parameter, so slight adjustments had been made.





