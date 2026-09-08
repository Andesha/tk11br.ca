---
title: "Stop installing things your agent doesn't need"
subtitle: "Keep the occasional tools in the projects that use them"
description: "Keep your Claude Code or Codex setup lean. Put specialized skills and plugins in the projects that need them instead of loading them everywhere."
date: 2026-09-08T16:00:00-04:00
draft: false
tags: ["agents", "workflow"]
---

Stop adding things to Claude Code or Codex that you use once and then forget about.

I like customizing my agents. Skills, plugins, extensions, whatever the particular tool calls them. But I want to combat the slow creep towards the dumb zone, and loading a bunch of unrelated stuff into every session works against that.

Matt Pocock has a useful description of the [smart zone and the dumb zone](https://github.com/mattpocock/dictionary-of-ai-coding/blob/main/dictionary/Smart%20zone.md). Early in a session, the agent is at its best. The longer the conversation goes, the more mistakes start to pop up. This is where those early-days patterns of hallucinations really came from. The context window isn't a promise that it'll work well at all times.

There's no universal line where this happens. Maybe 40% to 60%? It depends on the model. But every model shares the fact that the more things you pack into its context, the worse it gets over time.

## What are we adding?

Context is the available space the model has when it produces a response. Your conversation is part of it, but so are the base instructions from OpenAI or Anthropic, and information about the tools it can use. This is typically referred to as the system prompt. It supplies instructions before you've even typed anything.

Installing something extra doesn't necessarily put all of it into the system prompt. For example, [Claude Code only loads a skill's full instructions when it's used](https://code.claude.com/docs/en/skills), rather than loading every skill in full at startup. This is great, but dozens of skill descriptions and available tool definitions can still take up context, depending on how the application loads them.

## Keep the occasional stuff local

My recommendation is to start with nothing and only add things when you have a reason to use them. Don't just add the Google Calendar support because you might use it one day. Now it's in your system prompt for every project, creeping you closer towards the dumb zone.

However, if a tool helps with your everyday work across projects, keeping it in your global setup makes sense. If it's for deploying one particular website, keep it with that website. A specialized database integration doesn't need to be available while you're editing an unrelated Python package.

For a concrete example, Claude Code supports personal skills in `~/.claude/skills/` and project skills in `.claude/skills/`. The first makes a skill available across your projects. The second keeps it in that repository. Use the equivalent project-level setup in your agent, and check the scope when you install something.

Personally after writing this I cut about 10 different writing and planning skills from my globally installed skills and moved them all into a writing project. Try it out yourself!