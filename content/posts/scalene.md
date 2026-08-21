---
title: "Modern Approaches to Profiling in Python with Scalene"
subtitle: "Find the slow part before rewriting it"
description: "A practical introduction to profiling Python CPU, memory, and GPU use with Scalene on HPC systems."
date: 2023-05-03T12:00:00-04:00
draft: false
tags: ["talk", "python", "performance", "hpc"]
---

Before rewriting slow Python or moving it into Cython, it helps to find out what is actually slow.

This Compute Ontario Colloquium was an introduction to [Scalene](https://github.com/plasma-umass/scalene). Scalene separates time spent in Python from time spent in native libraries, and it can also profile memory and GPU use. I ran it on the Alliance systems from a Jupyter notebook, then compared native Python, vectorized code, Cython, and just-in-time compilation.

<iframe src="https://www.youtube.com/embed/Uq60vknROcM" title="Modern Approaches to Profiling in Python with Scalene" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Abstract

Python is a language developers choose to write in for convenience rather than speed. However, speed can be recovered by offloading calculations to libraries which leverage lower-level languages like NumPy, Cython, and more. Scalene is a high-performance CPU, GPU, and memory profiler which can illustrate where code should be passing calculations to other libraries for significant increases in speed. Scalene also includes support for Jupyter Notebooks, OpenAI suggestions for vectorizing code, as well as a significantly lower overhead and higher accuracy than other profilers. This talk will introduce the concepts required for understanding why external libraries are faster than native Python, interactions with approaches such as Cython and just-in-time compilers, as well as a live demonstration of Scalene on the Alliance systems inside of a Jupyter Notebook. Familiarity with Python, virtual environments, and Jupyter notebooks will be assumed.

The [slides, notebooks, and examples are available on GitHub](https://github.com/Andesha/sharcnet-scalene).
