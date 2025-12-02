## Introduction
How can we predict what a computer program will do without ever running it? This is the central challenge of [static program analysis](@entry_id:755375). With potentially trillions of execution paths depending on user input, verifying a program's correctness or security seems like an impossible task. To make this tractable, analysts adopt one of two fundamental philosophies: seeking absolute certainty about what *must* be true on all paths, or cataloging the universe of what *may* happen on at least one path. This article focuses on the latter approach, known as **may analysis**. It addresses the knowledge gap of how we can reason about program behavior reliably in the face of uncertainty.

This article provides a comprehensive overview of this powerful concept. First, in "Principles and Mechanisms," we will dissect the core ideas of may analysis, including the crucial strategy of over-approximation that makes it a sound tool for bug finding and the trade-offs that lead to analytical imprecision. Following this, the "Applications and Interdisciplinary Connections" section will demonstrate how these principles are applied in the real world, from enabling [compiler optimizations](@entry_id:747548) and ensuring [system stability](@entry_id:148296) to uncovering critical security vulnerabilities, revealing the profound impact of reasoning about possibility.

## Principles and Mechanisms

### The Fortune Teller's Dilemma: Certainty vs. Possibility

Imagine a computer program not as a static block of text, but as a dynamic journey with a multitude of branching paths. A simple `if` statement is a fork in the road; a loop is a path that can be traveled many times. Given that a program might take trillions of different paths depending on its inputs, how can we possibly say anything definitive about its behavior without running it for an eternity? This is the fundamental challenge of **[static program analysis](@entry_id:755375)**: to predict a program's behavior without actually executing it.

Faced with this infinite landscape of possibilities, we can adopt two distinct philosophies, much like an ancient oracle might. We can either seek **certainty** or we can catalog **possibility**.

The first approach, the path of certainty, asks: "What *must* be true, no matter what path the program takes?" This is the world of **must analysis**. It searches for universal, inescapable truths. For example, if we have a variable `x` initialized to 5, and no code can ever change it, a must analysis can confidently state: "$x$ is always 5." If, however, an `if` statement could potentially change `x` to 10, the analysis loses its certainty. It can no longer claim $x$ *must* be 5.

The second approach, the path of possibility, asks a different question: "What *may* happen on at least one of the program's journeys?" This is the essence of **may analysis**. It doesn't need a guarantee; it's interested in what *could* be. In the same example, if `x` starts at 5 and an `if` block can change it to 10, a may analysis would conclude: "At the end of the program, `x` may be 5, or it may be 10." It embraces the uncertainty and reports the full range of [potential outcomes](@entry_id:753644).

This distinction is not just academic; it is the cornerstone of making computers reliable and efficient.

### The Art of Safe Over-Approximation

Let's consider one of the most important jobs for a static analyzer: finding bugs. A very common and dangerous bug is dereferencing a **null pointer**, which typically causes a program to crash. Our question to the analyzer is: "*May* this pointer be null when it is used?" This is a classic "may" question.

Now, what does it mean for such an analyzer to be **sound**, or correct? For bug finding, soundness means one thing above all: **it must never miss a real bug**. We can tolerate the analyzer crying wolf occasionally (a **[false positive](@entry_id:635878)**), but we can never allow it to give us a clean bill of health when a bug is lurking (a **false negative**).

To achieve this guarantee, may analysis employs a powerful strategy: **over-approximation**. It systematically casts a wider net than the program's actual behavior requires. The fundamental rule is that the set of all true, concrete behaviors of the program must be a subset of the possibilities reported by the analysis. If the analysis says a variable `v` can have a value in the set `S`, then any real value `v` takes on during execution *must* be in `S`.

A beautiful illustration of this principle comes from analyzing a simple program structure [@problem_id:3619092]. Imagine a pointer `p` that is set to `null` down one branch of an `if` statement and set to a valid memory address down the other. When the two paths merge, what do we know about `p`?

- A **may analysis**, tasked with finding potential null dereferences, must consider both possibilities. At the merge point, its conclusion is that `p` *may* be `null`. Its abstract state for `p` becomes `⊤` (pronounced "top"), a special value meaning "it could be anything" or, more precisely, "it could be null, or it could be non-null." If the program then tries to use `p`, the may analysis will raise a warning. It has successfully identified a potential crash.

- A **must analysis**, in contrast, seeks certainty. At the merge point, it sees that on one path `p` is `null` and on the other it is `non-null`. Since there is no property that holds on *all* paths, it concludes it knows nothing certain. Its state becomes `⊥` (pronounced "bottom"), meaning "no information" or "unreachable." It would fail to raise a warning, thereby missing a definite bug.

This demonstrates the crucial trade-off: may analysis finds all possible bugs at the cost of sometimes flagging safe code, whereas must analysis is unsound for bug hunting because its quest for certainty makes it blind to problems that only occur on some paths [@problem_id:3619092]. This principle of collecting all possibilities extends to many areas, such as security. In **taint analysis**, to determine if a sensitive variable *may* be influenced by untrusted user input, the analyzer must use union (`∪`) at every merge point, gathering all variables that were tainted on *any* incoming path [@problem_id:3642674].

### The Conservative Optimizer: When "May" Means "Don't Touch"

The roles reverse dramatically when we switch from finding bugs to optimizing code. A compiler **optimizer**'s goal is to rewrite a program to make it run faster, but its primary directive is equivalent to the Hippocratic Oath: "First, do no harm." An optimization is only safe if it is guaranteed not to change the program's behavior.

