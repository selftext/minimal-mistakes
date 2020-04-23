---
title: Recent Readings in Experimentation and Causal Inference
excerpt: "New papers and blog posts from the A/B testing literature."
header:
  overlay_color: "#777"
---

I’ve worked on experimentation platforms at Kickstarter, Spotify, and, most recently, Sawyer. At Sawyer I’m starting from scratch, designing the architecture for assigning treatment groups and tracking outcomes, thinking through the methodology for analyzing results, and building organizational processes for running rigorous experiments and learning from them. Meanwhile, I’m trying to keep things simple, use off-the-shelf technology whenever possible, and ensure buy-in from across the company.

To guide this work, I’ve been diving back into the A/B testing literature. A few papers and blog posts have been particularly helpful, so I’m documenting them here (for others, and for my future self).

## Architecture
I don't think much of Uber as an organization, but it’s hard not to be impressed by their technology. This [deep dive into XP](https://eng.uber.com/xp/), Uber’s experimentation platform, hits all my buttons, from “Bayesian optimization with contextual multi-armed-bandit tests” to “block bootstrap and delta methods to estimate standard errors.”

As a bonus feature, it’s also worth checking out [Uber’s post on analyzing quantile treatment effects in experiments](https://eng.uber.com/analyzing-experiment-outcomes/).

## Sample sizes
Optimizing sample sizes is particularly important for early-stage companies without a lot of traffic. Chris Said has [an interesting series of posts](https://chris-said.io/2020/01/10/optimizing-sample-sizes-in-ab-testing-part-I/) on the subject.

Also worth checking out is [this paper by Elea McDonnell Feit and Ron Berman on "profit-maximizing A/B tests"](https://arxiv.org/abs/1811.00457).

## Analysis
There’s no shortage of writing on analyzing A/B tests, but a few recent posts caught my attention. Etsy wrote about [the causal analysis of cannibalization in online products](https://codeascraft.com/2020/02/24/the-causal-analysis-of-cannibalization-in-online-products/).  LinkedIn has a piece on [detecting network effects in experiments](https://engineering.linkedin.com/blog/2019/06/detecting-interference--an-a-b-test-of-a-b-tests). And Convoy has [a good overview of Bayesian approaches to A/B testing](https://medium.com/convoy-tech/the-power-of-bayesian-a-b-testing-f859d2219d5).

-----

There’s a common misconception that A/B testing simply involves figuring out your minimum sample size, running a test, and calling a winner. But experimentation and causal inference are hard. There are so many places where bias may creep in, where your statistical assumptions break down, where the amount of uncertainty is not definitive enough to make a decision. As the data experts, it’s up to us to understand and manage that complexity while delivering actionable insights to our stakeholders. Hopefully the readings above can help with that critical work.
