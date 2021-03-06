---
layout: post
title: what is the Mutex and Semaphore?
subtitle: Mutext and Semaphore for concurrency executing.
category: Linux
tags: [summary]
permalink: /2018/04/02/Mutext_Vs_Semaphore/
---


The Mutext and Semaphore is kernel resources that provides synchronization and concurrency services.

When you think of these kind of concepts about Mutext and Semaphore, you could compare them to how to use toiler with lock and key. 

Let's say there are one toilet and one key, this case is similar to the mutex sychronizing.

So, regarding the toilet as one resource for several processes or threads to work on. If a process(a thread) enter toilet, another process(another thread) cannot use it until the previous process(thread) exits. 

In the case of several toilets and keys(identical resources), Let's say there are three toilets. no matter how many processes(threads) there are, Only three processes(threads) can use the toiltes.

That is because there are three keys, Let's explain this situation on code, There is semaphor count, this count is adjusted denpending on using the resources.

a process(a thread) occupied a part of the resources, the count is decremented, so if the count is zero, any ohters cannot use the resource until the occupying process(thread) releases the resoure. 

So if a process(a thread) releases the resource, at the time the count is incremented. 

I cited the bleow text from [GeeksforGeeks about Mutext vs Semaphore](https://www.geeksforgeeks.org/mutex-vs-semaphore/) and [What is the difference between a mutex and a semaphore? in Quora](https://www.quora.com/What-is-the-difference-between-a-mutex-and-a-semaphore)

# Mutex

Mutext utilizes locking mechanism. i.e. A mutex provides mutual exclusion, either producer or consumer can have the key(mutex) and proceed with their work. As long as the buffer is filled by producer, the consumer needs to wait, and vice versa.

Officially: "Mutexes are typically used to serialise access to a section of reentrant code that cannot be executed concurrently by more than one thread. A mutex object only allows one thread into a controlled section, forcing other threads which attempt to gain access to that section to wait until the first thread has exited from that section."

# Semaphore

Semaphore utilize signaling mechanism. i.e. A semaphore is a generalized mutex. in stead of single buffer, we can split the 4KB buffer into four 1KB Buffers(identical resource). A semaphore can be associated with these four buffers. The consumer and producer can work on different buffers **at the same time**.

Officially: "A semaphore restricts the number of simultaneous users of a shared resource up to a maximum number. Threads can request access to the resource(decrementing the semaphore), and can signal that they have finished using the resource(incrementing the semaphore)."

# Reference 

 - [GeeksforGeeks about Mutext vs Semaphore](https://www.geeksforgeeks.org/mutex-vs-semaphore/)
 
 - [What is the difference between a mutex and a semaphore? in Quora](https://www.quora.com/What-is-the-difference-between-a-mutex-and-a-semaphore)
 
 - [Stackoverflow1](https://stackoverflow.com/questions/2350544/in-what-situation-do-you-use-a-semaphore-over-a-mutex-in-c/2350628#2350628)
 
 - [Stackoverflow2](https://stackoverflow.com/questions/2332765/lock-mutex-semaphore-whats-the-difference)
 
 - [Race condition on wikipedia](https://en.wikipedia.org/wiki/Race_condition)
