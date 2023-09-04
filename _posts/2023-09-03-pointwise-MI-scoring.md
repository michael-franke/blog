---
title: Pointwise mutual information scoring has nothing to do with pointwise mutual information
date: 2023-09-03
math: true
mermaid: true
categories: [NLP, terminology]
tags: [information-theory, LLM, pedantry, ranting]
---

When testing the performance of Large Language Models (LLMs), a popular scoring function for multiple-choice options is referred to as "pointwise mutual information scoring" ("PMI scoring").
The definition of "PMI scoring" certainty *looks like* the notion of pointwise mutual information (PMI) from information theory, but, on closer look, it is actually totally misleading terminology.
While the formal notion of "PMI scoring" is probably useful in practice, it has nothing to do with PMI as we know it from information theory.

So, what? Why should we care? - 
Firstly, misleading terminology can lead to blatant factual errors in widely cited papers. 
"PMI scoring" is such a case, as shown below.
Secondly, if we want to avoid overselling results, we must start with careful nomenclature of the underlying formal notions.
In other words, we must avoid a certain **terminological garbage in, terminological garbage out**!
Finally, we should care for conceptual clarity because we can learn something about the models, ideas and notation involved. 
For "PMI scoring", confusion arises from misinterpreting a simple conditional probability expression like $P(y \mid x)$ in the context of LLMs. 

So, let's have a look at "PMI scoring" and why it is unrelated to PMI.

<!-- While it may or may not be the case that these conceptual mistakes do not matter when the goal is to find robust methods that increase performance on benchmarks, it is important to be conceptually precise and not use misleading terminology not only in reporting the results, but also in referring to the  -->


## Background: Scoring functions

Large Language Models (LLMs) produce fluent, seemingly meaningful text.
Much recent research investigates the extent to which LLMs manage to select the target answers in benchmark tests, or whether they show human-like performance in text-based experiments that resemble, or are identical to, experiments with human participants.
A simple experimental trial usually shows a context string $x$ (e.g., task instructions) and requires the model to choose between $k$ multiple choice options $y_1, \dots, y_k$, which are strings as well. 
To determine the LLM's prediction, we consult a **scoring function**, $\text{Score}(x, y_{i}) \in \mathbb{R}$, and define the model's choice as:

$$
\arg \max_i \text{Score}(x,y_i)\,.
$$

One obvious scoring function is plain conditional probability, $P_{\text{LLM}}(y_{i} \mid x)$, but a demonstrably better and widely used scoring function is **average next-word surprisal**:

$$
\text{Score}_{avg}(x,y) = \frac{1}{|y_i|} \log P_{\text{LLM}}(y_i \mid x)\,,
$$

where $\|y_i\|$ is the length (number of words/tokens) of option $y_i$, and 

$$
\log P_{\text{LLM}}(y_i \mid x) = \sum_{j=1}^{\|y_i\|} \log _{\text{LLM}}P(y_{i,j+1} \mid x, y_{i,1}, \dots, y_{i,j})
$$

is the sum of next-word surprisals, as generated from from an autoregressive LLM. 

Though relatively successful in practice, a problem with this notion is that it does not account for potential differences in  *a priori* probability of options. 
If $y_1$ is just a very awkward string with infrequent words and grammar, its score might be lower than that of $y_2$ even though, in terms of their semantics, $y_1$ should be the preferred option. 
Essentially, this would be a problem of experimental design, namely unbalanced material, but since we cannot always have perfectly manicured data, we might want a scoring function that compensates for these differences.

## "Pointwise mutual information" scoring

To address this problem "pointwise mutual information scoring" ("PMI scoring") is defined as follows:

$$
\text{Score}_{PMI}(x,y_i) = \log \frac{ P_{\text{LLM}}(y_i \mid x) } {P_{\text{LLM}}(y_i)}\,.
$$

Formally, this scoring function compensates for different *prior probabilities* of the different choice options.
In practice, this works quite well, apparently.

## Pointwise mutual information

The previous definition looks very much like information-theoretic PMI.
But there is a huge difference residing in how to interpret the conditional probability notation.
Let's unpack this, starting with a recap of what information-theoretic pointwise mutual information is.

Let $P$ be a joint probability distribution over product space  $X \times Y$, then the pointwise mutual information of a pair $x \in X$ and $y \in Y$ is defined as:

$$
\text{PMI}(x,y) = \log \frac{P(x,y)}{P(x) P(y)}\,,
$$

where $P(x)$ and $P(y)$ are the marginal distributions, as usual.
Intuitively, we can think of PMI as a measure of excess surprisal (negative log) of treating $x$ and $y$ as conditionally independent (therefore expecting them to occur with probability $P(x) P(y)$), instead of the actual joint probability $P(x,y)$.

Using Bayes rule, we can furthermore rewrite PMI using conditional probabilities:

$$
\text{PMI}(x,y) = \log \frac{P(x,y)}{P(x) P(y)} = \log \frac{P(y \mid x)}{P(y)} = \log \frac{P(x \mid y)}{P(x)} 
$$

