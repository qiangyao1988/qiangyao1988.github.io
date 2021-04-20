---
title: Reading notes of paper "Adversarially Robust Distillation"
date: 2020-4-08
categories:
- Paper Digest
tags:
- Adversarial Robust
- Knowledge Distillation
---

This paper "Adversarially Robust Distillation" is published in AAAI 2020 by Goldblum et al.  The authors propose whether the adversarial robust can be transferred from the teacher networks to the student networks.

### Background

State-of-art deep neural networks for computer visions or natural language processing tasks have achieved pretty good performance, but most of them have millions of parameters, hundreds of layers, and require billions of operations for both training and inference. Although most deep neural networks are deployed as inference on mobile devices that have limited compute, memory, and power budgets, we still need to train deep neural networks on mobile devices directly due to some real-world scenario reasons, such as connectivity issues or privacy reasons. In addition, mobile devices usually do not have GPUs to accelerate the training and inference processes. There is a huge demand to design efficient lightweight networks on mobile devices. 

In the literature, there are several strategies to compress deep neural networks, such as quantization and pruning techniques. These approaches get smaller lightweight deep neural networks and very good performance. Hinton et al., 2015 apply knowledge distillation to transfer the knowledge of a large pre-trained teacher network to a smaller lightweight student network. The student network is trained to emulate the outputs of the teacher network instead of being trained on one-hot class labels. The student network can get more information by training with the soft labels generated from the teacher network. In the one-hot labels, all the false class has the classification probability as 0. However, different classes should have different classification probabilities in the results of the deep neural networks. The differences between these classification probabilities actually contain important information, which can be used as the generalization of the neural networks. For example, in an image classification task, the classification probability of a car should be much more similar to the truck than to the cat in the results of the probability vector from a neural network. In other words, the feature of the car should be very similar to the truck, while it should be different from the cat. We lose this important information by only using the one-hot vectors. 

Usually, there are two different parts in the loss function of the knowledge distillation approach. One is the distillation loss, the other one is the task loss. In the following equation, *KLdiv* is the KL-divergence loss function as the distillation loss, the task loss here is the *CrossEntropy*. Qs and Qt are the predictions from the student network and the teacher network, respectively. T here is the temperature in the distillation, and alpha is a hyperparameter. 

![](../../../../../assets/images/papernotesimgs/54.png){:style="margin:0 auto"}

There are also several options for the distillation loss, such as KL-divergence, mean square error, and cross entropy. Furthermore, researchers are working on two directions about how to select soft labels from the teacher network, such as output distillation and feature distillation. Here are three figures to show the differences between the two directions. 

![](../../../../../assets/images/papernotesimgs/55.png){:style="margin:0 auto"}

{:.image-caption}

*The soft labels are selected as the logits from the teacher network*

![](../../../../../assets/images/papernotesimgs/56.png){:style="margin:0 auto"}

{:.image-caption}

*The soft labels are selected as the features learned from the teacher network*

![](../../../../../assets/images/papernotesimgs/57.png){:style="margin:0 auto"}

{:.image-caption}

*The soft labels are selected as the output predictions from the teacher network*

### Proposal

In this paper, the authors aware that the small student networks in knowledge distillation are vulnerable to adversarial attacks. While in some domains, such as self-driving cars, medical diagnosis, and copyright control, efficiency and accuracy are not enough, which means the small student networks must also be adversarially robust. In this situation, the authors propose whether the adversarial robust can be transferred from the teacher networks to the student networks. From the following table and figure, we can see the student network may learn robust behavior from a robust teacher, even if only see clean images during distillation. Furthermore, their method Adversarially Robust Distillation (ARD) outperforms traditional knowledge distillation for producing robust student networks. 

![](../../../../../assets/images/papernotesimgs/58.png){:style="margin:0 auto"}

{:.image-caption}

*Adversarial robust transfer experiments*

![](../../../../../assets/images/papernotesimgs/59.png){:style="margin:0 auto"}

{:.image-caption}

*The student network mimics the teacher network*

### Method

We can see their idea and the loss function they used in ARD in the following figures. They combine the ideas in knowledge distillation and adversarial training and set up a new loss function. With this new loss function, the student networks can not only get the adversarial robustness transferred from the robust teacher networks but only gain some robustness through the adversarial training. 

![](../../../../../assets/images/papernotesimgs/60.png){:style="margin:0 auto"}

{:.image-caption}

*Loss function in ARD*

![](../../../../../assets/images/papernotesimgs/61.png){:style="margin:0 auto"}

{:.image-caption}

*ARD workflow*

### Experiments

They mainly select ResNet18 as the teacher network and MobileNetV2 as the student network. For the attack method, they select the 20-step PGD. We can see that performance on CIFAR-10 is pretty good, the student even gets higher robust accuracy than the teacher showing in the following table. 

![](../../../../../assets/images/papernotesimgs/62.png){:style="margin:0 auto"}

### Critiques

**Pros:**

The idea of this paper is very novel. Their approach deals with the vulnerable problem of student networks in knowledge distillation. The adopted methodology is clearly described and easy to be understood. Their experiments are well designed (especially the two experiments in the introduction part) and the results help answer several questions that may be asked by the reviewers. 

**Cons:**

In this paper, they only try the PGD attack method, they should have tried several other attacks, such as BIM and CW. What is more, they should have employed their methods on other modes, such as different student and teacher networks. Finally, they should have done some theoretical analysis instead of just showing the experiment results.

### Reference

[1] Goldblum, Micah, et al. "Adversarially robust distillation." *arXiv preprint arXiv:1905.09747* (2019).

[2] Hinton, Geoffrey, Oriol Vinyals, and Jeff Dean. "Distilling the knowledge in a neural network." arXiv preprint arXiv:1503.02531 (2015).

[3] Mishra, Asit, and Debbie Marr. "Apprentice: Using knowledge distillation techniques to improve low-precision network accuracy." arXiv preprint arXiv:1711.05852 (2017).

[4] Heo, Byeongho, et al. "A comprehensive overhaul of feature distillation." *Proceedings of the IEEE International Conference on Computer Vision*. 2019.