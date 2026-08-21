---
title: "ViewClust: Early Days"
subtitle: "And its cousin ViewClust-Vis!"
description: "Early notes on packaging ViewClust and ViewClust-Vis for cluster metrics and HPC usage analysis."
date: 2022-03-22T13:23:54-04:00
draft: false
tags: ["python", "hpc", "ViewClust"]
---

In the early days of working for [SHARCNET](https://www.sharcnet.ca/my/front/), my colleague and I decided to standardize how cluster metrics were computed across our internal data frames. As mentioned in a [previous post](/posts/pandas1/), part of the solution was pandas.

The second part was figuring out how to deploy the package for others to contribute to, as well as install on their own specific HPC clusters. Some quick searching revealed that [PyPI](https://pypi.org/) and [`pip`](https://pip.pypa.io/en/stable/) were the way to go.

To make a long story short, here are a few references that made it approachable:

- [Editable/interactive mode for pip](https://pip.pypa.io/en/latest/cli/pip_install/#cmdoption-e).
- [Cookiecutter](https://cookiecutter.readthedocs.io/en/1.7.2/).
- [Virtual environments](https://docs.python.org/3/tutorial/venv.html).

The package is still in use today inside SHARCNET and has also received development support from [WestGrid](https://www.westgrid.ca/), [Calcul Québec](https://www.calculquebec.ca/en/), and [MILA](https://mila.quebec/en/).

ViewClust can be found on [GitHub](https://github.com/Andesha/ViewClust). Its cousin package, [ViewClust-Vis](https://github.com/Andesha/ViewClust-Vis), implements several summary figures.
