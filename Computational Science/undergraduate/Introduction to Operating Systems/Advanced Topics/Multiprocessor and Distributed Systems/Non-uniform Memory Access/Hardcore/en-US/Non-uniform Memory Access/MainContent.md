## Introduction
In the world of modern [high-performance computing](@entry_id:169980), not all memory accesses are created equal. The simple assumption of a uniform memory access (UMA) model, where any processor can access any memory location with the same speed, breaks down in today's multi-socket servers. This brings us to the concept of Non-Uniform Memory Access (NUMA), a fundamental architectural reality where the time it takes to access memory depends on its physical location relative to the processor. Failing to understand and account for NUMA can lead to severe and unexpected performance bottlenecks, preventing applications from realizing the full power of the underlying hardware. This article addresses the critical knowledge gap between NUMA hardware capabilities and the software design required to exploit them.

Over the next three chapters, you will embark on a comprehensive journey into the world of NUMA. We will begin in "Principles and Mechanisms" by dissecting the core architecture, quantifying the performance difference between local and remote access, and exploring the primary strategies [operating systems](@entry_id:752938) use for memory placement and [dynamic balancing](@entry_id:163330). Next, "Applications and Interdisciplinary Connections" will demonstrate how these principles translate into practice, showcasing NUMA-aware design patterns in operating systems, databases, [high-performance computing](@entry_id:169980), and virtualized environments. Finally, "Hands-On Practices" will challenge you to apply these concepts to solve concrete problems, solidifying your understanding of the trade-offs involved in NUMA optimization. Let's begin by exploring the foundational principles that govern performance in a NUMA system.

## Principles and Mechanisms

In a multiprocessor system, the physical architecture of the memory subsystem dictates the fundamental rules of performance. While simpler models assume all memory accesses are equal, the reality in most modern high-performance servers is one of Non-Uniform Memory Access (NUMA). This chapter delves into the core principles of NUMA and the sophisticated mechanisms that operating systems and hypervisors employ to manage, and even exploit, its characteristics.

### The NUMA Memory Hierarchy: Latency, Bandwidth, and Nodes

At its heart, a **Non-Uniform Memory Access (NUMA)** architecture is one in which the time to access a memory location varies depending on the physical proximity of that memory to the processor executing the request. A modern multiprocessor server is typically composed of several **NUMA nodes**. Each node, often corresponding to a physical processor socket, contains a set of CPU cores and its own local bank of memory, managed by its own [memory controller](@entry_id:167560).

When a thread running on a core within a given NUMA node accesses memory that is physically connected to that same node, the access is termed a **local access**. This is the fastest path, characterized by the lowest latency, denoted as $L_{\text{local}}$, and the highest sustainable bandwidth, $B_{\text{local}}$. Conversely, if the thread needs to access memory belonging to a different NUMA node, the request must traverse a high-speed **interconnect** fabric that links the nodes. This is a **remote access**, and it incurs a higher latency, $L_{\text{remote}}$, and typically provides lower sustained bandwidth, $B_{\text{remote}}$, where $L_{\text{remote}} > L_{\text{local}}$ and $B_{\text{remote}}  B_{\text{local}}$ . For example, typical values on a modern server might be $L_{\text{local}} = 85$ ns and $L_{\text{remote}} = 165$ ns .

This physical reality imposes a clear objective for any NUMA-aware software: to maximize the proportion of memory accesses that are local. This principle of **locality**, co-locating computation with the data it operates upon, is the central challenge in NUMA systems.

The performance impact of remote accesses is most pronounced in [memory-bound](@entry_id:751839) applications. The effective average memory access latency experienced by a thread is a weighted average of local and remote latencies, determined by the fraction of its accesses that are remote. If a fraction $p$ of a thread's memory accesses are remote, its average access latency $L_{\text{avg}}$ becomes:

$L_{\text{avg}} = (1 - p) \cdot L_{\text{local}} + p \cdot L_{\text{remote}}$

For a workload whose performance is dictated by the speed of memory, the overall throughput is inversely proportional to this average latency. An increase in the remote access fraction $p$ directly leads to a higher $L_{\text{avg}}$ and a corresponding decrease in performance .

