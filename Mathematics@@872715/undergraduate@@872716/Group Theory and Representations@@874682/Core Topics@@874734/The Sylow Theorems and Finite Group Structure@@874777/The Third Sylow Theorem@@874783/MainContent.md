## Introduction
The Sylow theorems are a cornerstone of [finite group theory](@entry_id:146601), providing deep insights into the structure of groups by examining their subgroups of prime-power order. While the First and Second Sylow Theorems establish the existence and conjugacy of these subgroups, a crucial question remains: how many such subgroups can exist? This article addresses this question by focusing on the Third Sylow Theorem, a powerful result that places strict arithmetic constraints on the number of Sylow $p$-subgroups, revealing profound information about a group's internal architecture. We will first explore the **Principles and Mechanisms** behind the theorem, using [group actions](@entry_id:268812) to derive its divisibility and [congruence](@entry_id:194418) conditions. Next, we will survey its broad utility in **Applications and Interdisciplinary Connections**, from proving groups are not simple to uncovering its relevance in geometry and chemistry. Finally, you will apply these concepts in a series of **Hands-On Practices** to solidify your understanding and build problem-solving skills.

## Principles and Mechanisms

Following the establishment of the existence of Sylow $p$-subgroups (the First Sylow Theorem) and the relationship between them through conjugation (the Second Sylow Theorem), we now turn to the third and perhaps most powerful of these foundational results. The Third Sylow Theorem provides remarkably strong arithmetic constraints on the number of Sylow $p$-subgroups a finite group can possess. These constraints are not merely numerical curiosities; they are deep reflections of the group's internal structure and are instrumental in analyzing and [classifying finite groups](@entry_id:142836).

Let $G$ be a finite group of order $|G|$, and let $p$ be a prime divisor of $|G|$. We can write the order of the group as $|G| = p^k m$, where $p^k$ is the highest power of $p$ that divides $|G|$, meaning $\gcd(p, m) = 1$. Let $n_p$ denote the number of distinct Sylow $p$-subgroups of $G$. The Third Sylow Theorem states that:

1.  The number of Sylow $p$-subgroups, $n_p$, divides the index of the Sylow $p$-subgroup, which is $m$. Thus, **$n_p | m$**.
2.  The number of Sylow $p$-subgroups satisfies the congruence **$n_p \equiv 1 \pmod p$**.

In this chapter, we will dissect the mechanisms that give rise to these two conditions. We will then explore their profound consequences, demonstrating how these simple arithmetic rules can be used to unravel the complex [structure of finite groups](@entry_id:137958).

### The Divisibility Condition: An Orbit-Stabilizer Perspective

The first condition, $n_p | m$, arises from the fundamental interplay between [group actions](@entry_id:268812), orbits, and stabilizers. The Second Sylow Theorem states that all Sylow $p$-subgroups are conjugate to one another. This can be rephrased in the language of [group actions](@entry_id:268812): the group $G$ acts on the set of its own subgroups by conjugation. Under this action, the set of all Sylow $p$-subgroups, which we denote as $Syl_p(G)$, forms a single orbit.

Let $P$ be any Sylow $p$-subgroup. The **Orbit-Stabilizer Theorem** states that the size of the orbit of $P$ is equal to the index of its stabilizer in $G$. The orbit of $P$ is the set of all its conjugates, $\{gPg^{-1} : g \in G\}$, which is precisely the set $Syl_p(G)$. Therefore, the size of the orbit is $n_p$. The stabilizer of $P$ under this action is the set of elements $g \in G$ that fix $P$, i.e., for which $gPg^{-1} = P$. This is by definition the **normalizer** of $P$ in $G$, denoted $N_G(P)$.

Applying the Orbit-Stabilizer Theorem gives us the crucial identity:

$$ n_p = |Syl_p(G)| = [G:N_G(P)] = \frac{|G|}{|N_G(P)|} $$

This formula is the direct mechanism behind the divisibility condition. We know that $P$ is a subgroup of its own normalizer, $P \le N_G(P)$. By Lagrange's Theorem, the order of $P$, $|P|=p^k$, must divide the order of $N_G(P)$. Thus, we can write $|N_G(P)| = p^k \cdot r$ for some integer $r$. Crucially, since $P$ is a Sylow $p$-subgroup of $G$, it is also a Sylow $p$-subgroup of any subgroup containing it, including $N_G(P)$. This implies that $r$ cannot be divisible by $p$. Now, substituting this into our formula for $n_p$:

