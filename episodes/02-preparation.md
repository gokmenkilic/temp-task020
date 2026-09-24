---
title: "Preparation"
teaching: TBD # teaching time in minutes
exercises: TBD # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do we choose a characteristic benchmark of codebase?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Prepare the benchmark case
- Define the benchmark characteristics

::::::::::::::::::::::::::::::::::::::::::::::::

In this subsection, we will look at how to prepare a benchmark case to see the performance of the code. It usally calls "pre-assessment" (e.g. defining charctesistics of benchmark, preparing the compiler setup etc). As all domains could differentiate from one to other in terms of algoritmic complexity and behaviour etc, we will treat the code like a black-box and prepare the setup based on some rules. This rules can be checked via a checklist to identify basic informations from code. This informations will help the person that will run the benchmark between the code owner. Because it is not always the case we benchmark our own codes. It generally carries out via external people who might be unfamillar to our domain. Without previous knowledge of code, the checklist will help us to understand underlying characteristics of code and its behaviour on targeting machine. 

## Checklist

::::::::::::::::::::::::::::::::::::::::::::::callout
Before starting benchmark the code and analysis it, it is expected to fill the knowledge gap between owner of the code and benchmark analyst. Below points reflects initial checks for code:
 
 1. An archive that contains all files,
 2. Relying on a static files (making sure that the files for benchmarking is not going to be changed during the analysis),
 3. Include the documentation of benchmark (e.g. how to build and run the code)
 4. Reduce size of benchmark, however not too small, it should be representative for the case study.
::::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

This part of section related how to use Cosma Azimuth system.
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Is this a good benchmark case?

A main routine of a large scientific code has planned into a benchmark. It only tests that main routine,
and it can only run a small problem size.

1. According to the checklist above, is this a good benchmark?
2. What's the main thing missing?

:::::::::::::::::::::::: solution

### Solution

**1.** No, it's missing two things the checklist asks for.

**2.** It only tests a main routine,however it worth to check how other routines are behaving in the code. It also can be benchmark with different problem sizes. A good
benchmark should cover multiple routines and be configurable to
run at different problem sizes.

::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Benchmark Characteristics

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


## Compiler Setup

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
