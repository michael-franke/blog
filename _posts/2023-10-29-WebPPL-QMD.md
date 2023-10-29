---
title: Including WebPPL in Quarto-generated HTML documents
date: 2023-10-29
math: true
mermaid: true
categories: [technical]
tags: [quarto, markdown, writing]
---

This post describes how to integrate executable WebPPL code boxes into HTML documents, generated with Quarto.


# What's WebPPL?

[WebPPL](http://webppl.org/) is a light-weight probabilistic programming language, which is [built on top of Javascript](http://dippl.org/).
It is great for fast-prototyping or just trying out ideas about stochastic processes.
You can just [run it in a browser](http://webppl.org/) and it even provides intelligent visualizations of many common data formats.

For example, the WebPPL code calculates the Bayesian solution for the [3-card puzzle](https://www.problang.org/chapters/app-01-probability.html):

<pre class="webppl">
// three cards; with blue or red on either side
var cards = [["blue", "blue"],
             ["blue", "red"],
             ["red", "red"]]

var model = function() {
  var card  = uniformDraw(cards)
  var color = uniformDraw(card)
  condition(color == "blue")
  return card.join("-")
}

viz(Infer({method: "enumerate",
           model: model
           }))
</pre>

<script>
// find all <pre> elements and set up the editor on them
var preEls = Array.prototype.slice.call(
                  document.getElementsByClassName("webppl"));
preEls.map(function(el) {
    console.log(el);
    editor.setup(el, {language: 'webppl'}); });
</script>

WebPPL, or tools like it, are extremely useful also for teaching: no installation requirements, no fuzz with visualization, direct hands-on exploration of stochastic processes and Bayesian inference.
Consequently, several instructional web-books have used WebPPL for interactive illustrations and exercises, e.g., on [probabilistic models of cognition](https://probmods.org/), [probabilistic language understanding](https://www.problang.org/), or statistics (see [here](https://mhtess.github.io/bdappl/) or [here](https://michael-franke.github.io/intro-data-analysis/index.html)).


# What's Quarto?

[Quarto](https://quarto.org/) is a relatively new "open-source scientific and technical publishing system" [from the Quarto website] and may become a more general alternative to replace Jupyter notebooks or Rmarkdown.
I've used [Jupyter-notebook based webbooks](https://michael-franke.github.io/npNLG/000-intro.html) and [Rmarkdown-based webbooks](https://michael-franke.github.io/intro-data-analysis/index.html) for educational material in my classes, and it worked fine.
But I also recently tried Quarto and found the ease, portability and overall configurability improved (totally subjective, I guess).

Since I will likely use Quarto in the future, and since others likely will, too; and since I would love to see more people use tools like WebPPL for education in stats and probabilistic modeling,  this post describes how to integrate executable WebPPL code boxes into HTML documents, generated with Quarto.


# Integrating WebPPL in Quarto documents

Here's what you need to do to get interactive WebPPL code boxes and outputs into your HTML-output from QMD files.

1.  In the YML preamble of your QMD file, include the following:

    {% highlight yml %}
    include-before-body:
        text: |
            <link rel="stylesheet" href="https://s3-us-west-2.amazonaws.com/cdn.webppl.org/webppl-editor-1.0.9.css">
            <link rel="stylesheet" href="https://s3-us-west-2.amazonaws.com/cdn.webppl.org/webppl-viz-0.7.11.css">
            <script src="https://s3-us-west-2.amazonaws.com/cdn.webppl.org/webppl-editor-1.0.9.js"></script>
            <script src="https://s3-us-west-2.amazonaws.com/cdn.webppl.org/webppl-viz-0.7.11.js"></script>
            <script src="https://s3-us-west-2.amazonaws.com/cdn.webppl.org/webppl-v0.9.13.js" defer async></script> {% endhighlight %}

1.  Wrap all WebPPL code in \`<pre class="webppl"> &#x2026; </pre>\`.
2.  Include the following JS-script at the end of your QMD file:

    {% highlight HTML %}
    <script>
    // find all <pre> elements and set up the editor on them
    var preEls = Array.prototype.slice.call(
                      document.getElementsByClassName("webppl"));
    preEls.map(function(el) {
        console.log(el);
        editor.setup(el, {language: 'webppl'}); });
    </script>  {% endhighlight %}


# Full example

Here is a full example of how your QMD file might look like.

    {% highlight markdown %}
    ---
    title: "Testing webPPL in QMD"
    author: "Ernie and Bert"
    include-before-body:
      text: |
        <link rel="stylesheet" href="https://s3-us-west-2.amazonaws.com/cdn.webppl.org/webppl-editor-1.0.9.css">
        <link rel="stylesheet" href="https://s3-us-west-2.amazonaws.com/cdn.webppl.org/webppl-viz-0.7.11.css">
        <script src="https://s3-us-west-2.amazonaws.com/cdn.webppl.org/webppl-editor-1.0.9.js"></script>
        <script src="https://s3-us-west-2.amazonaws.com/cdn.webppl.org/webppl-viz-0.7.11.js"></script>
        <script src="https://s3-us-west-2.amazonaws.com/cdn.webppl.org/webppl-v0.9.13.js" defer async></script>
    ---
    
    # Set up
    
    To include WebPPL in QMD files Do this:
    1. Use `include-before-body` (as done here) to include relevant CSS and JS files.
    2. Wrap WebPPL code in `<pre class="webppl"> ... </pre>`.
    3. Include the `script` snippet below at the end of the QMD document.
    
    
    # Example
    
    Here is the three-card problem:
    
    <pre class="webppl">
    // three cards; with blue or red on either side
    var cards = [["blue", "blue"],
                 ["blue", "red"],
                 ["red", "red"]]
    
    var model = function() {
      var card  = uniformDraw(cards)
      var color = uniformDraw(card)
      condition(color == "blue")
      return card.join("-")
    }
    
    viz(Infer({method: "enumerate",
               model: model
               }))
    </pre>
    
    <script>
    // find all <pre> elements and set up the editor on them
    var preEls = Array.prototype.slice.call(
                      document.getElementsByClassName("webppl"));
    preEls.map(function(el) {
        console.log(el);
        editor.setup(el, {language: 'webppl'}); });
    </script> {% endhighlight %}

