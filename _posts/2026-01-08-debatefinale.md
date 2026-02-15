---
title: "RL Debates Finale: Synthesis and the Gap"
layout: single
tags: [RL, synthesis, agency, architecture, debate]
categories: [2026, January]
---

For the final session of the **[RL Debate Series]({{ "/debates/" | relative_url }})**, we brought all six contenders back, not to declare a winner, but to attempt a synthesis. What actually happened was messier and more interesting than that.

The discussion was organized around two goals: **Scientific Understanding** (can RL explain biological agency?) and **Engineering Utility** (can RL build artificial agents that work?). We asked each presenter to put a number on it. The numbers told a somewhat unexpected story.

---

## Part 1: How much can RL explain?

### The scientific side: a surprising consensus

A striking consensus emerged: nearly every contender, *including* RL-proponent Adam Lowet, estimated that standard RL explains only **~10–20%** of biological behavior.

Adam's reasoning was disarmingly concrete. The basal ganglia---the brain structure most associated with RL---occupies only 1.5% of human brain volume. Even scaling that up generously, huge swaths of what we do (perception, locomotion, language, reading) just aren't well-captured by reward maximization. As he put it: "I'm not always practicing my tennis serve. Sometimes I'm just walking."

Tom placed it at 20-30%, but added that RL has a **0% chance** of explaining how someone decides to move to a new city to start a new career. That kind of goal invention, he argued, lives entirely outside RL's reach.

Anne Collins gave 10-20% with a crucial caveat: the umbrella word "RL" itself is part of problem. The engineering sense, the behavioral sense, and the neuroscientific sense of "RL" are somewhat different things, and collapsing them into one term contributes to people talking past each other.

### The engineering side: a sharp divide

On the question of building agents, the room split:

* **The optimists:** Adam Lowet argued that in any domain with verifiable rewards---such as coding, math, and formal reasoning---RL + pre-training is sufficient for superhuman performance. He put engineering at 90%. Eli Sennesh went to 80%, *but only if* you count KL-controlled fine-tuning of LLMs as RL (which is really just shaping a trajectory distribution, not solving nested Bellman equations).

* **The skeptics:** Anne Collins estimated ~30%, noting that every successful RL application she's seen depends on engineers adding massive structure on top. Niels Leadholm argued that deep learning's fundamental brittleness (e.g., adversarial examples, unreliable generalization) makes it unsuitable for open-ended, non-stationary worlds, no matter how much you scale it.

Fritz declined to give a precise number ("Higher than 10%, I don't care"), but made a subtle point: RL's engineering numbers look inflated because we define narrow tasks with clean reward functions. That's not the robot reproducing natural behavior. That's us making the problem easy enough for RL to solve.

---

## Part 2: The big arguments

### <a href="https://www.youtube.com/watch?v=GKSPT8-yyBk&t=1380s" target="_blank">[00:23:00] "Abolish the Value Function"</a>

The sharpest philosophical exchange was between Eli Sennesh and Adam Lowet. Eli argued that treating biological life as "maximizing reward" is an ontological error. The "reward function" in standard RL is what he called a *Deus Ex Machina*: a non-constructive existence proof from von Neumann-Morgenstern utility theory. It says: *if* an agent acts coherently, *then* there exists some function describing that behavior. But it doesn't tell you how to find it, how to construct it, or how the brain implements it.

Adam pushed back: the engineering success of *actually instantiating* value functions (actor-critic methods, TD learning) is astonishing regardless of philosophical purity. The thing didn't *need* to be constructible, but it turns out that by constructing it, you can explain not only choice but also learning.

Eli's counter: that's fine for engineering, but if our goals are scientific, we need *identifiable* quantities---variables with real physical units, one-to-one mappings between data and parameters. A reward function whose only mathematical property is "it's more when behavior is better" gives an experimentalist nothing to work with.

### <a href="https://www.youtube.com/watch?v=GKSPT8-yyBk&t=1770s" target="_blank">[00:29:30] The Dark Matter of Behavior</a>

This led to what might be the most important critique of the entire series. Eli pointed out that neuroscience systematically screens off the hardest questions. When experimentalists train a monkey to do two-alternative forced choice---saccade left or saccade right---they're *causally eliminating* the decision of why the animal acts the way it does. The animal's own goal selection, context sensitivity, and behavioral switching get dismissed as "misbehavior."

