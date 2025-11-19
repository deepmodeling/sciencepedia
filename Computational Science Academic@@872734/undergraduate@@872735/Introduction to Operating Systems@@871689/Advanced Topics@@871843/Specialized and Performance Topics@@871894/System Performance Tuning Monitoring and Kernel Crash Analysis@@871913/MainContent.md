## Introduction
Achieving peak performance and unwavering stability are the twin pillars of modern [operating system design](@entry_id:752948). Yet, as systems grow in complexity with [multicore processors](@entry_id:752266), deep memory hierarchies, and concurrent execution, identifying performance bottlenecks and diagnosing the root cause of system failures becomes an increasingly formidable challenge. Engineers can no longer rely on intuition alone; they require a rigorous, evidence-based methodology to navigate this complex landscape. This article addresses this need by providing a comprehensive guide to the principles and practices of system performance tuning and kernel crash analysis.

Over the course of three chapters, you will build a robust conceptual toolkit for both optimizing a running system and investigating a failed one. We will begin in **Principles and Mechanisms** by dissecting the core trade-offs in CPU, I/O, and memory management, exploring concurrency primitives like RCU, and identifying critical failure modes such as deadlocks and memory corruption. Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action, using quantitative models and diagnostic reasoning to solve real-world performance problems and analyze complex system crashes. Finally, you will solidify your understanding through a series of **Hands-On Practices**, applying these analytical techniques to concrete engineering challenges. By moving from theory to application, this journey will equip you to build faster, more reliable, and more efficient computing systems.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms that govern system performance, concurrency, and stability. We move from the high-level goal of optimizing a functional system to the low-level, forensic analysis required when a system fails. Our exploration will be grounded in quantitative models and concrete case studies, providing a conceptual toolkit for both tuning and debugging complex [operating systems](@entry_id:752938).

### Core Principles of System Performance

System performance is not a single metric but a balance of competing objectives. The most common trade-offs are between **latency** (the time to complete a single task) and **throughput** (the number of tasks completed per unit time), and between **fairness** (ensuring all tasks receive a reasonable share of resources) and **efficiency** (maximizing total work done). Effective performance tuning requires understanding how underlying mechanisms influence these trade-offs.

#### CPU Scheduling Performance

The Central Processing Unit (CPU) is often the most critical system resource. The CPU scheduler's role is to allocate processor time among runnable tasks, and its design has a profound impact on system responsiveness and overall throughput.

A primary overhead in a [multitasking](@entry_id:752339) system is the **context switch**, the process of saving the state of one task and restoring the state of another. While necessary for concurrent execution, [context switching](@entry_id:747797) is non-productive work; it is pure overhead. To understand its impact, consider a single-core CPU with $n$ identical, compute-bound threads. If the scheduler dispatches each thread for a fixed [time quantum](@entry_id:756007) $q$, the total time for one dispatch cycle includes the quantum and the context switch cost, $C_s(n)$. The fraction of CPU time spent on useful work is thus $\frac{q}{q + C_s(n)}$.

The cost of a context switch, $C_s(n)$, is not always constant. It often depends on the number of runnable threads, $n$. For instance, a scheduler that maintains runnable threads in a data structure like a [balanced binary search tree](@entry_id:636550) (as some modern schedulers do) will have a decision-making component that scales with the logarithm of $n$. We can model this cost as $C_s(n) = C_0 + a \ln(n)$, where $C_0$ is the constant hardware and state-saving overhead, and $a$ is a constant reflecting the scheduler's [algorithmic complexity](@entry_id:137716). The system's effective throughput $T(n)$, starting from a baseline single-thread rate of $X_0$, can then be expressed as:

$$
T(n) = X_0 \frac{q}{q + C_0 + a \ln(n)}
$$

This model reveals that as $n$ increases, the denominator grows, and throughput $T(n)$ decreases. There exists a critical point where the overhead becomes so significant that it equals the useful work time. We can define this point, $n^*$, as the number of threads where the context switch cost equals the [time quantum](@entry_id:756007), $C_s(n^*) = q$. Solving for $n^*$ gives us a measure of the system's scalability limit with respect to thread count [@problem_id:3686464]:

$$
C_0 + a \ln(n^*) = q \implies n^* = \exp\left(\frac{q - C_0}{a}\right)
$$

