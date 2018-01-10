---
layout: post
categories: Chapel Data-Structures Projects
title: "Designing a distributed and resizable hash table for Chapel"
---

TODO: Basic summary is to extend the Interlocked Hash Table (in my original
publication for Go's map) in a way that distributes each root PointerList across
each node, where each recursive PointerList will just be local to the same node
the root is allocated on. This would be a legendary data structure, indeed!