Adam, wearing his experimentalist hat, acknowledged the problem but highlighted the practical bind: "No one has yet come up with an experiment that would really allow you to ask in animals the questions that Eli is posing." The challenge is real, but it's not that people are ignoring the dark matter. It's that nobody knows how to illuminate it.

Eli's answer was directed at theorists: we need to step up and provide models with identifiable variables so that experimentalists know what to measure. Until theorists do that work, the experimental impasse will continue.

### <a href="https://www.youtube.com/watch?v=GKSPT8-yyBk&t=4260s" target="_blank">[01:11:00] Structure vs. Scale: The Brittleness Problem</a>

Niels Leadholm mounted the strongest case against the "scale is all you need" position. He cited Gilmer et al. (2018), a deceptively simple result: take two data clouds in 500 dimensions, train a classifier with hundreds of millions of samples, get 99.9999% accuracy, and the decision boundary is still riddled with errors in regions you'd never naturally sample from. Adversarial attacks exploit exactly these gaps.

His broader point: deep learning creates "alien" systems. They work brilliantly within their training distribution, but their failure modes are inhuman and unpredictable. Vibe coding has the reputation it has for a reason. If we're building something for open-ended, non-stationary worlds (actual AGI) we can't paper over this with more data.

Hadi (moderator) pushed back with a recent paper from Geirhos et al. (late 2025) showing that video models exhibit zero-shot generalization and even respond to perceptual illusions in human-like ways. Every six months, the models solve problems we thought were fundamental limitations. Niels held his ground: as long as performance scales with data rather than with architectural insight, the system remains fundamentally data-bottlenecked and brittle at the edges.

### <a href="https://www.youtube.com/watch?v=GKSPT8-yyBk&t=3095s" target="_blank">[00:51:35] Curiosity vs. Empowerment</a>

Fritz Sommer and Tom Ringstrom had a revealing exchange about what drives exploration. Fritz defined curiosity strictly as **optimal experimental design**: you face something novel, you need to understand how it works, so you design actions that maximally reduce your uncertainty about specific hypotheses. Tom defined empowerment as maximizing the mutual information between your actions and sensory outcomes: a measure of how much control you have over your world.

Fritz argued empowerment is sometimes useful but "too compulsive" as a general principle. Pole balancing, for instance, requires *reducing* the mutual information between your actions and sensory input. You want the pendulum to stay boring and still. Tom countered that empowerment is the only framework he knows that scales to high dimensions and can explain how things become *valuable in context*, that is, how you do credit assignment for functional significance. Without it, you end up with Pareto frontiers of competing values and no principled way to weight them.

Fritz also stressed a point that deserves more attention: you can't understand algorithms divorced from the hardware they run on. Metabolic efficiency, energy constraints, and neuromorphic computing aren't implementation details. They are fundamental considerations that shape what algorithms are possible in the first place.

### <a href="https://www.youtube.com/watch?v=GKSPT8-yyBk&t=1570s" target="_blank">[00:26:10] Layered Control in Real Robotics</a>

Eli offered a pragmatic engineering picture that cut through some of the RL-vs-not-RL framing. In real working robots, control is layered: **RL or logical reasoning at the top** (task selection), **model predictive control in the middle** (planning), and **classical control at the bottom** (stabilizing individual actuators). The frontier isn't about any single algorithm. It's getting these layers to communicate. Perception researchers and control researchers sit in different labs, and fusing their representations remains more of a "people problem" than a mathematical barrier.

Adam partially agreed but noted that recent advances in sim-to-real transfer---better NVIDIA simulation environments, simple algorithms like PPO scaling with compute---are why bipedal robots can now walk over uneven terrain where Boston Dynamics couldn't for years.

---

## Part 3: Hadi's attempt at a failed synthesis (and what emerged from it)

### <a href="https://www.youtube.com/watch?v=GKSPT8-yyBk&t=5530s" target="_blank">[01:32:10] Prediction Error Minimization as Unifying Theme?</a>

Hadi tried to propose **prediction error minimization** as a unifying framework: each camp just defines a different prediction and a different error. Adam predicts reward. Eli predicts sensory states relative to set points. Fritz predicts information gain. Tom predicts option termination and empowerment. Niels predicts sensorimotor mismatch.

