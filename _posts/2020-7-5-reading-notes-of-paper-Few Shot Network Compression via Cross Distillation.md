---
title: Reading notes of paper "Few Shot Network Compression via Cross Distillation"
date: 2020-7-05
categories:
- Paper Digest
tags:
- Model Compression
- Knowledge Distillation
---

This paper "Few Shot Network Compression via Cross Distillation" is published in AAAI 2020 by Bai et al. This paper presents cross distillation a novel knowledge distillation approach for learning compact student network given limited number of training samples. 

### Background

#### Few-Shot Problem

As this paper mentioned, given a few samples per class, it is hard to effectively compress the network with a negligible performance drop. And they just tried to deal with the few-shot problem using cross distillation, which is different from traditional few-shot learning. This approach does not have the ability of generalization. While traditional few-shot learning refers to the practice of feeding a learning model with a very small amount of training data, contrary to the normal practice of using a large amount of data. There are several different directions for few-shot learning. For example, data-level approaches utilize external data sources or produce new data sources to get more training data. And parameter-level approaches apply regularization techniques or novel loss functions. 

#### Network Pruning

Network pruning is a technique of model compression via reducing the size of the network by removing parameters. In the literature, there are several pruning techniques. The structure pruning aims to remove the parameters by group, while the unstructured pruning just removes the parameters individually. Furthermore, some network pruning approaches apply a scoring method to score parameters based on their absolute values, trained important coefficients, or contributions to network activations or gradients. And some scheduling methods are applied to prune the parameters in on step or iteratively over several steps. Usually, most approaches apply fine-tuning that continues training the pruned networks after pruning to achieve better performance.


#### Knowledge Distillation

Hinton et al., 2015 applied knowledge distillation to transfer the knowledge from a large pre-trained teacher network to a smaller lightweight student network. Then, several variants of knowledge distillation have been developed for some specific tasks. For example, Li et.al., 2018 raised a new approach using knowledge distillation to deal with the few-sample problem. The authors designed student-net from scratch or by compressing teacher-net then added 1x1 conv-layer at the end of each block of student-net and aligned teacher and student by estimating the parameter using least-square regression. In the end, the final student-net absorb or merge the added 1x1 conv-layer into the previous conv-layer.

### Introduction

#### Two Challenges

In this paper, the author raised a novel approach to solve two challenges in the literature. Firstly, the model compression requires sufficient training data to fine-tune the light-weighted DNNs, which could be challenged by privacy and security issues. Secondly, the compressed network can easily overfit on the few training instances in the few-shot problem.

#### Solutions

The authors proposed cross distillation, which reduces layer-wisely accumulated estimation errors by interweaving hidden layers of teacher and student networks. Furthermore, this method offers a general framework compatible with prevalent network compression techniques such as pruning.

### Methods

The authors employed three different cross distillation methods in their approach. Let me first introduce the traditional layer-wise knowledge distillation which can take layer-wise supervision from the teacher network. The layer-wise distillation aims to find the optimal **Ws** (Equation 1) that minimizes the Euclidean distance between **ht** and **hs**. **Lr** here is the estimation error. The problem of this traditional layer-wise distillation is that the student network **Fs** tends to suffer from high estimation errors on the test set as a result of over-fitting.

![](../../../../../assets/images/papernotesimgs/40.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/41.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/42.png){:style="margin:0 auto"}

To address this problem, the author designed a novel layer-wise distillation method. Showing in the following figures, they direct ht to **Fs** in substitution of **hs** to reduce the historically accumulated estimation errors. And they called this new loss **lc** as correction loss. But, minimizing this **lc** could lead to a biasedly-optimized student net because of the inconsistency error es in the forward pass.

![](../../../../../assets/images/papernotesimgs/43.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/44.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/45.png){:style="margin:0 auto"}

In order to maintain the consistency during forward pass for **Fs**. the authors designed imitation loss **li** which inverse the strategy by guiding **hs** to **Ft** shown in the following figures. 

![](../../../../../assets/images/papernotesimgs/46.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/47.png){:style="margin:0 auto"}

In this way, the final loss function is a convex combination of these two new loss terms:

![](../../../../../assets/images/papernotesimgs/48.png){:style="margin:0 auto"}

**μ** here is a tuning hyper-parameter. The author also gave some theoretical analysis to prove that minimize this loss function is in the right direction to improve the student net **Fs**. But this loss function involves two loss terms with four convolutions to compute per batch of data, which doubles the training time.

So, the author designed another variant to balance **lc** and **li** by empirically soften the hard connection of **hs** and **ht**, shown in the following figures. 

![](../../../../../assets/images/papernotesimgs/49.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/50.png){:style="margin:0 auto"}

**α** and **β** here are two hyper-parameters that adjust how many percentages are used for cross connection. 

Then the authors showed how to combine cross distillation with network pruning methods in the following figures. 

![](../../../../../assets/images/papernotesimgs/51.png){:style="margin:0 auto"}

Then we can add different regularization terms in this equation to achieve non-structured pruning and structured pruning, such as:

![](../../../../../assets/images/papernotesimgs/52.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/53.png){:style="margin:0 auto"}

### Experiments

In their experiments, they select two benchmark data sets, i.e., CIFAR-10 and ImageNet-ILSVRC12 with two base networks, i.e., VGG and ResNet. They select several baselines on different aspects, such as L1-norm pruning, FitNet and FSKD which are two knowledge distillation methods, and ThiNet and Channel Pruning (CP) which are layer-wise regression based channel pruning methods. In addition, they also use three variants of their methods to compare with these baselines. 

The authors did extensive experiments and the results demonstrated the efficiency of their method. 

### Summary

This paper presents cross distillation a novel knowledge distillation approach for learning compact student network given limited number of training samples. By reducing estimation errors between the student network and teacher network, cross distillation can bring a more powerful and generalizable student network. The proposed method offers a general framework compatible with prevalent network compression techniques such as pruning. 

### Review

Pros: 

- The idea of this paper is novel. Their approach deals with few-shot examples in a novel way and technically correct. 
- The adopted methodology is clearly described and easy to be understood. Additionally, they also provide theoretical analysis.
- The authors take extensive experiments to demonstrate the effectiveness of their approach. And the tables and figures are well designed and explained clearly.

Cons:

- The baselines are not well-designed for few-shot learning, so they are not comparability at all. The authors should have selected some other methods for few-shot learning to compare with, e.g., MAML.
- There are some typos in their paper that could make readers confused. 

Overall, this paper is a good paper and it tried to find a new direction to deal with the few-shot examples problem.

### Reference

[1] Bai, Haoli, et al. "Few Shot Network Compression via Cross Distillation." arXiv preprint arXiv:1911.09450 (2019). AAAI2020
[2] Blalock, Davis, et al. "What is the state of neural network pruning?." arXiv preprint arXiv:2003.03033 (2020).
[3] Li, Tianhong, et al. "Knowledge distillation from few samples." (2018).
[4] Finn, Chelsea, Pieter Abbeel, and Sergey Levine. "Model-agnostic meta-learning for fast adaptation of deep networks." arXiv preprint arXiv:1703.03400 (2017).
[5] Geoffrey Hinton, Oriol Vinyals, and Jeff Dean. 2015. Distilling the knowledge in a neural network. arXiv preprint arXiv:1503.02531.