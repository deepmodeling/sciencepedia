## Introduction
Permutations, the bijections of a set onto itself, are foundational elements in abstract algebra and beyond. While the standard two-line notation provides a complete description of a permutation's mapping, it is often cumbersome and fails to reveal its deeper structural properties. This article addresses this notational and conceptual gap by introducing a more powerful representation: the disjoint [cycle decomposition](@entry_id:145268).

In the following chapters, you will gain a comprehensive understanding of this essential tool. The first chapter, **Principles and Mechanisms**, will guide you through the algorithm for decomposing any permutation into a unique product of [disjoint cycles](@entry_id:140007) and explore the algebraic properties this form reveals, such as order and parity. Next, **Applications and Interdisciplinary Connections** will demonstrate how this decomposition serves as a vital bridge connecting group theory to combinatorics, linear algebra, and number theory. Finally, **Hands-On Practices** will provide you with opportunities to solidify your skills by tackling a curated set of problems. By the end of this article, you will not only be able to perform the decomposition but also leverage it to solve complex problems and appreciate its central role in modern mathematics.

## Principles and Mechanisms

While the two-line notation for [permutations](@entry_id:147130) is comprehensive, it is often notationally cumbersome and can obscure the underlying structure of the mapping. A more insightful and algebraically powerful representation is the **disjoint [cycle decomposition](@entry_id:145268)**. This chapter explores the principles governing this decomposition and the mechanisms through which it reveals the fundamental properties of a permutation.

### From Two-Line Notation to Cycles

A **cycle** is a permutation of a particularly simple form. A cycle denoted by $(a_1 \ a_2 \ \dots \ a_k)$ is a permutation that maps each element in the list to the next, with the last element mapping back to the first. That is, $\sigma(a_1) = a_2$, $\sigma(a_2) = a_3$, ..., $\sigma(a_{k-1}) = a_k$, and $\sigma(a_k) = a_1$. Any element not present in the list is a **fixed point**, meaning the cycle maps it to itself. The number of elements in the cycle, $k$, is called its **length**. A cycle of length $k$ is also known as a **[k-cycle](@entry_id:181391)**. For example, the cycle $(1 \ 5 \ 3)$ in $S_5$ maps $1 \to 5$, $5 \to 3$, and $3 \to 1$, while fixing $2$ and $4$.

Two cycles are said to be **disjoint** if they have no elements in common. For instance, in $S_5$, the cycles $(1 \ 2)$ and $(3 \ 4 \ 5)$ are disjoint, whereas $(1 \ 2)$ and $(2 \ 3)$ are not. The power of this concept lies in the fact that any permutation can be uniquely expressed as a product (i.e., composition) of [disjoint cycles](@entry_id:140007).

### The Disjoint Cycle Decomposition

The central theorem of this topic states that every permutation in $S_n$ can be written as a product of [disjoint cycles](@entry_id:140007). This decomposition is unique up to the ordering of the cycles and the choice of starting element within each cycle. To find this decomposition, one can follow a simple and effective algorithm.

The algorithm proceeds as follows:
1.  Choose the smallest element from the set $\{1, 2, \dots, n\}$ that has not yet been placed in a cycle. Let this element be $x$.
2.  Begin a new cycle with $x$. Trace its orbit by computing $\sigma(x)$, then $\sigma(\sigma(x))$, and so on, until you return to $x$. This sequence of elements forms one of the [disjoint cycles](@entry_id:140007).
3.  Repeat steps 1 and 2 until all elements from $\{1, 2, \dots, n\}$ have been placed in a cycle.

To illustrate this algorithm, consider the permutation $\sigma \in S_{12}$ given in two-line notation [@problem_id:1615629]:
$$
\sigma = \begin{pmatrix}
1  & 2  & 3  & 4  & 5  & 6 & 7 & 8 & 9  & 10 & 11 & 12 \\
11 & 8  & 1  & 10 & 2  & 6 & 5 & 3 & 12 & 4  & 7  & 9
\end{pmatrix}
$$
We begin with the smallest element, $1$. We trace its orbit: $\sigma(1)=11$, $\sigma(11)=7$, $\sigma(7)=5$, $\sigma(5)=2$, $\sigma(2)=8$, $\sigma(8)=3$, and finally $\sigma(3)=1$. This closes the loop, giving us our first cycle: $(1 \ 11 \ 7 \ 5 \ 2 \ 8 \ 3)$.

The smallest element not yet included is $4$. Its orbit is $\sigma(4)=10$ and $\sigma(10)=4$. This yields the 2-cycle $(4 \ 10)$.

The next available element is $6$. We find that $\sigma(6)=6$. This is a fixed point, which corresponds to a 1-cycle, $(6)$.

