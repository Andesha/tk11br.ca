---
title: "Your dotfiles repo should be private now"
subtitle: "An old idea that got a lot more useful with agents"
description: "Keeping your config in a git repo isn't new. What's new is an agent that can set up a fresh machine from Markdown instructions, and a private repo that can hold your whole working setup."
date: 2026-11-09T09:00:00-05:00
draft: false
tags: ["agents", "workflow"]
---

I use three agent harnesses: Pi and Claude Code locally, and Hermes on a remote box. For a while each one had its own copy of my instructions and skills, and of course, they slowly drifted apart. Then I got another new box and a new build node to set up, and I was copying files around by hand again.

So I made one private repo the source of truth for all of it, and now setting up a new machine is mostly me approving what an agent proposes.

## This isn't a new idea

People have been keeping their dotfiles in a git repo for a long time, and GNU Stow, the tool I use to symlink them into place, has been around since the '90s. Tons of people publish their dotfiles repos on GitHub. I didn't invent anything here, and I didn't write a tool for it either. Stow and git already do the job.

My repo actually started that way back in April. The first commits were some dotfiles, a dump of my apt packages, and an SSH port-forward script that I have a keybind to run. It only became something more in August, when I started pointing agents at it.

## What's different now

Two things changed. **The setup is Markdown, not a script.** The old way was a `bootstrap.sh` that you hoped still worked on the new machine. Now the repo has a `FLEET.md` that tells the agent the rules, and a bootstrap runbook that it walks through. The runbook says it's "a checklist, not an unattended script." Every step that touches my home directory gets previewed first:

```bash
stow --simulate --verbose --dir packages --target "$HOME" <package>
```

The agent shows me that output, and only runs the real `stow` after I say yes. If a file already exists where a symlink should go, it stops, backs it up, and shows me the diff instead of clobbering it. If a harness is missing on the new machine, it tells me and carries on with the packages that don't need it, where a script would have just fallen over halfway through.

The layout is pretty boring, which is the point:

```text
FLEET.md          rules and the current catalog, for the agent
CONTEXT.md        what this repo is and isn't
packages/         Stow trees: claude, pi, skills, ssh, git, ghostty
assets/           shared instructions and skills
docs/runbooks/    bootstrap and other procedures
software/         apps to install on a new machine
career/           bios, brag doc, blog pipeline
```

Skills I didn't write are pinned to an exact commit. Matt Pocock's skills are on a specific SHA with an allowlist of the 19 I actually use, so nothing changes under me because someone upstream pushed to `main`.

**Private means it can hold everything.** A public dotfiles repo has to be safe for strangers to read, so it ends up being just config. Mine is private, so it also holds my SSH host list for the clusters I log into, the list of apps I want on every machine, my bios, my brag doc, and the pipeline of blog post ideas. An agent is way more useful with all of that sitting next to my config. Need a bio for a talk? The source material is already there.

The one hard rule is that secrets never go in. No keys, no tokens, no credential files. The repo can say a credential lives in some file or environment variable, but never what it is. Private isn't a substitute for that.

## Start one

If you use agents and don't have one of these yet, make a private repo today. Put your `CLAUDE.md` or `AGENTS.md` in it, plus a list of the apps you always install. Then write a short README that tells an agent what the repo is and how to put things in place. Grow it from there when you hit something you had to redo by hand.

Now on a fresh machine my first prompt is pretty much "read FLEET.md and bootstrap me." Try it out yourself!

## Related posts

- [Stop installing things your agent doesn't need]({{< relref "prompt-context-is-a-resource.md" >}})
- [Writing an AGENTS.md for a national cluster]({{< relref "writing-an-agents-md-for-a-national-cluster.md" >}})
- [Send your agent a screenshot]({{< relref "send-your-agent-a-screenshot.md" >}})
