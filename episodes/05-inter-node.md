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

#fixme: add running nbody on multiple nodes example

:::::::::::::::::::::::: solution 

#fixme: probably some profiling with vtune can go here - not sure how it can squeeze plots, maybe sort of utulization or hotspot?

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

An illustrative run with $n_1 = 100{,}000$ and $t(1) = 200$ s:

| Nodes $p$ | $n$ | $t(p)$ [s] | $E_{inter}$ |
|---|---|---|---|
| 1 | 100,000 | 200 | 1.00 |
| 2 | 141,421 | 210 | 0.95 |
| 4 | 200,000 | 235 | 0.85 |
| 8 | 282,843 | 290 | 0.69 |
| 16 | 400,000 | 360 | 0.56 |
| 16, larger problem | 600,000 | 520 | 0.87 |

At 16 nodes efficiency falls under 60%, so the problem is enlarged.
The bigger problem brings efficiency back above 80%, which is the
good behaviour as we mentioned at introdcution of this lesson.

::::::::::::::::::::::::::::::::::::::::::::::: callout

Amdahl's Law, from Episode 1, fixes the problem size. Gustafson's Law
lets the problem grow with the machine. With $s$ the serial fraction
of the runtime on the parallel system, the scaled speedup is:

$S(p) = p - s\,(p - 1)$

With $s = 0.02$ on 16 nodes, $S = 15.7$, an efficiency of about 98%.
A growing problem hides a small serial part, which is why the
N-body code can scale well when its problem is enlarged with the node
count. The method in this episode does not use Gustafson's formula
directly. It measures efficiency with the workflow and calibration above.

:::::::::::::::::::::::::::::::::::::::::::::::::::::

## Preperation

Before running a multinode benchmark case, it will identify algoritmic complexity of problem, so that we'll increase the complexity to calibrate number of nodes we'll be using. Let's say an algorithm's cost grows as $O(n^g)$ with problem size $n$.
For $g = 1$, doubling $n$ doubles the runtime. For $g = 2$, it
quadruples it. The efficiency becomes:

$E_{inter}(p) = \dfrac{t(1)/n_1^{\,g}}{\left(t(p)/n_{inter}^{\,g}\right)\cdot p}$

Here $n_1$ is the problem size on a single node, $n_{inter}$ the size on
$p$ nodes, and the timings are raw.

## Evaluation

After increasing node counts and measuring the timings, we should collect every node count
where we had to increase the problem size. For each one,we'll take the
efficiency of the larger setup and let $C_{inter}$ be the number of such
jumps, $C^{80\%}_{inter}$ the number that reach 80% or more, and
$C^{60\%}_{inter}$ the number that land between 60% and 80%. Rest of evaluation will be as same as our benchmark rubrics idea at [core level benchmarking](episodes/03-core.md).


:::::::::::::::::::::::::::::::::::::::::::::: callout

Performance metrics describe observed behaviour. They carry no weighting
against the other rubrics (core, intra-node, GPU, I/O), so deciding
which way around to tackle first needs input from the people who know the
code and its science. 

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- Weak scaling across nodes starts from one reasonably large problem size
- Efficiency across different problem sizes must be calibrated with the algorithm's complexity
- A code scales well across nodes if each problem-size increase brings efficiency back above 80%
- #fixme (if we can add a callout or challenge how does that work for hybrid codes if there is an avalible example for it)

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
