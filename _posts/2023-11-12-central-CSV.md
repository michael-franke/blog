---
title: The "Central CSV" approach for planning data-rich projects
date: 2023-11-12
math: true
mermaid: true
categories: [productivity]
tags: [project planning, data analysis, writing]
---

I remember vividly my first experimental project that involved [preregistration](https://help.osf.io/article/145-preregistration).
It felt crippling, intensely difficult.
You have to plan in advance all the analyses that you will want to run on the data in what seems like a very far future (even if it was really just next week, when data collection was completed).
But after a first afternoon of pain, the positive results were only too obvious: preregistration gives you an *actual plan*, it forces you to be honest to yourself, to define your goals.
In a sense, only when you actually spell out the plan of action at the level of detail necessary for preregistration do you really have a clear plan of action; without, you only have vague ideas.

Having vague ideas can be just fine for most of us most of the time.
But if we are honest, working out vague ideas into concrete, communicable results is *always painful*.
When that working out happens before data collection, it is most often, actually, less time consuming than when this happens in hours of poking around and &ldquo;playing with the data&rdquo;.
Being playful with data can feel productive, can conjure images of adventurous explorers venturing into unknown territory, but &#x2026; it could be so much more efficient when there already is road map.

Preregistration (and more generally: concerns about robust methods and reproducibility) are sadly not particularly *en vogue* in all areas of science.
But even if a project is entirely exploratory, which it may be for very good reasons, there is added benefit (of clarity, directedness, productivity) for central planning.
In many data-heavy projects, a useful approach can be to plan around the &ldquo;central CSV&rdquo;.
So, let me here advocate the &ldquo;central CSV&rdquo; planning method.

The &ldquo;central CSV&rdquo; planning method essentially is this.
If your project involves a data collection phase and a subsequent data analysis phase, don&rsquo;t do this:

    plan data collection ->
    collect data ->
    explore data ->
    plan data analysis ->
    analyze

but do this:

    plan data collection & analysis ->
    collect ->
    analyze

When you do, focus your planning on the research questions you want to address.
This is where the &ldquo;Central CSV&rdquo; comes in.
Data collection results in, well, data.
This then needs to be analyzed.
The bottleneck is a point where all data is collected, but not yet analyzed.
The &ldquo;Central CSV&rdquo; approach plans everything through this bottleneck.
It defines the variables of interest (columns) and the types of measurements you ultimately need to address your research questions.
If you can, make sure the data is already [tidy](https://vita.had.co.nz/papers/tidy-data.pdf) before you collected a data point.
So, following the &ldquo;Central CSV&rdquo; approach you would formulate your research questions, then write out a data structure that has all the measurements you need to address them in exactly the format to address them most efficiently, and then plan the data collection from there.

Of course, depending on the nature of your research questions or data, the &ldquo;Central CSV&rdquo; need not be tabular data.
But most often it will.
So, the name &ldquo;Central CSV&rdquo; is probably fine.

The advantages in productivity that the &ldquo;central CSV&rdquo; method gives are:

-   **less hassle with data wrangling**, because you make sure that the data is structured in the right way from the start
-   **no regrets during analysis**, because you make sure that you have if you know what you want to address with the data you won&rsquo;t find out

Here are examples where the &ldquo;central CSV&rdquo; method can give structure and boost productivity:

-   experimental studies
-   simulations of evolutionary dynamics under different conditions
-   multi-agent learning simulations of emergent behavior
-   investigating the predictions of LLMs for a particular task
-   &#x2026;

