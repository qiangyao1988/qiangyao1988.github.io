---
title: Reading notes of paper "Answer Identification from Product Reviews for User Questions by Multi-task Attentive Networks"
date: 2019-10-01
categories:
- Paper Digest
tags:
- Question Answering
- Natural Language Processing
---

This paper "Answer Identification from Product Reviews for User Questions by Multi-task Attentive Networks" is published in AAAI 2019 by Long Chen, Ziyu Guan. The authors propose a novel multi-task attentive model named QAR-net to identify plausible answers from product reviews for user questions.

### Contributions

There are two main contributions of this paper. First, they develop a novel multi-task deep learning method to leverage both users generated QA data and manually labeled QR data to identify plausible answers in reviews. Second, they construct a manually labeled QR dataset from Amazon dataset, researchers can work on this dataset in the future. 

### Background

Let me first introduce some background knowledge of **Question Answering (QA)**. There are several different kinds of QA in the literature. 

Open-World and Closed-World: An open-world question-answering dataset constitutes a set of question-answer pairs accompanied by a knowledge database, with no explicit link between the question-answer pairs and knowledge database entries. In closed-world question answering, the associated snippets are sufficient to answer all corresponding questions.

Span-based Answers: The answers are multi-word spans from the context. The answers are select form the context of the knowledge base, the results show the begin and end words as the span. These answers can be evaluated by accuracy or other confusion matrices for the classification task.

Free-form Answers: Systems generate free-form answers and are evaluated by automatic metrics such as ROUGE-L and BLEU-1.

Community/Opinion Question Answering: The answers are from reviews or some community responses. 

Researchers are working on QA mainly in two different areas, Textual Question Answering and Visual Question Answering (VQA). In Textual Question Answering, the answer is found in a specific textual narrative ( i.e. reading comprehension) or in large knowledge bases ( i.e. information retrieval). VQA is an extension of Textual Question Answering with additional visual supporting information. In VQA, given an image and question in natural language, it requires reasoning over visual elements of the image and general knowledge to infer the correct answer, typically a few words or a short phrase. There are four different approaches to deal with the QA problems: joint embedding method, attention mechanisms, compositional models, and knowledge base enhanced approaches. 

### Preliminary

#### Inspiration

1. Most e-commerce Websites now offer a Question Answering (QA) system that allows users to ask other users who have purchased the product some information about the products.
2. Many times, users still need to wait patiently for others' replies.
3. Customer reviews are an invaluable source of information where the user question can be answered.
4. It is unrealistic for a user to browse through the massive customer reviews for answers.
5. It is possible to identify answers automatically from reviews and respond to the users instantly.

#### Example

![](../../../../../assets/images/papernotesimgs/14.png){:style="margin:0 auto"}

Shown in the above picture, P is the product containing some information, Q is the customers' question, A is the corresponding answer, R is the review selected form the customers' reviews. Form the two examples, we can see there is some useful information in the reviews which can be the answer to the questions.

#### Two tasks

The authors claim two tasks in their approach, one is QR binary prediction problem (can answer or not) as the main task, another is QA binary prediction as an auxiliary task. They also indicate that it would not be a good idea to simply train answer identification models for reviews by supervision on user generated QA data,

in my opinion, it is not very clear and reasonable, as there are already some other researchers working in this way. The main purpose of this QA problem is to identify answers automatically from reviews like what they claim in the introduction part, and there are many approaches dealing with this problem and their results seem good. If their work is just predicting the question can be answered or not, it does not make too much sense. In my opinion, one step further could make their work much more meaningful.

#### Problem Formulation

QR pairs: Q is a user submitted question, R is a review sentence (the authors take sentences as the basic unit of reviews instead of the whole reviews), y is the binary label indicating whether R can answer Q.

QA pairs: A is the answer to the question provided by customers, y is the binary label indicating whether A can answer Q similarly.

After the training process, given a new pair (Qnew; Rnew), the model can accurately predict whether Rnew can answer Qnew. In this way, their task is a simple classify problem. 

### Algorithm

