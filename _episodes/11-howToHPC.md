---
title: "Using a HPC"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- "First objective."
keypoints:
- "First key point."
---

With all of this in mind, let's connect to a cluster (if you haven't done so already!). 
For these examples, we will connect to Gowonda - a high-performance cluster located at Griffith University.
Although it's unlikely that every system will be exactly like Gowonda, 
it's a very good example of what you can expect from a HPC.

![HPC](../files/hpc-architecture/slide1.jpg)

There are several steps we will need to follow to run analysis on a HPC. 
* First you will need to write a batch scrip (used by the HPC scheduler). This tells the HPC how much resources you need (i.e. no of CPU's and amount of time it will take to run). The batch script also tells the HPC where scripts and data are for analysis. 
* You will need to copy your scripts and data accross to the HPC.


In the following we will go through these steps in detail.
