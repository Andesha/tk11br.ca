---
title: "What Does a GPU-Hour Actually Measure?"
subtitle: "A duration without the hardware and allocation details isn't useful for comparison"
description: "GPU-hours hide differences in GPU models, whole-device allocations, and MIG slices. Research reports need to say what was actually used and how the total was calculated."
date: 2026-09-22T10:30:00-04:00
draft: false
tags: ["hpc", "metrics"]
---

You've probably seen a line like this in a paper or grant report:

> We used 10,000 GPU-hours.

It looks like a useful answer. There's a number and a unit. Very official.

But what does a GPU-hour actually measure? On its own, pretty much nothing. I can't compare that number with another project until I know what counted as a GPU, whether it was a whole device or a slice, and how the authors calculated the total.

## One GPU-hour is not like another

An hour on an NVIDIA A100, H100, or B200 counts as one GPU-hour under the usual calculation. That doesn't make those hours equivalent. These are different generations of hardware with different memory capacities, bandwidth, and compute capabilities. They have tons of different features too.

The workload matters too. A newer GPU might make a huge difference for one model and barely move another. `number of GPUs × elapsed time` throws all of that information away. It's pretty much the worst collapsing across dimensions you could do.

In the past, research papers have long reported CPU models and architectures because an hour on one processor doesn't automatically compare with an hour on another. Plenty of papers still include that detail, and they should. GPU reporting deserves at least as much care.

## Device slicing makes it worse

Multi-Instance GPU, usually called MIG, is device slicing. An administrator can divide one physical NVIDIA GPU into isolated instances, each with a portion of the compute and memory resources. NVIDIA's [MIG documentation](https://docs.nvidia.com/datacenter/tesla/mig-user-guide/introduction.html) says supported GPUs can be divided into as many as seven instances.

This is a good thing. Several jobs can share an expensive GPU without fighting over the same resources. Schedulers can present each slice to a job much like a physical GPU. [Slurm can schedule MIG instances as individual GPU resources](https://slurm.schedmd.com/gres.html), for example.

Here's where the reporting gets weird. Say two jobs each run for one hour. One gets an entire H100. The other gets one MIG slice of an H100. If the accounting system calls each allocation one GPU, both jobs used one GPU-hour. Same number. Very different allocation.

Calling these "MIG-hours" or "slice-hours" doesn't fix much by itself. MIG profiles assign different amounts of compute and memory. Ten hours on a small slice and ten hours on a large slice still become ten slice-hours when the report leaves out the profile.

## Show your math

Different people need different numbers. A cluster operator may care about how long allocations were occupied. A funding report may care about use of the physical hardware. A researcher needs enough detail to understand or reproduce an experiment. Those are different questions. They don't have to produce the same total.

One report might count every scheduled MIG instance as a GPU. Another might convert slices into fractions of a physical device. It could count allocated time even when the job wasn't keeping the device busy. All of those approaches can make sense for a particular job. Calling every result "GPU-hours" is the problem. Once the calculation disappears, the reader can't recover what happened.

A universal normalized GPU-hour sounds tempting, but I don't think it fixes this. Converting every device and slice into one equivalent unit requires assumptions about relative performance. Those assumptions change with the workload, software, numerical precision, and bottleneck. It's problematic either way.

## At least report this much

If you publish GPU usage, include:

- the GPU manufacturer and model
- whether jobs received whole devices or slices
- the MIG profile or equivalent partition size when slicing was used
- the number of allocations
- the elapsed duration
- the exact calculation behind any aggregate total

A methods section or figure caption could say:

> We used eight allocations of an NVIDIA H100 `3g.40gb` MIG profile for five hours each, for 40 H100 `3g.40gb` slice-hours. We calculated slice-hours as the number of allocated instances multiplied by allocation duration.

Yes, that's longer than "40 GPU-hours." You can also tell what it means. The reader knows these were slices, which hardware they came from, and how the total was produced.

If the work used several device models or MIG profiles, report them separately. Don't add unlike allocations together and slap a precise-looking label on the result.

## A caption is allowed to do some work

A single GPU-hour total fits nicely on a dashboard. The useful version takes a caption, a definition, or a few lines in a methods section. That's fine. This is what those things are for.

GPU-hours can still work as internal shorthand for one stable pool of identical hardware. Everyone in that context knows what the unit means. The shorthand falls apart as soon as the number leaves that context.

Don't make readers guess. Name the hardware, describe the allocation, and show your math.
