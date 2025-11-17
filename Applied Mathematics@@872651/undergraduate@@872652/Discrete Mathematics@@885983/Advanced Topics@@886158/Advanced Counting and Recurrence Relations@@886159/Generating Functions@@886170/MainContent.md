## Introduction
Generating functions represent one of the most powerful tools in enumerative [combinatorics](@entry_id:144343), providing a remarkable bridge between the discrete world of counting and the continuous world of analysis. They offer a systematic method for solving a vast array of problems that can seem intractable by direct combinatorial arguments, from counting constrained arrangements to solving complex recurrence relations. This article addresses the challenge of analyzing discrete structures by translating them into the language of algebra and calculus. Over the next chapters, you will gain a comprehensive understanding of this versatile technique. The journey begins with **Principles and Mechanisms**, where we will build generating functions from the ground up, learning the core rules and advanced techniques for their construction and manipulation. Next, in **Applications and Interdisciplinary Connections**, we will see how these tools are deployed across diverse fields like computer science, probability, and physics, revealing their unifying power. Finally, the **Hands-On Practices** section will allow you to solidify your knowledge by applying these principles to solve challenging, practical problems.

## Principles and Mechanisms

Generating functions provide a powerful and versatile bridge between [discrete mathematics](@entry_id:149963) and continuous analysis. They encode an infinite sequence of numbers, which typically represent the solution to a counting problem for each integer $n$, into a single function. By manipulating these functions algebraically, we can solve complex combinatorial problems that are often intractable by other means. This chapter explores the fundamental principles governing the construction and manipulation of generating functions and the core mechanisms through which they are applied.

### The Ordinary Generating Function: An Algebraic Representation of Choice

At its core, a [generating function](@entry_id:152704) is a formal power series used to model choices in a combinatorial construction. For a sequence of numbers $(a_n)_{n \ge 0} = (a_0, a_1, a_2, \ldots)$, its **ordinary [generating function](@entry_id:152704) (OGF)** is defined as the formal power series:

$$
A(x) = \sum_{n=0}^{\infty} a_n x^n = a_0 + a_1 x + a_2 x^2 + \cdots
$$

In this construction, the variable $x$ is not typically evaluated; it serves as a formal placeholder. The exponent of $x$ tracks a parameter of the combinatorial objects we are counting, such as size, length, or value. The coefficient $a_n$ represents the number of objects with parameter value $n$.

The simplest generating functions represent elementary choices.
*   The choice of a single, specific object of size 1 is represented by $x$.
*   The choice of "no object" is represented by $x^0 = 1$.
*   The choice to select any number of identical items corresponds to the sum $1 + x + x^2 + x^3 + \cdots$, which is the [geometric series](@entry_id:158490) $\frac{1}{1-x}$. Each term $x^k$ signifies the choice of taking $k$ of these items.
*   The choice to select an object at most once is $1+x$ ("don't take it" or "take it").
*   The choice to select an object from a set of $m$ distinct types (all of size 1) is $mx$.

These elementary building blocks are the vocabulary of the language of generating functions. The grammar is provided by a set of powerful rules for combining them.

### The Fundamental Operations: Sum and Product Rules

Just as complex structures are built from simpler components, complex generating functions are built from elementary ones using well-defined operations. The two most fundamental operations are addition and multiplication, corresponding to the sum and product rules of [combinatorics](@entry_id:144343).

The **Sum Rule** applies to disjoint choices. If we can form a structure by choosing an object from class $\mathcal{A}$ (counted by $A(x)$) *or* from a disjoint class $\mathcal{B}$ (counted by $B(x)$), the generating function for the combined class $\mathcal{A} \cup \mathcal{B}$ is simply $A(x) + B(x)$.

The **Product Rule** is more profound and applies to sequential or composite choices. If a structure is formed by taking an element from class $\mathcal{A}$ and, independently, an element from class $\mathcal{B}$, the generating function for the resulting [ordered pairs](@entry_id:269702) is the product $A(x)B(x)$. The coefficient of $x^n$ in this product, $[x^n]A(x)B(x)$, is given by the Cauchy product of the series coefficients:

$$
[x^n]A(x)B(x) = \sum_{k=0}^{n} ([x^k]A(x)) \cdot ([x^{n-k}]B(x)) = \sum_{k=0}^{n} a_k b_{n-k}
$$

