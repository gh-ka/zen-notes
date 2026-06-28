---
title: BERT Compression
author: y-z
description: A survery of BERT model compression
icon: 
status: draft
# template: 
hide: 
tags:
    - Model Compression
    - Quantization
cdate: 2020-08-06 18:45
mdate:
    - 2020-08-25 20:45
---

# BERT Compression

***Contents***

[TOC]

---

Category: Word-Representation
Keywords: Model Compression, Quantization
Slug: BERT-Compression
Comment_id: BERT-Compression

In the [A little history of wordrepresentation](./2020-05-09-word-repr-hist.md), I mentioned that [BERT][] model is 


## Why Do We Need Compression


## Data Quantization

Data quantization refers to representing each model weight
using fewer bits, which reduces the memory footprint of the
model and lowers the precision of its numerical
calculations. There are a few chatacteristics of data
quantization:

- It can reduce the memory requirment.
- With proper hardward, it can also improve inference speed.
- It can be applied to all different components of one model.
- It does not change the model architecture.

One simple idea is directly to truncate the weight bits to
the target bitwidth. However, this operation usually leads
to large drop in accuracy[@@ganesh2020compressing]. In order
to overcome this problem, the Quantization Aware
Training(QAT)[@@jacob2018quantization] approach is proposed.
Different from simply truncating the weights, QAT quantizes
the weights and retrain the model to adjust the new weights.

There are not many papers that directly quantizes the
models of BERT family.

**[@zafrir2019q8bert]** quantizes the all general matrix
mulitply operations in BERT Fully connected and embedding
layers. All these weights are quantized to 8 bit integers.
In the pretraining process, they manually introduce some
quantization error to let the model to learn the error gap.
They use Straight-Through
Estimator(STE)[@@jacob2018quantization] to estimate the
gradient. According to their experiments, they claim they
can compress the model by $4$ times with minimal accuracy
loss.

Similarly, [@fan2020training] also tries to let the model
adjust to quantization during training process. In this
paper, the authors made a simpel modification to QAT
approach.  The idea is, in the forward pass, they randomly
select a subset of weights instead of the full network as in
QAT.  Other parts of the weights remain the same. They
call this approach **Quant-Noise**. I think Quant-Noise is very
similar to the idea of dropout.

Instead of quantizing all the weights into the same
bitwidth, **[@shen2020q]** tries to quantizes models
dynamically. The motivation is different components (or
layers) of a model have different sensitivity. We should
assign more bits to more sensitive components. In this
paper, they proposed a new hessian matrix based metric to
evaluate the sensitivity of different layers. Interestingly,
in their experiments, they find that the embedding layer is
more sensitive than other weights for quantization, which
means embedding layer needs more bits to maintain the
accuracy.

The above three papers are the only ones that I can find
involving applying data quantization to BERT models. I think
one possible reason is that data quantization methods can only
reduce the model size not the inference time. Although, with
proper hardwares, data quantization can also improve the
inference speed, I hardly think any one has such hardwares.


## Weights Pruning

Weight pruning is another line of work to compress BERT
style models. In general, weight pruning means identifying
and removing redundant or less important weights and/or
components. Related work can be divided into three
categories:

1. Prove the weights are indeed redundant.
2. Element-wise pruning.
3. Structured pruning.

### Prove Weights are Redundant

This line of work emperically shows that weights of large
transformer-based models are indeed redundant. A significant
part of them can be removed without hurting the final
performance. 

[@kovaleva2019revealing] conduct $6$ different experiments
regarding the attentions on BERT model. The authors conclude
that BERT model is highly over-parametered by showing a
repeated self-attention pattern in different heads.
Moreover, in their disabling experiments, they found that
both single and multiple heads is not detrimental to model
performance and in some cases even improves it. Their
experiments also show that it is the last two layers that
encode the task-specific features and contributes to the
gain of performance.


