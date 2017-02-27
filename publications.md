---
layout: page
title: Publications
permalink: /publications/
---

## Concurrent Map for Go

### Status: In Preparation

### Authors: Louis Jenkins, Michael F. Spear

### Abstract

The Go programming language offers many features that simplify the creation of highly concurrent systems.  However, it lacks built-in data structures that allow fine-grained concurrent access.  In particular, its map data type, one of only two generic collection types in the language, limits concurrency to the case where all operations are read-only; any mutation (inserts, updates, and removals) requires exclusive access to the entire map.

In this paper, we extend the Go compiler and run-time to support a new concurrent map data type, the Interlocked Hash Table (IHT).  By leveraging a novel optimistic synchronization protocol, the IHT permits concurrency among reads, writes, and iteration operations, without risking deadlock.  We also allow large critical sections that access a single IHT element.  The net effect is a highly scalable, high-performance data structure that offers straightforward and useful semantics, and outperforms all known concurrent maps for Go, achieving performance up to 7x better than the state of the art at 24 threads.

### Manuscript

Available [here]({{ site.baseurl }}/publications/A_Concurrent_Map_for_Go.pdf).
