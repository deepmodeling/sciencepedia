## Introduction
The classification of finite groups is a cornerstone of modern algebra, aiming to create a complete catalog of all possible finite group structures. While this grand project is immensely complex, certain classes of groups offer a more tractable yet highly instructive landscape. Groups of order $pq$, where $p$ and $q$ are distinct prime numbers, represent one such foundational case. Their structure is remarkably constrained, making a complete classification not only possible but also an elegant demonstration of core group-theoretic tools. This article addresses the fundamental question: what are all the possible group structures of order $pq$?

This article systematically derives the complete classification, showing that for any given pair of distinct primes, there are at most two non-[isomorphic groups](@entry_id:148221) of that order. The first chapter, **Principles and Mechanisms**, will leverage the power of Sylow's theorems and the concept of the semirect product to establish this classification and dissect the structural properties of the resulting groups. The second chapter, **Applications and Interdisciplinary Connections**, explores how these groups serve as canonical examples in advanced topics like representation theory and Galois theory. Finally, **Hands-On Practices** will provide an opportunity to apply these theoretical concepts to concrete problems, solidifying your understanding of these essential algebraic objects.

## Principles and Mechanisms

In the study of finite groups, a central objective is the classification of all possible group structures of a given order. While this is a formidable task in general, for certain orders, a complete classification is attainable. Groups of order $n=pq$, where $p$ and $q$ are distinct prime numbers, represent a foundational and highly instructive case. The structure of such groups is rigidly constrained, yielding at most two [isomorphism classes](@entry_id:147854) for any given pair of primes. This chapter will systematically derive this classification, relying principally on Sylow's theorems and the concept of the [semidirect product](@entry_id:147230).

### The Universal Normal Subgroup

Let $G$ be a group of order $|G|=pq$, where $p$ and $q$ are prime numbers. Without loss of generality, let us assume $p  q$. Our first step is to analyze the Sylow subgroups of $G$. The Sylow theorems provide powerful constraints on the number of Sylow $k$-subgroups, denoted $n_k$.

According to Sylow's Third Theorem, the number of Sylow $q$-subgroups, $n_q$, must satisfy two conditions:
1.  $n_q$ must divide the index of the Sylow $q$-subgroup in $G$, which is $p$. Thus, $n_q \in \{1, p\}$.
2.  $n_q \equiv 1 \pmod q$.

Since we have assumed $p  q$, the condition $n_q = p$ would imply $p \equiv 1 \pmod q$, which is impossible. Therefore, the only possibility is $n_q=1$.

This is a powerful and universal result for any group of order $pq$. It establishes that there is always a **unique Sylow $q$-subgroup**. A fundamental theorem of group theory states that a Sylow subgroup is **normal** in $G$ if and only if it is unique. Thus, every group of order $pq$ (with $p  q$) contains a [normal subgroup](@entry_id:144438) of order $q$. Since any group of [prime order](@entry_id:141580) is cyclic, this [normal subgroup](@entry_id:144438), which we shall denote as $Q$, is isomorphic to the [cyclic group](@entry_id:146728) of order $q$, i.e., $Q \cong \mathbb{Z}_q$.

For instance, consider any group of order $55 = 5 \times 11$. Here, $p=5$ and $q=11$. The number of Sylow 11-subgroups, $n_{11}$, must divide 5 and be congruent to $1 \pmod{11}$. The only integer satisfying both is $1$. Thus, any group of order 55, abelian or not, must possess a normal subgroup of order 11 [@problem_id:1606372].

### A Fundamental Dichotomy: The Structure of Sylow p-Subgroups

Having established the invariant nature of the Sylow $q$-subgroup $Q$, we now turn our attention to the Sylow $p$-subgroups, each of which we denote by $P$. A Sylow $p$-subgroup in $G$ has order $p$ and is thus isomorphic to $\mathbb{Z}_p$.

Again, applying Sylow's Third Theorem, the number of Sylow $p$-subgroups, $n_p$, must satisfy:
1.  $n_p$ must divide $q$. Since $q$ is prime, $n_p \in \{1, q\}$.
2.  $n_p \equiv 1 \pmod p$.

This presents a fundamental bifurcation. Unlike the case for $n_q$, both possibilities for $n_p$ can be viable under certain conditions. The structure of $G$ depends entirely on whether $n_p=1$ or $n_p=q$. This choice, in turn, is determined by a simple number-theoretic condition relating $p$ and $q$.

