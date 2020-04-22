---
title: "Introduction to High Performance Computing"
teaching: 10
exercises: 0
questions:
- "What is High Performance Computing?"
- "Why should I be using High Performance Computing for my research?"
- "Don't I need to know how to program to use High Performance Computing?"
- "What are the different types of High Performance Computers (HPC), and what are the different problems each one can solve?"
objectives:
- "Understand what an HPC is."
- "Understand the different types of HPC and their uses."
- "Understand how HPC can improve your research efficiency."
- "Understand the 'barrier to entry' is lower than you'd think."
keypoints:
- "HPC typically involves connecting remotely to a **cluster** of computers."
- "HPCs can be used to do work that would either be impossible or much slower in a Desktop environment."
- "Typical HPC workflows involve submitting \"jobs\" to a scheduler which queues/priortises the \"jobs\" of all users."
- "The standard method of interacting with HPC's is via a Linux-based Command Line Interface called \"The Shell\"."
---

## What is a High Performance Computation?
High Performance Computing, known commonly as HPC or HPRC, is the name given to the use of computers with capabilities beyond the scope of standard desktop computers. The computers that qualify as HPC systems are typically seen as being more powerful than other systems; 
usually because they have more central processing units (CPUs), CPUs that operate at higher speeds, more memory, more storage, and faster connections with other computer systems. HPC systems are used when the resources of more standard computers, such as most dektops and laptops, are not enough to provide results in a timely fashion, if at all.  
The words "cloud", "cluster", and "high-performance computing" get thrown around a lot.
So what do they mean exactly?
And more importantly, how do we use them for our work?

The "cloud" is a generic term commonly used to refer to remote computing resources.
Cloud can refer to webservers, remote storage, API endpoints, and as well as more traditional "raw compute" resources. 
A cluster on the other hand, is a term used to describe a network of compters.
Machines in a cluster typically share a common purpose, 
and are used to accomplish tasks that might otherwise be too substantial for any one machine. 

![Clouds are made of Linux servers](../files/linux-cloud.jpg)

A high-performance computing cluster is a set of machines that have been 
designed to handle tasks that normal computers can't handle.
This doesn't always mean simply having super fast processors. 
High-performance computing covers a lot of use cases.
Here are a couple of use cases where high-performance computing becomes extremely useful:

* You need access to large numbers of CPUs.
* You need to run a large number of jobs.
* Your jobs are running out of memory on your computer.
* Perhaps you need to store tons and tons of data.
* You require an exceptionally high-bandwidth internet connection for data transfer.
* You need a safe archival site for your data.
* Your compute jobs require specialized GPU or FPGA hardware.
* Maybe your jobs just take a long time to run.

Chances are, you've run into one of these situations before.
Fortunately, high-performance computing installations exist to solve these types of problems.

> ## A Cluster of Computers?
>
> Most frequently, HPC systems are an interconnected network or **cluster** or many CPU's.  Each CPU can perform many tasks simultaneously.  By distributing \"jobs\" across many CPU's, hundreds or thousands of tasks can be performed in parallel.

## How do we interact with HPC's?

Working with HPC systems involves the use of a \"UNIX shell\" through a **command line interface** (CLI). A UNIX shell is a program which passes user instructions to other programs and returns results to the user or other programs. The user can pass the shell instructions interactively via typing them, or programatically by executing scripts. The most popular UNIX shell is **Bash**, the **B**ourne **A**gain **Sh**ell, which we will be using to interact with the HPC. As HPC users we need an understanding of basic UNIX commands, which will be the initial focus of this lesson.

Although users can work interactively with HPC systems, it is more common (and better practice) to perform most tasks via submitting \"jobs\". A job consists of commands which request HPC resources and specify a task to be completed. Jobs are prioritised and placed in a queue by a \"job scheduler\" before being executed.

## Why use an HPC?

