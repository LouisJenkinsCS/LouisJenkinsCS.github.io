---
layout: page
title: Publications
permalink: /publications/
---

### [Redesigning Go’s Built-In Map to Support Concurrent Operations]({{ site.baseurl }}/publications/PACT2017.pdf)

#### Status: Published

#### Venue: PACT 2017

#### Authors: Louis Jenkins, Tingzhe Zhou, and Michael F. Spear

#### Abstract

The Go language lacks built-in data structures that allow ﬁne-grained concurrent
access. In particular, its map data type, one of only two generic collections in
Go, limits concurrency to the case where all operations are read-only; any
mutation (insert, update, or remove) requires exclusive access to the entire map.
The tight integration of this map into the Go language and runtime precludes its
replacement with known scalable map implementations.

This paper introduces the Interlocked Hash Table (IHT). The IHT is the result of
language-driven data structure design: it requires minimal changes to the Go map
API, supports the full range of operations available on the sequential Go map,
and provides a path for the language to evolve to become more amenable to scalable
computation over shared data structures. The IHT employs a novel optimistic locking
protocol to avoid the risk of deadlock, and allows large critical sections that
access a single IHT element, and can easily support multikey atomic operations.
These features come at the cost of relaxed, though still straightforward, iteration
semantics. In experimentation in both Java and Go, the IHT performs well, reaching
up to 7× the performance of the state of the art in Go at 24 threads. In Java, the
IHT performs on par with the best Java maps in the research literature, while providing
iteration and other features absent from other maps.
