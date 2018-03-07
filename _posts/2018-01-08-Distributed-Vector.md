---
layout: post
categories: Chapel Data-Structures Projects
title: "Designing a distributed parallel-safe vector for Chapel"
---

**TODO:**

Overall idea:
  1. Make use of wait-free atomic fetch-and-add counters; useful
     for performing obstruction-free helper-bounds-checking, and for maintaining
     consensus over the global head and tail.
  2. Have one concurrent linked list per core per locale and store the head/tail
     count in each node and sort by said count. Tasks only takes node if their
     fetch-add count matches

**Benefits:**

  1. By using the helper bounds-checking algorithm, we ensure that communication is
  only interrupted when a task attempts to add an item when the data structure
  is full, or attempts to take an item when the data structure is empty. This
  scales extremely well so long as the user is conscious about their usage.

  2. By keeping a Fetch-and-Add counter for the head and tail, we ensure that claiming
  a position is entirely wait-free in both computation and communication. This
  scales phenomanally, especially if the head and tail counters are allocated on
  separate nodes to prevent any one node from getting 'bogged down'.

  3. By keeping a concurrent linked list per core, we can ensure that if there is a
  remote 'executeOn' statement, we can ensure that we have at most maxTaskPar tasks
  performing an operation at any given time while gaining concurrency. By doing this
  for each node it is distributed over, we gain more parallelism/concurrency as
  we increase the nodes we distribute over.

  4. By keeping the concurrent linked list sorted we allow readers to scan the list
  for their operation. By keeping the read head/tail count in each node, we ensure
  that if a task successfully performs a fetch-and-add on the head/tail without
  yet adding their element to the list does not cause another task to remove
  another node out-of-order. This ensures we maintain an overall order on the
  data structure.

  5. Can make use of Cray Aries NIC hardware 'Network Atomics'.


**Drawbacks:**

  1. Relies on Quiescent State-Based Reclamation and a concurrent sorted linked list.
  2. Relies on network atomics for true scalability.
