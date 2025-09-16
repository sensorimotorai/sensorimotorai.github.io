---
layout: single
title: "RL Debate Series"
permalink: /debates/
---

Why do we have brains? Simple: to survive and reproduce. And neither is possible without ***some action***. Therefore, brains are for generating behavior.

All animals move, even the ones that don't see. This puts action center stage in our quest to understand and build intelligence. But how do we formalize active learning?

The mainstream approach here is **reinforcement learning (RL)**, which posits that agents 'act' to maximize 'rewards'. Consider this canonical figure from the Sutton & Barto textbook:

![Sutton and Barto RL Diagram](/assets/images/sutton-barto.png)

At each time step *t*, the agent produces action *A<sub>t</sub>*, causing the environment's state to evolve from *S<sub>t</sub>* to *S<sub>t+1</sub>*. The environment, in return, provides the agent with a scalar reward *R<sub>t+1</sub>*. This summarizes the standard textbook view of active learning. But this approach faces fundamental challenges, including:

1. Rewards are inferred, not given.  
2. The scalar reward is ill-defined and/or insufficient for complex behaviors.
3. Not all active learning is reinforcement learning.

These issues motivate the need to upgrade---or even replace---RL as our go-to framework for active learning. That's why we're launching the ***RL Debate Series***, where researchers will defend and debate alternative theories of interactive learning and agency.

## The first round: 3 presentations + final debate/synthesis

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
