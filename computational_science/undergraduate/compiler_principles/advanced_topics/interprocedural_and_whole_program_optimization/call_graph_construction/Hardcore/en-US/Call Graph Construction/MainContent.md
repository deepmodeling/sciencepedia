## Introduction
The [call graph](@entry_id:747097) is a fundamental data structure in computer science, serving as a high-level map of a program's execution flow. It represents all the functions within a program and the potential call relationships between them. For compilers, [program analysis](@entry_id:263641) tools, and software developers, this graph provides indispensable insights, enabling powerful optimizations, sophisticated bug detection, and a deeper understanding of complex software architectures. Without a clear picture of how different parts of a program interact, many advanced analyses would be impossible.

However, constructing a complete and accurate [call graph](@entry_id:747097) for modern software is a significant challenge. While direct function calls are straightforward to identify, features like function pointers, virtual method dispatch in [object-oriented programming](@entry_id:752863), and dynamic code loading introduce [indirect calls](@entry_id:750609) whose targets are not known until runtime. The core problem this article addresses is how [static analysis](@entry_id:755368) can safely and precisely resolve these ambiguities at compile time to build a sound [call graph](@entry_id:747097)—one that accounts for every possible call that could ever occur.

This article provides a comprehensive exploration of [call graph](@entry_id:747097) construction, structured across three chapters. In **Principles and Mechanisms**, you will learn the theoretical underpinnings, including the definition of soundness and the iterative, fixpoint-based framework for building a whole-program graph. We will dissect the key algorithms—from Class Hierarchy Analysis (CHA) and Rapid Type Analysis (RTA) for object-oriented programs to various forms of [points-to analysis](@entry_id:753542) for handling function pointers. Next, **Applications and Interdisciplinary Connections** will demonstrate the immense value of this structure, showing how it drives [compiler optimizations](@entry_id:747548) like [dead code elimination](@entry_id:748246), facilitates architectural analysis in software engineering, and even helps secure emerging technologies like blockchain smart contracts. Finally, **Hands-On Practices** will offer you the chance to solidify your understanding by working through practical exercises and implementation challenges.

## Principles and Mechanisms

The construction of a program's [call graph](@entry_id:747097) is a foundational task in [static analysis](@entry_id:755368), enabling a wide range of [compiler optimizations](@entry_id:747548), program understanding tools, and security analyses. While the concept of a graph representing function calls seems intuitive, the principles governing its construction and the mechanisms required to handle the complexities of modern programming languages are sophisticated. This chapter delineates these principles, starting from the formal definition of a sound [call graph](@entry_id:747097), moving to a unified framework for its construction, and detailing the specific analyses required to resolve different types of calls.

### Fundamental Concepts: The Call Graph and Soundness

Formally, a **[call graph](@entry_id:747097) (CG)** is a [directed graph](@entry_id:265535) $G = (V, E)$, where the set of vertices $V$ represents the procedures (functions or methods) in a program, and the set of directed edges $E \subseteq V \times V$ represents potential calls between these procedures. An edge $(u, v) \in E$ signifies that procedure $u$ may invoke procedure $v$ during some execution of the program.

The critical property of a [call graph](@entry_id:747097) constructed for compiler analysis is **soundness**. An analysis is sound if it is conservative, meaning it may over-approximate the set of actual behaviors but must never under-approximate it. In the context of call graphs, this means the statically constructed graph must account for every call that could possibly occur at runtime. Let $\mathcal{R}$ be the set of all runtime call pairs $(u, v)$ that can ever occur across all possible executions of a program. A [call graph](@entry_id:747097) $G = (V, E)$ is sound if and only if it is a superset of these runtime calls, or more formally, $\mathcal{R} \subseteq E$. 

To understand this principle, consider testing a candidate [call graph](@entry_id:747097) against a set of observed execution traces. Suppose for a program with procedures including `main`, `dispatch`, `C.t`, and `f`, we observe the following runtime calls in different executions:
*   A call from `dispatch` to `C.t`.
*   A recursive call from `f` to `f`.

