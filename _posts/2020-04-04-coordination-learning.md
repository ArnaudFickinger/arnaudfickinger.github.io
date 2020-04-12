---
title: "Coordination Learning"
date: 2020-04-04
permalink: /posts/2020/04/gibbard-theorem-and-irl/
tags:
  - research
---

# Abstract

In this post I will show that when an IRL system aggregates demonstrations from multiple humans, the best response trajectory for a self-interested human
is not the expert trajectory. 

# Motivation

> Show that coordination literature don't use imitation learning methods and imitation learning don't think about coordination

Instead of learning from a reward signal, Imitation Learning learn from observing optimal trajectories. This method is oftem
related to young children that learn by imitating. Imitation of a trajectory performed by an agent with a different action set
has been studied in this [paper](https://arxiv.org/pdf/1703.01703.pdf).

Yet when observing someone doing a task, the natural reaction is not to imitate but rather to assist. Hence we want to come up
with a method to transform a trajectory on an action space $A_H$ into a trajectory on a joint action space $A_H \times A_R$.

# Experiment

# Related Work

In [Third Person Imitation Learning](https://github.com/bstadie/third_person_im), Stadie et al. generate a policy that perform well
in an environment slightly different from the expert. In Theory they assume different action spaces
but in practice they perform only minor modification like changing the camera angle, the color of the 
targets and length of the arm 
