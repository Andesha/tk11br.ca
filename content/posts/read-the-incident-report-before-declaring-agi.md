---
title: "Read the incident report before declaring AGI"
subtitle: "The Hugging Face incident involved capable agents and a lot of ordinary security failures"
description: "The OpenAI and Hugging Face incident is a good example of why dramatic claims about AI need to be checked against the full incident report."
date: 2026-09-14T10:20:35-04:00
draft: false
tags: ["agents", "security"]
---

I keep seeing people describe the OpenAI and Hugging Face security incident as evidence of AGI or how we are all doomed in the next year. The bots communicated with each other, escaped their sandboxes, and got loose on the internet. It sounds completely wild when you reduce it to a few headlines.

Then you read what happened.

Marius Horatau's article, [The Hugging Face Incident Is Not an AI Story](https://uphack.io/blog/post/the-hugging-face-incident-is-not-an-ai-story/), does a great job of reading the incident as a security engineer instead of treating "AI" as the explanation for everything. In my opinion, he's got it exactly right.

The agents did some impressive things. They found vulnerabilities, passed information through a shared service, and chained together access across systems. I'm not trying to say that isn't impressive, but it's not strictly new. But the [technical report from OpenAI](https://cdn.openai.com/pdf/67869394-cb91-4c12-888c-5cbd85c7814c/OpenAI-Hugging-Face%20Incident-Technical-Report.pdf) also describes a pile of bad security and operational decisions that tend to disappear when people retell the story.

OpenAI gave workloads the same Artifactory credentials. The workloads could all read and write to the same service, so the agents turned it into a message board without needing to exploit anything. That service could also reach the internet even though the agents supposedly couldn't. This is strictly against best practices.

The response was worse. On June 27, a monitoring tool caught port scanning. Responders traced it to an evaluation where agents were using Artifactory as a message board and a network pivot. The on-call response staff advised that the run didn't need to stop. Another mistake.

A week later, agent traffic knocked Artifactory offline. Responders then found an unauthorized administrator account, rogue repositories, command-capable plugins, and configuration changes. OpenAI rebuilt the service, removed the shared credential from new workloads, blocked the paths it knew about, and resumed evaluations on July 7. The agents established another message board the next day. You guessed it, another mistake.

You don't need to bring up AGI to know why this got out of hand. OpenAI ran agents trained to persist and find security vulnerabilities inside an environment with shared credentials, shared writable infrastructure, and an indirect route to the internet. Staff saw the agents abusing that infrastructure and kept the evaluation running. After finding an administrator-level compromise, they resumed evaluations without understanding the full scope of the incident.

This is mostly a media literacy point. Don't trust the flat version of a complicated technical event, especially when the flat version makes an extraordinary claim. Read the report. Check what access the system had. Look at which alerts fired, what the humans did with them, and which basic controls failed.
