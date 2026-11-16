---
title: "My agent adoption journey"
subtitle: "Every stage had to prove itself before I moved on to the next one"
description: "How I went from AI commit messages in late 2025 to agents triaging issues and drafting posts a year later, and why each step needed proof before I trusted the next."
date: 2026-11-16T09:00:00-05:00
draft: false
tags: ["agents", "workflow"]
---

People ask me where to start with agents pretty much every week. Usually they've seen someone else moving really fast and want to skip straight to that part and level of trust. I get it, but that isn't how it went for me.

Mitchell Hashimoto wrote up [his own AI adoption journey](https://mitchellh.com/writing/my-ai-adoption-journey), and I liked that he showed *how* he got there instead of just where he ended up. So here's my take. The short version is that each stage had a burden of proof. Something had to work well enough that I trusted it, and only then did I hand over a bigger piece of work. For some problems, there's not enough trust in the world to use AI.

## Super early days

Like most people, I was using ChatGPT casually. Often it was useful for teaching myself something, or helping with complex regex questions. For me, really, the best part was that it never ran out of ideas. It was very helpful to have something that would keep thinking of new ways to debug a problem. This was also around the time when hallucinations happened all the time. I was still writing all my code myself and on Stack Overflow quite often.

## November 2025: single lines and commit messages

I started with Cursor for really small stuff. Minor edits to single lines, commit messages, and boilerplate for new projects. If it got a line wrong I'd see it immediately, and a bad commit message never hurt anyone. Not a lot of proof needed for that.

Looking at my git history, this barely shows up. I made one commit on my machine in September 2025. Agents weren't changing how much I got done yet, just saving me some typing.

For me, the most fun I had in this period of time was being able to bootstrap small visualization projects. Cursor made it really easy for me to just iterate on small chunks of code from unfamiliar libraries.

## March 2026: the screenshot that changed things

For the early winter of 2026, I faded away from Cursor. At the time I was working on a lot of Jupyter notebook projects and it was just difficult to use.

Then I tried Claude Code with Sonnet 4.6, and it was mind blowing. The moment that did it was the PyLossless criteria function plots. Those figures existed in the old MATLAB version of the pipeline and I wanted them in Python. All I did was give it a screenshot, and it recreated them. I wasn't familiar enough with the PyLossless codebase at the time, so it was basically just magic to me. Further work from there would confirm it had done it right too.

One success isn't proof, so I tested it on several codebases I worked on, and it always performed well. That was enough to change how I worked. I ended up programming in a much more pair programming oriented way, where I'm still in every decision but I'm not typing every line. I was still breaking down the problems into testable pieces for the agent to work through one at a time. Laughably, I also spent a ton of time tweaking my `CLAUDE.md` almost every day.

The git history shows this one pretty clearly. I went from about one commit a month to 94 in March and 199 in April. I'd started zero new repos since mid-2024, and from March on I was starting four to nine a month. A lot of those were small one-off tools that I never would have bothered with before, because now they were cheap to build.

## May 2026: whole features

By May I was bouncing between Pi, Codex, and Claude Code, and Opus 4.7 and 4.8 increased the complexity of work that was possible for me. I could hand over entire features and have agents triage issues on projects, which is a much bigger unit of work than a pair programming session. July was my busiest month at 285 commits.

I trusted this because March had already earned it. I knew what the models were good at on my code, so handing over a whole feature was a reasonable next step instead of a leap. Around the same time `CLAUDE.md` turned into `AGENTS.md`, and about 20 of my repos have one now.

## Where it set me back

Not every step forward worked. Writing reports without steering at various stages is what set me and my trust back. The output read fine, but it missed the nuance the work required. A report has judgment calls all through it, and when nobody steers those, the agent makes them for you and misses obvious problems.

That's where I learned the burden of proof runs both ways. A good result moves you forward, and a bad one should move you back. I still use agents around reports, but I steer at every stage now. A lot of that work I just do myself.

## August 2026: skills

The latest step was skills. I'd been adding Matt Pocock's skills to individual projects since the end of April, and in August I installed them globally and wrote my own `article-drafting` skill a couple of days later. My first agent post on this site came out three days after that, and I've written 20+ since.

Skills let me turn something that worked once into something I can repeat. That's what made automations and the more interesting interactions possible. These days my commits are down but spread across issue-driven projects, because more of my time goes to triaging and steering than typing.

## Start with your own small proof

If you're at my November 2025 stage, don't try to jump to the end. Find one small thing where you already know what the right answer looks like and see if an agent can get there. A figure you already have is a great one, because you can tell at a glance whether it's right. If it works, try a bigger piece. If it doesn't, you've learned where the line is for now.

It's been about a year since the commit messages. Pretty wild how far it's come.

## Related posts

- [From a Throwaway QC Prototype to PyLossless]({{< relref "pilot-qc-to-pylossless-feature.md" >}})
- [Send your agent a screenshot]({{< relref "send-your-agent-a-screenshot.md" >}})
- [Writing More Code with AI Agents]({{< relref "writing-more-code-with-ai-agents.md" >}})
- [What researchers ask about agents]({{< relref "what-researchers-ask-about-agents.md" >}})
