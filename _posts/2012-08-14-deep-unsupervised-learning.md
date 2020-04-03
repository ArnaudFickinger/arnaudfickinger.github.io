---
title: 'Deep Unsupervised Learning'
date: 2020-04-03
permalink: /posts/2020/04/deep-unsupervised-learning/
tags:
  - lectures
---

Flows
=

We got samples $(x_1, ..., x_n) \in X^n, X\subset \mathbb{R} \$ from un unknown probability distribution $p \in \Delta X$. We want
to fit the parameters of a model distribution $p_{\theta}$ and sample from it. If we have an idea of the form of $p$,
we can directly optimize $\theta$ for the log-likelihood of the data:
$$\theta^* = \text{argmax}_{\theta} \sum^n \log p_{\theta}(x_i)$$
Yet in the real world we have no idea of the form that might have $p$ and we don't want to have issue due to
[model mis-specification](https://jsteinhardt.wordpress.com/2017/01/10/latent-variables-and-model-mis-specification/).
  Therefore we want to optimize with the minimum of assumption on the structure of $p$. Here we only assume that
  $p$ has been obtained by transforming a known distribution (a gaussian for example) with a differentiable and invertible function:
$$p_{\theta}(x)dx = p(z)dz \\
    z = f_{\theta}(x) \\
    z \sim \mathcal{N}(0,1)
    $$
By injecting this in the log-likelihood of the data, the optimization problem becomes:
$$\theta^* = \text{argmax}_{\theta} \sum^n \log p(f_{\theta}(x_i)) + \log \frac{df_{\theta}}{dx}(x_i)$$
     
  
  
  
You can have many headings
======

Aren't headings cool?
-

