---
title: "ViewClust: Early Days"
subtitle: "and its cousin ViewClust-Vis!"
date: 2022-03-22T13:23:54-04:00
draft: false
tags: ["python", "viewclust", "pip"]
---

In the early days of working for [SHARCNET](https://www.sharcnet.ca/my/front/), my colleague and I decided to standardize how cluster metrics were computed across our internal data frames. As mentioned in a [previous post](http://localhost:1313/posts/pandas1/), part of the solution was pandas.

The second part was to figure out how to deploy the package for others to contribute to, as well as install on their own specific HPC clusters. Some quick searching of course revealed [PyPi](https://pypi.org/project/pip/) and `pip` were the way to go.

To make a long story short, here's some references that made it super easy and approachable:

* [Editable/interactive mode for pip](https://pip.pypa.io/en/latest/cli/pip_install/#cmdoption-e)
* [Cookie cutter](https://cookiecutter.readthedocs.io/en/1.7.2/)
* [Virtual environments](https://docs.python.org/3/tutorial/venv.html)

The package is still in use today inside of SHARCNET and has also received development support from [WestGrid](https://www.westgrid.ca/), [Calcul Quebec](https://www.calculquebec.ca/en/), as well as [MILA](https://mila.quebec/en/).

ViewClust can be found on GitHub, [here](https://github.com/Andesha/ViewClust). Its cousin package ViewClust-Vis can be found [here](https://github.com/Andesha/ViewClust-Vis), which implements several summary figures.
