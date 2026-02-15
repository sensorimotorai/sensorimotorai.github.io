---
title: "RL Debates Finale: Synthesis and the Gap"
layout: single
tags: [RL, synthesis, agency, architecture, debate]
categories: [2026, January]
---

For the final session of the [RL Debate Series]({{ "/debates/" | relative_url }}), we brought all previous contenders back not to declare a winner, but to attempt a synthesis of the different perspectives on agency.

To ensure a productive discussion and avoid cross-talk, the session was explicitly structured around two distinct goals that have motivated this series from the start:

1. **Scientific Understanding:** Explaining biological agency. Is "*reward maximization*" a scientifically accurate and sufficient description of how organisms behave?
2.  **Engineering Utility:** Building artificial agents. Is the RL framework sufficient to build robust, general intelligence, or do we need other computational paradigms?

The discussion began with an exercise where contenders mapped out the "gap" between what biological agents do and what standard RL currently explains. The consensus was clear: everyone agrees there is a gap. The debate is about what fills that gap---whether it's structural inductive biases, intrinsic motivation, homeostatic regulation, or resource constraints.

### Key Highlights & Timestamps

* **[05:15] The Venn diagram exercise:** The session opened with a review of the pre-meeting "homework," establishing that no contender believes standard RL explains 100% of biological behavior or is currently sufficient for all engineering goals.

* **[25:30] Biological constraints vs. infinite compute:** A key debate emerged between the biological perspective and the engineering perspective. Adam Lowet questioned whether biological constraints (like limited working memory, detailed by Anne Collins) are relevant when building AGI with massive compute resources. Anne argued that efficiency and robustness remain critical engineering goals, regardless of compute availability.

* **[35:20] The category error of reward:** Eli Sennesh argued forcibly on the scientific axis, suggesting that framing biological life as "maximizing cumulative reward" is a fundamental category error. He posited that organisms are regulators maintaining homeostasis (or more precisely, *allostasis*: forward-predictive homeostatis), not maximizers chasing arbitrary points.

* **[52:10] Structure vs. scale:** On the engineering axis, Niels Leadholm reiterated his critique of backpropagation and unstructured architectures. The discussion touched on whether the recent success of massive transformers invalidates the need for explicit brain-like structure, or if current methods are hitting a ceiling in data efficiency and generalization.

* **[1:18:00] The "Mars Rover" synthesis:** In the final segment, the group participated in a thought experiment to design a robot that could survive on Mars, taking one crucial component from each theory. This moved the discussion from abstract disagreement to practical architecture.

* **[1:32:00] Connecting compute to survival:** A fascinating synthesis emerged during the exercise connecting Eli's concept of interoception (monitoring battery life as a survival constraint) with Anne's emphasis on resource-aware computation. The group converged on an architecture where the "cost of thinking" is treated as a metabolic expense that directly impacts survival chances, arbitrated by temporal predictions (Tom Ringstrom).

Watch the full finale and the resulting synthesis below:

<iframe width="560" height="315" src="https://www.youtube.com/embed/GKSPT8-yyBk?si=l3K-awJlHVvGXK8E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
