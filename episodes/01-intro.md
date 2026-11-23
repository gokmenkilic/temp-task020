---
title: "Introduction"
teaching: 20 # teaching time in minutes
exercises: 5 # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- Why assess performance in large scientific codes?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Differentiate performance assessment, analysis and engineering
- Explain why is it necessary to benchmark code without relying on exsiting version
::::::::::::::::::::::::::::::::::::::::::::::::

This lesson will introduces concept of benchmarking and with the theory behind it. The aim is not to analyse your code for you during the course,but show you how to assess your own code once the course is over. 

Altough there is no single standard way to benchmark a code,there are common fundementals. We will cover these and build them into a structured workflow that you can adapt to your own research andown performance assessments. Along the way we will introduce key metrics of benchmarking and collect them in the glossary of this course. By the end, you should be able to decide which metrics matter for your code, understand what each one tells you, and choose the right techniques to benchmark and assess it. 

It is assumed that the learner of this course has a limited knowledge of benchmarking, profiling and the algorithms used.  Before starting this course, it is assumed that the learner has:

 1. Has a code to be evaluated.
 2. Has a pre-defined metric which is a proxy for code performance (e.g. run time, ns per day, etc).
 3. Has sufficient knowledge of the code to know how to modify compiler flags and algorithms within it.
 4. Awareness that benchmarking might be specific to the system on which it is performed; running the code on another system might give different performance characteristics.

The last point is the reason you need to benchmark your code yourself. Some other published results, or results from a diffrent version of the code, were measured with diffrent combination of codeversion, compiler, libraries, input and machine. They are a useful starting point, however they can not tell you how your code bhhaves on your system.

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

This is a note for instructor of this course who might need to use COSMA Azimuth. 

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge 

## Have you been already performance analaysis?

Now, take a minute and think of a time in daily life when you compared two
ways of doing something to see which was more efficent or faster
even if you never called it "benchmarking."

:::::::::::::::::::::::: solution 

### Examples

- Timing two different driving routes to see which
  actually gets you there faster.
- Watching which supermarket checkout line is moving faster before
  joining one.
- Comparing two meals how much calorie you will gain according to the your diet.

Each of these is exactly what benchmarking a program does: measuring
real performance under different conditions, then using that
measurement to decide what to do next. 
 
:::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

This lesson aims to create a glossary that covers theory of performance analysis and optimisation. Please open it via
[Glossary](reference.html#glossary) in a new tab and refer back to it
as you go through this lesson.

:::::::::::::::::::::::::::::::::::::::::::::
 

## Amdahl's Law 
::::::::::::::::::::::::::::::::::::: callout

It can be tricky to understand how much speedup parallelisation you can actually gain after benchmark your code.
To figure out that we use **Amdahl's Law**. It describes how many processors you keep a problem, the part of the code that should run serially puts a limit on total speedup.


![The theoretical maximum speedup of an HPC described by Amdahl's law at above figure which shows logaritmic parallelization vs lineer speedup. Whether how much of code could be paralelized and how much speed up you would gain after it. As it is clear in the figure speedup restricly constrained by unparallelizable portion.The figure has taken from wikipedia: https://en.wikipedia.org/wiki/Amdahl%27s_law](episodes/fig/AmdahlsLaw.svg){alt='Amdahls law'}

::::::::::::::::::::::::::::::::::::::::::::::::

## Speedup and Efficiency

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

::::::::::::::::::::::::::::::::::::: challenge

### Is benchmarking the same as performance analysis?

Now, let's think about a health screening in medicine: a doctor checks your
blood pressure, pulse etc for standard checks. If some metrics are not in the ideal region
where they should be, it will be issued for further tests. It will then switch to analysis part.

1. When you **benchmark** your code (e.g. measuring $S(p)$ and $E(p)$
across different systems), which stage does that belong to assetments or analysis?
2. Is "benchmarking" and "performance analysis" the same thing? Why or
why not?

:::::::::::::::::::::::: solution

### Solution

**1.** Benchmarking is **assessment**. Measuring speedup and
efficiency is like taking blood pressure and pulse — you're recording
 *what* happens, not explaining *why*.

 **2.** No, they're not the same thing. Benchmarking only tells you
 *that* something might be wrong (e.g. speedup is lower than expected).
 It doesn't tell you *why*. Finding the "why" — for example, using a
 profiler to discover that most of the time is spent waiting on memory
 rather than computing — is **performance analysis**, the equivalent of
 the doctor ordering follow-up tests once a vital sign looks off.

 In short: **benchmarking is how you assess the code; analysis is how you
 explain what the assessment found.**

:::::::::::::::::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- Benchmarking measures how code performs, it doesn't explain why, and it doesn't fix anything in the code
- Performance work follows assessment, then analysis, then engineering
- Speedup $S(p) = t(1)/t(p)$ and efficiency $E(p) = S(p)/p$ are quantified by Amdahl's Law, which shows that a code's non-parallelisable fraction caps its total achievable speedup
- Profiling reveals where time is spent overall; tracing reveals the order in which events happened

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
