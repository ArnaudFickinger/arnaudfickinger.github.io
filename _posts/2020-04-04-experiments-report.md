---
title: 'Experiments Report'
date: 2020-04-04
permalink: /posts/2020/04/experiments-report/
tags:
  - research
  - experiments
---
$\newcommand{\norm}[1]{\left\lVert#1\right\rVert}$

# April 10, 2020

## Multi-Agent RL with Asymmetric Expertise
As seen on the plot, my current VPG agent don't get anymore signal after just one iteration:

![](/images/vpg.png)

I am adding a random action selection so that the policy does not get stuck directly. With an exploration rate of 
0.5, the loss is not zero anymore but the gradient is also zero in average after one iteration.

![](/images/vpg_exploration_rate.png)

Let's try without exploration rate but with an other optimizer: ADAM instead of SGD. Now the gradient don't vanish but I have
just noticed that I was minimizing instead of maximizing:

![](/images/vpg_adam.png)

Now with the right objective, the reward is continuously increasing: 

![](/images/vpg_adam2.png)

Let's try with more iterations. Since the training is very slow, I train on GPU and I save the logprob during the sample like in the pytorch reinforce [tuto](https://github.com/pytorch/examples/blob/master/reinforcement_learning/reinforce.py) on github.
Actually I got an error (Only Tensors created explicitly by the user (graph leaves) support the deepcopy protocol at the moment) and github don't have ot because they 
update the parameter a the end of each episode. What I can do is to sum the loss at sample time (against replay buffer attitude). The training is still very slow,
maybe because we are sending action to the GPU during each timestep (!). Let's compare to the tuto [openai](https://github.com/openai/spinningup/blob/master/spinup/examples/pytorch/pg_math/1_simple_pg.py):
    * They use one hidden layer of size 32
    * They don't use cuda
I forget about the monitor and I decrease the batch size to 50. It's better but still slow, so I might choose an AWS. We see that the learning is not stable:

I will try with v0 which has a lower max step and a batch of 100, but it's still very slow.
I sill have hope because the implementation in spinningup is actually very quick! Let's find out what happen in my code tomorrow!


# April 11, 2020

## Multi-Agent RL with Asymmetric Expertise
If I remember correctly, if we don;t put any random action the policy get stuck. I will add a video [monitoring](https://github.com/openai/gym/wiki/FAQ#how-do-i-export-the-run-to-a-video-file)
and display the [video](https://about.gitlab.com/handbook/engineering/ux/technical-writing/markdown-guide/#display-local-videos-html5) here.

# April 9, 2020
## Best response to MaxEntIRL for two agents
Firstly we need to think about an environment where the regularizer can easily change the trajectory of $H_2$

## Multi-Agent RL with Asymmetric Expertise
Let's create a easier game to solve, one agent at a time. When the environment robot go through the half part of the player, 
a ball is created. The player has to catch it before the robot go to the other half. The two player can't go to the other half.
Do we assume that they see them? First no then yeah.

Since we want the robot to act, we need to create the game for the 3 players. But first let's see how our algorithm perform 
on a simple task of catching a ball set randomly. Let's say the game stop at a certain time step. And let's try to have
a easy state space, like the (global) position of the player, and the position of the ball (-1,-1) if there is no ball.

Firslty let's test our algorithm on a gym environment. 

## Best response to MaxEntIRL for a single agent
Let's try the sparse regularizer with [CVXPY](https://www.cvxpy.org/examples/machine_learning/lasso_regression.html)

# April 8, 2020

## Multi-Agent RL with Asymmetric Expertise
* Let's think about an environment where we can train H1 and H2 separetely and the robot can help them but without joint training at first. The robot can make 
their task easier, and see which one the robot follow at the end. The problem is how the robot can learn to help and not doing the task, he must have a restricted 
action space that prevent him to get reward but can make reward of one human faster. Also the problem is the credit assignment when the robot is learning and the humans are
already getting reward. The human should also be trained jointly and their reward should depend on robot action. So we should train both human separetely in a 2 players
environment first. Or the robot needs to be in a certain position to enable H1 or H2 to do what they were train to do in a single player mode (put the ground in a different color).
* First I need to train one agent and see what he can do. So let's continue OpenAI tutorial. I have implemented the vanilla PG and will test it tomorrow.

## Cooperation Learning
To implement my ideas, let's build on [garage](https://github.com/rlworkgroup/garage).

# April 7, 2020
## Best response to MaxEntIRL for a single agent
* To gain in productivity, I have made my code more modular. Here is the results discussed on 4/5, firstly for the LP and $\lambda=0$ as a sanity check:
 Objective       | $\Phi A\rho$           
 --- |---
 LP uniform (gives b)   | $[2.41210546 2.41210546 0.11599564]$
 LP start middle    | $[2.07387119 2.07387119 0.3910971 ]$
 QP $\lambda=0$     | $[2.07387037 2.07387037 0.39109759]$      

We see that the solution of the QP without regularizer approximately gives the same as the solution of the LP with a non-uniform start distribution.
We notice that even if the trajectories are symmetric, the rewards are not. This is because the initial $\theta$ is the same but is not necessarily symmetric!

![](/images/san_check.png)

Now let's try with strictly positive value for $\lambda$:

 
Objective       | $\Phi A\rho$           | $\norm{ A\rho - b }_2$  | $\norm{ \Phi(A\rho - b) }_2$  
---       | ---           | ---  | ---
LP       | $[2.41210546 2.41210546 0.11599564]$           | $0$  | $0$  
QP       | $[[2.07387114] [2.07387114] [0.39109711]]$           | $1.4419671500227427$  | $0.551802253219664$  
QP       | $[[2.07387106][2.07387106][0.39109735]]$           | $1.4419657250082745$  | $0.5518024830705811$  
QP       | $[[2.07465583][2.07465583][0.39295618]]$           | $1.4324016870598635$  | $0.5517713795525508$  
QP       | $[[2.07684072][2.07684072][0.39813496]]$           | $1.406848235873857$  | $0.5517313583602333$  

![](/images/sym_env.png)

We see that the occupancy measure are already symmetric even if the trajectory is not. We need to put another constraint on the occupancy measure.
To assess that, let's plot the occupancy measure for each time step with lambda = 1000:

![](/images/occupancy_per_time.png)

Next time let's try on the asymmetric environment, and the initial environment where we saw a difference, for that we need to add 2 column and make the start closer to the left.

Actually let's try with an asymmetric start, it will force the non-regularized QP to have an asymmetric occupancy measure.
We see that the solution is indeed modified but we still don't have the behavior from the paper:

Next time let's try a sparse regularization at each timestep to force the occupancy to choose only one way at a time. 

# April 5, 2020

## Best response to MaxEntIRL for a single agent
* Let's validate yesterday's hypothesis. To do that, let's write my optimization problem:
    
    $$\max_{\rho} r^T\rho - \lambda\norm{ \Phi(A\rho - b) }_2^2$$

    where $\Phi$ is the feature matrix sending $\mathbb{R}^S$ into $\mathbb{R}^K$. Here $S=110$ and $K=3$. So of course 
    regularizing in $\mathbb{R}^S$ and $\mathbb{R}^K$ is not the same. My intuition is that $A\rho$ and $b$ have more chance to
    be closer in term of Euclidian distance in a space of smaller dimension (we can upperbound by the operator norm, 
    can we relate it to the dimension?) thus the regularization would be stronger
    if we don't send $A\rho$ and $b$ into $\mathbb{R}^K$. Recall that for every value of $\lambda$, $b$ is fixed. Here is how I will 
    process: For every value of $\lambda$, I will report $\Phi b$, $\Phi A\rho$, $\Phi(A\rho - b)$, $\norm{ \Phi(A\rho - b) }_2^2$ and 
    $\norm{ A\rho - b }_2^2$ on a table and I will plot $A\rho$. But first let's cut the part of the environment without importance to 
    save computation time. Also I have just noticed that the reward are symmetric in the original paper! I create two environments:
    * A symmetric environment of size (7,5)
    * An asymmetric environment of size (8,5)
    Let's plot the expert trajectory and the expected state-visitation count for the symmetric environment. The first strange thing is 
    that computing $Ax$ does not give me the same thing as computing the SVF from $x$ (occupancy measure):
    
    ![](/images/result_3.png)
    
    Let's inspect $A$ again. Ok nevermind, I just mixed the horizon and the height, here is the corrected plot:
    
    ![](/images/result_4.png)
    
    And $b$ is $[2.41210546 2.41210546 0.11599564]$
    

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

    