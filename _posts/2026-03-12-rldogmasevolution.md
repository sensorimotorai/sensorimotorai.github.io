---
title: "Illuminating the Three Dogmas of RL under Evolutionary Light (Mani Hamidi)"
layout: single
tags: [RL, evolution, open-endedness, adaptation, agency, novelty-search, thermodynamics]
categories: [2026, March]
---

Last week, [David Abel argued]({% post_url 2026-03-05-threedogmasrl %}){:target="_blank" rel="noopener"} that RL's central concepts (agent, learning, reward) need more precise definitions. He identified three dogmas limiting the field's scientific ambitions. But he left one question conspicuously underdeveloped: *what is adaptation, exactly?*

This week, Mani Hamidi from the University of Tübingen picked up where Dave left off. His response paper offers evolutionary theory as a concrete paradigm that can address two of the three dogmas: it gives *adaptation* (Dogma 2) algorithmic substance through open-ended novelty search, and it complicates the *reward hypothesis* (Dogma 3) through multi-objective, non-scalar accounts of biological motivation. For the last one, the absence of a formal theory of *agency* (Dogma 1), Mani explicitly argues that evolution is not enough and that we should look for an answer in thermodynamics and the physics of self-persistence.

Regarding the conceptual overlap in their work, Mani said: Dave's three dogmas provided a scaffolding, and these evolutionary ideas just fell into place.

