---
title: "Revisiting Cookiecutter in the Age of Coding Agents"
subtitle: "Do project templates still earn their keep?"
description: "A practical comparison of Cookiecutter PyPackage, a coding agent, and using both to build a modern Python package."
date: 2026-08-24T12:00:00-04:00
draft: true
tags: ["python", "Cookiecutter", "agents"]
---

A few years ago, I used Cookiecutter to show how to get from `import blah` to `pip install blah`.

This sounds simple buit it isn't. A Python script can live almost anywhere, but a formal package needs a proper structure to be built into a Wheel. It needs dependency metadata, versions, releases, a licence, and some way to test that it still works.

Cookiecutter gave us a standard template. Instead of remembering every file and setting and creating them manually, we answered a few questions and started with a working package. I gave [a talk about that workflow in 2022]({{< relref "teaching-python-packaging-cookiecutter.md" >}}).

Personally, I stopped shipping tools that needed it, so I stopped thinking about Cookiecutter. Recently, I needed to package something again, and an obvious question came up. Why use a project template when I can ask an agent to build the project?

## A small comparison

For comparison, I used the same throwaway project for each attempt. It's a small package called `csv-summary`. All it does is read a CSV file and summarizes its numeric columns, plus a `csv-summary` command. I also wanted tests and enough infrastructure to install, check, version, and release the package.

I tried three different options:

1. [`cookiecutter-pypackage`](https://github.com/audreyfeldroy/cookiecutter-pypackage) without an agent
2. An agent starting from an empty directory
3. The Cookiecutter project followed by the same agent

I did this with one prompt, not a benchmark. The goal was to see what each approach considered a finished package and where I would have to step in and fix things.

## Cookiecutter by itself

Cookiecutter PyPackage has changed a lot since my 2022 talk. The current template uses `uv`, Ruff, pytest, `ty`, and GitHub Actions. `uv` wasn't even really mainstream until late 2024. What's nice is it now includes workflows for continuous integration, documentation, CodeQL, and publishing to PyPI with trusted publishing. It even has Dependabot configuration, release tooling, security documentation, and a changelog.

This is a lot more infrastructure than this example needed, but that's pretty much the trade-off for Cookiecutter. The opinionated set of files is great, but if the package is truly small, this is overkill.

## The agent by itself

Starting from an empty directory, Claude (Opus 5) produced the leanest project. It chose Polars, added a `src` layout, wrote two focused tests, configured Ruff and pytest, built both a wheel and source distribution, and checked them with Twine.

The agent also stopped at a fairly light definition of "done." Releases used a documented sequence of `uv`, Hatch, and Twine commands. There was no continuous integration, automated PyPI publishing, documentation site, dependency updater, or security scanning.

This is pretty much what you'd want for a small internal tool. It's less convincing as the default for a package that other people will depend on.

The prompt had asked for release automation, but the agent gave me a workable release process instead. Cookiecutter gave me a repeatable and automated one.

A better prompt could have asked for every missing piece. Of course, writing that prompt means knowing which pieces to request.

## Cookiecutter followed by the agent

The combined approach produced the most complete result. Cookiecutter supplied the project policy, while the agent spent its time implementing the package. Everything passed as you would expect.

What was nice was that the agent went further with the minimal example and pinned dependency versions for things like `pandas`, and also chatted about what Python version to support.

I expect that since Cookiecutter did a lot of what my prompt outlined, the agent had less to do and took some liberties to go a step or two further than the raw agent test did.

## Templates still have a job

In general, an agent is good at doing the work in front of it. Additionally, a maintained template is good at noting work that is easy to forget.

That difference is important. I can ask an agent to create CI, configure trusted publishing, pin GitHub Actions, add release notes, and set up documentation. I can also forget to ask for one of those things at any stage.

Cookiecutter PyPackage records those decisions in files that have been battle tested. With these templates, the agent's job smaller. It did not need to invent a release process or choose a documentation system. It could focus on other things, like the consequences of dependencies or Python versioning support.

There are of course concerns. Things like Cookiecutter can get out of date, technologies can fall out of style but the original maintainer keeps it in... There's tons of things that could happen. You could even argue that this entire thing could just be a markdown file or a skill. Still useful for a beginner though!

## What I would use

For small internal scripts that only needs to be installable, I would just let an agent drive. There's no need for all of the fancy GitHub features or other considerations.

For a package that I would be publishing and maintaining, I would start with Cookiecutter and then give the generated project to an agent. Cookiecutter would provide the boring, repeatable decisions and then the agent would adapt them and run with it.
