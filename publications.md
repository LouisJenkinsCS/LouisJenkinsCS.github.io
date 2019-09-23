---
layout: page
title: Publications

permalink: /publications/
---

## Published

### [Redesigning Go’s Built-In Map to Support Concurrent Operations]({{ site.baseurl }}/publications/PACT2017.pdf)

#### Authors: Louis Jenkins, Tingzhe Zhou, and Michael F. Spear

#### [Presentation @ NSF REU]({{ site.baseurl }}/presentations/go_concurrent_map.pdf)

#### Presentation @ PACT 2017 (Unavailable)

#### Venue: PACT 2017

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

#### Authors: Louis Jenkins

#### [Presentation]({{ site.baseurl }}/presentations/RCUArray.pdf)

#### Venue: [The 5th Annual Chapel Implementers and Users Workshop 2018](https://chapel-lang.org/CHIUW2018-cfp.html)

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

### [Chapel HyperGraph Library (CHGL)]({{ site.baseurl }}/publications/CHGL.pdf)

#### Authors: Louis Jenkins, Marcin Zalewski, Sinan Aksoy, Hugh Medal, Cliff Joslyn,...

#### [Poster @PNNL]({{ site.baseurl }}/posters/CHGL.pdf)

#### Venue: 2018 IEEE High Performance Extreme Computing Conference(HPEC ‘18)

#### Abstract

We present the Chapel Hpergraph Library (CHGL), a library for hypergraph computation in the emerging Chapel language. 
Hypergraphs generalize graphs, where a hypergraph edge can connect any number of vertices. Thus, hypergraphs capture 
high-order, high-dimensional interactions between multiple entities that are not directly expressible in graphs. 
CHGL is designed to provide HPC-class computation with high-level abstractions and modern language support for parallel 
computing on shared memory and distributed memory systems. In this paper we describe the design of CHGL, including ﬁrst 
principles, data structures, and algorithms, and we present preliminary performance results based on a graph generation 
use case. We also discuss ongoing work of codesign with Chapel, which is currently centered on improving performance.

### [Chapel Aggregation Library (CAL)]({{ site.baseurl }}/publications/CAL.pdf)

#### Authors: Louis Jenkins, Marcin Zalewski, Michael Ferguson

#### [Presentation @SC18]({{ site.baseurl }}/presentations/CAL-SC18.pdf)

#### Venue: [Parallel Applications Workshop, Alternatives To MPI](https://sourceryinstitute.github.io/PAW/PAW-ATM18/indexPAW-ATM18.html)

#### Abstract

Fine-grained communication is a fundamental principle of the Partitioned Global
Address Space (PGAS), which serves to simplify creating and reasoning about
programs in the distributed context. However, per-message overheads of
communication rapidly accumulate in programs that generate a high volume of
small messages, limiting the effective bandwidth and potentially increasing
latency if the messages are generated at a much higher rate than the effective
network bandwidth. One way to reduce such ﬁne-grained communication is by
coarsening the granularity by aggregating data, or by buffering the smaller
communications together in a way that they can be handled in bulk. Once these
communications are buffered, the multiple units of the aggregated data can be
combined into fewer units in an optimization called coalescing.  

The Chapel Aggregation Library (CAL) provides a straightforward approach to
handling both aggregation and coalescing of data in Chapel and aims to be as
generic and minimal as possible to maximize code reuse and minimize its increase
in complexity on user applications. CAL provides a high-performance,
distributed, and parallel-safe solution that is entirely written as a Chapel
module. In addition to being easy to use, CAL improves the performance of some
benchmarks by one to two orders of magnitude over naive implementations at 32
compute-nodes on a Cray XC50.

### [High Performance Hypergraph Analytics of Domain Name System Relationships]({{ site.baseurl }}/publications/HICSS.pdf)

#### Authors: Cliff Joslyn, ...,  Louis Jenkins, et al.

#### [Presentation @HICSS]({{ site.baseurl }}/presentations/HICSS.pdf)

#### Venue: [HICSS Symposium on Cybersecurity Big Data Analytics](http://www.azsecure-hicss.org)

#### Abstract

We report on the use of novel mathematical methods in hypergraph analytics over a
large quantity of DNS data. Hypergraphs generalize graphs, as used in network science,
to better model complex multiway relations in cyber data. Specifically, casting DNS data
from Georgia Tech’s ActiveDNS repository as hypergraphs allows us to fully represent the
interactions between collections of domains and IP addresses. To facilitate large-scale
analytics, we fielded an analytical pipeline of two capabilities. HyperNetX (HNX) is a
Python package for the exploration and visualization of hypergraphs, acting as a frontend.
For the backend, the Chapel HyperGraph Library (CHGL) is a library for high performance
hypergraph analytics written in the exascale programming language Chapel. CHGL was used
to process gigascale DNS data, performing compute-intensive calculations for data reduction
and segmentation. Identified portions are then sent to HNX for both exploratory analysis
and knowledge discovery targeting known tactics, techniques, and procedures.

### [Chapel Graph Library (CGL)]({{ site.baseurl }}/publications/CGL.pdf)

#### Authors: Louis Jenkins, Marcin Zalewski

#### [Presentation]({{ site.baseurl }}/presentations/CGL.pdf)

#### Venue: [The ACM SIGPLAN 6th Annual Chapel Implementers and Users Workshop](https://chapel-lang.org/CHIUW2019.html)

#### Abstract

In this talk, I summarize prior work on the Chapel HyperGraph Library (CHGL), the Chapel Aggregation Library (CAL), and introduce the more general Chapel Graph Library (CGL). CGL is being designed to enable global-view programming, such that locality is abstracted from the user. CGL is also being designed in a way that is similar to Chapel's multiresolution design philosophy, where graphs are implemented in terms of hyper graphs, and where both the underlying hypergraph and overlying graphs are available for use. Some of the kinds of graphs being designed are bipartite graphs, directed and undirected graphs, and even trees.

## To Appear

### [Graph Algorithms in PGAS: Chapel and UPC++]({{ site.basurl }}/publications/HPEC.pdf)

#### Authors: Louis Jenkins, et al.

#### Venue: [2019 IEEE High Performance Extreme Computing Conference (HPEC ‘19)](http://ieee-hpec.org)

#### Abstract

The Partitioned Global Address Space (PGAS) programming
model can be implemented either with programming
language features or with runtime library APIs, each implementation
favoring different aspects (e.g., productivity, abstraction, flexibility,
or performance). Certain language and runtime features,
such as collectives, explicit and asynchronous communication
primitives, and constructs facilitating overlap of communication
and computation (such as futures and conjoined futures) can
enable better performance and scaling for irregular applications,
in particular for distributed graph analytics. We compare graph
algorithms in one of each of these environments: the Chapel
PGAS programming language and the the UPC++ PGAS runtime
library. We implement algorithms for breadth-first search and
triangle counting graph kernels in both environments. We discuss
the code in each of the environments, and compile performance
data on a Cray Aries and an Infiniband platform. Our results
show that the library-based approach of UPC++ currently provides
strong performance while Chapel provides a high-level
abstraction that, harder to optimize, still provides comparable
performance.