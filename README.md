# Advanced Multithreading


## Introduction
In this assignment, I should solve three problems related to multithreaded programming and its different areas.

## Implementation
### Pi Calculator
- I used an infinite series to calculate Pi. Based on pi = 4arctan(1) and the Maclaurin series for arc tangent, the series can be written as: pi = 4 (1 - 1/3 + 1/5 - 1/7...).
- `BigDecimal` class should be used when calculating very long numbers.
- I created a `FixedThreadPool` with 4 threads and each instance of the `CalculatePi` class is executed in this thread pool.
- This algorithm worked best among the ones I tried and although it passed the easy test, other tests failed. This may be because it needs to go so far in the series to reach the desired accuracy.
### Priority Stimulator
- This task is done using `CountDownLatch` class. An object of this class lets you count down from a number that you specify and makes one or more threads wait until the latch reaches a count of zero. So one or more threads can count down the latch and when it finally equals zero, one or more threads that are waiting on the latch can then proceed.  
- In order to use this, three CountDownLatches are made for each class using their own count. Then, latches are assigned to classes and in the `run` method, `CountDownLatch.countDown()` is called so that everytime the thread starts, one is subtracted from the latch. The massage is also printed in this method.
- It's worth mentioning that after starting the specified number of each thread type (in the for loop), `CountDownLatch.await()` is called to wait until it is finished and then move on to the next kind of thread.  
### Semaphore
- Semaphore in Java is a thread synchronization construct that sends signals to the threads and protects critical sections. With the use of counters, Semaphore manages access to the shared resources.
- Since, in this assignment, a maximum of 2 operators should access the resource concurrently, an instance of the `Semaphore` class with 2 permits. It also has a second parameter called fairness and when set to true, it ensures that whichever thread that was waiting for the permit the longest will be given the permit first. This single instance of Semaphore is shared between all threads so that the threads will be synchronized.
- The Semaphore instance is acquired before the critical section. You can either surround `Semaphore.acquire()` with try catch or use `Semaphore.acquireUninterruptibly()`. After the critical section, Semaphore is released. Additionally, Semaphores can acquire and release more than one permit.
- Current thread name and system time is printed in the `Resource` class.
- And don’t forget to put release in a `finally` block.