#### Model Architecture

The model consists of three different parts: text embedding, attention pooling, fusion and output. The model is very simple and does not contain any new techniques. 

![](../../../../../assets/images/papernotesimgs/15.png){:style="margin:0 auto"}

Text Encoding: Each word in the review, question and answer sentences is first converted to its respective word-level embedding vector **et** and character-level embedding vector **ct**. The word-level embedding vector **et** comes from pre-trained GloVe embeddings, while the character level embedding vector **ct** is from the final hidden states of a bi-directional RNN (bi-RNN) applied to **wt**'s characters and trained with the model, the authors claim the character level embedding can help handle out-of-vocabulary words. I am wondering how this character-level embedding helps in the training process, if it could improve the results a lot, I can also try to add this character-level embedding in my models. They choose the bi-GRU network after embedding layers to generate low-level representation **ht** for each word due to the computational efficiency of bi-GRU comparing with LSTM. The following equations show the computation of bi-GRUs to get forward and backward hidden states respectively. Concatenating the two hidden states can get the complete hidden state. 

Finally, the results of the text encoding part are three different matrices representing A, R and Q, they are $H^A \in R ^{2u \times m}$, $H^R \in R ^{2u \times l}$,  and $H^A \in R ^{2u \times n}$,  respectively.

#### Attention Pooling

The purpose of the attentive pooling step is to extract salient patterns from questions, answers, and reviews, so that more efficient and accurate matching can be performed in the subsequent steps. For the two tasks, the authors design two different attention mechanisms. In order to extract the mapping patterns between Q and A, they set a bi-attention module, while a self-attention module to distill focus-related keywords in R corresponding to Q. 

​     The bi-attention module is shown in the following figure, the inputs are the two matrices ***HQ\*** and **HA**，the outputs are two fixed-length vector representations ***rQA*** and **rAQ** in two directions. Let me introduce the process step by step. 

![](../../../../../assets/images/papernotesimgs/17.png){:style="margin:0 auto"}

 The first step is to compute an affinity matrix G. This matrix provides a soft mapping between words in **Q** and **A** in terms of the obtained hidden vectors. The (i; j)-th entry of G reflects the similarity between ***hAi\*** and *hQj.* **U** here is a parameter matrix. 

![](../../../../../assets/images/papernotesimgs/18.png){:style="margin:0 auto"}

​     The second step applies row-wise summation and column-wise summation on

G to obtain score vectors RowSum(G) and ColSum(G) to calculate the attention vectors ***aQA*** and **aAQ** in two directions respectively (**Q** to **A** and **A** to **Q**). The author points here that they use sum pooling rather than max-pooling because sum pooling

could better reflect the overall importance of words. 

![](../../../../../assets/images/papernotesimgs/19.png){:style="margin:0 auto"}

  The final step gets the attention-weighted representations of **Q** and **A**.

![](../../../../../assets/images/papernotesimgs/20.png){:style="margin:0 auto"}

   The self-attention mechanism is similar to other soft attention methods. U and v are the parameters need to be trained in the model. The input of this module is the matrix of review sentences ***HR\***, and the output ***rR*** is attention-weighted representations of this matrix. 

![](../../../../../assets/images/papernotesimgs/21.png){:style="margin:0 auto"}

#### Fusion and Output

As there are totally three outputs of the attention pooling layer, ***rQA, rAQ*** and **rR**, the fusion module consists of two sequential steps to get the final outputs. The first step is to get the final output of the task QA binary prediction, and the results of the first step contribute to the final result of the task QR binary prediction. Here are the computation equations: 

![](../../../../../assets/images/papernotesimgs/22.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/23.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/24.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/25.png){:style="margin:0 auto"}

#### Loss functions

 The training objective functions for both QR and QA tasks are standard cross-entropy functions over the predictions ***^yQR\*** and***^yQA*** on training data. So the loss functions of the two tasks are like this: 

