---
title: "BERT Compression: Weight Pruning"
author: y-z
description: A survey of BERT compressin using weight pruning.
icon: 
status: 
# template: 
hide: 
tags:
    - Model Compression
    - Weight Pruning
cdate: 2020-09-03 19:37
mdate:
    - 2020-09-04 16:54
---

# BERT Compression: Weight Pruning

***Contents***

[TOC]

---

Category: BERT
Keywords: Model Compression, Weight Pruning
Slug: bert-compression-weight-pruning
Comment_id: bert-compression-weight-pruning
Series: BERT-Compression

## Introduction

Weight pruning is another line of work to compress BERT
style models. In this post, I will survey BERT related
weight pruning papers.

In general, weight pruning means identifying and removing
redundant or less essential weights and/or components.
Related work can be divided into three categories:

1. Prove the weights that are indeed redundant and prunable.
2. Element-wise pruning.
3. Structured pruning.

Just like the [data quantization](./2020-09-03-bert-compr-prun.md),
one characteristic of this line of work is, after pruning,
the weights usually become very sparse. Sparse weights can
reduce the model size largely. However, it can not speed up
the inference time. As a result, special hardware is needed
to achieve a decent computation speed-up after element-wise
pruning.

# Prove Weights are Redundant

This line of work empirically shows that weights of large
transformer-based models are indeed redundant. A significant
part of weights can be removed without hurting the final
performance. 

[@kovaleva2019revealing] conducts $6$ different experiments
regarding the attentions on BERT model. The authors conclude
that BERT model is highly over-parametered by showing a
repeated self-attention pattern in different heads.
Moreover, in their disabling experiments, they find that
both single and multiple heads are not detrimental to model
performance and, in some cases, even improves it. Their
experiments also show that the last two layers encode the
task-specific features and contribute to the performance
gain.

Similarly, [@michel2019sixteen] also conducts extensive
experiments to analyze the importance of attention heads in
transformer-based models. They perform their experiments on
WMT [@@ott2018scaling] and BERT [@@devlin2019bert]. In their
first setting, they remove each head to see the impact of
the removed head. They find that the majority of attention
heads can be removed without hurting too much from the
original score. They also find in some cases, removing an
attention head can increase performance, which is consistent
with the conclusions of [@kovaleva2019revealing]. To answer
the question that **is more than one head is needed?** they
remove all attention heads but one within a single layer.
Surprisingly, they find that one head is indeed sufficient
at test time. Next, they also try to prune these attention
heads iteratively. Experiments show that removing $20\%$ to
$40\%$ of heads does not incur any noticeable negative
impact. 

Consistent results are also found in the paper
[@voita2019analyzing]. But in [@voita2019analyzing], they
take a further step showing that some "important heads" can
be characterized into 3 functions: (i) positional (ii)
syntactic, and (iii) rare words. Besides, they also propose
a new pruning method by applying a regularized objective
when fine-tuning.  They observe that these specialized heads
are often the last to be pruned, which confirms their
importance.

# Element-wise Pruning

After empirically showing the weights are indeed redundant,
many pruning methods are proposed—one line of work focus on
identifying and removing individual weights of the given
model. The importance of each weight can be determined by
its absolute value, gradients, or other measurements defined
by designers. 

[@gordon2020compressing] apply a simple Magnitude Weight
Pruning [@@han2015learning] strategy on the BERT. Using this
strategy, they prune the BERT model from $0\%$ to $90\%$ in
increments of $10\%$. Their experiments show that using a
simple pruning strategy like magnitude weight pruning can
remove $30\%-40\%$ of the weights without hurting
pre-training loss or inference on any downstream task.
However, with the sparsities keeps increasing, the
pre-training loss starts increasing, and performance starts
degrading.

Similarly, [@sanh2020movement] uses a modified magnitude
weight pruning strategy to prune the weights.  The basic
idea is to learn a scoring matrix during training,
indicating the importance of each weight.  Intuitively,
magnitude selects the weights that are far from zero. In
contrast, movement pruning selects the weights that moving
away from zero during the training process. The experiments
show that using this modified magnitude weight pruning
method, BERT can achieve $95\%$ of the original BERT
performance with only $5\%$ of the encoder's weight on
natural language inference (MNLI) [@@williams2018broad] and
question answering (SQuAD v1.1) [@@rajpurkar2016squad].