This formula precisely captures the combinatorial process: to form a composite structure of total size $n$, we choose a component of size $k$ from $\mathcal{A}$ (in $a_k$ ways) and a component of size $n-k$ from $\mathcal{B}$ (in $b_{n-k}$ ways), and sum over all possible sizes $k$ for the first component.

A clear illustration of this principle is the construction of "partitioned keys," which are alphanumeric strings consisting of a non-empty block of digits followed by a non-empty block of lowercase letters [@problem_id:1371609]. Let's model this. A single decimal digit can be chosen in 10 ways, so a sequence of $k$ digits can be formed in $10^k$ ways. The OGF for a non-empty sequence of digits, where $x$ tracks the length, is:
$$
D(x) = 10x + (10x)^2 + (10x)^3 + \cdots = \frac{10x}{1-10x}
$$
Similarly, there are 26 lowercase letters. The OGF for a non-empty sequence of letters is:
$$
L(x) = 26x + (26x)^2 + (26x)^3 + \cdots = \frac{26x}{1-26x}
$$
A partitioned key is formed by concatenating a digit sequence and a letter sequence. The total length is the sum of the component lengths. By the [product rule](@entry_id:144424), the OGF for all partitioned keys is the product of the individual OGFs:
$$
A(x) = D(x) L(x) = \left(\frac{10x}{1-10x}\right) \left(\frac{26x}{1-26x}\right) = \frac{260x^2}{(1-10x)(1-26x)}
$$
The coefficient of $x^n$ in the expansion of this rational function gives the number of such keys of length $n$.

The [product rule](@entry_id:144424) also elegantly handles choices from mixed collections of distinct and identical items. Consider a gift basket assembled from 10 distinct artisan pastries and an unlimited supply of identical classic macarons [@problem_id:1371583]. For each of the 10 distinct pastries, we have two choices: include it or not. This is modeled by the factor $(1+x)$. Since there are 10 independent such choices, the OGF for selecting pastries is:
$$
P(x) = (1+x)(1+x)\cdots(1+x) = (1+x)^{10} = \sum_{k=0}^{10} \binom{10}{k}x^k
$$
Here, the coefficient of $x^k$ is $\binom{10}{k}$, the number of ways to choose $k$ pastries from 10. For the macarons, which are identical, we can choose any non-negative number. The OGF is:
$$
M(x) = 1 + x + x^2 + \cdots = \frac{1}{1-x}
$$
A complete gift basket is a combination of pastries and macarons. By the product rule, the OGF for the entire basket, where $x$ tracks the total number of items, is:
$$
A(x) = P(x)M(x) = \frac{(1+x)^{10}}{1-x}
$$
To find the number of ways to create a basket with exactly 15 items, we would need to find the coefficient $[x^{15}]A(x)$.

### Modeling Constrained Selection Problems

One of the primary applications of generating functions is in solving [integer partition](@entry_id:261742) problems, often disguised as allocation or distribution tasks. The general problem is to find the number of [non-negative integer solutions](@entry_id:261624) to an equation of the form $e_1 + e_2 + \cdots + e_k = n$ under various constraints on the variables $e_i$.

The strategy is to model the allowed values for each variable $e_i$ with its own [generating function](@entry_id:152704), $P_i(x)$, where the exponents represent the permissible integer values. The [generating function](@entry_id:152704) for the total number of solutions is then the product $A(x) = P_1(x)P_2(x)\cdots P_k(x)$. The answer to the problem is the coefficient of $x^n$ in $A(x)$.

Consider a scenario where $n=30$ computational tasks must be allocated among four processors, each with specific constraints [@problem_id:1371588]. Let $e_i$ be the number of tasks for processor $P_i$. The problem is to find the number of integer solutions to $e_1 + e_2 + e_3 + e_4 = 30$ subject to:
*   $P_1$: $e_1$ must be a positive odd integer. The allowed values are $\{1, 3, 5, \ldots\}$. The corresponding OGF is $P_1(x) = x^1 + x^3 + x^5 + \cdots = x(1 + x^2 + x^4 + \cdots) = \frac{x}{1-x^2}$.
*   $P_2$: $e_2$ must be a non-negative even integer. The allowed values are $\{0, 2, 4, \ldots\}$. The OGF is $P_2(x) = x^0 + x^2 + x^4 + \cdots = \frac{1}{1-x^2}$.
*   $P_3$: $e_3$ must be strictly greater than 5. The allowed values are $\{6, 7, 8, \ldots\}$. The OGF is $P_3(x) = x^6 + x^7 + x^8 + \cdots = x^6(1+x+x^2+\cdots) = \frac{x^6}{1-x}$.
*   $P_4$: $e_4$ must be between 0 and 10, inclusive. The allowed values are $\{0, 1, \ldots, 10\}$. The OGF is the finite geometric sum $P_4(x) = 1 + x + \cdots + x^{10} = \frac{1-x^{11}}{1-x}$.

