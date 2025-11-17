## Introduction
A permutation reorders a set of objects. But what happens when we perform one reordering after another? The answer lies in the **composition of permutations**, the fundamental operation that transforms the set of all permutations into a rich algebraic structure known as a group. Understanding composition is not just about calculation; it's about unlocking the deep structural properties of symmetry and transformation. While individual [permutations](@entry_id:147130) are simple to grasp, their interactions can be complex and non-intuitive. This article addresses the gap between knowing what a permutation is and understanding the rules that govern how they combine, why the order of operations matters, and what collective properties emerge from their composition.

We will guide you through this essential topic across three chapters. In "Principles and Mechanisms," you will learn the mechanics of composing [permutations](@entry_id:147130), calculating their disjoint cycle form, and determining key properties like order and parity. "Applications and Interdisciplinary Connections" will then reveal how these abstract concepts are used to model real-world problems in cryptography, number theory, and computer science. Finally, "Hands-On Practices" provides targeted exercises to solidify your skills and deepen your conceptual understanding. Let's begin by dissecting the core principles and mechanics of combining permutations to see how structure arises from this single, powerful operation.

## Principles and Mechanisms

Having established the fundamental concept of a permutation as a [bijective function](@entry_id:140004) on a [finite set](@entry_id:152247), we now turn to the primary operation that endows the set of all [permutations](@entry_id:147130) with a rich algebraic structure: **composition**. This chapter will elucidate the mechanics of composing permutations, explore the structural consequences of this operation, and introduce key related concepts such as order, parity, and [commutativity](@entry_id:140240).

### The Mechanics of Composition

The composition of two [permutations](@entry_id:147130), $\sigma$ and $\tau$, on a set $S$ is simply their composition as functions. If we denote the composite permutation by $\sigma\tau$, its action on an element $x \in S$ is defined by applying $\tau$ first, followed by $\sigma$. This is expressed as:

$$ (\sigma\tau)(x) = \sigma(\tau(x)) $$

This right-to-left convention is standard in group theory and is essential to remember for all computations. Composition is an associative operation, meaning for any three permutations $\alpha, \beta, \gamma$, we have $(\alpha\beta)\gamma = \alpha(\beta\gamma)$. This allows us to write products of multiple permutations without ambiguity.

To find the result of a composition, we must determine the final destination of each element in the set being permuted. This is most systematically done by converting the product into its unique **disjoint [cycle notation](@entry_id:146599)**. The process involves tracking the path of each element through the sequence of permutations, applied from right to left.

Consider a permutation $\sigma \in S_9$ given as a [product of transpositions](@entry_id:138554):
$$ \sigma = (1 \ 5)(3 \ 8)(1 \ 9)(2 \ 4)(8 \ 6)(5 \ 2) $$
To find the disjoint cycle form of $\sigma$, we select an element and trace its path. Let's start with $1$:
- The rightmost transposition, $(5 \ 2)$, fixes $1$.
- Moving left, $(8 \ 6)$ and $(2 \ 4)$ also fix $1$.
- The [transposition](@entry_id:155345) $(1 \ 9)$ maps $1 \mapsto 9$.
- The remaining transpositions, $(3 \ 8)$ and $(1 \ 5)$, fix $9$.
Thus, the net effect is $\sigma(1) = 9$.

Now we trace the path of $9$:
- $(5 \ 2)$, $(8 \ 6)$, and $(2 \ 4)$ fix $9$.
- $(1 \ 9)$ maps $9 \mapsto 1$.
- $(3 \ 8)$ fixes $1$.
- $(1 \ 5)$ maps $1 \mapsto 5$.
So, $\sigma(9) = 5$.

Continuing this process, we find:
- $\sigma(5)=4$ (since $5 \xrightarrow{(5\ 2)} 2 \xrightarrow{(2\ 4)} 4$)
- $\sigma(4)=2$ (since $4 \xrightarrow{(2\ 4)} 2$)
- $\sigma(2)=1$ (since $2 \xrightarrow{(5\ 2)} 5 \xrightarrow{(1\ 5)} 1$)

