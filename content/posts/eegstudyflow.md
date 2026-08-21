---
title: "EEGStudyFlow"
subtitle: "An opinionated starting point for a new EEG study"
description: "A working template that guides students and supervisors through the decisions behind a reproducible EEG study."
date: 2026-05-05T00:00:00-04:00
draft: false
tags: ["python", "eeg", "bids", "workflow", "EEGStudyFlow"]
---

Starting an EEG study means making dozens of small decisions. Where will the original recordings live? How will they become a BIDS dataset? Which software environment will the study use? Where does preprocessing end and analysis begin?

A student has to answer these questions before they've had enough experience to know what the consequences will be. Their supervisor then has to review those answers, remember what everyone decided, and figure out whether the project can still be reproduced two years later.

A classic example is storing processed files by stage. Unless you remember exactly what ran and in what order, you can end up with a tree of files and lose the plot completely. Good luck reproducing an error from somewhere in the middle of that.

[EEGStudyFlow](https://github.com/Andesha/EEGStudyFlow) is my opinionated answer. It's a working template and an educational example for running an EEG study. I've made these decisions many different ways, and the repository records the defaults I now trust. A new student shouldn't have to rediscover every bad option firsthand.

## One repository per study

When you start a study, clone EEGStudyFlow and rename the new copy. That's now the study's source of truth. The student works through it as the study develops, and the supervisor can come back to the same place to see how the data were imported, processed, and analyzed.

The notebooks follow the study instead of being a pile of disconnected code examples. They cover:

- testing the Python environment and plotting setup
- inspecting a source recording before settling on an import process
- initializing a BIDS study from the original files
- preprocessing the recordings with [PyLossless](https://github.com/Andesha/pylossless)
- running a traditional event-related potential analysis across participants

Each step gives the next one a known structure. Raw source files stay separate from the BIDS dataset, and processed derivatives stay separate from both. The instructions and analysis live beside the study without getting mixed into the recordings.

When someone asks which script ran, when the filtering happened, or which subjects were rejected, you can find the answer inside the study. It documents itself as you work.

## Opinionated on purpose

EEGStudyFlow doesn't try to list every valid way to run an EEG study. That would recreate the problem it's meant to solve. It gives students a path they can trust and supervisors a common starting point for teaching and review.

The notebooks don't hide the decisions behind a single command. Students can see what happens when the source data become BIDS, what PyLossless produces, and what the analysis consumes. They can learn the workflow while using it, then come back when they reach the next stage of the study.

The detailed explanations live in the repository, close to the code they describe. The short version is this: if you're starting an EEG study and don't yet know which setup decisions will matter later, clone EEGStudyFlow before making them. If you supervise EEG students, it gives you one place to send them and one place to check their work.

It's what I would've wanted when I first started.
