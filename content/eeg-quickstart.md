---
title: "EEG Quickstart Guide"
description: "Starting points for reproducible EEG analysis workflows."
date: 2026-05-08T00:00:00-04:00
---

Often a fresh graduate student is assigned an EEG project with no idea where to start, or how many skills might be required. This page is an attempt to roughly quantify both the hard/soft skills as well as provide a reference as to where I send researchers to start their EEG quest.

A large amount of this information is duplicated in the README of [EEGStudyFlow](/posts/eegstudyflow/), but this page will provide some extended context.

My standard suggested path looks like this:

1. Work through the Luck textbook or the ERP Bootcamp to build the basic EEG vocabulary.
2. Learn enough Python to read files, manipulate DataFrames, call functions, make plots, and understand error messages.
3. Try MNE-Python with real or example data so you can inspect recordings while getting more comfortable with Python.
4. Build a mock analysis for one subject from your current project. The goal is to understand each step before scaling up.
5. Learn Git for version control before your analysis starts to grow.
6. Learn Bash if you need to use command-line tools, high performance computing systems, or automated pipelines.
7. Generalize the single-subject analysis across all subjects once the one-subject version is understandable and repeatable.
8. Keep improving the workflow as you learn.

This will take **months**. It is not a fast process.

The sections below collect dedicated learning materials for each part of that path.

## EEG Fundamentals

Unsurprisingly, theory is the first steppingstone.

1. [The Luck Textbook](https://mitpress.mit.edu/9780262525855/an-introduction-to-the-event-related-potential-technique/)
   - Does an excellent job of onboarding brand new researchers to EEG.
   - Introduces all the terms in a standard way.
   - Numerous additional resources online expand or reexplain sections if you are stuck.
   - Time commitment: roughly 20 to 30 focused hours to work through the book with notes.
   - The book is about 370 pages, so this assumes technical reading at about 15 to 20 pages per hour, plus time to stop and look up terms.
2. [ERP Bootcamp](https://courses.erpinfo.org/courses/Intro-to-ERPs)
   - More of a coursework-focused approach than just a textbook.
   - Has video materials.
   - Includes quizzes to help check your progress.
   - Time commitment: roughly 15 hours for a more curated version of the same material.

You should be familiar with the following terms and concepts by the end of either of these:

- EEG, ERP, channel, electrode, montage, reference, impedance, and cap layout.
- Event markers, triggers, epochs, baseline correction, and trial averaging.
- Sampling rate, time window, latency, amplitude, peak amplitude, and mean amplitude.
- Signal-to-noise ratio, noise floor, artifacts, blinks, eye movements, muscle activity, line noise, and drift.
- Filtering, high-pass filters, low-pass filters, and notch filters.
- Artifact rejection, artifact correction, independent component analysis, and bad-channel interpolation.
- Common ERP components, including P1, N1, P2, N2, P3 or P300, N400, error-related negativity, and lateralized readiness potential.
- Experimental design basics, including condition coding, counterbalancing, randomization, stimulus timing, response timing, and trial counts.
- Data organization, raw data, derivatives, preprocessing logs, quality control reports, exclusions, and reproducibility.
- Statistical basics, including subject-level averages, grand averages, regions of interest, multiple comparisons, and preregistered analysis windows.

## Technical Skills

This is the toughest section. I cannot stress enough that programming skill is built through accumulated practice. Much like learning a new spoken language, the more time you spend with it, the better you get.

As context, the languages on this list are often given an entire dedicated course in a standard computer science degree. Someone who has chosen programming as an area of study usually gets 11 weeks, a standard Canadian semester, in a formal learning environment.

A novice does not "learn Python" in a week. If they do, they should probably be studying computer science.

The following links point to Software Carpentry introductions for each language or concept:

- [Python](https://swcarpentry.github.io/python-novice-inflammation/).
  - Python has a huge amount of online support, including tutorials, examples, package documentation, and troubleshooting threads.
  - Great first programming language because many core concepts transfer cleanly to other languages.
  - Python has library support for data frames, statistics, machine learning, visualization, web tools, and EEG analysis workflows.
  - My main recommendation.
- [Bash/Shell](https://swcarpentry.github.io/shell-novice/).
  - Bash is essential if you need to automate repetitive tasks, move files safely, run command-line tools, or understand what a pipeline is doing.
  - Required practical knowledge if you plan to use high performance computing resources.
  - Helps you understand file paths, environments, scripts, and logs, which makes debugging much easier.
- [R](https://swcarpentry.github.io/r-novice-gapminder/).
  - Worth learning if your lab already uses it heavily for statistics, reports, or visualization.
  - If you want to build web tools, automate general workflows, or work across many domains, choose Python first.
  - R syntax and some core concepts transfer less cleanly to other languages than Python does.
- MATLAB.
  - I no longer recommend MATLAB as a first language for new EEG researchers.
  - Still common in older EEG workflows, so you may need to read or maintain it in some labs.
  - MATLAB-specific data structures and habits do not transfer as well to other tools. For example, MATLAB's table support is not as flexible as the data frame tooling in Python or R.
  - Licensing is bad, especially for students who leave institutional access.
  - Not open source, which makes long-term reproducibility and redistribution harder.

## Software and Workflow Tools

This list is more software-specific. These are the tools and standards I would expect someone to recognize before they start managing a real EEG project.

- [BIDS Specification](https://bids-specification.readthedocs.io/).
  - BIDS defines a standard way to organize neuroimaging datasets, including EEG datasets.
  - It gives you shared expectations for file names, folder structure, metadata, events, participants, and derivatives.
  - Learning BIDS early prevents a common failure mode: every project inventing its own undocumented folder layout.
  - Time commitment: roughly 3 to 6 hours to understand the core ideas, and longer if you are converting an existing messy dataset.
- [Introduction to Git](https://swcarpentry.github.io/git-novice/).
  - Git introduces version control: how to track changes, recover old work, collaborate safely, and understand what changed between two versions of a project.
  - Git is also how most open source scientific software is distributed, so knowing the basics helps you download, inspect, and cite tools properly.
  - You do not need to become a Git expert immediately, but you should understand commits, branches, remotes, and pull requests.
  - Time commitment: roughly 4 to 8 hours for practical basics, plus repeated use before it feels natural.
- [MNE-Python](https://mne.tools/stable/index.html).
  - MNE-Python is a major Python ecosystem for reading, preprocessing, visualizing, and analyzing EEG, MEG, and related electrophysiology data.
  - It is a strong fit if you want scriptable, reproducible workflows that connect naturally to Python data science tools.
  - It has good documentation, examples, tutorials, and support for many file formats.
  - Time commitment: roughly 10 to 20 hours to become comfortable with the beginner tutorials, and substantially more to build a complete study-specific pipeline.
- [EEGLAB](https://eeglab.org/).
  - EEGLAB is a long-running MATLAB-based platform for EEG analysis.
  - It remains important because many labs, papers, plugins, and legacy workflows are built around it.
  - I would learn enough EEGLAB to understand existing lab pipelines, reproduce older work, and communicate with collaborators who use it.
  - I would not usually choose it as the first tool for a new researcher starting from scratch, for the same reasons I do not recommend MATLAB as a first language.

Feel free to contact me directly if you have any questions about this post or your own specific path!