---
title: "Projects"
description: "Selected research software, workflow, and HPC projects."
---

A few of the things I work on, in and around High Performance Computing. Most are open source; the rest live inside SHARCNET / Digital Research Alliance of Canada infrastructure.

## ViewClust

A Python package for computing and visualizing usage metrics on Slurm-based HPC clusters. Originally built at SHARCNET to standardize how cluster utilization was measured across analyst dataframes; now also used by collaborators at WestGrid, Calcul Québec, and MILA. Companion package `ViewClust-Vis` adds a set of summary figures.

- Source: <https://github.com/Andesha/ViewClust>
- Companion: <https://github.com/Andesha/ViewClust-Vis>

## PyLossless

Python tooling for reproducible EEG preprocessing and quality-control workflows. Aimed at making the pre-analysis steps of EEG studies auditable and easy to re-run as data and pipelines evolve.

## EEGStudyFlow

Workflow patterns and tooling for managing EEG studies end-to-end &mdash; from raw recordings, through preprocessing and quality control, to analysis-ready outputs that researchers can hand off without re-deriving state.

## SHARCNET analytics

Internal analytics and operational-insight work supporting research computing systems and the people who use them: usage forecasting, fairshare investigations, scheduler tuning, and ad-hoc deep-dives into cluster behaviour.
