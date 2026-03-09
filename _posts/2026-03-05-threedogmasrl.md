---
title: "Three Dogmas of Reinforcement Learning (David Abel)"
layout: single
tags: [RL, agency, reward-hypothesis, continual-learning, philosophy-of-science, paradigm]
categories: [2026, March]
---

Newton gave force, inertia, and motion precise mathematical definitions. This unlocked centuries of progress in mechanics. Carnot formalized heat engines as ideal reversible cycles. This launched decades of progress in thermodynamics. Turing made "computation" precise. Shannon did it for "information." In each case, the act of giving a field's central concept a rigorous mathematical definition is what turned a loose collection of intuitions into a real science.

Today, "agency" is where "computation" was before Turing: everybody uses the word, but we still lack a precise definition for it. And the field is stuck because of this.

This was David Abel's opening argument when he spoke at our journal club today. Read on for a summary of one of our liveliest sessions yet.

- Paper: [Three Dogmas of Reinforcement Learning](https://arxiv.org/abs/2407.10583){:target="_blank" rel="noopener"}
    - See also: [Settling the Reward Hypothesis](https://proceedings.mlr.press/v202/bowling23a.html){:target="_blank" rel="noopener"}
    - And: [On the Expressivity of Markov Reward](https://openreview.net/forum?id=9DlCh34E1bN){:target="_blank" rel="noopener"}
- Presenter: David Abel (Google DeepMind), with co-author Mark Ho (NYU) joining for discussion

Dave's talk was both conceptually rich and technically precise, reflecting his background in both philosophy and computer science. The discussion was just as lively: **Alison Gopnik**, **Michael DeWeese**, **Mani Hamidi**, **Eli Sennesh**, **Thomas Ringstrom**, **Zachary Laborde**, **Henley Smith**, and others helped turn the session into a wide-ranging conversation about representation, reward (and its origins), development, empowerment, adaptation, and the nature of agency. I (**Hadi**, the organizer) also participated, mostly on adaptation and the statistics of the environment. **Mark Ho**, Dave's co-author, emphasized the anti-behaviorist implications of the first dogma.

## Table of Contents

- [Background: paradigms and why they matter](#background-paradigms-and-why-they-matter)
- [Dogma 1: The Environment Spotlight](#dogma-1-the-environment-spotlight)
- [Dogma 2: Learning as finding a solution](#dogma-2-learning-as-finding-a-solution)
- [Interlude: The adaptation thread](#interlude-the-adaptation-thread)
- [Dogma 3: The Reward Hypothesis](#dogma-3-the-reward-hypothesis)
- [Wrapping up: the pragmatist counterpoint](#wrapping-up-the-pragmatist-counterpoint)
- [Where rewards come from, and where this is all heading](#where-rewards-come-from-and-where-this-is-all-heading)
- [Broader implications: why this work matters](#broader-implications-why-this-work-matters)

---

## Background: paradigms and why they matter

Dave opened with a philosophical framing. Drawing on Popper, Kuhn, and the Duhem-Quine thesis, he argued that the *paradigm* we work within shapes not just what answers we find, but what questions we're *capable of asking*. He illustrated this with the anecdote of Cremonini refusing to look through Galileo's telescope, arguing the instrument itself must be introducing artifacts. The preconception of what counted as evidence was already shaping the conclusion before anyone looked.

The core question: has reinforcement learning finalized its paradigm? Or are there assumptions baked into the standard framework---assumptions so familiar they've become invisible---that are limiting what we can conceive of?

Dave and his co-authors Mark Ho and Anna Harutyunyan identified three such assumptions, which they call *dogmas* (an homage to Quine's "Two Dogmas of Empiricism"). The paper argues that these dogmas constrain the kinds of theories and definitions RL can develop about agents, intelligence, and learning.

## Dogma 1: The Environment Spotlight

The first dogma is our tendency to model environments explicitly while leaving agents as an afterthought. We do have a "standard model" of the environment---the MDP, with its five-tuple, its Bellman equations, its rich taxonomy of variants (POMDPs, bandits, contextual bandits). But what about the agent? What's the standard model of an *agent*?

Dave claims there isn't one. We talk about agents constantly, but we haven't done the careful conceptual analysis and formal modeling of agents that we've done for environments. He quoted Michael Tomasello:

> *"Agency is the organizational framework within which both behavioral and mental processes operate."*
> --- The evolution of agency: Behavioral organization from lizards to humans [(Tomasello, 2022)](https://mitpress.mit.edu/9780262047005/the-evolution-of-agency/){:target="_blank" rel="noopener"}

And Quine:

> *"The less a science has advanced, the more its terminology tends to rest on an uncritical assumption of mutual understanding."*
> --- Truth by Convention [(Quine, 1936)](https://www.hist-analytic.com/QuineTruthbyConvention.pdf){:target="_blank" rel="noopener"}

This prompted a rich exchange. **Zachary Laborde** asked whether this connects to the enactivist program. Dave said the proposal is broader, and there are many ways to re-center the agent, but that what's missing is the *formal apparatus* to do so.

**Alison Gopnik** chimed in here, stating that the enactivist program has historically been anti-representational, which is a liability. You could have an agent-centric program *with* representations, and that might be the best of both worlds.

**Mark Ho** reinforced this point, noting that MDPs give us a general space to reason about trade-offs across environments. Can we build an analogous space for agents?

Dave then showed a backup slide on **bounded agents**: a finite-state-machine formalization where the agent has a finite internal state space (capturing something like a memory or capacity constraint), a state-update function, and a policy that maps internal states to actions.

I noted this connects directly to Anne Collins' work that she presented as part of the [RL Debate Series]({{ "/debates/" | relative_url }}){:target="_blank" rel="noopener"}, which showed that human deviations from RL predictions arise from finite working memory (see [RL Debates 5: Anne <em>"not everything is RL"</em> Collins]({% post_url 2025-11-13-annecollins %}){:target="_blank" rel="noopener"}).

**Alison** pushed further: representation is exactly what lets you compress an arbitrarily long history into a manageable state space. A theory, a causal graph, a world model. These are all mechanisms for doing that compression. She also advocated for developmental and comparative approaches to studying agency, arguing that adult human introspection is probably not the best window into what agency fundamentally *is*.

## Dogma 2: Learning as finding a solution

The second dogma targets our habit of treating learning as a finite search that terminates when a "solution" is found. Dave pointed to the standard RL benchmarks---Breakout, Mountain Car, Montezuma's Revenge---as paradigmatic of this view: there's a task, there's a solution, and learning is the process of finding it.

The alternative: learning as *adaptation*, as playing an *infinite game*. Dave cited James Carse's distinction: a finite game is played for the purpose of winning; an infinite game, for the purpose of continuing the play.

He noted that even Sutton and Barto gesture toward this view. In an early draft, they wrote that the point of maximizing reward is not that the quantity is ever maximized, but that the agent is always *trying* to increase it. **Henley Smith** pointed out that this quote appears in the 2015 draft but was removed from the published 2018 edition. Dave found this fascinating and somewhat puzzling.

## Interlude: The adaptation thread

This is where one of the session's most interesting threads developed [*full disclosure: I asked this question!*]. I asked Dave to define adaptation, alluding to the talk's own argument that precise definitions are what unlock real progress.

It turns out this was Dave's next slide. He offered four candidate views of learning/adaptation:

1. **mechanistic** (the presence of a special learning mechanism, like gradient computation),
2. **behaviorist** (meaningful behavior change due to experience),
3. **uncertainty/knowledge** (reduction of uncertainty or acquisition of knowledge over time),
4. **performance-based** (improvement on a task, the classic Mitchell definition).

I then proposed a specific notion of adaptation rooted in theoretical neuroscience: adapting to the *statistics of the environment* across timescales. I gave the example of the visual cortex containing more neurons selective for cardinal orientations (vertical, horizontal) than oblique ones, mirroring the statistical prevalence of these orientations in natural scenes. This kind of adaptation spans evolutionary (e.g., development) to moment-to-moment timescales (e.g., gain modulation), and if you formalize this, it starts to look like a cross-entropy or generative modeling objective.

**Eli Sennesh** pushed back on the evolutionary timescale version, calling it tautological: "Fish aren't found out of water because they'd be dead." But my point was about the *representational imprint*: the structure of the organism's internal model reflecting the statistics of its environment. Dave categorized this as the mechanistic view, since the claim is about internal representations rather than behavior per se. He also teased that his upcoming talk on **plasticity and empowerment** (in two weeks) would formalize adaptation in terms of *influence*: can the data the organism receives influence either the content of the agent's mind or its behavior?

**Alison** added another dimension: the inverse-problem view from vision science and philosophy of science. The environment has structure; the agent receives samples generated by that structure; the problem is recovering the structure from the samples. She noted this doesn't reduce to uncertainty. Paradigm shifts, for instance, aren't about updating probabilities but about restructuring the framework itself. And this isn't just about fancy scientific learning: 3- and 4-year-olds go through something like paradigm shifts too.

## Dogma 3: The Reward Hypothesis

The final and most technical segment tackled the Reward Hypothesis directly: Sutton's claim that all goals and purposes can be well thought of as maximization of expected cumulative scalar reward.

Dave summarized the [Settling the Reward Hypothesis](https://proceedings.mlr.press/v202/bowling23a.html){:target="_blank" rel="noopener"} paper (led by Michael Bowling and John Martin), which translates this natural-language statement into a formal conjecture and identifies the exact conditions under which it's true. The framework uses "**seven doors**": **two interpretive choices** that turn the hypothesis into a conjecture, and **five axioms** that determine when the conjecture holds.

We start from a verbatim statement of *The Reward Hypothesis*:

> *"All of what we mean by goals and purposes can be well thought of as maximization of the expected value of the cumulative sum of a received scalar signal (reward)."*
> --- [Sutton (2004)](http://incompleteideas.net/rlai.cs.ualberta.ca/RLAI/rewardhypothesis.html){:target="_blank" rel="noopener"}

### The first interpretive door:

Here, **"goals and purposes"** is interpreted in terms of **preference relations** over outcomes (distributions over histories of experience). I asked whether this is consensus or proposal. Dave said it's not consensus. Philosopher Ruth Chang has argued against it on grounds of incommensurability. But preferences are general enough that he finds them hard to reject as at least a starting point.

This sparked a rich exchange. **Mani Hamidi** also brought up Chang's incommensurability argument and we discussed it further. **Alison Gopnik** connected it to Isaiah Berlin's picture of tragic value pluralism (illustrated by Bernard Williams's Gauguin example: you can't put your obligation to your family and your artistic drive on a single preference scale).

**Thomas Ringstrom** offered the empowerment perspective: preferences might be *secondary* to empowerment, which can *induce* a preference relation. In this view, there has to be a *reason* for preferences, and empowerment provides it. Dave found this thread fascinating and noted that in earlier work, he and his co-authors had struggled with the order in which objects are introduced---does the environment come first, then preferences, then rewards? Or do preferences come first?

### The second interpretive door

The phrase **"well thought of"** means preferences can be *conveyed* through rewards, in the sense that the ordering on policies induced by reward-based value matches the ordering induced by preferences over outcomes, eventually (after some finite point in time).

### The five formal axioms

These are essentially the familiar **[von Neumann-Morgenstern axioms](https://en.wikipedia.org/wiki/Von_Neumann%E2%80%93Morgenstern_utility_theorem){:target="_blank" rel="noopener"}**: completeness, transitivity, independence, and continuity, plus a fifth condition [Bowling et al., (2023)](https://proceedings.mlr.press/v202/bowling23a.html){:target="_blank" rel="noopener"} called **temporal gamma-indifference**, which says discounting must remain consistent through time for Markov rewards.

Here's the main result: a preference relation can be captured by a Markov reward-discount pair **if and only if** it satisfies these five axioms.

That bidirectional **if and only if** is the key point. Writing down a reward function is not a neutral modeling move. It implicitly commits you to all five axioms. If even one fails, then no scalar reward function can fully capture the underlying preferences.

As Dave noted, humans seem to violate many of these axioms in practice. **Mani** asked how this relates to *distributional RL* and risk-sensitive methods like *Conditional Value at Risk* (CVaR). Dave's answer was that risk sensitivity breaks the independence axiom, and that once you relax individual axioms, you open the door to a much broader space of decision theories, including partial orders, lexicographic orders, and multi-criteria RL.

## Wrapping up: the pragmatist counterpoint

**Michael DeWeese** offered a spirited pragmatist defense of reward. He argued that brains have a common currency (roughly, dopamine), and this currency works across wildly different domains, such as walking on the beach, eating an apple. Apparent violations of the axioms might be explained by proxies and normalizations our bounded brains use, not fundamental failures of the reward framework. Dave agreed that understanding the *implicit commitments* of the reward view is valuable regardless of whether you ultimately embrace it. On that, Mike and Dave found common ground.

## Where rewards come from, and where this is all heading

**Mani** asked what might be the deepest question of the session: what is the relationship between the *reward hypothesis* (can preferences be captured by rewards?) and the question of *where rewards come from*? Dave answered that they can be addressed independently, but they bear on each other. The reward hypothesis, as formalized, kicks the can to preferences and asks whether preferences can be expressed as rewards. Where those preferences come from is a separate question. But, if you buy the five axioms, you can at least ask: how does the mechanism producing rewards come to satisfy them?

**Eli Sennesh** proposed a different framing of learning altogether: learning as the extension of dynamical timescales of control. Using the mountain car example, he argued that the actual challenge isn't specifying the cost function (just minimize distance to the flag) but discovering that the system can be controlled on a *longer timescale* by accepting short-term costs. Dave tentatively categorized this as a behavioral view of learning and noted its resonance with Tom Ringstrom's framework.

I closed by asking Dave about the connection between the reward hypothesis and alternative information-theoretic frameworks like empowerment, divergence minimization, and free energy. Dave responded by connecting objectives to optimization: reward takes on meaning only once it enters an optimization process, and any scalar signal can be accumulated and optimized. Multi-objective RL, where you have multiple "channels" of reward (the "RGB channels of reward," as Dave put it), might be where the different perspectives unify. That is, once you start relaxing the axioms that enforce collapsing everything to a single expected scalar.

## Broader implications: why this work matters

Here is why I think this line of work is interesting and important.

Fields mature when their central concepts become precise enough to analyze systematically. Newton did this for motion, Turing for computation, and Shannon for information. Formalization does not solve everything, but it changes the game. It turns vague intuitions into mathematical objects you can compare, test, refute, and build on.

That is what makes Three Dogmas valuable. It does not offer a new benchmark result or a better algorithm. It asks whether some of RL's most familiar concepts, like agent, learning, and reward, are actually as clear and well grounded as we pretend they are. In that sense, the paper is doing real foundational work: surfacing hidden assumptions and showing how they shape what the field can easily think about.

At the same time, I do not think the project is complete. For me, the thinnest point, both in the paper and in today's discussion, was **adaptation**. The critique of "learning as finding a solution" is compelling, but the alternative still needs much more development. Adaptation to what, exactly? Over what timescales? In behavior, internal representations, or both? If adaptation is going to play a central role, it needs a comprehensive and more formal treatment.

This sets up the next discussions nicely. **Mani Hamidi** presents next week (**March 12**) with an *evolutionary response* to these very dogmas, and **Dave** returns on **March 19** to present *plasticity as the mirror of empowerment*, which may be where the adaptation question gets a more thorough treatment it deserves.

Can't wait!

---

Watch the full meeting here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/P8nm8fR9gK8?si=gZfEnxuP6IG_Fh4w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
