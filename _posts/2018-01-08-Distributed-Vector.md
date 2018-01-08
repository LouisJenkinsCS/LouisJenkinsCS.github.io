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
over the domain and array itself isn't much of a solution.

**TODO**  
