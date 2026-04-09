---
title: "Intrinsic Goals for Autonomous Agents (Reece Keller)"
layout: single
tags: [NeuroAI, intrinsic-motivation, exploration, world-models, zebrafish, curiosity, empowerment, reinforcement-learning, self-supervised]
categories: [2026, April]
---

Why do we do things? Standard RL says to maximize rewards, generously handed to us by the environment. But if you watch a baby crawling around a room, touching everything, putting things in its mouth, wandering with no instruction and no reward, you realize how shallow that answer is.

The baby has no task. No one is supervising it. And yet its behavior is structured, purposeful, and unmistakably intelligent.

How do you write down an objective function for *that*?

This was the opening question when Reece Keller (Carnegie Mellon University) joined us for the first session in our April world-modeling series. Reece presented his recent work on model-based intrinsic motivation, using a virtual zebrafish to show that a single self-supervised objective---trained on *zero* neural data---can simultaneously capture the animal's behavior *and* predict its whole-brain dynamics.

- Paper: [Intrinsic Goals for Autonomous Agents](https://openreview.net/forum?id=g2vViuEVDS){:target="_blank" rel="noopener"}
- Presenter: Reece Keller (Carnegie Mellon University)

The discussion was wide-ranging and interactive, with questions woven throughout the presentation. **Eli Sennesh** pushed on the state-oriented nature of existing intrinsic motivations and the relationship to information gain. **Michael DeWeese** asked about proprioceptive fidelity in the head-fixed preparation. **Giacomo Aldegheri** probed the alternatives to the niche-seeking model and the relationship between behavioral and neural alignment. **Keir Havel** asked about state entropy versus policy entropy. **Mani Hamidi** connected the work to Tomasello's evolutionary stages of agency. **Alec Segal** asked about empowerment. I (**Hadi**, the organizer) pressed on the normative philosophy behind the approach, the tension between principled and practical methods, and the relationship to empowerment as a diagnostic tool.

## Table of Contents

- [NeuroAI done right](#neuroai-done-right)
- [The autonomy spectrum](#the-autonomy-spectrum)
- [Why heuristic exploration fails](#why-heuristic-exploration-fails)
- [Three flavors of model-based intrinsic motivation](#three-flavors-of-model-based-intrinsic-motivation)
- [Zebrafish as a model system](#zebrafish-as-a-model-system)
- [3M Progress: a compass for exploration](#3m-progress-a-compass-for-exploration)
- [Results: behavior and brain alignment](#results-behavior-and-brain-alignment)
- [Discussion: empowerment, active inference, and the road ahead](#discussion-empowerment-active-inference-and-the-road-ahead)

---

## NeuroAI done right

Before Reece started his slides, I wanted to flag something about the *philosophy* behind this work, because it stands apart from the dominant mode in NeuroAI today.

Most NeuroAI papers take the following approach: fit a model to neural data, report a predictive score, publish. There is nothing wrong with that---data-driven models are essential for discovering phenomena. But they are descriptive, not explanatory. You learn *that* a model predicts neural activity, not *why* the brain would compute things that way.

Reece's approach is normative. It starts from a principle (the agent generates its own intrinsic drive), derives an objective function, trains a model with *no neural data at all*, and then asks: does this unsupervised agent's internal activity match what we see in the real brain? The fact that it does---for both behavior and neural dynamics---is the payoff. And because the model was never trained on neural data, any correspondence tells you something about the computational logic of the circuit, not just about the statistical structure of the recording.

This connects to a framework Reece's advisor Aran Nayebi and colleagues have proposed: a **NeuroAI Turing test** [[00:13:17]](https://youtu.be/VIDEO_ID?t=797){:target="_blank" rel="noopener"}. The original Turing test asks whether a machine can produce behavior indistinguishable from a human. The embodied Turing test extends this to continuous sensorimotor behavior (can a robot walk like a human?). The NeuroAI Turing test goes further: not only must the model match behavior, but its internal mechanisms must be sufficient and necessary to predict brain data. Behavioral mimicry is not enough. There has to be representational convergence.

I think this is the right standard. Fitting models to neural data is a means, not an end. The end is understanding *why* neural circuits compute what they compute, and that requires models that can stand on their own normative legs.

## The autonomy spectrum

Reece framed his work around a distinction between *extrinsic* and *intrinsic* drives [[00:05:12]](https://youtu.be/VIDEO_ID?t=312){:target="_blank" rel="noopener"}. Extrinsic drives are externally conditioned: a monkey presses a lever because it gets juice. Intrinsic drives are the interesting ones---exploration, curiosity, play---behaviors that have no external reward signal and yet are structured and adaptive.

He defined **autonomy** as the capacity to motivate behavior not only by external states but by internal states, and to dynamically switch between them. An automaton is an input-output function. An autonomous agent has internal states that drive behavior, and it can reconfigure which drive is active at any moment.

The motivating example was a time-lapse of a baby playing in a room [[00:18:10]](https://youtu.be/VIDEO_ID?t=1090){:target="_blank" rel="noopener"}. We have robots that can do backflips (Boston Dynamics), drive across San Francisco (Waymo), and fold laundry (Figure). But how do you get a robot to do *that*---to play, to explore, to poke at things with no clear objective? You can't write down a loss function for it. And if you try ("touch everything with uniform probability"), the resulting behavior doesn't look anything like what the baby does.

## Why heuristic exploration fails

In standard RL, exploration is handled by heuristics [[00:21:48]](https://youtu.be/VIDEO_ID?t=1308){:target="_blank" rel="noopener"}. Epsilon-greedy works in gridworlds because the action space is small enough that random actions have a decent chance of being useful. Max-entropy RL works in continuous control by adding an entropy bonus to the policy. But both of these require an extrinsic task to anchor the learning. If you remove the task reward entirely and just optimize the entropy bonus, you get a policy that is maximally random, which is not exploration---it's noise.

Reece showed a video of what happens when you apply prediction-error-based curiosity (ICM, from Deepak Pathak's work at Berkeley) to a continuous-control swimming agent [[00:43:05]](https://youtu.be/VIDEO_ID?t=2585){:target="_blank" rel="noopener"}. The agent twitches its joints in place. There's a ball in the environment it could interact with, but it never goes near it. The prediction error from joint-twitching is enough to saturate the world model's learning, so the policy has no gradient pushing it toward more structured behavior.

## Three flavors of model-based intrinsic motivation

Reece surveyed three representative model-based approaches [[00:26:30]](https://youtu.be/VIDEO_ID?t=1590){:target="_blank" rel="noopener"}:

**Curiosity (ICM):** Train a world model to predict the next state. Use prediction error as the intrinsic reward. The agent pursues transitions its model can't predict. This works in discrete environments (the Mario demo was striking---an agent with *no* game score reward beating early levels), but fails in continuous control and falls prey to the **noisy TV problem**: if there's a source of irreducible stochasticity, the agent perseverates on it forever because it can never reduce its prediction error there.

**Eli** anticipated this, asking whether information gain would be a better signal [[00:30:28]](https://youtu.be/VIDEO_ID?t=1828){:target="_blank" rel="noopener"}. Reece confirmed: that's the natural next step, and ensemble disagreement is one computationally efficient estimator of Bayesian information gain.

**Disagreement:** Train an ensemble of world models. Use the variance of their predictions as intrinsic reward. This approximates information gain without requiring explicit KL computation. It avoids the noisy TV problem because ensembles converge on irreducible noise, so disagreement drops to zero.

**Learning progress (Gamma Progress):** Track the *dynamics* of prediction error over time using an exponential moving average of model parameters. Reward the agent for transitions where its prediction error is *changing*, not just large. This also avoids perseveration on static noise.

I mentioned Fritz Sommer's work on **predictive information gain (PIG)** [[00:33:51]](https://youtu.be/VIDEO_ID?t=2031){:target="_blank" rel="noopener"}, which starts from the forward KL, quantifies the learnable information remaining in the environment, and turns it into Bayesian inference. Reece was familiar with it and agreed it's among the more principled formulations, but noted that the deep RL community has generally traded mathematical elegance for computational efficiency---coming up with fast online estimators rather than tight bounds.

This points to a tension we didn't have time to fully explore: the gap between *elegant, principled, but intractable* approaches and *inelegant, hacky, but working* engineering solutions. Empowerment is another example on the elegant side. Fritz's PIG is yet another. The deep RL intrinsic motivation literature has mostly landed on the hacky side, and yet, as Reece showed, even the hacky methods produce impressively structured behavior in discrete domains.

## Zebrafish as a model system

Why zebrafish? Because they don't cooperate with experimenters [[00:45:27]](https://youtu.be/VIDEO_ID?t=2727){:target="_blank" rel="noopener"}. Unlike monkeys or mice, you can't really train a zebrafish to perform a task for a reward. Their behavior---hunting, foraging, predator avoidance, exploration---is intrinsically motivated. This makes zebrafish a natural testbed for studying autonomy: the data is untainted by task structure.

The specific dataset comes from a preparation where a larval zebrafish is head-fixed in a virtual reality environment. A striped ground plane drifts beneath it, simulating a current. When the sensorimotor loop is **closed**, the fish's tail movements control the visual feedback---it swims and sees itself swimming. When the loop is **open**, the visual feedback is disconnected---the fish tries to swim but nothing happens.

The behavioral signature is **futility-induced passivity** [[00:47:47]](https://youtu.be/VIDEO_ID?t=2867){:target="_blank" rel="noopener"}. In the open-loop condition, the zebrafish tries to swim, fails, and after some time gives up. Then it tries again. Then gives up again. This switching between active bursts and passive intervals is the target behavior.

The neural data is equally striking. Whole-brain calcium imaging (possible because larval zebrafish have transparent heads) reveals that during failed swimming, noradrenergic neurons fire across the entire brain. Radial astrocytes---non-spiking glial cells---accumulate calcium from these neurons via a leaky integration process. When the astrocyte calcium reaches a threshold, downstream GABAergic neurons silence the motor system, and the fish goes passive [[00:49:07]](https://youtu.be/VIDEO_ID?t=2947){:target="_blank" rel="noopener"}.

**Eli** asked whether the astrocytes' integrate-and-threshold dynamics make them equivalent to neurons [[00:50:31]](https://youtu.be/VIDEO_ID?t=3031){:target="_blank" rel="noopener"}. Reece clarified: astrocytes don't spike. They accumulate calcium at tripartite synapses (wrapping around pre- and post-synaptic terminals) and release it in a graded fashion downstream. It's more like neuromodulation than signaling.

**Michael DeWeese** raised a subtle point about proprioceptive fidelity [[01:01:13]](https://youtu.be/VIDEO_ID?t=3673){:target="_blank" rel="noopener"}: the head-fixed fish is in near-normal water (not viscous agar), so its tail movements are relatively natural, but the visual feedback is decoupled from actual hydrodynamics. Reece acknowledged that the model's proprioception is primitive---just joint velocities from the 5-link torque-actuated body---and doesn't model mechanoreceptors or skin. The key assumption is that proprioception is undistorted.

## 3M Progress: a compass for exploration

The central metaphor is a compass [[01:11:14]](https://youtu.be/VIDEO_ID?t=4274){:target="_blank" rel="noopener"}. A compass gives you a one-dimensional signal---where north is---and that's enough to navigate. You don't have to go north, but knowing where it is structures your decisions. What is the "north" for exploration?

Reece's answer: the physics of your ecological niche. Animals develop (or are born with) a model of how dynamics *should* work in their natural environment. When placed in a new environment, they can explore relative to that prior. The 3M (Model-Based, Memory-Informed, Multimodal) Progress algorithm has two stages:

**Active pre-training:** The agent swims freely in a naturalistic environment, learning a forward model of transition dynamics. This model becomes its fixed prior---its "compass needle."

**Exploration:** The agent is placed in the experimental protocol (head-fixed, open-loop). It also learns an online model of the new dynamics. The intrinsic reward is the absolute value of the difference between the online model's prediction residual (relative to the prior) and a leaky-integrated running average of that residual [[01:17:16]](https://youtu.be/VIDEO_ID?t=4636){:target="_blank" rel="noopener"}.

The absolute value is the normative choice: it makes the reward symmetric, so the agent is rewarded both for entering familiar-physics states (niche-seeking) and for leaving them (niche-avoidance). The result is an agent that straddles the boundary between known and unknown dynamics---Reece compared this to computation at the edge of chaos, where the most interesting dynamics live near a critical transition.

The pre-training phase can be interpreted as simulating development, or as a proxy for evolution. I asked about this directly [[01:43:44]](https://youtu.be/VIDEO_ID?t=6224){:target="_blank" rel="noopener"}, noting work by Barabási and others showing zebrafish motor behavior is largely genetically predetermined. Reece agreed the distinction matters but argued the key point is model-agnostic: *some process* endows the animal with a dynamics prior, and 3M Progress just needs that prior to exist, regardless of how it got there.

## Results: behavior and brain alignment

All baseline algorithms---ICM, disagreement, learning progress, random network distillation, max-entropy---converge to **stationary policies** in the open-loop condition [[01:04:14]](https://youtu.be/VIDEO_ID?t=3854){:target="_blank" rel="noopener"}. Some swim at full power for the entire episode. Some go fully passive. None produce the characteristic active-passive switching seen in real zebrafish.

3M Progress does. Its activity trace shows short active bursts interspersed with longer passive intervals, matching the real zebrafish barcode.

For neural alignment, Reece used a stringent metric: for each real neuron, find the single most correlated unit in the model [[01:23:08]](https://youtu.be/VIDEO_ID?t=4988){:target="_blank" rel="noopener"}. Zebrafish brains are so homogeneous across individuals that this one-to-one matching (no linear regression, no population weighting) already saturates inter-animal alignment. 3M Progress saturates this benchmark. The baselines don't.

I raised the caveat that this ceiling is reachable partly because zebrafish whole-brain activity during this behavior is low-dimensional---the first two PCs capture nearly all the variance [[01:29:59]](https://youtu.be/VIDEO_ID?t=5399){:target="_blank" rel="noopener"}. Reece agreed and emphasized that in more complex animals, the absolute scores would be lower, but the *relative* ordering should hold: the model with the right mechanisms should still outperform the ones without.

He also made a point I want to underscore: ICM actually predicts ~60% of the neural variance *despite* failing to capture the behavior. If we were just looking at a predictive score---a "brain score"---we might rank ICM as a decent model of zebrafish. But it's mechanistically wrong. It's missing the prior. The behavioral filter is essential: without matching the behavior, neural predictivity is ambiguous, because many different computations could produce correlated activity patterns in such a low-dimensional signal.

The principal components of the 3M agent's RNN map cleanly onto the biological circuit: PC1 tracks noradrenergic neuron activity (high during active swimming, low during passivity), and PC2 tracks astrocyte calcium dynamics (ramping up toward the active-to-passive transition) [[01:30:46]](https://youtu.be/VIDEO_ID?t=5446){:target="_blank" rel="noopener"}.

## Discussion: empowerment, active inference, and the road ahead

**Alec Segal** asked about the relationship to empowerment [[02:03:47]](https://youtu.be/VIDEO_ID?t=7427){:target="_blank" rel="noopener"}. Reece offered a nuanced answer: empowerment and curiosity are not competing on the same axis. Empowerment measures an agent's capacity to controllably reach states; curiosity measures its capacity to predict states. Empowerment is control-focused and converges to a single stable state of maximum controllability. Curiosity is prediction-focused and can keep the agent moving. For *exploration*, curiosity-type signals may be more appropriate. For learning *motor primitives* and discovering controllable options in the environment, empowerment is more natural.

I suggested that empowerment might be best used as a **diagnostic tool** rather than a training signal---a quantity you can compute post-hoc to characterize an agent or an environment, rather than something you optimize directly. Reece was receptive to this, noting that the zebrafish behavior is itself deeply related to empowerment: the fish is avoiding states where its actions have no causal effect on the environment, which is roughly what low empowerment means.

I also suggested a concrete analysis: take all the different agents (3M, ICM, disagreement, etc.), estimate their empowerment and plasticity using the framework Dave Abel presented in his recent talk on [Plasticity as the Mirror of Empowerment]({% post_url 2026-03-19-plasticityempowerment %}){:target="_blank" rel="noopener"}, and see whether 3M occupies a distinctive point on that simplex. This could connect the zebrafish work directly to the information-theoretic formalism from the RL mini-series.

**Mani Hamidi** connected the work to **Tomasello's evolutionary stages of agency** [[01:59:54]](https://youtu.be/VIDEO_ID?t=7194){:target="_blank" rel="noopener"}, asking where zebrafish fall in that phylogeny. Reece hadn't read the book but offered a general view: existing animals are snapshots of the evolutionary process at different points, and the goal of his program is to write down objectives that capture each stage's capacities after the fact, rather than trying to replicate the evolutionary process that produced them.

Two threads we didn't have time to explore fully deserve mention:

**Active inference.** The idea of introducing a prior over dynamics that captures the agent's expectations about how the world *should* work is strongly reminiscent of active inference, where agents minimize the divergence between their generative model and sensory observations. Reece uses actor-critic with PPO rather than variational inference, so the optimization machinery is different. But the normative structure---a prior, a residual, behavior driven by discrepancy---has clear parallels. How well a pure active inference agent would perform on this task, compared to 3M Progress, is an open and interesting question.

**Principled vs. practical.** We briefly touched on the tension between mathematically principled intrinsic motivations (predictive information gain, empowerment, Bayesian information gain) and the computationally efficient approximations that actually get deployed (ensemble variance, exponential moving averages, random network distillation). The deep RL community has mostly sided with the practical, and the practical has been surprisingly effective. But as Reece's results show, even the practical methods fail when you test them against real animal behavior. Whether the principled methods would do better---or whether the right answer lies in a different direction entirely, as 3M Progress suggests---remains open.

---

Next week, we continue the world-modeling series with Reece's academic grandfather, **Dan Yamins** (Stanford), presenting on [World Modeling with Probabilistic Structure Integration](https://arxiv.org/abs/2509.09737){:target="_blank" rel="noopener"}.

---

Watch the full meeting here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/Wv0QXDouf74?si=TdVQbYGMSSQ4e_3q" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
