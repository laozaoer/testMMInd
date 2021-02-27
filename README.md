# MMIntAdd: A Novel Minorize-Maximize Algorithm for Additive Risks Model with Interval-Censored Data


## Overview
The **MMIntAdd** package implements a novel minorize-maximize algorithm to estimate parameters of additive risks  model with interval-censored data. This algorithm can efficiently estimate the regression parameter and the cumulative hazard function simultaneously. The package takes advantage of C++ computational efficiency to reduce the computation time.

## Installation

Downlowd the compressed file *MMIntAdd_1.0.tar.gz* to the working directory and  use the following command to install it
```
install.packages("MMIntAdd_1.0.tar.gz")
```

## Example
There is an example to show how to use this package. First, use the following command to simulate data. Data simulating have a dependenciy [**nleqslv**](https://cran.r-project.org/web/packages/nleqslv/index.html).
```
# Load package
library(MMIntAdd)
```
### Scenario 1 (single time-independent covariate): <img src="http://chart.googleapis.com/chart?cht=tx&chl= \beta=0.5" style="border:none;">, <img src="http://chart.googleapis.com/chart?cht=tx&chl= X(t)=X" style="border:none;">

#### Simulate data:
```
set.seed(1)
Zt=function(X,t) X*t
Lambdat=function(t) 0.2*t
data=Data_generation(n=100,beta=c(0.5),Lambdat,Zt)
head(data)
     left.inspec right.inspec left.censoring interval.censoring right.censoring covariate_1
[1,]   3.2768387          Inf              0                  0               1           0
[2,]   1.3761127          Inf              0                  0               1           0
[3,]   0.0000000     1.035933              1                  0               0           1
[4,]   0.9769485     3.742266              0                  1               0           1
[5,]   3.8487090          Inf              0                  0               1           0
[6,]   0.0000000     1.983089              1                  0               0           1
```
This function generates a cohort with 100 subjects with a scalar time-independent covariate. The covariate for each subject is generated from Bernoulli(0.5) distribution. Users can user their own cumulative hazard function by changing the specific form of Lambdat. 

#### Estimate parameters:
The regression parameter and the cumulative hazard function can be estimated using the command
```
testresult=Main_func_ind(data,hn.m=1.5)
```
The output includes the estimate and the corresponding standard error for the regression parameter, estimate for the cumulative hazard function and the log-likelihood value.


### Scenario 2 (single time-dependent covariate): <img src="http://chart.googleapis.com/chart?cht=tx&chl= \beta=0.5" style="border:none;">, <img src="http://chart.googleapis.com/chart?cht=tx&chl= X(t)=X\exp(t)" style="border:none;">
#### Simulate data:
```
set.seed(2)
Zt=function(X,t) X*(exp(t)-1)
Lambdat=function(t) 0.2*t
data=Data_generation(n=100,beta=c(0.5),Lambdat,Zt)
head(data)
     left.inspec right.inspec left.censoring interval.censoring right.censoring covariate_1
[1,]   0.0000000    1.6873373              1                  0               0           0
[2,]   0.0000000    1.0261550              1                  0               0           1
[3,]   0.0000000    0.9221906              1                  0               0           1
[4,]   0.0000000    1.7733140              1                  0               0           0
[5,]   0.0000000    1.5533323              1                  0               0           1
[6,]   0.2042359    3.4580896              0                  1               0           1
```
This function generates a cohort with 100 subjects with a scalar time-dependent covariate. The covariate for each subject is generated from Bernoulli(0.5) distribution. Users can user their own cumulative hazard function by changing the specific form of Lambdat. 

#### Estimate parameters:
The regression parameter and the cumulative hazard function can be estimated using the command
```
testresult=Main_func_Expt(data,hn.m=1.5)
```
The output includes the estimate and the corresponding standard error for the regression parameter, estimate for the cumulative hazard function and the log-likelihood value.



### Scenario 3 (two time-independent covariates): <img src="http://chart.googleapis.com/chart?cht=tx&chl= \beta_1=0.5" style="border:none;">, <img src="http://chart.googleapis.com/chart?cht=tx&chl= \beta_2=1" style="border:none;">, <img src="http://chart.googleapis.com/chart?cht=tx&chl= X(t)=X" style="border:none;">


#### Simulate data:
```
set.seed(3)
Zt=function(X,t) X*t
Lambdat=function(t) 0.2*t
data=Data_generation(n=100,beta=c(0.5,1),Lambdat,Zt)
head(data)
     left.inspec right.inspec left.censoring interval.censoring right.censoring covariate_1 covariate_2
[1,]    1.729597          Inf              0                  0               1           0           1
[2,]    0.000000     1.642734              1                  0               0           1           1
[3,]    0.000000     1.257545              1                  0               0           0           0
[4,]    0.000000     1.136453              1                  0               0           0           1
[5,]    0.000000     1.736199              1                  0               0           1           1
[6,]    0.649395     2.807536              0                  1               0           1           0
```
This function generates a cohort with 100 subjects with two time-independent covariates. The covariates for each subject are generated from Bernoulli(0.5) distribution. Users can user their own cumulative hazard function by changing the specific form of Lambdat. 

#### Estimate parameters:
The regression parameter and the cumulative hazard function can be estimated using the command
```
testresult=Main_func_ind(data,hn.m=1.5)
```
The output includes the estimate and the corresponding standard error for the regression parameter, estimate for the cumulative hazard function and the log-likelihood value.

