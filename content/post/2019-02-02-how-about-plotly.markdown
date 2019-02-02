---
title: How About Plotly?
author: ''
date: '2019-02-02'
slug: how-about-plotly
categories: []
tags: []
image:
  caption: ''
  focal_point: ''
---

Let's try some plotly


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
library(ggplot2)
library(plotly)
```

```
## 
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggplot2':
## 
##     last_plot
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```

```
## The following object is masked from 'package:graphics':
## 
##     layout
```

```r
p1 <- mtcars %>%
 mutate(Cylinders = as.factor(cyl)) %>%
 ggplot(., aes(x=hp, y=mpg, col=Cylinders) ) + 
  geom_point(size=4, alpha=0.7) + 
  theme_bw()

ggplotly(p1)
```

```
## Error in loadNamespace(name): there is no package called 'webshot'
```