$$ n_p = \frac{|G|}{|N_G(P)|} = \frac{p^k m}{p^k r} = \frac{m}{r} $$

This equation reveals that $n_p$ is a divisor of $m$, which is the first part of the Third Sylow Theorem.

This relationship between $n_p$ and the normalizer is a powerful computational tool. For instance, consider a hypothetical group $G$ of order $|G|=132 = 2^2 \cdot 3 \cdot 11$. Let $P$ be a Sylow 11-subgroup, so $|P|=11$. If we were given structural information that the normalizer of $P$ is $P$ itself (i.e., $N_G(P) = P$), we could immediately determine the number of Sylow 11-subgroups. Using the formula, we find:

$$ n_{11} = [G:N_G(P)] = \frac{|G|}{|P|} = \frac{132}{11} = 12 $$

There must be exactly 12 Sylow 11-subgroups in such a group [@problem_id:1824823]. This result is consistent with the Sylow conditions, as $12 | (132/11) = 12$ and $12 \equiv 1 \pmod{11}$.

A noteworthy property related to normalizers of Sylow subgroups is that they are "self-normalizing". For any Sylow $p$-subgroup $P$, it can be proven that $N_G(N_G(P)) = N_G(P)$. This means that the normalizer of $P$ cannot be a proper [normal subgroup](@entry_id:144438) of any larger subgroup of $G$. To see this, let $K = N_G(P)$. Since $P$ is a Sylow $p$-subgroup of $G$ contained in $K$, it is also a Sylow $p$-subgroup of $K$. As $P$ is normal in $K$ by definition of the normalizer, it is the *unique* Sylow $p$-subgroup of $K$. Now, consider an element $g \in N_G(K)$. Then $gKg^{-1}=K$. The subgroup $gPg^{-1}$ must be contained in $gKg^{-1}=K$. Since $gPg^{-1}$ is also a Sylow $p$-subgroup of $G$, and hence of $K$, its uniqueness in $K$ implies that $gPg^{-1}=P$. But this means $g$ is in the normalizer of $P$, so $g \in K$. This shows $N_G(K) \subseteq K$, and since the reverse inclusion is always true, we have $N_G(K)=K$ [@problem_id:1655663].

### The Congruence Condition: A Proof via Group Action

The second condition, $n_p \equiv 1 \pmod p$, is more subtle. Its most intuitive proof also relies on the concept of a [group action](@entry_id:143336), but with a clever choice of the acting group. Let $X = Syl_p(G)$ be the set of all $n_p$ Sylow $p$-subgroups. Instead of letting the full group $G$ act on this set, let us fix one Sylow $p$-subgroup, $P$, and let *it* act on the set $X$ by conjugation.

This action partitions the set $X$ into disjoint orbits. According to the Orbit-Stabilizer Theorem, the size of any orbit must divide the order of the acting group, which is $|P| = p^k$. Therefore, the size of every orbit is a power of $p$: $1, p, p^2, \ldots, p^k$.

Next, let's identify the fixed points of this action—that is, the orbits of size 1. A Sylow $p$-subgroup $Q \in X$ is a fixed point if and only if $gQg^{-1} = Q$ for all elements $g \in P$. This is equivalent to the condition that $P$ is a subgroup of the normalizer of $Q$, i.e., $P \le N_G(Q)$.

Now, consider the group $N_G(Q)$. Both $P$ and $Q$ are subgroups of $N_G(Q)$. Since their order, $p^k$, is the maximal power of $p$ dividing $|G|$, they are also Sylow $p$-subgroups of $N_G(Q)$. By its very definition, $Q$ is a normal subgroup of $N_G(Q)$. A fundamental property of [finite groups](@entry_id:139710) is that if a Sylow $p$-subgroup is normal, it must be the *unique* Sylow $p$-subgroup. Therefore, within the group $N_G(Q)$, $Q$ is the only Sylow $p$-subgroup. This forces $P$ to be equal to $Q$.

This elegant argument shows that the only Sylow $p$-subgroup fixed by the action of $P$ is $P$ itself. Thus, there is exactly one orbit of size 1, which is the set $\{P\}$.

