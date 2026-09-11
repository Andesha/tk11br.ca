---
title: "Your KPIs Aren't Telling You Enough"
subtitle: "Measure failure in a way that helps someone act"
description: "Uptime percentages and other headline KPIs can hide which capabilities failed, who was affected, and what an organization should do next."
date: 2026-09-11T10:30:00-04:00
draft: false
tags: ["metrics", "workflow"]
---

Is GitHub down if the website loads but GitHub Actions doesn't work? Technically, no. A lot of GitHub is still available. You can browse, review things, and push a commit. But if your release process depends on Actions, a big piece of GitHub is absolutely down for you.

The same thing happens with clusters. The login nodes might be available while storage is having problems. Most of the compute nodes might be healthy while one GPU partition is offline. The owners can truthfully say that the cluster is up, while a researcher can say that they can't do their work.

This is the problem with a lot of key performance indicators. The number may be correct, but it isn't telling you enough.

## Availability isn't really binary

Uptime is often presented as a percentage. A service was available 99.9% of the month. That sounds precise, and chasing additional "nines" can be worthwhile when failures are expensive.

It still leaves most of the useful questions unanswered.

Was there one long outage or dozens of short ones? Did the outage affect everyone, or did the same group of users get hit repeatedly? Did it happen overnight or during the busiest part of the week? Was the whole service unavailable, or only one capability?

Even the word "available" needs a definition. A cluster that lets me log in but can't read my data isn't meaningfully available for my job. A source-code platform without its build system might work for one developer and block another completely.

## Power companies have better questions

Power reliability is an interesting comparison because the outcome seems as binary as it gets. The lights are either on or off.

Utilities don't stop at reporting the percentage of time that power was available. Standard reliability measures also ask how often customers experienced interruptions, how long those interruptions lasted, and how long restoration took. These are commonly reported through measures such as SAIFI, SAIDI, and CAIDI, defined in the [IEEE guide for electric power distribution reliability indices](https://standards.ieee.org/ieee/1366/7243/).

Those measures describe different failure shapes. One neighbourhood losing power repeatedly is different from a rare system-wide interruption. A short outage is different from one that lasts all afternoon. Those differences matter to customers, and they suggest different work for the power company.

Software and research infrastructure need the same kind of thinking. "How available were we?" is less useful than asking:

- Which capabilities failed?
- How many people were affected?
- How often did they experience a failure?
- How long were they unable to continue their work?
- How quickly did we restore the capability they needed?

Now the KPI is starting to describe a problem someone can investigate and can help improve their service.

## Keep chasing nines, but explain them

There is nothing wrong with a reliability target. If a service supports critical work, the difference between 99.9% and 99.99% availability may be a really big deal. Consider banking versus Outlook. Both important, but one needs to be up way more than the other.

This doesn't tell us whether the target covers every part of the service. What about planned maintenance? Included or not?

These aren't necessarily fake numbers. They are answers to too basic of questions.

## Start with the job of the KPI

Before publishing a KPI, I think we should ask three questions:

1. **What is this KPI supposed to describe?** Name the service, capability, or outcome instead of relying on a broad label such as availability or responsiveness.
2. **What user experience does it actually represent?** Define who and what is included, what counts as failure, and what the summary number might hide.
3. **What are we supposed to do when it changes?** A useful KPI should help someone decide where to investigate or whether to act.

That context can live in a footnote. It might also require a few supporting measures instead of one headline percentage. The format matters less than admitting that the number has boundaries.

A KPI isn't useful because it makes performance look easy to summarize. It is useful when it describes failure clearly enough that we can do something about it.