![](../../../../../assets/images/papernotesimgs/26.png){:style="margin:0 auto"}

 For the main task, the authors add two regularization terms. The first is to penalize the similarity between the two attention vectors, this L2 norm cost forces the ***aR\*** to capture keywords other than those related to answer patterns : 

![](../../../../../assets/images/papernotesimgs/27.png){:style="margin:0 auto"}

Another regularization term is imposed on the attention-weighted representations of **Q** and **R**. Since for positive pairs we want both of them to capture the question focus, we penalize their Euclidean distance as follows:

![](../../../../../assets/images/papernotesimgs/28.png){:style="margin:0 auto"}

In this situation, the loss function of the main task is now:

![](../../../../../assets/images/papernotesimgs/29.png){:style="margin:0 auto"}

### Experiments

#### Datasets

The QA pairs and reviews are collected from two domains "Electronics" and "Cellphones & Accessories". They treat the top-voted answer as a positive QA pair and two answers from other products of the same domain as negative QA pairs. 

#### Implementation Details

They use Stochastic Gradient Decent (SGD) to train neural networks and apply Adam in the training process. They also apply dropout to the outputs of the Bi-GRU layer with a dropout rate of 0.5 to prevent overfitting.

#### Compared Methods

QREM(question review embedding matching): first embedding the sentences into matrices of word vectors, then employ row-wise max, min, and average pooling,

and concatenate the pooling results to generate the final fixed-length vectors, by using cosine similarity and threshold trained by logistic regression to generate the final classification labels.

QAR-net: it is the method of this paper.

QAR-net-QR: only train QAR-net with the QR task

QA-net-QA: only use QA pairs for training

QA-net-QR: only use QR pairs for training

QA-net-MTL: QA-net with both QA and QR training tasks

CQA-hard: employ CNN on the QA and QR pairs respectively and use the output of fully connected(FC) as the final predict labels.

NLP-soft: a modified version of the dependency parsing model 

#### Evaluation Metrics

As the dataset is highly imbalanced, they use precision, recall, F-measure and

Precision-Recall curves to evaluate these methods.

#### Results

**Main Results:** In their results, I am wondering why the results of the method QREM and CQA-hard could be so bad, both the tasks are binary classification, the results should be better. 

![](../../../../../assets/images/papernotesimgs/30.png){:style="margin:0 auto"}

![](../../../../../assets/images/papernotesimgs/31.png){:style="margin:0 auto"}

**Pre-training Degree:** To check the influence of pre-training, they vary the number of epochs from 10 to 100. The best performance is achieved at around 20 epochs shown in the figure. 

![](../../../../../assets/images/papernotesimgs/32.png){:style="margin:0 auto"}

**Regularization Terms:** From the ablation study, they conclude the two regularization terms are efficient and can help the attention module capture important patterns for QR matching

![](../../../../../assets/images/papernotesimgs/33.png){:style="margin:0 auto"}

**Parameter Study:** The following figure shows the effects of different hyper-parameters. I like the way they check and select the final set of parameters. 

![](../../../../../assets/images/papernotesimgs/34.png){:style="margin:0 auto"}

**Attention Visualization:** From the following figure, we can see the model can capture the most import words by the attention module. I think this attention visualization part needs to be more convincing, instead of just a toy-like example.

![](../../../../../assets/images/papernotesimgs/35.png){:style="margin:0 auto"}

### Conclusion

In this paper, the authors propose a novel multi-task attentive model named QAR-net to identify plausible answers from product reviews for user questions.

#### My opinion

In my opinion, the paper does not have any innovation point at all, the QA task has already come up in some other papers. And their bi-attention module is also not new in this research area. Although there is so many weakness in this paper, I still like it. I think the idea of making some difficult tasks easier firstly is very helpful. For my own research, I also want to do something on the QA tasks, as a beginner, it is a really hard problem, find an easier way may be a good solution at first. I also like their presentation, it is clear and very easy to be understood. 

### Reference

Chen, Long, et al. "Answer identification from product reviews for user questions by multi-task attentive networks." *Proceedings of the AAAI Conference on Artificial Intelligence*. Vol. 33. No. 01. 2019.