---
title: "Dropout as a Bayesian Approximation"
description: "Notes on the paper by Gal & Ghahramani"
publishDate: "8 March 2026"
tags: ["deep learning", "paper"]
---

## The paper

- Authors: Gal & Ghahramani
- Date: 2016
- Title: Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning.
- Conference: International Conference on Machine Learning

## The softmax problem

Something that can be bothering with neural networks in a classification problem is that it can predict a 'probability' of 0.98 on an input it has never seen. That sounds wrong. And it is. The softmax score is just a normalization. It tells you which class the model favors, not how confident it actually is. Feed a picture of an elephant to a model trained for cat/dog discrimination, and it will still give you a confident answer. That's a problem.

Bayesian approaches (like Bayesian Neural Networks) can give you proper uncertainty, but they're expensive and complicated to implement. This paper offers a nicer story.

## The main idea

The authors show that training a neural network with dropout is mathematically equivalent to approximate variational inference in a Gaussian Process. In other words, dropout (commonly used to regularize a model training) implicitly defines a distribution over weights, not just a single point estimate.

The practical consequence is that you can extract uncertainty from a model you already have, without changing anything about its architecture or retraining it.

## MC Dropout

The trick is simple. Normally, dropout is disabled at inference time. Here, you keep it on. You run the same input through the network $T$ times, each time dropping different neurons at random. You get $T$ slightly different predictions.

- The mean of those $T$ outputs is your final prediction.
- The variance is your uncertainty estimate.

## Why it works (briefly)

Minimizing the loss with dropout turns out to be equivalent to minimizing the KL divergence between a variational distribution $q$ and the true (intractable) posterior over the network weights. So we're doing Bayesian inference without realizing it.

## Limits

The inference cost scales with $T$ ($T \sim 10$ is ok). On large models, that adds up quickly.

Also, the experiments in the paper are mostly on small MLPs. How well this scales to modern architectures (Transformers, large CNNs) is still an open question as far as I know.