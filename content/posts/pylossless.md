---
title: "PyLossless"
subtitle: "Making EEG preprocessing easier to run at scale"
description: "Python tooling for reproducible EEG preprocessing and quality-control workflows."
date: 2026-05-05T00:00:00-04:00
draft: false
tags: ["python", "eeg", "preprocessing", "PyLossless"]
---

In April 2025, I wanted to put [PyLossless](https://github.com/andesha/pylossless) on the DRAC clusters as an official module. I had at least half a dozen datasets to clean, and I was still managing many projects with separate virtual environments. Reinstalling the same preprocessing package for every dataset made no sense.

It turned out that PyLossless was already available as a module. When I asked the internal team to update it, they gave me a list of changes they wanted first, especially if I planned to develop it myself. That request turned into active stewardship of the project and, eventually, co-ownership of its official repository.

Since then, I have touched pretty much every part of the project. I made it easier to install on HPC systems, replaced the old quality-control dashboard, simplified the configuration and rejection policy, and threw out a lot of stuff that was no longer helping anyone. Some of that cleanup was long overdue. Some came from watching researchers use the pipeline and finding the places where it made their lives harder for no good reason.

Since March 18, 2025, that has meant 92 commits, 87 changed files, 2,532 insertions, and 17,535 deletions. I am much happier about the deletions than the additions. PyLossless needed fewer moving parts before it needed more features.

## Making PyLossless practical on HPC

The original goal was simple. I wanted one maintained installation on DRAC instead of installing another copy for every project.

Packaging got in the way first. I removed `setup.py` and moved the package metadata and dependencies into `pyproject.toml` using `setuptools.build_meta`. PyLossless now declares Python 3.12 or newer and has an optional dependency group for the QC tools:

```toml
[project.optional-dependencies]
qc = [
    "jupyterlab",
    "PyQt5",
    "mne-qt-browser @ git+https://github.com/Andesha/mne-qt-browser.git@enable-qc"
]
```

That made EasyBuild much happier, which meant I could actually get the package installed on the cluster.

I also consolidated the requirements files. The old project split its dependencies across separate files for QC, tests, and Read the Docs. The replacement `requirements.txt` is a pinned environment export, with versions such as MNE 1.9.0, MNE-BIDS 0.16.0, NumPy 1.26.4, and PyQt5 5.15.11. It is not the prettiest requirements file, but it gives the HPC build a reproducible environment. The normal package requirements still live in `pyproject.toml`.

The documentation now includes the actual Narval setup and the batch workflow I use: a Python entry point, a job script, and a shell script for submitting a dataset. A generic installation page would not have helped much here. People needed to see how to run the thing on the cluster they actually had.

PyLossless had also assumed that every input already belonged to a BIDS dataset. That was too strict for some of the work people brought me. I added `non_bids_save()` and adjusted the save path so users can write derivatives without beginning with an existing BIDS path. BIDS remains useful, but it no longer blocks the rest of the pipeline.

## Replacing the QC dashboard

Once installation was in better shape, I moved on to quality control. I wanted grad students to review the pipeline's decisions without fighting the interface. I also missed some of the visual marking tools from earlier versions.

The project had a Dash application spread across `app.py`, `mne_visualizer.py`, `qcgui.py`, and `topo_viz.py`, along with its own assets, tests, and utilities. I removed it rather than trying to repair two QC systems at once.

Its replacement lives in `pylossless/qc.py`. It loads a processed derivative, shows the pipeline state, plots independent components and topographies, records interactive review decisions, and applies them through `RejectionPolicy`. The basic workflow is now:

```python
pipeline = ll.LosslessPipeline()
pipeline = pipeline.load_ll_derivative(...)
rejection_policy = ll.RejectionPolicy()
review = ll.QC(pipeline, rejection_policy)
review.run()
cleaned_raw = review.apply_qc()
```

This was also one of my first big AI-assisted development projects. I used AI while working through the interactive plots, click behaviour, difference views, and the connection between saved decisions and `RejectionPolicy`. It was most useful for the annoying little interaction problems. I could try something, find the awkward bit, and take another run at it. The QC work deserves its own post, so I will leave the full story for later.

I also added diagnostic plots earlier in the pipeline. The noisy-channel, noisy-epoch, and ICA noisy-epoch stages can now show the criteria used to mark data. That lets a researcher see what a threshold did instead of treating artifact rejection as a black box. Noisy ICA epoch flags are separated by run as `BAD_LL_noisy_ICs_1` and `BAD_LL_noisy_ICs_2`, and both ICA runs use a fixed random seed of 5184.

## Choosing fewer defaults

User feedback exposed another avoidable complication. PyLossless shipped separate adult and infant default configurations, even though most users needed one clear starting point.

I replaced them with `pylossless/assets/ll_default_config.yaml`. `Config.load_default()` no longer asks for `kind="adults"` or `kind="infants"`. Researchers can still change the settings for their data, but the package no longer pretends that two bundled files cover the meaningful differences between populations.

The rejection policy also had behaviour that was either broken or too implicit. I changed the default channel-cleaning mode from `None` to `"interpolate"`, added optional post-cleaning high-pass and low-pass filters, and made the policy load the raw data before applying rejection. It now recomputes the average reference after channel cleaning and again after ICA cleaning. Configuration loading updates dictionary keys rather than setting attributes, and `repr()` reports the post-filter settings.

These defaults reflect how I think the pipeline should behave. If a channel is already marked bad, I usually want it interpolated. If the data changes, I want the reference recomputed against the data that is still there. Users can override all of this, but the defaults should at least agree with each other.

## Removing what the project could not support

A large part of this work was deletion.

The repository still contained unfinished documentation, stale notes, broken examples, and notebooks that no longer represented the pipeline. I removed them and rewrote the README around the current package: its assumptions, processing stages, installation, QC dependencies, build check, and HPC workflow. I also removed old Codecov and Read the Docs badges and changed links from the previous fork to the current repository.

One especially painful find was an actual EEG recording committed as test data. It made every clone much larger. I removed the sample BIDS data along with the dataset and simulation utilities that depended on it. Real recordings do not belong in the package just because the tests need something to run against.

I also removed GitHub Actions, Dependabot, the pre-commit setup, Read the Docs configuration, and Codecov. I know removing CI sounds backwards. The project did not have a test suite I trusted, though, so most of that automation was checking stale assumptions. I would rather admit the gap than keep a collection of official-looking green badges around.

The old package tests went with the code they exercised. I replaced them with a smaller top-level suite built around EEG quality, ICA quality, signal-to-noise ratio, artifact reduction, and basic pipeline execution. The new tests still need work, but their measurements are closer to the questions I care about than the previous file-by-file checks.

This cleanup made the repository smaller and easier to install, but deletion was not the goal by itself. Each removal narrowed the project to code and documentation that I was prepared to maintain.

## What remains unfinished

PyLossless is easier for me and other researchers to install, run, and review than it was when I requested that module update. It is not finished.

The documentation still needs another pass beyond the README and HPC examples. I want to compare PyLossless against other EEG preprocessing pipelines instead of relying on internal metrics. The tests need to cover more than basic builds and a handful of signal-quality measures. Once I trust those tests, I will bring CI back.

For now, PyLossless is smaller, easier to install, and less fussy about how a dataset reaches it. The workflow also looks a lot more like the way people around me actually clean EEG data. They run it on shared infrastructure, check what the automated stages marked, make their review decisions, and save the result. That was what I needed when I first asked for the DRAC module update, so I am pretty happy with where it landed.
