## Introduction
In the quest for maximum performance, optimizing compilers employ a sophisticated arsenal of techniques to transform source code into highly efficient machine instructions. While simple optimizations can remove obviously redundant work, a more subtle and common challenge arises from computations that are repeated on some, but not all, execution paths. This phenomenon, known as partial redundancy, represents a significant missed opportunity for performance improvement. How can a compiler safely and profitably eliminate these partially redundant operations without altering program behavior?

This article delves into Partial Redundancy Elimination (PRE), a powerful and unifying optimization that directly addresses this problem. Across the following chapters, you will gain a deep understanding of this cornerstone of compiler design. The first chapter, **Principles and Mechanisms**, will dissect the core data-flow analyses, such as availability and anticipatability, that govern [safe code motion](@entry_id:754483). Next, **Applications and Interdisciplinary Connections** will explore how PRE is used in practice—from foundational loop optimizations to its conceptual analogues in hardware design and [distributed systems](@entry_id:268208). Finally, **Hands-On Practices** will challenge you to apply these concepts to concrete problems, solidifying your knowledge. We begin by examining the fundamental principles that allow compilers to turn partial redundancies into fully eliminable ones.

## Principles and Mechanisms

Partial Redundancy Elimination (PRE) is a powerful [compiler optimization](@entry_id:636184) that aims to remove computations that are redundant along some, but not necessarily all, execution paths. It is a form of [code motion](@entry_id:747440) that generalizes and unifies two more traditional optimizations: [common subexpression elimination](@entry_id:747511) (which handles fully redundant computations) and [loop-invariant code motion](@entry_id:751465). The core idea of PRE is to transform partial redundancies into full redundancies, which can then be safely and profitably eliminated. This chapter details the fundamental principles and data-flow mechanisms that underpin this sophisticated optimization.

### Defining Redundancy: From Full to Partial

At its heart, PRE deals with the efficient evaluation of expressions. An expression is considered **fully redundant** at a program point if its value has already been computed on every possible path leading to that point, and the operands of the expression have not been modified since that computation. A simple [common subexpression elimination](@entry_id:747511) pass can identify and remove such computations.

However, a more common scenario is **partial redundancy**. An expression is partially redundant if it is computed on some, but not all, paths leading to a point where it is re-evaluated. Consider a classic diamond-shaped [control-flow graph](@entry_id:747825) where block $B_1$ branches to two blocks, $B_2$ and $B_3$, which later merge at a join block $B_4$. If an expression, say $x+y$, is computed in $B_2$ and also in $B_4$, then along the path $B_1 \to B_2 \to B_4$, the computation in $B_4$ is redundant. However, along the path $B_1 \to B_3 \to B_4$ (assuming $B_3$ does not compute $x+y$), the computation in $B_4$ is necessary. PRE seeks to resolve this inefficiency by inserting a computation of $x+y$ on the "deficient" path (i.e., the path through $B_3$) to make the computation in $B_4$ fully redundant, and thus, removable.

### Core Data-Flow Properties for Safe Code Motion

To move code without altering program semantics, PRE relies on rigorous [data-flow analysis](@entry_id:638006). Two key properties, **availability** and **anticipatability**, govern where expressions can be moved and eliminated.

#### Availability

An expression $e$ is **available** at a program point $p$ if, along every path from the program's entry to $p$, the expression $e$ has been computed, and none of its operands have been redefined since the last computation. Availability is a "forward" data-flow property. If an expression is available at the entry to a block, we know its value has already been computed and is ready for use. This property is central to identifying full redundancy.

#### Anticipatability (Down-Safety)

The safety of hoisting a computation—moving it to an earlier point in the program—is governed by **anticipatability**, also known as **anticipation** or **down-safety**. An expression $e$ is **anticipatable** (or down-safe) at a program point $p$ if, along every path starting from $p$ to the program's exit, the expression $e$ will be computed before any of its operands are redefined.

Anticipatability is a "backward" data-flow property. It ensures that inserting a computation at point $p$ is not "in vain"; the computed value will be used downstream on all subsequent paths. More importantly, it guarantees that hoisting the computation does not introduce a new, speculative evaluation on a path that would not have originally computed it. This prevents the introduction of spurious exceptions (e.g., from division by zero) and ensures the optimization is behaviorally conservative.

