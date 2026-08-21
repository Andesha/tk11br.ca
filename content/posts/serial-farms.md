---
title: "Serial Farms: Package Options and When to Switch to Farming"
subtitle: "Submitting hundreds of small jobs without making a mess"
description: "A practical comparison of job arrays and serial-farming tools for running many small jobs on HPC systems."
date: 2025-12-03T12:00:00-05:00
draft: false
tags: ["talk", "hpc", "scheduling"]
---

Submitting a few small jobs one at a time is fine. Submitting hundreds that way is annoying for you and hard on the scheduler.

This webinar compared ways to group lots of serial tasks into manageable jobs. I covered when ordinary submissions stop making sense, how array indexes can drive repeated runs, and when it is time to use a serial farm.

<iframe src="https://www.youtube.com/embed/sMZ13XJQiWo" title="Serial Farms: Package Options and When to Switch to Farming" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Abstract

Small jobs are convenient to submit individually, but at scale they can overload a scheduler, inflate queue times, and ultimately reduce throughput. This webinar examines practical strategies for consolidating large numbers of short tasks, including job arrays, task-bundling techniques, and wrapper-based aggregation. We will discuss how these approaches differ in overhead, portability, scheduler behavior, and job-failure handling. The session will also provide guidance on recognizing when packaging options no longer yield sufficient throughput and when transitioning to a serial-farming model becomes advantageous. Serial farms can mitigate scheduler pressure, improve wait times on busy clusters, and offer more predictable performance. Examples will be provided throughout the webinar and shared on GitHub for future reference.

The [SHARCNET seminar archive](https://helpwiki.sharcnet.ca/wiki/Online_Seminars) has the event listing.
