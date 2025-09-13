---
layout: single
title: "RL Debate Series"
permalink: /debates/
---

Why do we have brains? Simple! Brains are for *survival* and *reproduction*. And neither is possible without ***some action***. Therfore, brains are for generating *actions* (or behvaior).

This puts action center stage in our quest for intelligence. But how can we formalize active learning?

The mainstream approach is **reinforcement learning (RL)**, which posits that agents "act" to maximize "rewards". Consider this canonical figure from the Sutton & Barto RL textbook:

![Sutton and Barto RL Diagram](/assets/images/sutton-barto.png)

The agent produces action *A<sub>t</sub>* at time *t*, causing the environment's state to evolve from *S<sub>t</sub>* to *S<sub>t+1</sub>*. The environment, in return, provides the agent with a scalar reward, *R<sub>t+1</sub>*. This is the standard textbook approach to model active learning. But there are fundamental challenges with this view. To name a few:

1. Rewards are inferred, not given.  
2. What, exactly, is this scalar reward for complex, natural environments and tasks?  
3. Not all active learning is reinforcement learning.  

Below, we will explore these issues more in depth, motivating the need for an upgrade (or a replacement) of RL as the main theoretical framework for active learning. We will then discuss our planned RL debate series, and end with introducing our brave contestants and the view they plan to defend.

Here's the punchline, the flyer for our debate series:

(insert...)

And here are more details below, if you're curious, read on.

---

## 1. Rewards must be inferred, they are ultimately subjective

TODO

## 2. RL works only in toy settings where the reward is known

TODO

## 3. Not all active learning is reinforcement learning: a tale of Tolman's rats

TODO 

## The RL debate series

TODO

## Meet our brave contestants 

TODO

## Conclusions, and what to expect next

TODO
