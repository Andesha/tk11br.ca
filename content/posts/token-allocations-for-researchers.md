---
title: "Grants will need a line for tokens"
subtitle: "A prediction about research funding, with all the usual caveats"
description: "More research money is going to LLM tokens. I predict Canadian granting agencies will add a token allocation tied to sovereign, safe infrastructure."
date: 2026-10-30T10:00:00-04:00
draft: false
tags: ["agents", "hpc"]
---

Predictions are of course dangerous. They're also pretty much impossible and random. Who saw that location services on cell phones would create Uber and lead to disruption in the taxi industry? VisiCalc was supposed to kill accountants, but we have even more of them now, they just do different stuff.

You should also beware anyone who predicts things like "here's why I'll be fine but everyone else is in trouble." With that out of the way, here's mine.

## Grant money is turning into token money

Researchers submit grant applications in terms of dollars for the research they want to do. Many now spend a chunk of that on tokens, and it's going past simple day-to-day interactive use. I run [Brine](https://docs.alliancecan.ca/wiki/Nibi#Brine:_AI-as-a-Service_platform), the AI-as-a-Service platform on Nibi, and more and more of the researchers I talk to want to [run real workloads]({{< relref "your-llm-loop-is-a-batch-job.md" >}}) through it, not just chat with it.

## Where those tokens go really matters

I've written before about [the Navier–Stokes announcement]({{< relref "check-what-your-ai-plan-does-with-your-data.md" >}}). Tristan Buckmaster paid for his AI tools out of research funds, and OpenAI couldn't rule out that data from that usage helped improve its models. Research money paid for those sessions, and the work in them potentially ended up available for training.

That makes picking a provider an ethics and safety question, not just a purchasing one.

## My prediction

I predict the granting agencies in Canada will have to make this part of their process. Something like NSERC, CIHR, and SSHRC adding an allocation for tokens as part of the funds, spendable on sovereign and safe setups, so the money they pay for research doesn't end up as someone's training data.

We kind of already do this for compute. Researchers don't buy a cluster with their grant, they apply to the Alliance for an allocation. Tokens are going to need the same treatment.

## What to do now

If you're a researcher, start tracking what you spend on tokens and which services that money goes to. If you're at an agency or in research computing, I'd rather we decide this on purpose than find out later what got decided by default.

Ask me again in a year to see how this one aged!

## Related posts

- [Check what your AI plan does with your data]({{< relref "check-what-your-ai-plan-does-with-your-data.md" >}})
- [Your LLM Loop Is a Batch Job]({{< relref "your-llm-loop-is-a-batch-job.md" >}})
- [What Does a GPU-Hour Actually Measure?]({{< relref "what-does-a-gpu-hour-actually-measure.md" >}})
