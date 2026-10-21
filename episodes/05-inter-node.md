---
title: "Inter node level benchmarking"
teaching: 40 # teaching time in minutes
exercises: 10 # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- How to make good use of multiple nodes?
- How we interpret efficency while increasing size of problem?
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain why weak scaling is using to assess performance across multiple nodes rather than strong scaling
- Calibrate efficiency for changing problem sizes using the algorithm's complexity
::::::::::::::::::::::::::::::::::::::::::::::::

When we want to scale up our code across to multiple nodes, there are certain things we have to be extra careful. To prioritise, weak and strong scaling are key metrics to have an idea about how our code perform with multiple nodes. In this lesson, we will use nbody simulation to get better understanding of weak and strong scaling aling with relavant performance metrics. To remind our 80% - 60% rule to say if insufficent or if we increase the problem size it get back to a level of 100% - %80 efficiency. 

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

Make sure that you are running example code in right kernel. If you spot anything odd to initilaze your kernel please kill and close all your running kernels before restarting it.
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

Running MPI ranks on a single node, with physically shared memory,
belongs to the intra-node assessment from the previous episode. Only
runs over several physically separate nodes count as inter-node.

:::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge 

#fixme add Gustafson's Law here with Nbody example

:::::::::::::::::::::::: solution 

## Output
 
```output
[1] "This new lesson looks good"
```

:::::::::::::::::::::::::::::::::

#fixme add a challenge or introduce before hyrid codes

:::::::::::::::::::::::: solution 

You can add a line with at least three colons and a `solution` tag.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Workflow

Determine Nbody simulation with following metrics:

1. Pick a problem size $n_1$ for single node.
2. Measure the time $t(1)$.
3. Increase the number of nodes and measure the timings.
4. Compute $E_{inter}$ , using the calibrated formula.
5. If $E_{inter} \le 60\%$, increase the problem size and continue
from there with the larger setup.

How much can we  increase the problem size? It would be as large as the nodes can handle, while keeping each node's
local memory footprint close to what it was for $n_1$ on a single node.

## Preperation

Before running a multinode benchmark case, it will identify algoritmic complexity of problem, so that we'll increase the complexity to calibrate number of nodes we'll be using. Let's say an algorithm's cost grows as $O(n^g)$ with problem size $n$.
For $g = 1$, doubling $n$ doubles the runtime. For $g = 2$, it
quadruples it. The efficiency becomes:

$E_{inter}(p) = \dfrac{t(1)/n_1^{\,g}}{\left(t(p)/n_{inter}^{\,g}\right)\cdot p}$

Here $n_1$ is the problem size on a single node, $n_{inter}$ the size on
$p$ nodes, and the timings are raw.

::::::::::::::::::::::::::::::::::::: callout

Callout sections can highlight information.

They are sometimes used to emphasise particularly important points
but are also used in some lessons to present "asides": 
content that is not central to the narrative of the lesson,
e.g. by providing the answer to a commonly-asked question.

::::::::::::::::::::::::::::::::::::::::::::::::


## Evaluation

In this section, we'll determine how our nbosy simulation utulizing accross the nodes with our performance metrics.

::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