The generating function for the total number of valid allocations is the product of these individual functions:
$$
A(x) = P_1(x)P_2(x)P_3(x)P_4(x) = \left(\frac{x}{1-x^2}\right) \left(\frac{1}{1-x^2}\right) \left(\frac{x^6}{1-x}\right) \left(\frac{1-x^{11}}{1-x}\right) = \frac{x^7(1-x^{11})}{(1-x^2)^2 (1-x)^2}
$$
The number of ways to allocate exactly 30 tasks is the coefficient $[x^{30}]A(x)$. While calculating this coefficient by hand can be algebraically intensive (often requiring [partial fraction decomposition](@entry_id:159208)), the setup itself is systematic and powerful, transforming a complex counting problem into a problem of algebraic manipulation.

### Generating Functions and Recurrence Relations

Generating functions offer a standard and effective method for solving [linear recurrence relations](@entry_id:273376). The core idea is to transform the recurrence relation, which defines a relationship between terms of a sequence, into an algebraic equation involving the sequence's generating function.

The general procedure is as follows:
1.  Write the recurrence relation for $a_n$.
2.  Multiply the entire equation by $x^n$.
3.  Sum both sides over all values of $n$ for which the recurrence is valid (e.g., from $n=1$ or $n=2$ to $\infty$).
4.  Manipulate the resulting series so they are expressed in terms of the [generating function](@entry_id:152704) $A(x) = \sum_{n=0}^{\infty} a_n x^n$ and other known functions.
5.  Solve the resulting algebraic equation for $A(x)$.

Let's apply this to model the population of a synthetic microorganism [@problem_id:1371589]. The population, $a_n$, after $n$ hours starts at $a_0$, doubles every hour, and receives an injection of $C$ new organisms. This yields the [recurrence relation](@entry_id:141039):
$$
a_n = 2a_{n-1} + C \quad \text{for } n \ge 1
$$
We multiply by $x^n$ and sum from $n=1$ to infinity:
$$
\sum_{n=1}^{\infty} a_n x^n = \sum_{n=1}^{\infty} (2a_{n-1} + C)x^n = 2\sum_{n=1}^{\infty} a_{n-1}x^n + C\sum_{n=1}^{\infty} x^n
$$
Now, we express each sum in terms of $A(x) = \sum_{n=0}^{\infty} a_n x^n$:
*   The left-hand side is $\sum_{n=1}^{\infty} a_n x^n = (a_0 + a_1 x + \cdots) - a_0 = A(x) - a_0$.
*   The first term on the right is $2x \sum_{n=1}^{\infty} a_{n-1}x^{n-1} = 2x \sum_{m=0}^{\infty} a_m x^m = 2x A(x)$.
*   The second term on the right is a [geometric series](@entry_id:158490): $C \frac{x}{1-x}$.

Substituting these back into the equation gives:
$$
A(x) - a_0 = 2x A(x) + C \frac{x}{1-x}
$$
This is a simple linear equation in $A(x)$. Solving for $A(x)$ yields:
$$
A(x)(1 - 2x) = a_0 + \frac{Cx}{1-x}
$$
$$
A(x) = \frac{a_0}{1-2x} + \frac{Cx}{(1-x)(1-2x)} = \frac{a_0(1-x) + Cx}{(1-x)(1-2x)}
$$
This [closed-form expression](@entry_id:267458) for $A(x)$ contains all the information about the sequence $a_n$. By using [partial fraction expansion](@entry_id:265121) on this result, we could find an explicit formula for $a_n$.

### Advanced Algebraic and Analytic Techniques

Beyond the basic operations, a rich collection of advanced techniques allows generating functions to solve an even broader class of problems.

#### The Partial Sum Operator

