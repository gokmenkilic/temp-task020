---
title: "Introduction to Fundamental of Benchmarking"
teaching: 20 # teaching time in minutes
#exercises: 5 # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- Why assess performance in large scientific codes?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Differentiate performance assessment, analysis and engineering
- Explain why is it necessary to benchmark code without relying on exsiting version
::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction to Fundamental of Benchmarking

This lesson will introduce concept of benchmarking with underlying theory. The main idea is not deploying your code here to analyse, rather it is guiding you how to asset your own code. 

Altough there is no standard way to benchmark the code, we will touch fundamentals of benchmkaring and structure a workflow to help a scentist to use in their own process or assetments. Therefore, we will start to introduce key metrics of benchmarking and put them glossary of this course so that you will have a better understanding of benchmarking at the end of the course. Saying that to have a skill to  decide which metrics means what and how you can use relavant technics to benchmark and asset your code.


What you need to know before starting this course are:

 1. It has assumed that the learner of this course has a limited knowledge of benchmarking domain and the algorthims used.
 2. It has evaluated that how a code performs while taking consideration of characteristics.
 3. It has defined pre-experimental setup for experiments.
 4. It has considered that the performance of the code bound the machine's point - not the algoithm or science case. 

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

Inline instructor notes can help inform instructors of timing challenges
associated with the lessons. They appear in the "Instructor View"

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Can you do it?

What is the output of this command?

```r
paste("This", "new", "lesson", "looks", "good")
```

:::::::::::::::::::::::: solution 

## Output
 
```output
[1] "This new lesson looks good"
```

:::::::::::::::::::::::::::::::::


## Challenge 2: how do you nest solutions within challenge blocks?

:::::::::::::::::::::::: solution 

You can add a line with at least three colons and a `solution` tag.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Figures

You can use standard markdown for static figures with the following syntax:

`![optional caption that appears below the figure](figure url){alt='alt text for
accessibility purposes'}`

![You belong in The Carpentries!](https://raw.githubusercontent.com/carpentries/logo/master/Badge_Carpentries.svg){alt='Blue Carpentries hex person logo with no text.'}

::::::::::::::::::::::::::::::::::::: callout

Amdahl's Law

It can be tricky to understand how much speedup parallelisation you can actually gain after benchmark your code.
To figure out that we use **Amdahl's Law**. It describes how many processors you keep a problem, the part of the code that should run serially puts a limit on total speedup.


![The theoretical maximum speedup of an HPC described by Amdahl's law at above figure which shows logaritmic parallelization vs lineer speedup. Whether how much of code could be paralelized and how much speed up you would gain after it. As it is clear in the figure speedup restricly constrained by unparallelizable portion.](episodes/fig/AmdahlsLaw.svg){alt='Amdahls law'}

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout


:::::::::::::::::::::::::::::::::::::::::::::

## Math

Two term we'll use throughout this lesson are
**speedup** and **efficiency**.

Speedup compares the time taken on one processor, $T(1)$, to the time
taken on $p$ processors, $T(p)$:

$S(p) = \dfrac{T(1)}{T(p)}$

Efficiency normalises speedup by the number of processors used, giving
a value between 0 and 1 (or 0% and 100%):

$E(p) = \dfrac{S(p)}{p}$

**Amdahl's Law** predicts the maximum speedup achievable given a fixed
problem size, where $f$ is the fraction of the code that must run
serially:

$S(p) = \dfrac{1}{(1 - f) + \dfrac{f}{p}}$

As $p \to \infty$, speedup meets to $\dfrac{1}{1-f}$.

::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
