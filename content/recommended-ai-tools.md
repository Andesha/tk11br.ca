---
title: "Recommended AI Tools"
description: "Opinionated buying guidance for AI tools and services."
date: 2026-09-23T00:00:00-04:00
---

This page is my current reference for AI tools. Check the date before relying on it. This space changes a lot in a short time.

## How I choose

Typically, I open up Pi and coordinate my tasks based on GitHub issues via the Matt Pocock skills. GPT 6 Sol on low is my daily driver. I only raise the reasoning level for really hard work. For long-running tasks with lots of context, I've started reaching for Opus 5.5.

These recommendations assume you're using a subsidized subscription plan. Paying API rates for all your day-to-day agent work gets too expensive. Check what's actually included in your plan before making an expensive model your default.

## Harnesses

1. [Pi](https://github.com/earendil-works/pi): My daily driver. It ships as a bare skeleton without extensions. The cool part is that its own documentation and code are available in its context, so it can modify itself. Say you want a modern "goal" or "btw" feature like the ones in Codex or Claude Code. You ask Pi to build it, and it will. Pi is really meant for enthusiasts who want aggressive control over everything. These are the extensions I use:
   * add dir: Symlinks other directories into your context.
   * web search: Self-explanatory.
   * power bar: Shows token use, context stats, and more in a toolbar below the prompt line.
   * ask user question: A rip-off of Claude's questions feature.
   * goal light: My own super-lightweight goal and loop framework.
   * prompt stats: My own summary of the current system prompt and tools.

2. [T3 Code](https://t3.codes/): More of an orchestration platform. It lets you combine all your subscriptions and get away from the terminal, making it easier to copy and paste screenshots, text blocks, and so on. It also has very cool remote access support. You can start a session from your phone and run it across a bunch of different machines. Claude and Codex have similar features, but T3 is better at working with a distributed fleet of machines.
   * It is open source, so you can change things pretty easily.
   * As soon as they add Pi support, I would daily-drive this.

3. [Codex](https://openai.com/codex/): If you already have a ChatGPT subscription, start here. It has the best "computer use" skills on the market right now. You can have it control Chrome or other apps on your computer to find buried settings and handle similar tasks. I don't use it much anymore unless I need to fill out a ton of online forms or do something like that.

4. [Cursor](https://cursor.com/): This was my entry point into the space. It started as a VS Code fork with advanced AI features, though it does lots of other things now. I appreciate that Cursor customizes its prompts and harness settings for every model you select. It is also a good starting point.

5. [Claude Code](https://claude.com/product/claude-code): The Claude models are amazing, but both the desktop app and the TUI feel a bit dated by my standards. Many of the killer features they pioneered now exist in the tools above, along with more interesting additions.

## Models

I don't think a strict ranking captures how I use these. Here's what I reach for and why:

* **GPT 6 Sol:** My daily driver in Pi on low. So far it feels like a straightforward upgrade over GPT 5.6 Sol, including better default prose without writing skills. Low is enough for most tasks. I only turn up the reasoning for really hard ones.
* **Astra:** The first model release that genuinely surprised me. Without being asked, it spun up multiple Playwright browsers to test and compare its work and recorded video to show it had finished. It can overengineer open-ended tasks, though, and it costs too much for me to use every day.
* **Fable:** Excellent at producing code I can trust and merge. If I give it a huge, nearly impossible task, it comes back to me when stuck instead of burning tokens forever. Plan access and cost keep it from being my default, especially when Sol on low is usually good enough.
* **Opus 5.5:** My choice for long-running tasks that need lots of context. It feels fast, and its prose is much better than earlier Opus releases. Opus 5 was a flat no for me, 4.8 was alright, but Sol 5.6 beat it easily.
* **Cursor's models:** A good way to try a variety of models without building my setup. Cursor tunes the experience for its models, and I'd still suggest it as a starting point.

I haven't used Luna 6 yet, so I can't recommend it either way. Local models have their place, but they're beyond the scope of this page.

## Outside coding

I replaced a self-hosted Hermes setup for my curated daily news brief with Grok Bot. It did the job better for me, without requiring me to host something I considered potentially risky. That's a recommendation for that particular job, not a coding-model ranking.

## Skill packages

I use only two major skill sets. I use one almost in full and took what I wanted from the other. I also create one-offs for certain projects when it makes sense, but those aren't really shareable.

1. [Matt Pocock's Skills](https://github.com/mattpocock/skills)
   * A great way to hand the project management side over to agents.
   * Grilling and Wayfinder are amazing for exploring ideas and putting them into issue trackers.
   * The instructional content and docs are really good.
   * Try adopting as much of this as you can, minus the obviously goofy skills, and give Wayfinder a shot.

2. [pstack, aka Poteto Mode](https://github.com/cursor/plugins/tree/main/pstack)
   * The writing skills are awesome, especially Unslop.
   * It has more skills and workflows for working with parallel agents.
