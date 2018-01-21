---
layout: post
categories: Chapel Abstractions Synchronization
title: "Designing a distributed reader-writer lock for Chapel"
---

**TODO:**

Overall idea:
  1. Have one global write lock
  2. Have task-local/thread-local reader-writer locks to reduce contention
  3. Writers must acquire global write lock and each task-local/thread-local reader-writer lock for each node.
  4. Readers only acquire task-local/thread-local reader-writer lock

Benefits:
  Readers are uncontended when they acquire the reader-writer lock for majority
  of time, and even when they are they do not require any communication, either
  between nodes or other threads.
Drawbacks:
  Writers are super-slow, similar to RCU except that they require actual mutual
  exclusion from concurrent readers, but are simpler in that memory reclamation
  is made easy. Should have comparable performacne when writes are seldom.