Different from [@gordon2020compressing] and
[@sanh2020movement], which prune the weights depending on
the value of each weight, [@guo2019reweighted] use a
regularizer to constraint the weights. [@guo2019reweighted]
proposes a pruning method called Reweighted Proximal Pruning
(RPP), in which the authors iteratively reweight the
regularizer $L_1$.  In their experiments, they show that RPP
can achieve $59.3\%$ weight sparsity without inducing the
performance loss on both pre-training and fine-tuning tasks.

# Structured Pruning

Different from element-wise pruning, structured pruning
compresses models by identifying and removing component
modules, such as attention heads or embedding layers.

Self-attention in transformers is used to let the model find
the most related part of the input. However,
[@raganato2020fixed] show that replacing these **learnable**
attention heads with a simple fixed **non-learnable**
attentive pattern does not impact the translation quality.
These attentive patterns are solely based on position and do
not require any external knowledge.

[@fan2019reducing] propose a different structured pruning
method which adopts the idea of dropout. In learning neural
networks, we usually apply dropout to achieve better
performance. [@fan2019reducing] follows the same idea, but
here, they drop an entire layer instead of each weight. They
called this method **LayerDrop**. In the training time, they
sample a set of layers to be dropped in each iteration; in
the test time, we can choose how many layers we want to use
depending on the task and computation resources.

Instead of focusing on the attention heads or entire
transformer layers, [@wang2019structured] prune the model by
factorizing the weight matrices. The idea is to factorize
the matrix into two smaller matrices and inserting a
diagonal mask matrix. They prune the diagonal mask matrix
via regularization and use an augmented Lagrangian approach
to control the final sparsity.  One advantage of this method
is that this is generic, which can be applied to any matrix
multiplication.

# Summary

A list of weight pruning papers:

- Revealing the dark secrets of BERT [@@kovaleva2019revealing] [pdf](https://arxiv.org/pdf/1908.08593.pdf) 
- Are sixteen heads really better than one?  [@@michel2019sixteen] [pdf](https://papers.nips.cc/paper/9551-are-sixteen-heads-really-better-than-one.pdf)
- Analyzing Multi-Head Self-Attention-Specialized Heads Do the Heavy Lifting, the Rest Can Be Pruned  [@@voita2019analyzing] [pdf](https://arxiv.org/pdf/1905.09418.pdf)
- Compressing BERT-Studying the Effects of Weight Pruning on Transfer Learning  [@@gordon2020compressing] [pdf](https://arxiv.org/pdf/2002.08307.pdf)
- Reweighted Proximal Pruning for Large-scale Language Representation  [@@guo2019reweighted] [pdf](https://arxiv.org/pdf/1909.12486.pdf)
- Movement Pruning Adaptive Sparsity by Fine-Tuning  [@@sanh2020movement] [pdf](https://arxiv.org/pdf/2005.07683.pdf)
- Fixed encoder self-attention patterns in transformer-based machine translation  [@@raganato2020fixed] [pdf](https://arxiv.org/pdf/2002.10260.pdf)
- Reducing transformer depth on demand with structured dropout  [@@fan2019reducing] [pdf](https://arxiv.org/pdf/1909.11556.pdf)
- Structured Pruning of Large Language Models  [@@wang2019structured] [pdf](https://arxiv.org/pdf/1910.04732.pdf)

The comparison between weight pruing papers:

|           Paper           |  Memory (BERT:100%)| Inference |       Component       | Pretrain |   Performace   |
|:-------------------------:|:-------:|:---------:|:---------------------:|:--------:|:--------------:|
|    [@@zafrir2019q8bert]   |   N/A   |    N/A    |          N/A          |    N/A   |       N/A      |
|    [@@fan2020training]    |   N/A   |    N/A    |          N/A          |    N/A   |       N/A      |
|       [@@shen2020q]       |   N/A   |    N/A    |          N/A          |    N/A   |       N/A      |
| [@@gordon2020compressing] |  30~40% |    N/A    |      all weights      |   True   |      Same      |
|   [@@guo2019reweighted]   | 12%~41% |    N/A    |      all weights      |   True   |      worse     |
|    [@@sanh2020movement]   |  3%~10% |    N/A    |   layers and heads.   |   False  |      worse     |
|   [@@raganato2020fixed]   |   N/A   |    N/A    |    attention heads    |   False  |     similar    |
|    [@@fan2019reducing]    | 25%~50% |    N/A    |   transformer layers  |   True   |      same      |
|   [@@wang2019structured]  |   65%   |    N/A    | matrix multiplication |   False  | slightly worse |
