## Introduction
Register allocation—the process of assigning program variables to a finite set of processor registers—is a critical optimization for generating fast machine code. While traditional graph-coloring algorithms can produce high-quality code, their [computational complexity](@entry_id:147058) often makes them unsuitable for time-sensitive scenarios like Just-In-Time (JIT) compilation. This creates a knowledge gap for a faster, yet effective, alternative. This article delves into linear scan [register allocation](@entry_id:754199), a high-speed algorithm that has become a cornerstone of modern compilers.

Across the following chapters, you will gain a comprehensive understanding of this technique. The "Principles and Mechanisms" chapter will deconstruct the core algorithm, from computing live intervals to making spill decisions. Next, "Applications and Interdisciplinary Connections" will explore how linear scan interacts with compiler ecosystems and advanced hardware, from [calling conventions](@entry_id:747094) to GPU architectures. Finally, the "Hands-On Practices" section will provide practical problems to solidify your understanding of these concepts.

## Principles and Mechanisms

The linear scan approach to [register allocation](@entry_id:754199) offers a compelling alternative to the [combinatorial complexity](@entry_id:747495) of graph coloring. Its primary virtue is speed, achieved by reframing the problem from a global graph-coloring challenge to a linear traversal of the program's instruction sequence. This chapter will deconstruct the principles and mechanisms of linear scan [register allocation](@entry_id:754199), from its foundational concepts of liveness to the sophisticated optimizations that make it a practical and powerful technique in modern compilers, especially those in Just-In-Time (JIT) environments.

### Liveness and Live Intervals

The bedrock of any modern [register allocation](@entry_id:754199) algorithm is the concept of **liveness**. A variable (or temporary) is said to be **live** at a given program point if its current value may be used in the future. The contiguous range of program points where a variable is live is known as its **[live interval](@entry_id:751369)** or **[live range](@entry_id:751371)**. Linear scan [register allocation](@entry_id:754199) operates directly on these live intervals.

To build these intervals, we first need to compute liveness at every program point. This is typically accomplished using a backward **[dataflow analysis](@entry_id:748179)**. For a control flow graph (CFG), we can compute the set of live variables entering and exiting each basic block. Let $\mathrm{IN}[B]$ be the set of variables live at the entry of a basic block $B$, and $\mathrm{OUT}[B]$ be the set of variables live at its exit. These sets are determined by the variables used and defined within the block. Let $\mathrm{USE}[B]$ be the set of variables used in $B$ before any redefinition in $B$, and $\mathrm{DEF}[B]$ be the set of variables defined in $B$. The liveness information propagates backward from uses, governed by the standard [dataflow](@entry_id:748178) equations:

$$ \mathrm{OUT}[B] = \bigcup_{S \in \mathrm{succ}(B)} \mathrm{IN}[S] $$
$$ \mathrm{IN}[B] = \mathrm{USE}[B] \cup (\mathrm{OUT}[B] \setminus \mathrm{DEF}[B]) $$

Here, $\mathrm{succ}(B)$ is the set of successor blocks of $B$. These equations are solved iteratively until a fixed point is reached. Once block-level liveness is known, a similar [backward pass](@entry_id:199535) can be performed within each block to determine liveness at the boundary of every instruction.

A variable's [live interval](@entry_id:751369) is then constructed as the span from its definition to its last use. Formally, we represent this as an interval $[s, e)$, where $s$ is the program point of the definition and $e$ is the program point immediately following the last use. The precise definition of these endpoints is critical. A subtle off-by-one error in determining the end of an interval can lead to incorrect estimates of [register pressure](@entry_id:754204). For example, in an instruction like $c := a + b$, the liveness of operands $a$ and $b$ should arguably extend up to the point just *before* the instruction, while the liveness of the result $c$ begins just *after*. Incorrectly modeling these as occurring at the same point can inflate the perceived number of simultaneously live variables, potentially leading to unnecessary spills .

### The Basic Linear Scan Algorithm

