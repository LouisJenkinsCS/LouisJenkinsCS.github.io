---
layout: post
categories: Chapel Data-Structures Projects
title: "Designing a distributed, resizable, and indexable container for Chapel"
---

A large part of my Google Summer of Code experience has been solving problems
in areas others either aren't interested in solving or weren't able to solve,
and a big one is the problem of distributed arrays and resizing. Currently,
Chapel's arrays, distributed or not, are extremely complicated (and that is
no exaggeration) and focused on providing the most performance for common
use-cases, which is entirely fair and the smartest thing to do; unfortunately
my use-cases are anything but 'common', and in fact are for very niche and
low-level purposes.

Chapel arrays and distributions rely heavily on the concept of domains, which
describe the set of inputs such as the range of which is an array is allocated,
so if we're talking about a dense array containing 1024 elements, then it will
have a domain from 1..1024 (or 0..1023). So, for a visual example...

```chpl
// Our domain
var dom : {1..1024};
// Our array distributed on this domain
var arr : [dom] int;
```

Now imagine that we need to resize this array to hold twice the number of elements.
In Chapel, arrays are set-in-stone; in fact I believe they are even embedded into
whatever structure they are declared in. The importance of this is the fact that
resizing `arr` requires us to resize `dom`, the domain itself. This may not sound
bad, but imagine if you have multiple arrays sharing the same domain...

```chpl
// Our domain
var dom : {1..1024};
// Our arrays distributed on this domain
var arr1 : [dom] int;
var arr2 : [dom] int;
```

This is a legal and very valid thing to do. The obvious thing that should come to
mind is that if we wanted to resize `arr1`, we would have to resize `dom` which
will consequently resize `arr2`. Now this is easily remedied by giving each array
its own distinct domain, but there is another issue. If a domain is resized, the
arrays using said domains become unsafe, so this becomes an issue for resizable
domains as well as arrays. The implementation of domains are as complicated
(if not more so) than the arrays themselves. Note that since this problem includes
domains, we must handle domains distributed across an entire cluster as well as
sparse domains. Without needing to say much, any coarse-grained synchronization
over the domain and array itself isn't much of a solution, and fine-grained synchronization
can come with its own set of problems such as deadlock, livelock, priority inversion,
only to name a few. To approach a problem that has never been solved, a novel
solution must be devised.

### Distributed Read-Copy-Update (RCU)

While different granularities of synchronization each come with their own set
of problems, it is needed to some extent. I have devised a something similar to
RCU, a synchronization technique that allow for concurrent readers *during* a write.
It should be noted that RCU differs from a reader-writer lock in that a reader-writer
lock requires full mutual exclusion for writers, while RCU does not; this comes
at the expense of writes becoming extremely expensive, likely having to clone parts
or the entirety of the data it is protecting, updating the clone, atomically setting
the cloned instance, and then adding on the cost of waiting for concurrent readers
using the original to finish before disposing of it. To give a more pseudo-code
look at what RCU looks like...

```chpl
// Read
var instance = getCurrentInstance();
// Copy
var newInstance = clone(instance);
// Update
modify(newInstance);
updateCurrentInstance(newInstance);
```

The above assumes that `getCurrentInstance` and `updateCurrentInstance` are
atomic. This algorithm, while trivial, comes with its own set of problems, most
importantly: "What happens to the old instance?". In a garbage collected language
this is simple as "the garbage collector collects it", but as this is Chapel, we
must perform the painstaking task of memory management ourselves. As well, unlike
other RCU implementations, we are targeting distributed architectures here, with
possible heterogeneity, and as such we need to have our memory management be as
abstract as possible, far from hardware and kernel-level barriers; we must create
a distributed barrier that both readers and writers respect.

**TODO**
