---
title: "Harder than \"just use a container\""
subtitle: "Sandboxing an agent against Brine, and why I want you to try to break it"
description: "Researchers already pin the environment a job runs in. Doing the same for a coding agent on a laptop took more work than I expected, and my own testing found a hole. brine-sandbox needs more people trying it."
date: 2026-11-24T09:00:00-05:00
draft: false
tags: ["agents", "hpc", "workflow"]
---

A lot of the researchers I talk to want a coding agent on their laptop that uses [Brine](https://docs.alliancecan.ca/wiki/Nibi#Brine:_AI-as-a-Service_platform), the AI-as-a-Service platform I run on Nibi. They don't want that agent reading their SSH keys or sending their data to some random server. My usual answer has been to [run it in a container or a VM]({{< relref "what-researchers-ask-about-agents.md" >}}). That's still good advice, but this week I tried to build the setup properly myself, and it was a lot harder than that one sentence makes it sound.

The result is [brine-sandbox](https://github.com/sharcnet/brine-sandbox). It runs the [Pi](https://pi.dev) coding agent inside a [nono](https://github.com/nolabs-ai/nono) sandbox. The agent can write to your project directory and talk to Brine, and that's pretty much it. It never sees your real Brine key either. nono holds the key and swaps it in on the way out, and only for chat completions and the model list.

## Pin it like a job

Researchers are already aware of this habit. You pin a container image or a set of modules so a job runs in a known environment, and you can rerun it later and get the exact same setup. An agent needs the same thing, except here the environment is also the thing keeping it in line. If the sandbox binary changes under you, so does what the agent can reach.

So, the launcher doesn't trust whatever `nono` is on your `PATH`. It hashes the binary and refuses to start unless the sha256 matches one of the pinned 0.82.0 release builds. Checking the version string alone only tells you it's compatible, not that it's the real thing.

Getting those pins right was most of the install work. nono publishes a `SHA256SUMS.txt`, but that file comes from the same place as the download, so it only catches a broken download. It doesn't tell you who built it. nono doesn't publish detached signatures either. What it does have is GitHub's signed build provenance, so every upgrade starts with `gh attestation verify` on each Linux tarball, and then I pin the sha256 of the `nono` binary inside, not the tarball.

That matters more than usual here, because nono is pre-1.0 and releases about every two weeks, and it has surprises. In 0.82.0, an empty `allow_domain` list leaves the network fully open, even with a credential route set up. The first pilot run reached example.com because of it.

## The hole I found anyway

The part that surprised me most came from letting Pi probe the sandbox from inside. A direct write to my home directory got denied, which is what I wanted. But a request through the desktop session bus created a harmless marker file in my home directory anyway. The same run could also connect to my SSH agent and my Wayland display. The filesystem rules were fine. The agent just asked a service outside the sandbox to do the write for it.

The fix was turning on nono's Unix socket mediation, which denies `connect` and `bind` on every Unix socket the profile doesn't list. `--check` now probes the session bus, SSH agent, Wayland and X11 against live sockets, and the host control connects to the session bus while the sandbox gets `EACCES`. It also checks that a deliberately granted socket gets caught, so a grant that slips in later can't pass quietly.

That's why I don't think "just use a container" is the whole answer. Drawing a box around the agent was the easy bit. Checking that every way out is actually closed on your machine took most of the time, and I still missed one.

## Try it, then try to break it

brine-sandbox needs more people running it. It wants Linux with kernel 6.7 or newer. macOS isn't tested yet, and WSL2 doesn't enforce the network rules, so don't use it there. It's also not for sensitive data, since Brine's terms still say not to send any. [brine-secure](https://github.com/sharcnet/brine-secure) is the one to look at for that.

If you use Brine, follow the README, run `brine-sandbox --check` in a project, and open an issue on [sharcnet/brine-sandbox](https://github.com/sharcnet/brine-sandbox/issues) with what passed, failed, or got skipped on your setup. In my opinion, different desktops and distros are where the next gap is going to show up.

If you think about security, read the launcher, `profile.json` and `checks.mjs`. It's a few hundred lines of shell, JSON and JavaScript, short enough to read in one sitting. The README has a table of every threat it claims to block and the probe that tests it. Try to make one of those claims false.

My own review found a hole on day one, so I'd honestly be surprised if it was the last one. Please go find the next one!

## Related posts

- [What researchers ask about agents]({{< relref "what-researchers-ask-about-agents.md" >}})
- [Approve the irreversible bits]({{< relref "approve-the-irreversible-bits.md" >}})
