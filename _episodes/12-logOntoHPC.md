---
title: "Log onto a HPC"
teaching: 15
exercises: 10
questions:
- "How do I log on to the HPC?"
objectives:
- "Understand the general HPC architecture."
keypoints:
- "A cluster is a set of networked machines."
- "Clusters typically provide a login node and a set of worker nodes."
- "Files saved on one node are available everywhere."
---

## Logging onto the HPC

Open a bash terminal, you should see something similar to the following:
```
sNumber@PC123456-OSX:~$
```
{: .bash}
This part indicates that bash is in your computer **sNumber@PC123456-OSX**.

Now let's use the `ssh` command to connect to the HPC now:
```
ssh sNumber@gc-prd-hpclogin1.rcs.griffith.edu.au
```
{: .bash}

```{.output}
Last login: Fri Jan 24 14:40:59 2020 from pc12345-osx.staff.ad.griffith.edu.au
```

If you've connected successfully, you should see a prompt like the one below. 
This prompt is informative, and lets you grasp certain information at a glance:
in this case `[sNumber@gc-prd-hpclogin1 ~]$`. The address has changed from our computer directory to the server address, **were on the HPC!!!!**

```{.output}
[sNumber@gc-prd-hpclogin1 ~]$
```

## Where are we? 

Very often, many users are tempted to think of a HPC installation as one giant, magical machine.
Sometimes, people even assume that the machine they've logged onto is the entire computing cluster.
So what's really happening? What machine have we logged on to?
The name of the current computer we are logged onto can be checked with the `hostname` command.
(Clever users will notice that the current hostname is also part of our prompt!)

```
hostname
```
{: .bash}
```
gc-prd-hpclogin1
```
{: .output}

Clusters have different types of machines customized for different types of tasks.
In this case, we are on the login node.
The login node serves as a gateway to the cluster and serves as a single point of access.
As a gateway, it is well suited for uploading and downloading files, setting up software, and running quick tests.

**It should never be used for doing actual work.**

The real work on a HPC gets done by the "worker" nodes.
Worker nodes come in many shapes and sizes, but generally are dedicated to doing all of the heavy lifting that needs doing. 
All interaction with the worker nodes is handled by the scheduler software. 

There are also specialized machines used for managing disk storage, user authentication, 
and other infrastructure-related tasks. 
Although we do not interact with these directly, 
but these enable a number of key features like ensuring our user account and files are available throughout the cluster.
This is an important point to remember: 
files saved on one node (computer) are available everywhere on the cluster!
