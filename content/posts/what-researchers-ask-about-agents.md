---
title: "What researchers ask about agents"
subtitle: "Questions from the SHARCNET intro to ARC sessions, and the answers I keep giving"
description: "Most questions at Tuesday's intro to ARC session were about trust and verification, not which model is smartest. The answers are mostly old research habits."
date: 2026-11-12T09:00:00-05:00
draft: false
tags: ["agents", "workflow"]
---

I taught at SHARCNET's intro to ARC sessions on Tuesday, and the questions were pretty much the same ones I get every time. Almost nobody asked which model is smartest. They asked whether they could trust it, how to set it up, and where it falls over. Those are good questions, and in my opinion most of the answers are research habits people already have. So here are my answers, written down once.

## Can I trust it?

### How do I run agents safely?

Put it somewhere it can't hurt you. If you're nervous, my first suggestion is to spin up a VM and let an agent loose on a toy project. You get to watch what it actually does without anything real on the line. After that, run it in a container or a VM and keep your code in git, so any mistake is one revert away. Have it confirm anything that's hard to undo or that leaves your machine, and keep git operations behind your approval. Also check [what your AI plan does with your data]({{< relref "check-what-your-ai-plan-does-with-your-data.md" >}}) before you point an agent at anything sensitive.

### How do I check its work?

Have a different model review it. A model reviewing its own work has the same blind spots it had while writing it, so asking it again kind of gets you the same answer back. I wrote more about this in [get a second opinion from another model]({{< relref "get-a-second-opinion-from-another-model.md" >}}).

### Is TDD worth it with agents?

Yes. A test is a spec the agent can check itself against, so it's the cheapest way to know the code does what you asked. Write the test first, watch it fail, then let the agent make it pass. The `tdd` skill from Matt Pocock's set walks the agent through exactly that loop.

### Can I use AI to find things in my data?

Sure, but anything it finds is always a hypothesis. Using an agent to fish through a dataset is fine as exploration. The finding still has to be replicated with another study or data the agent never saw, same as it always did. The catch is that agents make fishing really cheap. Ask enough questions of one dataset and you'll find something every time, which is pretty much the textbook setup for a result that doesn't replicate.

## How do I set it up?

### What goes in AGENTS.md?

Start with almost nothing. Add a line each time the agent gets something wrong that it couldn't have known, like site policy or the way your lab lays out data. Skip what the model already knows like SLURM commands, etc. I went through this for the Alliance clusters in [writing an AGENTS.md for a national cluster]({{< relref "writing-an-agents-md-for-a-national-cluster.md" >}}).

### What skills do you use?

Mostly [Matt Pocock's skills](https://github.com/mattpocock/skills), plus the writing skills from [pstack](https://github.com/cursor/plugins/tree/main/pstack). The details are on my [recommended AI tools]({{< relref "recommended-ai-tools.md" >}}) page.

### Should I run multiple agents in worktrees?

Only when you need to. They're useful, but every extra agent is more output for you to review. Start with one, and reach for parallel agents in their own worktrees once you actually have independent work to hand out.

## Where does it fall over?

### Why did my bio research get a worse model?

Requests in bio fields can get downgraded to older models by the guard rails. My advice is to keep your questions on the software side. You own the research anyway. Ask the agent to write the preprocessing script or fix the plotting code, and leave the biology to you.

### How good are open models?

They were very good. It looks like anti-distillation techniques are working, though, and open models have fallen behind by at least six months. They're still solid for a lot of work.

## Part two

The second half of the session is tomorrow, and I'll be presenting some new things. See you there!

## Related posts

- [Writing an AGENTS.md for a national cluster]({{< relref "writing-an-agents-md-for-a-national-cluster.md" >}})
- [Get a second opinion from another model]({{< relref "get-a-second-opinion-from-another-model.md" >}})
- [Your research isn't Navier–Stokes]({{< relref "your-research-isnt-navier-stokes.md" >}})
