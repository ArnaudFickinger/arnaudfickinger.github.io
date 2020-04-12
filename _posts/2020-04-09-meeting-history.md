---
title: 'Meeting History'
date: 2020-04-02
permalink: /posts/2020/04/meeting-history/
tags:
  - reading
  - research
---

# April 11, 2020
* Preparing Meeting with Jakob:
    * Questions about Thesis
        * Abstract
            * To what extent can we have centralized training? If a new agent come, if agents have different expertise, were not train the same way (self-play have problem, how do they solve it?).
            * If using extra state info during training, how to manage the break of information during testing. Don't we also need to meta learn how to go from training to testing? Te optimal amount 
            of information that we would give during training, is there any tradeoff to make?
            * MA credit assignment: Do you build on the technic for temporal credit assignment, can we draw an easy analogy
            * Counterfactual MAPG: how to train the counterfactual baseline?
            * MA common knowledge: can we define norm as common knowledge? do you learn common knowledge during training? Are u not stuck in an equilibria after that? Does purpose of trainng is to learn equilibria?
            * So MAIRL is about learning a static equilibria during training and executing it? Or at least approximate equilibria? 
            * Can we learn the game during execution or the purpose is to find equilibria during training? Can we learn metastrategy?
            * Non stationarity: the agent are modifying the environment while learning (autocuriculum), can we slow down the autocuriculum?
            * Metadata fingerprint: If a policy was random, should we prefer it since it would be more close to the present than a specific policy?
            * Discovering communication: during training, can we think about decentralized way to learn language (maybe the work here Learning to learn to communicate)
            * Is LOLA a metastrategy learner?
            * account for learning of other agent when rewards unknown: in LOLA and BAD we suppose we know?
            * how to account for the agency of humans in the environment
        * Introduction
            * non iid in RL: the dataset in not independant of the decision, the training process is not stationary, the distribution of the datatset change during learning (meta Rl alleviate that?)
            * difference between optimal control and RL: transition and reward unknown
            * Learning with humans: to what extent can we use centralized training? can we have a part of training during the execution? online learning?
            * amazon story: same as manipulation
            * he focus on learning collaboration, communication and reciprocity: can we use a top bottom approach and make them emerge, or another kind of intelligence?
            * MA credit assignment: firslty not sure we did something but also we dont observe action of the other --> coordination problem challenging
            * Why commucation learning is harder than adding actions to the action space? Maybe communication is observable action...
            * Cooperation: how to encourage other agent to cooperate, LOLA tit for tat, can we modify strategy opponent?
            * To what extent can we centralize training if execution is with human?
            * For competition, are agent better when train with central state info, sounds like people not train with it would have an advantage?
            * Learn to go from central state info to no info at execution?
            * How should I test a MA algorithm? (is there a Empirically Evaluating Multiagent Learning Algorithms? for MARL)
            * Credit Assignment problem: how can a human use the credit assignment problem to manipulate the robot --> find the technical failure (fairness problem)
            * COMA: centralized critic detect true optimality, maybe create R1,...,Rn from R
    * Questions about project
        * Why Vickrey not Gibbard
        
     
# April 10, 2020
* Preparing Meeting with Mahendra:
    * Mechanism Design: why it work and can we relate it to IRL/RL?
    * computational complexity of finding optimal voter strategies for voting systems: what is the complex part?
    * litterature on aggregation for AI: sequential DM?


# April 9, 2020
* Meeting with Tom (10-11am):
    * Distinguish normative AI from descriptive AI
    * Look at Natasha Jacques, Gillian Hadfield, Michael Dennis, Pierre Bourdieux
    * In economics model are always criticized and choosing right prior/norms seems is impossible, can we make good norm emerge with MAIRL/MARL?
    * Dichotomy of signalling preferences/following the norm
    * Work on car of Anca Dragan: 
    * In which domains the multiagent IRL is motivated and more useful than simply n times single agent IRL?
    * Norms are collective by nature (coordination or pareto efficiency)--> need to think what make a equilibria nash vs pareto efficient, if one
    is not willing to follow the norm the other are screwed, we think about the other on a pessimistic way --> tit for tat is optimistic, can we learn it?
    what it means in a multi agent case?
    * Utilitarian vs maximin in MARL setting? Fairness
* Meeting with Stuart (1-2pm):
    * Think about Bayesian Games, how to choose an action if we have no model of the transition and reward?
    * Can we talk about equilibrium during the process of learning?
    * We internalize the norm, we agree to be manipulated up to a certain point
    * Look at Dutch action

