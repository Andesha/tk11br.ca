---
title: "How Do You Test Whether EEG Got Cleaner?"
subtitle: "One metric is not going to do it"
description: "A failed attempt to add cleanliness tests to PyLossless, and why evaluating EEG preprocessing needs several kinds of evidence."
date: 2026-08-31T12:00:00-04:00
draft: false
tags: ["python", "eeg", "preprocessing", "workflow", "PyLossless"]
---

In April 2025, I opened a very short issue in my PyLossless fork:

> there should be some sort of metric out there that we can add to the test suite to show the data is "cleaner" after pipeline runs

Seemed reasonable and I figured that there would be a publication or something out there answering this. This came up because I was rounding out a test suite. I wanted something that could tell me if the data was "better" in a meaningful way, because I already had one making sure the input was different than the output.

I tried generating a bunch of quality metrics to fill that gap. The result was hundreds of lines covering signal-to-noise ratio, extreme amplitudes, variance, kurtosis, frequency bands, and ICA components. I even put pytest examples that asserted the numbers improved after cleaning.

It looked pretty complete. I merged it, and let it run on the first example case I had handy. It promptly failed half of the improvement criteria despite the fact that I knew it was cleaner... At least I didn't have to write all of those tests by hand?

## The metric can reward the wrong thing

One metric treated the difference between the original and cleaned recordings as noise, then used that difference to calculate an improvement in signal-to-noise ratio. That is a pretty big assumption. The pipeline changed the data, therefore the change was noise, therefore removing it was an improvement. Pretty much unusable because optimally for this metric you just reject everything.

Another metric rewarded reductions in extreme amplitudes and variance. That can be useful if the pipeline is removing large artifacts. It can also reward a pipeline for flattening the signal.

The frequency metrics had the same problem again. Less power in a band associated with muscle or line noise might be good. Less power in a band I care about for the actual research question might be very bad.

Pretty much all of the early "cleanliness" metrics just benefit from rejecting everything. Funny, but not useful.

## Compare the things that can disagree

Take a basic ERP experiment. One rejection policy removes nearly every blink, but throws away a lot of trials. Another keeps more trials and leaves a bit more ocular activity.

Which one is better? Kind of depends. Counting blinks favours the first. Counting trials favours the second. Neither really tells me what happened to the ERP.

I would also want to compare the effect estimate and its uncertainty. Did the amplitude move? Did the confidence interval get much wider? Does the result hold under both policies?

This is not an excuse to tune preprocessing until the p-value gets smaller. A stronger effect is not automatically a more correct effect. If anything, a large change in the result is a reason to stop and figure out what the pipeline is doing.

Researchers already report rejected trials, interpolated channels, ICA decisions, and final statistics in papers. I think we should start looking at these together much earlier, while the pipeline is still being built.

A useful test would probably keep a small set of results instead of trying to collapse everything into one score:

- Did the targeted artifact decrease?
- How many channels, samples, or trials were lost?
- Did signal properties relevant to the study change?
- Did the effect estimate and its uncertainty stay reasonably stable?

The disagreement between those answers is really useful.

## PyLossless is set up nicely for this

Luckily, this is where the design of [PyLossless](https://github.com/lina-usc/pylossless) helps.

PyLossless records possible problems before deciding what to remove with its RejectionPolicy class. It can flag channels, periods of time, and independent components while leaving the source recording alone. A rejection policy later decides which channels to interpolate, which periods to reject, and which components to remove.

That means I can take the same set of flags and try more than one reasonable policy. I can compare a stricter policy against a more relaxed one without changing the detection step every time. Then I can look at artifact reduction, retained data, and the study result side by side.

PyLossless doesn't have that whole reporting system right now. This isn't me announcing a finished feature. What I like is that the non-destructive approach gives us a sensible way to move forward.

The first version could be pretty boring. Save the before-and-after artifact measurements. Count what each policy removes. Run a small analysis that represents the eventual research question. Put the results beside each other.

That would be much more useful than my original pile of quality metrics pretending to know whether the EEG got cleaner.

The test I wanted back in April was not a single assertion after all. It was a comparison. That is a little harder to fit into pytest, but at least it asks the right question.
