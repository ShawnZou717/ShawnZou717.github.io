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

Recently, a great personal assistant and chit-chat robot ChatGPT gained a lot of attention. Unlike other wooden voice assistants on our phones such as Siri, ChatGPT can process textual and semantic information in natural language, meaning it can talk to people continuously on a given topic and understand undelying meanings. Find it hard to believe? Let's have a try.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/ChatGPT_joke.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

You can see that not only can ChatGPT keep the conversation but also give natural responses to my PhD joke. Why is it so fluent and elegant? What sets ChatGPT apart from Siri and Bixby? The reason is the powerful informatic extraction ability of ChatGPT's submodule, Transformer. Transformer's application extends way out of NLP domain. As a powerful mathematical tool, it has helped us in DNA recognition, medical research and many aspects in other research area. I believe it is safe to say that one day we may all need to apply this model in our project. Thus, a solid understanding of Transformer architecture is neccesary. To this end, this blog focuses on a comprehensive introduction of Transformer.

## Transformer Architecture
---
In 2017, Google posted a paper named [Attention is All You Need](https://arxiv.org/abs/1706.03762v4) in arXiv bringing Transformer into history. Though Transformer follows the `seq2seq` structure (also known as `decoders and encoders`), its encoders and decoders consist of sole `self-attention` modules instead of `RNN` and `CNN` like most other NLP models. This is exactly the origin of the article title, a neural network composed entirely of self-attention mechanisms. Now let's take the classic Transformer as an example reviewing this unique model. Below shows a simplified Transformer structure and detail composition of encoders and decoders.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/transformer-entire.png" class="img-fluid d-block mx-auto rounded z-depth-1" max-width="60%" max-height="60%" zoomable=true %}
    </div>
</div>
<div class="caption">
    Simplified Transformer Structure
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/transformer-en-decoders.png" class="img-fluid d-block mx-auto rounded z-depth-1" max-width="60%" max-height="60%" zoomable=true %}
    </div>
</div>
<div class="caption">
    Transformer encoders and decoders
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/transformer-en-decoders.png" class="img-fluid d-block mx-auto rounded z-depth-1" max-width=60% max-height=60% zoomable=true %}
    </div>
</div>
<div class="caption">
    Transformer encoders and decoders
</div>

Transformer model stacks 6 encoders and 6 decoders, ahead by a source embedding and a target embedding networks, end with a softmax classifier. Embedding units can be self-constructed algorithms or pre-trained networks such as `Word2Vec`. The encoder and decoder have a very similar structure, only that the decoder has one extra layer of `ADD & NORM` and one extra layer of `multi-head attention`. In addition, it should be noted that a `mask operation` has been added to the 1st multi-head attention layer of each decoder, which aims to use the seq2seq structure while ensuring the parallelism of the network. The softmax classifier consists of a `linear transformation` and a `softmax` layer. To know more technique details of these operators, let's start orgnize the forward propagation of Transformer.

## Forward Propagation
---

### Word Embedding

Before we go further, I'd like to give you some preliminary knowledge about word encoding, that is the method for digitalizing human words as computers are not capable of recognizing human language sympols. The most widely used ones are `one-hot encoding` and `word embedding` methods.

* **One-hot encoding**

    One-hot encoding is a technique that transfers words into binary vector where each value represent one word in the lexicon. Fot a given word, the value at its corresponding position is turned on (set to be 1) while the others remain turned off (set to be 0). For example, we have RGB Tricolor, each color can be expressed by the following vectors:

    | Color | Vector |
    | :------------: | :------------: |
    |  red | [1, 0, 0] |
    | green | [0, 1, 0] |
    | blue | [0, 0, 1] |

    Though one-hot encoding solves the words digitalizing problem, the produced vector cannot be directly applied in the neural networks. Because neural networks are actually nothing else but layered matrix computations. While one-hot vectors combined together form a sparse matrix. This kind of matrix has far more 0 valued elements than other effective elements leading to a very low informatic density, i.e. a very small informatic volume and an extremely large matrix size. As a result, neural network models would suffer from huge computation complexity increases and only gain very poor language processing ability.

* **Word embedding**

    To tackle this problem, `word embedding` is proposed. This method aims to represent words with a intensive vector in a high dimension space, meanwhile the distance among vectors represent the textual and semantic similarity of their corresponding words. For example, all the words descripe emotions such as **happy** and **sad** should concentrate in one area after word embedding.

    There are some widely used word embedding methods including `Word2Vec`, `FastText` and `GloVe`. Wanna know more? Try asking ChatGPT about it. 

To specify the parameter shape of classic Transformer, we assume this Transformer is used for translating English to Germany with both 32,000 words lexicon. 

The input of word embedding network is `ont-hot` word vector. Say we have 32000 words in a English lexicon ranking in dictionary order. `One hot` method transforms each word to a vector of length 32000 with 31999 zero values and 1 one value locating at the word's index in lexicon. For example, we all know (At least every Chinese student knows) the **abandon** ranks no.1 in all High School English dictionaries of China. That make **abandon**'s `one-hot` vector be $[1, 0, 0, ...0]$, vector length = 32000. Same as other words.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/one-hot-encoding.jpg" class="img-fluid d-block mx-auto rounded z-depth-1" max-width="60%" max-height="60%" zoomable=true %}
    </div>
</div>
<div class="caption">
    One hot encoding
</div>

`Word embedding` maps words into intensive vectors. An intensive vector is such a vector of length far smaller than the dictionary size and indicating the relationship of words by their space distrution. The needs of `word embedding` encoding come from the intensive relevance of human word. Though `one hot` encoding gives accurate representation of each word, these vector are orthogonal to each other, that makes 

For example, in [Attention is All You Need](https://arxiv.org/abs/1706.03762v4), the intensive word vector size is set to be 512, while the `one-hot` vector size is 32000. Compressing the vector size can not only avoid the delimma of 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/transformer-analysis/word-embedding-space.jpeg" class="img-fluid d-block mx-auto rounded z-depth-1" max-width="60%" max-height="60%" zoomable=true %}
    </div>
</div>
<div class="caption">
    Word embedding space (Chinese characters as an example), come from csdn blog (https://blog.csdn.net/Alex_81D/article/details/114287498)
</div>