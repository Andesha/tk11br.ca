---
title: "Cython: A First Look"
subtitle: "Surely not 40x, right?"
date: 2022-03-20T14:40:38-04:00
draft: false
tags: ["talk", "python"]
---

Back when I first got hired at SHARCNET, I used a lot of Python. I mean a lot. What this meant is that I quickly became the lightning rod for all Python related questions (and commentary).

During a fun Friday chat, a colleague remarked that Python was on average 40x slower than C++. I defended my current language of choice saying it was better than that, surely. To make a long story short, I was wrong. It really is about 40x slower depending on the problem. Determined to prove myself capable, and my language of choice a bit more defensible, I decided to look into ways to make Python faster.

I eventually landed on Cython. Turns out the best way to make Python faster was to use as much C++ as possible.

Below is my abstract for the talk as well as the recording:

<iframe src="https://www.youtube.com/embed/y6bKDKFavPA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

"Often we write programs in Python for convenience, not for speed. When work becomes elevated to High Performance Computing (HPC) environments, speed once again becomes a concern. Cython is an extension of Python which allows functions to be compiled as C (or C++) and recover the significant performance trade-offs of Python. Cython achieves this by supporting calling C functions, declaring of type information, as well as providing access to C++ STL functionality. Popular packages and libraries that take advantage of Cython include: TensorFlow, OpenCV, NumPy, Pandas, and more. This webinar will cover a basic introduction to Cython, a demo translating vanilla Python into Cython, followed by a short demo of how to run Cython in our own Compute Canada HPC environments. Experience with Python will be expected, while familiarity with C/C++ and Jupyter notebooks will be helpful. Webinar material and code will be made available on GitHub for reference."
