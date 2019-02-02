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
library(widgetframe)
library(dplyr)
library(ggplot2)
library(plotly)
library(webshot)

p1 <- mtcars %>%
 mutate(Cylinders = as.factor(cyl)) %>%
 ggplot(., aes(x=hp, y=mpg, col=Cylinders) ) + 
  geom_point(size=4, alpha=0.7) + 
  theme_bw()
```


```r
p2 <- ggplotly(p1)
frameWidget(p2)
```

<!--html_preserve--><div id="htmlwidget-7211f92b0291f526e0c7" style="width:100%;height:480px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-7211f92b0291f526e0c7">{"x":{"url":"/post/2019-02-02-how-about-plotly_files/figure-html//widgets/widget_unnamed-chunk-2.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

