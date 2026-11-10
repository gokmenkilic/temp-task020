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

::::::::::::::::::::::::::::::::::::: challenge 

What if you change to arhitecture of your code or want to build it with different compiler? What will be first thing you need to check it?

:::::::::::::::::::::::: solution 

You need to check compute capability across the different machines. Take a look at [CUDA GPU Comupte Capability](https://developer.nvidia.com/cuda/gpus). 

:::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

#fixme Compute Capability


## Data Collection

To get the observed rate in FLOPS/s we need the number of
floating point operations the kernel executed, and its runtime.

On Nvidia GPUs, Nsight Compute (`ncu`) can count the operations:

```bash
ncu --metrics "regex:^sm_.*d_op_(d|f[^p]|h).*\\.sum$" --csv \
    --log-file out.csv ./code
```

::::::::::::::::::::::::::::::::::::: callout

Callout sections can highlight information.

They are sometimes used to emphasise particularly important points
but are also used in some lessons to present "asides": 
content that is not central to the narrative of the lesson,
e.g. by providing the answer to a commonly-asked question.

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
