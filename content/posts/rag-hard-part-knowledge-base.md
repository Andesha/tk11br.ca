---
title: "Before You Rebuild Your RAG Pipeline, Try an Agent"
subtitle: "Let it search the original documents instead of feeding it broken chunks"
description: "If RAG is returning incomplete answers from dense technical documentation, try letting an agent search and read the source material directly."
date: 2026-09-15T10:40:34-04:00
draft: false
tags: ["agents", "RAG"]
---

If your RAG system keeps giving incomplete answers, try going fully agentic.

I'm not saying retrieval-augmented generation is useless. It can make a large collection of documents cheap and fast enough to query. But if you have some tokens to burn and your corpus isn't massive, it may be better to let an agent search the original documents itself.

I ran into this with a public-facing technical wiki. The articles are dense. They have long tables, code samples, configuration details, and links to many related pages. A useful answer might depend on a warning above a table, one row in the table, and an example farther down the page.

Chunking pretty much destroys this on average as the length of documents grows.

## Retrieval commits too early

A typical RAG pipeline splits documents into chunks, creates embeddings for them, and retrieves a small set that appears relevant to the question. The model answers using those chunks.

That works when each chunk still makes sense on its own. A paragraph from a straightforward policy document might survive the process just fine. Technical documentation is less cooperative.

A chunk can contain half a table without its heading. A code sample can lose the paragraph that explains when to use it. Two adjacent chunks can look unrelated to an embedding search even though a human reading the page would clearly use them together.

You can improve the pipeline. You can change the chunk size, preserve more document structure, add overlapping context, retrieve more candidates, or rerank the results. Those techniques are useful. They also keep the same basic constraint: the system decides which pieces matter before the model has understood the problem. Sometimes the model needs to investigate first.

## Give the agent the source

Instead of retrieving a handful of chunks, agents can use standard tools to explore the wiki. It can run searches via `grep`, open complete pages, follow links, inspect examples, and search again when the first result wasn't enough.

That changed the job. The agent wasn't forced to answer from whatever fragments happened to rank highest. It could start with a broad search, learn the terminology used by the documentation, and then narrow its search. If a page referred to another procedure or configuration option, it could go read that too.

In my experiments, this produced much better results. The agent could create complete GROMACS scripts customized for our clusters. The RAG approach was more likely to produce a generic guess because it didn't retrieve enough of the cluster-specific instructions together.

The difference wasn't that the agent knew more about GROMACS. It had a better way to find and assemble the relevant local information.

## This isn't free

Direct exploration spends more tokens. It takes longer than looking up a few precomputed chunks, and it won't make sense for every collection of documents. It also requires a model strong enough to do proper tool calling.

If you have millions of pages, tight response-time requirements, or thousands of simultaneous users, you probably need retrieval to narrow the search. Access controls and source filtering may also require more deliberate infrastructure than handing an agent a directory and letting it roam around.

But many internal knowledge bases and technical documentation sites aren't that large. The agent doesn't need to read everything. Search tools let it reduce the corpus as it works, much like a person looking through unfamiliar documentation.

That makes corpus size and token cost practical limits, not reasons to assume RAG should always come first.

## Run the comparison

If your current RAG system works, keep it. If it keeps missing context, returning generic answers, or falling apart around tables and code samples, don't immediately build a more complicated retrieval pipeline.

Give an agent access to the same source documents. Let it search them, read full pages, and follow links. Then ask both systems the questions your users actually care about and compare the answers.

Maybe the agent will be too slow or expensive. Maybe the corpus really is too large. That's useful to know. You now have a concrete reason to improve retrieval and a better result to compare it against.

But if the agent gives you a complete, locally correct answer while the RAG system keeps returning polished fragments, you may not need better chunking. You may need to stop deciding what context matters before the agent has had a chance to look around.