- Paper: [Illuminating the Three Dogmas of Reinforcement Learning under Evolutionary Light](https://arxiv.org/abs/2507.11482){:target="_blank" rel="noopener"}
- Presenter: Mani Hamidi (University of Tübingen)

## Table of Contents

- [Background: Mani's path to this paper](#background-manis-path-to-this-paper)
- [The key distinction: selectionist vs. instructional learning](#the-key-distinction-selectionist-vs-instructional-learning)
- [Dogma 2: Adaptation through open-ended novelty search](#dogma-2-adaptation-through-open-ended-novelty-search)
- [Dogma 3: Multi-objective goals and the origins of reward](#dogma-3-multi-objective-goals-and-the-origins-of-reward)
- [Dogma 1: Toward a theory of agency via thermodynamics](#dogma-1-toward-a-theory-of-agency-via-thermodynamics)
- [The Mani–Dave exchange: where do goals come from?](#the-manidave-exchange-where-do-goals-come-from)
- [Darwinian neurodynamics: evolution inside the brain](#darwinian-neurodynamics-evolution-inside-the-brain)
- [Broader implications: adaptation remains the missing piece](#broader-implications-adaptation-remains-the-missing-piece)

---

## Background: Mani's path to this paper

We opened with a fireside-style Q&A about Mani's background. As is typical for interdisciplinary folks, his trajectory has been quite nonlinear: biophysics and math undergrad at UBC, a master's in genome science, a stint in the biotech industry doing antibody discovery, and now a PhD in Tübingen. The through line, he explained, was a fascination with the question *"what is life?"*, catalyzed by Schrödinger's book as an undergrad and later deepened by a talk he attended by Terrence Deacon (his co-author on this paper) at SFU in Vancouver.

Deacon's book *Incomplete Nature* was formative. Mani described it as tackling the is-versus-ought problem by working up from the origins of life, while carefully avoiding two traps: the *homuncular* trap (invoking some unexplained vital force) and the *golem* trap (dismissing agency and consciousness as mere epiphenomena with nothing to explain). After traveling the world, re-reading the book on the road, and writing a PhD proposal he sent to Deacon, Mani eventually spent time at Berkeley, including visits to the Redwood Center, to which he offered a warm tribute.

When Mani saw Dave Abel's Three Dogmas paper, everything clicked: the three dogmas provided the organizational structure he'd been searching for to package a set of disparate evolutionary ideas he'd been developing for years. He wrote the paper in about 2--3 weeks before a workshop deadline, and, to his amazement, noticed that the word "evolution" appeared *nowhere* in Dave's original paper, despite adaptation being its central alternative to terminal search.

I (Hadi) flagged one theme from Mani's background that I think deserves more attention: the coupling of metabolism and information processing in biological systems, and its decoupling in AI. A transformer processes every token with equal computational cost, with no sense of energetic value attached to computation. This is one of the biggest missing pieces in today's AI, and it came up repeatedly throughout the session.

## The key distinction: selectionist vs. instructional learning

Mani's central thesis is that there are two fundamentally different models of learning. Drawing on a distinction from evolutionary biology:

**The instructional model** is what we typically think of as learning: supervised, RL, even most unsupervised methods. There's a target, there's an error signal, and the system molds itself toward the objective, like a smart mattress conforming to the sleeper. The key feature: a signal (gradient, reward) propagates back to the learner, instructing it how to change.

**The selectionist model** is evolution's approach. A population of variants is generated, some happen to exhibit *fittedness* (a property that lets them persist and proliferate), which are then selected. Importantly, the generation of variants is *not* directed by the selection criterion. It's non-teleological. You don't need to know what's good in advance; you just need to produce enough diversity that something good shows up.

**Eli Sennesh** immediately asked whether the selectionist model could be understood as constrained maximum entropy: randomly varying in all dimensions that still pass the selection test. Mani agreed this captures something essential, and noted it foreshadows the open-endedness ideas he'd develop next.

**Keir Havel** raised whether GANs, where the criterion itself evolves, sit closer to the selectionist model. Mani argued that GANs still fall under the instructional regime: both discriminator and generator optimize explicit objectives via gradient updates. The coevolutionary flavor is real, but the open-endedness is missing. [*Keir also shared a paper in the chat on the dynamics of interacting agents whose "optimization-like" individual behavior produces non-optimization-like collective dynamics ([Balduzzi et al., 2018](https://arxiv.org/abs/1802.05642){:target="_blank" rel="noopener"}), noting that the lead author was originally involved in formulating the IIT consciousness theory before switching gears.*]

**Zachary Laborde** asked whether the key distinction is simply that the target is static in the selectionist model versus dynamic and responsive in the instructional one. Mani clarified that the dynamic target is part of the story (captured by coevolution), but the deeper distinction is about the *non-objective* nature of variation generation: evolution doesn't hill-climb toward anything. It *satisfices*.

This brings us to Herbert Simon's famous quote, which Mani returned to multiple times throughout the talk:

> ...organisms adapt well enough to *"satisfice"*; they do not, in general, *"optimize"*.
> --- [Herbert Simon (1956)](https://pages.ucsd.edu/~mckenzie/Simon1956PsychReview.pdf){:target="_blank" rel="noopener"}, Rational choice and the structure of the environment

For living organisms, satisficing (satisfying enough to suffice) is the operating principle, not maximization.

## Dogma 2: Adaptation through open-ended novelty search

Mani started with the second dogma (learning as terminal search) because it's where evolution has the most to say. Dave's paper proposed *adaptation* as the alternative to terminal search, but left the concept underdeveloped.

Mani approaches adaptation by drawing from the body of work on **open-ended novelty search** by Ken Stanley, Joel Lehman, Jeff Clune, and others, spanning roughly two decades. This gives adaptation concrete algorithmic form.

Mani distilled three mechanisms from this literature that together make an evolutionary process open-ended:

### 1. Speciation / Niching

The key idea, captured by a quote Mani kept returning to: *"Grass does not preclude grasshoppers, nor do bacteria compete directly with bears. Competition is restricted and often localized within the niche."* Evolution produces *diversity*, not a single optimum.

Algorithmically, this means organizing solutions across a grid of behavioral or structural features (an "archive"), and ensuring that organisms breaking into a *previously unoccupied* niche face little or no selective pressure. Within a niche, fitness optimization can proceed. But *across* niches, the dynamic is divergent: the system expands outward into new territory rather than converging to a point.

Mani visualized this as a contrast between **convergent** and **divergent** dynamics. Standard optimization is convergent: a potential function, gradient descent, stable steady states. Open-ended evolution is divergent: the gradients point *away* from any given point. The system is constantly generating new possibilities.

I asked Mani how this squares with the **replicator equation** from evolutionary game theory, which *can* be represented as gradient descent on a KL divergence and has a convergent attractor (the evolutionary stable strategy). Mani's answer: both perspectives coexist. Fitness optimization within a niche is real and gradient-like. The contribution of open-ended novelty search is acknowledging the *other* engine, the divergent, diversity-generating one, that our optimization-centric lens tends to overshadow. The **quality-diversity** algorithms (like MAP-Elites) capture both: quality (fitness within a niche) and diversity (expansion across niches).

[*MAP-Elites is the algorithm underlying Google DeepMind's [AlphaEvolve](https://deepmind.google/discover/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/){:target="_blank" rel="noopener"}; additionally, [Sakana AI](https://sakana.ai/){:target="_blank" rel="noopener"} has built its research program around taking evolutionary algorithms seriously for AI development. This shows that search-based ideas are gaining real traction in industry.*]

### 2. Coevolution

The second mechanism is coevolution: both the agent and the environment co-evolve. Mani highlighted the **POET** algorithm (Paired Open-Ended Trailblazer), where the environment itself has a "genome" that evolves alongside the agent. As the agent solves simpler problems, the environment evolves into harder ones, forming a self-progressing curriculum. This produces both surprising diversity *and* fitter agents, even by standard objective-driven metrics.

### 3. Minimal criterion

The third mechanism replaces fitness comparison entirely. In minimal criterion strategies, there is no fitness function. Individuals only need to satisfy a simple binary threshold to propagate their lineage. As long as the entity meets the bare minimum for duplication, it survives, and anything beyond that threshold goes unexplored. This maximizes diversity generation by removing the convergent pressure of fitness ranking.

Mani then offered a dynamical-systems framing he came up with the night before the talk: convergent optimization corresponds to systems attracted to equilibrium fixed points. Open-ended evolution, by contrast, resembles dissipative systems that are *constantly driven away from equilibrium*, a connection to the thermodynamic ideas he'd return to under Dogma 1.

## Dogma 3: Multi-objective goals and the origins of reward

For the reward hypothesis, Mani focused on two threads: the distinction between **objective** and **non-objective** goals, and the **multi-objective** nature of biological motivation.

On the first: the open-ended novelty search literature, particularly Stanley's *Why Greatness Cannot Be Planned: The Myth of the Objective*, provides a vocabulary for goals that aren't objectives in the optimization sense. Non-objective search is *not* random search; it uses structured mechanisms (niching, coevolution, minimal criteria) to explore productively. But it lacks a predetermined target.

Mani argued that this challenges the first interpretive "door" in the [Bowling et al. formalization of the reward hypothesis](https://proceedings.mlr.press/v202/bowling23a.html){:target="_blank" rel="noopener"}: the assumption that goals can be expressed as a preference relation over outcomes. In an open-ended evolutionary process, the coexistence of grass and grasshoppers implies *no* complete preference ordering, so the completeness axiom fails.

On the multi-objective thread, Mani cited both computational work (Dahlberg's work on vector-valued reward signals) and the **homeostatic** or **drive** theories of motivation from psychology and neuroscience. A quote from Summerfield captured the point: most RL models assume value is unidimensional, which seems incongruous given that animals must jointly satisfy many constraints: satiety, hydration, warmth, social capital.

Mani also highlighted recent neuroscience questioning the hypothesis that dopamine conveys a scalar, homogeneous signal, citing work by Rachel Lee and colleagues. I added that there's a heavy debate in neuroscience about whether dopamine neurons represent reward at all in some brain regions: careful measurements of mouse kinematics reveal dopamine populations that track movement, not reward.

### Where do rewards come from?

All of this leads to what Mani considers the deepest question: **where does reward originate?** He traced a chain of deferrals: homeostatic RL papers ground reward in physiological set points, but when asked where those set points come from, they defer to evolution. And evolution itself, at least in these accounts, is invoked as an unexplained explanatory black box. A paper by Keramiti and Gutkin makes the circularity explicit: theories of conditioning rest on the argument that animals seek reward, while reward is defined as what animals seek. 

Summerfield frames this as "the reward paradox": RL offers computational tools for understanding behavior, but it's unclear who designs the reward function against which behavior is optimized.

Mani's argument: if we're going to defer to evolution as the source of reward, then we owe ourselves a richer account of what evolution actually is, beyond the caricature of random mutation plus natural selection.

## Dogma 1: Toward a theory of agency via thermodynamics

The first dogma, the absence of a formal theory of agency, is where Mani spent the least time, partly due to the breadth of the topic and partly by his own admission of limited technical depth in far-from-equilibrium statistical mechanics. But the sketch he offered connects the other two dogmas.

The argument: if agency requires open-ended evolutionary adaptation, and if the origins of instrumental goals are deferred to evolution, then a theory of agency requires grounding evolution itself in something more fundamental. Mani pointed to **thermodynamics** and the **origins of life** literature as the right place to look.

He cited Jeremy England's work (*Physics of Adaptation*), which uses Jarzynski equalities from non-equilibrium thermodynamics to connect self-replication ability with energy dissipation. He also discussed the deep relationship between metabolism and information, noting that ATP, life's main energy currency, is literally one of the nucleotides (the "A" in ATGC) used in DNA. Whether this is a coincidence of Earth's particular biochemistry or a deeper design principle is an open question that Mani finds compelling.

I offered two connections to foreshadow the next talk in this mini-series. First, one way to define an agent is by comparing it to inanimate matter: agents have more *empowerment* (more control over their futures) and are driven further from thermodynamic equilibrium. Whether there's a formal link between empowerment and distance-from-equilibrium is an open question worth pursuing. Second, there are formal results (Crooks' fluctuation theorem) connecting inference (going from prior to posterior beliefs) with thermodynamic work, which suggests that adaptation to the statistics of the environment has literal energetic costs.

**Keir Havel** pointed Mani to work on **semantic information** by Kolchinsky, which extends Shannon information to capture something about preserving identity over time. (A frog in a blender has more Shannon entropy than a living frog, which can't be right.) [*Keir shared the paper in the chat: [Kolchinsky & Wolpert (2018)](https://royalsocietypublishing.org/rsfs/article/8/6/20180041/64255/Semantic-information-autonomous-agency-and-non?guestAccessKey=){:target="_blank" rel="noopener"}.*]

## The Mani–Dave exchange: where do goals come from?

**David Abel** joined partway through the session and immediately engaged with the reward discussion. His first question drew a careful distinction between two different things: the **breadcrumbs** (signals that incentivize learning in a complex world, which could be scalar or multi-dimensional) and the **account of what a goal is** (maximizing a scalar? achieving a point on a Pareto frontier?). These are logically independent: you could give scalar breadcrumbs to find a Pareto-optimal point, or multi-criteria breadcrumbs toward a scalar goal. Which was Mani most interested in?

Mani's answer introduced a distinction that structured the rest of their exchange: **instrumental** versus **terminal** goals. Instrumental goals are the breadcrumbs, the physiological drives (hydration, satiety, warmth) that homeostatic RL models capture well with convergent optimization. Terminal goals are the deeper question: the source of those drives, the reason evolution produces goal-seeking agents in the first place. And the non-objective, divergent, open-ended novelty generation of evolution is what Mani considers the origin of terminal goals, even though calling it a "goal" feels strained, since the whole point is that it lacks teleological direction.

Dave pushed further: even if we move away from rewards, we're still left with the question of where goals come from. Is the move in open-endedness a rejection of writing down goals at all (in the spirit of *The Myth of the Objective*)? Or is it a mechanistic account, like satisficing, that still begs the question of where the threshold comes from?

Mani's reply was candid: yes, we're deferring to terminal goals as the ultimate origin, and yes, evolution is being asked to carry the explanatory weight. But the problem with most invocations of evolution in the RL literature is that they use it as a homunculus, as if saying "evolution did it" constitutes an explanation. Mani's point is that evolution *doesn't come for free*. It requires specific mechanisms (niching, coevolution, minimal criteria), and understanding those mechanisms yields real insight, not hand-waving.

Dave then mentioned **Les Valiant's work on evolvability**, a computational learning theory approach (from the creator of PAC learning) that asks what makes evolution computationally powerful enough to search through organism space more effectively than random search . [*Dave shared the paper in the chat: [Valiant (2009)](https://dl.acm.org/doi/pdf/10.1145/1462153.1462156){:target="_blank" rel="noopener"}.*] Mani was enthusiastic about this pointer, and connected it to the related concept of **evo-devo** (evolutionary developmental biology) and the mechanisms for producing *evolvable* variation that inspired Ken Stanley's early work on HyperNEAT architectures.

## Darwinian neurodynamics: evolution inside the brain

One of Mani's most provocative claims is that evolution can operate *within a single lifetime*, not just across generations. The first and most concrete example: the **adaptive immune system**, which performs an evolutionary process to generate antibodies against novel antigens that neither you nor your ancestors have ever encountered. This was, in fact, the insight that led Nobel laureate Gerald Edelman to propose **Neural Darwinism**: if evolution can happen within the body (in the immune system), perhaps it happens in the brain too.

Edelman's original Neural Darwinism fell out of favor, partly because it required prolific birth and death of neurons, which turned out to be mostly false. But **Eörs Szathmáry** and colleagues revived the idea under the name **Darwinian Neurodynamics**, sidestepping the physiological requirements. In their model, the units of selection aren't cells but *dynamical patterns*, temporal activity motifs generated by networks of neurons. These patterns can be duplicated across neural populations (via known plasticity mechanisms), mutated, and selected. Szathmáry's implementation uses a grid of reservoir computers (randomly initialized RNNs) whose readout neurons produce temporal patterns that can be copied across the grid via established synaptic plasticity rules.

[*The paper also cites [Dragoi (2023)](https://www.nature.com/articles/s41583-023-00763-0){:target="_blank" rel="noopener"}, which draws an analogy between hippocampal anticipatory neural dynamics (where the brain pre-generates sequences of neural activity patterns before the animal encounters a novel environment) and the anticipatory antibody production of the adaptive immune system. This parallel between neural "preplay" and immune anticipation is, I think, one of the more striking examples of the selectionist model operating at within-lifetime timescales.*]

Mani quoted Neil Bramley, a cognitive scientist: "When it comes to individual higher-level cognition, we habitually think of minds as doing something far cleverer... Minds are thought to encode a hierarchical causal generative model of their environment. The generative model framework also seems to capture an important sense in which the mind seems set up to produce stochastic variation and novelty of the sort that could allow for evolutionary mechanisms".

And then Mani went further than his paper, voicing what he called a "radical hypothesis" that he was "afraid to say out loud": that evolutionary selection mechanisms can operate within the brain, and moreover that something akin to the *origin of life*, the bootstrapping of an evolutionary process from non-evolutionary substrates, might occur in neural tissue during a lifetime. Not literally the origin of organic life, but the same kind of thermodynamic dynamics: Darwin's "warm pond," but for neural activity patterns that self-replicate and undergo selection.

**Audience contributions:** Before we wrap up, I just want to highlight some of the many interesting points raised by our active audience.

**Alec Segal** mentioned the paradigm of diffusion as a third model alongside selection and instruction, a drift process operating in both directions simultaneously, with concurrent creation and destruction. He also mentioned **GFlowNets** as an approach to diversity via amortized search (maximizing the probability of reward rather than maximizing reward itself) [*from the chat*], and later flagged the concept of **epliplexity**: information accounting for a limited computational resource, since in Shannon's sense computation produces no information [*from the chat*]. **Leonhard Piff** observed in the chat that heredity can be understood as passing selection information into the generating distribution in a structured way, a crisp reformulation of the selectionist model. **Zachary Laborde** noted connections to the viability research program [*from the chat*].


## Broader implications: adaptation remains the missing piece

### Taking evolution seriously

This talk made me (Hadi) take evolutionary algorithms seriously in a way I hadn't before. The ones that don't just optimize a fitness function, but *smartly generate diversity in anticipation*, letting selection sort out what works. I was surprised to learn from the paper (and hear confirmed in Mani's presentation) that you can apply this way of thinking to shorter timescales, within the learning of a single organism. The analogy between hippocampal anticipatory neural dynamics and immune system antibody production (via [Dragoi (2023)](https://www.nature.com/articles/s41583-023-00763-0){:target="_blank" rel="noopener"}) will stick with me.

A recurring theme in this mini-series has been the search for precise definitions. Dave's talk last week argued that RL suffers from imprecise definitions of *agent*, *learning*, and *reward*, just as physics once suffered from imprecise definitions of *force* and *heat*. What Mani's talk added is that **adaptation** is just as much in need of precise definition as **agent**, and that perhaps you can't define one without the other. An agent, in Mani's framing, is an entity capable of open-ended evolutionary adaptation. And adaptation, understood properly, goes beyond gradient descent on a fitness landscape: it's the conjunction of fitness optimization *and* non-objective diversity generation, grounded ultimately in the thermodynamics of self-persistence.

This sets up the next talk in our RL mini-series. **David Abel** returns on **March 19** to present [Plasticity as the Mirror of Empowerment](https://openreview.net/forum?id=eOZFqyE9Ok){:target="_blank" rel="noopener"}, which formalizes adaptation in terms of an agent's capacity to be *influenced* by its experience (the "plasticity" part) and connects it to empowerment. If Mani's talk established that adaptation is the missing concept, Dave's next talk may be where it starts getting the formal treatment it deserves.

---

Watch the full meeting here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/GOYOkt-7yyQ?si=OQDZ4FIpq0o76aop" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
