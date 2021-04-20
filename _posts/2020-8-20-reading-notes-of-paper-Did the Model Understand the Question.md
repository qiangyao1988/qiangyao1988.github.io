---
title: Reading notes of paper "Did the Model Understand the Question？"
date: 2020-8-20
categories:
- Paper Digest
tags:
- Explainable Machine Learning
- Natural Language Processing
- Question Answering
---

This paper studies IG, an attribution technique, on three question answering models.  The authors demonstrate we can either use attribution to craft effective adversarial examples or aid the developer in iterating on model quality more effectively.

### Problem Setup

While we are answering some questions in the text, there are often some attention notes in the question paragraph, such as "Read the question carefully". In this way, we need to pay attention to the question text and try to really understand it. In machine learning problems, there are several question answering tasks, e.g., Tabular QA [1], Visual QA [2], and Reading Comprehension [3]. This paper cares about have the models read the question carefully similar to the real-world scenario?

The standard way of measuring question answering systems is to evaluate its error on a test set. In this way, high accuracy indicates a good model. However, most tasks have large test and training sets leading to impracticable manual check. Therefore, the authors propose techniques to analyze the sensitivity of a deep learning model to question words to help humans identify important question words and anticipate their function in question answering. In one word, the attribution generated from Integrated Gradients (IG) can augment standard measures of accuracy and empower investigation of model performance. Furthermore, the authors also apply attribution to generate adversarial questions efficiently

### Introduction

First, let us take one example. The following figure is an example from VQA task. The original question is "how symmetrical are the white bricks on either side of the building?". And the ground truth and the prediction of the deep learning model are both "Very". Then we can get the attribution via IG from this question. Showing in the figure, two high attributions in this question are "how" and "bricks". So the authors try to generate an adversarial example of this question by changing some words (but not the attributions) in this question. The new adversarial question now is "how spherical are the white bricks on either side of the building?" replacing "symmetrical" with "sphere". Although the ground truth for this adversarial question is not "very" anymore, the deep learning model still generates the prediction as "very". So we can see this adversarial question fool the model and is a good attack. In other words, the model actually does not read the question carefully. 

![](../../../../../assets/images/papernotesimgs/63.png){:style="margin:0 auto"}

### Related Work

#### Adversarial Examples Generating

Jia and Liang [4] proposed a model independent method to craft passage perturbations via crowdsourcing, e.g., adding an irrelevant sentence at the end of the reading paragraph to fool the model generating an incorrect prediction. Differently, this approach peeks into the logic of a network to identify high attribution question terms then craft targeted attacks. 

#### Attribution

In the literature, there are lots of methods to generate the attributions. For example, DeepLift (Deep Learning Important FeaTures) [5] computes importance scores based on explaining the difference of the output from some 'reference' output in terms of differences of the inputs from their 'reference' inputs. Some methods generate attribution based on the gradients during the training process, such as Layer-wise relevance propagation (LRP) [6]. Deconvutional networks [7] map the activities back to the input pixel space, showing what input pattern originally caused a given activation in the feature maps. Similarly, Guided back-propagation [8] is a variant of the deconvolutional network. 

Different from these approaches, there are several advantages to use IG generating attributions. First, the original paper [9] demonstrates IG has several axiomatic justifications. Second, it is easy to be implemented, because we only need to do som gradient computations. Finally, it is really efficient, it only takes less than 0.5 seconds to generate attributions for a given input example. 

### Integrated Gradients

Integrated Gradients (IG) was first proposed in [9] to generate attributions of the prediction of a deep network to its inputs. For example, we can use IG to attribute an object recognition network's prediction to its pixels. Or we can attribute a text sentiment network's prediction to individual words. This paper applies IG to isolate question words that a deep learning network uses to produce an answer. 

