---
title: "RL Debates 3: Niels <em>\"you have 1000 brains in your brain\"</em> Leadholm"
layout: single
tags: [active-learning, sensorimotor, thousand-brains, monty]
categories: [2025, October]
---

In our 3rd [RL Debates]({{ "/debates/" | relative_url }}) presentation, Niels from the [Thousand Brains Project](https://thousandbrains.org/){:target="_blank"} shared how their team is reverse-engineering the cortex to build sensorimotor systems that learn and infer like the brain. 

- Paper: [Thousand-Brains Systems: Sensorimotor Intelligence for Rapid, Robust Learning and Inference](https://arxiv.org/abs/2507.04494){:target="_blank"}
- Slides: [Drive link](https://drive.google.com/file/d/124LvxLSBkzkFMB-exDgM5dSCq3k-2uTq/view?usp=sharing){:target="_blank"}
- Presenter: Niels Leadholm

Niels explained the core thesis of the Thousand Brains theory: the neocortex is not a single learning system but is composed of thousands of semi-independent cortical columns, each learning complete models of the world. A key mechanism for this is the use of *reference frames*, which allow each column to understand the structure of objects through active sensing. As an agent interacts with the world, these columns "vote" to reach a consensus on what they are sensing, leading to robust inference.

Niels demonstrated this with their simulated agent, ***"Monty,"*** which learns object models rapidly by actively moving its sensors over them. This approach is highly data-efficient, saving a vast number of parameters and FLOPs compared to data-hungry deep learning methods. As a result, Monty achieves impressive robustness on challenging tasks like **out-of-distribution (OOD) generalization** and **continual learning**, where traditional models often struggle.

Watch the full meeting here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/Q0FFfbYzE1s?si=xXh6Jlc1wTMUq2iM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
