---
title: "Start your five-hour window early"
subtitle: "Weekly is the real budget"
description: "How Claude and Codex five-hour and weekly limits reset, and why an early-morning ping can get you a fresh window by lunch."
date: 2026-10-14T12:00:00-04:00
draft: false
tags: ["agents", "workflow"]
---

I hate when you sit down to work at 9:30 after clearing emails, send your first prompt, and by 1pm you're out of usage. The window doesn't come back until 2:30, so you lose an hour and a half of the afternoon waiting on a timer.

To be clear, there are actually two limits here, and they do pretty different jobs. The five-hour window controls when you can use your plan. The weekly cap controls how much you get in total. Most people worry about the five-hour one because it's the wall they keep hitting, but in my opinion the weekly cap is the real budget.

## How the windows work

On Claude Pro and Max, the five-hour session starts with your first message. It's a rolling window, not a fixed clock time, and it resets five hours after that first message. The weekly limit is separate. It resets at a fixed time for your account, and waiting out a session won't clear it. Chat, the desktop and mobile apps, and Claude Code all draw from the same pool.

Codex is split by plan. Plus and Standard Business have a five-hour window. Pro [currently has none](https://learn.chatgpt.com/docs/pricing). Weekly limits "may also apply," and OpenAI's docs send you to your usage dashboard for the actual reset times rather than spelling them out.

Neither provider really counts messages. Model choice, context length, reasoning effort, and tool use all change how fast you burn through a window. A long agent session in a big repo with a top model eats through it way faster than a handful of chat questions for each of them though.

These rules change a lot, so check your own numbers instead of trusting a blog post, this one included. In Claude Code, `/usage` shows your session and weekly bars. In Codex, `/status` shows both percentages and when they reset.

## Start the clock before you sit down

The five-hour clock starts on your first message, so you get to pick when it starts. If something sends a message at 7am, your first window closes at noon and you get a fresh one right after lunch. Now the morning is one window and the afternoon is another, instead of one window running right through the middle of your day.

The simplest version is pretty much just a ping. Most agent tools have a headless mode, so a cron job can send a throwaway prompt to a cheap model:

```
0 7 * * 1-5 claude -p "Reply with OK" --model haiku
```

`codex exec "Reply with OK"` does the same for Codex. Cron runs with a bare environment, so you may need the full path to the binary. A local cron job also only fires if your machine is on at 7am.

The nicer version is to have that early job do something useful. Most of the modern tools can run scheduled tasks, so set up a custom news brief. Have it cover what changed in the repos you care about, release notes for your tools, or whatever you'd otherwise skim over coffee. It starts the clock as a side effect, and you have something to read when you sit down.

## The catch

This doesn't ever raise your weekly cap. It gives you a second full window during your working hours, so you can burn through that cap faster. If you were already finishing most weeks with headroom, that's a good trade. If you regularly hit the weekly wall on Thursday, you'll hit it on Wednesday instead. Be careful.

## What about peak hours?

For a while earlier this year, the time of day you used Claude mattered too. Weekday mornings from 5 to 11am Pacific drained five-hour sessions faster than the rest of the day. Anthropic [removed that reduction](https://www.anthropic.com/news/higher-limits-spacex) for Claude Code on Pro and Max in May, and doubled Claude Code's five-hour limits at the same time. Weekly limits didn't double.

So off-peak usage isn't worth more on Claude Code right now. Providers have done it before, though, and could easily do it again, so check whether it applies to your plan before you plan your day around it.

## What I'd do

If the afternoon wall is what keeps getting you, try the early ping or a morning brief. Just keep an eye on that weekly bar!

## Related posts

- [Why I still use Sol on low]({{< relref "why-i-still-use-sol-on-low.md" >}})
