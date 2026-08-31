---
title: "From a Throwaway QC Prototype to PyLossless"
subtitle: "Getting the big impossible blob of code to run"
description: "How a throwaway repository helped prove a new EEG quality-control workflow before it moved into PyLossless."
date: 2026-08-28T12:00:00-04:00
draft: true
tags: ["python", "eeg", "preprocessing", "workflow", "PyLossless", "agents"]
---

In March 2025, I had an idea for improving quality control in [PyLossless](https://github.com/Andesha/pylossless). I wanted to bring back being able to review an EEG recording to select independent components, choose a time window, and immediately compare the raw signal against the result of removing those components.

It had been done in the previous version in MATLAB, but I was less familiar with the inner working of PyLossless at the time. I was also a complete novice when it came to things like Qt 5, PyQt, and the [mne-qt-browser](https://github.com/mne-tools/mne-qt-browser).

To be clear, trying to build this system would require knowing the PyLossless pipeline state, MNE's ICA tools, the MNE Qt browser, Matplotlib figures, file watching, and the actual EEG-cleaning logic. I had already failed a few attempts at this before because I just got tired of there being too many things to juggle.

On the suggestion of a friend, I made a new repository called [`pilot-qc`](https://github.com/Andesha/pilot-qc) and decided to throw some AI at it and see what would happen. Worst case would only be another failure.

## Let the prototype be ugly

There wasn't much of a plan beyond getting something on the screen.

The commit history tells the story pretty well. The first two commits landed on March 21. One was called `first commit`. The next was `wow this is amazing`, which is honestly a pretty good record of how I felt at the time. Later that day, I had figures communicating with each other, scalp snapshots for a selected time window, a history of component rejection, and raw and cleaned signals appearing together.

The prototype used a file named `.local_reject` to pass state between the plots. It stored a selected time range and a set of rejected ICA components. A Qt timer checked the file every half second. When something changed, the code copied the original recording, applied the current ICA exclusions, cropped it to the selected window, and plotted the cleaned channels over the raw channels.

Would I design a finished application this way? Absolutely not. But it answered the question I actually had. Could a reviewer change the rejected components and see what those decisions did to the EEG? All in Python and with the mne-qt-browser? Yep.

## AI made the scratch repository more useful

This was early in my adoption of AI coding tools. The repository description was pretty clear about it: "Trying some AI assisted QC figure generation."

I knew what I wanted from the EEG review process. The plotting and GUI code was another story. AI made it cheap to try another event handler, connect two figures, or rebuild a plot when the first attempt did something weird. Instead of staring at documentation and trying to design the whole thing in my head, I could run some code and complain about what it did.

The scientific judgement still came from me. An agent could connect a click to a plot update. It couldn't decide which comparison would actually help someone judge whether removing an ICA component improved the recording. AI got me through unfamiliar implementation details quickly, and the throwaway repository kept the resulting mess away from PyLossless.

This worked much better than asking for a polished feature all at once. Generated code was allowed to be awkward in there. Anything I did was just a throwaway anyway.

## Moving the useful part into PyLossless

The prototype didn't become a package or a long-lived dependency. I had briefly wondered in the PyLossless issue whether it should be a submodule. Thankfully, I talked myself out of that one.

I moved the useful parts into PyLossless instead.

On April 10, about three weeks after the first experiment, I opened and merged [PyLossless PR #29](https://github.com/Andesha/pylossless/pull/29). It added the initial `pylossless/qc.py`, including the component topographies, scrolling ICA time courses, and raw-versus-cleaned comparison tested in `pilot-qc`. The pull request added 481 lines across seven files.

The merged code was still pretty rough. It even kept my hacky local file based approach while the interaction settled down. That was fine. I didn't need the prototype to produce immaculate code that could be copied over unchanged. I needed proof that this collection of plots and interactions could work at all.

That changed the work completely. I wasn't trying to make the full QC system while juggling six libraries in my head anymore. I just needed to take the important parts from what worked, and bring that over. I now had my old QC workflow back!

I've since gone back and cleaned up some chunks and improved the local file calling. But I couldn't have done any of that without the throwaway prototype to fall back on.

## Try the intimidating version somewhere disposable

A throwaway prototype is great when a feature feels too large because a bunch of unknowns are stuck together. Try pulling them out of the main project. Use real enough data to test the idea, but don't spend the first day deciding where every class belongs. Nobody cares yet.

Make the smallest repository that can answer your question. Let it use a weird little file for communication if that gets the idea on screen. Let the commits say `wow this is amazing`. Clean up whatever survives later.

If your favourite project has a feature you've been avoiding because it looks like one big impossible blob, give it a disposable repository and an afternoon. See what happens.