This completes our first cycle: $(1 \ 9 \ 5 \ 4 \ 2)$. We then select an element not in this cycle, such as $3$, and repeat the process. This reveals a second cycle, $(3 \ 8 \ 6)$. The element $7$ is unmoved by any of the transpositions, so it is a fixed point and is typically omitted from the final notation. The complete disjoint cycle representation is therefore $\sigma = (1 \ 9 \ 5 \ 4 \ 2)(3 \ 8 \ 6)$ [@problem_id:1655271]. A similar calculation can be performed for any product of permutations, such as the one arising from a sequence of hypothetical 'C-SWAP' gates on a data register, which are merely [transpositions](@entry_id:142115) [@problem_id:1842381].

The composition of [permutations](@entry_id:147130) that are not disjoint can lead to interesting results. For example, composing two cycles that share just one element can merge them into a single, larger cycle. Consider $\alpha = (1 \ 2 \ 3 \ 4 \ 5)$ and $\beta = (5 \ 6 \ 7 \ 8 \ 9)$ in $S_9$. The composition $\pi = \beta\alpha$ is found by tracing elements as before. We find $\pi(1) = \beta(\alpha(1)) = \beta(2) = 2$, $\pi(2) = 3$, and $\pi(3) = 4$. However, at element $4$, we have $\pi(4) = \beta(\alpha(4)) = \beta(5) = 6$. The two cycles are linked through the element $5$. Continuing this process reveals that the product is the single 9-cycle $\pi = (1 \ 2 \ 3 \ 4 \ 6 \ 7 \ 8 \ 9 \ 5)$ [@problem_id:1608016].

### Fundamental Properties of Composition

While composition is always associative, it lacks another familiar property of arithmetic: commutativity. In general, for two permutations $\sigma$ and $\tau$, the product $\sigma\tau$ is not equal to $\tau\sigma$.

To illustrate this crucial property, let's examine two [permutations](@entry_id:147130) in $S_5$: $\sigma = (1 \ 5 \ 2)$ and $\tau = (1 \ 3 \ 4 \ 2)$. Let us compute both $\tau\sigma$ and $\sigma\tau$.

For $\tau\sigma$:
- $(\tau\sigma)(1) = \tau(\sigma(1)) = \tau(5) = 5$.
- $(\tau\sigma)(5) = \tau(\sigma(5)) = \tau(2) = 1$. This gives the cycle $(1 \ 5)$.
- $(\tau\sigma)(2) = \tau(\sigma(2)) = \tau(1) = 3$.
- $(\tau\sigma)(3) = \tau(\sigma(3)) = \tau(3) = 4$.
- $(\tau\sigma)(4) = \tau(\sigma(4)) = \tau(4) = 2$. This gives the cycle $(2 \ 3 \ 4)$.
Thus, $\tau\sigma = (1 \ 5)(2 \ 3 \ 4)$.

For $\sigma\tau$:
- $(\sigma\tau)(1) = \sigma(\tau(1)) = \sigma(3) = 3$.
- $(\sigma\tau)(3) = \sigma(\tau(3)) = \sigma(4) = 4$.
- $(\sigma\tau)(4) = \sigma(\tau(4)) = \sigma(2) = 1$. This gives the cycle $(1 \ 3 \ 4)$.
- $(\sigma\tau)(2) = \sigma(\tau(2)) = \sigma(1) = 5$.
- $(\sigma\tau)(5) = \sigma(\tau(5)) = \sigma(5) = 2$. This gives the cycle $(2 \ 5)$.
Thus, $\sigma\tau = (1 \ 3 \ 4)(2 \ 5)$.

Clearly, $(1 \ 5)(2 \ 3 \ 4) \neq (1 \ 3 \ 4)(2 \ 5)$, demonstrating that [permutation composition](@entry_id:137723) is **non-commutative** [@problem_id:1634757]. The object that measures this failure to commute is the **commutator**, defined as $[\sigma, \tau] = \sigma\tau\sigma^{-1}\tau^{-1}$. If and only if $\sigma$ and $\tau$ commute, their commutator is the identity permutation.