The next available element is $9$. Its orbit is $\sigma(9)=12$ and $\sigma(12)=9$, giving the cycle $(9 \ 12)$. All elements from $1$ to $12$ are now accounted for. The full decomposition of $\sigma$ is therefore $(1 \ 11 \ 7 \ 5 \ 2 \ 8 \ 3)(4 \ 10)(6)(9 \ 12)$.

### Uniqueness and a Canonical Representation

As noted, the [cycle decomposition](@entry_id:145268) is not strictly unique. Firstly, [disjoint cycles](@entry_id:140007) commute, a property we will prove shortly. This means that $(1 \ 2)(3 \ 4)$ and $(3 \ 4)(1 \ 2)$ represent the same permutation. Secondly, a single cycle can be written in multiple ways; for instance, $(1 \ 2 \ 3)$ is the same permutation as $(2 \ 3 \ 1)$ and $(3 \ 1 \ 2)$.

To resolve this ambiguity and provide a single, standard representation for every permutation, we can define a **canonical disjoint [cycle decomposition](@entry_id:145268)**. A common set of conventions for this canonical form is as follows [@problem_id:1788791]:
1.  Omit all 1-cycles (fixed points) from the notation. The only exception is the identity permutation, which may be denoted by $(1)$ or simply $e$.
2.  Write each cycle with its smallest element first.
3.  Order the cycles from left to right in increasing order of their first elements.

Applying these rules to our previous example, $\sigma = (1 \ 11 \ 7 \ 5 \ 2 \ 8 \ 3)(4 \ 10)(6)(9 \ 12)$, we first omit the 1-cycle $(6)$. Then we ensure each cycle begins with its smallest element and order them.
- $(1 \ 11 \ 7 \ 5 \ 2 \ 8 \ 3)$ already starts with its smallest element, $1$.
- $(4 \ 10)$ already starts with its smallest element, $4$.
- $(9 \ 12)$ already starts with its smallest element, $9$.
Ordering these by their first elements ($1 \lt 4 \lt 9$), the [canonical form](@entry_id:140237) is $\sigma = (1 \ 11 \ 7 \ 5 \ 2 \ 8 \ 3)(4 \ 10)(9 \ 12)$.

This canonical form is essential for determining whether two [permutations](@entry_id:147130), perhaps written differently, are in fact the same. For example, consider $\sigma = (3 \ 1 \ 8)(6 \ 9)(4 \ 7 \ 2 \ 5)$ and $\tau = (2 \ 5 \ 4 \ 7)(1 \ 8 \ 3)(9 \ 6)$ in $S_9$. By converting each to its canonical form—$(1 \ 8 \ 3)(2 \ 5 \ 4 \ 7)(6 \ 9)$—we can definitively conclude that $\sigma = \tau$ [@problem_id:1788791].

### The Algebra of Permutations in Cycle Form

The disjoint cycle form simplifies many algebraic manipulations.

#### Commutativity of Disjoint Cycles

A cornerstone property is that **[disjoint cycles](@entry_id:140007) commute**. Let $\sigma$ and $\tau$ be two [disjoint cycles](@entry_id:140007). This means the set of elements moved by $\sigma$ (its **support**) and the set of elements moved by $\tau$ are disjoint. To prove they commute, we must show that $\sigma\tau = \tau\sigma$, which means $\sigma(\tau(x)) = \tau(\sigma(x))$ for all elements $x$.
- If $x$ is not moved by either $\sigma$ or $\tau$, then $\sigma(\tau(x)) = \sigma(x) = x$, and $\tau(\sigma(x)) = \tau(x) = x$.
- If $x$ is moved by $\sigma$ but not $\tau$, then $\tau(x)=x$. So $\sigma(\tau(x)) = \sigma(x)$. Since $\sigma(x)$ is also in the support of $\sigma$, it is not in the support of $\tau$, so $\tau(\sigma(x)) = \sigma(x)$.
- A symmetric argument holds if $x$ is moved by $\tau$ but not $\sigma$.
Since the supports are disjoint, no element is moved by both. Thus, $\sigma\tau = \tau\sigma$.

This property is elegantly demonstrated through conjugation. Consider two [disjoint cycles](@entry_id:140007) $\sigma=(1 \ 7 \ 3)$ and $\tau=(2 \ 9 \ 5 \ 8)$ in $S_{10}$ [@problem_id:1615648]. Calculating the product $\sigma\tau\sigma^{-1}$ yields $\tau$. Since $\sigma\tau\sigma^{-1} = \tau$ implies $\sigma\tau = \tau\sigma$, this confirms their commutativity.

#### Inverses of Permutations

Finding the inverse of a permutation is straightforward in its disjoint cycle form. Since [disjoint cycles](@entry_id:140007) commute, the inverse of a product of [disjoint cycles](@entry_id:140007) is the product of their inverses: if $\pi = \sigma_1 \sigma_2 \dots \sigma_m$, then $\pi^{-1} = \sigma_1^{-1} \sigma_2^{-1} \dots \sigma_m^{-1}$.

