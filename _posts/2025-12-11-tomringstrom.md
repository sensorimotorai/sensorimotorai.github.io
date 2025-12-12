---
title: "RL Debates 6: Thomas <em>\"no reward for you\"</em> Ringstrom"
layout: single
tags: [empowerment, compositionality, option-kernels, intrinsic-motivation]
categories: [2025, December]
---

In our 6th and final [RL Debates]({{ "/debates/" | relative_url }}) presentation, Tom introduced a rigorous framework for compositional planning that replaces the standard scalar reward with predictive "option kernels" and intrinsic empowerment.

- Paper: [A Unified Theory of Compositionality, Modularity, and Interpretability in MDPs](https://arxiv.org/abs/2506.09499){:target="_blank"}
- Slides: [Drive link](https://drive.google.com/file/d/1H_cZFGEVdOQT1Ypl-sdfwefdffvv/view?usp=sharing){:target="_blank"}
- Presenter: Tom Ringstrom

We began with Tom describing his observation of flexible animal intelligence to realizing that standard RL principles are insufficient for high-dimensional planning [00:01:44]. He used the famous example of **[Stoffel the honey badger](https://www.youtube.com/watch?v=c36UNSoJenI){:target="_blank"}** to illustrate the need for agents that can reason about complex, sequential goals (like escaping an enclosure) without needing explicit external rewards for every step [00:09:35].

Tom argued that standard value functions act merely as "scorecards," compressing rich spatiotemporal information into a single number and failing to factorize in high dimensions [00:15:38]. He proposed a new formalism based on **Option Kernel Bellman Equations (OKBEs)**, which learn **State-Time Option Kernels (STOKs)**, defined as predictive representations of *when* and *where* an agent will end up [00:23:47]. Unlike Successor Representations, STOKs are sequentially compositional, allowing agents to chain skills together to solve complex tasks [00:38:24]. He further showed how this framework enables **Empowerment** (a measure of controllability) to be computed in high dimensions, serving as the primary driver for **goal selection** [01:01:31]. In this view, **"valence"** is formally defined as **relative empowerment**---the specific gain or loss in future control that a state affords the agent.

The meeting concluded with a discussion on how this framework compares to existing approaches like Linearly Solvable MDPs and Goal-Conditioned RL [01:17:46]. Tom clarified that while related, his approach offers distinct advantages in temporal prediction and compositional generalization. He illustrated the theory's explanatory power with the example of losing a passport: under this framework, the resulting "panic" is not a negative reward signal, but a **sudden, catastrophic drop in empowerment** [01:33:11]. The agent effectively panics because its horizon of possible futures---traveling, attending events, returning home---has instantaneously collapsed.

Watch the full meeting here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/a5nh6lr7ikg?si=FmjwKjQOM49nieHQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
