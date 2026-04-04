---
title: "The Affective Gradient Hypothesis (Amitai Shenhav)"
layout: single
tags: [RL, affect, motivation, goals, perception, interoception, agency, Pavlovian, decision-making]
categories: [2026, March]
---

Why did the chicken cross the road? Because it expected the other side would feel better.

...or at least that's what this week's speaker proposed. Amitai Shenhav (UC Berkeley) joined us in person for the fourth and final presentation in our March 2026 RL mini-series. Over the previous three weeks, we had identified what a theory of agency needs: precise definitions of agency itself ([Dave Abel's Three Dogmas]({% post_url 2026-03-05-threedogmasrl %}){:target="_blank" rel="noopener"}), a grounding in adaptation and evolution ([Mani Hamidi's response]({% post_url 2026-03-12-rldogmasevolution %}){:target="_blank" rel="noopener"}), and a formal vocabulary for an agent's capacity to control and be influenced ([Dave's plasticity-empowerment framework]({% post_url 2026-03-19-plasticityempowerment %}){:target="_blank" rel="noopener"}).

But one question was left hanging: where does *motivated behavior* come from? Dave's framework had empowerment and plasticity but no goals, no rewards, no reason to do one thing rather than another.

Amitai's work fills that gap. He claims that all motivated behavior, from avoiding predators to giving a talk to choosing sushi over tacos, is driven by a single quantity. Not goals. Not reward in the RL sense. *Affect*.

We do things because we anticipate they will make us feel better or prevent us from feeling worse. Goals, in this view, are not antecedents of action but emergent properties of affect optimization.

