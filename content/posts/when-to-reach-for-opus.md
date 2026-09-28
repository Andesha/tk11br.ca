---
title: "When to reach for Opus"
subtitle: "Give it the ticket, not just the next step"
description: "Sonnet works well when I break down the work for it. For a whole feature ticket with decisions along the way, I'd try Opus."
date: 2026-09-28T12:00:00-04:00
draft: false
tags: ["agents", "workflow"]
---

After I updated my [model recommendations]({{< relref "why-i-still-use-sol-on-low.md" >}}), I got some feedback from people still reaching for Sonnet or models like Luna. I get it. If I'm breaking a job down and checking every step, Sonnet can get me pretty much the same result as Opus most of the time. But why am I doing all that planning for it? That defeats the purpose of a fully agentic approach. What I typically try to do with Opus is give it a wider task: give it the goal, let it work through the branches, and come back to review what it did.

Say I have a ticket to implement an entire feature branch. The agent has to read the existing code, decide what needs changing, deal with whatever it finds along the way, and test the result. With Sonnet, I'd expect to need to help break that into smaller jobs. I'd essentially be pair programming with Sonnet, with it controlling the keyboard. This is totally fine, but missing a lot of the strengths of the frontier models.

On the other hand, Opus is the one I'd try giving the whole ticket to. No single step has to be especially hard. The agent is just doing more on its own without steering. Maybe it finds that the existing tests don't cover the change, or that the first implementation needs work once it runs them. With Sonnet I'd expect to stop, look at that, and decide what to ask for next. With Opus I'd give it room to investigate and keep going. That's the difference I care about when I say "wide," not whether Opus writes a better line of code.

This isn't a claim that Sonnet can't implement the feature. If I'm there to break down the work and steer it, I'd expect it to do fine in the average case. Models like Sonnet and Luna have their place, but I wouldn't choose them for a job where I want to leave the agent alone to work through all those branches.

Of course, I still read the changes, run the tests, and check the result against the ticket. If the ticket involves decisions I need to own, I don't hand those over either. I just don't want to have to tell the agent what to do next every five minutes.

If you've only been giving agents small jobs, try giving Opus a whole ticket and see how far it gets. Then check its work.

## Related posts

- [Why I still use Sol on low]({{< relref "why-i-still-use-sol-on-low.md" >}})
