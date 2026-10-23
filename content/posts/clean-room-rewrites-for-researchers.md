---
title: "Clean-Room Rewrites for Researchers"
subtitle: "Getting your old paradigm out of a closed tool"
description: "Tools like REA let a coding agent take closed software apart. Escaping research lock-in is one of the best uses for them, as long as you stay in your lane."
date: 2026-10-23T12:00:00-04:00
draft: false
tags: ["llm", "workflow"]
---

[REA](https://github.com/morluto/rea), short for Reverse Engineer Anything, went from nothing in April to about 370,000 GitHub stars this month. It's an MCP server that hands your coding agent the reverse-engineering tools people have used for years, like Ghidra, IDA, and Hopper, and lets it work out how a program behaves without the source. It should be noted that these tools typically are only used by experts and they take a lot of skill to use.

It arrived in the middle of a messy time for software licensing. The chardet library was rewritten with Claude Code and relicensed from LGPL to MIT, and its original author objected. PhotoCraft is building a "clean-room" Photoshop in Rust. Someone even launched Malus, a satire site selling "Clean Room as a Service".

However, I think most of that unease is about commercial clones and relicensing other people's work, and security concerns. There's a much more boring use case that I think is really valuable though, getting your own research out of a tool you're stuck with.

## What REA actually does

REA doesn't decompile anything itself. Your agent calls it over MCP, REA drives whichever analysis tool fits the target, and the findings come back with the evidence behind each one. The agent can then use those findings to explain the behaviour, or to write and test a new implementation.

The docs even describe how to keep it clean-room. The agent writing the new code runs somewhere that can't read REA or its analysis output, and only gets a spec. That's the classic two-team clean-room setup, just with LLM agents instead of people.

## The paradigm you get stuck with

Lots of labs have an experiment or piece of code like this. The paradigm was built years ago in E-Prime, Presentation, or a MATLAB toolbox that only ships compiled code or something too difficult to modify. It works, but the licence is expensive, it only runs on one old Windows machine in the corner, and nobody who built it is still around. You'd like it in PsychoPy, but the details that matter are hidden. How the trials are randomised, which trigger codes go out when, and what goes in the output file.

That's pretty much exactly what REA is for. Point the agent at the old paradigm, let it recover those details, and have it write them down as a spec. A second agent builds the PsychoPy version from that spec alone. That used to be a big chunk of somebody's entire year as a Masters student when they didn't even have a Computer Science degree. Now it's a lot more doable.

## Stay in your lane

Two things keep this on the right side of the grey area.

**Ask first.** Email the vendor or the original author before you take anything apart. They might just send you the spec, or the source, and then you don't need REA at all. Or better yet, you and your lab are the owners anyway!

**Validate against the original.** Run the old and new versions side by side and compare the trial order, the trigger timing, and the output files. The rewrite is only useful in a paper if you can show it behaves the same, so honestly that comparison matters more than the code.

Cloning a commercial product to sell, or rewriting someone's library to drop their licence, is a different thing. That's where the chardet fight came from, and personally I'd stay far, far away from this.

## Try it

If a closed tool is the only thing between you and a reproducible study, this is now a realistic project. Pick the paradigm that's been stuck on that old lab machine, and see how far an agent and REA get you.
