---
title: "Core Level Benchmarking"
teaching: TBD # teaching time in minutes
exercises: TBD # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do you find out if your code is making good use of a single core?
- What separates a "good enough" measurement from a misleading one?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain what core level performance benchmarks are
- Describe how to prepare a good core level benchmark case
- Calculate a core performance ratio and classify it

::::::::::::::::::::::::::::::::::::::::::::::::

When we look at the core level performance the first thing we investigate is measure how well our code utilize a single core. Recently, most of the hardwares designed for using vector instructions efficiently where data moves between memory and compute via fast cachechannels. However, whether our code takes advantage of them is entierly different question.

When you use high level performance analysis tools, it is common you will likely see vectorication ratios, memory utulizations and those kind of metrics which can not be a good starting point too look at. To prepare a good benchmark case, we therefore start with hig level numbers. For example, how close does our code get to the machine's peak performance? Despite the running any heavy profiling tools, these number will tell us whether our code compute bound or memory bound and how it is well utulize the microarcitechture of harware. 

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

This part is for running small examples on COSMA/Azimuth service for instructors.
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge 

#### The benchmark rubrics

Across every section of this course, we will use three classification:

- **Green** (≥ 80%): performing efficiently
- **Yellow** (60–80%): not using the hardware to its full potential
- **Red** (< 60%): a clear performance flaw

::::::::::::::::::::::::::::::::::::::::::::::::::

## Running a single core benchmark

As we mention in the preparation section, benchmark needs to be set up according to the all environment that we have. To do that we have to care about some criterias:

- A representative benchmark case should fit in the cache. You may no idea if the problem you will be running on fits on the cache or not. Having unrealistic results could be a bad benchmark case you desgined and run. To avoid this we have to be sure that the problem size is not too small to sit L1/L2/L3 cache. Before running the benchmark case, it is always necessary that we are checking target system memory according to the our case.

- So that we have to know what is peak performance of hardware algin with using single core. Please be aware many HPC systems allows you to run your program on login node initially. However, to be able to benefit from peak performance you have to run the program on a single core. 

- Also we will need to know what is peak performance of our program where we run executable.

Recall the `deploy.sh` pattern from the Preparation episode this is
exactly where a core level benchmark run. Once the code is
built, you'd run a peak performance pinned to a single
core, rather than the all program:

```bash
## Runnining single core level peak performance check
likwid-bench -t peakflops -w S0:16kB:1
```
Above command pins the application the `peakflops` benchmark to a single core on the
first socket (`S0`), via a data half the size of the L1 cache. This method allows us to avoid memory effects and pinned on compute.

::::::::::::::::::::::::::::::::::::: callout

As we mention earlier it is worth to check you have using weather project code or partition submit your job or you interactively using the hardware. Because sharing resources on login node may cause you have not quite right numbers for result. Therefore we usally reccomend you have a exculise node access while running your benchmarks.

::::::::::::::::::::::::::::::::::::::::::::::::

## Evaluation

To evaluate core performance, we will need two numbers:

- The **maximum single-core peak performance** the hardware can
  theoretically deliver
- The **obtained single-core peak performance** your code actually
  achieves

```bash
likwid-perfctr -f -C 0 -g FLOPS_DP ./code
```
Above command will pin our code's serial run to the first physical core and
measures double precision floating point throughput.



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
