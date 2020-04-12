---
title: 'Deep Unsupervised Learning'
date: 2020-04-03
permalink: /posts/2020/04/deep-unsupervised-learning/
tags:
  - lectures
---

# Flow Models


We got samples $(x_1, ..., x_n) \in X^n, X\subset \mathbb{R} \$ from an unknown probability distribution $p \in \Delta X$. We want
to fit the parameters of a model distribution $p_{\theta}$ and sample from it. If we have an idea of the form of $p$,
we can directly optimize $\theta$ for the log-likelihood of the data:

$$\label{eq:1} \theta^* = \text{argmax}_{\theta} \sum^n \log p_{\theta}(x_i)$$

Yet in the real world we have no idea of the form that might have $p$ and we don't want to have issue due to
[model mis-specification](https://jsteinhardt.wordpress.com/2017/01/10/latent-variables-and-model-mis-specification/).
  Therefore we want to optimize with the minimum of assumption on the structure of $p$. Here we only assume that
  $p$ has been obtained by transforming a known distribution (a gaussian for example) with a differentiable and invertible function:

$$\label{eq:2} p_{\theta}(x)dx = p(z)dz \\
    z = f_{\theta}(x) \\
    z \sim \mathcal{N}(0,1)
    $$
    
By injecting this model $\ref{eq:2}$ in the log-likelihood of the data $\ref{eq:1}$, the optimization problem becomes:

$$\theta^* = \text{argmax}_{\theta} \sum^n \log p(f_{\theta}(x_i)) + \log |\frac{df_{\theta}}{dx}(x_i)|$$
     
>Is there a derivative operator in the AutoDif package? What is the coast to include the derivative of the output in the objective?
>
>In PyTorch the method torch.autograd.grad() can be used to include derivative in the objective

In practice we represent the flow $f$ as the output of a neural network and optimize $\theta$ using stochastic gradient descent.
Once $\theta$ has been optimized we can sample from $p$ following:

$$ z \sim \mathcal{N}(0,1) \\
    x = f_{\theta}^{-1}(z)
    $$
    
>What is the family of invertible NN and how can we efficiently invert the output? 
>
>Any compositions of invertible and differentiable functions is also invertible and differentiable. For a 
>continuous variable, we just have to take invertible activation functions like Sigmoid or Tanh. For more dimension, we might make sure that the weight matrices keep invertible.

Coming back to our first motivation to alleviate model mis-specification, we might wonder how large is the set of distributions 
we can reach with this method. For continuous one-dimensional variable, every distribution can be reached by a flow. To see that, consider 
a distribution $p \in \Delta \mathbb{R}$ with Cumulative Distribution Function $F$ and define $F^{-1}$ as:

$$\forall u \in [0,1], F^{-1}(u) = \inf \{x: F(x)=u\}$$

Then, if U is the uniform distribution on [0,1], the CDF of $F^{-1}(U)$ is F:

$$
\forall x \in \mathbb{R}, p(F^{-1}(U)\leq x) = p(U \leq F(x)) = F(x)
$$
  
*Last Update: L3 1h*
