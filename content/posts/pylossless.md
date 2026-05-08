---
title: "PyLossless"
subtitle: "TODO: LOREM IPSUM"
description: "Python tooling for reproducible EEG preprocessing and quality-control workflows."
date: 2026-05-05T00:00:00-04:00
draft: false
tags: ["python", "eeg", "pylossless"]
---

In April 2025 I had the idea to get [PyLossless](https://github.com/andesha/pylossless) put onto the DRAC clusters as an official module due to needing to clean at least half a dozen different datasets. At the time I managed a lot of my projects with virtual environments PER project, so this was going to involve reinstalling the same package over and over.

Funnily enough, the module was already there! When I requested it be updated by the internal team, they said they had a few things that they'd like changed about it, especially if I was going to be doing active development on it myself.

This lead to my active stewardship of the project and becoming a co-owner on the project's official repository.

The rest of this blog post is dedicated to the work I have since done on the project up to today to make it more HPC friendly, user friendly, documented, easy to containerize, and more. 

Since March 18th 2025, there have been **92 commits**!

- **87 files changed**
- **2,532 insertions**
- **17,535 deletions**

# Major repo changes since then

Since I took over for Scott Huberty, here's a rough list of my changes:

- HPC usability
- simplified installation
- modern `pyproject.toml` packaging
- removal of old Dash dashboard, CI, docs, examples, and bundled data
- a new QC implementation in `pylossless/qc.py`
- simplified default configuration
- improved/manual rejection workflow
- diagnostic plotting
- non-BIDS save support
- new metric-oriented tests rather than the original test suite

The following subsections will go over things in more detail.

### 1. First pass of cosmetic changes

There were a lot of "in progress" things in the documentation as well as TODOs that had been completed. This was a first easy step.

- README rewritten to describe this as an **HPC-ready lightweight fork**.
- Links and install instructions changed from `lina-usc/pylossless` to `Andesha/pylossless`.
- Original badges for Codecov and ReadTheDocs were removed.
- Many old TODOs, notes, test scripts, and extra materials were removed.

### 2. CI / CD removed

Personally, while I know CI/CD is very important, the project in my opinion wasn't quite ready for this before we had official tests.

Deleted GitHub and project automation files:

- `.github/dependabot.yml`
- `.github/workflows/build_doc.yml`
- `.github/workflows/check_linting.yml`
- `.github/workflows/pypi.yml`
- `.github/workflows/test_pipeline.yml`
- `.pre-commit-config.yaml`
- `.readthedocs.yaml`
- `codecov.yml`

### 3. Documentation and examples heavily changed

Previous documentation was really dated. In included examples that didn't work anymore that were also bloating the repository. I chose to take all of this out, and rewrite it.

Removed old examples and notebooks:

- `examples/plot_0_implementation.py`
- `examples/plot_10_run_pipeline.py`
- `examples/test_config.yaml`
- `examples/usage.py`
- `notebooks/pipeline_algorithms.ipynb`
- `notebooks/qc_example.ipynb`

Added/expanded README content for:

- pipeline assumptions
- pipeline stages
- installation
- QC dependencies
- running a simple build test
- HPC/Narval environment setup
- sample HPC workflow using `main.py`, `job.sh`, and `run_all.sh`

Added test documentation:

- `tests/documentation.md`

### 4. Test data and simulated datasets removed

A classic issue that needed fixing, here. Someone had accidentally committed an actual recording file slowing down cloning by a huge amount. Ripping this out helped tons.

Deleted bundled sample/test BIDS data under:

- `pylossless/assets/test_data/...`

Deleted dataset utilities:

- `pylossless/datasets/__init__.py`
- `pylossless/datasets/datasets.py`
- `pylossless/datasets/simulated.py`

### 5. Dash dashboard removed

My next intention was to improve the quality control procedure to be easier to use for grad students, and bring back some of the past Vised Marks features. First step was of course to remove the old ones.

The old Dash-based QC/dashboard implementation was removed entirely:

- `pylossless/dash/app.py`
- `pylossless/dash/mne_visualizer.py`
- `pylossless/dash/qcgui.py`
- `pylossless/dash/topo_viz.py`
- related Dash tests/assets/util files

### 6. New QC system added

Incidentally, this was one of the first major AI assisted projects I ever worked on. I'll really leave this up to its own blog post to tell the full story but everything turned out really great.

A new QC module was added:

- `pylossless/qc.py`
- loading and applying local rejection files
- inspecting pipeline state
- plotting IC/topographic review views
- interactive click behavior
- scroll/difference plotting
- applying QC decisions through `RejectionPolicy`

README now shows usage like:

```python
pipeline = ll.LosslessPipeline()
pipeline = pipeline.load_ll_derivative(...)
rejection_policy = ll.RejectionPolicy()
review = ll.QC(pipeline, rejection_policy)
review.run()
cleaned_raw = review.apply_qc()
```

### 7. Config system simplified

Just a simple bit of feedback from a user here. It was pointed out to me there really should just be one default config.

Default config changed from adult/infant variants to one config:

- Renamed:
  - `pylossless/assets/ll_default_config_adults.yaml`
  - to `pylossless/assets/ll_default_config.yaml`
- Deleted:
  - `pylossless/assets/ll_default_config_infants.yaml`

`Config.load_default()` no longer accepts `kind="adults"` / `kind="infants"`.

Now it just loads:

```python
pylossless/assets/ll_default_config.yaml
```

### 8. Default config changed

This section is a little downplayed, but mainly included support for being able to see that effect of your artifact rejection parameter choice in the first stage of the pipeline. It was another big AI win.

Notable config changes include:

- diagnostic plotting flags added:
  - `noisy_channels.plot_diagnostic`
  - `noisy_epochs.plot_diagnostic`
  - `ica.noisy_ic_epochs.plot_diagnostic`
- ICA random seed fixed:
  - `random_state: 5184` for both ICA runs
- default channel cleaning mode later changed to interpolation through rejection policy behavior
- default adult/infant split removed

### 9. Pipeline behavior changed

Already mentioned it in the previous section, but this was really about plotting the criteria function outcomes. Also as a result of some more user feedback it became a priority to add some less firm assumptions around BIDS requirements.

Important changes in `pylossless/pipeline.py`:

- Import changed from:

```python
from .config import Config
```

to:

```python
from .config.config import Config
```

- `_detect_outliers()` gained a `plot_diagnostic` option that can display diagnostic plots.
- IC noisy epoch flags are now separated by ICA run:
  - old: `BAD_LL_noisy_ICs`
  - new:
    - `BAD_LL_noisy_ICs_1`
    - `BAD_LL_noisy_ICs_2`
- `flag_noisy_ics()` now takes a `run_id`.
- Added `non_bids_save()` helper for saving derivatives without starting from an existing BIDS path.
- Several pipeline comments/TODOs were removed.
- Save behavior got a workaround for non-BIDS save use cases.

### 10. Rejection policy changed

There were some bugs in the RejectionPolicy class. This phase fixed them, and also added my own assumptions.

`pylossless/config/rejection.py` received several functional changes:

- Default `ch_cleaning_mode` changed from `None` to `'interpolate'`.
- Added post-cleaning filter options:
  - `post_filter_l_freq`
  - `post_filter_h_freq`
- `raw.load_data()` is now called before applying rejection.
- Average reference is recomputed after channel cleaning and again after ICA cleaning.
- Config file loading logic was changed to update dict keys instead of setting attributes.
- `__repr__()` now reports post-filter settings.

### 11. Build / packaging modernized

This was small, but very big for the HPC side. From this point on things worked better with EasyBuild.

`setup.py` was deleted.

`pyproject.toml` now contains modern package metadata:

- build backend: `setuptools.build_meta`
- package name/version:
  - `pylossless`
  - `0.2.0`
- Python requirement:
  - `>=3.12`
- dependencies moved into `[project]`
- added optional QC dependency group:

```toml
[project.optional-dependencies]
qc = [
    "jupyterlab",
    "PyQt5",
    "mne-qt-browser @ git+https://github.com/Andesha/mne-qt-browser.git@enable-qc"
]
```

### 12. Requirements changed significantly

Similar to the previous, EasyBuild now no longer had trouble resolving dependencies.

`requirements.txt` changed from a short abstract dependency list to a large pinned environment export.

Original style:

```txt
numpy>=1.21.2
mne>=1.7
mne_bids>=0.14
...
```

New style includes many pinned packages, including:

- `mne==1.9.0`
- `mne-bids==0.16.0`
- `mne-icalabel==0.7.0`
- `numpy==1.26.4`
- `torch==2.6.0`
- `jupyterlab==4.4.0`
- `PyQt5==5.15.11`
- custom `mne-qt-browser` Git dependency

Deleted separate requirement files:

- `requirements_qc.txt`
- `requirements_rtd.txt`
- `requirements_testing.txt`

### 13. Tests replaced / reorganized

This was inspired by reading some artifact rejection benchmarks. It needs more polish but functions as a nice minimal test suite.

Old package tests were removed:

- `pylossless/tests/test_pipeline.py`
- `pylossless/tests/test_rejection.py`
- `pylossless/tests/test_simulated.py`
- `pylossless/tests/test_utils.py`

New top-level tests and metrics files added:

- `tests/artifact_reduction_metrics.py`
- `tests/ica_quality_metrics.py`
- `tests/snr_metrics.py`
- `tests/test_eeg_metrics.py`
- `tests/conftest.py`

These appear focused on EEG quality metrics, ICA quality, SNR, artifact reduction, and pipeline run/build validation.