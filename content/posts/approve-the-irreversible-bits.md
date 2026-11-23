---
title: "Approve the irreversible bits"
subtitle: "Why I'm comfortable running agents in auto mode"
description: "Approving every agent action trains you to stop reading the prompts. I keep approvals for the few things git can't undo and let everything else run."
date: 2026-11-30T09:00:00-05:00
draft: true
tags: ["agents", "workflow"]
---

For a while I approved everything my agents did. Every file read, every `hugo` build, every grep. Somewhere around the hundredth yes of the day I noticed I wasn't actually reading the prompts anymore, just hitting enter. That's pretty much the worst type of safety you can have, because it feels careful and protects you from nothing.

Two other things pushed me the same way. Setting up new machines across three harnesses meant writing my rules down every time, since each one needed the same instructions. And longer runs kept stalling on a prompt while I was off doing something else, so I'd come back to an agent that had been sitting there waiting for permission to read a file.

Most of my work runs in auto mode now, and I'm comfortable with that because I only approve the irreversible bits.

## What I still approve

My rules are written down, mostly in my global instructions and in the `FLEET.md` that runs my config repo. The list is short:

- Anything that changes git, like branches, commits, the working tree, the index, or remotes
- Anything that changes my machine outside the repo, previewed first
- Anything outward facing, like pushing, publishing, or sending something to another service
- Secrets, which never go in a repo at all

The git one started as a single line in my global instructions: "Get my explicit approval before commands that change branches, commits, the working tree, the index, or remotes." That's a request though, and an agent can still blatantly forget it halfway through a long run. So it's also a `PreToolUse` hook in Claude Code now. Before any git command runs, the hook checks whether it changes anything, and if it does I get asked, auto mode or not. Reading the log or a diff is fine. Committing isn't, unless I say so.

The machine one is a bit more involved. When an agent sets up a new box from my config repo, it runs `stow --simulate` and shows me the output before linking anything into my home directory. If a file already exists where a symlink should go, it stops, makes a timestamped backup, and shows me the diff instead of overwriting it.

Everything else just runs: reading files, searching, running builds and tests, and editing files inside a repo.

## Why that's enough

Inside a git repo pretty much every edit is reversible. If an agent makes a mess of a post or a function, `git diff` shows me exactly what changed and I throw it away. A bad edit costs me a few minutes. So approving each one buys me almost nothing, and it burns the attention I need for the prompts that matter.

The things on my list are the ones git can't undo. Things like a force push, a file in my home directory that wasn't tracked anywhere, an email, a post that's already been indexed. That's where a mistake actually costs something, so that's where I want to be reading carefully. Because there's only a handful of them, I actually do. It isn't risk-free, and I don't want to pretend it is.

## Write your list

If you're still clicking approve on everything, write down the three to five things that should always need you. Start with git and anything that leaves your machine. Put them in your `AGENTS.md` or `CLAUDE.md` in plain sentences. For the one you'd regret most, which is probably git, back it up with a hook so it isn't just a request. Then turn on auto mode and see how it feels for a week.

Personally, I'd never go back to approving every grep.

## Related posts

- [Your dotfiles repo should be private now]({{< relref "your-dotfiles-repo-should-be-private-now.md" >}})
- [My agent adoption journey]({{< relref "my-agent-adoption-journey.md" >}})
