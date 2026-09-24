---
title: "What Should EEG Cleaning Improve?"
subtitle: "The trade-offs matter more than a cleanliness score"
description: "How to compare EEG preprocessing choices without mistaking cleaner-looking data for a better estimate."
date: 2026-09-23T12:00:00-04:00
draft: false
tags: ["eeg", "preprocessing"]
---

When I [tried to write tests for whether EEG got cleaner]({{< relref "cleanliness-metrics-eeg-pipelines.md" >}}), several of my metrics rewarded rejecting everything. This is an absolutely classic case of badly defined test metrics.

Consider an ERP study and two cleaning policies. One rejects nearly every blink, along with a lot of trials. The other leaves a little ocular activity but keeps more trials. If I only count blinks, the first one wins. If I only count retained trials, the second one wins. Neither one is really better than the other.

I'd be wary of picking a method because it has a higher signal-to-noise ratio or fewer outliers despite how many publications in the field report this way. Those numbers depend on how you define signal and noise. My old metric counted the difference between raw and cleaned data as noise. By that definition, removing more data looked like progress. A flat recording could also score well on a variability metric and be useless for the study.

That doesn't make artifact measures pointless. I just want to know whether a blink correction reduced blink contamination. I also want to know what it cost.

## Compare what you get and what you lose

For an actual study, I'd put a few plausible preprocessing choices next to each other and ask:

- How much targeted artifact remains? Which type of artifact hurts us the most?
- How many channels, time periods, and trials did each choice remove or reconstruct? Did that differ between conditions or participants?
- What happened to the effect estimate and its uncertainty, such as its confidence interval?

A narrow confidence interval isn't automatically good. If a pipeline systematically distorts the effect, it can give a precise answer to the wrong question. A smaller p-value isn't always the goal either. If two pipelines disagree, I'd look at what each one removed before picking the result I like better.

Real recordings usually don't tell us the true effect, so comparing their results can't establish which pipeline is correct. If I can simulate data or inject a known effect into realistic recordings, I can ask a harder question: does the method recover the effect without systematic bias? Across repeated simulated datasets, do nominal 95% confidence intervals contain the known effect about 95% of the time? How wide are those intervals, and how much data did the method discard to get them? This is the sort of thing I want to see in pipeline style publications.

The answer might depend on the study. A method that throws away a lot of time could be acceptable for one analysis and disastrous for another. An aggressive trial-rejection rule might remove artifacts while leaving too few trials for a useful estimate, or reject one condition more often than the other. That's information a single cleanliness score won't give me.

I don't expect every EEG study to run a giant pipeline benchmark or accidentally turn into a methods paper. A useful first pass is to run a couple of defensible cleaning choices on the same data and put the artifact measurements, data-loss counts, and effect estimates side by side. If we can test against a known effect, we should check whether the method recovers it. That's more work than picking the cleanest-looking trace, but at least it tells us what we paid for the cleaning.

## Related posts

- [How Do You Test Whether EEG Got Cleaner?]({{< relref "cleanliness-metrics-eeg-pipelines.md" >}})
