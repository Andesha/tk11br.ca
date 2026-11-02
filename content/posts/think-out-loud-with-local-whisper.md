---
title: "Think out loud with local Whisper"
subtitle: "Free, private voice-to-text needs a lot less hardware than you'd think"
description: "Talking through a problem is a good way to organize your thoughts, and OpenWhispr with a local Whisper model lets you capture it for free on hardware you probably already have."
date: 2026-11-02T11:00:00-05:00
draft: false
tags: ["workflow"]
---

Personally, I feel there's a part of your brain that organizes its thoughts pretty well when it's thinking out loud. You start talking through a problem and halfway through the sentence you realize what the actual problem is. Classic rubber ducky type stuff. Recording that and getting it into text is really useful, and it turns out you can do it for free on hardware you probably already have.

To be clear, I'm not suggesting the full AI psychosis of getting rid of your keyboard and only using a microphone. I still type most things. But for stream of consciousness stuff, where you're really just trying to get organized, and for notes in general, it's pretty useful.

## What I use

I use [OpenWhispr](https://github.com/OpenWhispr/openwhispr). You press a hotkey, talk, press it again, and the text shows up wherever your cursor is. It's MIT licensed, runs on macOS, Windows, and Linux, and it can even use custom providers. Lately, I've done about 185 dictations, roughly 46 minutes of audio and around 6,000 words.

## Running it on your own machine

The cool thing is that you probably don't need a GPU for this. OpenWhispr runs the model locally with [whisper.cpp](https://github.com/ggml-org/whisper.cpp), which can run on just a CPU. If you do have a GPU, it'll use it through Metal on a Mac, CUDA on NVIDIA, or Vulkan on AMD and Intel. The models are also pretty small. Here's roughly where I'd start:

- Any recent laptop: base, a 142 MB download that needs about 400 MB of memory, and the one OpenWhispr recommends
- A bit more room: turbo-q5, a 574 MB download
- A GPU with 4 GB or more: turbo (1.6 GB) or even large-v3 (3 GB, about 3.9 GB of memory)

Setup is pretty much: install it, switch transcription to local in the settings, pick a model, and let it download. That's it. No API keys, and your audio never leaves your computer. If the result is too slow, drop down a size. If it makes too many mistakes, move up one.

## The step up

On my own laptop I don't actually run the model. I run whisper-large-v3-turbo on a GPU machine at SHARCNET and point OpenWhispr at it, so the laptop just records audio and sends it over. Same privacy story, since the audio never leaves hardware we control, but I get the bigger model and the laptop does no work.

You don't need this to get started, but it's a nice option once you're hooked.

## Try it

Install OpenWhispr, pick base or turbo-q5, and use it for a week of brain dumps and notes. If it isn't useful, you've lost nothing but a small download. It's also a pretty interesting look at what you can host for yourself these days.