A sound [call graph](@entry_id:747097) must, at a minimum, contain the edges $(\text{dispatch}, \text{C.t})$ and $(\text{f}, \text{f})$. A proposed graph that omits either of these edges is demonstrably unsound because it fails to account for an observed behavior. Conversely, a graph can be sound even if it contains edges for calls that were not observed in our limited set of traces, or even edges that can never occur at runtime. For example, a graph containing all observed edges plus an additional edge, say $(\text{main}, \text{g})$, is still considered sound with respect to the observed traces, although it may be less precise. . The goal of a good call [graph algorithm](@entry_id:272015) is to be as precise as possible (introducing few spurious edges) while always maintaining soundness.

### A Unified Framework for Call Graph Construction

For any non-trivial program, especially one built from separately compiled modules, constructing a complete and sound [call graph](@entry_id:747097) is not a single-pass process. The discovery of one call path may reveal new reachable code, which in turn may contain further calls to be resolved. This iterative process is best understood through the lens of [dataflow analysis](@entry_id:748179) and [fixpoint iteration](@entry_id:749443). 

Imagine a system built from multiple translation units, $C_1, \dots, C_n$. A compiler can first perform a local analysis on each unit to produce a summary $S_i$. This summary would contain the functions defined in $C_i$ and the direct calls between them. However, it would also contain unresolved indirect call sites (like calls via function pointers). The challenge is to combine these summaries to build a whole-program [call graph](@entry_id:747097).

We can formalize this as a **[fixpoint iteration](@entry_id:749443)**:
1.  **The Lattice:** We define a [partially ordered set](@entry_id:155002) of call graphs. Given two graphs $G_1 = (V_1, E_1)$ and $G_2 = (V_2, E_2)$, we say $G_1 \preceq G_2$ if $V_1 \subseteq V_2$ and $E_1 \subseteq E_2$. This structure, known as a lattice, has a [least element](@entry_id:265018) $\bot = (\varnothing, \varnothing)$, representing an [empty graph](@entry_id:262462).

2.  **Initialization:** We initialize our global [call graph](@entry_id:747097) $G$ to $\bot$, or perhaps to a graph containing only the program's entry point (e.g., `main`) and any direct calls immediately visible.

3.  **Iteration:** We iteratively process the summaries $S_i$ and update the global graph $G$. In each step, we resolve the calls in a summary $S_i$ against the currently known functions in $G$. For example, if $S_i$ contains an indirect call site that requires a function of a certain type, we add edges from the caller to *all* functions currently in $G$ that match this type. The result is a new set of edges (and potentially new functions) which are then merged into $G$.

4.  **The Merge Operator:** The merge operator, or **[least upper bound](@entry_id:142911) ($\sqcup$)**, combines the information from the current graph $G_k$ and the newly derived graph $H$ from a summary. For this lattice, the operator is simply the component-wise union: $G_{k+1} = G_k \sqcup H = (V_k \cup V_H, E_k \cup E_H)$. This operation is monotonic and inflationary—it only ever adds functions and edges, never removes them.

5.  **Convergence:** Because the total set of functions and possible edges in a program is finite, this inflationary process is guaranteed to terminate. It reaches a **fixpoint** where an iteration over all summaries produces no new functions or edges. The final graph $G^\star$ is the least fixpoint, representing a sound over-approximation of all possible runtime calls. This iterative process, regardless of the order in which summaries are processed (a "chaotic iteration"), is guaranteed to converge to the same sound result. 

This framework provides the theoretical foundation for [call graph](@entry_id:747097) construction. The core "mechanism" of the algorithm lies in the procedure for resolving calls within each iteration.

### Resolving Call Edges: From Direct to Indirect Calls

The edges of a [call graph](@entry_id:747097) can be partitioned into two categories: direct calls and [indirect calls](@entry_id:750609). 

#### Direct Calls

A **direct call** is the simplest case, where the name of the callee is specified syntactically at the call site (e.g., `log();`). These calls can be identified by a simple traversal of the program's [abstract syntax tree](@entry_id:633958) or [intermediate representation](@entry_id:750746). The set of direct calls, $E_{\text{direct}}$, typically forms the initial seed of the [call graph](@entry_id:747097) in the [fixpoint iteration](@entry_id:749443) process.

#### Indirect Calls

An **indirect call** occurs when the target procedure is determined at runtime, typically through a variable such as a function pointer or an object reference. For example, a call like `p()` or `s->m()` is indirect. Resolving these calls requires [static analysis](@entry_id:755368) to determine the set of all possible concrete functions the variable could refer to at that program point.

