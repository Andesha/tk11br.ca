---
title: "Check what your AI plan does with your data"
subtitle: "Paying for an AI tool doesn't mean your sessions are excluded from training"
description: "The OpenAI Navier–Stokes announcement is a good reason to check whether your AI plan allows your sessions to be used for model training."
date: 2026-09-09T13:00:00-04:00
draft: false
tags: ["agents", "workflow"]
---

There is a lot of drama around OpenAI's claimed solution to the Navier–Stokes existence and smoothness problem. I'm not going to try to evaluate the proof or untangle the dispute around it. One sentence near the bottom of [OpenAI's announcement](https://openai.com/index/navier-stokes-solution/) was very interesting to me:

> While unlikely, we cannot rule out that de-identified data derived from their usage of our products helped improve our models.

Anyone using an AI tool for research stop and check their plan.

## What happened here?

Tristan Buckmaster and Levent Alpöge had been using several language models while working on fluid dynamics problems. In [Buckmaster's statement](https://cims.nyu.edu/~tristanb/statement.pdf), he says their collaboration was personal rather than an official project of either researcher's employer. He also says he paid for the tools from his research funds, including "footing a large bill to OpenAI."

OpenAI says it didn't see their work before producing its own proof. It also says it cannot completely rule out de-identified data from the researchers' product usage having helped improve its models.

That doesn't prove their work was used for training. It definitely doesn't prove OpenAI's result came from it. But the fact that nobody can rule it out is the part worth carrying into your own work.

## Paying isn't the same as opting out

It's easy to assume that paying for an AI tool makes your sessions private. That isn't necessarily how the product works.

OpenAI's [current explanation of its data practices](https://openai.com/policies/how-your-data-is-used-to-improve-model-performance/) says content from individual services such as ChatGPT may be used to train its models. You can opt out, after which new conversations won't be used for training. Temporary Chats aren't used for training either.

Its business products and API are different. OpenAI says it doesn't train on their inputs and outputs by default. Customers have to explicitly opt in.

This isn't about simply free versus paid, or OpenAI versus another company. It can be between two plans sold by the same company. Other AI providers have their own products, defaults, controls, and terms.

## Go check

I use these tools constantly. This announcement made me check my own settings, and I think you should do the same.

For every AI service you use:

1. Check which product and plan your account is actually on.
2. Find out whether conversations, uploaded files, coding sessions, and feedback can be used to improve models.
3. Turn off model training where that option exists.
4. For unpublished, sensitive, or competitive work, use a product whose data terms actually match what you need.

Don't assume that paying is enough. Don't assume that a setting in one product applies to every product from the same company. And don't wait until your work is part of the biggest research story of the week to find out what you agreed to.
