The package implements recently developed inference procedures for the accelerated failure time (AFT) models with both the rank-based approach and the least squares approach. For the rank-based approach, the package allows various weight choices and uses an induced smoothing procedure that leads to much more efficient computation than the linear programming method. With the rank-based estimator as an initial value, the generalized estimating equation (GEE) approach is used as an extension of the least squares approach to the multivariate case, where the within cluster dependency is accountered for with working covariance structures. Additional sampling weights are incorporated to handle missing data needed as in case-cohort studies or general sampling schemes.

Here are some sample examples to get started:

``` r
library(survival)
data(kidney)

library(aftgee)
fit.rk <- aftsrr(Surv(time, status) ~ age + sex, id = id, data = kidney, se = c("ISMB", "ZLMB"))
summary(fit.rk)
#> Call:
#> aftsrr(formula = Surv(time, status) ~ age + sex, data = kidney, 
#>     id = id, se = c("ISMB", "ZLMB"))
#> 
#> Variance Estimator: ISMB
#>     Estimate StdErr z.value p.value    
#> age   -0.001  0.016  -0.077   0.939    
#> sex    1.522  0.476   3.199   0.001 ***
#> ---
#> Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
#> 
#> Variance Estimator: ZLMB
#>     Estimate StdErr z.value p.value    
#> age   -0.001  0.018   -0.07   0.944    
#> sex    1.522  0.416    3.66  <2e-16 ***
#> ---
#> Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
fit.ge <- aftgee(Surv(time, status) ~ age + sex, id = id, data = kidney)
summary(fit.ge)
#> Call:
#> aftgee(formula = Surv(time, status) ~ age + sex, data = kidney, 
#>     id = id)
#> 
#> AFTGEE Estimator
#>             Estimate StdErr z.value p.value    
#> (Intercept)    2.071  0.637   3.251   0.001 ***
#> age           -0.005  0.008  -0.677   0.498    
#> sex            1.374  0.363   3.782  <2e-16 ***
#> ---
#> Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```