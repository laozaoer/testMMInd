# MMIntAdd: A Novel Minorize-Maximize Algorithm for Additive Risks Model with Interval-Censored Data


## Overview
The **MMIntAdd** package implements a novel minorize-maximize algorithm to estimate parameters of additive risks  model with interval-censored data. This novel algorithm can efficiently estimate the regression parameter and the cumulative hazard function simultaneously. The package takes advantage of C++ computational efficiency to reduce the computation time.

## Installation

Downlowd the compressed file *MMIntAdd_1.0.tar.gz* to the working directory and  use following command to install it
```
install.packages("MMIntAdd_1.0.tar.gz")
```

## Example
There is an example to show how to use this package. First, use following command to simulate data. Data simulating have a dependenciy [**nleqslv**](https://cran.r-project.org/web/packages/nleqslv/index.html).
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
This is the cumulative hazard function, Users can use their own Lambdat by changing the specific form. 
data=Data_generation(100,c(0.5),Lambdat,Zt)
```
This function generates a cohort with 100 subjects with a scalar covariate. The covariate for each subject is generated from Bernoulli(0.5) distribution. Users can user their own cumulative hazard function by changing the specific form of Lambdat. 

#### Estimate parameters:
The regression parameter and the cumulative hazard function can be estimated using the command
```
testresult=Main_func_ind(data$X,data$Delta,data$Inspec,data$mimic,1.5,1000,1e-3)
```
The output includes the estimate and the corresponding standard error for the regression parameter, estimate for the cumulative hazard function and the log-likelihood value.


### Scenario 2 (single time-dependent covariate): <img src="http://chart.googleapis.com/chart?cht=tx&chl= \beta=0.5" style="border:none;">, <img src="http://chart.googleapis.com/chart?cht=tx&chl= X(t)=X\exp(t)" style="border:none;">
#### Simulate data:
```
set.seed(1)
Zt=function(X,t) X*t
Lambdat=function(t) 0.2*t
This is the cumulative hazard function, Users can use their own Lambdat by changing the specific form. 
data=Data_generation(100,c(0.5),Lambdat,Zt)
```
This function generates a cohort with 100 subjects with a scalar covariate. The covariate for each subject is generated from Bernoulli(0.5) distribution. Users can user their own cumulative hazard function by changing the specific form of Lambdat. 

#### Estimate parameters:
The regression parameter and the cumulative hazard function can be estimated using the command
```
testresult=Main_func_ind(data$X,data$Delta,data$Inspec,data$mimic,1.5,1000,1e-3)
```
The output includes the estimate and the corresponding standard error for the regression parameter, estimate for the cumulative hazard function and the log-likelihood value.



### Scenario 3 (two time-independent covariates): <img src="http://chart.googleapis.com/chart?cht=tx&chl= \beta_1=0.5" style="border:none;">, <img src="http://chart.googleapis.com/chart?cht=tx&chl= \beta_2=1" style="border:none;">, <img src="http://chart.googleapis.com/chart?cht=tx&chl= n=100" style="border:none;">

#### Simulate data:
```
set.seed(1)
Zt=function(X,t) X*t
Lambdat=function(t) 0.2*t
This is the cumulative hazard function, Users can use their own Lambdat by changing the specific form. 
data=Data_generation(100,c(0.5,1),Lambdat,Zt)
```
This function generates a cohort with 100 subjects with two covariates. The covariates for each subject are generated from Bernoulli(0.5) distribution. Users can user their own cumulative hazard function by changing the specific form of Lambdat. 

#### Estimate parameters:
The regression parameter and the cumulative hazard function can be estimated using the command
```
testresult=Main_func_ind(data$X,data$Delta,data$Inspec,data$mimic,1.5,1000,1e-3)
```
The output includes the estimate and the corresponding standard error for the regression parameter, estimate for the cumulative hazard function and the log-likelihood value.

