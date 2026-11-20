---
title: 'Reference'
---

## Glossary

performance assessment
: It describes collecting, measuring and reporting targeted performance metrics of code and reporting them without exlanining underlying reasons.

performance analysis
: It describes explanining why a code behaves the way it does, usally after a performance assetment performed.

performance engineering
: It describes improvment and refactoring of code after performance anaylsis done.

refactoring
: It describes improvment of a code, changing structure without affecting its external behaviour.

profiling
: It stands for recording total times, such as how much time spent in each funtion. It shows effect of running the program. See [profiling](https://en.wikipedia.org/wiki/Profiling_(computer_programming)). 

execution
: It usally describes running of a program on a machine, as opposed to building it.

job
: It describes an indivual unit of work submitted to a cluster. 

task
: It describes a unit of work run across parallel resources. See[task](https://en.wikipedia.org/wiki/Task_(computing)).

compile time
: It describes a stage where source code is translated into executable program, before it runs.

tracing
: It describes recording of individual events in the order they happaned in a source code. See [tracing](https://en.wikipedia.org/wiki/Tracing_(software)).

idle
: It usally desribes a state that CPU or GPU are not being used by any code or proceses. See [idle](https://en.wikipedia.org/wiki/Idle_(CPU)).

cluster
: It describes a set of networked nodes working together through parallel processing. 

node
: It describes one standalone comptuter or server within a cluster that excuetes source codes, jobs and tasks.

core
: It describes a single processing unit inside a node.

login node
: It describes the node you connect to on an HPC system. It usally uses for compiling and submitting jobs, however not benchmarking, because evreyone on ystem shares it.

compute node
: It describes a node where jobs actullay run.

intra-node
: It describes within a single node where there is no data exchange betwen other nodes and therefore no MPI.

inter-node
: It desribes between separte nodes, which exchange data over netwrok, usally with MPI.

scheduler
: It stands for a sofware which descides which jobs run on which nodes and when. Slurm is an good example for scheduler. See [slurm workload manager](https://en.wikipedia.org/wiki/Slurm_Workload_Manager).

dynamic scheduling
: It describe assinging work to processors at runtime rather than before execution begans. See [load blancing](https://hpc-wiki.info/hpc/Load_Balancing).
	
speedup
: It is a number that measures the relavtive performance of two or more systems processing on the same problem. See [speedup](https://en.wikipedia.org/wiki/Speedup)). 

task-based parallelisation
: It desribes splitting a program into many tasks, some of which dpend on others. See [task parallelism](https://en.wikipedia.org/wiki/Task_parallelism). 

theoretical concurrency
: It desribes how much work could run at the same time in principle within a source code and its dependencies to compare with practical concurrency.

practical concurrency
: It desribes how much of available parallel work can really run at the same time on a given machine to compare with theoretical concurrrency.

threading analysis
: It describes to analyse threads activities in profiling tools such as how well cores are used and general picture what threads are doing. See [threading analysis](https://www.intel.com/content/www/us/en/docs/vtune-profiler/user-guide/2026-1/threading-analysis.html).  

multithreading
: It describes using multiple threads inside one process. See [multithreading](https://en.wikipedia.org/wiki/Multithreading_(computer_architecture)).

overhead
: It describes extra time spent managing parallel work. Synchronising threads and cummunation between nodes are good example for overhead. 

occupation
: It describes a part of available cores or threads that are busy with doing actual work.

utulization
: It describes fraction of time a code doing actual work. 

coverage analysis
: It describes measuring how much of a program's runtime is spent in code that runs in parallel, compared with code that runs serially.

flame graph
: It illustrates  which functions call which, and the width of each bar shows how much time was spent there. See [flame graphs](https://www.brendangregg.com/flamegraphs.html).

strong scaling
: It describes keeping the total problem size fixed while increasing number of processors. 

weak scaling
: It describes increasing problem size while keeping number of processors constant. 

hotspot analysis
: It describes finding funtions or lines where a code spends most of its time. See [hotspot analysis](https://www.intel.com/content/www/us/en/docs/vtune-profiler/user-guide/2026-0/basic-hotspots-analysis.html).

performance characterization analysis
: It gives a summary of compute intensive code where usage of CPU, memory and floating point of operations can be found. See [performance characterization analysis](https://www.intel.com/content/www/us/en/docs/vtune-profiler/user-guide/2024-2/hpc-performance-characterization-analysis.html). 

observed parallelism
: It is same meaning as practical parallelism, tells us how much work is actually running at the same time.

blancing
: It describes sharing work evenly between cores so that none of them sit idle waiting to others. See [load balancing](https://en.wikipedia.org/wiki/Load_balancing_(computing)).

global efficiency
: It describes how well the parallelization of code performing.

parallel efficiency
: It describes how well the execution of code performing.

load balance efficeny
: It shows how well the distribution of work to processes of threads is performed by code.

communication efficiency
: It shows the loss of efficiency by communication time.

computation efficiency
: It describes how well the computational load of code scales with number of processes. 

runtime
: It describes the time a program or a part of it takes to run on hardware.

I/O 
: It stands for input output where processor read and write to storage according to the data pipeline. 

inclusive
: It describes a timing that counts a funtion's own time plus the time of ecreything it calls. This term can interpret with exculisive.

exculisive
: It usally describes a dedicated hardware to access for a single user or a timing only counts the time spent in a fcuntion itself.

compute bound
: test

memory bound
: test

optimisaation
: test

slurm
: It desribe a most widely used job scheduler on HPC systems. See [Slurm](https://slurm.schedmd.com/).

numactl
: test

algoritmic scaling
: test

problem size
: It describes the amount of work set by the input data, for example the number of particles or grid points.

algorithm complexity
: It measures how amount of the work an algorithm grows with the problem size. Some others use term of "computational complexity" to describe it. For more info please see [computational complexity](https://en.wikipedia.org/wiki/Computational_complexity).

hybrid codes
: It usally refers codes where MPI and OpenMP used for paralelization. These codes combines MPI for making good use of multiple nodes, OpenMP for threading on a single node.