By visual pattern matching, the expression $\log \frac{P(y \mid x)}{P(y)}$ looks exactly like the definition of "PMI scoring", which seems to justify its name.
But that's a huge mistake!

## Why "PMI scoring" is not PMI?

"PMI scoring" is different from PMI because the definition of "PMI scoring" implicitly refers to different events $y_{i}$ in the numerator and the denominator.
Concretely, $P_{\text{LLM}}(y_i \mid x)$ is the probability the LLM assigns to the event that the string $y_{i}$ occurs after $x$, while $P_{\text{LLM}}(y_i)$ is the probability of just generating $y_{i}$ without prior context.
The notation $y_{i}$, though seemingly the same in the conditional and unconditional probability, does not refer to the same event in a plausible joint probability space.
The actual PMI is 0 because the event of generating $y_{i}$ without prompt and the event of generating $y_{i}$ after some prompt are stochastically independent.
This is because these generations must come from different "runs of the LLM".

To make this more concrete, let's consider the simplest case in which $x=w_1$ and $y_i=w_2$ are single words, for example, "it" and "is".
Given any autoregressive LLM, we get the probability $P_{\text{LLM}}(x)$ of observing "it" as the first word in a sentence, and the probability $P_{\text{LLM}}(y_i \mid x)$ of observing "is" as the second word after "it."
From this, we can compute the joint probability of the sequence "it is", $P_{\text{LLM}}(x, y_i)$ as the product of $P_{\text{LLM}}(x)$ and $P_{\text{LLM}}(y_i \mid x)$.
So far, so good.

But what would it mean to write $P_{\text{LLM}}(x \mid y_{i})$?
This notation is ambiguous, and there are two possibilities. 
First, $P_{\text{LLM}}(x \mid y_{i})$ could mean the (usual, autoregressive) probability of generating "it" after having generated "is".
We would generated this probability by multiplication with a term which we would write as $P_{\text{LLM}}(y_{i})$ and interpret as the probability of generating $y_{i}$ as the first word in a sequence.
Second, $P_{\text{LLM}}(x \mid y_{i})$ could also mean the "backward probability", obtained by Bayes rule from the computations of the previous paragraph, of "it" being the first word, given that "is" is the second.

So, if we want to use Bayes rule like in the rewritten version of PMI, the $y_{i}$ must refer to the event that "is" is the second word.
It is in this sense that the definition of "PMI scoring" only looks like information-theoretic PMI.
The denominator should actually be interpreted as the event that $y_i$ occurs after $\|x\|$ tokens of text.

## What would be a better term than "PMI scoring"?

What "PMI scoring" tries to capture is the idea how much the probability of $y_{i}$ differs from two perspectives: (i) after having processed the prompt $x$, and (ii) without having processed the prompt $x$ (e.g., in a null context).
This is not a use-case for PMI but for notions of divergence between different probability distributions, like Kullback-Leibler divergence (aka. relative entropy).
So one less misleading name for PMI could be "**pointwise relative entropy**".

But this term is uncommon and may also create confusion.
Maybe a better way would be to think of it in terms of **surprisal reduction**.
We consider two different probability distributions (models, or model states):
$P_{\text{LLM}^{\emptyset}}(\cdot)$ is the probability distribution induced over strings by the LLM without any prompting, and 
$P_{\text{LLM}^{\mid x}}(\cdot)$ is the probability distribution over strings after processing context $x$.
We could then express the same notion as "PMI scoring" as surprisal reduction with clear notation as follows: 

$$
\begin{align*}
\text{Score}_{PMI}(x,y_i) & = \text{"surprisal of $y_{i}$ without $x$"} - \\
                              & \ \ \ \ \ \ \ \text{"surprisal of $y_{i}$ after processing $x$"} \\
& = - \log(P_{\text{LLM}^{\emptyset}}(y_{i})) + \log(P_{\text{LLM}^{\mid x}}(y_{i})) \\
& =  \log \frac{P_{\text{LLM}^{\mid x}}(y_{i}) } {P_{\text{LLM}^{\emptyset}}(y_{i})}
\end{align*}
$$

## Errors from misleading terminology and notation

Misleading terminology and ambiguous notation can lead to factual errors. 
For example, although information-theoretic PMI is "symmetric" because (for well-defined events on joint probability spaces):

$$
\log \frac{P(y \mid x)}{P(y)} = \log \frac{P(x \mid y)}{P(x)}\,,
$$

this is not the case for "PMI scoring" with its non-uniform interpretation of events (contrary to suggestions of Holtzman et al. (2021)).

## Conclusion

Probability notation is tricky and can lead to misleading conceptualizations of (otherwise useful!) notions.
These misleading conceptualizations can then lead to factual errors, which may in turn have negative effects for applications or the interpretation of results.
From the point of view of good scientific practice, using precise and careful wording for theoretical notions is also important to safeguard against (intentional or unintentional) overselling of results.
