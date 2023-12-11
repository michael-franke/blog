---
title: "Wittgenstein says: ChatGPT does not speak English"
date: 2023-12-10
math: true
mermaid: true
categories: [NLP]
tags: [LLMs, philosophy]
---

Put on your philosopher&rsquo;s funny-hat and prepare for a wild goose chase from inverse reinforcement learning, via evolutionary explanations, the language modeling objective, and Wittgenstein&rsquo;s late philosophy to the final conclusion that ChatGPT does not speak English because it cannot shut up.
Don&rsquo;t worry, it will all make sense, or won&rsquo;t it?

![img](/mfpics/LW-playing.png)


# Reinforcement learning, inverse RL, and optimality-based explanations

In standard reinforcement learning, modellers fix a reward function and have the system evolve behavior that optimizes the (expected rewards).
Inverse reinforcement learning, in contrast, supplies examples of behavior and has the system infer a reward function that, if behavior is optimized under it, would match the observed.
This is superficially similar to evolutionary explanations of human behavior, or Anderson&rsquo;s [rational analysis](https://en.wikipedia.org/wiki/Rational_analysis#:~:text=Rational%20analysis%20is%20a%20theoretical,the%20structure%20of%20the%20mind.) approach in Cognitive Science, where we also seek to explain behavior in terms of a purpose it serves.
In linguistics, [functional explanations](https://plato.stanford.edu/entries/linguistics/) seek to show how particular features of language are adaptations for a particular goal, such as to [maximize discriminability](https://philpapers.org/rec/DEBTOO-3) (e.g., in the vowel space), or to [efficiently communicate about a specific semantic domain](https://www.pnas.org/doi/full/10.1073/pnas.0610341104).
The centerpiece of such explanations are, essentially, postulated reward functions that human behavior has evolved to optimize.
Whence the parallel to inverses RL, only that in inverse RL the agent tries to find the reward function, whereas in optimality-based explanations the researchers come up with it.


# Language modeling as reward

Large language models mimic human language astonishingly well, despite the fact that they are first and foremost trained on the **language modeling objective**, which is to maximize the probability of the next word or token.
Later stages of fine-tuning move the system away from the pure LM-objective, but let&rsquo;s put that aside for a moment to consider a crazy question that may give interesting insights after all: what if the LM-objective was the reward function that explains how humans developed language? - Anyone? What would we expect to find?

Nothing!
If agents&rsquo; goal was to optimize the LM-objective, the behavior that optimizes both this reward function and a secondary, but natural criterion of efficiency is to say nothing.
Absolutely nothing at all.
Or just one word.
The same.
Over and over again.

So, totally silly question, or maybe a bit insightful after all?
I&rsquo;d say we can glimpse from this why we intuit that [LLMs are &ldquo;stochastic parrots&rdquo;](https://dl.acm.org/doi/pdf/10.1145/3442188.3445922) and that [LLMs may have mastered formal competence, but seem to lack functional competence](https://arxiv.org/abs/2301.06627).
The language modeling objective provides no incentive to use language to achieve any goals.
LM-modeling agents do not share information, make promises and don&rsquo;t greet one another even if they produce that string &ldquo;hi!&rdquo;

Would anything change if we also consider fine-tuning a foundation LLM with subsequent reinforcement learning, which modulates the output to be more helpful (and less toxic, &#x2026;)?
Yes, but only a bit.
Silence would not be the optimal solution in a society of agents optimizing this conjoined objective anymore.
But **there is much more to human language use than being a helpful assistant**.
The richness and diversity of human purposes behind our flapping lips, hands, pens and keystrokes is not even approximately met.
(There are many language games, of which being a helpful assistant is just one, in our human forms of life; see below.)


# Language games and forms of life

There is a sense in which LLMs, despite all their formal competence and despite additional fine-tuning, do not speak or know a language.
Yes, it is a wide sense of &ldquo;speaking or knowing a language&rdquo; and you may not like it.
But, by appeal to authority, this wide sense should perhaps not be immediately dismissed, because: Wittgenstein!

In his later work, the notion of **language game** was very important to Wittgenstein, because he wanted to show that the concept of meaning and proper linguistic behavior (possibly, including syntax) should be viewed in the context of our interactive practices.
We play many language games (informing, role-playing, debating, &#x2026;) and language emerges as the pivotal element to guide these conventionalized practices.
Our playing of multiple language games is what Wittgenstein refers to as a **form of life**, another key concept of his later writing.
In his *Philosophical Investigations* §23 we read:

>  Das Wort &ldquo;Sprachspiel&rdquo; soll hier hervorheben, dass das Sprechen der Sprache ein Teil ist einer Tätigkeit, oder einer Lebensform.
>
> The phrase &ldquo;language game&rdquo; is here supposed to highlight that speaking a language is part of a practice, or a form of life.


# ChatGPT doesn&rsquo;t speak English because it does not *not* speak

According to this view, we cannot disassociate speaking or knowing a language from engaging in the practices that render this language meaningful.
If we adopt this wide sense of &ldquo;speaking English&rdquo;, then we should require sufficient comfort with different language games.
Here the **lack of functional grounding in LLM productions** matters: it is hard to see whether LLMs like ChatGPT can engage in any kind of language game that involves making social commitments or establishing social relationships.
It cannot by design.
For better or worse.

But how do we know that the SOTA LLMs cannot do any of this?
They are probably able to produce fluent language suggesting that they reason about social commitments and relationships.
And any kind of non-linguistic action we would require the LLM to show as part of a language game is, well, simply unfair.
That ChatGPT cannot give me five apples with unicorn stickers when I want it to play shop-keeper and customer, is not something that we should hold against it.

This leaves us in a conundrum.
We claim that LLMs are lacking something, the ability to engage adequately in language-based interaction, but they are probably able to produce language *about* these practices and we cannot require them to take worldly actions to follow up on their promises.

But maybe there is a way.
To go back to early Wittgenstein, in particular the idea in the Tractatus that the limits of thought and language show in the edge cases of meaningfulness (tautologies and contradictories, *showing* but not *expressing* the logical structure or representations), maybe we need to seek the edge-cases of the effable, the border between the linguistic and the non-linguistic act, in order to show that LLMs fail to properly act non-linguistically where, in principle, they could have.
This borderline action, clearly, is saying nothing.
It&rsquo;s linguistic and it&rsquo;s not.
Obviously.

So, the ultimate test is whether an LLM can play this move &ldquo;silence&rdquo; at the appropriate moment in a simple language game, such as a request, which should be totally compatible with its role as helpful assistant.
But, unfortunately:

![img](/mfpics/ChatGPT-STFU.png)

I thought this story needed telling, because:

> Worüber das Ding nicht schweigen kann, darüber muss man sprechen.