A common task is to analyze the cumulative or [partial sums](@entry_id:162077) of a sequence. If $a_n$ is a sequence with OGF $A(x)$, and we define a new [sequence of partial sums](@entry_id:161258) $s_n = \sum_{k=0}^{n} a_k$, what is its OGF, $S(x)$? We can derive this relationship directly:
$$
S(x) = \sum_{n=0}^{\infty} s_n x^n = \sum_{n=0}^{\infty} \left(\sum_{k=0}^{n} a_k\right) x^n
$$
By interchanging the order of summation (a valid operation for formal [power series](@entry_id:146836)), we get:
$$
S(x) = \sum_{k=0}^{\infty} a_k \sum_{n=k}^{\infty} x^n = \sum_{k=0}^{\infty} a_k \frac{x^k}{1-x} = \frac{1}{1-x} \sum_{k=0}^{\infty} a_k x^k = \frac{A(x)}{1-x}
$$
Thus, multiplication by $\frac{1}{1-x}$ is the generating function operator corresponding to taking [partial sums](@entry_id:162077). For instance, if we know the OGF for the Catalan numbers is $C(x) = \frac{1 - \sqrt{1-4x}}{2x}$, the OGF for the "cumulative Catalan numbers" $s_n = \sum_{k=0}^{n} c_k$ is immediately found to be $S(x) = \frac{C(x)}{1-x} = \frac{1-\sqrt{1-4x}}{2x(1-x)}$ [@problem_id:1371601].

#### Integer Partitions

Generating functions are the natural language for the theory of [integer partitions](@entry_id:139302). A partition of an integer $n$ is a way of writing $n$ as a sum of positive integers. The rules for constructing OGFs for partitions are direct consequences of the product rule.
*   To count partitions of $n$ into parts from a set $S \subseteq \mathbb{Z}^+$, where each part can be used any number of times, the OGF is $\prod_{k \in S} \frac{1}{1-x^k}$. Each factor $(1 + x^k + x^{2k} + \cdots)$ represents the choice of how many times to use the part $k$.
*   To count partitions of $n$ into *distinct* parts from a set $S$, the OGF is $\prod_{k \in S} (1+x^k)$. Each factor represents the choice of using the part $k$ either once ($x^k$) or not at all (1).

As an example, consider the number of ways a crystal can have a total energy of $n\epsilon_0$, where allowed phonon energies are distinct odd integer multiples of $\epsilon_0$ [@problem_id:1371610]. This is equivalent to counting partitions of the integer $n$ into distinct odd parts. The [generating function](@entry_id:152704) is therefore:
$$
A(x) = \prod_{j=0}^{\infty} (1 + x^{2j+1}) = (1+x)(1+x^3)(1+x^5)\cdots
$$
This [infinite product](@entry_id:173356) is a valid and complete answer. Using identities from Euler, it can be transformed into other forms, revealing deep connections within [partition theory](@entry_id:180359). For instance, it is a famous result from [partition theory](@entry_id:180359) that this product, which generates partitions into distinct odd parts, is also the [generating function](@entry_id:152704) for self-conjugate partitions.

#### The Roots of Unity Filter

A particularly elegant algebraic technique, the [roots of unity filter](@entry_id:266389), allows us to extract terms from a generating function whose exponents are congruent to a certain value modulo $m$. Let $P(x) = \sum p_n x^n$. Suppose we want to find the sum of coefficients $p_k$ where $k$ is a multiple of $m$. This sum is given by:
$$
\sum_{j=0}^{\infty} p_{jm} = \frac{1}{m} \sum_{k=0}^{m-1} P(\omega^k)
$$
where $\omega = \exp(2\pi i / m)$ is a primitive $m$-th root of unity. This identity relies on the property that the sum $\sum_{k=0}^{m-1} (\omega^j)^k$ equals $m$ if $m$ divides $j$, and 0 otherwise.