The critical role of anticipatability is illustrated by considering an expression whose operands are modified along some paths [@problem_id:3661891]. Imagine a function `hash(z)` where the operand $z$ may be redefined. Let's analyze two expressions, `hash(x)` and `hash(y)`, in a CFG where block $B_0$ branches to $B_1$ and $B_2$, which then join.
- Suppose `hash(x)` is computed in both $B_1$ and $B_2$, and the operand $x$ is not redefined in either block. At the exit of $B_0$, `hash(x)` is anticipatable because on both outgoing paths, it is guaranteed to be computed before any redefinition of $x$. It is therefore safe to hoist the computation of `hash(x)` to $B_0$.
- Now, suppose `hash(y)` is computed in $B_1$, but in block $B_2$, the operand $y$ is redefined (`y := y + 1`) before a later use of `hash(y)` at the join point. At the exit of $B_0$, `hash(y)` is *not* anticipatable. Along the path through $B_2$, its operand $y$ is redefined. Hoisting a computation of `hash(y)` to $B_0$ would use the *old* value of $y$. This hoisted value would be incorrect for the use after the redefinition in $B_2$. The redefinition of $y$ effectively "kills" the value of `hash(y)` computed with the old operand, making the hoisting unsafe.

### The PRE Transformation in Practice

The PRE algorithm conceptually involves three main phases:
1.  **Data-Flow Analysis**: The compiler performs forward and backward data-flow analyses to compute properties like availability and anticipatability for all expressions at all program points.
2.  **Transformation Decision**: Based on the analysis, the compiler identifies insertion points for expressions to make them fully available at later points of use. These insertions are placed at the earliest points that are safe (the expression is anticipatable) and profitable.
3.  **Code Rewriting**: The program is rewritten by inserting the new computations (typically into temporary variables) and replacing the now fully redundant computations with uses of these temporaries.

Let's walk through a concrete example [@problem_id:3661929]. Consider a diamond CFG with blocks $B_1, B_2, B_3, B_4$. The expression $e = x+y$ is computed multiple times.
- In block $B_2$: $t := x+y$ (Occ. 1), followed by $u := x+y$ (Occ. 2). Then $x$ is redefined: $x := h(x)$.
- In block $B_3$: $p := x+y$ (Occ. 4), followed by $q := x+y$ (Occ. 5). Then $y$ is redefined: $y := k(y)$.
- In block $B_4$ (the join point): $w := x+y$ (Occ. 7).

The computations of $x+y$ in $B_2$ and $B_3$ are partially redundant. Data-flow analysis will determine that $x+y$ is anticipatable at the exit of $B_1$, as both outgoing paths ($B_1 \to B_2$ and $B_1 \to B_3$) lead to a computation of $x+y$ before any of its operands are redefined. Therefore, the end of $B_1$ is an earliest safe insertion point.

The transformation proceeds as follows:
1.  **Insertion**: A new computation `r := x + y` is inserted at the end of block $B_1$, before the conditional branch.
2.  **Replacement**: We can now replace any subsequent occurrences of $x+y$ with the temporary variable $r$, but only where the value of $x+y$ is guaranteed to be identical to $r$.
    - Occurrences 1 and 2 in $B_2$ can be replaced with $r$, as neither $x$ nor $y$ has been redefined on the path from the insertion of `r` to these uses.
    - Occurrences 4 and 5 in $B_3$ can also be replaced with $r$ for the same reason.
    - After the redefinition $x := h(x)$ in $B_2$, the value of $x+y$ changes. Thus, any later occurrences on this path cannot be replaced by $r$.
    - Similarly, after the redefinition $y := k(y)$ in $B_3$, the value of $x+y$ changes.
    - At the join block $B_4$, the value of $x+y$ is not equal to $r$ on *any* incoming path due to the intervening redefinitions in both $B_2$ and $B_3$. Therefore, occurrence 7 cannot be replaced.

This example demonstrates how PRE carefully tracks the liveness and modification of operands to ensure [semantic equivalence](@entry_id:754673).

### PRE Strategies: Eager vs. Lazy Code Motion

The placement of new computations is not unique. Different PRE algorithms employ different strategies, primarily categorized as "eager" or "lazy."

-   **Eager PRE** hoists computations to the earliest possible safe program points. While this maximizes the region where the expression is available, it can lead to unnecessarily long live ranges for the temporary variables, which may increase [register pressure](@entry_id:754204).

-   **Lazy PRE** (or [lazy code motion](@entry_id:751190)) places computations as late as possible. A computation is only moved as early as necessary to be available on all paths leading to a join point where it can be eliminated. This strategy is often preferred because it tends to keep live ranges short. In a scenario with nested conditionals where an expression is computed on some but not all paths, a lazy approach may "sink" the computations to a common join block rather than hoisting it high up in the CFG [@problem_id:3661875]. The final placement in a lazy scheme often occurs at the latest possible point that still captures the full benefit of eliminating downstream redundancies.

### Advanced Considerations and Practical Constraints

Real-world compilers must handle complexities that go beyond simple arithmetic expressions. The principles of PRE extend to these cases, but require more sophisticated analysis.

#### PRE in Static Single Assignment (SSA) Form

Modern compilers almost universally use an [intermediate representation](@entry_id:750746) called **Static Single Assignment (SSA) form**, where each variable is assigned exactly once. In SSA, PRE is often implemented as part of a more general algorithm called Global Value Numbering (GVN).

