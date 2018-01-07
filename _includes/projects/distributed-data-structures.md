---
title: Distributed Data structures
url: https://summerofcode.withgoogle.com/projects/#5363251622707200
---

For [Google Summer of Code](https://summerofcode.withgoogle.com/projects/#5363251622707200)
internship, I created a distributed data structures framework for Chapel, called the 'Collections'
module, which provide the first pseudo-interface. I have also created two
novel data structures, that at 64-nodes (3072 processors) on a Cray-XC40 outperform
a naive implementation by at least two orders of magnitudes. One was an ordered
Deque, outperforming by ~100x, and an unordered Bag (Multiset) that outperformed
by ~500x. Both are the first of their kind, and are a result of experimentation
and taking the best ideas from various publication, even [my own]({{ site.baseurl }}/publications/PACT2017.pdf).
