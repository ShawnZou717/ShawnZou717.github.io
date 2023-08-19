---
layout: post
title: Transformer Analysis
date: 2023-08-03 11:57:00+0800
description: a plain introduction of Transformer and professional derivation of its forward and backward propagation
tags: Transformer
categories: deep-learning
related_posts: false
---

## Table of Contents
- [Table of Contents](#table-of-contents)
- [Transformer Architecture](#transformer-architecture)
- [Forward Propagation](#forward-propagation)
  - [Word Embedding](#word-embedding)


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
---
In 2017, Google posted a paper named [Attention is All You Need](https://arxiv.org/abs/1706.03762v4) in arXiv bringing Transformer into history. Though Transformer follows the `seq2seq` structure (also known as `decoders and encoders`), its encoders and decoders consist of sole `self-attention` modules instead of `RNN` and `CNN` like most other NLP models. This is exactly the origin of the article title, a neural network composed entirely of `self-attention` mechanisms. Now let's take the classic Transformer as an example reviewing this unique model. Below shows the simplified structure of Transformer and detailed composition of encoders and decoders.

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

Transformer model stacks 6 encoders and 6 decoders, ahead by a source embedding and a target embedding networks, end with a softmax classifier. Embedding units can be self-constructed algorithms or pre-trained networks such as `Word2Vec`. The encoder and decoder have a very similar structure, only that the decoder has one extra layer of `ADD & NORM` and one extra layer of `Multi-head Attention`. In addition, it should be noted that a mask operation has been added to the 1st `Multi-head Attention` layer of each decoder, which aims to use the `seq2seq` structure while ensuring the parallelism of the network. The softmax classifier consists of a `Linear Transformation` and a `Softmax` layer. The `Linear Transformation` maps the word vector to `one-hot` vector whose size is equal to the size of the dictionary. Let's analyzing these 4 kinds of units in detail while deriving Transformer's forward propagation.

## Forward Propagation
---

### Word Embedding

First let's see what is `one-hot` encoding. The input of word embedding network is `ont-hot` word vector. Say we have 32000 words in a English lexicon ranking in dictionary order. `One hot` method transforms each word to a vector of length 32000 with 31999 zero values and 1 one value locating at the word's index in lexicon. For example, we all know (At least every Chinese student knows) the **abandon** ranks no.1 in all High School English dictionaries of China. That make **abandon**'s `one-hot` vector be $[1, 0, 0, ...0]$, vector length = 32000. Same as other words.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/one-hot-encoding.jpg" class="img-fluid d-block mx-auto rounded z-depth-1" max-width="80%" zoomable=true %}
    </div>
</div>
<div class="caption">
    one hot encoding
</div>

`Word Embedding` maps words into intensive vectors. An intensive vector is such a vector of length far smaller than the dictionary size and indicating the relationship of words by their space distrution. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/word-embedding-space.jpeg" class="img-fluid d-block mx-auto rounded z-depth-1" max-width="80%" zoomable=true %}
    </div>
</div>
<div class="caption">
    word embedding space (Chinese characters as an example), come from [csdn blog](https://blog.csdn.net/Alex_81D/article/details/114287498)
</div>