Beyond $n^*$ threads, the system spends more time switching between tasks than executing them, a condition known as **[thrashing](@entry_id:637892)**. This analysis demonstrates a crucial principle: adding more [concurrency](@entry_id:747654) does not always improve throughput and can be actively harmful beyond a certain point.

Beyond managing overhead, schedulers must also implement a policy for fairness and prioritization. The Linux **Completely Fair Scheduler (CFS)** provides an excellent example. Instead of fixed time slices, CFS allocates CPU time proportionally based on **scheduling weights**. Each task has a **niceness** value, an integer typically from $-20$ (highest priority) to $+19$ (lowest priority), which maps to a weight $w_i$. The core principle of CFS is to equalize the **[virtual runtime](@entry_id:756525)**, $v_i$, of all runnable tasks. When a task $i$ runs for a real time increment $\mathrm{d}t$, its [virtual runtime](@entry_id:756525) advances by $\mathrm{d}v_i = \mathrm{d}t \cdot \frac{W_0}{w_i}$, where $W_0$ is a reference weight. By always picking the task with the smallest $v_i$, the scheduler ensures that, over time, tasks with higher weights (lower niceness) are allowed to run for longer periods to keep their [virtual runtime](@entry_id:756525) from falling behind.

This mechanism leads to a direct relationship between a task's weight and its share of the CPU. For a set of $N$ continuously runnable tasks, the long-run fraction of CPU time $s_k$ allocated to task $k$ is simply its weight divided by the total weight of all runnable tasks [@problem_id:3686485]:

$$
s_k = \frac{w_k}{\sum_{i=1}^{N} w_i}
$$

For example, on a system with three tasks having niceness values of $0$, $5$, and $10$ (corresponding to canonical weights $w_1=1024$, $w_2=335$, and $w_3=110$), the total weight is $1469$. The second task's share of the CPU would be $s_2 = \frac{335}{1469} \approx 0.228$, or $22.8\%$. This elegant mechanism allows system administrators to tune task priorities predictably.

#### I/O Scheduling Performance

Similar to CPU scheduling, I/O scheduling involves managing a queue of requests for a shared resource—in this case, a storage device. Here, the central conflict is often between system-wide throughput and inter-process fairness.

A throughput-oriented scheduler might adopt a policy akin to Shortest Job First (SJF) to maximize the number of I/O operations per second (IOPS). For a disk, this often translates to servicing requests that require the least physical movement of the disk head, a strategy that minimizes [seek time](@entry_id:754621). A modern **Multi-Queue (MQ)** scheduler could implement this by selecting the ready request that minimizes a [cost function](@entry_id:138681), such as one that prioritizes smaller requests or gives preference to reads over writes if reads are faster on the underlying hardware. While this approach maximizes overall bandwidth, it risks **starvation**. A process issuing large, slow requests could be perpetually delayed as the scheduler prioritizes a stream of small, fast requests from other processes [@problem_id:3686479].