Let me first introduce the mechanism of IG. As we can int interpolate between the baseline and the input, the prediction moves along a trajectory from uncertainty to certainty (the final probability). The baseline here is used to compare with the current inputs. For example, we can assume the black image as the baseline, or we can use the zero embedding vector as the baseline in text. Then, at each point on this trajectory, one can use the gradient of the function F (a deep network) with respect to the input to attribute the change in probability back to the input variables. Finally, IG can simply aggregate the gradients of the probability with respect to the input along this trajectory using a path integral. In this paper, the authors use a straight line between the baseline and the input as the path integral. Now, we can get the attributions (a1, ..., an) which are influences or blame-assignments to the variables (x1, ..., xn) on the probability F corresponding to the baseline here. The following figure shows the definition of IG based on these mechanisms. 

![](../../../../../assets/images/papernotesimgs/64.png){:style="margin:0 auto"}

In order to use IG on these question answering tasks, the authors demonstrate there are several properties the attributions generated by IG. The attributions can be applied to find the uninfluential variable of the inputs. If all else variables are fixed, only varying the influential variable does not change the output probability. Furthermore, the influential variables do not get any attribution through IG. Conversely, the influential variables always get some attribution. With these two properties, we can perturb the high-attribution terms to change the networks' response. On the contrary, we can perturb terms that receive a low attribution which does not change the networks' response. In this way, the authors design attack methods against the network by perturbing instances where generic (e.g., "a", "the") receive high attribution or contentful words receive low attribution. 

### Experiments

In the VQA task, the authors use the deep network from [10] on the VQA 1.0 dataset. They have got several observations from the experiments: (1) There are very few words that have high attribution. (2) If we only alter the low attribution words in the question, it does not change the network's answer. (3) Most of the highly attributed words are words such as "there", "what", "how", "doing"- they are usually the less important words in questions. (4) Informative words in the question (e.g., nouns) often receive very low attribution, indicating a weakness on part of the network. 

In the Reading Comprehension task, the authors use the model from [11] on the SQuAD dataset. They analyze the adversarial examples generated by Jia and Liang for their success in fooling and unsuccessful case. Then they use attributions to improve the effectiveness of attacks and improve the attack accuracy. 

### Summary

This paper studies IG, an attribution technique, on three question answering models. And they demonstrate attributions are helpful to identify weakness of these models. In this way, we can either use attribution to craft effective adversarial examples or aid the developer in iterating on model quality more effectively. 

### Reference

[1] Khalid, Mahboob Alam, Valentin Jijkoun, and Maarten de Rijke. "Machine learning for question answering from tabular data." 18th International Workshop on Database and Expert Systems Applications (DEXA 2007). IEEE, 2007.

[2] Antol, Stanislaw, et al. "Vqa: Visual question answering." Proceedings of the IEEE international conference on computer vision. 2015.

[3] Rajpurkar, Pranav, et al. "Squad: 100,000+ questions for machine comprehension of text." arXiv preprint arXiv:1606.05250 (2016).

[4] Jia, Robin, and Percy Liang. "Adversarial examples for evaluating reading comprehension systems." arXiv preprint arXiv: 1707.07328 (2017).

[5] Shrikumar, Avanti, Peyton Greenside, and Anshul Kundaje. "Learning important features through propagating activation differences." arXiv preprint arXiv:1704.02685 (2017).

[6] Binder, Alexander, et al. "Layer-wise relevance propagation for neural networks with local renormalization layers." International Conference on Artificial Neural Networks. Springer, Cham, 2016.

[7] Zeiler, Matthew D., and Rob Fergus. "Visualizing and understanding convolutional networks." European conference on computer vision. Springer, Cham, 2014.

[8] Springenberg, Jost Tobias, et al. "Striving for simplicity: The all convolutional net." arXiv preprint arXiv:1412.6806 (2014).

[9] Sundararajan, Mukund, Ankur Taly, and Qiqi Yan. "Axiomatic attribution for deep networks." arXiv preprint arXiv: 1703.01365 (2017).

[10] Kazemi, Vahid, and Ali Elqursh. "Show, ask, attend, and answer: A strong baseline for visual question answering." arXiv preprint arXiv:1704.03162 (2017).

[11] Yu, Adams Wei, et al. "Fast and accurate reading comprehension by combining self-attention and convolution." International Conference on Learning Representations. 2018.