This method can be used to find a [closed-form expression](@entry_id:267458) for the number of subsets of $\{1, 2, \ldots, n\}$ whose size is a multiple of 4 [@problem_id:1371592]. The generating function for all subsets of an $n$-element set, where $x$ tracks [cardinality](@entry_id:137773), is the [binomial expansion](@entry_id:269603) $P(x) = (1+x)^n = \sum_{k=0}^{n} \binom{n}{k}x^k$. We want to compute $a_n = \sum_{j \ge 0} \binom{n}{4j}$. Using the filter with $m=4$ and the 4th roots of unity $\{1, i, -1, -i\}$, we have:
$$
a_n = \frac{1}{4} \left( P(1) + P(i) + P(-1) + P(-i) \right) = \frac{1}{4} \left( (1+1)^n + (1+i)^n + (1-1)^n + (1-i)^n \right)
$$
For $n \ge 1$, this simplifies to $a_n = \frac{1}{4} \left( 2^n + (1+i)^n + (1-i)^n \right)$. By converting $1+i$ and $1-i$ to [polar form](@entry_id:168412) ($1+i = \sqrt{2}e^{i\pi/4}$, $1-i = \sqrt{2}e^{-i\pi/4}$) and applying De Moivre's formula, the sum becomes:
$$
(1+i)^n + (1-i)^n = (\sqrt{2})^n (\cos(\frac{n\pi}{4}) + i\sin(\frac{n\pi}{4})) + (\sqrt{2})^n (\cos(\frac{n\pi}{4}) - i\sin(\frac{n\pi}{4})) = 2 \cdot 2^{n/2} \cos(\frac{n\pi}{4})
$$
Substituting this back gives the remarkable [closed-form expression](@entry_id:267458):
$$
a_n = \frac{1}{4}(2^n + 2^{n/2+1}\cos(\frac{n\pi}{4})) = 2^{n-2} + 2^{n/2-1}\cos(\frac{n\pi}{4})
$$

### The Symbolic Method: From Combinatorial Structure to Functional Equations

The [symbolic method](@entry_id:269772) provides a formal framework for translating the [recursive definition](@entry_id:265514) of a combinatorial structure directly into a functional equation for its [generating function](@entry_id:152704). This approach is central to the field of [analytic combinatorics](@entry_id:144725).

For **unlabeled structures**, where objects are considered identical (counted by OGFs), we define combinatorial classes and constructions:
*   **Atom ($\mathcal{Z}$):** A basic object of size 1. OGF: $x$.
*   **Empty Set ($\mathcal{E}$):** An object of size 0. OGF: $1$.
*   **Disjoint Union ($\mathcal{A} + \mathcal{B}$):** An object is either from $\mathcal{A}$ or $\mathcal{B}$. OGF: $A(x) + B(x)$.
*   **Cartesian Product ($\mathcal{A} \times \mathcal{B}$):** An object is an [ordered pair](@entry_id:148349) $(a,b)$ with $a \in \mathcal{A}, b \in \mathcal{B}$. OGF: $A(x)B(x)$.
*   **Sequence ($\text{SEQ}(\mathcal{A})$):** An ordered sequence of objects from $\mathcal{A}$. OGF: $\frac{1}{1-A(x)}$.

This formalism allows us to describe complex structures recursively. Consider the class of rooted plane trees, where each node's children are ordered. A tree is either a single root node, or a root node attached to a sequence of one or more subtrees, each of which is itself a rooted plane tree. To analyze trees by both the number of nodes ($n$) and leaves ($k$) [@problem_id:1371603], we use a bivariate generating function $T(x,y)$, where $x$ marks nodes and $y$ marks leaves.
*   A tree consisting of a single node is a leaf. Its symbolic representation is $\mathcal{L} = \mathcal{Z}_x \times \mathcal{Z}_y$, with GF $xy$. ($\mathcal{Z}_x$ marks a node, $\mathcal{Z}_y$ marks a leaf).
*   A non-leaf tree consists of a root node ($\mathcal{Z}_x$) followed by an ordered sequence of one or more subtrees from the class $\mathcal{T}$ itself. The construction is $\mathcal{Z}_x \times \text{SEQ}_{\ge 1}(\mathcal{T})$. The corresponding GF is $x \cdot \frac{T(x,y)}{1-T(x,y)}$.

The entire class of trees $\mathcal{T}$ is the disjoint union of these two cases: $\mathcal{T} = \mathcal{L} + (\mathcal{Z}_x \times \text{SEQ}_{\ge 1}(\mathcal{T}))$. Translating this directly into a [functional equation](@entry_id:176587) for the [generating function](@entry_id:152704) $T(x,y)$ gives:
$$
T(x,y) = xy + x \frac{T(x,y)}{1-T(x,y)}
$$
This can be rearranged into a quadratic equation for $T(x,y)$:
$$
T(x,y)^2 - T(x,y)(1-x+xy) + xy = 0
$$
Solving with the quadratic formula and choosing the branch that gives $T(0,y)=0$ (since there are no trees of size 0) yields the solution:
$$
T(x,y) = \frac{1-x+xy - \sqrt{(1-x+xy)^2 - 4xy}}{2}
$$

