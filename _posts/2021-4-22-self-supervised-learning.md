---
title: Self-supervised learning paper collection
date: 2021-4-22
categories:
- Paper Digest
tags:
- Self-supervised Learning
- Feature Learning


---

In this blog, I collect and summary recent papers about self-supervised learning.

### General

- **A Theoretical Analysis of Contrastive Unsupervised Representation Learning**
[[Paper]](https://arxiv.org/pdf/1902.09229.pdf)<br>
Description: This paper formalizes the notion of semantic similarity by introducing latent classes. Similar pairs are assumed to be drawn from the same latent class. A downstream task is comprised of a subset of these latent classes.

- **Predicting What You Already Know Helps: Provable Self-Supervised Learning**
[[Paper]](https://arxiv.org/pdf/2008.01064.pdf)<br>
Description: This paper proposes a mechanism based on approximate conditional independence (ACI) to explain why solving pretext tasks created from known information can learn representations that provably reduce downstream sample complexity.
- **Self-Supervised Learning for Large-Scale Unsupervised Image Clustering**
[[Paper]](https://arxiv.org/pdf/2008.10312.pdf)
[[Code]](https://github.com/Randl/kmeans_selfsuper)<br>
Description: This paper proposes an additional way of evaluating self-supervised learning: training a clustering algorithm on extracted features in an unsupervised manner. The authors also show that self-supervised learning provides a strong baseline for unsupervised computer vision and mentions some possible direction for the current self-supervised methods performance improvement.
- **Self-supervised Visual Feature Learning with Deep Neural Networks A Survey**
[[Paper]](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9086055&casa_token=lpa6IChv6PcAAAAA:2cLIsBwmEtpF2gxKT6iWZ39s68I1D8SBxKo-tk3GWtRqy31Dv4IlHSIHozhkb1kiiXeJ7nrB&tag=1)<br>
- **Towards Good Practices in Self-supervised Representation Learning**
[[Paper]](https://sslneuips20.github.io/files/CameraReadys%203-77/35/CameraReady/neurips_2020.pdf)<br>
Description: This paper presents several efficient practices in SSL. e.g., nonlinear projection head, strong data augmentation, and negative samples.
- **Understanding Contrastive Representation Learning through Alignment and Uniformity on the Hypersphere**
[[Paper]](https://arxiv.org/pdf/2005.10242.pdf)
[[Code]](https://ssnl.github.io/hypersphere/)<br>
Description: This paper identifies alignment (closeness) of features from positive parts and uniformity of the induced distribution of the features on the hypersphere are two key properties in contrastive loss. The authors propose quantifiable metrics to evaluate the representation quality for these two kinds of features. 
- **Understanding Self-supervised Learning with Dual Deep Networks**
[[Paper]](https://arxiv.org/pdf/2010.00578.pdf)<br>
Description: This paper provides a systematic theoretical analysis of modern SSL methods with deep ReLU networks that also incorporates data augmentation, and show how the gradient-based SSL work inside the neural network.
- **Understanding self-supervised learning using controlled datasets with known structure**
[[Paper]](https://sslneuips20.github.io/files/CameraReadys%203-77/64/CameraReady/Understanding_self_supervised_learning.pdf)<br>
Description: This paper investigates how SimCLR represents data with discrete, hierarchically structured classes, showing that the distances between examples in the representation space reflect the hierarchy.
- **What Makes for Good Views for Contrastive Learning?**
[[Paper]](https://arxiv.org/pdf/2005.10243.pdf)
[[Code]](https://hobbitlong.github.io/InfoMin/)<br>
Description: This paper first demonstrates that optimal views for contrastive representation learning are task-dependent Then the authors analyze an "InfoMin principle", which means a good set of views are those that share the minimal information necessary to perform well at the downstream task. 

### Computer Vision

- **Adversarial Self-Supervised Contrastive Learning**
[[Paper]](https://arxiv.org/pdf/2006.07589.pdf)
[[Code]](https://github.com/Kim-Minseon/RoCL)<br>
Description: This paper proposes a novel adversarial attack for unlabeled data, which makes the model confuse the instance-level identities of the perturbed data samples. Further, the authors present a self-supervised contrastive learning framework to adversarially train a robust neural network without labeled data, which aims to maximize the similarity between a random augmentation of a data sample and its instance-wise adversarial perturbation.

- **A critical analysis of self-supervision, or what we can learn from a single image**
[[Paper]](https://arxiv.org/pdf/1904.13132.pdf)
[[Code]](https://github.com/yukimasano/linear-probes)<br>
Description: In this paper, the authors make several conclusion: (1) the weights of the early layers of deep networks contain limited information about the statistics of natural images, that (2) such low-level statistics can be learned through self-supervision just as well as through strong supervision, and that (3) the low-level statistics can be captured via synthetic transformations instead of using a large image dataset.

 - **A Multi-view Perspective of Self-supervised Learning**
[[Paper]](https://arxiv.org/pdf/2003.00877.pdf)<br>
Description: 

- **A Simple Framework for Contrastive Learning of Visual Representations**
[[Paper]](https://arxiv.org/pdf/2002.05709.pdf)
[[Code]](https://github.com/google-research/simclr)<br>
Description: This paper introduces a simple framework for contrastive learning of visual representations named SimCLR. It makes several contributions for contrastive learning: (1) data augmentations play a critical role; (2) introducing a learnable nonlinear transformation; (3) demonstrating contrastive learning benefits from larger batch sizes and more training steps.

- **Big Self-Supervised Models are Strong Semi-Supervised Learners**
[[Paper]](https://arxiv.org/pdf/2006.10029v1.pdf)
[[Code]](https://github.com/google-research/simclr)<br>
Description: The proposed semi-supervised learning framework comprises three steps: (1) unsupervised or self-supervised pretraining, (2) supervised fine-tuning, and (3) distillation using unlabeled data.

- **Bootstrap Your Own Latent A New Approach to Self-Supervised Learning**
[[Paper]](https://arxiv.org/pdf/2006.07733.pdf)
[[Code]](https://github.com/deepmind/deepmind-research/tree/master/byol)<br>
Description: BYOL uses two neural networks, referred to as online and target networks, that interact and learn from each other. Starting from an augmented view of an
BYOL image, trains its online network to predict the target network's representation of another augmented view of the same image.

- **Contrastive Learning with Adversarial Examples**
[[Paper]](https://arxiv.org/pdf/2010.12050.pdf)<br>
Description: This paper introduces a new family of adversarial examples for contrastive learning and using these examples to define a new adversarial training algorithm for SSL, denoted as CLAE. When compared to standard CL, the use of adversarial examples creates more challenging positive pairs and adversarial training produces harder negative pairs by accounting for all images in a batch during the optimization.

- **Contrastive Learning with Hard Negative Samples**
[[Paper]](https://arxiv.org/pdf/2010.04592.pdf)<br>
Description: This paper formulates a method for sampling hard negative pairs, and an efficient sampling strategy that takes into account the lack of true dissimilarity information.

- **Domain Generalization by Solving Jigsaw Puzzles**
[[Paper]](https://arxiv.org/pdf/1903.06864.pdf)
[[Code]](https://github.com/fmcarlucci/JigenDG)<br>
Description: In this paper, the designed model learns the semantic labels in a supervised fashion, and broadens its understanding of the data by learning from self-supervised signals how to solve a jigsaw puzzle on the same images. This secondary task helps the network to learn the concepts of spatial correlation while acting as a regularizer for the classification task.

- **MixCo： Mix-up Contrastive Learning for Visual Representation**
[[Paper]](https://arxiv.org/pdf/2010.08887.pdf)
[[Code]](https://github.com/Lee-Gihun/MixCo-Mixup-Contrast)<br>
Description: This paper proposes Mix-up Contrast (MixCo), which extends the contrastive learning concept to semi-positives encoded from the mix-up of positive and negative images. MixCo aims to learn the relative similarity of representations, reflecting how much the mixed images have the original positives

- **Momentum Contrast for Unsupervised Visual Representation Learning**
[[Paper]](https://arxiv.org/pdf/1911.05722.pdf)
[[Code]](https://github.com/facebookresearch/moco)<br>
Description: This paper builds a dynamic dictionary with a queue and a moving-averaged encoder enabling building a large and consistent dictionary on-the-fly that facilitates contrastive unsupervised learning

- **Prototypical Contrastive Learning of Unsupervised Representations**
[[Paper]](https://arxiv.org/pdf/2005.04966.pdf)
[[Code]](https://github.com/salesforce/PCL)<br>
Description: This paper proposes prototypical contrastive learning, a unsupervised representation learning method that bridges contrastive learning and clustering.

- **SelfMatch: Combining Contrastive Self-Supervision and Consistency for Semi-Supervised Learning**
[[Paper]](https://arxiv.org/pdf/2101.06480.pdf)<br>
Description: This paper introduces SelfMatch two stages: (1) self-supervised pre-training based on contrastive learning and (2) semi-supervised fine-tuning based on augmentation consistency regularization.

- **Self-Supervised Domain Adaptation with Consistency Training**
[[Paper]](https://arxiv.org/pdf/2010.07539.pdf)
[[Code]](https://github.com/Jiaolong/ss-da-consistency)<br>
Description: This paper adds a consistency loss based on mutual information theory to the main task loss and pretext loss in a domain adaption tasks. 

- **Self-supervised Domain Adaptation for Computer Vision Tasks**
[[Paper]](https://arxiv.org/pdf/1907.10915.pdf)
[[Code]](https://github.com/Jiaolong/self-supervised-da)<br>
Description: This paper proposes a generic method for domain adaptation with self-supervised visual representation learning. The authors focus on the image rotation prediction pretext learning task with prediction layer alignment and batch normalization calibration to further boost the self-supervised domain adaptation.

- **Self-supervised Label Augmentation via Input Transformations**
[[Paper]](https://arxiv.org/pdf/1910.05872.pdf)
[[Code]](https://github.com/hankook/SLA)<br>
Description: This paper proposes a simple yet effective approach utilizing self-supervision on fully-labeled datasets via learning a single unified task with respect to the joint distribution of the original and self-supervised labels. 

- **Self-Supervised Learning of Pretext-Invariant Representations**
[[Paper]](https://arxiv.org/pdf/1912.01991.pdf)<br>
Description: PIRL learns representations that are invariant to the transformation t and retain semantic information.

- **S4L: Self-Supervised Semi-Supervised Learning**
[[Paper]](https://openaccess.thecvf.com/content_ICCV_2019/papers/Zhai_S4L_Self-Supervised_Semi-Supervised_Learning_ICCV_2019_paper.pdf)<br>
Description: This paper bridges the gap between self-supervision methods and semi-supervised learning by suggesting a framework (S4L) which can be used to turn any self-supervision method into a semi-supervised learning algorithm.

- **Self-supervised Representation Learning with Relative Predictive Coding**
[[Paper]](https://openreview.net/pdf?id=068E_JSq9O)<br>
Description: This paper introduces Relative Predictive Coding (RPC), a new contrastive representation learning objective that maintains a good balance among training stability,
minibatch size sensitivity, and downstream task performance. The key to the success of RPC is two-fold. First, RPC introduces the relative parameters to regularize the objective for boundedness and low variance. Second, RPC contains no logarithm and exponential score functions, which are the main cause of training instability in prior contrastive objectives.

- **Towards Good Practices in Self-supervised Representation Learning**
[[Paper]](https://arxiv.org/pdf/2012.00868.pdf)<br>
Description: This paper makes several contributions based on their empirical studies: 1) They empirically show why MLP head helps contrastive instance learning and visualize it using a feature inversion approach. 2) They present the semantic label shift problem caused by strong data augmentation in supervised learning and study the difference between supervised and contrastive learning. 3) They investigate on negative samples and find that good practices can help to eliminate the need of using large number of them, thereby could simplify the framework design.

- **Universal Domain Adaptation through Self-Supervision**
[[Paper]](https://arxiv.org/pdf/2002.07953.pdf)
[[Code]](https://github.com/VisionLearningGroup/DANCE)<br>
Description: This paper proposed two novel self-supervised techniques, such as neighborhood clustering and entropy separation, dealing with arbitory category shift in domain adaptation tasks. 

- **Unsupervised Domain Adaptation through Self-Supervision**
[[Paper]](https://arxiv.org/pdf/1909.11825.pdf)
[[Code]](https://github.com/yueatsprograms/uda_release)<br>
Description: The key contribution of this work is to draw a connection between unsupervised domain adaptation and self-supervised learning. The main idea is to achieve alignment between the source and target domains by training a model on the same task in both domains simultaneously. 

- **Unsupervised Intra-domain Adaptation for Semantic Segmentation through Self-Supervision**
[[Paper]](https://openaccess.thecvf.com/content_CVPR_2020/papers/Pan_Unsupervised_Intra-Domain_Adaptation_for_Semantic_Segmentation_Through_Self-Supervision_CVPR_2020_paper.pdf)
[[Code]](https://github.com/feipan664/IntraDA)<br>
Description: This paper applied self-supervised technique to minimize both inter-domain and intra-domain gap simultaneously for domain adaptation tasks in semantic segmentation.

### Natural Language Processing

- **Cross-Domain Sentiment Classification With In-domain Contrastive Learning** 
[[Paper]](https://arxiv.org/pdf/2012.02943.pdf)<br>
Description: This paper applies two data augmentation methods, i.e., synonym substitution and back translation, to define pretext task in contrastive learning. 

- **Evaluating Models’ Local Decision Boundaries via Contrast Sets** 
[[Paper]](https://arxiv.org/pdf/2004.02709.pdf) 
[[Code]](https://allennlp.org/contrast-sets)<br>
Description: Contrast sets provide a local view of a model's decision boundary, which can be used to more accurately evaluate a model's true linguistic capabilities. This paper proposed a new annotation paradigm for NLP to generate contrast samples. 

- **Self-Supervised Dialogue Learning** 
[[Paper]](https://arxiv.org/pdf/1907.00448.pdf)<br>
Description: This paper We proposes a general framework to jointly learn self-supervised network (SSN) and the dialogue models, where the sequential order in dialogues can be explicitly used to guide the utterance generation.

- **Self-Supervised Learning for Contextualized Extractive Summarization** 
[[Paper]](https://www.aclweb.org/anthology/P19-1214.pdf)
[[Code]](https://github.com/hongwang600/Summarization)<br>
Description: This paper aims to improve contextualized extractive summarization task by introducing three auxiliary pre-training tasks, i.e., mask, replace, and switch, that learn to capture the document-level context in a self-supervised fashion.

### Others

- **Contrastive Multi-View Representation Learning on Graphs**
[[Paper]](https://arxiv.org/pdf/2006.05582.pdf)<br>
Description: This paper applies self-supervised approach to learn contrasting structural views of graphs. The authors mention contrasting encodings form first-order neighbors and a graph confusion is more effective than multi-scale encodings in some graph classification benchmarks. 

- **Federated Self-Supervised Learning of Multi-Sensor Representations for Embedded Intelligence**
[[Paper]](https://arxiv.org/pdf/2007.13018.pdf)<br>
Description: This paper hypothesizes that the fusion of self supervision with federated learning could result in an effective method for learning from unlabeled, private, and diverse types of sensory data, which is crucial for several embedded (personalized) machine learning tasks.

### Blogs

- **Self-Supervised Representation Learning**
[[Link]](https://lilianweng.github.io/lil-log/2019/11/10/self-supervised-learning.html)

- **Contrastive Learning**
[[Link]](https://github.com/HobbitLong/PyContrast)

- **Awesome Self-supervised Learning**
[[Link]](https://github.com/jason718/awesome-self-supervised-learning)

