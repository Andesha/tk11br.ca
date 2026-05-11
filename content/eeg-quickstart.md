---
title: "EEG Quickstart Guide"
description: "Starting points for reproducible EEG analysis workflows."
date: 2026-05-08T00:00:00-04:00
---

Often a fresh graduate student is assigned an EEG project with no idea where to start, or how many skills might be required. This page is an attempt to roughly quantify both the hard/soft skills as well as provide a reference as to where I send researchers to start their EEG quest.

A large amount of this information is duplicated in the README of [EEGStudyFlow](/posts/eegstudyflow/), but this page will provide some extended context.

## EEG Fundamentals

Unsurprisingly, theory is the first steppingstone.

1. [The Luck Textbook](https://mitpress.mit.edu/9780262525855/an-introduction-to-the-event-related-potential-technique/)
   - Does an excellent job of onboarding brand new researchers to EEG.
   - Introduces all the terms in a standard way.
   - Numerous additional resources online expand or reexplain sections if you are stuck.
   - Time commitment: roughly 20 to 30 focused hours to work through the book with notes. 
   - The book is about 370 pages, so this assumes technical reading at about 15 to 20 pages per hour, plus time to stop, look up terms.
2. [ERP Bootcamp](https://courses.erpinfo.org/courses/Intro-to-ERPs)
   - More of a coursework-focused approach than just a textbook.
   - Has video materials.
   - Includes quizzes to help check your progress.
   - Time commitment: a more curated experience to the above of around 15 hours of content.

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

The following are links to Software Carpentry platforms teaching the introduction to each language/concept:

- [Python](https://swcarpentry.github.io/python-novice-inflammation/)
  - Tons of support online for additional learning materials
  - Learning Python first can allow you to transition to other languages easily, the concepts generalize
  - Rich library support for DataFrames and anything else you can image
- [Bash/Shell](https://swcarpentry.github.io/shell-novice/)
  - If you need to automate things, or use command line interfaces, bash is a must
  - You must learn this if you are intending to use high performance computing resources
- [R](https://swcarpentry.github.io/r-novice-gapminder/)
  - Worth learning if your lab does advanced stats
  - If you ever intend to do things with the web, choose Python instead
  - Syntax and other concepts do not generalize well to other languages/platforms
- MATLAB
  - I no longer recommend MATLAB as a suggested language.
  - Reasons include:
    - Stand structures are MATLAB specific and do not transfer to other skills. For example, MATLAB's implementation of DataFrames is a Table and is barely functional.
    - Licensing is extremely annoying
    - Not open source
