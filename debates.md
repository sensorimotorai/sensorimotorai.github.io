---
layout: single
title: "RL Debate Series"
permalink: /debates/
---

Why do we have brains? Simple! Brains are for *survival* and *reproduction*. And neither is possible without ***some action***. Therefore, brains are for generating actions (or behavior).

All animals move, even the ones that don't see. This puts action center stage in our quest for intelligence. But how can we formalize active learning?

The mainstream approach here is **reinforcement learning (RL)**, which posits that agents <p>&lsquo;act&rsquo; to maximize &lsquo;rewards&rsquo;</p>. Consider this canonical figure from the Sutton & Barto RL textbook:

![Sutton and Barto RL Diagram](/assets/images/sutton-barto.png)

The agent produces action *A<sub>t</sub>* at time *t*, causing the environment's state to evolve from *S<sub>t</sub>* to *S<sub>t+1</sub>*. The environment, in return, provides the agent with a scalar reward *R<sub>t+1</sub>*. This is the standard textbook approach to model active learning. But there are fundamental challenges with this view. To name a few:

1. Rewards are inferred, not given.  
2. What, exactly, is this scalar reward for complex behaviors in natural environments?  
3. Not all active learning is reinforcement learning. 

Below, we will explore these issues more in depth, motivating the need for an upgrade (or a replacement) of RL as our go-to theoretical framework for active learning. That's why we're launching the **RL Debate Series**, where where researchers defend competing views of how to model interactive learning and agency.

## First round: 3 views + 1 debate

Meet our three contestants, each defending a particular view:

![RL Debate SeriesFlyer](/assets/images/rl_debates_flyer.png)

---

## Appendix: shortcomings of mainstream RL

We will go over some conceptual, practical, and empirical issues that challenge mainstream RL that partially motivated our debate series.

### 1. Rewards must be inferred, they are ultimately subjective

TODO

### 2. RL typically works in toy settings where the reward is known

TODO

### 3. Not all active learning is reinforcement learning: a tale of Tolman's rats

TODO