### Structural Consequences of Composition

The way [permutations](@entry_id:147130) combine has profound implications for their individual and collective properties. Two of the most important are the [order of a permutation](@entry_id:146478) and its parity.

#### Order of a Permutation

The **order** of a permutation $\sigma$ is the smallest positive integer $k$ such that $\sigma^k$ (the composition of $\sigma$ with itself $k$ times) is the identity permutation, $e$. The order is determined directly from the disjoint cycle structure of the permutation.

**Theorem:** The [order of a permutation](@entry_id:146478) written as a product of [disjoint cycles](@entry_id:140007) is the [least common multiple](@entry_id:140942) (LCM) of the lengths of those cycles.

For instance, the permutation $\tau\sigma = (1 \ 5)(2 \ 3 \ 4)$ from our earlier example has order $\operatorname{lcm}(2, 3) = 6$. Similarly, $\sigma\tau = (1 \ 3 \ 4)(2 \ 5)$ also has order $\operatorname{lcm}(3, 2) = 6$ [@problem_id:1634757].

This relationship allows us to deduce information about a permutation's cycle structure from its order, and vice versa. Suppose we are told a permutation $\sigma \in S_6$ has the property that $\sigma^3 = e$ [@problem_id:1783264]. This implies that the order of $\sigma$ must be a divisor of 3, so its order is either 1 or 3. By the theorem, the length of every cycle in its disjoint decomposition must divide the order. Therefore, all cycles must have length 1 or 3. Since the sum of the cycle lengths must equal 6, we can find all possible partitions of 6 into parts of size 1 or 3:
1. $6 = 1+1+1+1+1+1$: Cycle structure $(1, 1, 1, 1, 1, 1)$. This corresponds to the identity permutation.
2. $6 = 3+1+1+1$: Cycle structure $(3, 1, 1, 1)$.
3. $6 = 3+3$: Cycle structure $(3, 3)$.
These are the only three possible cycle structures for a permutation in $S_6$ whose order divides 3.

Conversely, knowing aspects of the cycle structure and the order can reveal the full structure. If a permutation $\pi \in S_9$ has order 12 and is known to be the composition of exactly three [disjoint cycles](@entry_id:140007) of lengths $a, b, c$, we have two conditions: $a+b+c=9$ and $\operatorname{lcm}(a,b,c)=12$. Since $12 = 2^2 \cdot 3$, at least one cycle length must be divisible by 4, and at least one must be divisible by 3. The only set of three positive integers that satisfies both the sum and the LCM condition is $\{2, 3, 4\}$ [@problem_id:1783288].

#### Parity and the Sign of a Permutation

A **transposition** is a permutation that swaps two elements and leaves all others fixed, i.e., a 2-cycle. A fundamental theorem states that any permutation can be written as a composition of transpositions. While the specific transpositions are not unique, their number will always have the same parity (even or odd). A permutation is called **even** if it can be written as an even number of [transpositions](@entry_id:142115), and **odd** if it requires an odd number.

This parity is captured by the **[sign homomorphism](@entry_id:185002)**, a function $\operatorname{sgn}: S_n \to \{+1, -1\}$ where $\operatorname{sgn}(\sigma) = +1$ if $\sigma$ is even and $\operatorname{sgn}(\sigma) = -1$ if $\sigma$ is odd. The power of the sign function lies in its homomorphic property:

$$ \operatorname{sgn}(\sigma\tau) = \operatorname{sgn}(\sigma)\operatorname{sgn}(\tau) $$

This means the parity of a composition can be found by multiplying the signs of its constituents. For example, the composition of two odd permutations, $\sigma_1$ and $\sigma_2$, results in a composite permutation $\pi = \sigma_2\sigma_1$. Its sign is $\operatorname{sgn}(\pi) = \operatorname{sgn}(\sigma_2)\operatorname{sgn}(\sigma_1) = (-1)(-1) = +1$. Therefore, the composition of any two odd permutations is always an [even permutation](@entry_id:152892) [@problem_id:1839546].