### Memory Placement Mechanisms

The operating system (OS) is the primary agent responsible for managing NUMA locality. It does so through two main levers: placing memory pages on specific nodes and scheduling threads onto specific cores. The initial placement of memory is a critical first step.

#### First-Touch Policy: The Default Allocation Strategy

Most general-purpose operating systems employ a simple yet effective heuristic for initial page placement known as the **[first-touch policy](@entry_id:749423)**. Under this policy, a physical page of memory is allocated on the NUMA node of the CPU core that *first writes* to that page . This strategy is based on the assumption that the thread that initializes data is likely the one that will process it later.

The power and pitfalls of this policy are best illustrated with an example. Consider a large matrix $A$ being initialized before a [parallel computation](@entry_id:273857).
- If a single thread on node 0 initializes the entire matrix, the [first-touch policy](@entry_id:749423) will cause all pages of $A$ to be allocated on node 0. If the subsequent computation involves threads on other nodes (e.g., node 1) accessing parts of this matrix, those threads will suffer from slow, remote memory accesses, bottlenecking system performance .
- In contrast, if the initialization is done in parallel, where each thread initializes the specific rows of the matrix it will later process, the [first-touch policy](@entry_id:749423) naturally distributes the matrix's pages across the NUMA nodes according to the workload's data decomposition. This leads to predominantly local accesses for all threads during the main computation phase, maximizing performance.

To make this concrete, imagine a system with $m=3$ nodes and $q=12$ threads, where threads $\{0,1,2,3\}$ are pinned to node 0, threads $\{4,5,6,7\}$ to node 1, and threads $\{8,9,10,11\}$ to node 2. An array is divided into 12 chunks, and thread $i$ initializes chunk $i$. Due to the [first-touch policy](@entry_id:749423), each node will end up owning the pages for the 4 chunks initialized by its local threads, resulting in each of the 3 nodes owning exactly $\frac{1}{3}$ of the total pages. Now, if the computational phase involves each thread $i$ reading data from chunk $(i+1) \pmod{12}$, we can precisely predict the locality. Threads $0, 1, 2$ will read from chunks $1, 2, 3$ respectively, all of which are on their local node 0. However, thread 3 will read from chunk 4, which is on node 1—a remote access. By analyzing this pattern for all threads, we can find that exactly 3 out of the 12 threads will perform fully remote reads, leading to an overall remote access ratio of $\frac{3}{12} = \frac{1}{4}$ for the entire workload . This demonstrates how initialization patterns and thread placement directly and predictably determine the performance characteristics of the application.

#### Explicit Placement Policies: Interleaving and Binding

While first-touch is a powerful default, the OS also provides explicit controls for memory placement. Two common strategies are **[interleaving](@entry_id:268749)** and **node binding**.

**Node binding** (or local allocation) is the strategy of forcing all of a thread's memory allocations to its local node. This is the ideal strategy for workloads that can be perfectly partitioned, where each thread operates on its own private dataset. In a streaming workload with $N$ threads, one per node, perfect node binding allows the total system throughput to be the sum of the individual node bandwidths, $\sum_{i=1}^{N} B_i$, as there is no remote traffic to congest the interconnect .

**Interleaving**, by contrast, stripes memory pages across all NUMA nodes in a round-robin fashion. When a thread accesses a large, interleaved [data structure](@entry_id:634264), approximately $\frac{1}{N}$ of its accesses will be local and $\frac{N-1}{N}$ will be remote. This strategy is beneficial when a large data structure is shared and accessed unpredictably by all threads, as it balances the load across all memory controllers. However, it is detrimental for partitioned workloads, as it forces threads to constantly make remote accesses, destroying locality . Furthermore, [interleaving](@entry_id:268749) imposes two potential bottlenecks on system throughput: the bandwidth of the slowest node (total throughput is limited by $N \times \min_i\{B_i\}$) and the saturation of the interconnect (total throughput is limited by $S \frac{N}{N-1}$, where $S$ is the interconnect bandwidth) . The choice between binding and [interleaving](@entry_id:268749) depends critically on the application's memory access pattern.

#### Strategic Placement for Different Data Types