A similar, state-based approach can handle constraints on sequences, such as those defined by [regular languages](@entry_id:267831). For example, counting passwords that forbid the substring 'BB' and have an odd number of 'W's [@problem_id:1371579] can be done by building an automaton whose states track the forbidden substring constraint. One can then write a [system of linear equations](@entry_id:140416) for the generating functions associated with paths starting from each state, which can be solved using [matrix inversion](@entry_id:636005). The constraint on the number of 'W's is handled by introducing a second variable $y$ and using the [roots of unity filter](@entry_id:266389) (in this case, $(F(x,1)-F(x,-1))/2$) to isolate terms with an odd power of $y$.

### Exponential Generating Functions for Labeled Structures

While OGFs are suited for problems involving unlabeled objects (like coins or identical tasks), a different tool is needed for labeled objects (like distinct people or positions in a sequence). **Exponential generating functions (EGFs)** are designed for this purpose. For a sequence $a_n$ that counts the number of structures on $n$ labeled elements, its EGF is:
$$
A(x) = \sum_{n=0}^{\infty} a_n \frac{x^n}{n!}
$$
The division by $n!$ normalizes for the [permutations](@entry_id:147130) of labels. The product rule for EGFs has a distinct combinatorial meaning: the product $A(x)B(x)$ corresponds to partitioning a set of labeled elements into two subsets, creating a structure of type $\mathcal{A}$ on the first subset and a structure of type $\mathcal{B}$ on the second.

The [symbolic method](@entry_id:269772) also applies to labeled structures, but with different translations:
*   **Set ($\text{SET}(\mathcal{A})$):** Forming an unordered set of components from $\mathcal{A}$. EGF: $\exp(A(x))$.
*   **Cycle ($\text{CYC}(\mathcal{A})$):** Arranging objects from $\mathcal{A}$ in a cycle. EGF: $\ln(\frac{1}{1-A(x)})$, if $\mathcal{A}$ is the atomic class $\mathcal{Z}$.

This framework is perfectly suited for permutation problems. A permutation can be decomposed into a set of [disjoint cycles](@entry_id:140007). The EGF for a single cycle of any length $k \ge 1$ is $\sum_{k=1}^\infty \frac{(k-1)!}{k!} x^k = \ln(\frac{1}{1-x})$. Since a permutation is a *set* of cycles, the EGF for all permutations is:
$$
P(x) = \exp\left(\ln\left(\frac{1}{1-x}\right)\right) = \frac{1}{1-x} = \sum_{n=0}^\infty x^n = \sum_{n=0}^\infty n! \frac{x^n}{n!}
$$
The coefficient of $\frac{x^n}{n!}$ is $n!$, correctly counting the total number of permutations of $n$ elements.

This method shines when constraints are added. A **[derangement](@entry_id:190267)** is a permutation with no fixed points (no cycles of length 1). This corresponds to a "Secret Santa" arrangement where no employee draws their own name [@problem_id:1369377]. To find the EGF for [derangements](@entry_id:147540), we simply remove cycles of length 1 from our building blocks. The EGF for cycles of length $\ge 2$ is $\ln(\frac{1}{1-x}) - x$. The EGF for [derangements](@entry_id:147540) is thus:
$$
D(x) = \exp\left(\ln\left(\frac{1}{1-x}\right) - x\right) = \frac{\exp(\ln(\frac{1}{1-x}))}{\exp(x)} = \frac{e^{-x}}{1-x}
$$
To find the number of [derangements](@entry_id:147540) $d_n$, we need the coefficient of $\frac{x^n}{n!}$ in $D(x)$. This is $n![x^n]D(x)$. By multiplying the series for $e^{-x}$ and $\frac{1}{1-x}$:
$$
[x^n]\left(\sum_{k=0}^{\infty} \frac{(-1)^k x^k}{k!}\right)\left(\sum_{j=0}^{\infty} x^j\right) = \sum_{k=0}^n \frac{(-1)^k}{k!}
$$
Therefore, the number of [derangements](@entry_id:147540) of $n$ items is given by the well-known formula:
$$
d_n = n! \sum_{k=0}^n \frac{(-1)^k}{k!}
$$
This derivation showcases the elegance and power of EGFs in solving problems involving labeled structures and [permutations](@entry_id:147130).