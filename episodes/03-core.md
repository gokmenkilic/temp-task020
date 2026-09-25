---
title: "Core Level Benchmarking"
teaching: 30 # teaching time in minutes
exercises: 10 # exercise time in minutes
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



## Core performance ratio

The core performance ratio is:

$C_{core} = \dfrac{\text{obtained peak performance}}{\text{maximum peak performance}}$

Classified as:

| $C_{core}$ | Classification | Meaning |
|---|---|---|
| $C_{core} \geq 0.8$ |  Green | Core compute performance is good |
| $0.6 \leq C_{core} < 0.8$ | Yellow | Not making full use of the hardware |
| $C_{core} < 0.6$ |  Red | Core compute performance is poor |

Note that above is normalised againist scalar peak. Due to some routines can not be vectorized, scalar peak used.

::::::::::::::::::::::::::::::::::::: challenge

### Classify these results. 

Three codes were benchmarked for single-core peak performance on the
same harware, where the hardware's maximum peak is 40 GFLOPS/s:

| Code | Obtained performance |
|---|---|
| A | 34 GFLOPS/s |
| B | 28 GFLOPS/s |
| C | 19 GFLOPS/s |

1. Calculate $C_{core}$ for each code.
2. Classify each as green, yellow, or red.
3. Which code(s), if any, need further investigation?

:::::::::::::::::::::::: solution

### Solution

| Code | $C_{core}$ | Classification |
|---|---|---|
| A | $34/40 = 0.85$ |  Green |
| B | $28/40 = 0.70$ |  Yellow |
| C | $19/40 = 0.475$ |  Red |


Code A is performing well and does not need further investigation at this
level of benchmark. Code B is worth a double check look. It is not clearly broken, but
there's room for improvement. Code C shows a clear issue and should be
prioritised for optimisation.

::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