The optimal placement strategy depends on how data is used. For data that is primarily written and read by a single thread, first-touch or explicit binding to that thread's node is best. For read-only data that is shared among many threads, the situation is more complex. Placing it on one node forces all other nodes to access it remotely. Interleaving can improve aggregate bandwidth for reading this data. If the data structure is small enough, the best strategy is often to replicate it on every NUMA node, eliminating remote accesses entirely at the cost of increased memory usage .

For data with mixed read/write patterns from different nodes, a quantitative decision can be made. Consider a data structure written exclusively by threads on node A and read exclusively by threads on node B. Let the remote read penalty be $p_r$ and the remote write penalty be $p_w$. If the fraction of write operations is $\rho$, the expected access latency is the same whether the data is on node A or B when $\rho$ equals a specific threshold, $\rho^*$. This threshold can be derived from first principles:

$\rho^* = \frac{p_r}{p_w + p_r}$

If the actual write fraction $\rho > \rho^*$, the workload is write-dominated, and it is optimal to place the data on node A (local to the writer). If $\rho  \rho^*$, it is read-dominated, and placement on node B (local to the reader) is preferable . This elegant result shows how knowledge of hardware characteristics and workload patterns can inform precise, optimal placement decisions.

### Dynamic Balancing: Adapting to Changing Workloads

Initial placement is not the end of the story. Application behavior can change over time, and threads may be moved by the scheduler for load-balancing purposes. A static placement can thus become suboptimal. To address this, modern operating systems implement **NUMA balancing**, a dynamic process that continuously monitors for and corrects mismatches between thread location and memory location. This involves two primary mechanisms: [thread migration](@entry_id:755946) and [page migration](@entry_id:753074).

#### Thread Migration: Moving Computation to Data

The OS scheduler is tasked with placing threads on CPU cores. In a NUMA system, this task has two, often conflicting, goals: maintaining **load balance** by distributing runnable threads evenly across all cores, and preserving **locality** by keeping threads on the node where their data resides. The Linux Completely Fair Scheduler (CFS), for instance, primarily prioritizes fairness, but NUMA balancing mechanisms can influence its decisions .

To reconcile these goals, schedulers can use **soft affinity**. Rather than strictly pinning a thread, the scheduler uses a [scoring function](@entry_id:178987) to evaluate the "cost" of placing a thread on a candidate socket. This cost typically includes a term for locality and a term for load. A sophisticated [scoring function](@entry_id:178987) might look like:

$S(j) = \alpha P(d(j,m)) + \beta U(j)$

Here, $U(j)$ is the CPU utilization (load) of the target socket $j$, and $P(d(j,m))$ is a penalty for the NUMA distance $d$ between the socket $j$ and the thread's home memory node $m$. The choice of the [penalty function](@entry_id:638029) $P(d)$ is crucial. A linear penalty ($P(d)=d$) creates a fixed trade-off. A better approach is a [concave function](@entry_id:144403), such as $P(d) = 1 - \exp(-\gamma d)$, which imposes a large penalty for the first step away from the local node but has diminishing marginal penalties for moving between already-remote nodes . This allows the load-balancing term $\beta U(j)$ to dominate the decision when a thread is already far from its data, preventing severe load imbalances while still strongly encouraging locality.

#### Page Migration: Moving Data to Computation

The other side of [dynamic balancing](@entry_id:163330) is moving the data itself. If a thread consistently accesses a remote page, the OS may decide to migrate that page to the thread's local node. This is **[page migration](@entry_id:753074)**. The central question is *when* to migrate.

A migration decision is fundamentally a cost-benefit analysis. Migrating a page incurs a significant one-time cost, $C_m$. This cost is only justified if the cumulative latency savings from future local accesses outweigh it. The saving for each remote access that becomes local is $\Delta L = L_r - L_l$. Therefore, to break even, the number of future remote accesses, $N$, must satisfy $N \cdot \Delta L \ge C_m$. An OS can implement a heuristic based on this: it monitors the number of remote accesses to a page over a time window and triggers a migration if this count exceeds a threshold $T = \frac{C_m}{L_r - L_l}$ .

Migration policies must also be stable. An **eager** policy migrates as soon as the threshold is crossed, offering quick responses but risking reacting to transient spikes in access patterns. A **lazy** policy, which waits for the condition to hold for several consecutive observation periods, provides more stability at the cost of slower adaptation .