Consider an optimization called **Dead Store Elimination (DSE)**. If we have an instruction `x := 42` but the value of `x` is never read again, the instruction is "dead" and can be safely removed. To make this decision, the optimizer must ask: "*May* the value of `x` from this instruction be used on any future path?" This is a **[liveness analysis](@entry_id:751368)**.

Here, being "conservative" means retaining the instruction if there is any doubt. The optimizer must assume the worst-case scenario to preserve correctness. A may analysis is precisely what's needed. If it reports that `x` *may* be live (used in the future), the optimizer conservatively keeps the instruction [@problem_id:3635637].

This has profound economic consequences in modern processors that can execute instructions out of order. Consider scheduling two memory operations: a store `*p = a` and a load `b = *q` [@problem_id:3647173]. Can the processor execute the load before the store to improve performance? The answer depends on whether `p` and `q` could possibly point to the same memory location. The processor must ask an **alias analysis** unit: "*May* `p` and `q` be aliases?" If the answer is "yes," the processor must conservatively execute them in their original order. A precise analysis that can prove they are *not* aliases unlocks greater parallelism. In one simple scenario, an imprecise may-alias result reduced the number of valid, high-performance schedules from 40 down to 15, a significant loss of opportunity. This pressure drives the demand for ever more precise static analyses.

### Where Does Imprecision Come From?

We've established that may analysis is a sound strategy for finding bugs and enabling safe optimizations, but its over-approximations can lead to [false positives](@entry_id:197064). Where does this imprecision—this gap between what the analysis reports and what is concretely true—come from? It arises from several sources of abstraction.

#### Source 1: The Shape of Abstraction

The first source of imprecision is the very nature of the abstract values we use. Imagine a program where a variable `x` is set to `0` on one path and `2` on another. After the paths merge, the set of concrete, possible values for `x` is exactly $\{0, 2\}$.

Now, suppose we use a popular, simple abstract domain called **intervals**. This domain can only represent a continuous range of numbers, like `[a, b]`. To over-approximate the set $\{0, 2\}$, the smallest interval that contains both values is `[0, 2]`. The analysis now believes `x` could be 0, 1, or 2. The value `1` is a "ghost"—a false positive introduced because the interval domain is not expressive enough to represent a set with a hole in it [@problem_id:3635651]. This is a classic trade-off: intervals are computationally cheap, but they sacrifice precision.

#### Source 2: Forgetting Relationships

Another critical source of imprecision is when an analysis treats each variable independently, forgetting the relationships between them. Consider this code: starting with `x` and `y` being equal, we execute `x := x + 1` followed by `y := y + 1`. At the end, will `x` still equal `y`? Of course. The invariant $x - y = 0$ is maintained.

A simple **non-relational** analysis, like the intervals domain, tracks `x` and `y` separately. If it starts knowing only that $x=y$, it might abstract this to $x \in [-\infty, \infty]$ and $y \in [-\infty, \infty]$. The crucial link between them is immediately lost. After the increments, it still knows nothing about their relationship and cannot prove that the assertion `assert(x == y)` is safe [@problem_id:3619168].

A more powerful, and more expensive, **relational domain** like **convex [polyhedra](@entry_id:637910)** or **octagons** can handle this. It can represent the initial state as the linear constraint $x - y = 0$. It can then prove that this invariant is transformed into $x - y = 1$ after the first increment, and back to $x - y = 0$ after the second, thus proving the assertion is safe [@problem_id:3619168]. This reveals a fundamental spectrum in [program analysis](@entry_id:263641): a deep trade-off between the computational **cost** of an analysis and the **precision** of its results.

#### Source 3: The Act of Merging

Perhaps the most subtle source of imprecision lies in the very algorithm used by analyzers. The theoretically "perfect" analysis would trace every possible execution path separately—a technique known as the **Meet Over all Paths (MOP)** solution. But since the number of paths can be infinite, this is computationally impossible.

Practical analyzers use an iterative algorithm that approximates this, known as the **Maximum Fixed Point (MFP)** solution. Its key shortcut is that whenever paths merge, it combines their abstract states *first* and then applies the next transformation to the merged state. This shortcut is the source of the classic `may` analysis imprecision.

Imagine a transfer function `f` at a node `j` that only produces a special fact `a` if it sees facts `c` and `d` *at the same time*: $f^{\star}(S) = \{a\}$ if $\{c, d\} \subseteq S$, and $\varnothing$ otherwise. Now, suppose two paths merge at `j`: one path brings the fact `c`, and the other brings `d` [@problem_id:3642725].

- The practical MFP algorithm merges first: it computes the input to `j` as $\{c\} \cup \{d\} = \{c,d\}$. Then it applies the function: $f^{\star}(\{c,d\}) = \{a\}$. The result is `a`.
- The ideal MOP semantics considers each path separately: on the first path, the result is $f^{\star}(\{c\}) = \varnothing$. On the second, $f^{\star}(\{d\}) = \varnothing$. The union of these results is $\varnothing \cup \varnothing = \varnothing$.

The practical algorithm yields a larger, less precise result. This happens because the function is **non-distributive**: applying the function to the union of inputs is not the same as taking the union of the function applied to each input. This elegant mathematical property underpins why the approximations we make in [static analysis](@entry_id:755368) are both necessary and fundamentally imperfect, yet in a well-defined and safe way. May analysis, in its many forms, is a testament to the power of abstraction, allowing us to reason soundly about the infinite complexities of computation.