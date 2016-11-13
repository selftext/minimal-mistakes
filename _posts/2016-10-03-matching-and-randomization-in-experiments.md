---
title: Matching and Randomization in Experiments
excerpt: "Thoughts on a classic paper on causality."
header:
  overlay_color: "#456"
---

I recently read Donald Rubin’s classic paper [Estimating Causal Effects of Treatments in Randomized and Nonrandomized Studies](http://dx.doi.org/10.1037/h0037350) ([PDF](http://www.biostat.jhsph.edu/~dscharf/Causal/rubin.journ.psych.ed.pdf)) as part of the Kickstarter Data team’s reading group.

Two arguments in this paper jumped out at me, the first about the value of matching and the second about the costs and benefits of conducting a randomized versus observational study.

## Matching

Rubin proposes a hypothetical experiment on 2*N* units in which the experimental treatment E is assigned to *N* units while the control treatment C is assigned to a different set of *N* units. If for every unit receiving E there is a matched unit receiving C such that we expect the pair to react identically to the same treatment, then there are *N* identically matched pairs. Rubin observes that

> if one had *N* identically matched pairs, a "thoughtless" random assignment could be worse than a nonrandom assignment of E to one member of the pair and C to the other. By "thoughtless" we mean some random assignment that does not assure that the members of each matched pair get different treatments. (692)

In this case, “thoughtless” randomization “could be worse” in the sense that the statistical power of the experiment will suffer, and you will be less likely to detect an effect if there really is one.

Geography is a good example of this. If you’re running an experiment on users across the United States, matching similar geographic regions might be more effective than a completely randomized trial because the variation *between* regions might be higher than variation within *regions*, diluting the effect.

Of course, a multilevel model that takes into account region is one solution. For an insightful description of how Google has approached this problem, see [Estimating causal effects using geo experiments](http://www.unofficialgoogledatascience.com/2016/06/estimating-causal-effects-using-geo.html).

## Randomized vs. Observational Studies

Another one of Rubin’s claims that stood out to me is a comparison of the costs and benefits of typical randomized and observational studies.

One major advantage of randomized studies is that, with a large enough sample size, you often don’t have to worry about controlling for confounding factors that might bias your results.

There can be downsides to randomized studies though. They can have nontrivial setup costs, and running a randomized study over a long window (e.g. years) is often not feasible. Moreover, because randomized trials are often conducted in a controlled environment, Rubin claims that they tend to be less natural than an observational study — that is, the units of analysis are often constrained to a particular setting or selected to be a subset of the population of interest.

Granted, this is more the case for experiments in fields like psychology than in online experiments on the web, but it does suggest that generalizability is a factor we should consider when interpreting the results of a randomized trial.

Comparing these costs and benefits, Rubin argues that

> the first issue, the effect of variables not explicitly controlled, is usually more serious in nonrandomized than in randomized studies, while the second, the applicability of the results to a population of interest, is often more serious in randomized than in nonrandomized studies. (698)

I take this as a reminder to think carefully about the generalizability of the results of an experiment. When we run experiments on specific parts of a website or on particular subsets of users, often our goal is to generalize these results to the entire website or to all users. Rubin reminds us that observational studies, when analyzed properly, may in fact be better suited to those kinds of claims, particularly when matching can be used.

