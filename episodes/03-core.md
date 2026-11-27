---
title: "Core Level Benchmarking"
teaching: 30 # teaching time in minutes
exercises: 10 # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do you find out whether your code is making good use of a single core?
- What separates a "good enough" measurement from a misleading one?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain what core level performance benchmarks are.
- Describe how to prepare a good core level benchmark case.
- Calculate a core performance ratio and classify it.

::::::::::::::::::::::::::::::::::::::::::::::::

When we look at the core level performance, the first thing we investigate is how well our code uses a single core. Most modern processors are designed to use vector (SIMD )instructions efficiently, where data moving between memory and the compute units through a hierachy of fast caches. Whether our code takes advantage of them, is an entierly different question.

High level performance analysis tools typically report detailed metrics such as vectorisation ratios and memory utulisation, but these are not a good starting point. To prepare a good benchmark case, we therefore start with high level numbers. For example, how close does our code get to the machine's peak performance? Before running  any heavy profiling tools, these numbers tell us whetherour code is compute bound or memory bound, and how uses the microarchitecture of the hardware. 

<!-- NOTE: Comparing a code's FLOP rate with the peak FLOP rate alone cannot
tell us whether a code is compute bound or memory bound. It is needed the
memory bandwidth and the code's arithmetic intensity.

Either soften this sentence ("these
numbers are the first step towards telling whether...") or add one line
saying a bandwidth measurement is the second number needed. -->

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

This part is for running small examples on COSMA/Azimuth service for instructors.
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

<!-- NOTE: We potentially need to amend below exercise. It may read better as a `callout` than a `challenge`. Also citation to performance analysis guidebook would be nice.-->

::::::::::::::::::::::::::::::::::::: challenge 

#### The benchmark rubrics

Across every section of this course, we will use three classifications:

- **Green** (≥ 80%): performing efficiently
- **Yellow** (60–80%): not using the hardware to its full potential
- **Red** (< 60%): a clear performance flaw

:::::::::::::::::::::::::::::::::::::::::::::::

## Running a single core benchmark

As we mention in the preparation episode, a benchmark needs to be set up the environment that we are running in. To do that, we need to consider a few criteria: 

- A representative benchmark case should not fit in the cache. You may not know whether the problem you will be running fits in the cache. If it does, the reults will be unrealistically good, and the benchmark case you designed and ran will be a poor one. To avoid this, make sure the problem size is not so small that it sits in the L1,L2 or L3 cache. Before running the benchmark case, always check the cache and memory sized of the target system against the memory your case uses.

<!-- NOTE: There could be a typo in performance analysis guidebook for core level benchmarking about caches. Need to be verified.-->

- We need to know the peak performance the hardware can deliver on a single core. Be aware that many HPC systems let you run your program on a login note at first. However, login nodes are shared,so to measure peak performance you need to run on a dedicated core of a compute node.

<!--Requesting a node with an exculisive access can go here -->

- Also we will need to know what is peak performance of our program where we run executable.

Recall the `deploy.sh` pattern from the Preparation episode this is
exactly where a core level benchmark run. Once the code is
built, you'd run a peak performance pinned to a single
core, rather than the all program:

```bash
## Running single core level peak performance check
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
::::::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- Core level benchmarking starts with obtained peak performance vs the hardware's maximum
- A good measurement needs a representative benchmark case larger than cache, exclusive node access, and pinned thread affinity
- $C_{core} = \text{obtained} / \text{maximum peak}$, classified as green (≥80%), yellow (60–80%), or red (<60%)
- $C_{core}$ is normalised against scalar not vectorised peak

:::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
