---
title: "Intra node level benchmarking"
teaching: 10 # teaching time in minutes
exercises: 2 # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- How a code scale across a whole node?
- How do we interprate parallelism by using performance analysis tools? #fixme (performance anlaysis tools something meant to default per lesson where added user profiles on Azimuth)
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understanding scalability before running a whole node test
- Distinguish parallesiation of code frantions and identify their scaling
- Providing guidance on code's behaviour on a pre-defined architecture
- Evaluation of Amdahl's Law and blancing the performance

::::::::::::::::::::::::::::::::::::::::::::::::

## Intra-node level becnhmarking

After learning how to learn our codes utulize in a single core, now we can disvocer node-level performance analysis. We also called it "intra node" which means basically inside the node. At this point, we willtouch practice of Amdalh's Law again weather our code make good use of parallelisation or not. To understand this we can benefit from below graph.

![Desicion Graph](episodes/fig/DesicionGraph.png){alt='Desicion Graph'}

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

Select the appropriate kernel to let you generate perforamnce analysis backend within Moodle service.

#fixme add kernel info from Azimuth 

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

![Decision graph for intra-node analysis. Start by identifying parallelism in the code, then compare theoretical parallelism to observed parallelism. If they disagree, the cause is either that tasks are too small or that tasks serialise each other.](fig/decision-graph.png){alt='Flowchart. A box reading "Identify parallelism in the code" leads to a diamond reading "Compare theoretical parallelism to observed parallelism". Two arrows leave the diamond: one to "Tasks are too small" and one to "Tasks serialize each other".'}

::::::::::::::::::::::::::::::::::::: challenge

###  Which branch of the decision graph?

Let's say we have two codes both have plenty of parallel work in principle, yet both
scale poorly on a single node. Using the decision graph, decide which
branch each one belongs to.

**Code A.** The code creates millions of very short tasks, each
running for only a few microseconds. The profile shows most of the
time going into the OpenMP runtime (barrier and overhead functions),
and effective CPU utilisation is well below 80%.

**Code B.** The code creates a moderate number of tasks, and each one
contains a loop with a very small critical section. The profile shows
a large amount of spin time in the threading back-end, even though
all threads look busy.

1. Which branch does each code belong to?
2. What evidence in the description points to that branch?

:::::::::::::::::::::::: solution

**Code A: tasks are too small.** Concurrency is high, but creating and
cleaning up each task costs more than the work inside it. The overhead
shows up in the runtime rather than in your own functions, which is
why the runtime dominates the profile. A reasonable task should run
for at least tens of microseconds.

**Code B: tasks serialise each other.** The tasks look parallel, but
each one briefly locks the others out, so in effect they run one after
another. Many short critical sections in a row appear as heavy spin
time in the threading back-end. 

In both cases the symptom is the same: parallelism exists in theory
but not in the measurements. The evidence inside the profile is what
separates the two branches. 

:::::::::::::::::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::
## Figures

You can use standard markdown for static figures with the following syntax:

`![optional caption that appears below the figure](figure url){alt='alt text for
accessibility purposes'}`

![You belong in The Carpentries!](https://raw.githubusercontent.com/carpentries/logo/master/Badge_Carpentries.svg){alt='Blue Carpentries hex person logo with no text.'}

::::::::::::::::::::::::::::::::::::: callout

Callout sections can highlight information.

They are sometimes used to emphasise particularly important points
but are also used in some lessons to present "asides": 
content that is not central to the narrative of the lesson,
e.g. by providing the answer to a commonly-asked question.

::::::::::::::::::::::::::::::::::::::::::::::::


## Math

One of our episodes contains $\LaTeX$ equations when describing how to create
dynamic reports with {knitr}, so we now use mathjax to describe this:

`$\alpha = \dfrac{1}{(1 - \beta)^2}$` becomes: $\alpha = \dfrac{1}{(1 - \beta)^2}$

Cool, right?

::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
