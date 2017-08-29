---
layout: page
title: Projects
permalink: /projects/
---

## Concurrent and Scalable Built-in Hash-Table for the Go Programming Language

[Source](https://github.com/LouisJenkinsCS/Go_With_Concurrent_Map_Builtin)

[Presentation]({{ site.baseurl }}/presentations/go_concurrent_map.pdf)

Originally titled "A Concurrent and Scalable Built-in Hash-Table for the Go Programming Language", this is the fruits of my labor for
all of my effort during the "Smart Spaces" R.E.U (for the awards, check the awards section [here]({{ site.baseurl }}/awards)).
It also shows a specialized version of the "Interlocked Hash Table" for the Go runtime. The concurrent map implementation can be seen
[here](https://github.com/LouisJenkinsCS/Go_With_Concurrent_Map_Builtin/blob/master/src/runtime/concurrent_map.go).


## MoltarOS

[Source](https://github.com/LouisJenkinsCS/MoltarOS)

![Screenshot](https://raw.githubusercontent.com/LouisJenkinsCS/MoltarOS/master/multitasking.JPG)

Defined as the pinnacle of programming, operating systems development for a hobby is as far as you can go
in terms of challenges. Unfortunately due to time constraints, updates and progress are made in bursts.
The OS will be built entirely from scratch for the x86 architecture, and is planned to have a minimal but
hopefully complete environment: Interrupts, Multitasking, Memory Management (Paging), ELF Binary Loading,
System Calls, etc. This could take years, but it wouldn't be worth it if it was easy.


## S.A.K-Overlay (Android Windows Manager)

[Source](https://github.com/LouisJenkinsCS/S.A.K-Overlay)

[Presentation]({{ site.baseurl }}/presentations/sak_overlay.pdf)

[Summary Report]({{ site.baseurl }}/presentations/SAK_Overlay_Report.pdf)

![Screenshot](https://raw.githubusercontent.com/LouisJenkinsCS/S.A.K-Overlay/master/S.A.K-Overlay_Screenshot.png)

My one and only Android Application I've ever wrote. When I wrote it, I had the idea that it would be my playground:
Anything I wanted to do, anything I wanted to learn, could be done in a single application, which gave it it's name,
the "Swiss-Army Knife Overlay". The final product was meant to be used while gaming, in providing a kind of Steam-like
overlay which is non-existent. As well, it later was planned to have the ability to create your own 'widgets' which are
mini-windows, as can be seen in the screenshot through a drag-and-drop WYSIWYG editor. Unfortunately, time constraints
lead to it being cut, and the fact that I was running out of things to learn from it. It was always meant to be open source
and free, but unfortunately it has died due to never being complete.

## Code-Glosser (Student Code Evaluation Tool)

[Source](https://github.com/LouisJenkinsCS/Code-Glosser)

[Video Demo](https://www.youtube.com/watch?v=FailmQ7r73s)

[Presentation]({{ site.baseurl }}/presentations/Code-Glosser.pdf)

[Department Seminar Flier]({{ site.baseurl }}/presentations/Code-Glosser_Flyer.pdf)

![Screenshot](https://raw.githubusercontent.com/LouisJenkinsCS/Code-Glosser/master/screenshots/CG_MoltarOS_C_Final.png)

For an "independent study", which meant me creating software for credits to make it easier for the professor to grade homework assignments,
I developed "Code-Glosser", an academic enrichment tool with the sole purpose to make giving feedback effortless. Code-Glosser pretty much allows
you to markup a student's code similar to a highlighter or pen, except without the inconvenience of having to do it on paper. It also allows the reuse
of templates, which are markups already prepared ahead of time. It supported marking up entire projects (multiple files and directories), as well as
169 langauges through the highlight.js library. Releases for can be found [here](https://github.com/LouisJenkinsCS/Code-Glosser/releases) for the curious
and any issues can be submitted to the issue tracker, [here](https://github.com/LouisJenkinsCS/Code-Glosser/issues). This was shown at an department seminar
at Bloomsburg University.

## Minimal-J.V.M

[Source](https://github.com/LouisJenkinsCS/Minimal-JVM)

[Presentation]({{ site.baseurl }}/presentations/OPL_Final_Project_Presentation.pdf)

For a course called the "Organization of Programming Languages", I decided to create a Java Virtual Machine in Haskell.
This was purely for a challenge, as everyone else in my class decided to do things they were more familiar with, I chose two
things entirely new: Functional Programming (Haskell) and Runtime Systems (ByteCode Interpreter). The end-result was a very minimal
Java Virtual Machine that ran a very small subset of bytecode instructions, running actually valid '.class' files generated from Java and
even Scala (with some issues) that used bytecode implemented. Was a very fun project.

## Utilities Package for the C Programming Language

[Source](https://github.com/LouisJenkinsCS/C_Utils)

My very first project, which still holds a place in my heart to this day, the amount of times I've tried 'revising' it is reflected in the absurd number of
commits. The project itself is defunct and I wouldn't use it for any project like it was intended to be, but it was my first GitHub repository. It was my
literal playground to teach myself C and as much theory as I wanted. There, I've created a thread pool, lock-free data structures (Stack and Queue using
Hazard Pointers, defined [here](http://web.cecs.pdx.edu/~walpole/class/cs510/papers/11.pdf)), abstractions for memory management and reference counting,
and much more. I've learned so much from it, and put so much work into it that it deserves to be listed here.