It fell flat. Eli called it a "deepity": superficially profound, actually vacuous. Any stable dynamical system can be written as a gradient flow on some Lyapunov function. That's a theorem, not an insight. The hard work is identifying *which* function, *which* gradient, and *which* implementation.

Hadi, agreeing with Eli, responded with an analogy to physics: saying "everything is gradient descent" is like saying "everything obeys the principle of stationary action" in physics. It is true, but the Nobel Prizes went to people who found the specific Lagrangians that explain something about the physical reality, with testable predictons.

Anne's objection was even more fundamental: she doesn't think unification is necessary or likely. The brain developed through evolution---a messy, path-dependent, locally-optimal, resource-constrained process. Nothing guarantees a single elegant principle underneath. If someone found one, great, but she'd need it to have explanatory power, interpretability (mapping computational processes to neural circuits), and predictive power.

### <a href="https://www.youtube.com/watch?v=GKSPT8-yyBk&t=5990s" target="_blank">[01:39:50] The Mars Rover: Build a Survivor</a>

Since top-down synthesis failed, we tried bottom-up. The thought experiment: you're building a Frankenstein agent to survive on Mars. Each presenter adds one component (and you're encouraged to pick from *someone else's* camp).

* **Niels** chose **Empowerment** (from Tom's camp) --- the ability to evaluate which actions keep the most future options open.
* **Anne** chose **Resource Constraints** --- bottlenecks that force the system to organize information efficiently, possibly explaining why we have a working memory capacity of ~4 items despite billions of neurons. Maybe it's a feature: constraints that promote generalization.
* **Eli** chose **Interoception** --- temperature sensors, battery level monitors, all feeding directly into the learning system. Whatever objective function the agent optimizes, it needs to know that if it doesn't get its solar panels into the light, it dies.
* **Tom** chose **Temporal Distributions** --- the ability to represent and reason about time as a variable, so the agent can ask: "Will I run out of battery *before I reach the base*?"
* **Adam** chose **A Good Simulation** --- the equivalent of evolutionary pre-adaptation, or the specific training needed to survive Mars. Humans would do poorly if dropped on Mars without preparation. A deep learning system needs sufficient simulated experience before deployment.

Something interesting emerged in the overlap. Eli's interoception gives the agent *awareness* of its resource state. Anne's computation under rerouce constraints force it to be *efficient* with those resources. Tom's temporal reasoning lets it *plan* around resource depletion over time. Without anyone trying to unify their frameworks, the Mars rover naturally converged on a system that regulates internal resources under constraints with temporal foresight---a picture closer to allostatic regulation than to reward maximization.

---

## The Takeaway

The RL Debate Series started with a simple question---*what drives behavior?*---and ended with something more honest than a clean answer.

RL explains a modest slice of biological behavior (10-30% by most estimates). It's more useful in engineering, especially for well-defined tasks with verifiable rewards, but everyone acknowledged it's insufficient for open-ended intelligence. The hardest unsolved problems---goal selection, context-sensitive value, lifelong learning, the fusion of perception with control---live outside RL's current reach.

A deep tension emerged, but it wasn't between RL and its alternatives. It was between the desire for grand unifying theories and the messy reality that brains are evolved systems full of local optima, resource constraints, and historical accidents. Whether that messiness conceals an elegant principle or simply *is* the principle remains the open question.

The field's biggest bottleneck may be theoretical: we lack identifiable, physically grounded computational theories of natural behavior. The kind that could tell an experimentalist exactly what to measure and tell an engineer exactly what to build.

Until theorists provide that, the *dark matter of behavior* will stay dark.

---

*Organized by Hadi Vafaii at the [Redwood Center for Theoretical Neuroscience](https://redwood.berkeley.edu/), UC Berkeley. Supported by the Redwood Center and its director, Bruno Olshausen. Recordings of all sessions are available on [YouTube](https://www.youtube.com/@SensorimotorAI).*

---

Watch the full finale and the resulting synthesis below:

<iframe width="560" height="315" src="https://www.youtube.com/embed/GKSPT8-yyBk?si=l3K-awJlHVvGXK8E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
