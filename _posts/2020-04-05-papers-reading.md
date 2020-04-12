---
title: 'Papers Reading'
date: 2020-04-05
permalink: /posts/2020/04/papers_reading/
tags:
  - reading
  - research
---



# The Gibbard–Satterthwaite theorem: a simple proof (Benoit 2000)

* Proof in the case of strict linear preference ordering
* The social choice function selects one alternative
* The theorem shown states that any unanimous and strategyproof SCF is a dictatorship
* The intuition behind this proof is that to prevent someone to hide his preferences,
at least one must actually decide 

> The proof assume that the alternative chosen by the dictator has been chosen by everyone before him. 
>Is it a restricted case? We just say that there is one dictator, we don't say that everyone can be a dictator!
>We show that the pivotal agent for one alternative is actually the pivotal agent for any alternative and thus a dictator

> Let's think of a multi-armed bandit setting


# Legibility and Predictability of Robot Motion (Dragan 2013)

* Legibility (intent-expressive) and predictability (intent-predictive) are different in Motion Planning:
    * Predictable motion: expert trajectory from the goal (what trajectory the human expect if he knows the goal, in this paper it's the expert)
    * Legible motion: enable to infer goal from trajectory (what trajectory will make the human understand the goal)

> We should get the same trajectories as the best response in CIRL since it's also from trajectory to goal. Here 
>I think the difference is that we infer the goal online, and the robot want us to infer goal as soon as possible.

* For the legible trajectory, they model human's goal inference with Bayesian inference on every portion of trajectory $S \rightarrow Q$:

    $$ G^* = \max_{\Xi_{S\rightarrow Q}} P(G|\Xi_{S\rightarrow Q}) \\
        P(G|\Xi_{S\rightarrow Q}) \propto P(\Xi_{S\rightarrow Q}|G)P(G) \\
        P(\Xi_{S\rightarrow Q}|G) = \frac{\int P(\Xi_{S\rightarrow Q \rightarrow G})}{\int P(\Xi_{S\rightarrow G})} $$
        
> I guess the marginal proba of a trajectory is a gaussian centered on the straight line
        
* As done in the MEIRL paper, they separate trajectories:
    $$ \int P(\Xi_{S\rightarrow Q \rightarrow G}) = P(\Xi_{S\rightarrow Q})\int P(\Xi_{ Q \rightarrow G})$$
    
> My concern is that it enables a quasioptimal trajectory to oscillate

* They use the principle of maximum entropy as a prior for $P(\Xi)$ and use Laplace's method and approximate $C$ as a quadratic (Hessian constant) to approximate the integral.

> Read about Laplace's method, Laplace prior and the paper of Levine of Laplace IRL


# Third Person Imitation Learning (IL) (Abbeel 2017)

> My idea of Coordination IL is to transform a human action set into a joint human-robot action set. Here, before
>reading, it sounds like it transforms human into robot so it seems very pertinent to my project. I am wondering 
>how do they train this transformation, and what is the scope of the trained model, ie can it generalize to other task? 
>Or does the human has different similar intention around the same task? Furthermore by reading the abstract they talk about
>domain confusion, I like the word and I am pretty exited to read about that.

* Domain Confusion was introduced in this [paper](https://arxiv.org/abs/1412.3474) as a method to improve generalization
on new image dataset

    > They include a loss that endure a domain invariant representation, so I guess they need example from
    >different dataset, so isn't it the same as learning a hierarchical representation or meta learning?

* They adapt GAIL to the third person. The difficulty is that matching raw features is not possible here and they alleviate this 
with [technique](http://proceedings.mlr.press/v37/ganin15.pdf) in domain adaptation.
http://proceedings.mlr.press/v37/ganin15.pdf

    > This paper add the domain adaptation idea to GAIl, we need to come up with another idea. What about coordination. What make coordination different than just third? The reward is different, hey can be multiple optimal policies. Even with the same action space it's challenging.                                                                                                                                                                                                                                                                                                                   

* Their reward is only a function of s, which make the domain adaptation easier since we can keep the same reward. The robot still need to see what action leads him to
what states. 

> In our case it's difficult to imagine the robot trying to see what joint action leads to what space in the presence of a human      

* They still train a generator to trick the discriminator, but since the observations come from 2 different environment,
they add a pre-discriminator that extract features from the observation. The generator has to make sure that the mutual information
of the label and the output of the pre-discriminator is 0

> Then what's the purpose of the other discriminator? Cause if the pre-discriminator remove the info about the domain... Actually there is 
>two variable, the domain and the class, and the pre-discriminator remove the domain. But both variable have max of mutual information 
>because they are actuallt the same...                      

* As in InfoGAN, they train another classifier to estimate the mutual information (they derive a lower bound and do variational Information maximization), they use gradient flipping, they use TRPO. Need to explain this
3 things

    * How GAIL work: the policy is trained to maximize the reward defined as the discriminator loss
        > Is there any credit assignment problem or difficulty of non-stationarity? The reward is defined for any states even in general. But at the end it's 0.5 for every state so should we stop before? 

* They use 2 hyerparameter: weight of domain confusion and number of look-ahead frames. Explain the influence.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               