Since the orbits partition the set $X$, the sum of their sizes must equal the total number of elements, $n_p$. We have one orbit of size 1, and all other orbits have sizes that are positive powers of $p$. This gives us the equation:

$$ n_p = \underbrace{1}_{\text{orbit } \{P\}} + \underbrace{\sum_{i} p^{k_i}}_{\text{other orbits}} $$

where each $k_i \ge 1$. The sum on the right is clearly a multiple of $p$. Therefore, we conclude that $n_p \equiv 1 \pmod p$, proving the second part of the theorem.

As a concrete illustration, suppose a group $G$ has $n_7 = 8$ Sylow 7-subgroups. Let $P$ be one of them. When $P$ acts on the set of these 8 subgroups, the set must be partitioned into orbits whose sizes are powers of 7 (in this case, 1 or 7). We know there is exactly one orbit of size 1, namely $\{P\}$. The remaining $8-1=7$ subgroups must therefore form a single orbit of size 7. The partition of the 8 subgroups is $8 = 1 + 7$, which is perfectly consistent with the congruence $8 \equiv 1 \pmod 7$ [@problem_id:1655660].

An alternative, more [combinatorial proof](@entry_id:264037) of the [congruence](@entry_id:194418) condition can be constructed using the double [coset](@entry_id:149651) decomposition of $G$ with respect to a Sylow $p$-subgroup $P$. This involves analyzing the index formula $[G:P] = \sum_{x \in S} [P : P \cap xPx^{-1}]$, where $S$ is a set of double coset representatives. By partitioning the sum based on whether $x$ belongs to the normalizer of $P$, one can again derive the result $n_p \equiv 1 \pmod p$ [@problem_id:1824789].

### Applications and Structural Consequences

The true power of the Third Sylow Theorem lies in its application. These two simple arithmetic rules provide a powerful lens for examining the internal structure of a [finite group](@entry_id:151756), often allowing us to prove the existence of normal subgroups or to drastically limit the structural possibilities for a group of a given order.

#### Constraining the Number of Sylow Subgroups

For any [finite group](@entry_id:151756) $G$, we can immediately write down a list of arithmetically possible values for $n_p$ for each prime $p$ dividing $|G|$. This process can significantly narrow our search for the group's structure.

Consider a group of order $|G| = 399$. The [prime factorization](@entry_id:152058) is $399 = 3 \cdot 7 \cdot 19$. Let's determine the possible values for $n_3, n_7,$ and $n_{19}$.

*   For $p=3$: $n_3$ must divide $\frac{399}{3} = 133 = 7 \cdot 19$, and $n_3 \equiv 1 \pmod 3$. The divisors of 133 are $1, 7, 19, 133$. Checking the [congruence](@entry_id:194418):
    *   $1 \equiv 1 \pmod 3$ (possible)
    *   $7 \equiv 1 \pmod 3$ (possible)
    *   $19 \equiv 1 \pmod 3$ (possible)
    *   $133 = 3 \cdot 44 + 1 \equiv 1 \pmod 3$ (possible)
    So, $n_3 \in \{1, 7, 19, 133\}$.

*   For $p=7$: $n_7$ must divide $\frac{399}{7} = 57 = 3 \cdot 19$, and $n_7 \equiv 1 \pmod 7$. The divisors of 57 are $1, 3, 19, 57$. Checking the [congruence](@entry_id:194418):
    *   $1 \equiv 1 \pmod 7$ (possible)
    *   $3 \not\equiv 1 \pmod 7$
    *   $19 = 2 \cdot 7 + 5 \not\equiv 1 \pmod 7$
    *   $57 = 8 \cdot 7 + 1 \equiv 1 \pmod 7$ (possible)
    So, $n_7 \in \{1, 57\}$.

*   For $p=19$: $n_{19}$ must divide $\frac{399}{19} = 21 = 3 \cdot 7$, and $n_{19} \equiv 1 \pmod{19}$. The divisors of 21 are $1, 3, 7, 21$. The only one satisfying the [congruence](@entry_id:194418) is $1$. So, $n_{19}=1$.

