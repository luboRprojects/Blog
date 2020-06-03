---
title: 'T-tests: Regression and mean value '
author: ''
date: '2020-06-03'
slug: t-tests-regression-and-mean-value
categories: []
tags:
  - r
  - statistics
image:
  caption: ''
  focal_point: ''
---

I have been asked by students about the difference between the "normal" t-test for mean value analysis and the "regression" t-test many times. So, is there any difference? Let's look the following example to get a practical intuition:

We will use the mtcars dataset to test whether cars with manual transmission have different fuel consumption than cars with automatic transmission. 

```r
library(dplyr)
data("mtcars")
boxplot(mtcars$cyl ~ mtcars$am)
```

<img src="/post/2020-06-03-t-tests-regression-and-mean-value_files/figure-html/unnamed-chunk-1-1.png" width="672" />

```r
mtcars %>% 
  group_by(am) %>%
  summarise(mpgAvg = mean(mpg))
```

```
## # A tibble: 2 x 2
##      am mpgAvg
##   <dbl>  <dbl>
## 1     0   17.1
## 2     1   24.4
```

Let's run the t-test for difference in means:


```r
t.test(mpg ~ am, var.equal = TRUE, data=mtcars)
```

```
## 
## 	Two Sample t-test
## 
## data:  mpg by am
## t = -4.1061, df = 30, p-value = 0.000285
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  -10.84837  -3.64151
## sample estimates:
## mean in group 0 mean in group 1 
##        17.14737        24.39231
```

And now check the regression outcome (there is no need to code am as factor has only 2 levels).


```r
lm(mpg ~ am, data=mtcars) %>%
  summary
```

```
## 
## Call:
## lm(formula = mpg ~ am, data = mtcars)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -9.3923 -3.0923 -0.2974  3.2439  9.5077 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   17.147      1.125  15.247 1.13e-15 ***
## am             7.245      1.764   4.106 0.000285 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.902 on 30 degrees of freedom
## Multiple R-squared:  0.3598,	Adjusted R-squared:  0.3385 
## F-statistic: 16.86 on 1 and 30 DF,  p-value: 0.000285
```
Both t-statics equal in absolute value to 4.106.

What does this actually mean? The mean-value t-test tests whether difference between `\(\mu_{am=aut} = \mu_{am=man}\)`, which can be rewritten as `\(\mu_{am=aut} - \mu_{am=man} = 0\)`. The "regression" t-test tests whether the effect of having `\(am=aut = 0\)`.  

