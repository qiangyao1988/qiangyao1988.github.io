---
title: Different Settings of Federated Learning
date: 2021-5-11
categories:
- Machine Learning
tags:
- Federated Learning


---

In this blog, I introduce three differences settings of federated learning. 

### Horizontal Federated Learning

The users' feature of  datasets from different clients overlap more while the users overlap less in the case of horizontal federated learning. For example, there are two banks in different regions. Their user groups are from their respective regions, thus the intersection between them is small. However, their businesses are similar, so the recorded users' features are the same.

### Vertical Federated Learning

The users of  datasets from different clients overlap more while the users' features overlap less in the case of vertical federated learning.  For example, there are two different institutions. One is a bank in one place and the other is an e-commerce company in the same place. Their user group is likely to include most of the residents of the place and therefore the intersection of users is large. However, because banks record users’ income and expenditure behaviors and credit ratings, while e-commerce stores users’ browsing and purchasing history, their user features overlap is small.

### Federated Transfer Learning

While both users and users' features of the datasets from different clients have less overlap, we apply transfer learning to overcome the lack of data or labels. For example, there are two different institutions, one is a bank located in China, and the other is an e-commerce company located in the United States. Due to geographical restrictions, the user groups of the two institutions have very little intersection. At the same time, due to the different types of institutions, only a small part of the data features overlap.  In this case, we use transfer learning to solve the problem of small unilateral data and small label samples to improve the effectiveness of the model. 

### Reference

Huang, Zhiqi, Fenglin Liu, and Yuexian Zou. "Federated Learning for Spoken Language Understanding." *Proceedings of the 28th International Conference on Computational Linguistics*. 2020.

