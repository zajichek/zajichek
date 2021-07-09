---
title: A Look at Collider Bias
author: Alex Zajichek
date: '2021-07-08'
slug: a-look-at-collider-bias
categories: []
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2021-07-08T19:28:21-05:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/viz/viz.js"></script>
<link href="{{< blogdown/postref >}}index_files/DiagrammeR-styles/styles.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/grViz-binding/grViz.js"></script>

I’ve recently heard a lot of buzz around “causal inference.” Despite not knowing anything other than what is implied by the name, I was intrigued by the idea as it seems fundamental to why we do statistical analysis. To get started, I picked up [*The Book of Why: The New Science of Cause and Effect*](http://bayes.cs.ucla.edu/WHY/) (I’m a little over half way through). It has done a great job of introducing causal concepts, and more importantly, provided the realization that even from a scientific perspective, statistical theory and data themselves are not sufficient to provide the answers to questions truly of interest. Subject matter expertise is as (if not more) important to account for when constructing a model. This article takes a closer look at one of the concepts introduced: *collider bias*.

# Background

## What is collider bias?

A [*collider*](https://catalogofbias.org/biases/collider-bias/) is a type of junction that occurs when an event is independently caused by two (2) other events. For example, in the causal diagram below, event **C** is caused by events **A** and **B**:

``` r
DiagrammeR::grViz("
  digraph graph2 {
  
  graph [layout = dot, rankdir = LR]
  
  node [shape = oval]
  a [label = 'A']
  c [label = 'C']
  b [label = 'B']
  
  a -> c
  b -> c
  }
  ")
```

<div id="htmlwidget-1" style="width:672px;height:480px;" class="grViz html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"diagram":"\n  digraph graph2 {\n  \n  graph [layout = dot, rankdir = LR]\n  \n  node [shape = oval]\n  a [label = \"A\"]\n  c [label = \"C\"]\n  b [label = \"B\"]\n  \n  a -> c\n  b -> c\n  }\n  ","config":{"engine":"dot","options":null}},"evals":[],"jsHooks":[]}</script>

There is no relationship between **A** and **B** and that would be apparent if looked at marginally. However, if we were to condition on **C**, there would be an apparent correlation between **A** and **B** that does not truly exist. The latter is known as [*collider bias*](https://catalogofbias.org/biases/collider-bias/).

## Why does it matter?

In my experience, when estimating the individual effect of an exposure on an outcome, the general consensus tends to be that it is a “good thing” to control for *more* potential confounding factors than less. However, little attention is paid to the mechanistic relationships of those factors to the exposure, and so controlling for certain factors may artifically induce a relationship between the exposure and outcome that was never really there.

### Population definition

A more interesting and apparent case where the bias occurs is in the study population itself. We don’t often think about the bias induced by simply defining the population of interest. However, once this population is selected, we have conditioned on those characteristics. So if the collider bias exists then no matter how good the sampling procedure or statistical adjustments are, the bias will be there since it was inherent to the population selected.

# Example

**INCOMPLETE**

-   setup problem
-   derive probabilities
-   how much does this persist even when we don’t completely condition? (look at ranges based on probabilities)