### Case 1: The Abelian Group via Direct Product

Let us first investigate the scenario where $n_p=1$. In this case, the Sylow $p$-subgroup $P$ is also unique and therefore normal in $G$. We now have a group $G$ with two [normal subgroups](@entry_id:147397), $P$ and $Q$, of coprime orders $p$ and $q$. By Lagrange's theorem, their intersection $P \cap Q$ must have an order dividing both $|P|=p$ and $|Q|=q$, so $|P \cap Q| = 1$ and $P \cap Q = \{e\}$, where $e$ is the [identity element](@entry_id:139321).

A standard result in group theory states that if a group $G$ is the product of two [normal subgroups](@entry_id:147397) $P$ and $Q$ with trivial intersection, then $G$ is isomorphic to their [external direct product](@entry_id:136624), $G \cong P \times Q$. Since elements of $P$ commute with elements of $Q$ in this construction, the group is abelian [@problem_id:1606371]. Given that $P \cong \mathbb{Z}_p$ and $Q \cong \mathbb{Z}_q$, we have:
$G \cong \mathbb{Z}_p \times \mathbb{Z}_q$

Furthermore, because $\gcd(p,q)=1$, the Chinese Remainder Theorem ensures that this direct product is itself cyclic:
$G \cong \mathbb{Z}_{pq}$

This leads to our first major classification result: if a group of order $pq$ has a normal Sylow $p$-subgroup, it must be the [cyclic group](@entry_id:146728) $\mathbb{Z}_{pq}$.

Under what conditions does this case occur? The condition $n_p=1$ is forced if the alternative, $n_p=q$, is impossible. The alternative $n_p=q$ is only possible if $q \equiv 1 \pmod p$, which is equivalent to $p$ dividing $q-1$. Consequently, if $p$ does not divide $q-1$, then $n_p$ cannot be $q$, forcing $n_p=1$.

Thus, if $p \nmid (q-1)$, any group of order $pq$ must be isomorphic to the abelian group $\mathbb{Z}_{pq}$.

For example, for any group of order $35 = 5 \times 7$, we have $p=5, q=7$. Since $5 \nmid (7-1)=6$, we must have $n_5=1$. As we already know $n_7=1$, both Sylow subgroups are normal, and any group of order 35 must be isomorphic to $\mathbb{Z}_{35}$ [@problem_id:1606367]. As a consequence, its subgroup structure is fixed: it has exactly one subgroup for each divisor of 35 (orders 1, 5, 7, 35), for a total of four subgroups. Similarly, for orders $33 = 3 \times 11$ and $51 = 3 \times 17$, since $3 \nmid (11-1)$ and $3 \nmid (17-1)$, the only group structure possible is the cyclic one [@problem_id:1606354].

### Case 2: The Non-Abelian Group via Semidirect Product

Now we consider the more intricate case where $p \mid (q-1)$. In this scenario, $q \equiv 1 \pmod p$ is a valid [congruence](@entry_id:194418), which allows for the possibility that $n_p=q$. If $n_p=q \gt 1$, the Sylow $p$-subgroup is not normal, and the group $G$ cannot be abelian. The existence of such a group is guaranteed by the construction of the **[semidirect product](@entry_id:147230)**.

Since $Q$ is a normal subgroup of $G$, the group $G$ can be described as a [semidirect product](@entry_id:147230) $G \cong Q \rtimes P$. This construction is determined by a [group homomorphism](@entry_id:140603) $\phi: P \to \text{Aut}(Q)$, which describes how elements of $P$ act on elements of $Q$ by conjugation.

Let's analyze the components:
-   The group $P$ is isomorphic to $\mathbb{Z}_p$.
-   The group $Q$ is isomorphic to $\mathbb{Z}_q$.
-   The [automorphism group](@entry_id:139672) $\text{Aut}(Q) \cong \text{Aut}(\mathbb{Z}_q)$ is isomorphic to the group of units $(\mathbb{Z}/q\mathbb{Z})^\times$, which is a [cyclic group](@entry_id:146728) of order $q-1$. So, $\text{Aut}(Q) \cong \mathbb{Z}_{q-1}$.