Similarily, [@michel2019sixteen] also did a extensive
experiments to analyze the importance of attention heads in
transformer-based models. They conduct their experiments on
WMT [@@ott2018scaling] and BERT [@@devlin2019bert]. In their
first setting, they remove each head to see the impact of
the removed head. They found that the majority of attentions
heads can be removed without hurting too much from the
original score. They also found in some cases, removing an
attention head can increase performance, which is consistent
with the conclusions of [@kovaleva2019revealing]. To answer
the question that **is more then one head is needed?**, they
then remove all attention heads but one within a single
layer. Surprisingly, they found that one head is indeed
sufficient at test time. Next, they also try to prune these
attention heads iteratively. Experiments showed removing
$20\%$ to $40\%$ of heads does not incure any noticeable
negative impact. 

Consistent results are also found in the paper
[@voita2019analyzing]. But in [@voita2019analyzing], they
took a further step showing that some "important heads" can
be characterized into 3 functions: (i) positional (ii)
syntactic; and (iii) rare words. Besides, they also proposed
a new pruning method by applying a regularized objective
when fine-tuning.  They observe that these specialized heads
are often the last to be pruned, which confirms their
importance.

### Element-wise Pruning

After emperically showing the weights are indeed redundant,
many pruning methods are proposed. One line of work focus on
identifying and removing individual weights of the given
model. The importance of each weight can be determined by
its absolute value, gradients, or other measurements defined
by designers. One characterisitc of this line of work is,
after pruing, the weights usually become very sparse. Sparse
weights can reduce the model size largely, however, it can
not speed up the inference time. As a result, special
hardware is needed to achieve a decent computation speed-up
after element-wise pruning.

[@gordon2020compressing] apply a simple Magnitude Weight
Pruning [@@han2015learning] strategy on the BERT. Using this
strategy, they prune the BERT model from $0\%$ to $90\%$ in
increments of $10\%$. In their experiments, they showed that
using a simple pruning strategy like magnitude weight
pruning can remove $30\%-40\%$ of the weights without
hurting pre-training loss or inference on any downstream
task. However, with the sparsities keeping increasing, the
pre-training loss started increasing and performance
started degrading.

Similarly, [@sanh2020movement] used modified magnitude
weight pruning strategy to prune the weights.  The basic
idea is to learn a scoring matrix during training, which can
indicate the importance of each weight.  Intuitively,
magnitude selects the weights that are far from zero, while
movement pruning select the weights that moving away from
zero during the training process. The experiments showed
that using this modified magnitude weight pruning method,
BERT can achieve $95\%$ of the original BERT performance
with only $5\%$ of the encoder's weight on natural language
inference (MNLI) [@@williams2018broad] and question answering
(SQuAD v1.1) [@@rajpurkar2016squad].

Different from [@gordon2020compressing] and
[@sanh2020movement] which prune the weights depending on the
value of each weights, [@guo2019reweighted] used a
regularizer to constraint the weights. [@guo2019reweighted]
proposed a new pruning method called Reweighted Proximal
Pruning (RPP), in which the authors iteratively reweight the
regularizer $L_1$.  In their experiments, they showed that
RPP can achieve $59.3\%$ weight sparsity without inducing
the performance loss on both pre-training and fine-tuning
tasks.

### Structured Pruning

Different from element-wise pruning, structured pruning
compress models by identifying and removing component
modules, for example, attention heads or embedding layers.

Self-attention in transformers is used to let the model find
the most related part of the input. However,
[@raganato2020fixed] showed that replacing these
**learnable** attention heads with a simple fixed
**non-learnable** attentive pattern does not impact the
translation quality. These attentive patterns are solely
based on position and do not require any external knowledge.

[@fan2019reducing] proposed a different structured pruning
method which adopts the idea of dropout. In learning neural
network, we usually apply dropout to achieve a better
performance. [@fan2019reducing] follows the same idea, but
here, they drop a entire layer instead of each weights. They
called this method **LayerDrop**. In the training time, they
sample a set of layers to be dropped in each iteration; in
the test time, we can choose how many layers we want to use
depending on the task and computation resources.


Instead of focusing on the attention heads or entire
transformer layers, [@wang2019structured] prune the model by
factorizing the weight matrices. The idea is to factorize
the matrix into two smaller matrices and inserting a
diagonal mask matrix. They prune the diagonal mask matrix
via  regularization, and use an augmented Lagrangian
approach to control the final sparsity.  One advantage of
this method is that this is generic, which can applied to
any matrix multiplication.


## Knowledge Distillization


[BERT]: https://en.wikipedia.org/wiki/BERT_(language_model)