The inverse of a single cycle $(a_1 \ a_2 \ \dots \ a_k)$ is found by simply reversing the order of its elements: $(a_k \ \dots \ a_2 \ a_1)$. This is because the original cycle maps $a_i \to a_{i+1}$, while the reversed cycle maps $a_{i+1} \to a_i$, undoing the action.

For example, in a hypothetical data encryption protocol where a 13-element block is permuted by $\sigma = (8 \ 1 \ 5)(4 \ 2 \ 11 \ 7)(9 \ 3 \ 10 \ 12 \ 6)$, the decryption key is $\sigma^{-1}$ [@problem_id:1615651]. We find the inverse of each cycle:
- $(8 \ 1 \ 5)^{-1} = (5 \ 1 \ 8)$
- $(4 \ 2 \ 11 \ 7)^{-1} = (7 \ 11 \ 2 \ 4)$
- $(9 \ 3 \ 10 \ 12 \ 6)^{-1} = (6 \ 12 \ 10 \ 3 \ 9)$
So, $\sigma^{-1} = (5 \ 1 \ 8)(7 \ 11 \ 2 \ 4)(6 \ 12 \ 10 \ 3 \ 9)$. Converting this to canonical form gives $(1 \ 8 \ 5)(2 \ 4 \ 7 \ 11)(3 \ 9 \ 6 \ 12 \ 10)$.

### Structural Properties Revealed by Cycle Decomposition

The true power of the disjoint [cycle decomposition](@entry_id:145268) is its ability to reveal deep structural properties of a permutation at a glance.

#### Order of a Permutation

The **order** of a permutation $\sigma$ is the smallest positive integer $k$ such that $\sigma^k$ is the identity permutation. For a permutation written as a product of [disjoint cycles](@entry_id:140007), $\sigma = \sigma_1 \sigma_2 \dots \sigma_m$, its order is the **[least common multiple](@entry_id:140942) (lcm)** of the lengths of the individual cycles. If the lengths are $L_1, L_2, \dots, L_m$, then $\text{ord}(\sigma) = \text{lcm}(L_1, L_2, \dots, L_m)$.

This is because, due to commutativity, $\sigma^k = (\sigma_1 \dots \sigma_m)^k = \sigma_1^k \dots \sigma_m^k$. For $\sigma^k$ to be the identity, each $\sigma_i^k$ must be the identity. The order of a single $L_i$-cycle is $L_i$, so we need $k$ to be a multiple of every $L_i$. The smallest such positive integer is their lcm.

For instance, if a data scrambling device uses the permutation $\sigma = (1 \ 3 \ 5 \ 7 \ 2)(4 \ 8 \ 6)$, the minimum number of times the operation must be applied to restore the original order is the order of $\sigma$. The cycle lengths are 5 and 3. Thus, the order is $\text{lcm}(5, 3) = 15$ [@problem_id:1788808].

#### Parity and the Sign of a Permutation

Every permutation can be written as a product of 2-cycles, also called **transpositions**. While this decomposition is not unique, the parity of the number of [transpositions](@entry_id:142115) is an invariant property of the permutation. A permutation is **even** if it can be written as an even number of [transpositions](@entry_id:142115), and **odd** otherwise.

The disjoint [cycle decomposition](@entry_id:145268) provides a simple way to determine parity. A $k$-cycle can be decomposed into $k-1$ transpositions: $(a_1 \ a_2 \ \dots \ a_k) = (a_1 \ a_k)(a_1 \ a_{k-1})\dots(a_1 \ a_2)$. Therefore, the **sign** of a $k$-cycle, denoted $\text{sgn}(\sigma)$, is $(-1)^{k-1}$. A $k$-cycle is even if its length $k$ is odd, and odd if its length $k$ is even.

The sign of a product of [disjoint cycles](@entry_id:140007) is the product of their signs. Thus, for $\sigma = \sigma_1 \dots \sigma_m$ with lengths $L_1, \dots, L_m$, we have:
$$ \text{sgn}(\sigma) = \prod_{i=1}^{m} \text{sgn}(\sigma_i) = \prod_{i=1}^{m} (-1)^{L_i-1} = (-1)^{\sum(L_i-1)} $$
A permutation is even if $\sum(L_i-1)$ is even, and odd if it is odd. For the scrambling permutation $\sigma = (1 \ 3 \ 5 \ 7 \ 2)(4 \ 8 \ 6)$, the sign is $(-1)^{5-1} \times (-1)^{3-1} = (-1)^4 \times (-1)^2 = 1 \times 1 = 1$. It is an [even permutation](@entry_id:152892) [@problem_id:1788808]. This property is crucial in defining the alternating group $A_n$, the subgroup of all even permutations in $S_n$ [@problem_id:1615586].

