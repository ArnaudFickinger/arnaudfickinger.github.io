---
title: 'Machine Learning'
date: 2020-04-05
permalink: /posts/2020/05/machine-learning/
tags:
  - lectures
---

# Classification

Every binary classifiers can be characterized by the shape of their *decision boundary*. Let's talk about two mainly used classifier:
* The decision boundary of the *linear classifier8 is the hyperplane that best separate the data.
* The decision boundary of the *nearest-neighbour classifier* is the Voronoi diagram separating only points from two different classes
* The decision boundary of the K-nearest-neighbours classifier becomes smoother as K increases. Since the algorithm use majority voting, K must be odd.

>How to compute the decision boundary of the K-nearest classifier?

We *validate* a classifier by computing the *test set error*. A method that has low training error but high test error is *overfitting* the training data. If
it has low test set error, it *generalizes* well.

*Last update: L1 1h*