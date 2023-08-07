---
layout: post
title: Transformer Analysis
date: 2023-08-03 11:57:00+0800
description: a plain introduction of Transformer and professional derivation of its backward propagation
tags: Transformer
categories: deep-learning
related_posts: false
---

## Table of Contents
- [Table of Contents](#table-of-contents)
- [Transformer Architecture](#transformer-architecture)


Among all the deep learning models, Transformer can be the most widely talked over one thanks to the tremendous performance that ChatGPT, a Transformer-based model, has shown in being a personal assistant and chatbot. Never heard of it? Let's take a look at ChatGPT's own words.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/try-chatGPT.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    How ChatGPT introduces Transformer model
</div>

Transformer's application extends way out of NLP domain. As a powerful mathematical tool, it has helped us in DNA recognition, medical research and many aspects in other research area. I believe it is safe to say that one day we may all need to apply this model in our project. Thus, a solid understanding of Transformer architecture is neccesary. To this end, this blog focuses on a comprehensive introduction of Transformer.

## Transformer Architecture

In 2017, Google posted a paper named [Attention is All You Need](https://arxiv.org/abs/1706.03762v4) in arXiv bringing Transformer into history. Though Transformer follows the `seq2seq` structure (also known as `decoders and encoders`), its encoders and decoders consist of sole `self-attention` modules instead of `RNN` and `CNN` like most other NLP models. This is exactly the origin of the article title, a neural network composed entirely of `self-attention` mechanisms. Now let's take the classic Transformer as an example reviewing the unique model introduced by Transformer.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/transformer-entire.png" class="img-fluid d-block mx-auto rounded z-depth-1" max-width="80%" zoomable=true %}
    </div>
</div>
<div class="caption">
    Simplified Transformer Structure (Click on image to zoom in)
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/transformer-en-decoders.png" class="img-fluid d-block mx-auto rounded z-depth-1" max-width="80%" zoomable=true %}
    </div>
</div>
<div class="caption">
    Transformer encoders and decoders (Click on image to zoom in)
</div>

As shown in the above figures, the Transformer backbone is composed of 6 encoders and 6 decoders. The output of the end encoder is used for the Key and Value calculations of the 2nd `multi-head attention` in all decoders. The encoder and decoder have a very similar structure, only that the decoder has one extra layer of `ADD&NORM` and one extra layer of `multi-head attention`. In addition, it should be noted that a mask operation has been added to the 1st `multi-head attention` layer of each decoder, which aims to use the `seq2seq` structure while ensuring the parallelism of the network.