A homomorphism $\phi: \mathbb{Z}_p \to \mathbb{Z}_{q-1}$ is defined by mapping a generator of $\mathbb{Z}_p$ to an element in $\mathbb{Z}_{q-1}$ whose order divides $p$. A non-abelian structure arises from a **non-trivial** homomorphism, where the generator of $\mathbb{Z}_p$ is mapped to an element of order $p$ in $\mathbb{Z}_{q-1}$. Such an element of order $p$ exists in the [cyclic group](@entry_id:146728) $\mathbb{Z}_{q-1}$ if and only if $p$ divides its order, $q-1$.

This confirms our earlier deduction: a [non-abelian group](@entry_id:144791) of order $pq$ exists if and only if $p \mid (q-1)$. Examples include:
-   Order $10 = 2 \times 5$: $2 \mid (5-1)=4$. The non-abelian [dihedral group](@entry_id:143875) $D_5$ exists. [@problem_id:1606349]
-   Order $21 = 3 \times 7$: $3 \mid (7-1)=6$. A [non-abelian group](@entry_id:144791) of order 21 exists. [@problem_id:1606344]
-   Order $39 = 3 \times 13$: $3 \mid (13-1)=12$. A non-abelian group of order 39 exists. [@problem_id:1606355]

How many non-isomorphic [non-abelian groups](@entry_id:145211) are there? This corresponds to the number of non-isomorphic semidirect products, which in turn relates to the number of non-trivial homomorphisms from $\mathbb{Z}_p$ to $\text{Aut}(\mathbb{Z}_q)$ modulo an [equivalence relation](@entry_id:144135). In our case, the cyclic group $\mathbb{Z}_{q-1}$ has a unique subgroup of order $p$. While there are $p-1$ distinct elements of order $p$ that can serve as the image of a generator of $\mathbb{Z}_p$, it can be shown that all resulting non-trivial homomorphisms produce isomorphic semidirect products. Therefore, when $p \mid (q-1)$, there is **exactly one** [non-abelian group](@entry_id:144791) of order $pq$ up to [isomorphism](@entry_id:137127) [@problem_id:1819752].

This completes the classification:
-   If $p \nmid (q-1)$, there is one group of order $pq$: $\mathbb{Z}_{pq}$.
-   If $p \mid (q-1)$, there are two groups of order $pq$: $\mathbb{Z}_{pq}$ and a unique [non-abelian group](@entry_id:144791), $\mathbb{Z}_q \rtimes \mathbb{Z}_p$.

### Structural Anatomy of Groups of Order $pq$

With the classification established, we can delve deeper into the specific properties of these groups, focusing on the more complex non-abelian case.

#### Explicit Construction

