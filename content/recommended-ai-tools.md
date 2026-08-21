---
title: "Recommended AI Tools"
description: "Opinionated buying guidance for AI tools and services."
date: 2026-05-12T00:00:00-04:00
---

This page is my current reference for AI tools. Check the date before relying on it. This space changes a lot in a short time.

## How I choose

Typically, I open up Pi and coordinate my tasks based on GitHub issues via the Matt Pocock skills. If the task is particularly difficult or involves design/prose/taste then I swap over the task to Opus 4.8 in T3 Code.

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

This is subjective, but my ranking is:

1. GPT 5.6 Sol (OpenAI)
   * I use this in Pi on "low" every day. I rarely reach for anything else.

2. Opus 4.8 (Anthropic)
   * I reach for this when writing large chunks of text or bouncing around ideas with something that will research them for me.
   * Claude models are impossible to beat for large-scale changes.

3. Cursor and its variants
   * Cursor hand-tunes a lot of things for its models, so the experience is pretty good out of the box.
   * As noted above, this is a good start if you want a one-size-fits-all option.

Some comments:

* Fable was really good, but I don't have it on my current plan.
* Opus 5 is bad, and I don't like it.
* I've never tried the Grok models.
* Local models absolutely have their place, but they are beyond the scope of this page.

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
