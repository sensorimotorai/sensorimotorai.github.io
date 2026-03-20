---
title: "Plasticity as the Mirror of Empowerment (David Abel)"
layout: single
tags: [RL, agency, empowerment, plasticity, information-theory, directed-information, world-models]
categories: [2026, March]
---

Two weeks ago, [David Abel argued]({% post_url 2026-03-05-threedogmasrl %}){:target="_blank" rel="noopener"} that RL's central concepts need precise mathematical definitions. Last week, [Mani Hamidi responded]({% post_url 2026-03-12-rldogmasevolution %}){:target="_blank" rel="noopener"} through the lens of evolutionary theory, showing that *adaptation* is just as underdeveloped as *agency*. Both talks circled the same gap: we talk about agents constantly, but we still lack a formal vocabulary for their properties, the way physics has mass and energy for inanimate matter.

Today, Dave returned with a concrete proposal. If mass and energy are the elemental properties of rocks, then **plasticity** and **empowerment** might be the elemental properties of agents. He formalized both using a single information-theoretic tool, showed they are exact mirrors of each other, and proved that no agent can simultaneously maximize both arbitrarily. This gives us a precise mathematical language for talking about adaptation and control as intrinsic properties of agents, not just side effects of solving tasks.

- Paper: [Plasticity as the Mirror of Empowerment](https://openreview.net/forum?id=eOZFqyE9Ok){:target="_blank" rel="noopener"}
- Presenter: David Abel (Google DeepMind)

The discussion was wide-ranging, as it has been this pat few meetings. **Alison Gopnik** connected the formalism to developmental biology, caregiving, and the explore-exploit trade-off. **Michael DeWeese** dug into the information-theoretic foundations and their history in satellite communication. **Eli Sennesh** pushed on the relationship between plasticity and homeostasis. **Mahsa Bastankhah** probed the definition of directed information. **Mandana Samiei** asked whether the asymmetry between plasticity and empowerment could reveal causal direction. **Alec Segal** raised the connection to epiplexity and fixed policies. **Catherine Ji** expressed excitement about the cycles of plasticity and empowerment. I (**Hadi**, the organizer) focused on the big missing piece I see in the framework: the role of internal models, the cognitive component that lets an agent *perceive*, *simulate*, *predict*, and *plan*, rather than merely react.

## Table of Contents

- [The setup: what are the elemental properties of agents?](#the-setup-what-are-the-elemental-properties-of-agents)
- [Empowerment and plasticity, informally](#empowerment-and-plasticity-informally)
- [Directed information and the conservation law](#directed-information-and-the-conservation-law)
- [The formalism: generalized directed information](#the-formalism-generalized-directed-information)
- [The main result: the plasticity-empowerment dilemma](#the-main-result-the-plasticity-empowerment-dilemma)
- [Discussion I: Development, caregiving, and exploration](#discussion-i-development-caregiving-and-exploration)
- [Discussion II: Causal direction and fixed policies](#discussion-ii-causal-direction-and-fixed-policies)
- [Discussion III: World models and the cognitive gap](#discussion-iii-world-models-and-the-cognitive-gap)
- [Discussion IV: Goals, rewards, and the inside-out view](#discussion-iv-goals-rewards-and-the-inside-out-view)
- [Broader implications: from behaviorist grounding to cognitive integration](#broader-implications-from-behaviorist-grounding-to-cognitive-integration)

---

## The setup: what are the elemental properties of agents?

Dave opened with a question by analogy. In a free body diagram, we know what the relevant properties are: mass, friction, the height of the ramp, the force due to gravity. These are the elemental quantities that factor into predictions. When it comes to agents, organisms, or any animate system, we don't have the same clarity. What are the analogs of mass and energy for a caterpillar?

One common approach in RL is to define agents indirectly through the environments they solve. The Arcade Learning Environment, the B-Suite, Montezuma's Revenge: these benchmarks reveal *symptoms* of agent capabilities (exploration, credit assignment, memory), but the underlying properties of the agent remain implicit. Dave's proposal: make them explicit. Start defining the agent in terms of quantities that are intrinsic to the agent-environment interaction, not derived from benchmark performance.

His candidates: **empowerment** (how much the agent's actions influence its future observations) and **plasticity** (how much the agent's observations influence its future actions).

## Empowerment and plasticity, informally

**Empowerment** captures the capacity to control. It measures how many distinguishable outcomes the agent can bring about through its actions. A caterpillar that can eat a flower, eat a leaf, transform into a butterfly, and fly over a river is more empowered than a rock sitting on the ground. The formal definition comes from [Klyubin et al. (2005)](https://arxiv.org/abs/nlin/0509006){:target="_blank" rel="noopener"}: empowerment is the channel capacity between the agent's actions and its subsequent observations.

**Plasticity** captures the capacity to adapt. How much does the agent change what it does based on what it observes? An agent that ignores all inputs and emits a fixed action sequence has zero plasticity. An agent that dramatically restructures its behavior in response to new information has high plasticity. The original natural-language definition goes back to William James in the 1890s, who described it as "the degree of yield of a structure." The computational definition Dave and collaborators propose is the mirror of empowerment: directed information from observations to actions, rather than from actions to observations.

Dave introduced the distinction between **behavioral plasticity** (does the agent change its *actions* in response to experience?) and **cognitive plasticity** (does experience change something *inside* the agent, like its beliefs, parameters, or neural circuitry?). The two are related, since most internal changes eventually manifest as behavioral changes, but they have different implications for formalization. For this paper, the behavioral view takes center stage, but Dave flagged the cognitive version as an important direction for future work.

The musician analogy made the mirror relationship vivid. Take three musicians jamming: a violinist, a pianist, and a guitarist. The violinist's **empowerment** is how much their notes influence what the pianist and guitarist play. The violinist's **plasticity** is how much the violinist is listening and responding to the piano and guitar. If the violinist fully controls the session, there's no room to be surprised or influenced back. If the violinist is purely reactive, they exert no influence on the group's direction. A good jam session lives in the balance.

## Directed information and the conservation law

The mathematical backbone of the paper is **directed information**, a concept from information theory that Dave said he didn't know before this project and has come to appreciate deeply. The story begins with Shannon's classic setup: Alice sends a message to Bob through a noisy channel. Shannon's mutual information measures how much of Alice's message survives the noise. But this is a one-directional channel.

In the 1970s, Marko extended this to a **bidirectional** channel: Alice sends a message to Bob, Bob sends a message back, and this exchange continues indefinitely. Now there are two kinds of information: how much Alice influences Bob, and how much Bob influences Alice. [Massey (1990)](https://ieeexplore.ieee.org/document/6774173){:target="_blank" rel="noopener"} formalized this as **directed information**, and [Massey and Massey (2005)](https://ieeexplore.ieee.org/document/1523643){:target="_blank" rel="noopener"} proved a result Dave called "the conservation law of directed information": the total information exchanged between Alice and Bob is exactly equal to the sum of the two directed informations (Alice-to-Bob plus Bob-to-Alice).

The conceptual move is to treat the agent-environment interaction as exactly this kind of bidirectional communication. The agent sends actions (like Alice's messages), the environment sends observations back (like Bob's responses), and the exchange continues indefinitely. Empowerment is the directed information from actions to observations. Plasticity is the directed information from observations to actions. The conservation law means their sum is bounded by the total information exchanged.

**Michael DeWeese** engaged deeply with the information-theoretic foundations. He asked whether the noise in the two directions needs to be symmetric (Dave's answer: probably not for the main result, but there may be subtleties), and connected the bidirectional channel idea to work on satellite communication, recalling a researcher (David MacKay, as Mike later identified in the chat) who had applied similar ideas to improve baud rates via feedback.

**Eli Sennesh** caught the two different arrow symbols in the conservation law diagram and asked why. Dave explained it's a fencepost issue: one signal has to go first, creating an off-by-one asymmetry in the conditioning.

## The formalism: generalized directed information

To make the framework flexible enough for studying agents, Dave introduced the **generalized directed information (GDI)**. Standard directed information is defined over equal-length sequences from time 1 to N. The GDI allows arbitrary time intervals: how much did actions during interval [A, B] influence observations during interval [C, D]? This lets you ask questions like: how empowered was the agent during the last hour? How plastic was it this morning?

The GDI satisfies three sanity checks. First, it recovers standard directed information when you set both intervals to [1, N]. Second, it respects temporal consistency: future X's can't influence past Y's (the quantity is zero when the action interval comes entirely after the observation interval). Third, it generalizes the conservation law, with an added conditioning on everything that came before the intervals, to remove confounders. (Dave illustrated this with an example: if X₁ being blue causes everything in both intervals to be blue, we need to condition out X₁ to avoid falsely attributing information flow between the intervals.)

Using the GDI, Dave unified several existing empowerment definitions. The original [Klyubin (2005)](https://arxiv.org/abs/nlin/0509006){:target="_blank" rel="noopener"} definition uses mutual information with a max over open-loop policies. [Capdepuy's (2011)](https://eecs.qmul.ac.uk/~dg/capdepuy-thesis.pdf){:target="_blank" rel="noopener"} extension uses directed information and allows arbitrary controller sets. The GDI subsumes both by allowing arbitrary intervals *and* arbitrary controller sets.

I asked Dave to map the landscape of empowerment definitions. He confirmed that the GDI lets you move between the Klyubin and Capdepuy versions by varying parameters, but noted there's a whole other category of empowerment definitions grounded in strictly causal language that the GDI may not fully capture.

**Mahsa Bastankhah** raised a precise technical question: would the formalism still work if you conditioned on all previous Y's and only looked at the latest message, rather than the full sequence? Dave traced through the GDI definition and showed this corresponds to setting A = B and C = D (a single time step), which recovers a conditional mutual information term that captures exactly this. He noted there may be something special about Markov settings here.

Capdepuy also distinguished between **potential empowerment** (max over all possible agents, capturing the morphology and interface) and **actual empowerment** (the empowerment of a specific agent with a specific policy). Dave focused primarily on the actual empowerment of individual agents.

## The main result: the plasticity-empowerment dilemma

With both concepts defined using the GDI, the main theorem follows: **for any agent, any environment, and any choice of time intervals, the sum of empowerment and plasticity is bounded above.**

Concretely: the bound M is determined by the size of the action and observation spaces and the lengths of the intervals. The upper bound on E + P is the minimum of the log of the observation space times the observation interval length, and the log of the action space times the action interval length. This creates a simplex: agents can be anywhere in the triangle below the diagonal, but the region above the diagonal is unrealizable.

Dave was careful to note that this is a *dilemma*, not a forced trade-off at every point. An agent with low plasticity and low empowerment can increase either without sacrificing the other. The tension only bites when the agent is near the boundary: increasing empowerment further then requires sacrificing plasticity, and vice versa.

Two small-scale experiments (two-armed Bernoulli bandits) built intuition. In the first, varying epsilon in epsilon-greedy Q-learning showed that plasticity decreases as the agent becomes more random: a fully random agent (epsilon = 1) has zero plasticity because its actions are completely disconnected from its observations. In the second, varying the value function initialization from pessimistic to optimistic showed empowerment increasing with optimism. Pessimistic agents stick to one action and don't create diverse experiences; optimistic agents explore and exert more influence on the environment.

**Alison Gopnik** flagged something counterintuitive: higher exploration (high epsilon) corresponds to *lower* plasticity. She asked whether this is just the explore-exploit trade-off under a new name. Dave said the two are related but distinct. Effective exploration requires empowerment (you need to cause diverse outcomes), but then responding appropriately to what you learned requires plasticity. So effective exploration involves a *temporal sequence* of empowerment followed by plasticity, not a single trade-off at one time point. The random exploration of high-epsilon is empowerment without plasticity: you perturb the environment but learn nothing from the result.

**Alec Segal** asked about fixed policies. A constant-action policy has zero plasticity (it ignores observations). A stationary Markov policy that selects actions based on the current observation has some plasticity at the action level, even though the policy itself doesn't change. This connects to the behavioral vs. cognitive distinction: if the "object being influenced" is the agent's policy rather than its action, then only agents that update their policy over time count as plastic.

Alec also raised the connection to **epiplexity**, an information-theoretic concept about the information accounting for computationally constrained agents. Dave agreed there's likely a deep connection: boundedness constrains both plasticity and empowerment, and epiplexity may formalize part of that constraint. [*Catherine Ji asked for the epiplexity paper in the chat; Alec shared [Mira (2025)](https://arxiv.org/abs/2601.03220){:target="_blank" rel="noopener"}.*]

## Discussion I: Development, caregiving, and exploration

**Alison** opened the discussion with three threads, all stemming from the temporal profile of plasticity and empowerment over a lifetime.

**Thread 1: The developmental trajectory.** There is a broad biological pattern, across a wide range of organisms, of high plasticity and low empowerment early in life, gradually shifting to high empowerment and low plasticity in adulthood. Human children are the most dramatic example: long periods of immaturity, high learning rates, large brains. This pattern is associated with intelligence broadly construed. Alison pointed out that it maps naturally onto the simplex: early life is the bottom-right corner (high plasticity, low empowerment), and adulthood is the top-left (high empowerment, low plasticity). From the neuroscience side, early brains show massive synaptic proliferation followed by pruning, and adult brains are highly myelinated (fast and efficient) but poor at plasticity. Neural net models, despite being "based on neural nets," don't exhibit this pattern.

Dave resonated with this and mentioned his colleague Claire Lyle's work on the loss of plasticity in neural networks, which documents how networks lose the ability to learn in ways that don't resemble biological aging.

**Thread 2: Caregiving as empowerment maximization.** Alison proposed that a caregiver can be understood as an agent that is trying to maximize the *empowerment* of another agent over a long period of time. Caregivers don't just keep children alive (reward maximization); they expand the range of things the child can eventually do. This fits the framework: the caregiver's goal is to move the child from high-plasticity/low-empowerment toward high-empowerment while the child can still learn from the process. Alison noted that caregiving is almost completely missing from formal cognitive science, political science, and economics.

**Thread 3: Empowerment *gain* over empowerment.** Instead of maximizing empowerment (which leads to a static equilibrium, like a deterministic casino), children seem to maximize *empowerment gain*: as soon as they master the busy box, it becomes boring and they move on to the next thing. Dave mapped this onto the simplex: he suspected empowerment gain happens in the low-empowerment/low-plasticity region, where gains don't come at the expense of plasticity.

Alison also asked about chickens and other organisms with the reverse pattern (constrained, reflex-like behavior early on, with associative learning enabling more plasticity later). And she raised LLMs: a base model that hasn't been fine-tuned might be an example of high plasticity (its outputs are extremely sensitive to its input context) and low empowerment (its outputs don't feed back to change anything about the model itself). Dave tentatively agreed on the plasticity side but was less sure about empowerment, since people interacting with LLMs can be substantially influenced by LLM outputs. Alison's point was that the base model, setting aside RLHF, isn't doing reinforcement learning at all: it's just extracting statistical structure from observations, not using the consequences of its actions to update itself.

Dave added that the GDI framework can address this by asking about the *timescale* of adaptation. Within a single context window, an LLM might show high plasticity. Over weeks or months, with no weight updates, the plasticity would be zero. The GDI lets you vary the intervals and reveal this temporal structure.

## Discussion II: Causal direction and fixed policies

**Mandana Samiei** asked whether the asymmetry between an agent's plasticity and empowerment (when action and observation spaces are comparable) could serve as a signal for learning causal direction. If the directed information from actions to observations is much higher than the reverse, does that tell us who is doing the "causing"?

Dave worked through the question carefully. In settings where the action and observation spaces are comparable, the asymmetry might reveal something about the relative capacity or "size" of the two systems, which is doing more of the pushing. But he was cautious about equating this with causality in the interventionist sense. The GDI is fundamentally information-theoretic, and there are subtleties, paradoxes of causality that arise when you condition on the past, where the information picture and the causal picture come apart. His colleague John Richens has been thinking about a more explicitly causal version of the plasticity-empowerment tension.

## Discussion III: World models and the cognitive gap

This was the thread I (Hadi) kept returning to throughout the session, and where I think the framework has its most promising direction for growth.

I raised this early: plasticity and empowerment, as defined, are purely behaviorist properties. They measure what the agent *does* in response to what it *sees*, and vice versa. But they leave out something fundamental: the agent's **internal model**. An agent that can *predict* its future observations, *simulate* the consequences of its actions before executing them, and *anticipate* its own physiological needs is doing something qualitatively different from an agent that merely reacts.

This is Kenneth Craik's idea. In *The Nature of Explanation* (1943), Craik proposed that organisms carry an internal model of external reality, a "small-scale model" that lets the agent try out alternatives, conclude which is the best, and react to future situations before they arise. Simulation, thinking, prediction: this is what a world model does. And it is absent from the plasticity-empowerment framework as currently stated.

Dave acknowledged this gap. He said plasticity and empowerment are intended to be *pieces* of the picture, not a comprehensive account of agency. Goals, intentions, and internal models are left out, implicitly present (an empowered agent probably has a good model of the world, or it couldn't exert influence effectively) but not explicitly formalized.

**Alison** pushed further from the other side. She noted that building a causal model of the environment is itself an act of plasticity (the model is updated by observation) and deeply connected to empowerment (interventions, which are a form of action, are how you test and refine the model). She's been thinking about how to connect the formal apparatus of causal model updating with the plasticity-empowerment picture.

I then offered a more specific argument. Empowerment, as Dave defines it, is agent-centric: it's the agent's *perceived* control over its future. But to have a perception of control, you need a mechanism that substantiates that perception. You need an internal model that can represent action-conditioned predictions. The capacity of that internal model should bound the agent's empowerment: a richer model lets you absorb more action-conditioned information and exert more precise influence over the environment.

Dave agreed. He connected this to [Tomasello's four tiers of agency](https://mitpress.mit.edu/9780262047005/the-evolution-of-agency/){:target="_blank" rel="noopener"}, which roughly upgrade the extent of an agent's causal model. Each tier gains more capacity for counterfactual reasoning, and this looks like an empowerment ladder.

I then speculated about the connection between internal models and position on the simplex. An agent with a *perfect* model might have maximal empowerment but zero plasticity: it doesn't need to update, it already knows everything. An agent in a setting where "all models are wrong, but some are useful" must retain some plasticity, because its model will always need revision. The model quality might constrain which regions of the simplex are reachable.

Dave liked this framing and extended it: if we know we're in a setting where the right model is unattainable, we know we must remain in a region of nonzero plasticity. Different models might correspond to different positions on the boundary, which opens up the question of what an *optimal* trajectory through the simplex looks like for agents with different modeling capacities.

I also speculated about ecology. If we could measure the plasticity and empowerment of real organisms (which is feasible, since these are behavioral measures requiring no brain recordings), and locate them on the simplex, would we find that real organisms cluster in a particular region? The extreme cases, an organism that can perceive everything but only emit bits, or vice versa, seem biologically implausible. Dave agreed that there are likely regions of the simplex that contain no biologically viable organisms, and connecting this to environmental constraints and evolutionary pressures could be a compelling research direction.

## Discussion IV: Goals, rewards, and the inside-out view

As the session neared its end, I steered the conversation to the elephant in the room: goals and rewards are absent from the framework.

Dave offered a few seeds. One option: designate reward as a special component of the observation, and define "reward plasticity" as the agent's sensitivity to changes in reward. But this doesn't capture what we actually care about, whether the agent's influence and adaptation are *in the service of* some goal. Getting there would require reward to exert a "normative pressure" on how the agent is influenced and how it does its influencing. He doesn't have a full picture for this yet.

I offered a more radical proposal, building on something Alison said two weeks ago. Maybe goals, as we usually think of them, are post-hoc rationalizations. We act, and then we retrospectively assign purpose. This echoes Buzsáki's *The Brain from Inside Out*: start from the syntax of neural activity, and let goal-like behavior *emerge*, rather than defining goals as a starting point. Could the information-theoretic framework be extended so that what we call "goals" emerges as a consequence of plasticity and empowerment dynamics, rather than being posited as an additional ingredient?

Dave found this compelling but flagged a technical worry: inverse RL shows that every agent is consistent with many reward functions, including the trivial one (the agent's goal is to do exactly what it did). Eliminating these trivial explanations in favor of genuinely explanatory ones is hard. But he pointed to work by Amin, Zhang, and Singh showing that with enough interventions, you can narrow the consistent reward functions down to an equivalence class unique up to affine transforms, analogous to the von Neumann-Morgenstern results. Maybe with the information-theoretic language, there are new mechanisms for doing this "inside out."

**Alison** raised a question that ran through the entire session: maybe the direction of explanation should be reversed. The standard RL story starts with reward and treats empowerment as secondary (an intrinsic reward signal, or a proxy). But maybe empowerment is primary. The fundamental thing agents do is increase their capacity to influence the world. Reward then becomes a *later* specialization: given all the things you *can* do, which one should you do *now*? (As I put it during the session: if you take the reward-explains-everything view seriously enough, you end up saying the electron orbits the nucleus because it's more rewarding. At that point the concept has lost all content.) This reversal, from empowerment-first to reward-as-specialization, feels more consistent with what we see in developing children. Babies invest enormous calories in exploring and expanding their action repertoire. They maximize empowerment gain. The reward-optimizing adult is a downstream product of that earlier investment.

I closed by connecting this to next week's talk: **Amitai Shenhav** will present the **affective gradient hypothesis**, which argues that we do things solely because we anticipate they will make us feel good or prevent us from feeling bad. It's all affect, all the way down. This may offer yet another angle on where goals come from, and whether reward, empowerment, or affect is the right primitive.

## Broader implications: from behaviorist grounding to cognitive integration

Here is why I (Hadi) think this talk was a turning point for the mini-series.

The first two talks identified what's missing: precise definitions of agency (Dave's Three Dogmas) and adaptation (Mani's evolutionary response). Today's talk delivered something concrete. We now have a mathematical framework, built on generalized directed information, that assigns real numbers to two properties of agents: their capacity to adapt (plasticity) and their capacity to control (empowerment). These numbers are defined in a way that is agent-centric, environment-independent (at least in the potential version), and respects a formal conservation law. And we have a theorem: these two capacities are in tension.

This is a behaviorist starting point, and a good one. It tells us what an agent *does*, not what it *thinks*. But the session made clear that the next step is integration with the cognitive picture: world models, causal reasoning, simulation. Kenneth Craik argued in his extremely prescient book [TODO] 1943 that the defining feature of thought is the ability to carry a "small-scale model" of external reality and use it to anticipate events. Dave's framework captures adaptation and control at the behavioral level. The open question is whether the same information-theoretic language can be extended to formalize the *internal model* that makes effective adaptation and control possible.

Here is my speculation. An agent's position on the plasticity-empowerment simplex should be *mediated* by the quality of its world model. A better model lets you convert plasticity into empowerment more efficiently: you learn faster from less data (high plasticity), and you exert more precise control with fewer actions (high empowerment). A worse model wastes both: observations don't update the agent appropriately, and actions don't produce the intended effects. If this is right, then the trajectory through the simplex over a lifetime, the arc from high plasticity to high empowerment that Alison identified as a universal biological pattern, might be best understood as the consequence of building/developing a progressively better world model.

The formalism is worth pursuing for another reason. Fields mature when their central concepts become precise enough to analyze systematically. Newton did this for motion, Turing for computation, Shannon for information. Dave's framework gives us a precise vocabulary for two properties that everyone agrees agents must have but nobody has defined in a unified way. The plasticity-empowerment dilemma is the kind of result that changes what questions a field can ask. It's a constraint that every theory of agency, biological or artificial, will eventually have to account for.

Next week, **Amitai Shenhav** closes the March RL mini-series by presenting the [affective gradient hypothesis](https://www.cell.com/trends/cognitive-sciences/abstract/S1364-6613(24)00202-X){:target="_blank" rel="noopener"}: the claim that all motivated behavior is driven by anticipated affect, not by goals or rewards in the RL sense. If Dave's talk gave us the behaviorist foundation, Amitai's may offer the affective one. Between empowerment, adaptation, and affect, the mini-series is converging on a picture of agency that is richer, more grounded, and more precise than what we started with. Join us on **March 26** for the finale.

---

Watch the full meeting here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/PLACEHOLDER" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
