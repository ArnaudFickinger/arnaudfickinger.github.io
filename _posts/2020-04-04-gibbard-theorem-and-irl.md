---
title: "Gibbard's Theorem and Inverse Reinforcement Learning"
date: 2020-04-04
permalink: /posts/2020/04/gibbard-theorem-and-irl/
tags:
  - research
---


# Abstract

In this post I will show that when an IRL system aggregates demonstrations from multiple humans, the best response trajectory for a self-interested human
is not the expert trajectory. 

# Motivation

Social choice theory is the branch of Economics modeling and analyzing collective decision-making
from the perspective of aggregating individual preferences. For example it is concerned with the 
design of fair voting systems. It is closely related to mechanism design, a branch of Game Theory
that is concerned with designing games where strategic players are incentivized to act truthfully. 
An important theorem lying at the intersection of both disciplines is the following: *any non-dictatorial
voting scheme with at least three possible outcomes is subject to individual manipulation*. In other words,
knowing the preferences of the others and adapting yours in consequence might change the outcome
in your advantage. 

In Inverse Reinforcement Learning, preferences are not shared directly to the system. Instead, the 
system observes a states-actions trajectory and compute a reward function such that the observed trajectory 
would have been produced by an optimal policy under that reward. For complex tasks, a lot of trajectories are 
aggregated in order to compute a good estimate of the reward function. Yet it is always assumed that the 
trajectories can be explained by the same reward function. In light of the issue in social 
choice theory discussed above, the question we want to answer is: *if an IRL system aims to compute the collective
preferences of two individuals by aggregating their two trajectories, does the expert trajectory remain the best response
of each individual?*

# Experiment

# Related Work

Because we compute the best response to an IRL system, our work is similar to Cooperative Inverse Reinforcement Learning. 
In this work, Hadfield-Menell et al. shows that the best response trajectory to an IRL system trying to infer
the preferences of a single human is not the expert trajectory, but rather involve active teaching.