#### Cycle Type and Conjugacy

The set of lengths of the cycles in the disjoint [cycle decomposition](@entry_id:145268) of a permutation $\sigma \in S_n$ (including 1-cycles for fixed points) forms a partition of the integer $n$. This list of lengths, usually written in non-increasing order, is called the **[cycle type](@entry_id:136710)** of the permutation. For example, the permutation $\alpha = (1 \ 2 \ 3 \ 4)(5 \ 6 \ 7)(8 \ 9)$ in $S_9$ has [cycle type](@entry_id:136710) $(4, 3, 2)$ [@problem_id:1615599].

A key observation is that a permutation $\sigma$ and its inverse $\sigma^{-1}$ always have the same [cycle type](@entry_id:136710). This is because the inverse of a $k$-cycle is another $k$-cycle, so the list of cycle lengths remains unchanged [@problem_id:1615638].

The concept of [cycle type](@entry_id:136710) is profoundly connected to the algebraic structure of the [symmetric group](@entry_id:142255). One of the most important theorems in this area states that **two permutations in $S_n$ are conjugate if and only if they have the same [cycle type](@entry_id:136710)**. Recall that $\pi$ is conjugate to $\sigma$ if there exists a $\tau \in S_n$ such that $\pi = \tau\sigma\tau^{-1}$.

The intuition behind this theorem is that conjugation is simply a "relabeling" of the elements. If $\sigma = (a_1 \ \dots \ a_k)$, then its conjugate is $\tau\sigma\tau^{-1} = (\tau(a_1) \ \dots \ \tau(a_k))$. This is a new $k$-cycle. This allows us to construct a conjugating element $\tau$ for any two permutations $\sigma$ and $\pi$ with the same [cycle type](@entry_id:136710). We simply define $\tau$ as the map that takes the elements of the cycles of $\sigma$ to the corresponding elements of the cycles of $\pi$ [@problem_id:1788751].

For example, to find $\tau$ such that $\pi = \tau\sigma\tau^{-1}$ for $\sigma = (1 \ 5 \ 3)(2 \ 8 \ 7 \ 4)(6 \ 9)$ and $\pi = (2 \ 6 \ 9)(1 \ 3 \ 4 \ 8)(5 \ 7)$, we match cycles of the same length and define $\tau$ accordingly:
- Map $(1 \ 5 \ 3)$ to $(2 \ 6 \ 9)$: $\tau(1)=2, \tau(5)=6, \tau(3)=9$.
- Map $(2 \ 8 \ 7 \ 4)$ to $(1 \ 3 \ 4 \ 8)$: $\tau(2)=1, \tau(8)=3, \tau(7)=4, \tau(4)=8$.
- Map $(6 \ 9)$ to $(5 \ 7)$: $\tau(6)=5, \tau(9)=7$.
This defines the permutation $\tau$, which can then be written in its own disjoint cycle form: $\tau = (1 \ 2)(3 \ 9 \ 7 \ 4 \ 8)(5 \ 6)$.

### Powers of a Cycle: A Deeper Look

We conclude with a more detailed investigation into the structure of powers of a single cycle. What is the disjoint [cycle decomposition](@entry_id:145268) of $\sigma^k$, where $\sigma$ is an $n$-cycle?

Let $\sigma = (a_1 \ a_2 \ \dots \ a_n)$. Applying $\sigma^k$ to an element $a_i$ maps it to $a_{i+k}$ (with indices modulo $n$). The structure of $\sigma^k$ depends fundamentally on the greatest common divisor, $\gcd(k, n)$. An element $a_i$ returns to itself under powers of $\sigma^k$ after $L$ steps, where $L$ is the smallest positive integer such that $Lk$ is a multiple of $n$. This value is given by $L = n / \gcd(k, n)$.

This means that $\sigma^k$ decomposes into several [disjoint cycles](@entry_id:140007), each of length $n / \gcd(k, n)$. How many such cycles are there? Since they partition the $n$ elements, the number of cycles must be $n / L = n / (n / \gcd(k, n)) = \gcd(k, n)$.

Thus, for an $n$-cycle $\sigma$, the permutation $\sigma^k$ decomposes into $\gcd(k, n)$ [disjoint cycles](@entry_id:140007), each of length $n / \gcd(k, n)$.

A particularly clear case arises when $k$ is a divisor of $n$. Let $n = km$. Then $\gcd(k, n) = \gcd(k, km) = k$. According to our formula, $\sigma^k$ decomposes into $k$ [disjoint cycles](@entry_id:140007), each of length $n/k = m$. This provides a powerful predictive tool for understanding the iterative application of a cyclic permutation [@problem_id:1615649].