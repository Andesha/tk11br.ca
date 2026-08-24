---
title: "Revisiting Cookiecutter in the Age of Coding Agents"
subtitle: "Do project templates still earn their keep?"
description: "A practical comparison of Cookiecutter PyPackage, a coding agent, and using both to build a modern Python package."
date: 2026-08-24T12:00:00-04:00
draft: false
tags: ["python", "Cookiecutter", "agents"]
---

A few years ago, I used Cookiecutter to show how to get from `import blah` to `pip install blah`.

This sounds simple, but it isn't. A Python script can live almost anywhere, but a formal package needs the right structure to be built into a wheel. It needs dependency metadata, versions, releases, a licence, and some way to test that it still works.

Cookiecutter gave us a standard template. Instead of remembering every file and setting and creating them manually, we answered a few questions and started with a working package. I gave [a talk about that workflow in 2022]({{< relref "teaching-python-packaging-cookiecutter.md" >}}).

Personally, I stopped shipping tools that needed it, so I stopped thinking about Cookiecutter. Recently, I needed to package something again, and an obvious question came up. Why use a project template when I can ask an agent to build the project?

## A small comparison

For comparison, I used the same throwaway project for each attempt. It's a small package called `csv-summary`. All it does is read a CSV file, summarize its numeric columns, and provide a `csv-summary` command. I also wanted tests and enough infrastructure to install, check, version, and release the package.

I tried three different options:

1. [`cookiecutter-pypackage`](https://github.com/audreyfeldroy/cookiecutter-pypackage) without an agent
2. An agent starting from an empty directory
3. The Cookiecutter project followed by the same agent

I did this with one prompt, not a benchmark. The goal was to see what each approach considered a finished package and where I would have to step in and fix things.

## Cookiecutter by itself

Cookiecutter has changed a lot since my 2022 talk. The current template uses `uv`, Ruff, pytest, `ty`, and GitHub Actions. `uv` wasn't even mainstream until late 2024. The template now includes workflows for continuous integration, documentation, CodeQL, and publishing to PyPI with trusted publishing. It also has Dependabot configuration, release tooling, security documentation, and a changelog.

This is a lot more infrastructure than this example needed, but that's pretty much the trade-off for Cookiecutter. The opinionated set of files is great, but if the package is truly small, this is overkill.

## The agent by itself

Starting from an empty directory, the agent produced the leanest project. It chose Polars, added a `src` layout, wrote two focused tests, configured Ruff and pytest, built both a wheel and source distribution, and checked them with Twine.

The agent also stopped at a fairly light definition of "done." Releases used a documented sequence of `uv`, Hatch, and Twine commands. There was no continuous integration, automated PyPI publishing, documentation site, dependency updater, or security scanning.

This is pretty much what you'd want for a small internal tool. It's less convincing as the default for a package that other people will depend on.

The prompt had asked for release infrastructure, but the agent gave me a workable manual process. Cookiecutter gave me a repeatable and automated one.

A better prompt could have asked for every missing piece. Of course, writing that prompt means knowing which pieces to request.

## Cookiecutter followed by the agent

The combined approach produced the most complete result. Cookiecutter supplied the project policy, while the agent spent its time implementing the package. Its formatting, linting, type checks, tests, and package build all passed.

The agent went further with the combined example. It added a minimum version for `pandas`, locked the resolved dependencies, and discussed which Python versions to support.

Cookiecutter had already handled much of what my prompt requested. The agent had less setup work to do, so it spent more time on package-specific decisions than it did in the empty-directory test.

## Templates still have a job

In general, an agent is good at doing the work in front of it. A maintained template is good at recording work that is easy to forget.

That difference is important. I can ask an agent to create CI, configure trusted publishing, pin GitHub Actions, add release notes, and set up documentation. I can also forget to ask for one of those things at any stage.

Cookiecutter records those decisions in files that have been used and tested together. With a template, the agent's job is smaller. It doesn't need to invent a release process or choose a documentation system. It can focus on other things, such as the consequences of a dependency or which Python versions to support.

There are concerns, of course. A Cookiecutter template can get out of date. A technology can fall out of style while the template keeps generating it. You could even argue that the whole thing could be a Markdown file or an agent skill. Still useful for a beginner, though!

## What I would use

For a small internal script that only needs to be installable, I would just let an agent drive. There's no need for all the extra GitHub features.

For a package that I plan to publish and maintain, I would start with Cookiecutter and then give the generated project to an agent. Cookiecutter would provide the boring, repeatable decisions. The agent would adapt them and run with it.

Interesting to see how far we have come in just a few years.
