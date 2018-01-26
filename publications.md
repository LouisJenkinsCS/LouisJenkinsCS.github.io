---
layout: page
title: Publications
permalink: /publications/
---

## Published

### [Redesigning Go’s Built-In Map to Support Concurrent Operations]({{ site.baseurl }}/publications/PACT2017.pdf)

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

## Manuscript

### [RCUArray: An RCU-like Parallel-Safe Distributed Resizable Array]({{ site.baseurl }}/publications/RCUArray.pdf)

#### Status: Submitted

#### Venue: CHIUW 2018 (IPDPS)

#### Authors: Louis Jenkins

#### Abstract

I present RCUArray, a parallel-safe distributed
array that allows for read and update operations to occur
concurrently with a resize. As Chapel lacks thread-local and
task-local storage, I also present a novel extension to the ReadCopy-Update
synchronization strategy that functions without
the need for either. At 32-nodes with 44-cores per node the
RCUArray’s relative performance to an unsynchronized Chapel
block distributed array is as little as 20% for read and update
operations, but with runtime support for zero-overhead RCU
and thread-local or task-local storage it has the potential to be
near-equivalent; relative performance for resize operations is as
much as 3600% due to the novel design.
