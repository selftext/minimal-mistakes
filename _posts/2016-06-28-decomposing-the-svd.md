---
title: Decomposing the SVD
excerpt: "Thoughts on the singular value decomposition."
header:
  overlay_color: "#333"
---

I’ve been an avid reader of Jeremy Kun’s blog [Math ∩ Programming](https://jeremykun.com/) for some time. I especially like how he explains challenging concepts with an ensemble of different perspectives, first building intuition, then diving into mathematical theorems and proofs, then showing an example in code, and usually including some practical applications along the way.

His latest [two](https://jeremykun.com/2016/04/18/singular-value-decomposition-part-1-perspectives-on-linear-algebra/) [posts](https://jeremykun.com/2016/05/16/singular-value-decomposition-part-2-theorem-proof-algorithm/) have been on the singular value decomposition (SVD). I’ve studied SVD in the past and feel like I could explain it at a high level, but it’s been some time since I’ve delved deep into the math, so I took my time reading through the derivations.

I admit I got stuck in a few places. Since my linear algebra is a bit rusty these days, I’ve decided to use this blog post to work through my confusion to explain (to others, to my future self perhaps) what exactly is going on here.

### Projecting \\( x \\) onto \\( v \\).

My first question is this: Near the beginning of the post, why does Jeremy write that \\( {proj}_v(x) = (x \cdot v)v \\) but then later seem to use \\( (x \cdot v) \\) as the definition of \\( {proj}_v(x) \\) ?

A dot product returns a scalar, a single number. In this case, \\( (x \cdot v) \\) defines the length of \\( v \\) when we project \\( x \\) onto it. The operation \\( (x \cdot v)v \\) returns a vector --- the projection --- while \\( (x \cdot v) \\) is the length of that vector.

In other words, this is the difference between the _length_ of the projection of \\( x \\) onto \\( v \\) and the projection itself. This seems obvious in retrospect, but it’s easy to get caught up in the notation and not see these important differences.

### Maximizing instead of minimizing to find the line (or, in multiple dimensions, hyperplane) of best fit.

Later on, Jeremy switches from minimizing the sum of squared distances to maximizing the sum of squared lengths of the projections. This can only work if \\( \|{proj_v(x)}\|^2 \\) --- the squared length of the projection of \\( x \\) onto \\( v \\) --- is always less than or equal to \\( \|x\|^2 \\) --- the squared length of \\( x \\). Why is that always the case?

The intuitive answer is that in projecting \\( x \\) onto \\( v \\), we’ve created a right triangle, and the hypotenuse \\( x \\) of that triangle will always be the longest side. In the case where \\( \|x\|^2 \\) = \\( \|{proj_v(x)}\|^2 \\), the two vectors lie on the same line.

I wasn’t fully satisfied with this answer, especially since I can only visualize it in a few dimensions. Another way to think about this is with the cosine of the angle between \\( x \\) and \\( v \\). Let’s call this angle \\( \theta \\). When \\( v \\) is a unit vector, we can define the dot product between \\( x \\) and \\( v \\) as \\( x \cdot v = \|x\| \cos \theta \\). In other words, this is the length of \\( x \\) scaled by the cosine of the angle between \\( x \\) and \\( v \\). The cosine will always be between -1 and 1, so \\( \|x \cdot v\|^2 \\) will always be less than or equal to \\( \|x\|^2 \\).

As above, some of my confusion here stems from identifying when the notation is representing lengths of vectors rather than the vectors themselves. The notation can get a little slippery, so it’s been helpful to think carefully about what it means and try to articulate why it works the way it does.
