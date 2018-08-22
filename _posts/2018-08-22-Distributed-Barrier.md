---
layout: post
categories: Chapel Synchronization Ideas

title: "Distributed Ring Barrier"
---

While glossing over a paper called ["Barrier Synchronization: Simpliﬁed, Generalized, and Solved without Mutual Exclusion"](http://conferences.computer.org/ipdps/2018/pdfs/IPDPSW2018-2cSsu0vr9kD2vmKyKNi2iz/ExW4VvhyEkTUirxC9v1cc/6tUPOA1qBfzBJND5abY2QM.pdf), it gave me an idea for how this can be implemented in Chapel. First, I'll go over the idea proposed in the original paper and then make my own adaptations and improvements on it. 

In this paper the author, Alex Aravind, presents a Ring Barrier implementation where each processing unit, _p_, out of _N_, which I will denote as _p{i}_, for _i in [1..N]_, will notify its neighbor when it is notified by its predecessor. Hence _p{i}_ notifies _p{i+1}_ and gets notified by _p{i-1}_. The key point here is that while _p{i}_ is awaiting notification, it will be spinning locally, and when it needs to notify a neighbor it can do so using only a single remote memory access. After the _p{i}_ has notified its neighbor, it will then wait on a flag that may or may not be remote. Below is a basic sketch of the algorithm in Chapel.

```chpl
// Number of tasks that must hit barrier
const numTasks : int;
var epoch : atomic int;
var tids : atomic int;
var tid = tids.fetchAdd(1) % numTasks;
var signal = epoch.read(memory_order_relaxed);
var status : [0..#numTasks] atomic bool;
// If we have task id #0, we are bootstrap the process
if tid == 0 {
  status[tid + 1].write(signal);
  status[0].waitFor(signal);
} else if tid < status.domain.high { 
  status[tid].waitFor(signal);
  status[tid + 1].write(signal);
  status[0].waitFor(signal);
} else {
  status[tid].waitFor(signal);
  status[0].write(signal);
}
// Update epoch; ensures it is only incremented once per pass
epoch.compareExchange(signal, signal + 1);
```

Unlike in the paper, Chapel does not provide thread-local storage or task-local storage yet, and so each task must acquire their own 'tid' from the atomic counter _tids_. As well, the current epoch must be read which is used as the signal to wait on and to send to neighbors as they wake up. After waiting on the signal, each task will perform a compare-and-swap to swing the epoch forward one, and since it is compared to what was read from the epoch it will only be swung forward once.

*TODO:* Distributed Version
