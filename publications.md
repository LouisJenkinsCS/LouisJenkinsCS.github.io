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

### [RCUArray: An RCU-like Parallel-Safe Distributed Resizable Array]({{ site.baseurl }}/publications/RCUArray.pdf)

#### Venue: CHIUW 2018 (IPDPSW)

#### Authors: Louis Jenkins

#### [Presentation]({{ site.baseurl }}/presentations/CHGL.pdf)

#### Abstract

Presented in this work is RCUArray, a parallel-safe distributed array that
allows for read and update operations to occur concurrently with a resize via
Read-Copy-Update. Also presented is a novel extension to Epoch-Based Reclamation
(EBR) that functions without the requirement for either Task-Local or
Thread-Local storage, as the Chapel language currently lacks a notion of either.
Also presented is an extension to Quiescent State-Based Reclamation (QSBR) that
is implemented in Chapel's runtime and allows for parallel-safe memory
reclamation of arbitrary data. At 32-nodes with 44-cores per node, the RCUArray
with EBR provides only 20% of the performance of an unsynchronized Chapel block
distributed array for read and update operations but near-equivalent with QSBR;
in both cases RCUArray is up to 40x faster for resize operations.

## Manuscript

### [Chapel HyperGraph Library (CHGL)]({{ site.baseurl }}/publications/CHGL.pdf) ~To Appear~

#### Venue: HPEC-2018

#### Authors: Louis Jenkins, Marcin Zalewski, Sinan Aksoy, Hugh Medal, Cliff Joslyn,...

#### Abstract

We present the Chapel Hpergraph Library (CHGL), a library for hypergraph computation in the emerging Chapel language. 
Hypergraphs generalize graphs, where a hypergraph edge can connect any number of vertices. Thus, hypergraphs capture 
high-order, high-dimensional interactions between multiple entities that are not directly expressible in graphs. 
CHGL is designed to provide HPC-class computation with high-level abstractions and modern language support for parallel 
computing on shared memory and distributed memory systems. In this paper we describe the design of CHGL, including ﬁrst 
principles, data structures, and algorithms, and we present preliminary performance results based on a graph generation 
use case. We also discuss ongoing work of codesign with Chapel, which is currently centered on improving performance.


