---
title: "Recommended AI Tools"
description: "Opinionated buying guidance for AI tools and services."
date: 2026-05-08T00:00:00-04:00
---

My current recommendations for AI tools that are worth trying or paying for. This page is intentionally practical: what I would use, who it is for, and what caveats matter before spending money.

AI products change quickly, so treat this as buying guidance, not a permanent ranking. Start with the free tier when possible, pay for one tool that matches your main workflow, and cancel anything you are not using every week.

## Short Version

- **If you want one general AI subscription, start with [ChatGPT](https://chatgpt.com/).** It is the easiest default for mixed writing, brainstorming, coding help, image work, and everyday questions.
- **If you write code or long documents often, try [Claude](https://claude.ai/).** It is usually the first place I would go for careful editing, code review, refactoring plans, and long-context reasoning.
- **If you live in Google Workspace, try [Gemini](https://gemini.google.com/).** Its main advantage is integration with Google's ecosystem and very large-context workflows.
- **If you need sourced research fast, try [Perplexity](https://www.perplexity.ai/).** It is useful when citations and link trails matter more than raw drafting ability.
- **If you want AI in an editor, start with [Cursor](https://www.cursor.com/) or [GitHub Copilot](https://github.com/features/copilot).** Cursor is the stronger AI-native editor. Copilot is the safer default if you already like your current editor.
- **If you want a terminal coding agent, try [Claude Code](https://www.anthropic.com/claude-code), [OpenCode](https://opencode.ai/), [Aider](https://aider.chat/), or [pi](https://pi.dev/).** The right choice depends on how much you value model quality, open-source control, Git-native workflows, or custom harnesses.
- **If you want to compare many agents visually, look at [T3 Code](https://t3.codes/).** It is a useful open-source desktop interface for running coding agents side by side.

## General Assistants

These are the subscriptions I would compare first. Most people should pay for one of these before adding specialized tools.

- **[ChatGPT](https://chatgpt.com/)**: Best default if you want one general AI subscription for writing, brainstorming, coding help, images, documents, and everyday questions. It is broad, polished, and easy to recommend to someone who does not want to think too hard about the category.
  - **Best For:** General-purpose AI help; first drafts and rewrites; explanations; mixed text, code, image, and document workflows.
  - **Caveats:** It can sound confident when it is wrong. Ask for sources when facts matter, and compare it with Claude if your main work is code or long documents.
  - **Personal Comments:** This is the easiest default recommendation right now.
- **[Claude](https://claude.ai/)**: Best when reasoning quality, prose quality, long context, or careful code review matters more than having the broadest product ecosystem.
  - **Best For:** Coding help; code review; long documents; careful editing; refactoring plans; trade-off analysis.
  - **Caveats:** It is still not a substitute for tests, review, or domain judgment. Usage limits can matter in long sessions.
  - **Personal Comments:** This is usually where I go first for serious writing and coding work.
- **[Gemini](https://gemini.google.com/)**: Best if your work already lives in Google Workspace or you need very large-context workflows close to Gmail, Docs, Drive, Search, and Android.
  - **Best For:** Google Workspace users; long-context document work; multimodal questions; Google-account-native workflows.
  - **Caveats:** Ecosystem fit is the main reason to choose it. If you do not use Google products heavily, compare it with ChatGPT and Claude first.
  - **Personal Comments:** I would choose this because of Google integration, not because everyone needs another general assistant.
- **[Perplexity](https://www.perplexity.ai/)**: Best as a fast research companion when citations and link trails matter more than drafting polish.
  - **Best For:** Source-backed web research; recent information; comparing public claims; building a reading list.
  - **Caveats:** Citations can still be incomplete or misleading. Read the sources yourself before treating an answer as settled.
  - **Personal Comments:** I think of this as a research layer, not as my only AI tool.
- **Grok, Microsoft Copilot, Mistral Le Chat, DeepSeek, Qwen, Kimi, GLM, And Other Frontier Models:** These are worth knowing about, but I would not start most people here unless they have a specific reason. Grok is tied to X and real-time social data, Microsoft Copilot makes sense for Office-heavy organizations, Mistral is interesting for EU-hosted workflows, and the Chinese model ecosystem is increasingly important for open-weight and low-cost model access.
  - **Best For:** Model comparison; regional or sovereignty requirements; Microsoft 365 organizations; open-weight experimentation; low-cost API work.
  - **Caveats:** Availability, privacy posture, pricing, benchmarks, and model names change quickly. Do not choose one only because it is currently winning a leaderboard.
  - **Personal Comments:** I track these as part of the landscape, but they are not my first recommendation for a typical person buying one subscription.

## Coding Tools

The coding-tool market has split into editor assistants, terminal agents, open-source extensions, and remote cloud agents. I would not try to use all of these at once. Pick one editor assistant, one terminal agent, and maybe one experiment.

**Editor-First Tools**

- **[Cursor](https://www.cursor.com/)**: AI-native editor with chat, multi-file edits, codebase search, and agentic workflows in one polished interface.
  - **Best For:** Developers who want an AI-native editor; multi-file changes; fast prototyping; people willing to move into a new editor.
  - **Caveats:** Watch pricing and usage limits. It can make large changes quickly, so commit often and review diffs carefully.
  - **Personal Comments:** This is the first editor I would suggest to someone who wants the whole workflow centered on AI.
- **[GitHub Copilot](https://github.com/features/copilot)**: Practical default if you want AI inside your existing editor with minimal workflow change.
  - **Best For:** Keeping your current editor; autocomplete; small edits; teams already using GitHub.
  - **Caveats:** It is not always the strongest option for large autonomous refactors. Teams should review policy, licensing, privacy, and training settings.
  - **Personal Comments:** This is the conservative coding-tool recommendation.
- **[Windsurf](https://windsurf.com/)**: Cursor-like AI editor worth comparing on pricing, model access, and workflow feel.
  - **Best For:** AI-native editor workflows; Cursor alternatives; fast application prototyping; integrated editor and agent experiences.
  - **Caveats:** It overlaps heavily with Cursor, so the main question is fit, not whether the category is useful.
  - **Personal Comments:** I would test this directly against Cursor before committing.
- **Cline, Roo Code, And Continue**: VS Code-based options for people who want more control over models, prompts, approval steps, or bring-your-own-key setups.
  - **Best For:** VS Code users; open-source or configurable workflows; careful approvals; testing multiple model providers.
  - **Caveats:** Configuration takes more work than Copilot or Cursor, and bring-your-own-key costs can be harder to predict.
  - **Personal Comments:** These are better for tinkerers than for people who want one simple subscription.

**Terminal And Harness Tools**

- **[Claude Code](https://www.anthropic.com/claude-code)**: Terminal coding agent that can inspect a repo, edit files, run commands, and iterate with tests.
  - **Best For:** Real codebase maintenance; refactors with reviewable diffs; test-driven fixes; terminal-first developers.
  - **Caveats:** Keep changes small, run tests, and review every diff. Do not give broad agent access to secrets or production systems.
  - **Personal Comments:** This is the terminal agent I would compare everything else against.
- **[OpenCode](https://opencode.ai/)**: Open-source terminal coding agent with broad model-provider support.
  - **Best For:** Terminal-first coding; bring-your-own-model workflows; local or alternative providers; configurable permissions.
  - **Caveats:** You are responsible for model choice, API keys, and cost control. Expect more setup than a bundled subscription.
  - **Personal Comments:** This is appealing if you want the workflow without committing to one model vendor.
- **[Aider](https://aider.chat/)**: Mature Git-native pair-programming tool that keeps AI changes close to commits, diffs, and explicit file context.
  - **Best For:** Git-centered development; small and medium changes; terminal pair-programming; transparent diffs.
  - **Caveats:** It rewards users who understand Git well. Model quality and cost depend on what you connect to it.
  - **Personal Comments:** This is still one of the clearest tools if you want AI work to stay grounded in Git.
- **[pi](https://pi.dev/)**: Minimal terminal coding harness built around composability: tools, extensions, skills, prompt templates, themes, model providers, API usage, and SDK integration.
  - **Best For:** Custom coding-agent workflows; provider-agnostic model use; automation; scripting; RPC; SDK and package-based extension work.
  - **Caveats:** It is more primitives-first than turnkey. If you want a polished editor assistant, start with Cursor or Copilot.
  - **Personal Comments:** This is for people who want to shape the harness around their workflow instead of accepting a fixed product design.
- **Codex CLI And Gemini CLI**: Official terminal paths into OpenAI and Google coding workflows.
  - **Best For:** Trying model-specific coding workflows; lightweight terminal tasks; comparing model ecosystems; using existing credits or subscriptions.
  - **Caveats:** They may be less configurable than OpenCode, Aider, or pi, and value depends on current model quality and plan limits.
  - **Personal Comments:** I would treat these as useful experiments, not automatic defaults.
- **Goose**: Open-source agent broader than coding, with desktop, CLI, and workflow automation use cases.
  - **Best For:** Open-source agent experimentation; workflow automation beyond code edits; internal agent-platform exploration.
  - **Caveats:** It may be more platform than focused coding assistant. Permission boundaries matter.
  - **Personal Comments:** Interesting if you want an extensible agent platform, less obvious if you only want code edits.

**Agent Interfaces And Cloud Agents**

- **[T3 Code](https://t3.codes/)**: Open-source desktop control surface for managing coding agents across repositories or parallel sessions.
  - **Best For:** Comparing agents side by side; multi-repository sessions; parallel agent workflows; visual control over CLI agents.
  - **Caveats:** It depends on the underlying agents and models you connect, and it adds another layer to debug.
  - **Personal Comments:** I think of this as an agent dashboard more than a model or coding assistant by itself.
- **Devin, Replit Agent, And Cloud Agents**: Managed remote environments for prototypes, isolated tasks, and delegated implementation work.
  - **Best For:** Greenfield prototypes; isolated tasks with clear acceptance criteria; browser-based development; remote agent execution.
  - **Caveats:** They need clear instructions and careful review. Be cautious with sensitive repositories, credentials, and production access.
  - **Personal Comments:** I would use these only when the task is well-scoped and reviewable.

## Local And Self-Hosted Inference

Use these when you want more privacy, local experimentation, cheaper high-volume inference, or control over model hosting. Most non-technical users can skip this category.

**Single-User And Developer Tools**

- **Ollama, LM Studio, Jan, GPT4All, And llama.cpp:** These are the most relevant local-AI tools for individual users and developers. Ollama is the easiest terminal-first default, LM Studio is the polished GUI, Jan and GPT4All are privacy-friendly desktop options, and llama.cpp is the low-level engine underneath much of the local ecosystem.
  - **Best For:** Local model testing; private drafts; offline experimentation; comparing open-weight models; developer sandboxes.
  - **Caveats:** Local models still depend on your hardware. Smaller models can be useful, but they are not a drop-in replacement for the best hosted frontier models.
  - **Personal Comments:** I would start with Ollama or LM Studio before touching the deeper local stack.
- **LocalAI, text-generation-webui, KoboldCpp, Llamafile, Lemonade, node-llama-cpp, And Docker Model Runner:** These are more specialized tools for people who already know why they want them.
  - **Best For:** Power-user web UIs; OpenAI-compatible local APIs; creative-writing setups; portable model bundles; AMD acceleration; JS integrations; containerized local models.
  - **Caveats:** Expect more setup, rougher edges, and more responsibility for model selection.
  - **Personal Comments:** Useful once you have a specific local workflow, not where I would start.

**Production Serving And Tuning**

- **vLLM, SGLang, TensorRT-LLM, TGI, And LMDeploy:** These are production-serving tools for teams running models at scale.
  - **Best For:** Multi-user inference; batching; throughput; OpenAI-compatible internal endpoints; optimized GPU serving.
  - **Caveats:** This is infrastructure work, not a consumer buying decision. You need operations skill and a real reason to self-host.
  - **Personal Comments:** I would only reach for these when hosted APIs become too expensive, too limiting, or unsuitable for privacy reasons.
- **Unsloth, Axolotl, And ExLlamaV2:** These are optimization and fine-tuning tools for teams customizing or accelerating open models.
  - **Best For:** QLoRA fine-tuning; production training pipelines; GPTQ or EXL2 inference.
  - **Caveats:** Fine-tuning is easy to overestimate. Try prompting, retrieval, and workflow changes before training your own model.
  - **Personal Comments:** Powerful, but usually later than people think.

## Research And Literature Tools

Use these when you need evidence, papers, citations, or source-grounded synthesis rather than general brainstorming.

- **Elicit, Consensus, Semantic Scholar, Scite, SciSpace, ResearchRabbit, Connected Papers, PapersFlow, And Zotero:** These are the core academic-research tools I would compare. Elicit is good for structured extraction, Consensus is good for evidence questions, Semantic Scholar is a strong free index, Scite helps with citation context, SciSpace explains dense papers, ResearchRabbit and Connected Papers map related work, PapersFlow helps with literature-review drafting, and Zotero remains the reference-management anchor.
  - **Best For:** Literature reviews; paper discovery; citation trails; evidence comparison; research organization.
  - **Caveats:** Do not outsource judgment to any research tool. Read the actual papers when the claim matters.
  - **Personal Comments:** I would pair Zotero with one discovery tool and one synthesis tool rather than trying to use all of them.
- **NotebookLM And Deep Research Tools:** NotebookLM is useful when you want source-grounded synthesis from uploaded documents. Deep Research-style tools are useful for broader scoping.
  - **Best For:** Uploaded PDFs; source-grounded summaries; meeting notes; quick research briefs; starting bibliographies.
  - **Caveats:** Source-grounded does not mean perfect. Check quotes, citations, and omissions.
  - **Personal Comments:** NotebookLM is one of the easiest recommendations in this category because the workflow is clear.

## Image, Video, And Audio Generation

This category changes fast. I would choose based on the kind of media you actually make, not on a single viral demo.

**Image**

- **Midjourney, FLUX, Stable Diffusion, Imagen, DALL-E, Adobe Firefly, Ideogram, Leonardo.ai, And Getty Generative AI:** Midjourney is still known for aesthetic output, FLUX and Stable Diffusion matter for open and API-driven workflows, Imagen and DALL-E are convenient inside larger ecosystems, Firefly and Getty aim at commercial safety, Ideogram is strong for typography, and Leonardo.ai is creator-friendly.
  - **Best For:** Concept art; marketing images; social assets; product mockups; typography experiments; controllable open workflows.
  - **Caveats:** Rights, likeness, training data, and commercial-use rules matter. Read the license before using outputs in paid work.
  - **Personal Comments:** I would pick based on workflow first: Midjourney for aesthetics, Firefly or Getty for safer commercial contexts, and Stable Diffusion or FLUX when control matters.

**Video**

- **Veo, Runway, Kling, Sora, Pika, Luma, Seedance, Hailuo, Wan, HeyGen, Synthesia, Hedra, D-ID, And Stable Video Diffusion:** Video is split between cinematic generation, social-first clips, open-weight experimentation, and avatar or talking-head tools.
  - **Best For:** Short clips; ad concepts; storyboards; character references; avatar videos; product explainers; experimental filmmaking.
  - **Caveats:** Quality, pricing, rights, and availability shift constantly. Sora's consumer app and API are marked as being discontinued in 2026 in the landscape notes, so do not build a long-term workflow around it without checking current status.
  - **Personal Comments:** I would test with your actual use case before paying. Video demos can be much better than normal workflow output.

**Audio**

- **ElevenLabs, Play.ht, Resemble AI, WellSaid Labs, Murf AI, Descript, Coqui TTS, Whisper, Voxtral, Suno, Udio, ElevenLabs Music, Stable Audio, AIVA, MusicGen, And Lyria:** Voice tools are useful for narration, dubbing, transcription, and voice cloning. Music tools are useful for demos, backing tracks, and creative experiments.
  - **Best For:** Voiceovers; transcription; dubbing; podcast editing; sound design; song sketches; background music.
  - **Caveats:** Voice cloning, music rights, likeness rights, and platform rules matter. Be especially careful with commercial release.
  - **Personal Comments:** ElevenLabs and Whisper are the easiest voice tools to understand. For music, I would treat outputs as creative drafts unless licensing is crystal clear.

## Agents And Automation Frameworks

These are for builders. If you are not building AI workflows or internal tools, you can skip most of this.

**Frameworks And SDKs**

- **LangGraph, CrewAI, AutoGen / AG2, Microsoft Agent Framework, Semantic Kernel, LlamaIndex, Pydantic AI, Smolagents, MetaGPT, OpenAgents, OpenAI Agents SDK, Claude Agent SDK, Google ADK, Vercel AI SDK, Mastra, And Mirascope:** This is the builder landscape for agent orchestration. LangGraph is the production default I would investigate first, CrewAI is approachable for role-based prototypes, Microsoft Agent Framework is important for Microsoft shops, LlamaIndex is strongest around retrieval, and the vendor SDKs are useful when you are committed to one ecosystem.
  - **Best For:** Stateful agents; multi-agent workflows; retrieval-grounded agents; typed agent apps; vendor-native agents; production orchestration.
  - **Caveats:** Frameworks add complexity quickly. Start with a boring workflow and add orchestration only when the problem requires it.
  - **Personal Comments:** I would default to the smallest framework that makes state, tools, and evaluation understandable.

**Computer Use, Workflow Automation, And Observability**

- **Anthropic Computer Use, OpenAI Operator / ChatGPT Agent, Browser Use, Playwright MCP, n8n, Zapier, Make, Dify, Flowise, Langflow, LangSmith, Langfuse, Arize Phoenix, Helicone, And Braintrust:** These cover browser control, no-code or low-code automation, visual LLM app building, and eval or tracing.
  - **Best For:** Browser tasks; workflow automation; internal prototypes; visual app builders; tracing; cost tracking; evaluation.
  - **Caveats:** Automation without observability becomes fragile fast. Anything that can act in a browser or workflow tool needs permission boundaries.
  - **Personal Comments:** n8n and Playwright MCP are the first things I would inspect for practical automation. Langfuse, LangSmith, or Braintrust become important once money or users are involved.

## RAG, Vector Databases, And AI Infrastructure

This category matters when you are building retrieval systems, internal search, document workflows, or production LLM apps. Most buyers should not start here.

- **Pinecone, Qdrant, Weaviate, Milvus, Chroma, pgvector, LanceDB, Zilliz Cloud, Deep Lake, Faiss, Vespa, Elasticsearch, OpenSearch, And Turbopuffer:** These are vector search and retrieval storage options. Pinecone is managed and easy to adopt, Qdrant is a strong open-source default, pgvector is attractive if you already live in Postgres, Chroma is good for prototypes, and Milvus or Zilliz matter at larger scale.
  - **Best For:** Semantic search; RAG; recommendation systems; internal knowledge bases; hybrid retrieval; production vector storage.
  - **Caveats:** A vector database does not fix bad data. Chunking, metadata, permissions, evaluation, and freshness usually matter more than the logo.
  - **Personal Comments:** I would start with pgvector, Qdrant, or Chroma unless scale or managed operations clearly push you elsewhere.
- **OpenAI Embeddings, Voyage AI, Cohere Embed, BGE, E5, nomic-embed-text, Jina Embeddings, LlamaIndex, LangChain, Haystack, DSPy, RAGFlow, Verba, Quivr, Khoj, Unstructured.io, LlamaParse, Firecrawl, Reducto, Docling, OpenRouter, LiteLLM, Portkey, And MCP Servers:** These are the surrounding pieces for embeddings, retrieval frameworks, document ingestion, model routing, and tool integration.
  - **Best For:** Document parsing; retrieval pipelines; model routing; OpenAI-compatible gateways; local knowledge apps; MCP-based tool use.
  - **Caveats:** Each extra layer needs a reason. Keep the first system boring and measurable.
  - **Personal Comments:** I would pay special attention to ingestion quality and evaluation before arguing about vector database choice.

## Writing, Editing, And Documents

For workplace writing, the meaningful distinction is not only which tool writes best. It is where the data goes, whether prompts and outputs are retained, whether enterprise controls exist, and whether the tool fits the document system people already use.

- **ChatGPT And Claude:** Strong general-purpose tools for drafting, rewriting, structure, long-form prose, and technical explanation.
  - **Best For:** Drafts; rewrites; outlines; technical explanations; long-form editing; policy and documentation work.
  - **Caveats:** Do not paste sensitive material into consumer plans unless policy allows it. Review important writing for accuracy, tone, and missing context.
  - **Personal Comments:** Claude is usually my first choice for careful prose, while ChatGPT is the easier broad default.
- **Grammarly, Notion AI, Google Gemini In Docs/Gmail, And Microsoft Copilot In Word/Outlook:** Embedded writing tools that live where work already happens.
  - **Best For:** Email; documents; notes; workplace tone; grammar; summaries; enterprise document workflows.
  - **Caveats:** Integration is useful, but governance still matters. Check retention, training, admin controls, and sharing defaults.
  - **Personal Comments:** Embedded tools win when switching costs are the main barrier.
- **Lex, Sudowrite, Writer, Jasper, And Copy.ai:** Specialized writing and marketing tools.
  - **Best For:** Creative writing; brand-controlled copy; marketing drafts; campaign variants.
  - **Caveats:** They can produce polished generic prose. Brand quality still needs human taste and review.
  - **Personal Comments:** I would use these only when the specialized workflow beats a general assistant plus templates.

## Meetings, Transcription, And Productivity

Meeting bots are high-risk because they capture sensitive spoken content that people may not think of as documents. Treat them as data-capture systems, not just convenience tools.

- **Otter.ai, Fireflies.ai, Fathom, Granola, tl;dv, Zoom AI Companion, Microsoft Teams Copilot, And Google Meet Gemini:** Meeting transcription, summaries, searchable meeting histories, and meeting-native assistant features.
  - **Best For:** Meeting notes; searchable transcripts; CRM handoffs; project follow-up; Zoom, Teams, or Google-native summaries.
  - **Caveats:** Consent, retention, storage, sharing, and admin controls matter. Some meetings should not have a bot in them.
  - **Personal Comments:** I would approve these carefully and define where they are allowed before rolling them out broadly.

## Data Analysis, BI, And Analytics

The serious limitation here is semantic correctness. AI over dirty BI models produces confident nonsense. These tools work best when definitions, permissions, and data models are already managed.

- **ChatGPT, Claude, Julius AI, Power BI Copilot, Tableau Agent, Databricks Genie, Hex, Deepnote, ThoughtSpot Spotter, Sigma, Qlik, And Looker Gemini:** File analysis, spreadsheet help, notebook workflows, natural-language BI, and enterprise analytics assistants.
  - **Best For:** Ad hoc CSV analysis; spreadsheet explanation; chart drafts; BI Q&A; collaborative notebooks; lakehouse analytics.
  - **Caveats:** If the semantic layer is wrong, the AI answer will be wrong. Permissions, data lineage, and metric definitions matter.
  - **Personal Comments:** I would start with controlled, low-stakes analysis before trusting these with decisions.

## Enterprise Search And Knowledge Assistants

For organizations, this category can matter more than consumer chatbots because it touches internal knowledge, permissions, retention, and auditability.

- **Glean, Microsoft 365 Copilot, Google Gemini Enterprise, ChatGPT Enterprise / Team, Claude Enterprise / Team, Hebbia, Dust, Dify, Flowise, LangChain, LangGraph, LlamaIndex, Haystack, Pinecone, Weaviate, Qdrant, Chroma, Elastic, And OpenSearch:** Enterprise search, document analysis, internal assistants, RAG frameworks, vector databases, and hybrid search systems.
  - **Best For:** Internal search; governed assistants; document-heavy analysis; legal and finance workflows; custom internal AI apps; permission-aware retrieval.
  - **Caveats:** Connecting to data is not enough. The system must enforce permissions, log usage, support retention rules, and avoid training on your content unless explicitly approved.
  - **Personal Comments:** I would spend more time on permissions, ingestion quality, and evaluation than on the vector database logo.

## Developer Platforms And APIs

These matter when you are building AI into products or internal systems rather than buying an end-user app.

- **OpenAI API, Anthropic API, Google Vertex AI / Gemini API, Azure OpenAI / Azure AI Foundry, AWS Bedrock, Mistral AI, Cohere, Together AI, Fireworks, Groq, Cerebras, Hugging Face, Replicate, Modal, Baseten, And BentoML:** Model APIs, enterprise cloud AI platforms, hosted open-weight inference, model hubs, and deployment infrastructure.
  - **Best For:** Product features; internal tools; enterprise deployments; multimodal apps; hosted open models; custom model deployment.
  - **Caveats:** Vendor choice affects data handling, latency, cost, model availability, regional requirements, and operational complexity.
  - **Personal Comments:** I would choose the platform based on governance and deployment needs, not only model benchmarks.

## Practical Shortlists

**Tools For Ordinary Staff**

- **General Assistant:** ChatGPT, Claude, Gemini, Microsoft Copilot.
- **Search And Research:** Perplexity, ChatGPT Deep Research, Elicit.
- **Meeting Notes:** Otter, Fireflies, Zoom AI Companion, Teams Copilot.
- **Writing:** ChatGPT, Claude, Grammarly, Microsoft Copilot.
- **Slides And Design:** Canva, PowerPoint Copilot, Adobe Firefly.
- **Data And CSV Analysis:** ChatGPT, Claude, Julius, Power BI Copilot.

**Tools For Developers**

- **IDE Assistant:** GitHub Copilot, Cursor, Windsurf, Continue.
- **Terminal Or Code Agent:** Claude Code, Codex, Aider, Cline.
- **Local Models:** Ollama, LM Studio, Open WebUI.
- **Inference Serving:** vLLM, llama.cpp, TGI, SGLang.
- **RAG Apps:** LlamaIndex, LangChain / LangGraph, Haystack, Dify.
- **Vector Database:** Qdrant, Weaviate, Pinecone, Chroma.

**Tools For Organizations**

- **Enterprise Chat:** ChatGPT Enterprise, Claude Enterprise, Microsoft 365 Copilot, Gemini Enterprise.
- **Internal Search:** Glean, Microsoft 365 Copilot, Google Gemini, Hebbia.
- **BI And Analytics:** Power BI Copilot, Tableau Agent, Databricks Genie.
- **Secure App Building:** Azure AI Foundry, AWS Bedrock, Vertex AI, OpenAI API, Anthropic API.
- **Self-Hosted Or Private Workflows:** Open WebUI, AnythingLLM, Dify, Flowise, vLLM.

## Decision Tree

- **Does it touch sensitive data?** If yes, prefer enterprise-licensed tools with contractual controls. Avoid random consumer tools.
- **Does it need access to internal files, email, calendar, or code?** If yes, use Microsoft 365 Copilot, Google Gemini, Glean, ChatGPT Enterprise, Claude Enterprise, or a controlled internal RAG system.
- **Is it for coding?** Use GitHub Copilot, Cursor, or Windsurf for IDE work. Use Claude Code, Codex, Aider, Cline, or similar agents for repo work.
- **Is it for public research?** Use Perplexity, Elicit, Consensus, Scite, or Semantic Scholar, then synthesize with ChatGPT, Claude, or NotebookLM.
- **Is it for confidential research data?** Use enterprise tools, local or self-hosted tools, or a governed internal service.
- **Is it creative or media work?** Use Canva, Adobe Firefly, Runway, Sora, Veo, Kling, ElevenLabs, or similar tools, but check copyright, consent, likeness, and data-use policies first.

## Buying Advice

- **Pay for one general assistant first.** For most people, that means ChatGPT or Claude.
- **Add a coding tool only if you code every week.** Cursor, Copilot, Claude Code, OpenCode, Aider, and pi are easiest to justify when they replace real development time.
- **Use Perplexity when sources matter.** It is strongest as a research companion, not as your only assistant.
- **Pick a category before picking a brand.** Decide whether you want an editor assistant, terminal agent, open-source tool, cloud agent, or orchestration interface.
- **Prefer reviewable workflows.** The best coding tools make diffs, tests, logs, and rollback easy.
- **Watch usage-based pricing.** Bring-your-own-key and agentic tools can burn money faster than autocomplete tools.
- **Review subscriptions monthly.** AI tools overlap heavily, and it is easy to pay for three tools when one would do.
- **Treat workplace AI as governance, not novelty.** Ask what data is entered, where it is stored, whether it is used for training, whether prompts and outputs are logged, and whether the tool supports SSO, admin controls, retention, audit, and existing permissions.
- **Maintain approved-use lists.** At minimum, separate tools approved for general use, tools approved only for public or non-sensitive data, and tools approved for sensitive or internal data under enterprise controls.