Conversely, a fairness-oriented scheduler, such as the conceptual model of **Completely Fair Queuing (CFQ)**, aims to provide temporal fairness. It might organize requests into per-process queues and service them in a round-robin fashion. This ensures that every process gets a turn to have its I/O served, preventing starvation. However, this approach can reduce overall throughput, as enforcing a strict turn-taking order may prevent the scheduler from making the most efficient choice from a device-level perspective (e.g., servicing a nearby request instead of seeking to a different process's request location) [@problem_id:3686479]. The choice between these strategies depends on the workload: interactive systems may favor fairness to ensure responsiveness, while batch processing systems might favor throughput.

#### Memory Management Performance

Memory access is a cornerstone of performance. Modern systems employ complex hierarchies of caches and memory controllers to bridge the speed gap between the CPU and [main memory](@entry_id:751652). Understanding and optimizing memory access patterns is critical.

A key component in this hierarchy is the **Translation Lookaside Buffer (TLB)**, a hardware cache for virtual-to-physical address translations. A TLB miss is costly, requiring a multi-level [page table walk](@entry_id:753085) that can consume hundreds of CPU cycles. **Transparent Huge Pages (THP)** are a mechanism designed to mitigate this cost. By using a larger page size (e.g., $2\,\mathrm{MB}$ instead of $4\,\mathrm{KB}$), a single TLB entry can cover a much larger memory region. This dramatically increases the effective reach of the TLB.

The benefit of THP can be profound. Consider a process with a $48\,\mathrm{MB}$ anonymous memory working set on a system where the TLB holds $1536$ entries for $4\,\mathrm{KB}$ pages and $32$ entries for $2\,\mathrm{MB}$ pages. With $4\,\mathrm{KB}$ pages, the working set spans $12,288$ pages, vastly exceeding the TLB's capacity and leading to a high miss rate. With $2\,\mathrm{MB}$ [huge pages](@entry_id:750413), the same working set spans just $24$ pages. Since this fits entirely within the huge page TLB capacity of $32$, TLB misses are virtually eliminated, potentially saving billions of CPU cycles per second across multiple such processes [@problem_id:3686470].

However, THP is not a universal solution and comes with significant overheads. These include:
1.  **Compaction Cost**: To create a $2\,\mathrm{MB}$ huge page, the kernel must find a contiguous $2\,\mathrm{MB}$ block of free physical memory. Under memory pressure, this often requires costly [compaction](@entry_id:267261) operations, where existing pages are moved around to create a large enough free block. These operations consume CPU and can stall applications.
2.  **Copy-on-Write (CoW) Overhead**: When a process with [huge pages](@entry_id:750413) calls `[fork()](@entry_id:749516)`, the child process initially shares the parent's memory. If either process then writes to a shared huge page, the kernel must perform a copy-on-write. This may involve splitting the $2\,\mathrm{MB}$ page into 512 separate $4\,\mathrm{KB}$ pages, a highly expensive operation.
3.  **Internal Fragmentation**: In memory-constrained environments like containers, THP can be particularly harmful. If an application needs only a few kilobytes of memory, the kernel might still allocate a full $2\,\mathrm{MB}$ huge page. The entire $2\,\mathrm{MB}$ counts against the container's memory limit (cgroup), leading to artificial memory pressure, premature invocation of the memory reclaimer, and even Out-Of-Memory (OOM) kills [@problem_id:3686470].

For these reasons, a workload of many small containers with frequent forks and diverse memory needs may perform worse with THP enabled, as the overheads of [compaction](@entry_id:267261), CoW splits, and fragmentation can easily outweigh the limited TLB benefits, especially if a large portion of memory access is to file-backed pages not covered by THP. This highlights a key tuning principle: a mechanism's effectiveness is highly context-dependent.

Another critical aspect of [memory performance](@entry_id:751876) on modern servers is **Non-Uniform Memory Access (NUMA)**. In a NUMA architecture, a system has multiple memory nodes, and a CPU can access its local node faster than remote nodes. A NUMA-aware page allocator will always try to satisfy a memory request from the local node first. Under high memory pressure, however, the local node may run out of free pages. The allocator's fallback strategy is critical. A naive strategy might be to immediately allocate from the nearest remote node. This minimizes allocation latency but can lead to a high ratio of slow, remote memory accesses, degrading application performance.

A more robust strategy is needed to balance allocation latency with [memory locality](@entry_id:751865). The kernel first attempts to free local memory via **direct reclaim** (synchronously freeing pages) or **compaction**. If these fail, it must consider remote allocation. To prevent the system from being overwhelmed by remote accesses, a policy can be implemented to rate-limit them. A **[token bucket](@entry_id:756046)** algorithm is an effective mechanism for this. The bucket is filled with tokens at a predefined rate $\alpha$. Each remote allocation consumes one token. If the bucket is empty, the allocation request must block until a new token is generated. By setting the fill rate $\alpha$ to a desired maximum remote allocation rate (e.g., $\alpha = r_{\max} \cdot \hat{\lambda}$, where $r_{\max}$ is the target ratio and $\hat{\lambda}$ is the observed [arrival rate](@entry_id:271803) of allocation requests), the system can enforce a strict upper bound on remote memory usage. This provides crucial **[backpressure](@entry_id:746637)**, signaling to applications that the system is overloaded and preventing a runaway degradation in performance [@problem_id:3686489]. Policies that disallow remote allocation entirely or perform unbounded local work risk [livelock](@entry_id:751367) and are not viable.

### Concurrency Mechanisms and Synchronization Hazards

In a multicore, [preemptive kernel](@entry_id:753697), shared [data structures](@entry_id:262134) must be protected from concurrent access. The choice and implementation of [synchronization primitives](@entry_id:755738) are central to both correctness and performance.

#### Spinlocks vs. Mutexes: The Busy-Wait vs. Block Trade-off

Two fundamental locking primitives are spinlocks and mutexes.
-   A **[spinlock](@entry_id:755228)** is a simple lock where a thread attempting to acquire a busy lock enters a tight loop, repeatedly checking the lock's status—an action known as **[busy-waiting](@entry_id:747022)**. This consumes CPU cycles but avoids the high cost of a context switch.
-   A **[mutex](@entry_id:752347)** (or sleeping lock) causes a thread attempting to acquire a busy lock to block. The scheduler is invoked to deschedule the waiting thread and run another one. The waiting thread consumes no CPU until it is woken up when the lock is released.

The choice between them depends on the expected lock hold time. Spinlocks are efficient if the lock is held for a very short duration, typically less than the time required for two context switches (one to block, one to unblock). Mutexes are preferable for longer critical sections, as blocking avoids wasting CPU cycles on [busy-waiting](@entry_id:747022).

We can formalize this trade-off. Let the contention probability (the probability of finding the lock busy) be $p$. Let the CPU costs for an uncontended acquire-release be $a_s$ for a [spinlock](@entry_id:755228) and $a_m$ for a mutex, where typically $a_m > a_s$. If the lock is busy, the [spinlock](@entry_id:755228) user busy-waits for the residual lock holding time $R$, while the [mutex](@entry_id:752347) user blocks, incurring a fixed scheduler overhead $S$. The expected CPU costs per acquisition, $\mathbb{E}[C_s]$ and $\mathbb{E}[C_m]$, are [@problem_id:3686533]:

$$
\mathbb{E}[C_s] = (1-p)a_s + p(a_s + \mathbb{E}[R]) = a_s + p\mathbb{E}[R]
$$
$$
\mathbb{E}[C_m] = (1-p)a_m + p(a_m + S) = a_m + pS
$$

The break-even contention probability $p^*$ where both strategies have equal cost is found by setting $\mathbb{E}[C_s] = \mathbb{E}[C_m]$ and solving for $p$:

$$
p^* = \frac{a_m - a_s}{\mathbb{E}[R] - S}
$$

This equation provides a powerful guideline: for a given workload, if the contention probability is less than $p^*$, a [spinlock](@entry_id:755228) is more efficient; if it is greater, a [mutex](@entry_id:752347) is the better choice. The expected residual holding time, $\mathbb{E}[R]$, can be estimated from the mean $\mathbb{E}[T]$ and second moment $\mathbb{E}[T^2]$ of the lock holding time using the [inspection paradox](@entry_id:275710) formula from [renewal theory](@entry_id:263249), $\mathbb{E}[R] = \frac{\mathbb{E}[T^2]}{2\mathbb{E}[T]}$.

#### Read-Copy Update (RCU): A Lock-Free Read Mechanism

For [data structures](@entry_id:262134) that are read far more often than they are written, even the overhead of read-write locks can be prohibitive. **Read-Copy Update (RCU)** is a sophisticated synchronization mechanism that allows for lock-free reads.

The core idea is simple: readers access data directly without acquiring any locks. Writers who wish to modify the data structure create a copy, modify it, and then atomically update a global pointer to point to the new version. The old version of the data cannot be freed immediately, because pre-existing readers may still be referencing it. Instead, the writer must wait for a **grace period** to elapse. A grace period is defined as the time interval required for every CPU in the system to pass through a **quiescent state**—a state where it is guaranteed to not be in an RCU read-side critical section (e.g., by executing a [context switch](@entry_id:747796)). Once a grace period ends, the writer knows that all readers that were active at the time of the update have finished, and it is safe to reclaim the memory of the old data structure.

A critical subtlety of RCU is that it comes in several "flavors," or domains, designed for different kernel contexts. For example, regular RCU protects against preemption in normal kernel code, while RCU-BH (Bottom Half) protects against code running in software interrupt context. The writer and reader must use mechanisms corresponding to the same RCU domain. A mismatch can lead to catastrophic failure.

Consider a scenario where a reader enters a regular RCU critical section (using `rcu_read_lock()`). A writer then updates the [data structure](@entry_id:634264) and, to wait for readers, mistakenly calls `synchronize_rcu_bh()`. This function initiates and waits for an RCU-BH grace period. Since the reader is in a regular RCU section, not a bottom-half-disabled region, the RCU-BH subsystem considers it quiescent. The RCU-BH grace period can therefore end quickly, long before the reader has actually finished its work. Believing it is safe, the writer proceeds to free the old data. When the reader subsequently attempts to dereference its pointer to that data, it triggers a [use-after-free](@entry_id:756383) fault [@problem_id:3686483]. This illustrates a fundamental principle of using complex APIs: one must understand and respect the precise contract of the functions being called.

#### Deadlock and Livelock

The most feared hazard in [concurrent programming](@entry_id:637538) is **[deadlock](@entry_id:748237)**, a state where two or more threads are blocked forever, each waiting for a resource held by another. According to the Coffman conditions, [deadlock](@entry_id:748237) requires four conditions to hold simultaneously: [mutual exclusion](@entry_id:752349), [hold-and-wait](@entry_id:750367), no preemption, and [circular wait](@entry_id:747359). Preventing [deadlock](@entry_id:748237) involves breaking at least one of these conditions.

The most common strategy is to break the [circular wait](@entry_id:747359) condition by enforcing a strict global [lock ordering](@entry_id:751424). All threads must acquire locks in the same predefined order. A violation of this rule, known as a **lock order inversion**, creates a cycle in the lock-[dependency graph](@entry_id:275217) and introduces the risk of deadlock.

For instance, imagine three locks $L_A, L_B, L_C$ and three threads with the following acquisition patterns [@problem_id:3686487]:
-   Thread $T_1$: acquires $L_A$, then $L_B$. (Establishes dependency $L_A \rightarrow L_B$)
-   Thread $T_2$: acquires $L_B$, then $L_C$. (Establishes dependency $L_B \rightarrow L_C$)
-   Thread $T_3$: acquires $L_C$, then $L_A$. (Establishes dependency $L_C \rightarrow L_A$)

This set of acquisitions creates a directed cycle in the lock-order graph: $L_A \rightarrow L_B \rightarrow L_C \rightarrow L_A$. This cycle represents a [circular wait](@entry_id:747359) dependency. Under specific scheduling timings, $T_1$ could hold $L_A$ and wait for $L_B$, $T_2$ could hold $L_B$ and wait for $L_C$, and $T_3$ could hold $L_C$ and wait for $L_A$, resulting in a classic deadlock. Kernel lock validators are designed to detect such cycles dynamically and report them as latent bugs, even if a [deadlock](@entry_id:748237) has not yet occurred.

### Kernel Integrity and Crash Dump Analysis

While performance tuning aims to make a system fast, ensuring its stability and correctness is paramount. When the kernel encounters an unrecoverable internal error, it triggers a **panic**. The system halts, and if configured, a crash dump containing the kernel's memory state is saved. Analyzing these dumps is a form of digital forensics, requiring a deep understanding of OS internals to deduce the root cause from the available evidence.

#### Class 1: Memory Safety Violations

Memory safety bugs are a common and dangerous class of kernel errors. They can lead to [data corruption](@entry_id:269966), security vulnerabilities, and system crashes.

##### Stack-Based Buffer Overflow

The boundary between kernel space and user space is a critical security frontier. Kernel code must treat all input from user space as untrusted. A classic vulnerability arises when copying data from a user-supplied pointer into a fixed-size kernel buffer.

Consider a kernel handler that copies data into a stack-allocated buffer of size $L_{\max}$. The user provides a pointer and a length, $len$. The kernel function `copy_from_user` performs the copy but, for performance, does not validate the capacity of the destination buffer. The responsibility lies with the caller. If the handler blindly trusts the user-provided $len$ and it happens to be greater than $L_{\max}$, the copy will write past the end of the buffer, corrupting adjacent stack data. This can overwrite local variables, saved register values, and most critically, the function's return address and the **[stack canary](@entry_id:755329)**. A [stack canary](@entry_id:755329) is a secret value placed on the stack that is checked before a function returns; if it has been modified, a [buffer overflow](@entry_id:747009) is presumed to have occurred, and the kernel panics immediately to prevent a potential security exploit [@problem_id:3686517].

The only correct way to prevent this is to explicitly validate the user's input before the copy. The condition $0 \le len \le L_{\max}$ must hold. If it does not, the operation must be rejected with an error code (e.g., `-EINVAL` for invalid argument or `-EMSGSIZE` for message too long). Silently truncating the data (copying only $L_{\max}$ bytes) is poor API design, as it misleads the user-space application into believing the full operation succeeded, potentially leading to application-level bugs.

##### Use-After-Free and Double-Free via Reference Counting Errors

Dynamic objects in the kernel whose lifetimes are not tied to a simple scope often have their memory managed by **[reference counting](@entry_id:637255)**. An object maintains a counter, which is incremented every time a new reference to it is taken (`get`) and decremented when a reference is released (`put`). When the count reaches zero, the object has no more users and can be freed.

This seemingly simple scheme is notoriously difficult to get right. A single mistake in managing the count can lead to two major types of errors:
1.  **Memory Leaks**: If a `put` call is forgotten, the reference count will never reach zero, and the object will never be freed.
2.  **Use-After-Free (UAF) / Double-Free**: If `put` is called one too many times (e.g., a release without a corresponding acquire), the reference count can be prematurely decremented to zero. The object is freed, but one or more pointers to it may still exist. Any subsequent use of these stale pointers results in a UAF. If another `put` is called through a stale pointer, it becomes a **double-free**.

Modern kernel memory allocators and sanitizers (like KASAN, the Kernel Address Sanitizer) can help detect these errors. Upon freeing an object, the allocator can "poison" the memory region with a special bit pattern. A subsequent write to that region (a UAF) will corrupt the poison, which can be detected. A double-free attempt can be caught by checking if the memory being freed is already in a freed/poisoned state.

Analyzing a crash dump with a `double-free` report often involves reconstructing the call stack to identify the faulty code path. The stack trace, typically printed with the most recent function first, must be read from bottom to top to understand the chronological sequence of calls that led to the error. A common cause is a logic error where an object is released twice in a complex teardown sequence [@problem_id:3686496]. To proactively catch such bugs, robust assertions should be embedded in the [reference counting](@entry_id:637255) logic: immediately after an atomic decrement, assert that the new count is non-negative ($count \ge 0$). Before freeing, assert that the count is exactly zero ($count = 0$).

A UAF can also be caused by a [race condition](@entry_id:177665). Consider a request object in the I/O path that can be completed either by the [device driver](@entry_id:748349) or by a timeout handler. Both paths will release a reference. If the timeout handler's logic mistakenly fails to acquire its own reference before arming the timer, a race can occur. The I/O completes, decrementing the count to zero and freeing the object. Shortly after, the timeout handler fires and performs its own, illegitimate decrement on the now-freed object. This can drive the count to $-1$, a clear sign of underflow. The `ref = -1` log message is a smoking gun for this type of bug. An associated symptom might be the reference count appearing as a large unsigned number (e.g., $65535$), which is what $-1$ looks like when an unsigned integer wraps around [@problem_id:3686451]. The most robust defense is a centralized sanity check in the [reference counting](@entry_id:637255) helpers that validates the count against both a lower bound (zero) and a reasonable upper bound, warning developers of any deviation from expected behavior.

#### Class 2: Locking Protocol Violations

Just as memory access has strict rules, so does the use of [synchronization primitives](@entry_id:755738).

##### Double-Acquire of a Non-Recursive Lock

A standard [spinlock](@entry_id:755228) or [mutex](@entry_id:752347) is **non-recursive**. This means that a thread currently holding a lock cannot attempt to acquire it again without first releasing it. Such an attempt is a logical error. On a [spinlock](@entry_id:755228), this would cause the thread to spin forever, waiting for itself to release the lock—an immediate self-[deadlock](@entry_id:748237). On a [mutex](@entry_id:752347), it would also cause an unbreakable deadlock.

To prevent this, kernels often include checks that will cause an immediate panic if a double-acquire is detected. A panic message like "double-acquire of non-recursive [spinlock](@entry_id:755228)" points to a specific type of local bug: a code path that, through a nested or recursive call, attempts to take a lock it already holds [@problem_id:3686487].

It is crucial to distinguish this from the global [deadlock](@entry_id:748237) risk posed by lock-order inversions. A double-acquire is a local correctness violation within a single thread's execution. A lock-order cycle is a global property of the interactions between multiple threads. Fixing one does not fix the other. Even if a system's [lock ordering](@entry_id:751424) is perfectly acyclic and [deadlock](@entry_id:748237)-free, a double-acquire bug will still cause a panic. Both types of errors must be identified and fixed independently.