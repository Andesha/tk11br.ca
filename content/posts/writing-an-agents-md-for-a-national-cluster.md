---
title: "Writing an AGENTS.md for a national cluster"
subtitle: "Only tell the agent what it can't already know"
description: "What I learned putting an AGENTS.md into the Alliance software stack: skip what frontier models already know and spend the lines on site policy and when to stop and ask."
date: 2026-10-20T09:57:00-04:00
draft: false
tags: ["agents", "hpc"]
---

Agents have started causing problems on our clusters. Heavy work kicked off on shared login nodes, Slurm getting polled in tight loops, that sort of thing.

I'd been using a small `CLAUDE.md` for myself on Nibi for a while, and I was asked to turn it into something for everyone. The Alliance clusters get their environment from [ComputeCanada/software-stack-config](https://github.com/ComputeCanada/software-stack-config), so I opened [PR #111](https://github.com/ComputeCanada/software-stack-config/pull/111) to add an `agents/AGENTS.md` there on request. Claude Code reads `/etc/claude-code/CLAUDE.md` system wide, and most other harnesses look for an `AGENTS.md`, so one file and a symlink covers a lot of ground.

## Only say what the model can't know

My opinion after going through this is that an `AGENTS.md` should only hold what the model can't already know. Site policy, the stuff that's different about these clusters, and when to stop and ask the human. That's it.

Everything in the file is in the context of every session, so every line should carry a lot of value. Things like the module commands and Slurm commands are already known by the frontier LLMs. There's no need to give specific guidance on them. The lower tier LLM services won't even read these docs anyway.

## Review is important

The next morning after sharing there were about 20 inline comments, and nearly all were things no model could know from training. Not every compute node has internet, so tarballs and wheels need to be staged from the login node. Bundle anything that runs under 15 minutes and checkpoint anything over 12 hours. Avoid `uv`. If a wheel or module is missing, tell the user to contact support instead of getting creative.

It also caught my own mistake. My Python section said to load the module, make a virtual environment, and install from the wheelhouse. It never activated the environment. A classic.

```sh
module load python/<version>
virtualenv --no-download <venv>
source <venv>/bin/activate
pip install --no-index <package>
```

So the people who run the stack should absolutely be writing these with you. They know the local gotchas way better than any model does.

## Where I pushed back

The thing that kept coming up in review was adding specific wiki links to each section, plus fuller examples of commands like `module spider`. My problem with this is it's just bloat. I think we can just tell the agents to check the documentation, or perhaps just say the page name.

## What came after

A few more rules went in after that, similar to ones other sites have landed on, like [CHTC at UW–Madison](https://chtc.cs.wisc.edu/uw-research-computing/agent-recommendations). The file now says human users remain responsible for the actions of their agents. It also says to point out stale VS Code processes and offer to kill them, to wait at least 60 seconds between Slurm queries, and to never insert sleep commands into jobs. Those are the same kind of thing, site behaviour a model wouldn't guess.

The latest change points agents at a read only markdown copy of the Alliance wiki at `/cvmfs/soft.computecanada.ca/custom/docs/`, in English and French. Now the agent can go read the actual page when it needs the details, and none of it has to live in the file.

Since then, it has been deployed to the Nibi cluster. To see for yourself without SSHing to Nibi, visit [the PR](https://github.com/ComputeCanada/software-stack-config/pull/111).

## Related posts

- [Stop installing things your agent doesn't need]({{< relref "prompt-context-is-a-resource.md" >}})
- [Send your agent a screenshot]({{< relref "send-your-agent-a-screenshot.md" >}})
