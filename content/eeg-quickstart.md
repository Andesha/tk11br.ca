---
title: "EEG Quickstart Guide"
description: "Starting points for reproducible EEG analysis workflows."
date: 2026-05-08T00:00:00-04:00
---

New graduate students often arrive at an EEG project without knowing where to start or how many skills the work requires. This is the path I recommend.

1. Work through the Luck textbook or ERP Bootcamp to learn the basic EEG vocabulary.
2. Learn enough Python to read files, manipulate DataFrames, call functions, make plots, and understand error messages.
3. Try MNE-Python with real or example data. Inspecting recordings gives you a reason to keep learning Python.
4. Build a mock analysis for one subject from your project. Understand each step before you scale it up.
5. Learn Git before the analysis starts to grow.
6. Learn Bash if you need command-line tools, an HPC system, or an automated pipeline.
7. Generalize the analysis across subjects once the one-subject version is understandable and repeatable.
8. Keep revising the workflow as you learn.

This takes **months**. A novice does not learn Python or EEG analysis in a week.

## EEG fundamentals

Start with one of these:

1. [An Introduction to the Event-Related Potential Technique](https://mitpress.mit.edu/9780262525855/an-introduction-to-the-event-related-potential-technique/), often called the Luck textbook
   - My usual recommendation for someone new to EEG.
   - Budget about 20 to 30 focused hours for its roughly 370 pages. Stop to take notes and look up unfamiliar terms.
2. [ERP Bootcamp](https://courses.erpinfo.org/courses/Intro-to-ERPs)
   - A more structured course with videos and quizzes.
   - Budget about 15 hours.

Either route should give you enough vocabulary to discuss recordings, event markers, epochs, referencing, filtering, artifacts, ICA, experimental design, quality control, and subject-level analysis. You do not need to memorize every ERP component before opening a data file.

## Technical skills

Programming skill comes from practice. A university course gives students about 11 weeks to learn one language in a formal setting. Set your expectations accordingly.

- [Python](https://swcarpentry.github.io/python-novice-inflammation/) is my first recommendation. Learn to work with files, functions, DataFrames, plots, packages, and errors. Those skills transfer directly into MNE-Python and most scientific Python tools.
- [Bash](https://swcarpentry.github.io/shell-novice/) becomes necessary when you automate jobs or work on an HPC system. Learn paths, pipes, scripts, environment variables, and how to read logs.
- [R](https://swcarpentry.github.io/r-novice-gapminder/) is worth learning when your lab already relies on it for statistics or reports. Otherwise, I recommend Python first.
- MATLAB remains common in older EEG workflows, so you may need to read it. I no longer recommend it as a first language. Its licensing creates problems when students leave institutional access, and it is a poor default for work meant to be reproduced or redistributed.

## Software and workflow tools

Learn these while building the one-subject analysis. Reading about them without a real dataset will only get you so far.

- [BIDS](https://bids-specification.readthedocs.io/) gives EEG projects shared rules for file names, folders, metadata, events, participants, and derivatives. Learn it before your project invents an undocumented folder layout. Budget 3 to 6 hours for the basics.
- [Git](https://swcarpentry.github.io/git-novice/) tracks changes to scripts and configuration. Learn commits, branches, remotes, and how to compare versions. Budget 4 to 8 hours for the basics, followed by regular use until they stick.
- [MNE-Python](https://mne.tools/stable/index.html) reads, preprocesses, plots, and analyzes EEG data in Python. Budget 10 to 20 hours for its beginner material. A complete study-specific pipeline will take much longer.
- [EEGLAB](https://eeglab.org/) is useful when a lab or an older project already depends on it. Learn enough to inspect and reproduce those workflows. I would not choose it as the default for a new project.
