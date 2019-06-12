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

df <- data.frame(col1 = c( "Cat", "Dog", "Bird"),
                 col2 = c( "Feline", "Canis", "Avis"), 
                 stringsAsFactors=FALSE)
uniquenodes <- unique(c(df$col1, df$col2))

nodes <- create_node_df(n=length(uniquenodes), nodes = seq(uniquenodes), type="number", label=uniquenodes)
edges <- create_edge_df(from=match(df$col1, uniquenodes), to=match(df$col2, uniquenodes), rel="related")

g <- create_graph(nodes_df=nodes, edges_df=edges)
render_graph(g)
```

<!--html_preserve--><div id="htmlwidget-210ccf5db27782c5c4c9" style="width:672px;height:480px;" class="grViz html-widget"></div>
<script type="application/json" data-for="htmlwidget-210ccf5db27782c5c4c9">{"x":{"diagram":"digraph {\n\ngraph [layout = \"neato\",\n       outputorder = \"edgesfirst\",\n       bgcolor = \"white\"]\n\nnode [fontname = \"Helvetica\",\n      fontsize = \"10\",\n      shape = \"circle\",\n      fixedsize = \"true\",\n      width = \"0.5\",\n      style = \"filled\",\n      fillcolor = \"aliceblue\",\n      color = \"gray70\",\n      fontcolor = \"gray50\"]\n\nedge [fontname = \"Helvetica\",\n     fontsize = \"8\",\n     len = \"1.5\",\n     color = \"gray80\",\n     arrowsize = \"0.5\"]\n\n  \"1\" [label = \"Cat\", fillcolor = \"#F0F8FF\", fontcolor = \"#000000\"] \n  \"2\" [label = \"Dog\", fillcolor = \"#F0F8FF\", fontcolor = \"#000000\"] \n  \"3\" [label = \"Bird\", fillcolor = \"#F0F8FF\", fontcolor = \"#000000\"] \n  \"4\" [label = \"Feline\", fillcolor = \"#F0F8FF\", fontcolor = \"#000000\"] \n  \"5\" [label = \"Canis\", fillcolor = \"#F0F8FF\", fontcolor = \"#000000\"] \n  \"6\" [label = \"Avis\", fillcolor = \"#F0F8FF\", fontcolor = \"#000000\"] \n  \"1\"->\"4\" \n  \"2\"->\"5\" \n  \"3\"->\"6\" \n}","config":{"engine":"dot","options":null}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
export_graph(g,
file_name = "pic.png",
file_type = "png")


#frameWidget(g, height = 350, width = '95%')
```

