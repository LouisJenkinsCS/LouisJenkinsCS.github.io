---
layout: page
title: Publications
permalink: /publications/
---

## Concurrent Map for Go

### Status: Accepted, needs revision

### Venue: PACT 2017

### Authors: Louis Jenkins, Tingzhe Zhou, and Michael F. Spear

### Abstract

The Go programming language offers many features that simplify the creation of highly concurrent systems. However, it lacks built-in data structures that allow fine-grained concurrent access. In particular, its map data type, one of only two generic collections in Go, limits concurrency to the case where all operations are read-only; any mutation (insert, update, or remove) requires exclusive access to the entire map. The tight integration of this map into the Go language and runtime precludes its replacement with known scalable map implementations.

This paper introduces the Interlocked Hash Table (IHT). The IHT is the result of language-driven data structure design: it was designed to require minimal modifications to the existing Go map API, to support the full range of operations available on the sequential Go map, and also to provide a path for the language to evolve to become more amenable to scalable computation over shared data structures. The IHT employs a novel optimistic locking protocol, so that concurrent reads, writes, and iterations can make progress without risking deadlock. The IHT also allows large critical sections that access a single IHT element, and can easily support multikey atomic operations. These features come at the cost of relaxed, though still straightforward, iteration semantics. In experimentation in both Java and Go, the IHT performs well, reaching up to 7x the performance of the state of the art in Go at 24 threads. In Java, the IHT performs on par with the best Java maps in the research literature, while providing iteration and other features absent from other maps.

### Publication

Available [here]({{ site.baseurl }}/publications/A_Concurrent_Map_for_Go.pdf).