Any group of order 399 must have exactly one Sylow 19-subgroup. A tuple of values $(n_3, n_7, n_{19})$ representing a possible group structure must therefore be of the form $(a, b, 1)$, where $a \in \{1, 7, 19, 133\}$ and $b \in \{1, 57\}$. For example, the tuple $(7, 57, 1)$ is arithmetically possible, whereas $(7, 1, 19)$ is not [@problem_id:1824850].

This process can also definitively rule out certain scenarios. For a group of order $|G|=396 = 2^2 \cdot 3^2 \cdot 11$, let's consider $n_{11}$. It must divide $\frac{396}{11} = 36$ and satisfy $n_{11} \equiv 1 \pmod{11}$. The divisors of 36 are $1, 2, 3, 4, 6, 9, 12, 18, 36$. Of these, only $1$ and $12$ are congruent to $1$ modulo $11$. Therefore, for any group of order 396, it is mathematically impossible for it to contain, for example, exactly 3 Sylow 11-subgroups [@problem_id:1655710].

#### Immediate Corollaries of the Congruence

The condition $n_p \equiv 1 \pmod p$ leads to some interesting immediate consequences that further constrain the value of $n_p$.

First, for any prime $p$, it is impossible for $n_p$ to be equal to $p$. If we assume $n_p=p$, the [congruence](@entry_id:194418) condition would require $p \equiv 1 \pmod p$. By definition of [modular arithmetic](@entry_id:143700), this would mean that $p$ divides $(p-1)$. This is impossible for any prime $p$, as $p-1$ is a smaller positive integer. Therefore, the number of Sylow $p$-subgroups can never be $p$ [@problem_id:1824822].

A slight generalization of this reasoning shows that $n_p$ can never be equal to another prime $q$ such that $1  q  p$. If we were to assume $n_p = q$, the [congruence](@entry_id:194418) $q \equiv 1 \pmod p$ would imply that $p$ divides $(q-1)$. But since $0  q-1  p$, this is impossible. This is why, in our previous example of a group of order 396, $n_{11}$ could not be 3 [@problem_id:1655710].

#### A Powerful Tool for Proving Non-Simplicity

Perhaps the most significant application of the Sylow theorems is in determining whether a group has a non-trivial proper normal subgroup. A group that does not is called a **simple group**. Simple groups are the "building blocks" of all finite groups, and their classification is one of the monumental achievements of modern mathematics.

The connection is straightforward:
A Sylow $p$-subgroup $P$ is normal in $G$ if and only if it is the only Sylow $p$-subgroup, i.e., if and only if **$n_p=1$**.

The reasoning is clear: if $P$ is normal, it is equal to all its conjugates, so it must be unique. Conversely, if $P$ is unique, it must be equal to all its conjugates (since all Sylow $p$-subgroups are conjugate), which is the definition of a [normal subgroup](@entry_id:144438).

Therefore, if we can use the Third Sylow Theorem to show that $n_p=1$ for some prime $p$ dividing $|G|$, we have successfully proven that $G$ is not simple.

Let's examine a group $G$ of order $|G|=21=3 \cdot 7$.
*   For $p=7$, $n_7$ must divide 3 and $n_7 \equiv 1 \pmod 7$. The only possibility is $n_7=1$. Thus, any group of order 21 must have a normal Sylow 7-subgroup.
*   For $p=3$, $n_3$ must divide 7 and $n_3 \equiv 1 \pmod 3$. The divisors of 7 are 1 and 7. Both satisfy the congruence: $1 \equiv 1 \pmod 3$ and $7 \equiv 1 \pmod 3$. So, $n_3 \in \{1, 7\}$.

Now, suppose we are given the additional information that $G$ is non-abelian. If $n_3=1$, then both the Sylow 3-subgroup and the Sylow 7-subgroup would be normal. Since their orders are coprime, their intersection is trivial, and their product is the whole group. This implies $G$ would be isomorphic to the [direct product](@entry_id:143046) of its Sylow subgroups, $G \cong C_3 \times C_7 \cong C_{21}$, which is an abelian group. This contradicts our premise. Therefore, the case $n_3=1$ is impossible, and we must conclude that for a [non-abelian group](@entry_id:144791) of order 21, $n_3=7$ [@problem_id:1655709].

### Advanced Topics and Connections

The Sylow theorems serve as a gateway to more advanced structural group theory. Their principles connect deeply with the study of normal subgroups, [quotient groups](@entry_id:145113), and [group actions](@entry_id:268812).

