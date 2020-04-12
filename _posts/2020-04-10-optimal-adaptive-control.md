---
title: "Optimal and Adaptive Control"
date: 2020-04-10
permalink: /posts/2020/04/optimal-adaptive-control/
tags:
  - project
  - lectures
---


# Control

In the real world we can't usually observe the full state of the object we want to control. Thus we assume that a map between state and observation
is given:

$$h: S \times A \rightarrow O$$

In control theory the notations for the corresponding variable are $x$, $u$ and $y$.

What happen is that many states can be mapped to the same observation. In RL we have seen that
in general there is no policy on observation that reach the optimal behavior.

It's important to think about the state and not just the observation because the dynamics
is given for the state threw a vector valued differential equation: 

$$f: S \times A \rightarrow \mathbb{R}^{dim(S)} \\
f(x,u) = \.{x}$$



