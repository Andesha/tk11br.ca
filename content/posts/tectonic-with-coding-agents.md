---
title: "Tectonic makes LaTeX easier to work on with an agent"
subtitle: "A local alternative to Overleaf for solo document work"
description: "Using Tectonic and a coding agent to edit LaTeX, compile a résumé, and check the rendered PDF without browser automation."
date: 2026-10-13T12:00:00-04:00
draft: false
tags: ["LaTeX", "Tectonic", "agents", "workflow"]
---

I recently used [Tectonic](https://tectonic-typesetting.github.io/) to rerender my résumé and make changes with a coding agent. This made the back-and-forth a lot easier. I could ask for a change, have the agent edit the underlying LaTeX, and get another PDF to check.

In my opinion, Tectonic and a coding agent are now a pretty practical alternative to Overleaf if you're working on a document by yourself. The agent can work directly on local files and run the compiler. This way you don't need it clicking around a browser through computer-use tools trying to diagnose how your tables are formatted.

## A simpler local setup

If you haven't used LaTeX, it's a way to write documents as source files and compile them into typeset output, usually a PDF. It's useful for résumés and papers, especially when you want precise formatting or have lots of equations. Your textbooks use it, for example.

Getting a local LaTeX setup working can be more effort than you wanted to spend on editing a document. Some of this technology is unfortunately pretty ancient. Tectonic makes that part simpler. It's a TeX/LaTeX engine distributed as a single executable, and it downloads the support files it needs instead of requiring you to install a full LaTeX distribution up front.

There are [installation options](https://tectonic-typesetting.github.io/book/latest/installation/) for different systems. Once it's installed, compiling a document can be as simple as:

```sh
tectonic resume.tex
```

That produces `resume.pdf`. Tectonic also handles the repeated compilation passes that TeX and BibTeX can need. You'll need network access to download support files that aren't already cached, but you don't have to manage those downloads yourself.

## Let the agent keep trying

The useful part for me was making the changes interactively. LaTeX has plenty of classic formatting problems. Something doesn't fit, spacing looks wrong, or a change in one place moves something somewhere else. An agent doesn't really run out of things to try, which is pretty useful when you're working through that kind of problem.

Ask the agent to edit the source, compile it, and then render the PDF pages to images for visual inspection if it has the tools to do that. If the change didn't work, it can keep trying. Tectonic makes it easy for the agent to build/compile the PDF, and then other standard agent tooling can view the PDF for issues.

That last step is the big win. A successful compile tells you that you produced a PDF, not that the layout looks right. Ask the agent to review the rendered pages rather than stop as soon as the command succeeds. You should still look at the final document yourself every time of course.

This doesn't replace Overleaf's shared editing and collaboration features. But for a document I'm working on myself, letting an agent edit and compile the files directly is a much simpler workflow than having it operate a web editor.

If you've got an existing LaTeX document, try giving your agent the source and asking it to make a change with Tectonic. It worked pretty well for my résumé!