The multiplication rule for the non-abelian group $G = \mathbb{Z}_q \rtimes_\phi \mathbb{Z}_p$ can be written explicitly. Let elements of $G$ be [ordered pairs](@entry_id:269702) $(a, b)$ with $a \in \mathbb{Z}_q$ and $b \in \mathbb{Z}_p$. The group operation is:
$$ (a, b) \cdot (a', b') = (a + \phi_b(a'), b + b') $$
Here, $\phi_b$ is the [automorphism](@entry_id:143521) of $\mathbb{Z}_q$ corresponding to $b \in \mathbb{Z}_p$. Since $\text{Aut}(\mathbb{Z}_q)$ is isomorphic to multiplication by units modulo $q$, we can write this as:
$$ (a, b) \cdot (a', b') = (a + k^b a' \pmod q, b + b' \pmod p) $$
For this to define a [non-abelian group](@entry_id:144791), the integer $k$ must be an element of order $p$ in the [multiplicative group](@entry_id:155975) $(\mathbb{Z}/q\mathbb{Z})^\times$. For instance, to construct the non-abelian group of order 21, we need to find an integer $k$ such that $1  k  7$, $k^3 \equiv 1 \pmod 7$, and $k \not\equiv 1 \pmod 7$. The values $k=2$ and $k=4$ satisfy these conditions, leading to the same group structure [@problem_id:1606347].

#### Element Orders and Subgroup Lattices

The structure of a group is reflected in its set of element orders and its [lattice of subgroups](@entry_id:137113). The two types of groups of order $pq$ differ starkly in this regard.

In the abelian case, $\mathbb{Z}_{pq}$, the subgroups are in one-to-one correspondence with the divisors of $pq$. The divisors are $1, p, q, pq$, so there are exactly four subgroups, including the [trivial subgroup](@entry_id:141709) and the group itself.

In the non-abelian case, where $n_p=q$, the subgroup structure is richer. The group contains:
-   One [normal subgroup](@entry_id:144438) of order $q$.
-   $q$ distinct subgroups of order $p$ (the Sylow $p$-subgroups).

Let's count the elements. The single Sylow $q$-subgroup contains $q-1$ elements of order $q$. The $q$ Sylow $p$-subgroups are distinct, and any two can only intersect at the identity element. Each contains $p-1$ elements of order $p$. This gives a total of $q(p-1)$ elements of order $p$. Together with the identity, we have accounted for all $1 + (q-1) + q(p-1) = q + pq - q = pq$ elements of the group.

For example, in a non-abelian group of order 21 ($p=3, q=7$), there are $n_3=7$ Sylow 3-subgroups. This gives $7 \times (3-1) = 14$ elements of order 3 [@problem_id:1606344]. Contrast this with a group of order 10. The cyclic group $\mathbb{Z}_{10}$ has two proper, non-trivial subgroups (of orders 2 and 5). The non-abelian [dihedral group](@entry_id:143875) $D_5$ has one subgroup of order 5 and five subgroups of order 2, for a total of six proper, non-trivial subgroups, showcasing a more complex internal structure [@problem_id:1606349].

#### Conjugacy Class Structure

The [partition of a group](@entry_id:136646) into conjugacy classes is another fundamental structural property. For a non-abelian group $G$ of order $pq$ (with $p \mid q-1$), the sizes of the [conjugacy classes](@entry_id:143916) are highly constrained. The size of the conjugacy class of an element $x$ is given by the index of its centralizer, $[G:C_G(x)]$.

1.  **The Identity**: The identity element $e$ is always in its own class of size 1.
2.  **Elements in $Q$**: For any non-identity element $x \in Q$, its centralizer $C_G(x)$ contains all of $Q$. Because the action of $P$ on $Q$ is non-trivial, no element of $P \setminus \{e\}$ centralizes any element of $Q \setminus \{e\}$. Thus, $C_G(x) = Q$. The size of its conjugacy class is $[G:Q] = \frac{pq}{q} = p$.
3.  **Elements of Order $p$**: For any element $y$ of order $p$, it belongs to some Sylow $p$-subgroup $P_i = \langle y \rangle$. Its [centralizer](@entry_id:146604) $C_G(y)$ contains $P_i$. It can be shown that for such an element, $C_G(y) = P_i$. The size of its conjugacy class is $[G:P_i] = \frac{pq}{p} = q$.

In summary, for any non-abelian group of order $pq$, the possible sizes of the conjugacy classes are precisely $1$, $p$, and $q$ [@problem_id:1606343]. The [class equation](@entry_id:144428) for such a group is $pq = 1 + k \cdot p + m \cdot q$ for some integers $k, m$.

#### Solvability and Nilpotency

The concepts of solvability and [nilpotency](@entry_id:147926) provide a coarser classification of groups. A group is **solvable** if it has a subnormal series with abelian factors. A group is **nilpotent** if its [upper central series](@entry_id:139682) terminates at the group itself; for [finite groups](@entry_id:139710), this is equivalent to being the [direct product](@entry_id:143046) of its Sylow subgroups.

All groups of order $pq$ are solvable. This is a specific case of Burnside's $p^a q^b$ theorem, but it can be seen directly from our analysis. The series $G \triangleright Q \triangleright \{e\}$ is a subnormal series where the [factor groups](@entry_id:146225) are $G/Q \cong \mathbb{Z}_p$ and $Q/\{e\} \cong \mathbb{Z}_q$. Since these factors are abelian, the group $G$ is solvable.

A group of order $pq$ is nilpotent if and only if it is abelian. Nilpotency requires all Sylow subgroups to be normal. This is precisely our "Case 1" ($n_p=1$ and $n_q=1$), which led to the abelian group $\mathbb{Z}_{pq}$. The [non-abelian group](@entry_id:144791), which exists when $p \mid (q-1)$, has a non-normal Sylow $p$-subgroup ($n_p=q$) and is therefore not nilpotent.

This provides a ready-made family of groups that are solvable but not nilpotent, a distinction crucial in various advanced topics and applications, including [cryptography](@entry_id:139166). For instance, [non-abelian groups](@entry_id:145211) of orders $34 = 2 \times 17$, $38 = 2 \times 19$, and $39 = 3 \times 13$ are all solvable but not nilpotent, as in each case $p \mid (q-1)$ [@problem_id:1606354].