In SSA, merging values from different control-flow paths is handled explicitly by $\phi$-functions. If an expression is computed on multiple predecessor paths, PRE can be elegantly achieved by creating a $\phi$-function for the *result* of the expression. For instance, if path $B_1$ computes $e_1 = x_1 \times y_0$ and path $B_2$ computes $e_2 = x_0 \times y_2$, and a join block $B_3$ redundantly computes $x_3 \times y_3$ (where $x_3=\phi(x_1, x_0)$ and $y_3=\phi(y_0, y_2)$), the PRE/GVN transformation can replace the multiplication in $B_3$ with a simple merge: $e_3 = \phi(e_1, e_2)$ [@problem_id:3661877]. This directly eliminates the re-computation at the join point.

#### Handling Memory Operations and Aliasing

Applying PRE to memory accesses (loads) is far more complex than for scalar variables. The value of a load from memory, such as `arr[i]`, can be affected by any store to memory. Hoisting a load is only safe if it does not move past a store operation that might modify the same memory location.

This requires a sophisticated **alias analysis**. To hoist a load `arr[j]` past a store `arr[k] := h`, the compiler must prove that `arr[j]` and `arr[k]` cannot refer to the same memory location (i.e., they do not alias). If alias analysis determines that `k` and `j` *may-alias*, hoisting the load is unsafe and forbidden, as it would change the value read by `arr[j]` from the post-store value to the pre-store value [@problem_id:3661807]. Conversely, if analysis can prove that `i` and `j` *must-alias* (i.e., `i=j`), it can perform an additional optimization: hoist a single load of `arr[i]` and reuse its result for all accesses to both `arr[i]` and `arr[j]`.

#### Handling Side Effects and Trapping Instructions

The validity of PRE is strictly limited to **pure computations**—those that have no observable side effects beyond returning a value. A function call like `g(z)` can be treated as an expression and hoisted if `g` is pure. However, if `g` has side effects, such as performing I/O, modifying a global variable, or appending to a log, hoisting it is illegal [@problem_id:3661844]. A PRE transformation that reduces the number of calls to a side-effecting function would change the program's observable behavior, which violates the fundamental contract of optimization.

Similarly, instructions that can trap or raise exceptions, such as division (which traps on a [zero divisor](@entry_id:148649)), require special handling. A purely safe PRE algorithm based on anticipatability will not move a potentially trapping instruction to a location where it would execute on a path that did not originally contain it. More aggressive **speculative PRE** may hoist such an instruction, but it must be accompanied by a "guard" that preserves the original control-flow conditions, ensuring the exception semantics are unchanged.

### The Profitability of PRE: A Cost-Benefit Analysis

A transformation that is semantically safe is not always profitable. An [optimizing compiler](@entry_id:752992) must use a cost model to decide whether applying PRE will actually improve the final program. This decision involves trade-offs between instruction count, [register pressure](@entry_id:754204), and code size.

#### Register Pressure

One of the most significant costs of PRE is increased **[register pressure](@entry_id:754204)**. By hoisting a computation, PRE creates a new temporary variable whose [live range](@entry_id:751371) may span multiple basic blocks. If the number of simultaneously live variables in a region exceeds the number of available physical registers, the register allocator must "spill" some variables to memory, incurring high-cost store and load operations. A sophisticated PRE implementation will estimate the impact on [register pressure](@entry_id:754204). It may choose not to perform an otherwise safe transformation if the predicted cost of spilling outweighs the savings from eliminating the redundant computation [@problem_id:3661819]. For example, saving one cycle by eliminating an addition is a poor trade-off if it causes an 8-cycle spill and reload on a frequently executed path.

#### Code Size

In some cases, PRE can increase the overall code size. This is particularly true when enabling the optimization requires inserting complex or guarded code in multiple predecessor blocks. A size-aware heuristic might weigh the size of the code being eliminated against the size of the code being inserted. For instance, if eliminating $r$ occurrences of an expression (size $s_e$) requires inserting a guarded expression (size $s_e + s_g$) into each of $k$ predecessors, the transformation should only proceed if the code size does not increase, i.e., if $k \cdot (s_e + s_g) \le r \cdot s_e$ [@problem_id:3661906]. This is especially important for embedded systems or applications where code footprint is a critical constraint.

In summary, Partial Redundancy Elimination is a cornerstone of modern [compiler optimization](@entry_id:636184). It is a testament to the power of [data-flow analysis](@entry_id:638006), enabling compilers to restructure code for greater efficiency. However, its application is not a simple matter of [pattern matching](@entry_id:137990). It requires a deep and principled analysis of program semantics—from data dependencies and aliasing to side effects and exceptions—coupled with a pragmatic, cost-aware model to ensure that every transformation is both safe and genuinely profitable.