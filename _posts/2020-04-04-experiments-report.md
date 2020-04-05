---
title: 'Experiments Report'
date: 2020-04-04
permalink: /posts/2020/04/experiments-report/
tags:
  - research
  - experiments
---

# April 4, 2020

## Best response to MaxEntIRL for a single agent
* Let me recall the objective: I want to get the same trajectory as in [CIRL](https://arxiv.org/pdf/1606.03137.pdf): 
    
    ![](/images/cirl_br.png)
    
* Results: With a weight large enough on the regularizer, I end up with this trajectory and a bad recovered reward:

    ![](/images/result_1.png)

    By comparison, the expert obtains a better reward globally:
    
    ![](/images/result_2.png)

    My hypothesis is that I would have better result without embedding into the feature space during the QP solving. To test it tomorrow, 
    I will print the feature count and the svf and see if the regularized has a better feature count.
    
* Let me recall some thoughts I had before today:
    * Protocol: I recreate the same environment with 3 features and I write a quadratic program to regularize the trajectory
    * Observations: 
        * To get the expected feature count that will be served to regularize my trajectory, I need to solve the LP
    for a finite horizon, otherwise the expected feature count will be too big and not reachable by the solution to my QP, so 
    the trajectory won't be regularized
        * The features are not symmetric on the original environment so the expected feature count has more weight on the first feature.
    * Measurement: To compare the reward recovered by different trajectories, I use the same initialization for the reward weight. I need 
    to be careful to make a copy of the initial reward with *numpy.copy()* at each new call of the MaxEntIRL solver.
    * Results: 
    * Conclusions: I should test with symmetric features

    