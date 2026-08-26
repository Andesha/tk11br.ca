---
title: "Turning a MATLAB EEG Pipeline Into a Container"
subtitle: "A small proof of concept for sharing battle-tested analysis code"
description: "A proof of concept using MATLAB Compiler, MATLAB Runtime, and Docker to package an EEGLAB analysis pipeline for another platform."
date: 2026-08-26T15:03:45-04:00
draft: false
tags: ["MATLAB", "Docker", "eeg", "workflow"]
---

A MATLAB analysis pipeline can be battle-tested and still be difficult to share. The code can work, but the next platform may have the wrong MATLAB version, missing dependencies, or no MATLAB installation at all.

I put together a small [MATLAB container template](https://github.com/Andesha/matlab-container-template) to show that you don't necessarily need to rewrite the analysis to solve this. MATLAB supports compiling a standalone application and packaging it as a Docker image. The deployed application runs with MATLAB Runtime rather than a full MATLAB installation.

## The proof of concept

The example is an EEGLAB pipeline that loads a `.set` file, crops it to a time window, calculates power in five frequency bands, and writes the result to CSV. It isn't meant to do much, it's just enough to provide context.

The first step is to keep the analysis in an ordinary MATLAB function and test it inside MATLAB. The repository includes a known-good CSV so the result can be checked after every packaging step.

A thin command-line wrapper then validates the four expected arguments and calls the pipeline. That wrapper becomes the application's entry point. MATLAB Compiler builds it with one command:

```matlab
buildResults = compiler.build.standaloneApplication( ...
    'eeglab_psd_cli.m', ...
    'ExecutableName', 'eeglab_psd_app');
```

MATLAB can then package that build as a Docker image with another command:

```matlab
compiler.package.docker(buildResults, ...
    'ImageName', 'eeglab-psd-app');
```

The final test mounts the sample data as read-only, mounts a separate output directory, runs the image, and compares the new CSV with the known-good result.

## The boring problem that still matters

File permissions were the main gotcha in this example. The application can run correctly and still fail because its output path isn't writable inside the container. Pipelines with an existing directory structure, such as BIDS workflows, need the same check for every location they write to.

That isn't specific to MATLAB, but it is easy to miss when the analysis itself has worked for years.

## This is already an option

It was cool to see how little custom machinery it needed. The MATLAB Compiler and its Docker packaging support make container deployment a first-class path, not a workaround someone has to invent from scratch.

Now, a working MATLAB pipeline doesn't always need to become platform-independent source code with a new installation story. It may only need a clear command-line entry point, a known-good result, and a container.

The [template repository](https://github.com/Andesha/matlab-container-template) has the complete functions and commands. The code snippets really are most of the process.
