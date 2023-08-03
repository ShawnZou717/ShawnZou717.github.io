---
layout: post
title: Transformer Analysis
date: 2023-08-03 11:57:00+0800
description: function derivation in forward and backward propagation of transformer
tags: Transformer
categories: deep-learning
related_posts: false
---

## Table of Contents
- [Table of Contents](#table-of-contents)
- [What's Transformer?](#whats-transformer)


Among all the deep learning models, Transformer can be the most widely talked over one thanks to the tremendous performance that ChatGPT, a Transformer-based model, has shown in being a satisfying personal assistant and nice chatbot friend. As a powerful mathematical tool, Transformer has helped us in language translation, DNA recognition, medical research and many aspects in other research area. I believe it is safe to say that one day we all may need to apply this model in our project. Thus, a solid understanding of Transformer architecture is neccesary. To this end, this blog focuses on derivation of detailed functions in transformer tranining process.


## What's Transformer?

Tranformer is an advanced neural network model first proposed by Google in the paper [*Attention is All You Need*](https://arxiv.org/abs/1706.03762v4). Transformer consists of decoders and encoders (also known as `seq2seq` structure) like most of the NLP models, but instead of using RNN (Recurrent Neural Networks) and CNN (Convolution Neural Networks), . 

