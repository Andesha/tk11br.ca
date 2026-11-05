---
title: "Your research isn't Navier–Stokes"
subtitle: "LLMs are cracked interns, and most research doesn't come with a spec"
description: "Navier–Stokes was close to the best possible problem for an AI agent. Most research doesn't look like that, so the specifying and checking is still your job."
date: 2026-11-05T10:00:00-05:00
draft: false
tags: ["agents", "workflow"]
---

We get a lot of questions about LLMs replacing researchers, or about swarms of agents doing research on their own. Navier–Stokes usually comes up as the proof. If a model can produce a claimed proof for a Millennium Prize problem, why would anyone need a grad student?

Jay Kruer's [Why I'm still bearish on LLMs after Navier-Stokes](https://dank.systems/posts/2026-09-15-ai-bear.html) is the best answer to that question I've read so far. I mostly agree with it, with one real sticking point.

## Navier–Stokes was the best case

Kruer's point is that Navier–Stokes is pretty much the best possible setup for an agent. The theorem statement is already a rigorous spec that is battle tested. Mathematicians have been checking it for decades, and it translates directly into Lean using well-tested objects from Mathlib. Lean itself is a verifier built so that bogus proofs can't sneak through. Even that isn't perfect, and he notes soundness bugs in theorem provers have let LLMs slip bogus proofs through before.

To me this means that Navier–Stokes is an optimal problem for an agent, HOWEVER not all research takes the shape of that problem. Furthermore, it took tons of time to get Navier–Stokes into a position like that. The agent showed up after decades of people making the problem checkable.

## The cracked intern

Kruer's model for where this leaves us is an LLM as a "cracked intern", quick and effective in the hands of an adult but not given run of the place. I really like this one, especially the idea that only certain tasks are perfect for this sort of thing. He argues models do well on narrow tasks that look like what they were trained on, and fail or reward hack when the task shifts a bit.

His fix is a rigorous spec written by someone who knows the domain, and that's expensive. His example is hardware, where a typical CPU project anecdotally has about three spec and validation engineers for every design engineer, and 5:1 isn't unheard of. Writing down exactly what "correct" means can cost more than doing the work.

## Where research fits

The author lists three kinds of firms that can let LLMs run fully on their own. Ones that can fail cheaply, ones with a small set of narrow tasks and guardrails already in place, and ones that already pay for rigorous specification and validation, like chip design and drug discovery. Research doesn't always fit cleanly into any of them. Exploratory work can fail cheaply. Anything going into a paper can't, and it usually doesn't come with a spec either.

EEG cleaning is a good example from my own work. When I [tried to write tests for whether EEG got cleaner]({{< relref "cleanliness-metrics-eeg-pipelines.md" >}}), several of my metrics rewarded rejecting everything. Nobody has an agreed definition of clean EEG to write a spec against, so I made up my own metrics, and the optimal answer for some of them was to just reject everything. That's exactly the kind of spec an agent will reward hack.

The reaction-time demo from my [Writing More Code with AI Agents]({{< relref "writing-more-code-with-ai-agents.md" >}}) talk went the other way. A more detailed prompt still missed the bad participant files. When I supplied the criteria for the study myself, the agent turned them into checks that found all eight.

## Where I disagree

Kruer thinks most firms won't need frontier models, and that cheap open models will do. I'd push back here. Frontier models are still strictly better because you can do wider things. You don't have to be doing that pair programming paradigm. With [Opus]({{< relref "when-to-reach-for-opus.md" >}}), I give it the whole ticket and come back to review what it did, instead of breaking the work into steps and checking each one.

That's still an intern. The frontier one just takes a bigger assignment before you check its work. Review doesn't go away, it happens less often and on bigger pieces, and you can stretch it further by having [a second model review the first]({{< relref "get-a-second-opinion-from-another-model.md" >}}).

## Ask two questions first

Before you hand a research task to an agent, ask what your spec is and who checks the output against it. If you can't answer, that part of the work is still yours, and it's where your expertise is worth the most.

Navier–Stokes got easy for an agent after decades of people making it checkable. Worth asking which parts of your own field have had that kind of work done.

## Related posts

- [Check what your AI plan does with your data]({{< relref "check-what-your-ai-plan-does-with-your-data.md" >}})
- [Grants will need a line for tokens]({{< relref "token-allocations-for-researchers.md" >}})
- [When to reach for Opus]({{< relref "when-to-reach-for-opus.md" >}})
- [What Should EEG Cleaning Improve?]({{< relref "what-should-eeg-cleaning-improve.md" >}})
- [Writing More Code with AI Agents]({{< relref "writing-more-code-with-ai-agents.md" >}})
