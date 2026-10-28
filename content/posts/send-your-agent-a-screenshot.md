---
title: "Send your agent a screenshot"
subtitle: "The cheapest way to give it more information"
description: "Agents only know the dashboards they were trained on. When menus keep moving or a UI looks wrong, a screenshot gives the agent what's actually on your screen."
date: 2026-10-28T09:00:00-04:00
draft: false
tags: ["agents", "workflow"]
---

I always find myself getting lost in the Cloudflare dashboard. Every time I need to set up a redirect rule, it seems to have moved. I ask an agent where to find it, and it confidently tells me to click through menus that don't exist anymore. Then I'm the one clicking around again, and the agent can't help because it has no idea what I'm looking at.

The fix was pretty simple. It's what you would do with a friend who's a patient expert. I took a screenshot and sent it over, and the agent saw the menu as it actually was that day and told me it had moved to a different submenu.

## The agent's map is out of date

An agent's knowledge of a dashboard comes from whatever existed when it was trained. Cloudflare, GitLab, cloud consoles, really anything that ships UI changes constantly, will have moved on since then. So the agent gives you directions from an old map, and it has no way of knowing the map is old. A screenshot is today's version of the page, with the actual labels and the actual layout, so it doesn't have to guess.

## Describing what you see is lossy

The same thing happens with your own work. When something looks off in a UI I'm building, my first instinct used to be describing it. "The table lines are basically invisible." "The wrong toggle is highlighted." "The diagram is broken somewhere in the middle."

Each of those takes effort to put into words, and then the agent has to guess back from my words to the pixels. Half the time it fixed something next to the actual problem. A screenshot skips both steps. The agent sees the same thing you do, and you don't have to be good at describing UI bugs.

That's pretty much the whole point. Agents do better work with more information, and a screenshot is about the cheapest information you can give them.

## Tell it where to look

Dragging images into the chat works, but it gets old fast. What made it stick for me was adding one line to my global `CLAUDE.md`:

```text
If I mention screenshots, they can be found in "~/Pictures/Screenshots".
```

Now I take the screenshot like I normally would and type "see my latest screenshot." The agent goes and finds it. Put the equivalent in your `AGENTS.md` or whatever your agent reads, pointing at wherever your screenshots actually land.

One caution though. Dashboards like Cloudflare's love to show API tokens and account IDs, so crop those out before you share.

Agents can take their own screenshots too, with tools like Playwright, but that's another post. Next time you're lost in a menu or squinting at a UI bug, skip the description and send a screenshot. Try it out yourself!

## Related posts

- [Stop installing things your agent doesn't need]({{< relref "prompt-context-is-a-resource.md" >}})
- [Writing an AGENTS.md for a national cluster]({{< relref "writing-an-agents-md-for-a-national-cluster.md" >}})
