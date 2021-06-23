---
title: Moore's Law and Amdahl's law
header:
    image: /assets/posts/20130702/20130702_key_visual.jpg
---
Until the mid oft he 2000’s, there was some kind of an unbreakable fact regarding the vertical scalability of computer hardware and therefore the underlying scaling rules for computer software: Moore’s law. Moore’s law states that the number of transistors on integrated circuits doubles approximately every two years. In good old times of single core processors this meant that also the computing power doubled by this effect. This was a safe harbour for gaining performance in software development. The time was with you, you just had to wait and your execution was getting faster without any changes in the software architecture.

Moore’s law is still a valid rule of thumb, but times for the software developers and architects have changed. Although the number of transistors is still growing rapidly, this results in more processor cores since the mid of the 2000’s which means a shift of the vertical scaling approach to horizontal scaling. This also means to gain a positive impact from microprocessor evolution; software has to set on parallel computing. A single sequenced set of instruction is no longer automatically getting faster; problem solving has to happen on several cores in different threads.

Now Amdahl’s law comes into account. The computer architect Gene Amdahl has presented this rule in the mid 1960’s. It predicts the maximum theoretical speedup using multiple processor or cores. Simply speaking it states that the speedup depends on two factors: The overhead needed to control the execution of different threads to solve a problem and mainly the limit of speedup which is determined by the longest sequential process that cannot be parallelized. A short example:

- A program takes 5 minutes to execute sequentially in a single thread
- The longest sequential process in that program takes 2 minutes to execute
- As a result - no matter how many processors or cores you use - the overall program will not be faster than two minutes after parallelization

As a result the software architecture of modern systems need to be developed with parallel execution in mind. This can be accomplished by several mechanisms:
- Try to split the problem into smaller pieces, calculate them independently and combine the results (divide & conquer and map & reduce)
- Try to avoid accessing mutable objects in memory. This results in a huge effort for thread synchronization and - worst case - in non-determinism. Everyone who ever tried to develop complex multi threaded synchronized Java applications knows what I’m talking about
- Use instead immutability which in fact means change your development style to a more functional programming style instead of an imperative one
- Start to develop asynchronously. This limits the single, no more separable sequences within your software to a minimum

I’ve detected for myself that functional programming with Scala on the JVM with an asynchronous style using e.g. actors is a fantastic way of developing clear and concise highly scaling software components. It has the charm that it fits 100% into the large existing JVM/ Java ecosystem and that there are already great frameworks like the Playframework or Akka, but this is only one option from many you can choose of. Maybe languages like Clojure or Erlang fit better to your need or you may even adopt a more functional style in pure Java.