A major challenge in [page migration](@entry_id:753074) is **ping-ponging**, where a page is repeatedly moved back and forth between nodes due to fluctuating access patterns from threads on different nodes. To prevent this, a robust migration system can implement a **cooldown period**, $\tau$, during which a recently moved page cannot be migrated again. The ideal duration of this cooldown must satisfy two criteria: it must be long enough to amortize the migration cost, and it must be long enough to be statistically confident that the change in access pattern is persistent, not just random noise. A sophisticated policy might set the cooldown as:

$\tau = \max\left(\frac{C_m}{\Delta\ell \cdot |\mu|}, \alpha \frac{\sigma^2}{\mu^2 \lambda}\right)$

The first term is the **amortization time**, where $|\mu|$ is the observed access rate difference that prompted the migration. The second term is the **confidence time**, which ensures stability by waiting longer if the access pattern is volatile (high variance $\sigma^2$) or the signal is weak (low $|\mu|$) .

#### The Dynamics of Locality

In a truly dynamic system where both threads migrate and memory access patterns evolve, achieving perfect locality is impossible. There will always be a non-zero steady-state fraction of "mislocated" pages. This fraction can be modeled based on the relative rates of system dynamics. If threads migrate between nodes with a characteristic rate $\mu$, and pages are created and destroyed (turned over) with a rate $\lambda$, the steady-state fraction of mislocated pages, $F_{mis}$, is given by:

$F_{mis} = \frac{\mu}{\lambda + 2\mu}$

This shows that locality is inherently a race between thread movement and memory lifecycle. If threads move much more frequently than the [working set](@entry_id:756753) changes ($\mu \gg \lambda$), the fraction of mislocated pages will be high. If the working set is volatile and pages turn over quickly ($\lambda \gg \mu$), a page is likely to be evicted before a [thread migration](@entry_id:755946) makes it mislocated, resulting in better overall locality .

### Advanced Topics and Modern Contexts

The principles of NUMA extend into more complex areas of modern systems, including large page sizes and [virtualization](@entry_id:756508).

#### Transparent Huge Pages (THP) and NUMA

Operating systems can use **Transparent Huge Pages (THP)**—typically 2 MiB or 1 GiB in size—to reduce [page table](@entry_id:753079) overhead and improve TLB hit rates. However, THP interacts critically with NUMA balancing. The cost to migrate a 2 MiB huge page, $C_{mig,THP}$, is hundreds of times greater than migrating a standard 4 KiB page.

Applying the same [cost-benefit analysis](@entry_id:200072), the break-even number of accesses, $N^*$, required to justify migrating a huge page is enormous. For a page that improves from 10% local accesses to 95% local, with typical latencies and a migration cost of $C_{mig,THP} = 0.34$ ms, the break-even point can be on the order of 5000 accesses . This implies that migration decisions for [huge pages](@entry_id:750413) must be far more conservative than for small pages, as a wrong decision carries a much larger penalty.

#### NUMA in Virtualized Environments

Virtualization introduces another layer of complexity. A guest operating system inside a Virtual Machine (VM) is often presented with a virtual UMA architecture for simplicity and compatibility. However, the host system running the [hypervisor](@entry_id:750489) may be a NUMA machine. This creates an abstraction mismatch.

The hypervisor is responsible for placing the VM's virtual CPUs (vCPUs) and backing its memory with physical pages. If a VM's vCPUs are pinned to one node, the hypervisor's [first-touch policy](@entry_id:749423) will naturally place the VM's memory on that same node, ensuring good locality. However, other hypervisor operations can disrupt this. For instance, **[memory ballooning](@entry_id:751846)**, a technique used to reclaim memory from a VM, can force the [hypervisor](@entry_id:750489) to re-allocate the VM's memory on a remote node if the local node is under memory pressure. The guest OS remains unaware of this change, but its applications will experience a sudden performance degradation due to the increased average [memory latency](@entry_id:751862) from remote accesses . This illustrates that even when abstracted away, the underlying NUMA topology remains a critical factor for performance in virtualized cloud environments.