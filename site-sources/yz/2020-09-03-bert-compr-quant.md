---
title: "BERT Compression: Data Quantization"
author: y-z
description: A survey of BERT compressin using data quantization.
icon: 
status: 
# template: 
hide: 
tags:
    - Model Compression
    - Quantization
cdate: 2020-09-03 19:16
mdate:
    - 2020-09-04 16:14
---

# BERT Compression: Data Quantization

***Contents***

[TOC]

---

Category: BERT
Keywords: Model Compression, Quantization
Slug: bert-compression-data-quantization
Comment_id: bert-compression-data-quantization
Series: BERT-Compression

# Introduction

Since 2018, BERT [@@devlin2019bert] and its variants
([@liu2019roberta], [@yang2019xlnet]) show significant
improvements in many Natural Language Processing tasks.
However, all these models contain a large number of
parameters, which results in prohibitive memory footprint
and slow inference. In order to overcome such problems, many
methods have been proposed to compress these large models.
In this post, I will survey papers that compress these large
models using **Data Quantization**.

**Data quantization** refers to representing each model
weight using fewer bits, which reduces the memory footprint
of the model and lowers the precision of its numerical
calculations. There are a few characteristics of data
quantization:

- It can reduce memory requirements.
- With proper hardware, it can also improve inference speed.
- It can be applied to all different components of one model.
- It does not change the model architecture.

A straightforward idea is directly to truncate the weight
bits to the target bandwidth. However, this operation
usually leads to a large drop in
accuracy[@@ganesh2020compressing]. In order to overcome this
problem, the Quantization Aware
Training(QAT)[@@jacob2018quantization] approach is proposed.
Unlike simply truncating the weights, QAT quantizes the
weights and retrain the model to adjust the new weights.

# Data Quantization Papers

There are not many papers that directly quantizes the models
of the BERT model family.

[@zafrir2019q8bert] quantizes the all general matrix
multiply operations in BERT fully connected and embedding
layers. All these weights are quantized to 8-bit integers.
In the fine-tuning process, they manually introduce some
quantization error to let the model learn the error gap.
They use Straight-Through
Estimator(STE)[@@jacob2018quantization] to estimate the
gradient. According to their experiments, they claim they
can compress the model by $4$ times with minimal accuracy
loss.

Similarly, [@fan2020training] also tries to let the model
adjust to quantization during the training process. In this
paper, the authors made a simple modification to the QAT
approach.  The idea is, in the forward pass, they randomly
select a subset of weights instead of the full network as in
QAT.  Other parts of the weights remain the same. They call
this approach **Quant-Noise**. I think Quant-Noise is very
similar to the idea of dropout.

Instead of quantizing all the weights into the same
bandwidth, [@shen2020q] tries to quantizes models
dynamically. The motivation is different components (or
layers) of a model that have different sensitivity. We
should assign more bits to more sensitive components. In
this paper, they proposed a new hessian matrix-based metric
to evaluate the sensitivity of different layers.
Interestingly, in their experiments, they find that the
embedding layer is more sensitive than other weights for
quantization, which means the embedding layer needs more
bits to maintain accuracy.

# Summary

The above three papers are the only ones that I can find
involving applying data quantization to BERT style models. I
think one possible reason is that data quantization methods
can only reduce the model size, not the inference time.
Although data quantization can also improve the inference
speed with proper hardware, I hardly think anyone has such
hardware.

The list of data quantization papers:

- Q8bert: Quantized 8bit bert [@@zafrir2019q8bert] [pdf](https://arxiv.org/pdf/1910.06188.pdf)
- Training with quantization noise for extreme model compression [@@fan2020training] [pdf](https://yousiki.github.io/papers/files/2004.07320-QuantNoise.pdf)
- Q-BERT: Hessian Based Ultra Low Precision Quantization of BERT  [@@shen2020q] [pdf](http://amirgholami.org/assets/2019_QBERT.pdf)

The comparison between data quantization papers:

|         Paper        | Memory (BERT:100%) | Inference |  Component | Pretrain |   Performace   |
|:--------------------:|:------:|:---------:|:----------:|:--------:|:--------------:|
| [@zafrir2019q8bert] |   25%  |    N/A    | Float Bits |   False  |   very close   |
|  [@fan2020training] |   5%   |    N/A    | Float Bits |   False  |      worse     |
| [@shen2020q] |  7.8%  |    N/A    | Float Bits |   False  | slightly worse |