- Paper: [The Affective Gradient Hypothesis](https://www.cell.com/trends/cognitive-sciences/abstract/S1364-6613(24)00202-X){:target="_blank" rel="noopener"}
- Presenter: Amitai Shenhav (UC Berkeley)

The discussion was probing and sustained, and extended beyond the 2 hour meeting window. **Rosa Cao** asked whether affect has ground truth, whether this framework collapses into RL under a different name, and what it means for representations to be "explicit." **Eli Sennesh** pushed early on multi-objective optimization versus common currency, contributed a key amendment about affect lacking a pre-given optimum, and distinguished state prediction errors from reward prediction errors. **Mani Hamidi** asked about clinical implications for depression and anxiety, and connected the framework to affordance competition and evolutionary models. **Alec Segal** probed whether affect constitutes a separate learning system and whether feelings conditioned on prior experience can be wrong. **Dhruv Kumarjiguda** asked about the predator-prey simulation work from the ML side. I (**Hadi**, the organizer) focused on the perception-interoception parallel, the three-inference synthesis, and the connection back to the mini-series as a whole.

## Table of Contents

- [Three obstacles to solving motivated behavior](#three-obstacles-to-solving-motivated-behavior)
- [Affect as perception](#affect-as-perception)
- [The Affective Gradient Hypothesis](#the-affective-gradient-hypothesis)
- [Discussion I: Ground truth, prediction errors, and delusional optimism](#discussion-i-ground-truth-prediction-errors-and-delusional-optimism)
- [Discussion II: Clinical implications and the task redesign](#discussion-ii-clinical-implications-and-the-task-redesign)
- [Discussion III: RL, the singular agent, and the Pavlovian core](#discussion-iii-rl-the-singular-agent-and-the-pavlovian-core)
- [Synthesis: three inferences and the chicken, revisited](#synthesis-three-inferences-and-the-chicken-revisited)
- [Closing the loop on the mini-series](#closing-the-loop-on-the-mini-series)
- [Appendix A: Psychiatric disorders as disorders of affective perception](#appendix-a-psychiatric-disorders-as-disorders-of-affective-perception)
- [Appendix B: Delusional optimism and the unbearability of accurate inference](#appendix-b-delusional-optimism-and-the-unbearability-of-accurate-inference)

---

## Three obstacles to solving motivated behavior

Amitai opened with his lab's background in value-based decision-making and cognitive control, but quickly shifted to the motivating problem: their models work well for constrained lab tasks, but when you try to generalize to real-world behavior (having a conversation, driving while adjusting the radio and talking to your kid in the back seat), the models don't just need *scaling*. They hit fundamental obstacles.

He laid out several provocative claims up front: there is most likely only one objective function (not multiple), the brain may not represent goals explicitly, RL is probably overrated as a guide to real-world behavior, and people effectively do what they want, where "what they want" means what their Pavlovian system wants.

**Eli** jumped in immediately to ask what arguments rule out multi-objective optimization. Amitai's answer: what he's proposing is, in a sense, multi-objective (there can be many values, like valuing wine along certain dimensions and food along others), but there is a single *value code* common across them. You can't have fundamentally separate objective functions (utility, information, free energy, empowerment) running in parallel without either a homunculus to arbitrate between them or a set of criteria that are very hard to meet.

**Obstacle 1: The goal problem.** We take goals for granted as central to action selection, but we have no account of where they come from. Amitai talked to experts in goal-directed behavior across multiple fields, and to a person, they gave the same answer: we don't know how goals get selected. The reason we've been able to avoid this problem is sociological: in lab tasks, the experimenter constrains the goal and the reward function, so the model doesn't need to explain goal selection. But in any real-world example (Amitai used the example of giving a talk, with its layered sub-goals like "don't say anything stupid," "stay on time," "make eye contact," plus physiological drives like hunger, plus exogenous interruptions like someone sneezing), the question of which goal drives behavior at any moment becomes unanswerable.

I (Hadi) asked whether a recurrent circuit with learned attractor dynamics could solve this without a homunculus. Amitai's response: that's a value-free, policy-based solution that assumes you've pre-compiled every possible environment-goal configuration. It might work in Atari, but he's skeptical it can handle real-world behavior, for the same reason he's skeptical that habits cover as much of daily life as we assume. Even brushing your teeth involves concurrent goals and interruptions that seem far-fetched to have pre-compiled.

He went further: if you are interested in reinforcement learning, decision-making, or higher-level cognition, and you are not thinking about how to solve this goal problem, you are committing "malpractice as a theoretician." It's like studying visual processes without thinking about how light enters the brain.

**Obstacle 2: The value problem.** From Plato onward, theories of value have posited two streams: a "hot" (affective, reflexive) value system and a "cold" (non-hedonic, instrumental) value system. The problem is that if you have two value systems, something needs to arbitrate between them, and that something is another homunculus. **Eli** asked whether this hot/cold distinction is descriptive or an artifact of separate experimental traditions. Amitai was sympathetic to the suspicion that these were artificially separated, and noted that this was close to what he planned to argue: there is only one value system, and it's the hot one.

**Obstacle 3: The affect problem.** Most people hear "affect" and think of something charged, prolonged, categorical (the six basic emotions from *Inside Out*), and unitary ("how happy do you feel right now?"). Each of these assumptions is wrong, or at least unhelpfully narrow. Amitai's solution is to reconceive affect as something much more general and perceptual in nature.

## Affect as perception

This was the section of the talk I (Hadi) found most striking, and where Amitai and I went back and forth extensively.

Amitai proposed that affect can be understood as a feature of perception, sitting at an intermediate level between raw sensation and discrete categorizable emotion. He drew a direct parallel to visual processing. In vision, low-level processing extracts edges, mid-level processing assembles surfaces (the first stage at which conscious access becomes possible), and high-level processing assigns semantic and conceptual labels. The same hierarchy applies to interoception: raw physiological signals from the body are processed, and affect emerges at the mid-level as a continuous quantity varying along at least a valence dimension (good to bad). Discrete emotions like anger, sadness, and joy arise at the higher level, shaped by social context and conceptual labels, much as object recognition in vision is shaped by learned categories.

On this view, affect is not episodic, not necessarily charged or aroused, and not unitary. It includes neutral states and small variations around them (which is most of what we experience throughout the day). It can co-occur for multiple objects and events simultaneously. And it is present whenever there is a percept: there is no perceptual state without an affective component.

**Eli** offered what Amitai accepted as a "friendly amendment": affect, unlike perception, has no pre-given optimum or reference point. In vision, there's ground truth sensory data. In motor control, there's an internally generated intention against which errors can be corrected. In affect, things can be better or worse, but there's no pre-given best. Amitai agreed, though he maintained the connection to perception is more than analogy; he plans to argue in a forthcoming theory paper that affect is a direct aspect of perception.

I then pushed the perception-interoception parallel further. If we take the best models of perception, which frame it as hierarchical inference over raw sensory measurements (photon counts → surfaces → objects → invariants), then the same framework should apply to interoception. The raw input is no longer photons but physiological signals: heart rate, blood glucose, temperature, gut motility. The brain performs inference over these signals, and as you go deeper, you get more abstract descriptions of the body's state, culminating in affect. Amitai agreed this was a productive starting point and noted there are anchors in the neuroscience literature (taste, smell, pain) where the translational coding from sensation to affect is partially understood. **Eli** added that anatomically, taste, smell, and nociception are interoceptive modalities, reinforcing the parallel.

> **Editorial note.** If affect is inference over interoceptive signals, then defects in peripheral physiological sensation could distort affective states, just as retinal abnormalities distort visual perception. There is accumulating evidence that this is exactly what happens in psychiatric disorders. See [Appendix A](#appendix-a-psychiatric-disorders-as-disorders-of-affective-perception) for a deeper exploration of this idea.

## The Affective Gradient Hypothesis

With goals removed from the driver's seat and value unified under affect, Amitai presented the core proposal. At any given moment, we represent potential future states and how they would feel. We also represent our affordances: the actions available to us that could increase or decrease our chances of ending up in those states. All that's needed is a system for dynamically adjusting behavior to approach better-feeling states and avoid worse-feeling ones. This is the Affective Gradient Hypothesis: behavior follows the gradient of anticipated affect.

Amitai emphasized that this is not so controversial when framed in Pavlovian terms. An animal avoiding a predator or approaching food is following an affective gradient, adjusting dynamically to the predator's location and the prey's position. Nobody would argue that what the animal feels about the threat or the food is irrelevant. The hypothesis is that *all* motivated behavior, including abstract human behavior like working on a deadline, maintaining a conversation, or choosing a career path, operates on the same principle. We don't need an intermediate step of goal selection. Actions coordinate around expected outcomes, and goals become an emergent property of this process.

He connected this to model predictive control (MPC), the technique used in self-driving cars. In MPC, you don't plan a long-horizon decision tree. Instead, you represent your immediate affordances, predict potential future states over a short horizon, estimate their value, rapidly optimize your actions based on the nearest snapshot, and then refresh. The AGH proposes something along these lines for the brain: not model-free RL (pre-compiled weights that won't generalize), not traditional model-based RL (long-horizon decision trees), but short-horizon reactive planning over affective predictions.

One particularly vivid concept was the **affective cliff**. Consider walking out of a talk mid-sentence. You don't normally entertain this thought, but if you did (say, because your phone buzzes), you'd immediately experience an intense negative affective signal: "no, this would be terrible." Amitai's postdoc Yvonne refers to these as affective cliffs, dormant counterfactuals that buffer ongoing behavior. You're not continuously planning to stay; you're just not hitting any affective cliff that would pull you away. Their lab has found these counterfactual representations play a larger role in sustaining behavior than is typically appreciated.

## Discussion I: Ground truth, prediction errors, and delusional optimism

**Rosa** raised a question that generated extended discussion: where are the affective features coming from, if there's no ground truth in the world for them to match? In vision, there's an external world to be right or wrong about. Can you be *wrong* about how you feel?

Amitai's answer: no, not about current experience. How something feels to you is your own readout, like how something tastes, and you can't be wrong about that. But you can be wrong about *which state you'll end up in*. This distinction, between **state prediction errors** and **affective prediction errors**, became a recurring theme.

I offered an example: the Dan Gilbert findings on lottery winners and paraplegics. People seem to be bad at predicting how they'll feel. But Amitai argued that if you actually describe to someone exactly what their daily life will be like in the new state, their affective predictions might not be so far off. The error is often in failing to consider which states they'll actually encounter (they forget they'll still have to get their kids ready for school on vacation), not in how those states would feel. He extended this to politics: if you had told certain voters exactly which policies would follow from their vote, their affective predictions about each individual policy might have been accurate. The error was in their belief about which states would materialize, not in how those states would feel.

**Eli** separated the two kinds of prediction errors cleanly: state prediction errors (I didn't expect *this* to happen) versus reward prediction errors (this happened and it feels different from what I expected). Both exist, but Amitai argued the former are more prevalent than we typically assume, and we're better at affective prediction than we give ourselves credit for, especially in concrete, short-horizon cases like conversations, where we rapidly estimate how the other person would feel if we said something and adjust accordingly.

> **Editorial note.** Rosa's question raises a disquieting possibility: if there's no ground truth for affect, maybe accurate affective inference would be existentially unbearable, and what keeps us going is positively biased self-delusion. See [Appendix B](#appendix-b-delusional-optimism-and-the-unbearability-of-accurate-inference) for a deeper exploration of this idea.

## Discussion II: Clinical implications and the task redesign

**Mani** asked about translational implications, particularly for depression. Amitai connected this to a broader reframing: if the AGH is right, then motivational impairment in depression is a question about *distorted outcome expectations and their associated affect*. What outcomes is the depressed person representing? How do they feel about those outcomes? And what are their perceived affordances?

This reframing extends to anxiety. Amitai and his lab have been investigating what they call **failure risk**: the extent to which people represent potential failure while performing a task, even when they've historically performed well. An anxious person might avoid effortful tasks not because the effort itself is too costly, but because they disproportionately represent the possibility of failure and how that failure would feel. The lab's recent data suggest this counterfactual failure representation is a significant driver of task avoidance.

Amitai also discussed his student Skyler's work, which asks people to list their goals for the coming day, then for each goal, list the expected outcomes and their valence, and separately, the outcomes of *not* completing that goal. What predicts which goals people pursue is not just the positive valence of doing them, but, even more so, the negative valence of not doing them. The negative counterfactual is a bigger driver than the positive prospect.

The AGH also reinterprets standard cognitive neuroscience constructs. If the brain doesn't explicitly represent goals, then what we've been calling "goal relevance," "error monitoring," and "goal-directedness" should be reinterpreted as anchored in expected outcome representations. An error signal is not "I deviated from my goal" but "I'm now representing the consequences of that deviation and how they feel." Relevance is not "this stimulus matches my goal" but "this stimulus is connected to a predicted outcome with significant affective weight."

## Discussion III: RL, the singular agent, and the Pavlovian core

**Rosa** asked the question that was on several people's minds: can't an RL person just say the goal is to maximize affect at every point, and call it a day?

Amitai's answer was carefully layered. In one sense, yes: if you're committed to a single value function, this framework is not a radical departure. But in another sense, the differences are real. Standard RL, as typically practiced, assumes fixed goals and pre-compiled action-value functions. To apply RL to real-world behavior, you'd need to know in advance all possible valued actions, which Amitai called the **problem of omniscience**. The AGH avoids this by localizing the optimization: you don't need a global action-value map, you just need to represent a few predicted outcomes and their affective valence and then optimize locally. Rosa pushed back: don't you have an analogous omniscience problem for outcomes? No, Amitai replied, because you only need to work with what perception gives you. You're optimizing over whatever states are currently available to you, not over a global landscape.

A testable prediction follows: the same outcome representation should drive both Pavlovian (reflexive) and goal-directed (deliberative) behavior, contra the standard assumption of separate representational streams. The notion of intrapersonal conflict ("should" vs. "want," System 1 vs. System 2) also simplifies: there aren't separate agents inside you, just competing affective associations that vary in their strength, and whatever "wins" determines behavior. Self-regulation failure is not a cognitive system losing to an emotional system, but one affective association outweighing another.

**Dhruv** asked about the predator-prey simulation work from the ML perspective. Amitai described an attractor landscape defined by agents in the environment: as prey and predators change in affective salience, they reshape the landscape, and the agent optimizes its position within it at each moment. At a high level, you could describe this as "the agent's goal changed from X to Y," but that goal-talk is post-hoc: what's actually happening is that the affective gradients are shifting and the agent is following them.

Rosa closed with a comment that captured something important: "I have to say, this thing really tracks my internal experience of my psychology of decision-making much better than most decision-making talks, where it feels like it's highly idealized, and I definitely don't work like that."

## Synthesis: three inferences and the chicken, revisited

Toward the end of the session, I (Hadi) offered a synthesis of the framework as I understood it. The AGH, as I see it, reduces to three inference problems:

1. **State inference.** What is out there? Given my observations, what is the state of the world? This is the standard perceptual inference problem: P(state \| observations).

2. **Affordance inference.** What can I do? Given the inferred state, what actions are available, and what outcomes would they produce? This gives a distribution over possible outcomes conditioned on states and actions: P(outcomes \| state, actions).

3. **Affective inference.** How would each outcome feel? Given the possible outcomes, what affect is associated with each? This is the interoceptive/evaluative inference: P(affect \| outcomes).

Once you have these three pieces of subjective information, action follows: you act to move along the affective gradient, toward states that feel better and away from states that feel worse.

Amitai accepted this synthesis with one refinement: you don't necessarily need to infer a full landscape. Individual outcomes can locally tug at actions without requiring a globally computed map. Some outcomes will be in competition, others will be unrelated (you can have a conversation while drinking coffee). And the inference may be automatic, in the same way we infer the brightness of something, rather than requiring an extra deliberative layer. I agreed: unconscious inference. Bayesian inference without a committee meeting.

Now return to the chicken. The chicken is standing on one side of the road. It infers the state of the road (cars, weather, distance). It represents its affordances (walk, run, stay). It simulates the possible outcomes and infers the affect associated with each: the other side has food, this side has an approaching fox. The affective gradient points across the road. It crosses.

The joke is now substantiated. The chicken is performing affective gradient descent.

> *"Man can do what he wills but he cannot will what he wills."*
> --- Arthur Schopenhauer, [*On the Freedom of the Will* (1839)](https://archive.org/details/twofundamentalpr0000scho){:target="_blank" rel="noopener"}

Schopenhauer saw it two centuries ago. Perhaps what he called *Will* was *Affect* all along: not a mysterious metaphysical force, but a perceptual inference over the body's internal states, an inference that *precedes* and *generates* the experience of wanting. We don't choose what moves us. We are moved, and then we call it choice.

## Closing the loop on the mini-series

This was the fourth and final talk in the March 2026 RL mini-series, and I (Hadi) want to close by connecting the four talks into a single arc.

We started by asking: what is an agent? Four speakers gave four complementary answers, each adding a necessary piece.

**Dave Abel** (Talk 1, [Three Dogmas]({% post_url 2026-03-05-threedogmasrl %}){:target="_blank" rel="noopener"}) argued that the field needs precise definitions, and that three dogmas (environment spotlight, learning as task-solving, the reward hypothesis) are holding us back from formulating them. He offered a behaviorist starting point: define agents in terms of their measurable interactions with the environment.

**Mani Hamidi** (Talk 2, [Evolutionary Response]({% post_url 2026-03-12-rldogmasevolution %}){:target="_blank" rel="noopener"}) argued that agency cannot be understood without evolution and thermodynamics. Agents are far-from-equilibrium, driven-dissipative systems. Adaptation is not just learning from data but a multi-scale process ranging from evolutionary timescales to moment-to-moment neural dynamics.

**Dave Abel** (Talk 3, [Plasticity-Empowerment]({% post_url 2026-03-19-plasticityempowerment %}){:target="_blank" rel="noopener"}) delivered a concrete formalism. Using generalized directed information, he defined two measurable properties of agents: empowerment (influence over the environment) and plasticity (influence by the environment), and proved they are in tension. I argued that these behaviorist properties are mediated by a missing cognitive component: the agent's *internal world model*, which lets it simulate, predict, and plan.

**Amitai Shenhav** (Talk 4, today) argued that the mystery of motivated behavior dissolves if we can mathematically and mechanistically define *affect*. Goals are emergent, value is unified, and the engine that drives all behavior is the gradient of anticipated feeling.

Putting these together, we arrive at the beginnings of a composite answer to the question of what an agent is:

<div style="border: 2px solid; padding: 16px 20px; margin: 24px 0; border-radius: 4px;">

An agent is a <strong>far-from-equilibrium, driven-dissipative system</strong> that possesses <strong>empowerment</strong> (the capacity to influence its environment), <strong>plasticity</strong> (the capacity to be influenced by its environment), and an <strong>internal world model</strong> (the capacity to simulate, predict, and plan). These capacities are organized in service of <strong>maximizing affect</strong>: the agent acts to approach states it expects to feel better and avoid states it expects to feel worse. Goals, rewards, and plans are not inputs to this system but emergent properties of it.

</div>

This is, of course, a sketch, not a theorem. Each component needs its own formalization, and the interfaces between them are open problems (how does the quality of the world model bound achievable empowerment? how does affect shape the trajectory through the plasticity-empowerment simplex?). But after four talks, we have at least four candidate primitives, each with some mathematical grounding, and a direction for integration.

As we have emphasized throughout this series, fields mature when their central concepts become precise enough to analyze systematically. Newton did it for force. Shannon did it for information. "Agency" is not there yet. But it's closer than it was four weeks ago.

---

Watch the full meeting here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/PLACEHOLDER" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

## Appendix A: Psychiatric disorders as disorders of affective perception

*Editorial by Hadi Vafaii.*

This perception-interoception parallel has implications that go well beyond Amitai's talk, and I want to highlight one of them. If affect is inference over interoceptive signals, then defects in peripheral physiological sensation could distort affective and emotional states, just as defects in retinal processing distort visual perception. There is accumulating evidence that this is exactly what happens in psychiatric disorders.

Consider sensory processing. A [2022 meta-analysis](https://pubmed.ncbi.nlm.nih.gov/35489177/){:target="_blank" rel="noopener"} across 33 studies found that individuals with a broad range of psychiatric conditions (schizophrenia, depression, anxiety, PTSD, bipolar disorder) show elevated sensory sensitivity, sensory avoidance, and reduced sensory seeking, with large to very large effect sizes. People with [bipolar disorder report dramatically altered perception](https://psychiatryonline.org/doi/10.1176/appi.ajp.2017.16121379){:target="_blank" rel="noopener"} across mood states: during mania, vision sharpens, hearing amplifies, and touch becomes hypersensitive; during depression, the same modalities dull.

The retina provides a particularly striking case. [The retina develops from the same tissue as the brain](https://pmc.ncbi.nlm.nih.gov/articles/PMC4559409/){:target="_blank" rel="noopener"} (neuroectoderm), and retinal changes may parallel or mirror the integrity of brain structure and function. Multiple studies have documented structural and functional retinal abnormalities in schizophrenia: retinal nerve fiber layer thinning, widened venules, abnormal electrical responses to light, and dopaminergic abnormalities. A [2025 study in *Nature Mental Health*](https://www.nature.com/articles/s44220-025-00414-6){:target="_blank" rel="noopener"} showed that increased *genetic* risk for schizophrenia is associated with thinner retinas even in individuals *without* a schizophrenia diagnosis, mediated by neuroinflammatory pathways. As many as 62 percent of adults with schizophrenia experience visual distortions involving form, motion, or color.

If the same kind of distortion happens on the interoceptive side, which is exactly what the perception-interoception parallel predicts, then psychiatric disorders may involve a fundamentally distorted affective readout of the body's state. The brain is running inference over noisy or degraded interoceptive signals, and the resulting affect is off. This reframes conditions like depression and anxiety as, at least in part, disorders of *affective perception*, not just disorders of "mood" or "cognition." It's the interoceptive analog of having bad glasses: the world you see (or feel) is not the world that's there.

## Appendix B: Delusional optimism and the unbearability of accurate inference

*Editorial by Hadi Vafaii.*

Rosa's question about ground truth touches something I find philosophically urgent, and that the conversation only partially addressed. If affect is the ultimate arbiter of behavior, and if there's no external ground truth for affect to be measured against, then the *accuracy* of affective inference becomes a question with no objective answer. And this opens a disquieting possibility: maybe accurate affective inference would be *unbearable*.

There is evidence for this. [Taylor and Brown (1988)](https://psycnet.apa.org/record/1988-16903-001){:target="_blank" rel="noopener"} argued, against the prevailing view in clinical psychology, that mental health is characterized not by accurate self-perception but by *positive illusions*: overly positive self-evaluations, exaggerated perceptions of control, and unrealistic optimism. These illusions promote the ability to care about others, to be happy, and to engage in productive work. Negative information gets isolated and reframed in the least threatening way possible. The psychologist Roy Baumeister later coined the term "optimal margin of illusion" ([covered by Rob Henderson](https://www.robkhenderson.com/p/the-optimal-margin-of-illusion){:target="_blank" rel="noopener"}) to describe the sweet spot: enough contact with reality to function, enough self-delusion to keep going.

If we were performing perfectly calibrated affective inference, attending to the full distribution of outcomes with accurate weights, we might find existence intolerably painful and uncertain. What keeps organisms going may be precisely a *positively biased* affective inference system: one that systematically overweights the good, underweights the bad, and filters negative information through rose-tinted priors. The Norwegian philosopher Peter Wessel Zapffe argued that human consciousness is itself a tragic overevolution, and that we survive only through mechanisms of self-deception. If the AGH is right that affect is the sole driver of behavior, then the *quality* of that affective inference, including its systematic biases, may be among the most consequential properties of any agent. Too accurate, and you stop. Too biased, and you walk off a cliff. The healthy brain sits somewhere in between, and mental illness may reflect perturbations of that balance in either direction.
