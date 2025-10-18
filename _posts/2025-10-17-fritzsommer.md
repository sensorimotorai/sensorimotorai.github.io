---
title: "RL Debates 2: Fritz <em>\"learning for the sake of learning\"</em> Sommer"
layout: single
tags: [active-learning, information-theory, exploration, predicted-information-gain]
categories: [2025, October]
---

In our 2nd [RL Debates]({{ "/debates/" | relative_url }}) presentation, Fritz introduced a first-principles, information-theoretic approach to modeling exploration through the maximization of 'Predicted Information Gain' (PIG).

- Paper: [Learning and exploration in action-perception loops](https://www.frontiersin.org/journals/neural-circuits/articles/10.3389/fncir.2013.00037/full){:target="_blank"}
- Presenter: Fritz Sommer

Fritz framed exploration not as a search for rewards, but as a drive to reduce "missing information" about an agent's world model. He argued that an agent should choose actions that maximize the *predicted information gain* (PIG). This casts the agent in the role of a scientist, actively performing experiments (actions) to learn about its environment as efficiently as possible, a concept closely related to Bayesian experimental design.

Also, fun fact: Fritz's paper talks about world modeling in 2013, way before it was cool. You can hear at [49:01](https://www.youtube.com/watch?v=rlF-0tKOBEk&t=2941s), he's describing an agent that runs an **'internal simulation'** of the world to decide its next action.

Watch the full meeting here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/rlF-0tKOBEk?si=vggdZAsy_9BAwdNT" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
