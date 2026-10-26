---
title: "Get a second opinion from another model"
subtitle: "Different models have different taste, so let them check each other's work"
description: "Models are tuned to write code differently. If you have the tokens, having one review another's work is basic hygiene, and personas take the idea further."
date: 2026-10-26T09:00:00-04:00
draft: false
tags: ["agents", "workflow"]
---

The best part of pair programming is pretty much just having someone else look at what you wrote. They notice the stuff you stopped seeing an hour ago. I wouldn't merge my own work without a review, so why would I let the model that wrote the code be the only one to review it? A model reviewing its own work has the same blind spots it had while writing it. It made its choices for reasons that still seem good to it, so asking it again kind of gets you the same thing back.

## Models have taste

Different models are tuned to write code in different ways. Give two of them (of relatively the same capability, of course) the same task and you'll get two different shapes back. One adds structure where the other would cut stuff. One treats a pattern as normal and the other flags it. Neither is always right. They just have different taste, the same way two senior devs on a team do. That's why a second opinion is worth having. A different model is more likely to question the stuff the first one took for granted.

## How I run it

I personally keep the reviews independent. Each model reviews the same project in its own worktree, so neither one sees the other's take before writing its own. Then I have one agent merge and deduplicate the findings into a single write-up, or a parent issue with sub-issues if there's real work to do. What's great about this is that you don't necessarily need any sort of fancy agent setup. Just two different terminal windows to get you started.

This does cost tokens. It's two full reviews instead of one. Personally, I think it's just good hygiene if you have the tokens to burn. If you finish most weeks with headroom on your [weekly cap]({{< relref "start-your-five-hour-window-early.md" >}}), this is a really good way to spend it. If you're paying API rates for every token, it's a harder sell. But then again, you're probably in enterprise with a code review product.

## Change the reviewer, not just the model

You don't always need a second model to get a second perspective. You can tell an agent to review the code as someone specific.

[Ponytail](https://github.com/dietrichgebert/ponytail) is a good example. It makes your agent think like the lazy senior dev who, in its README's words, "has been at the company longer than the version control" and replaces your fifty lines with one. Its `/ponytail-review` and `/ponytail-audit` commands review a change or a whole repo from that point of view.

The idea is really easy to extend. Have a security person read the code looking for what an attacker would try. Have a junior who just joined the team read it looking for what they can't follow. It's been very useful for me to get feedback on sections of code from perspectives I don't have by default. I don't naturally read my own code like an attacker, or like someone seeing it for the first time.

Next time you finish a change, hand it to a different model, or ask your agent to review it as someone who isn't you. Try it out yourself!

## Related posts

- [When to reach for Opus]({{< relref "when-to-reach-for-opus.md" >}})
- [Why I still use Sol on low]({{< relref "why-i-still-use-sol-on-low.md" >}})
- [Start your five-hour window early]({{< relref "start-your-five-hour-window-early.md" >}})
