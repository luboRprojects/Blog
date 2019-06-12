---
title: Granger Causality and Multiple Time Series
author: ''
date: '2019-06-12'
slug: granger-causality-and-multiple-time-series
categories: []
tags: []
image:
  caption: ''
  focal_point: ''
---

We have recently submitted a paper about the short-term car registration forecasting. Forecasting models were based on several underlying variables which were analysed by a standard Vector Autoregressive Model. As the main purpose of the paper was not to present a black-box model with a good predictive power, we needed to analyse an importants of the car registration determinants.

A traditional approach to identify *"cause and effects"* in the context of time series analysis is to perform the Granger Causality test. Surprisingly, a treatment of the multivariate is not discussed much. Typically, two variables settings is presented with the caveat that solution works even for a more variables. This is only a partially true.

In the following text we will go through the simple 3 time-series example with various settings of interconnections.

## Three Variables, One driver

This example shows the analysis of the tree time series where the first time series *ts1* is a confounding time series.


```r
library(DiagrammeR)

DiagrammeR::grViz("digraph boxes_and_circles{

graph[layout = dot, rankdir = LR]

TS1; TS2; TS3

TS1 -> TS2 [label = 'AR1 + alpha TS1']
TS1 -> TS3 [label = 'AR1 + beta TS2']
TS2 -> TS3 [label = 'No Relation', color= 'red']
}")
```

```
## PhantomJS not found. You can install it with webshot::install_phantomjs(). If it is installed, please make sure the phantomjs executable can be found via the PATH variable.
```

```
## Warning in normalizePath(path.expand(path), winslash, mustWork):
## path[1]="webshot5ee41c2e7449.png": Systém nemuže nalézt uvedený soubor
```

```
## Warning in file(con, "rb"): cannot open file 'C:
## \Users\Lubor\AppData\Local\Temp\Rtmpqerj4r\file5ee418d87efa\webshot5ee41c2e7449.png':
## No such file or directory
```

```
## Error in file(con, "rb"): cannot open the connection
```

