---
title: "GPU level benchmarking"
teaching: 10 # teaching time in minutes
exercises: 2 # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- How close does a code get to the theoretical peak performance of the GPU?
- What should be checked before trusting a GPU benchmaark?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Preparing a GPU benchmark and using a problem larger than the GPU cache
- Calculating the observed work rate of a kernel from profiler

::::::::::::::::::::::::::::::::::::::::::::::::

Even though we used performance rubrics accross other lessons, we'll also use it in GPU level benchmarking to see how the code make a good use of hardware. With Nbody simulation, we'll try to investigate how the implementation of code benefit from parallelisim of theGPU. To do that we'll firstly investigate peak perforamnce of our system. We will use the same method as achieved performance divided by theoretical peak. Please note that in this episode we will assess a single GPU, using multiple GPUs is out of scope.

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

We're targeting to use Nvidia RTX 6000 on Azimuth cloud system as you do not have install any software for this lesson.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

## Preparation

To prepare our data for GPU benchmark, we need to pay attention several things such as our data, artitecture we will be using and complier versions etc. We can check our benchmark with following steps on GPUs:

1. Every GPU generation has a compute capability where code desigin to build and run on it. We have to tell our code which system we will be using via comptue capability.
2. To build our code we have to use most effective compiler. Choosing most recent compiler doe not mean you will get more performance. It is always worth to checking with latest compilers however.
3. Last thing for benchmark preparation deciding our data to represent well on GPU. As with the core measurement, a problem that fits in cache gives unrealistically fast results. We have to check the memory of the benchmark on the GPU to confirm it is big enough.

::::::::::::::::::::::::::::::::::::: challenge 

Your built your code for an older GPU, and now you
want to build and run it on an H200. What do you need to check and change
first?

:::::::::::::::::::::::: solution 

You need to check the compute capability of H200. ([NVIDIA compute capability](https://developer.nvidia.com/cuda/gpus)).
For the H200 we need to add `-code=sm_90` to our makefile.

:::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Data Collection

To get the observed rate in FLOPS/s we need the number of
floating point operations the kernel executed, and its runtime.

On Nvidia GPUs, Nsight Compute (`ncu`) can count the operations:

```bash
ncu --metrics "regex:^sm_.*d_op_(d|f[^p]|h).*\\.sum$" --csv \
    --log-file out.csv ./code
```

By help of above command we collected `sm__sass_thread_inst_executed_op_{METRIC}_pred_on.sum`,
where `{METRIC}` is one of `dfma`, `dadd`, `dmul`, `ffma`, `fadd`,`fmul`, `hfma`, `hadd` or `hmul`.

::::::::::::::::::::::::::::::::::::: callout

GPU vendors provides its own profiling tools, with similar but
different counters. You have to decide which metric you want to see out of profiling your code, and if it is available on the system. 

::::::::::::::::::::::::::::::::::::::::::::::::

## Evaluation

The GPU peak performance ratio is:

$C_{GPU} = \dfrac{R_{observed}}{R_{theoretical}}$

::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