##### Dynamic Dispatch in Object-Oriented Programs

In object-oriented languages, virtual method calls (`s->m()`) are a primary source of [indirect calls](@entry_id:750609). The concrete method body executed depends on the dynamic type of the receiver object `s`. Static analysis must conservatively determine the set of all possible dynamic types for `s`.

A foundational algorithm for this is **Class Hierarchy Analysis (CHA)**. Given a [virtual call](@entry_id:756512) on a receiver object with a static type $T$, CHA identifies the set of possible targets by inspecting the program's entire class hierarchy. The algorithm includes an edge to the implementation of the method in every concrete (instantiable) class that is a subtype of $T$. 

For example, consider a call site `o.m()` where `o` has the static type of an interface `I`. CHA proceeds by:
1.  Identifying all concrete classes in the program that implement `I` (either directly or by inheriting from a class that implements `I`).
2.  For each such concrete class, determining which specific method body for `m` would be invoked (its own override, or one inherited from a superclass).
3.  Adding an edge from the call site to each distinct method body found.

The precision of CHA is limited because the static type can be very general. If the static type is a high-level abstract class or interface, CHA may include many targets, some of which may correspond to classes that are never actually used. 

To improve precision, **Rapid Type Analysis (RTA)** refines the results of CHA. RTA performs a preliminary [reachability](@entry_id:271693) analysis to identify the set of all concrete classes that are actually instantiated in reachable code (the `Types_seen` set). It then intersects the target set produced by CHA with the methods belonging to classes in `Types_seen`. This prunes away targets from classes that are declared but never instantiated, or are only instantiated in [unreachable code](@entry_id:756339).  For instance, if the class hierarchy includes a `Square` class, but the only reachable code instantiates `Circle` objects, RTA would correctly exclude `Square.m` as a possible target of a [virtual call](@entry_id:756512), whereas CHA would have included it. 

##### Function Pointer Calls and Points-To Analysis

In languages like C and C++, function pointers are another major source of [indirect calls](@entry_id:750609). To resolve a call like `p(x)`, the compiler must determine what functions `p` can point to. This is the domain of **Points-To Analysis (PTA)**, also known as [pointer analysis](@entry_id:753541). PTA aims to compute, for each pointer variable, a *points-to set*—the set of memory locations or functions it might point to.

Points-to analyses exist along several dimensions of precision, which trade off accuracy for computational cost.

*   **Flow-Sensitivity:** A **flow-insensitive** analysis ignores the order of statements in the program. It computes a single points-to set for each variable, which is the union of all possible targets assigned to it anywhere in the procedure (or program). For example, if a pointer `p` is assigned `` in one branch of an `if` statement and `` in the other, a flow-insensitive analysis will determine that `p` can point to either `h` or `g` at *all* subsequent call sites using `p`.  

    In contrast, a **flow-sensitive** analysis tracks the points-to set for each variable at each program point, respecting the control flow. An assignment to a pointer `p := ` *kills* its previous points-to set and replaces it with `{f1}`. At points where control flow merges (e.g., after an `if-else` block), the points-to sets from the incoming branches are unioned. This additional precision can drastically reduce the size of the points-to sets at specific call sites, resulting in a much more precise [call graph](@entry_id:747097). For example, if `p` is assigned ``, then used, then reassigned `` and used again, a [flow-sensitive analysis](@entry_id:749460) will resolve the first call to `{f1}` and the second to `{f2}`, while a flow-insensitive analysis would resolve both to `{f1, f2}`. 

*   **Context-Sensitivity:** When analyzing calls between procedures, a **context-insensitive** analysis creates a single summary for each procedure that merges the effects from all its call sites. If a function `applier(f)` is called with pointer `p1` at one site and `p2` at another, the points-to set of the formal parameter `f` inside `applier` becomes the union of the points-to sets of `p1` and `p2`. Consequently, any indirect call via `f` inside `applier` is resolved to this merged, and potentially imprecise, set. . A [context-sensitive analysis](@entry_id:747793) would analyze `applier` separately for each call site (or calling context), maintaining a more precise mapping between actual and formal parameters, at a significantly higher analysis cost.

