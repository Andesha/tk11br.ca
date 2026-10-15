---
title: "Your LLM Loop Is a Batch Job"
subtitle: "Don't forget about classic HPC"
description: "800,000 small requests in a day slows a shared LLM service down for everyone. If your workload looks like that, a batch job on a GPU node will finish sooner."
date: 2026-10-15T12:00:00-04:00
draft: false
tags: ["hpc", "scheduling", "llm"]
---

Today I had to rate limit a user on SHARCNET's internal LLM service for the first time. In the last 24 hours they had sent about 800,000 requests, and every single one was under 500 tokens.

To be clear, they didn't do anything wrong. The service is set up to let them do it. They had a pile of small work and a working endpoint, so they wrote some sort of loop. I probably would have done the same. But a loop that sends hundreds of thousands of tiny prompts is a batch job, and this was a really good reminder of why batch clusters are still super important.

## What that load does to a shared service

A shared LLM endpoint is set up for lots of people asking questions here and there, interactive use. One person sending 800,000 of them back to back is a pretty different workload. Spread over a day, that's roughly nine requests per second, all day and all night.

Every one of those requests costs something before the model even sees it. Each is a network round trip with its own connection overhead and its own spot in the queue. It also messes with caching. Inference servers lean on caches to keep things quick for the people already using them, and a steady flood of unrelated prompts pushes that useful state out. Time-to-first-response goes up for everyone, including the person asking a single question in a chat window who did nothing different.

## Why a batch job is faster

On a GPU node in a batch job, you get the whole device to yourself. Nobody else's traffic is in the queue, and there's no network between your data and the model.

The bigger win is how the work gets handed over. Offline inference with a tool like [vLLM](https://docs.vllm.ai/) takes the entire list of prompts at once and packs them onto the GPU as tightly as it can. Small prompts are where that pays off most, because one small prompt on its own leaves most of the GPU idle. Hand it 800,000 together and it keeps the device busy the whole time. You load the model once, point it at your dataset, and collect the results when the job ends.

## If this is you

If your workflow loops over a dataset and calls an LLM once per row, please don't forget about classic HPC. Write it as a batch job, run it on a GPU node, and keep the shared service for the interactive stuff it's good at.

You'll get more done quicker, and everyone else gets their response times back!

## Related posts

- [Serial Farms: Package Options and When to Switch to Farming]({{< relref "serial-farms.md" >}})