This property is extremely useful for analyzing complex compositions. For instance, we can determine the parity of any commutator, $[\alpha, \beta] = \alpha\beta\alpha^{-1}\beta^{-1}$. We use the fact that a permutation and its inverse have the same sign, as $\operatorname{sgn}(\alpha)\operatorname{sgn}(\alpha^{-1}) = \operatorname{sgn}(\alpha\alpha^{-1}) = \operatorname{sgn}(e) = +1$.
$$ \operatorname{sgn}([\alpha, \beta]) = \operatorname{sgn}(\alpha)\operatorname{sgn}(\beta)\operatorname{sgn}(\alpha^{-1})\operatorname{sgn}(\beta^{-1}) = (\operatorname{sgn}(\alpha))^2 (\operatorname{sgn}(\beta))^2 $$
Since the square of either $+1$ or $-1$ is $+1$, the sign of any commutator is always $+1$. This proves that all commutators are even permutations [@problem_id:1783268].

### Generators and Special Subgroups

The set of [even permutations](@entry_id:146469) in $S_n$ is of paramount importance. It is closed under composition (the product of two even permutations is even) and contains the identity and all inverses, thus forming a subgroup called the **alternating group**, denoted $A_n$.

A key theorem in the study of symmetric groups states that for $n \ge 3$, the alternating group $A_n$ is **generated** by the set of all 3-cycles. This means that any [even permutation](@entry_id:152892) can be expressed as a composition of 3-cycles. To be an [even permutation](@entry_id:152892), a permutation's [disjoint cycle decomposition](@entry_id:137482) must contain an even number of cycles of even length (since a $k$-cycle can be written as $k-1$ transpositions). For example, the permutation $\sigma = (1 \ 3)(2 \ 5 \ 8)(4 \ 9 \ 7 \ 6)$ in $S_9$ is even because the transposition $(1 \ 3)$ is odd, the 3-cycle $(2 \ 5 \ 8)$ is even, and the 4-cycle $(4 \ 9 \ 7 \ 6)$ is odd. The composition of odd + even + odd results in an [even permutation](@entry_id:152892). As an element of $A_9$, it must be expressible as a product of 3-cycles, such as $(1 \ 2 \ 3)(2 \ 8 \ 1)(2 \ 4 \ 5)(4 \ 6 \ 2)(4 \ 9 \ 7)$ [@problem_id:1783280].

Finally, we return to the concept of commutativity. While [permutations](@entry_id:147130) in $S_n$ do not generally commute with each other, one might ask what happens if a permutation commutes with a large family of other [permutations](@entry_id:147130). Consider a permutation $\pi \in S_7$ that commutes with every [transposition](@entry_id:155345) of the form $(1, k)$ for $k \in \{2, 3, \dots, 7\}$. The condition $\pi \circ (1, k) = (1, k) \circ \pi$ can be analyzed by evaluating its action on specific elements. Let's evaluate at the element $1$:
$$ \pi((1,k)(1)) = (1,k)(\pi(1)) $$
$$ \pi(k) = (1,k)(\pi(1)) $$
Let $a = \pi(1)$. The equation becomes $\pi(k) = (1,k)(a)$. If we assume $a \neq 1$, then for any $k \neq a$, the transposition $(1,k)$ fixes $a$, which would mean $\pi(k) = a$ for multiple distinct values of $k$. This contradicts the fact that a permutation is a [bijection](@entry_id:138092). Therefore, the only possibility is that $a=1$, meaning $\pi(1)=1$. The equation then simplifies to $\pi(k) = (1,k)(1) = k$. Since this holds for all $k \in \{2, \dots, 7\}$, we conclude that $\pi$ must be the identity permutation [@problem_id:1783243]. This powerful result gives a first indication that for $n \ge 3$, the only permutation that commutes with all others is the identity itself.