#### Sylow Theory and Normal Subgroups

The theorems behave predictably with respect to normal subgroups under certain arithmetic conditions. Let $K$ be a [normal subgroup](@entry_id:144438) of $G$, and suppose the order of $K$ and the index of $K$ in $G$ are coprime, i.e., $\gcd(|K|, [G:K])=1$. Let $p$ be a prime that divides $|K|$.

Because $\gcd(|K|, |G|/|K|)=1$, the prime $p$ cannot divide $|G/K|$. Let $P$ be any Sylow $p$-subgroup of $G$. Consider its image in the [quotient group](@entry_id:142790) $G/K$ under the natural projection map. This image is a $p$-subgroup of $G/K$. But since the order of $G/K$ is not divisible by $p$, the only $p$-subgroup it can contain is the trivial one. This implies that the image of $P$ is trivial, which means $P$ must be entirely contained within the kernel of the map, so $P \le K$.

Since $P$ is a Sylow $p$-subgroup of $G$, its order $p^k$ is the highest power of $p$ dividing $|G|$. The coprime condition ensures that $p^k$ is also the highest power of $p$ dividing $|K|$. Thus, $P$ is also a Sylow $p$-subgroup of $K$. This shows that every Sylow $p$-subgroup of $G$ is also a Sylow $p$-subgroup of $K$. The converse is trivial. Therefore, the set of Sylow $p$-subgroups of $G$ is identical to the set of Sylow $p$-subgroups of $K$. This leads to the elegant conclusion:

$$ n_p(G) = n_p(K) $$

This result, a consequence of the Frattini argument, is extremely useful for relating the structure of a group to the structure of its [normal subgroups](@entry_id:147397) [@problem_id:1655690].

#### The Group Action on Cosets and the Core of the Normalizer

Revisiting the action of $G$ on the set $X=Syl_p(G)$ by conjugation provides a final, deep insight. This action is equivalent to an action on the set of left [cosets](@entry_id:147145) of the normalizer $H=N_G(P)$. This action defines a homomorphism $\phi: G \to S_{n_p}$, where $S_{n_p}$ is the [symmetric group](@entry_id:142255) on $n_p$ elements.

The kernel of this homomorphism, $\ker(\phi)$, consists of all elements in $G$ that fix every Sylow $p$-subgroup simultaneously. The kernel of the action is thus the intersection of the normalizers of all Sylow $p$-subgroups:
$$ \ker(\phi) = \bigcap_{Q \in Syl_p(G)} N_G(Q) $$
Since all Sylow $p$-subgroups are conjugate, say $Q = gPg^{-1}$, their normalizers are also conjugate: $N_G(Q) = gN_G(P)g^{-1}$. Therefore, the kernel is the intersection of all conjugates of $H=N_G(P)$, which is by definition the **core** of $H$ in $G$, denoted $K = \text{core}_G(H)$.

By the First Isomorphism Theorem, $G/K$ is isomorphic to a subgroup of $S_{n_p}$. This immediately implies that the order of the [quotient group](@entry_id:142790), $|G/K| = [G:K]$, must divide the order of $S_{n_p}$, which is $(n_p)!$. So, we have the relation:
$$ [G:K] \text{ divides } (n_p)! $$
Furthermore, we know that $n_p = [G:H]$. From the subgroup tower $K \le H \le G$, we have the [tower law](@entry_id:150838) for indices: $[G:K] = [G:H][H:K] = n_p[H:K]$. This shows a second relation:
$$ n_p \text{ divides } [G:K] $$
These two conditions, taken together, place strong constraints on the index of the largest normal subgroup of $G$ that is contained in $N_G(P)$. For example, in the simple group $G=A_5$, for $p=5$, we have $n_5=6$. The normalizer $H=N_{A_5}(P)$ has order 10. Since $A_5$ is simple, the core $K$ must be the [trivial subgroup](@entry_id:141709), so $[G:K]=|G|=60$. We can check that $n_5=6$ indeed divides $60$, and $[G:K]=60$ indeed divides $(n_5)! = 6! = 720$ [@problem_id:1655677]. This line of reasoning is a cornerstone in the study of [finite simple groups](@entry_id:143576).