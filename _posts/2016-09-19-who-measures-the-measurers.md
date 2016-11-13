---
title: Who Measures the Measurers?
excerpt: "How you think about metrics matters."
header:
  overlay_color: "#123"
---

Let’s say you’re a data-driven internet business. How do you know something is good? You measure it with metrics, of course. This has become [gospel](https://codeascraft.com/2011/02/15/measure-anything-measure-everything/) for a lot of organizations.

Fair enough, it’s hard to argue against metrics, though there’s a tendency to trust in them as objective truth, which can fuck things up if you’re not careful.

But how do you know if the metrics themselves are any good? Do you measure them with more metrics? *Is it metrics all the way down?*

Indeed, that’s the lesson from Alex Deng and Xiaolin Shi in their KDD 2016 paper [Data-Driven Metric Development for Online Controlled Experiments: Seven Lessons Learned](http://www.kdd.org/kdd2016/subtopic/view/data-driven-metric-development-for-online-controlled-experiments-seven-less).

Deng and Shi propose a framework for evaluating metrics, particularly those used in online experiments. I’m not going to provide a full summary — e.g. there are parts about validation sets and degradation experiments you should read if you’re interested. Rather, I’m going to explore how Deng and Shi answer an essential question: *What makes a metric good?*

## Yo dawg, I heard you like metrics
Which metrics should you use to measure your metrics? According to Deng and Shi, the answer is *directionality* and *sensitivity*.

Directionality measures the interpretability of the direction a metric moves. If a metric goes up, is that always a good thing, a bad thing, or does it depend?

Sensitivity measures how reactive a metric is to underlying changes. If the user experience changes, how quickly or accurately can you detect that?

## Why do you care?
Metrics may exhibit differing amounts of directionality and sensitivity depending on the purposes they serve:

1. Goal metrics — what Deng and Shi call “Overall Evaluation Criteria” (or OEC) — measure the fundamental health or success of a business. These are the most likely to be referred to by a cryptic acronym.
2. Guardrail metrics are sanity checks for cases where goal metrics might be misleading or inapplicable. For example, you might optimize one user experience metric to the point that you end up hurting revenue, so it’s good to have a guardrail to protect against that.
3. Debugging metrics help make sense of goal metrics by decomposing them into understandable pieces or putting them into context. For example, if you have a metric that’s a rate (e.g. pageviews per user), debugging metrics would be the numerator and denominator of that rate so you can interpret its movements.

Take the time to understand and communicate the purpose of a metric — why you’re using a metric makes a difference for how much you should care about its directionality and sensitivity. For example, you may not care if a revenue guardrail metric is particularly sensitive as long as its movement is clearly unambiguous. For a lot of folks, decreasing revenue is always bad. Is it for you?

## Metrics for metrics for metrics
Sensitivity itself is composed of two measurable quantities:

- Statistical power
- Probability of movement

A metric may track user behaviors that are hard to change. In this case, the metric will be insensitive because its underlying probability of movement will be low.

On the other hand, a metric may track something that’s highly skewed or exhibits big fluctuations. This metric will be insensitive because of low statistical power.

How can you determine the sensitivity composition of your particular metric? See the paper for Deng and Shi's approach using observations from historical experiment data.

## Best rates in town!
Rates are commonly used as metrics because they’re bounded between 0 and 1 and can be relatively insensitive to outliers.

The problem with rates lies in their composition. Because rate metrics are composed of two numbers — the numerator and the denominator — change can be ambiguous, leading to poor directionality. Did your rate metric increase because the numerator went up? Or because the denominator went down? Or because the numerator went up while the denominator remained stable? Or some other plausible reason?

Given that rates can be difficult to interpret, Deng and Shi present some helpful considerations:

- Keep the numerator and denominator as debugging metrics.
- Choose a rate metric where the denominator is fairly stable.
- Think about whether to compute your rate as a ratio of averages or an average of ratios.

Here’s a little more on that last point. Let’s say you’re measuring the conversion rate of users on a particular page.

With an average of ratios, you first compute the conversion rate per user and then average that rate across all users. With a ratio of averages, you sum up all the conversions and divide by the number of pageviews — this is equivalent to an average of ratios weighted by pageviews per user.

An average of ratios weights users equally, while a ratio of averages weights pageviews equally. They generally move in the same direction. When they don't, it's a sign that heavy users are behaving differently than average users.

Deng and Shi note that if you’re using a ratio of averages to measure an experiment and users are the randomization units, you should use the [delta method](https://en.wikipedia.org/wiki/Delta_method) to estimate variance.

## Measure twice...
Often the hardest things when working with data are the most deceptively simple. If you care about measurement, you should think deeply about your metrics. So ask yourself:

*What purpose does my metric serve? How can I quantify its directionality and sensitivity? To what extent is the sensitivity a result of statistical power or probability of movement? And how the fuck can I even wrap my mind around the complexity of rates?*

Then close your eyes, say “data-driven” ten times fast, and start on the documentation. You *are* documenting all this, right?