HPC systems are designed specifically to assist researchers with analytically demanding tasks. Users can perform many small tasks simultaneously, such as projecting a single model onto datasets from different years. This is an example of "serial programming", where each task is entirely independent from the others. Alternatively, with the assistance of Message Passing Interfaces (**MPI's**), users can combine multiple CPU resources to perform a single task more efficiently. This is an example of "parallel programming", where each CPU is working on a portion of single task, before results are assembled in the correct order by an MPI. The benefits of using HPC systems for research often far outweigh the cost of learning to use a Shell and include:

* **Speed** Hundreds of high performance CPU's can perform many small jobs at once, or accelerate individually demanding tasks.
* **Volume** HPC's are typically backed by very large pools of shared storage, oftentimes at PetaByte scale.
* **Cost** Why pay for high performance analytical environment when one is already available to you for free?
* **Convenience** Keep your Desktop free to check e-mail, surf the web, and run Excel without crashing :-)


### Example: Nelle's Pipeline: Starting Point

Consider the case of Nelle Nemo, a marine biologist, who
has returned from a six-month survey of the
[North Pacific Gyre](http://en.wikipedia.org/wiki/North_Pacific_Gyre),
where she has been sampling gelatinous marine life in the
[Great Pacific Garbage Patch](http://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch).
She collected 10,000 samples in all, and has run each sample through an assay machine
that measures the abundance of 300 different proteins.
The machine's output for a single sample is
a file with one line for each protein.
For example, the file `NENE01812A.csv` looks like this:

~~~
72,0.142961371327
265,0.452337146655
279,0.332503761597
25,0.557135549292
207,0.55632965303
107,0.96031076351
124,0.662827329632
193,0.814807235075
32,1.82402616061
99,0.7060230697
.
.
.
.
200,1.13383446523
264,0.552846392611
268,0.0767025200665
~~~

Each line consists of two "fields", separated by a comma (`,`).
The first field identifies the protein,
and the second field is a measure of the amount of protein in the sample.
Nelle needs to accomplish tasks such as the following:

1.  For any given file, extract the amount of a given protein.
2.  Find the maximum amount of a given protein across all files.
3.  For each file, run a program called `stats.py` that she wrote,
    which produces a graph, and writes some statistics
    (these go in the directories `plots/` and `results/` respectively.)

Suppose that each file takes about a minute to analyze on her desktop system and consuming all of the resources available, so no email or any other work while the program is running.  With 10,000 files in all this means that it will take approximately 166 hours, or just under 7 days to completely process all the files. 

Shifting this work to an HPC system will not only stand to speed up the processig of these files but the processing will importantly allow Nelle to continue to use her own computer for other work.

### What are the constraints on compute power and how can HPC help?
The way a HPC is configured impacts on performance and workfows are often categorised according to which part of the HPC system constrains their performance. You may see the following terms used to describe performance on an HPC system:

* **Compute bound** A workflow becomes compute-bound when the cpu's are running near 100% thus limiting the processing speed. The CPU's execute code. This is typically seen when peforming math-heavy operations such as diagonalising matrices in computational chemistry software or computing pairwise force interactions in biomolecular simulations.
* **Memory bound** Memory bound means the rate at which a process progresses is limited by the amount memory available and the speed of that memory access. The performance of the workflow is limited by access to memory (usually in terms of bandwidth, i.e. the amount of data accessible at any one time). Almost all current HPC applications have a part of their workflow that is memory bound. A typical example of a memory bound application would be something like computational fluid dynamics.
* **Input/Output (I/O) bound** The performance of the workflow is limited by access to storage (reading from or writing to disk, across networks or databases). This is usually in terms of bandwidth but sometimes in terms of numbers of files being accessed simultaneously. I/O bound workflows are often seen in climate modelling and bioinformatics workflows.

* **Seriel processing**
* **Parrallel processing** 


### In reality, most research workflows exhibit many of these bottlenecks at different points in their execution.

What is limiting your workflow?

With your neighbour, have a think about a research workflow you use and identify which of the bottlenecks above may apply to your workflow?

Identify 1 of these bottlenecks and explain why you think it applies to your workflow.