With live intervals for all temporaries computed, the linear scan algorithm proceeds in a single pass. The core idea is to process intervals in the order of their starting points. The allocator maintains a set of intervals that are currently live and held in registers, known as the **active set**.

The algorithm can be summarized as follows:
1.  **Initialization**: Create a list of all live intervals, sorted by their starting program point. The set of `active` intervals is initially empty. All physical registers are free.
2.  **Iteration**: For each interval $i$ in the sorted list:
    a.  **Expire Old Intervals**: Traverse the `active` set. Any interval $j$ in `active` whose end point precedes the start point of the current interval $i$ (i.e., $e_j \le s_i$) is now dead. Its register is freed, and it is removed from the `active` set.
    b.  **Allocate**: If the number of `active` intervals is less than the number of available physical registers $R$, there is a free register. Allocate a free register to interval $i$ and add $i$ to the `active` set.
    c.  **Spill**: If the number of `active` intervals is already equal to $R$, there is no free register. A spill is necessary. The allocator must choose an interval to evict from a register.

The crucial component of this algorithm is the **spill heuristic**—the policy for choosing which interval to evict. A common naive policy is to simply spill the current interval $i$ . However, a more effective heuristic, proposed in the seminal work by Poletto and Sarkar, is to spill the interval in the `active` set that has the **farthest end point**. That is, from the set containing the current interval $i$ and all intervals in `active`, the allocator chooses to spill the one that lives the longest. If the current interval $i$ has an end point farther than any interval in `active`, then $i$ itself is spilled and never allocated a register. Otherwise, the active interval with the farthest end is spilled, and its register is reassigned to $i$.

This heuristic is effective because it prioritizes keeping short-lived intervals in registers, which helps to free up registers more quickly.

### Advanced Mechanisms and Optimizations

The basic linear scan algorithm is simple and fast, but its greedy nature can lead to suboptimal decisions. Several powerful optimizations have been developed to improve its quality.

#### Live Interval Splitting

A major weakness of the basic algorithm is its handling of long-lived variables. A variable that is live for a large portion of the program can occupy a register for a long time, even if it is used infrequently. This can cause many shorter-lived variables that conflict with it to be spilled.

The solution is **[live interval](@entry_id:751369) splitting**. Instead of treating a long interval as a single, indivisible unit, the allocator can "split" it at a point of high [register pressure](@entry_id:754204). This is implemented by inserting a **store** instruction to save the variable's value to a memory location (the stack) and freeing its register. Later, just before its next use, a **reload** instruction is inserted to bring the value back into a register.

This effectively breaks a single long interval into two or more smaller fragments. The period between the store and the reload, where the value resides only in memory, is called a **hole** in the [live interval](@entry_id:751369). While splitting incurs the cost of a store and a load, it can be a net win if it prevents multiple spills of other intervals. For instance, consider a long-lived variable $v$ that conflicts with several pairs of short-lived temporaries. Splitting $v$ once may cost two memory operations (one store, one load), but if doing so frees a register that allows four other short-lived temporaries to avoid being spilled (saving $4 \times 2 = 8$ memory operations), the net saving is substantial .

Once values are spilled to the stack, a further optimization called **stack slot coloring** can be applied. The "spill live times" (the duration a value is live in memory) can be treated as intervals themselves. If two spill live times do not overlap, they can safely reuse the same memory location on the stack, reducing the total [stack frame](@entry_id:635120) size .

#### Rematerialization

For certain kinds of values, there is a cheaper alternative to spilling: **rematerialization**. A value is **rematerializable** if it can be recomputed more cheaply than storing and reloading it from memory. Classic examples include small integer constants or values computed from always-available base pointers, such as an address calculated by adding a constant offset to the [stack pointer](@entry_id:755333) .

When a rematerializable interval needs to be evicted from a register, the allocator simply discards its value. No store instruction is needed. Before its next use, instead of a load from memory, a sequence of instructions is inserted to recompute the value. The decision of whether to spill or rematerialize is based on a cost model. If the cost of a store and a load ($C_S + C_L$) is greater than the cost of recomputation ($C_M$), rematerialization is preferred . Like splitting, rematerialization creates holes in live intervals, reducing [register pressure](@entry_id:754204) at critical moments.

