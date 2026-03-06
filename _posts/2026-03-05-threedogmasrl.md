---
title: "Three Dogmas of Reinforcement Learning (David Abel)"
layout: single
tags: [RL, agency, reward-hypothesis, continual-learning, philosophy-of-science, paradigm]
categories: [2026, March]
---

Newton gave "force, inertia, and motion" precise mathematical definitions: this unlocked centuries of progress in mechanics. Carnot formalized "heat engines" as ideal reversible cycles: this launched decades of progress in thermodynamics. Turing made "computation" precise. Shannon did it for "information." In each case, the act of giving a field's central concept a rigorous mathematical definition is what turned a loose collection of intuitions into a real science.

Today, "agency" is where "computation" was before Turing: everybody uses the word, nobody can define it precisely, and the field is stuck because of it.

This was David Abel's opening argument when he spoke at our journal club today. Read on for a summary of one of our liveliest sessions yet.

- Paper: [Three Dogmas of Reinforcement Learning](https://arxiv.org/abs/2407.10583){:target="_blank"}
- See also: [Settling the Reward Hypothesis](https://proceedings.mlr.press/v202/bowling23a.html){:target="_blank"}, [On the Expressivity of Markov Reward](https://openreview.net/forum?id=9DlCh34E1bN){:target="_blank"}
- Presenter: David Abel (Google DeepMind), with co-author Mark Ho (NYU) joining for discussion
- Slides: slides TODO

Dave's background in both philosophy and computer science made for a presentation that was as conceptually rich as it was technically precise, and the audience showed up with matching energy. We had contributions from **Alison Gopnik** (on representation, paradigm change, multi-agent coordination, and the developmental perspective), **Michael DeWeese** (defending a pragmatist account of agents and reward), **Eli Sennesh** (proposing learning as extension of dynamical timescales of control), **Mani Hamidi** (on incommensurability, risk sensitivity, and the origin of rewards---a preview of his talk next week!), **Thomas Ringstrom** (arguing empowerment is primary, preferences secondary), **Zachary Laborde** (on the relationship to enactivism), **Henley Smith** (on representation and a sharp bibliographic correction), and me, **Hadi** (on adaptation, statistics of the environment, and connecting all these frameworks). **Mark Ho**, Dave's co-author, also chimed in to sharpen the anti-behaviorist thrust of the first dogma.

## Table of Contents

- [Background: paradigms and why they matter](#background-paradigms-and-why-they-matter)
- [Dogma 1: The Environment Spotlight](#dogma-1-the-environment-spotlight)
- [Dogma 2: Learning as finding a solution](#dogma-2-learning-as-finding-a-solution)
- [The adaptation thread](#the-adaptation-thread)
- [Dogma 3: The Reward Hypothesis](#dogma-3-the-reward-hypothesis)
- [Wrapping up: the pragmatist counterpoint](#wrapping-up-the-pragmatist-counterpoint)
- [Where rewards come from, and where this is all heading](#where-rewards-come-from-and-where-this-is-all-heading)
- [Broader implications: why this work matters](#broader-implications-why-this-work-matters)

---

## Background: paradigms and why they matter

Dave opened with a philosophical framing. Drawing on Popper, Kuhn, and the Duhem-Quine thesis, he argued that the *paradigm* we work within shapes not just what answers we find, but what questions we're *capable of asking*. He illustrated this with the anecdote of Cremonini refusing to look through Galileo's telescope, arguing the instrument itself must be introducing artifacts. The preconception about what counts as evidence was already doing the work before any observation took place.

The core question: has reinforcement learning finalized its paradigm? Or are there assumptions baked into the standard framework---assumptions so familiar they've become invisible---that are limiting what we can conceive of?

Dave and his co-authors Mark Ho and Anna Harutyunyan identified three such assumptions, which they call *dogmas* (an homage to Quine's "Two Dogmas of Empiricism"). The paper argues these dogmas are constraining the surface area that RL's theory and definitions can have with the grand phenomena of agents, intelligence, and learning.

## Dogma 1: The Environment Spotlight

The first dogma is our tendency to model environments explicitly while leaving agents as an afterthought. We do have a "standard model" of the environment---the MDP, with its five-tuple, its Bellman equations, its rich taxonomy of variants (POMDPs, bandits, contextual bandits). But what about the agent? What's the standard model of an *agent*?

Dave's claim: there isn't one. We talk about agents constantly, but we haven't done the careful conceptual analysis and formal modeling of agents that we've done for environments. He quoted Michael Tomasello: agency is the organizational framework within which both behavioral and mental processes operate. And Quine: the less a science is advanced, the more its terminology rests on an uncritical assumption of mutual understanding.

This prompted a rich exchange. **Zachary Laborde** asked whether this connects to the enactivist program. Dave said the proposal is broader, and there are many ways to re-center the agent, but that what's missing is the *formal apparatus* to do so. **Alison Gopnik** chimed in here, stating that the enactivist program has historically been anti-representational, which is a liability. You could have an agent-centric program *with* representations, and that might be the best of both worlds. **Mark Ho** reinforced this point, noting that MDPs give us a general space to reason about trade-offs across environments. Can we build an analogous space for agents?

Dave then showed a backup slide on **bounded agents**: a finite-state-machine formalization where the agent has a finite internal state space (capturing something like a memory or capacity constraint), a state-update function, and a policy that maps internal states to actions. **Hadi** noted this connects directly to Anne Collins' work that she presented as part of the [RL Debates]({{ "/debates/" | relative_url }}), which showed that human deviations from RL predictions arise from finite working memory (see [RL Debates 5: Anne <em>"not everything is RL"</em> Collins]({% post_url 2025-11-13-annecollins %}){:target="_blank"}).

**Alison** pushed further: representation is exactly what lets you compress an arbitrarily long history into a manageable state space. A theory, a causal graph, a world model. These are all mechanisms for doing that compression. She also advocated for developmental and comparative approaches to studying agency, arguing that adult human introspection is probably not the best window into what agency fundamentally *is*.

## Dogma 2: Learning as finding a solution

The second dogma targets our habit of treating learning as a finite search that terminates when a "solution" is found. Dave pointed to the standard RL benchmarks---Breakout, Mountain Car, Montezuma's Revenge---as paradigmatic of this view: there's a task, there's a solution, and learning is the process of finding it.

The alternative: learning as *adaptation*, as playing an *infinite game*. Dave cited James Carse's distinction: a finite game is played for the purpose of winning; an infinite game, for the purpose of continuing the play.

He noted that even Sutton and Barto gesture toward this view. In an early draft, they wrote that the point of maximizing reward is not that the quantity is ever maximized, but that the agent is always *trying* to increase it. **Henley Smith** pointed out that this quote appears in the 2015 draft but was removed from the published 2018 edition. Dave found this fascinating and somewhat puzzling.

## The adaptation thread

This is where one of the session's most interesting threads developed [*editorial note: of course I feel this way, because I asked this question haha!*]. **Hadi** asked Dave to *define* adaptation, noting that definitions are famously difficult here but that they matter enormously.

It turns out this was Dave's next slide. He offered four candidate views of learning/adaptation: (1) **mechanistic** (the presence of a special learning mechanism, like gradient computation), (2) **behaviorist** (meaningful behavior change due to experience), (3) **uncertainty/knowledge** (reduction of uncertainty or acquisition of knowledge over time), and (4) **performance-based** (improvement on a task, the classic Mitchell definition).

**Hadi** then proposed a specific notion of adaptation rooted in theoretical neuroscience: adapting to the *statistics of the environment* across timescales. He gave the example of the visual cortex containing more neurons selective for cardinal orientations (vertical, horizontal) than oblique ones, mirroring the statistical prevalence of these orientations in natural scenes. This kind of adaptation spans evolutionary to moment-to-moment timescales (e.g., gain modulation), and if you formalize it, it starts to look like a cross-entropy or generative modeling objective.

**Eli Sennesh** pushed back on the evolutionary timescale version, calling it tautological: "Fish aren't found out of water because they'd be dead." But Hadi's point was about the *representational imprint*---the structure of the organism's internal model reflecting the statistics of its environment. Dave categorized this as the mechanistic view, since the claim is about internal representations rather than behavior per se. He also teased that his upcoming talk on **plasticity and empowerment** (in two weeks) would formalize adaptation in terms of *influence*: can the data the organism receives influence either the content of the agent's mind or its behavior?

**Alison Gopnik** added another dimension: the inverse-problem view from vision science and philosophy of science. The environment has structure; the agent receives samples generated by that structure; the problem is recovering the structure from the samples. She noted this doesn't reduce to uncertainty---paradigm shifts, for instance, aren't about updating probabilities but about restructuring the framework itself. And this isn't just about fancy scientific learning: 3- and 4-year-olds go through something like paradigm shifts too.

## Dogma 3: The Reward Hypothesis

The final and most technical segment tackled the Reward Hypothesis directly: Sutton's claim that all goals and purposes can be well thought of as maximization of expected cumulative scalar reward.

Dave summarized the [Settling the Reward Hypothesis](https://proceedings.mlr.press/v202/bowling23a.html){:target="_blank"} paper (led by Michael Bowling and John Martin), which translates this natural-language statement into a formal conjecture and identifies the exact conditions under which it's true. The framework uses "seven doors": two interpretive choices that turn the hypothesis into a conjecture, and five axioms that determine when the conjecture holds.

The reward hypothesis states:

> *"All of what we mean by goals and purposes can be well thought of as maximization of the expected value of the cumulative sum of a received scalar signal (reward)."* --- Sutton (2004)

The first interpretive door: **"goals and purposes"** are understood as **preference relations** over outcomes (distributions over histories of experience). **Hadi** asked whether this is consensus or proposal. Dave said it's not consensus. Philosopher Ruth Chang has argued against it on grounds of incommensurability. But preferences are general enough that he finds them hard to reject as at least a starting point.

This sparked a wonderful exchange. **Mani Hamidi** brought up Chang's incommensurability argument. **Alison Gopnik** connected it to Isaiah Berlin's picture of tragic value pluralism (illustrated by Bernard Williams's Gauguin example: you can't put your obligation to your family and your artistic drive on a single preference scale). **Thomas Ringstrom** offered the empowerment perspective: preferences might be *secondary* to empowerment, which can *induce* a preference relation. In this view, there has to be a *reason* for preferences, and empowerment provides it. Dave found this thread fascinating and noted that in earlier work, he and his co-authors had struggled with the order in which objects are introduced---does the environment come first, then preferences, then rewards? Or do preferences come first?

The second interpretive door: **"well thought of"** means preferences can be *conveyed* through rewards, in the sense that the ordering on policies induced by reward-based value matches the ordering induced by preferences over outcomes, eventually (after some finite point in time).

The five formal axioms are essentially the **von Neumann-Morgenstern axioms** (completeness, transitivity, independence, continuity) plus a new fifth axiom called **temporal gamma-indifference** (discounting is consistent through time, needed specifically for Markov rewards). The main result: a preference relation satisfies these five axioms *if and only if* there exists a Markov reward-discount pair that captures it.

The "if and only if" is the key: writing down a reward function *implicitly commits you* to all five axioms. Violating any axiom means no reward function can capture your preferences. And as Dave noted, there's ample evidence that humans regularly violate basically all of these axioms. **Mani** asked how this squares with *distributional RL* and risk-sensitive methods like *Conditional Value at Risk* (CVaR). Dave explained that risk sensitivity violates the independence axiom, and that dropping individual axioms opens up a rich landscape of alternative decision-making theories (partial orders, lexicographic orders, multi-criteria RL).

## Wrapping up: the pragmatist counterpoint

**Michael DeWeese** offered a spirited pragmatist defense of reward. He argued that brains have a common currency (roughly, dopamine), and this currency works across wildly different domains, such as walking on the beach, eating an apple. Apparent violations of the axioms might be explained by proxies and normalizations our bounded brains use, not fundamental failures of the reward framework. Dave agreed that understanding the *implicit commitments* of the reward view is valuable regardless of whether you ultimately embrace it. On that, Mike and Dave found common ground.

## Where rewards come from, and where this is all heading

**Mani** asked what might be the deepest question of the session: what is the relationship between the *reward hypothesis* (can preferences be captured by rewards?) and the question of *where rewards come from*? Dave answered that they can be addressed independently, but they bear on each other. The reward hypothesis, as formalized, kicks the can to preferences and asks whether preferences can be expressed as rewards. Where those preferences come from is a separate question. But, if you buy the five axioms, you can at least ask: how does the mechanism producing rewards come to satisfy them?

**Eli Sennesh** proposed a different framing of learning altogether: learning as the extension of dynamical timescales of control. Using the mountain car example, he argued that the actual challenge isn't specifying the cost function (just minimize distance to the flag) but discovering that the system can be controlled on a *longer timescale* by accepting short-term costs. Dave tentatively categorized this as a behavioral view of learning and noted its resonance with Tom Ringstrom's framework.

**Hadi** closed by asking Dave about the connection between the reward hypothesis and alternative information-theoretic frameworks like empowerment, divergence minimization, and free energy. Dave's response was characteristically careful: reward takes on meaning only once it enters an optimization process, and any scalar signal can be accumulated and optimized. Multi-objective RL, where you have multiple "channels" of reward (the "RGB channels of reward," as Dave put it), might be where the different perspectives unify. That is, once you start relaxing the axioms that enforce collapsing everything to a single expected scalar.

## Broader implications: why this work matters

Here's why I think Dave's line of work is not just interesting but *essential*.

Every mature science has gone through a moment where someone took a vague, pre-theoretic concept and gave it mathematical teeth. Newton did it for motion. Carnot did it for heat engines. Turing did it for computation. Shannon did it for information. In each case, the formalization not only clarified the concept, but once could say, it even *created the science*. Before the definition, there were clever people with good intuitions. After the definition, there was a field with theorems, predictions, and systematic progress.

We are trying to build a science of intelligence. We talk constantly about "agents", "learning", "adaptation", "goals", "rewards". But as Dave showed today, we lack the kind of first-principles clarity about these terms that Newton had about force, or Shannon had about information. The Three Dogmas paper point out this gap, and also makes progress toward closing it, by surfacing the hidden assumptions in our paradigm and showing exactly where they constrain what we can conceive.

This kind of foundational, conceptual work is undervalued in a field obsessed with benchmarks and scaling laws. It's much harder to publish a paper that says "here's a better way to *think*" than one that says "here's a better number on a benchmark." But historically, the conceptual advances are the ones that last. I believe the Three Dogmas is that kind of work, and I'm glad Dave and his collaborators are pursuing it with such rigor and care.

And this is just the beginning! See the [schedule page]({{ "/schedule/" | relative_url }}) for what's coming next: **Mani Hamidi** presents *next week* (March 12) with an evolutionary response to these very dogmas, and **Dave returns on March 19** to present *Plasticity as the Mirror of Empowerment*, which promises to formalize adaptation and show that plasticity and empowerment are in fundamental tension.

Can't wait!

---

Watch the full meeting here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID_HERE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
