---
title: "Writing More Code with AI Agents"
subtitle: "Use AI slop to verify code you already trust"
description: "A practical way for researchers to use AI coding agents for tests, checks, and diagnostic work without handing over the scientific decisions."
date: 2026-08-27T12:00:00-04:00
draft: false
tags: ["talk", "agents", "hpc", "workflow"]
---

I recently gave a SHARCNET General Interest Webinar called "Writing More Code with AI Agents." More than 300 people registered. Attendance was excellent, there were lots of questions, and I've had a decent number of follow-up conversations over email. Pretty happy with how it turned out!

The response also confirmed why I wanted to give the talk. People are constantly asking me agents and what they should be doing with them. They're watching other researchers and developers move very quickly with these tools, and there's a real fear of missing out. They want to try them, but they don't necessarily know where to start or how much of the output they should trust.

My answer is to start with code you already trust, then put some AI slop around it.

<iframe src="https://www.youtube.com/embed/06jylC7Sib0" title="Writing More Code with AI Agents" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The rest of this post are my thoughts about the various points I bring up during the talk.

## The title was a bit of a lie

The title says you should write more code. This is technically true, but it depends on what we count as code.

Most researchers don't need an agent generating more of the main scientific loop. That is the meat and potatoes of the project. It includes the cleaning rules, statistics, simulations, models, and transformations that can change the result. The researcher needs to understand and own those decisions.

A lot of useful code lives outside that loop:

- tests and synthetic examples
- input validators
- diagnostic plots and reports
- logging and debugging tools
- profiling scripts
- build and release automation
- documentation

People tend to skip this stuff. It takes time, some of it is boring, and it may require programming knowledge that isn't directly related to the research question. It is also exactly the work that can make the main analysis easier to trust.

The title I really wanted was "Use AI agents to write slop to verify your code." It probably wouldn't have attracted 300 registrations.

## I asked Claude to do my stats

I built a synthetic reaction-time study for the talk. It had 48 participant files and a 2x2 repeated-measures design. Each participant should have completed four conditions with 80 trials in each condition.

Of course, the data wasn't actually that clean. One file duplicated an existing participant under a new acquisition ID. Two participants didn't finish. Some had near-chance accuracy. Others had reaction times that were implausibly fast or slow.

All of these are normal research-data problems. They're also serious enough that letting those files contribute to the final result would be wrong.

I gave the data to Claude three times.

For the first attempt, I used this prompt:

> These CSV files are the results from my experiment. Do my stats for me and make a plot I can use in my paper.

This is a terrible prompt on purpose. Claude still produced a polished plot and a significant interaction with a p-value of 0.040. It looked like a finished analysis.

It turns out it had invented an accuracy exclusion, picked its own reaction-time summary, allowed comically large response times, and included incorrect trials. There were decisions all over the place that the researcher didn't make and might not even notice.

The result was blatantly wrong, but it looked nice.

Never do this.

## A better prompt still wasn't enough

For the second attempt, I explained the study design. I described the factors, outcome, repeated-measures analysis, hypothesis, and how incorrect trials should be handled.

The code improved. Claude gave a more conservative p-value of 0.087. It also showed hints that it could produce useful checks around the analysis.

This is probably where a lot of people stop. The response knows the terminology, the figure looks good, and the result feels more defensible because the prompt was detailed.

There were still problems in the data that anyone familiar with the study would want to investigate. More context made the output better, but good prompting did not replace experience or domain knowledge.

This is also why I'm not especially interested in advice that boils down to "write a huge prompt." Context is useful. It does not prove that the code handled the real files correctly.

## Own the logic and delegate the annoying parts

For the third attempt, I supplied the core statistical code myself. It came from previous work, and I understood what it was doing. Claude wasn't asked to choose the analysis.

Instead, I asked it to write the surrounding checks. Report any of the missing four conditions. Report files with too few trials, high error rates, or reaction times outside the plausible range. Check participant identities. Show me potential failures.

This found all eight problematic subjects, including the duplicate participant. After reviewing and handling those cases, the analysis used 40 participants and returned the expected interaction with a p-value of 0.037.

The third attempt was better because I owned more of the important code, not because Claude suddenly became more trustworthy. The agent took criteria I supplied and turned them into reports and checks. That gave me things I could inspect before accepting the result.

**This is the kind of AI-generated slop I want more of.**

If a validator is a bit ugly but catches a duplicate participant, great. If a throwaway plot makes a broken distribution obvious, it did its job. If an alternate implementation disagrees with my main calculation, I now have something worth investigating.

None of that code needs to become permanent infrastructure. Its job is to answer a question or provide evidence.

## This works outside toy statistics

The same idea fits notebooks, shared pipelines, and SLURM jobs.

For a notebook, an agent can add data-shape checks, diagnostic cells, caching, or a small script that tests code pulled out of the notebook. For a shared pipeline, it can validate inputs, produce reports, or turn a previously discovered failure into a regression test. For a SLURM workflow, it can add preflight checks, logging, resource summaries, checkpoints, and checks that distinguish a complete output from a partial one.

The stakes change as the work gets larger. A bad notebook cell might waste an afternoon. A bad cluster job might wait in the queue for days, consume a large allocation, and leave partial files that look usable. Catching the same mistake before submission is much cheaper.

There are also obvious limits. Don't upload data unless you're allowed to. Run unfamiliar generated code in a sandbox, container, or virtual machine. Keep a human involved when mistakes can affect results, people, infrastructure, or budgets. You own the problems even when an agent wrote the code.

## Try one check

Don't start by giving an agent a new analysis and hoping it gets everything right.

Take a script, notebook, or pipeline that you've already used enough to understand. Something battle-tested. Ask the agent to add one check that doesn't touch the meat and potatoes.

You could ask for a synthetic case where you know the answer. Ask it to verify that every participant has the expected conditions. Have it make an exclusion report, plot a suspicious distribution, or write a second version of a calculation so you can compare the outputs.

Review what it writes. Run it. See whether it tells you anything useful about code you already know.

That is a much safer way to learn what agents are good at, and it produces something useful even if the generated code is disposable. The point isn't to trust AI more. The point is to cheaply make more of the stuff that helps you trust the important work.
