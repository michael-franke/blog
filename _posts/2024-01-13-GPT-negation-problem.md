---
title: "So much for understanding instructions: When removing X and Y removes everything but X and Y"
date: 2024-01-13
math: true
mermaid: true
categories: [NLP]
tags: [LLMs, GPT4v]
---

It is usually unhelpful to scream "wolf" on any occasion that state-of-the-art models make mistakes, but sometimes examples of extremely blatant failures are a reasonable corrective, alleviating over-confidence in modern AI's capabilities and human-likeness.
So, here's one of those blatant failures that just reminded me of where we currently are (roughly, pretty amazing for the most part, but creepy along the edges).

I wanted a minimalist logo of person, but I got one with a necktie (and some strange halo around the head), so I specifically asked for an ungendered figure.
I got this picture.

![img](/mfpics/2024-01-13-initial-picture.png)

So I repeated my request and gave, what I take to be, very clear instructions to remove the hat and the necktie, but:

![img](/mfpics/2024-01-13-updated-picture.png)

It is not new that LLMs have trouble with negation (["LMs are not naysayers"](https://ar5iv.labs.arxiv.org/html/2306.08189), [Negation Benchmark](https://aclanthology.org/2023.emnlp-main.531/) ), but this example in the context of text2img is really striking.
From the three features (hat, necktie and coat), the instruction to "Remove the hat and the necktie" resulted in removing the coat and keeping the other two, i.e., the did the exact opposite of what was asked.
This is not a simple neglect of a negation marker, but more of a failure to comprehend the meaning of "remove."
So much for actual language understanding here.