#### Alternative Spill Heuristics

The "farthest end point" heuristic is not the only option. An alternative and often more precise heuristic is to spill the interval with the **farthest next use**. At a point of [register pressure](@entry_id:754204), the allocator examines the active intervals and the current interval. For each, it finds the program point of its next use. The interval whose next use is furthest in the future is chosen for eviction. This policy is directly inspired by Belady's optimal algorithm for cache replacement and can lead to better spill choices by focusing on near-term register demand rather than the full lifetime of an interval .

### Handling Architectural and ABI Constraints

Real-world architectures and Application Binary Interfaces (ABIs) impose constraints that the register allocator must respect. These are often modeled as **pre-colored intervals**—live intervals that are required to reside in a specific physical register.

A common source of pre-coloring is instructions with fixed register operands. For example, some architectures require the operands for [integer division](@entry_id:154296) or multiplication to be in specific registers (e.g., `EAX` and `EDX` on x86). During the execution of such an instruction, these registers are unavailable for other temporaries. The linear scan allocator must treat these fixed intervals as non-spillable occupants of their registers. If another active interval is already in a pre-colored register when the fixed interval begins, it must be preempted—spilled or split—to honor the architectural constraint .

Another critical source of pre-coloring is the **[calling convention](@entry_id:747093)**, which governs how functions pass arguments and return values. For a call instruction:
- Registers used to pass arguments are pre-colored for the duration of the call setup.
- Registers are designated as either **caller-saved** or **callee-saved**.
  - **Caller-saved** registers may be freely used (clobbered) by the called function (the callee). Any live value in a caller-saved register must be saved to memory (spilled) by the caller before the call and reloaded after.
  - **Callee-saved** registers must be preserved by the callee. A caller can safely store a live value in a callee-saved register across a call without spilling it.

This convention creates a point of very high [register pressure](@entry_id:754204) around call sites. The allocator must identify all variables live across a call. It can place a number of them equal to the count of available [callee-saved registers](@entry_id:747091) into those safe registers. Any remaining live-across variables *must* be spilled to memory. For example, if four variables are live across a call and the ABI provides only two [callee-saved registers](@entry_id:747091), the allocator is forced to generate at least two spill-reload pairs, regardless of its cleverness .

### Comparison with Graph-Coloring Allocation

It is instructive to contrast linear scan with the more traditional graph-coloring approach. A graph-coloring allocator builds a global **[interference graph](@entry_id:750737)**, where nodes are live intervals and an edge connects any two intervals that are simultaneously live. It then attempts to find a coloring of this graph using $R$ colors (registers).

- **Global vs. Local View**: Graph coloring has a global view of all interferences. This allows it to find an optimal, spill-free allocation if the graph is $R$-colorable. Linear scan, by contrast, is a greedy algorithm with a local view. It makes decisions based only on the intervals it has seen so far and the current `active` set. This can lead to suboptimal choices. A simple reordering of independent instructions, which does not change the [interference graph](@entry_id:750737), can change the spill decisions and total spill cost for linear scan, whereas it would have no effect on a graph-coloring allocator . In some cases, linear scan's greedy choices will lead it to a spill, while a graph-coloring allocator, with its global perspective, could have found a spill-free assignment by making a non-local choice earlier in the allocation process .

- **Speed vs. Quality**: The global nature of graph coloring is its strength and its weakness. Building the [interference graph](@entry_id:750737) and attempting to color it can be computationally expensive, often quadratic or worse in the number of live intervals. Linear scan's single pass is nearly linear in the number of intervals, making it orders of magnitude faster.

This trade-off defines their primary use cases. Graph coloring is favored in Ahead-Of-Time (AOT) compilers (like GCC, Clang) where compilation time is less critical than the quality of the generated code. Linear scan is the allocator of choice for Just-In-Time (JIT) compilers (like those in Java's HotSpot JVM or JavaScript's V8 engine), where compilation must be extremely fast to avoid pausing the running application.