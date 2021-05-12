---
title: Macro Average VS Micro Average
date: 2021-5-10
categories:
- Machine Learning
tags:
- Basic Concept


---

In this blog, I introduce the differences between macro-average and micro-average. 

### Macro-average

A macro-average will compute the metric independently for each class and then take the average (hence treating all classes equally).

### Micro-average

A micro-average will aggregate the contributions of all classes to compute the average metric.

### Differences

Micro-average is preferable if you suspect there might be class imbalance in a multi-classification task. 

### Example