### The Call Graph in a Compiler Pipeline

The [call graph](@entry_id:747097) is not a static artifact. It evolves as the compiler applies transformations to the program's Intermediate Representation (IR). The graph built from the source code, $G_{\text{src}}$, may differ significantly from the graph of the optimized IR, $G_{\text{IR}}$. 

Several standard transformations have predictable effects on the [call graph](@entry_id:747097):
*   **Inlining:** When a call from `f` to `g` is inlined, the body of `g` is inserted into `f`, and the call edge $(f, g)$ is removed. If `g` is inlined at all of its call sites, its standalone procedure body may become dead code and be eliminated entirely. In this case, the node for `g` and all its associated edges may disappear from the graph.
*   **Cloning and Specialization:** A single [source function](@entry_id:161358) `f` may be duplicated into multiple specialized versions in the IR (e.g., `f_int`, `f_float`). This means one node in $V_{\text{src}}$ can map to multiple nodes in $V_{\text{IR}}$. However, these IR clones originate from distinct source functions and remain distinct; the IR clones of `f` are disjoint from the IR clones of a different [source function](@entry_id:161358) `g`.
*   **Outlining:** A compiler may identify a repeated region of code within a function `f` and extract it into a new, compiler-generated helper function, say `f_helper`. It then replaces the original code regions with direct calls to this new function. This creates a new node `f_helper` and new edges $(f, f_{\text{helper}})$ in $G_{\text{IR}}$ that have no direct counterpart in $G_{\text{src}}$.

Crucially, standard optimizations are designed not to create new, arbitrary calling relationships between user functions. An IR-level call from a procedure derived from [source function](@entry_id:161358) `f` to one derived from `g` can typically only exist if there was a corresponding call in the original source code, $(f, g) \in E_{\text{src}}$. 

### Advanced Topics and Practical Considerations

#### May-Call vs. Must-Call Analysis

The standard [call graph](@entry_id:747097) described thus far is a **[may-call graph](@entry_id:751783)**: an edge $(u, v)$ means `u` *may* call `v`. This over-approximation is essential for correctness-critical (safety) optimizations. For example, to safely devirtualize a [virtual call](@entry_id:756512), the compiler must know the complete set of all *possible* targets. Using an incomplete set would be an unsound optimization that breaks the program's semantics. 

A different but related analysis produces a **must-[call graph](@entry_id:747097)**. An edge $(u, v)$ in a must-[call graph](@entry_id:747097) means that on *every* possible execution of `u`, a call to `v` is guaranteed to occur. This information is an under-approximation of calling behavior. By definition, the set of must-call edges is a subset of the may-call edges, $E_{\text{must}} \subseteq E_{\text{may}}$.

Must-call information is not suitable for safety checks (as it misses possible calls), but it is invaluable for **profitability analysis**. An optimization like inlining carries a cost (e.g., increased code size). A compiler is more likely to apply an expensive optimization to a call edge $(u, v)$ if it knows the call is guaranteed to execute, because the performance benefit will be reliably realized. An edge that is only in the [may-call graph](@entry_id:751783) might be on a "cold" path that is rarely or never executed, making the optimization a poor trade-off. 

#### Handling Unresolvable Calls

In some cases, [static analysis](@entry_id:755368) may be fundamentally unable to determine the target of a call. A classic example is dynamic loading, where a function is looked up by a string name computed at runtime (e.g., via `dlsym` or a similar mechanism). If the string's value cannot be determined at compile time, what is the sound strategy? 

The most conservative and sound approach relies on a **closed-world assumption**: the analysis assumes that the dynamically loaded function must come from a known, finite set of libraries bundled with the application. Under this assumption, the analysis adds edges from the call site to *every* function in the bundled libraries that has a type signature compatible with the call site. While this can be very imprecise, it maintains soundness.

An alternative sound strategy is to transform the program to make it more analyzable. For instance, the compiler could insert a runtime guard that checks the computed string name against a predefined whitelist of allowed function names. The static analyzer can then use this whitelist to create a precise and sound set of target edges for the transformed program.  Approaches that are not exhaustive, such as relying on profiling data from production logs to guess the most likely targets, are fundamentally unsound as they cannot guarantee coverage for all possible executions.