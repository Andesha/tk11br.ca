---
title: "HPC Quickstart"
description: "A practical starting point for working on shared HPC systems."
date: 2026-05-08T00:00:00-04:00
---

Researchers often get access to a cluster and then have no idea where to start. The documentation is large, the terminology is unfamiliar, and it is hard to tell which skills matter first.

Use this page as a decision tree. Find the task you need to do, and follow the linked resource.

## What should I learn next?

| If you need to... | Start here |
| --- | --- |
| Work comfortably in a terminal | Software Carpentry's [Unix Shell lesson](https://swcarpentry.github.io/shell-novice/) |
| Write a research script | Software Carpentry's [Python lesson](https://swcarpentry.github.io/python-novice-inflammation/) |
| Connect to a cluster | Alliance [SSH documentation](https://docs.alliancecan.ca/wiki/SSH) |
| Store or transfer data | Alliance [Storage and file management](https://docs.alliancecan.ca/wiki/Storage_and_file_management) |
| Submit or monitor a job | Alliance [Running jobs](https://docs.alliancecan.ca/wiki/Running_jobs) |
| Find installed software | Alliance [Available software](https://docs.alliancecan.ca/wiki/Available_software) |
| Run software in a container | Alliance [Apptainer documentation](https://docs.alliancecan.ca/wiki/Apptainer) |
| Improve resource requests | [Conquering the Scheduler]({{< ref "posts/conq_sched.md" >}}) |
| Get help on SHARCNET | [SHARCNET training](https://helpwiki.sharcnet.ca/wiki/Training) and the [SHARCNET FAQ](https://helpwiki.sharcnet.ca/wiki/FAQ) |

## I am new to the command line

Start with [The Unix Shell](https://swcarpentry.github.io/shell-novice/) from Software Carpentry. It teaches the Bash skills used throughout most cluster documentation: navigating directories, working with files, combining commands, and writing small scripts.

You do not need to become a Bash expert before using a cluster. You do need to recognize paths, commands, options, environment variables, and error messages.

## I need to write or automate an analysis

Python is the most common language I recommend to researchers. Start with Software Carpentry's [Programming with Python](https://swcarpentry.github.io/python-novice-inflammation/) lesson. It covers the language well enough to begin turning a manual analysis into a script.

Python is not required for every HPC workload. If your field already uses R, Software Carpentry also has an [R for Reproducible Scientific Analysis](https://swcarpentry.github.io/r-novice-gapminder/) lesson. Compiled programs and specialized research software are common on clusters too.

## I need to connect or move files

Learn [Secure Shell, or SSH](https://docs.alliancecan.ca/wiki/SSH) to connect to a remote system. For file transfers, check your provider's instructions before choosing a tool. Small transfers, large datasets, and files shared between institutions may need different methods.

On Alliance systems, start with [Storage and file management](https://docs.alliancecan.ca/wiki/Storage_and_file_management). It explains where files belong and links to supported transfer tools. Storage areas differ in speed, backups, quotas, and how long files are kept. Do not treat every directory as interchangeable.

## I need to run a job

Shared clusters use a scheduler rather than letting everyone run long computations on the login node. [Slurm](https://slurm.schedmd.com/overview.html) is widely used. A Slurm job describes the program to run, its expected runtime, and the CPUs, memory, or GPUs it needs. The scheduler decides when and where it runs.

For Alliance systems, use [Running jobs](https://docs.alliancecan.ca/wiki/Running_jobs) to learn how to submit a job, check its state, cancel it, and read its output. Start with a small test. Check that the result is correct and inspect the resources it used before submitting many jobs or requesting more hardware.

Slurm documentation can be long and its flags can be arcane. A coding agent is good at explaining a command, translating a goal into scheduler options, or helping interpret an error message. Verify its answer against your cluster's documentation and the command's built-in help before running it.

## I need software for my job

First check whether the cluster already provides the program. Alliance users can search [Available software](https://docs.alliancecan.ca/wiki/Available_software) and learn how environment modules select software versions.

Use a language-specific environment when your project needs packages that the cluster does not provide. Containers become useful when modules and ordinary environments cannot reproduce the full software setup. Alliance systems support [Apptainer](https://docs.alliancecan.ca/wiki/Apptainer), which is designed to run containers on shared HPC systems.

## I do not know what resources to request

Begin with the smallest reasonable CPU, memory, GPU, and time request. Run a representative test, inspect what it used, and adjust. Larger requests do not automatically make a job faster, and they can leave a job waiting longer for suitable hardware.

The Alliance guide to [allocations and compute scheduling](https://docs.alliancecan.ca/wiki/Allocations_and_compute_scheduling) explains how resource requests affect scheduling. Once basic submission makes sense, [Conquering the Scheduler]({{< ref "posts/conq_sched.md" >}}) introduces ways to think about job configurations and the hardware available on a cluster.

## I use DRAC or SHARCNET

The Digital Research Alliance of Canada documentation is the main reference for national systems:

- [Getting started](https://docs.alliancecan.ca/wiki/Getting_started) covers accounts, connecting, available systems, jobs, software, and storage.
- The [Alliance technical documentation wiki](https://docs.alliancecan.ca/wiki/Technical_documentation) is the reference to search when you have a specific task.
- [SHARCNET training](https://helpwiki.sharcnet.ca/wiki/Training) lists self-paced courses, new-user sessions, and other training.
- The [SHARCNET FAQ](https://helpwiki.sharcnet.ca/wiki/FAQ) explains access and support, including how to ask staff for help.

Use those pages for current hostnames, policies, limits, and support details. These change, and the official documentation should be the source of truth.
