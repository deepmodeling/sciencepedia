## Introduction
In the world of number theory, the concept of [modular arithmetic](@entry_id:143700)—the arithmetic of remainders—provides a powerful lens for understanding the integers. By partitioning all integers into a finite number of [congruence classes](@entry_id:635978) modulo some integer n, we simplify complex problems into a manageable, finite system. However, to work effectively with these abstract classes, we need concrete sets of representatives. This need gives rise to two fundamental structures: complete residue systems, which represent every class, and reduced residue systems, which represent only the classes that are invertible. Understanding the distinction and relationship between these systems is crucial for unlocking deeper insights into number theory and its applications.

This article provides a structured exploration of complete and reduced residue systems, designed to build a solid theoretical and practical foundation. The journey is divided into three parts. First, in "Principles and Mechanisms," we will formally define these systems, examining their core properties, methods of construction, and behavior under key arithmetic transformations. Next, "Applications and Interdisciplinary Connections" will demonstrate the power of these concepts by applying them to prove classical theorems, solve [systems of congruences](@entry_id:154048) using the Chinese Remainder Theorem, and lay the groundwork for modern cryptography. Finally, "Hands-On Practices" will offer you the chance to solidify your understanding through guided computational and theoretical exercises, translating abstract knowledge into practical skill.

## Principles and Mechanisms

In the study of [modular arithmetic](@entry_id:143700), the partitioning of the integers $\mathbb{Z}$ into [congruence classes](@entry_id:635978) modulo an integer $n$ is a foundational concept. To work effectively with these classes, it is often necessary to select a specific integer to represent each class. Such a set of representatives is known as a **[residue system](@entry_id:637054)**. Depending on which classes we wish to represent, we arrive at two fundamental structures: complete residue systems and reduced residue systems. This chapter will elucidate the principles governing these systems and the mechanisms by which they are constructed and transformed.

### Complete Residue Systems

A **[complete residue system](@entry_id:188246) (CRS)** modulo $n$ provides a full set of representatives for all the [congruence classes](@entry_id:635978) in $\mathbb{Z}/n\mathbb{Z}$.

#### Definition and Core Properties

Formally, a set of integers $S$ is a **[complete residue system](@entry_id:188246) modulo $n$** if every integer is congruent modulo $n$ to exactly one element of $S$ [@problem_id:3083601]. This single condition implies two crucial properties. First, the set of [residue classes](@entry_id:185226) represented by elements of $S$ must cover all of $\mathbb{Z}/n\mathbb{Z}$ ([surjectivity](@entry_id:148931)). Second, distinct elements in $S$ must represent distinct [residue classes](@entry_id:185226) (injectivity).

Since there are precisely $n$ distinct [congruence classes](@entry_id:635978) modulo $n$, it follows that any [complete residue system](@entry_id:188246) must contain exactly $n$ integers. This leads to a practical, equivalent definition: a set $S$ of $n$ integers is a [complete residue system](@entry_id:188246) modulo $n$ if and only if its elements are pairwise incongruent modulo $n$ [@problem_id:3083601] [@problem_id:3084975]. This means that for any two distinct elements $s_i, s_j \in S$, it is the case that $s_i \not\equiv s_j \pmod{n}$. From an algebraic perspective, if we consider the reduction map $r_n: \mathbb{Z} \to \mathbb{Z}/n\mathbb{Z}$ that sends an integer to its [congruence](@entry_id:194418) class, a set $S \subset \mathbb{Z}$ with $|S|=n$ is a CRS if and only if the restriction of this map to $S$, denoted $r_n|_S$, is a bijection [@problem_id:3083601].

The most familiar example of a CRS is the set of least non-negative residues, $S = \{0, 1, 2, \dots, n-1\}$. However, the choice of representatives is not unique. For instance, for $n=7$, the set $S = \{-3, -2, -1, 0, 1, 2, 3\}$ is also a valid CRS, as its elements are congruent to $\{4, 5, 6, 0, 1, 2, 3\}$ modulo $7$, which is merely a permutation of the standard residues [@problem_id:3083421]. The definition does not require the representatives to fall within any particular range.

The condition of pairwise incongruence is essential. Consider for $n=8$ the multiset of numbers $\{0, 1, 2, 3, 4, 5, 6, 6\}$. This collection contains $8$ numbers, but it fails to be a CRS because the element $6$ is repeated, violating pairwise incongruence. By [the pigeonhole principle](@entry_id:268698), since two numbers map to the residue class $[6]_8$, some other residue class must be unrepresented—in this case, $[7]_8$ is missing [@problem_id:3083421].

#### Transformations of Complete Residue Systems

Understanding how basic arithmetic operations affect a CRS provides insight into their structure.

**Translation**: If $S$ is a [complete residue system](@entry_id:188246) modulo $n$, then for any integer $c$, the translated set $S+c = \{s+c \mid s \in S\}$ is also a [complete residue system](@entry_id:188246) modulo $n$ [@problem_id:3010587]. The proof is straightforward. The set $S+c$ clearly has $n$ elements. Suppose two elements are congruent: $s_i+c \equiv s_j+c \pmod{n}$. The laws of [modular arithmetic](@entry_id:143700) permit subtracting $c$ from both sides, yielding $s_i \equiv s_j \pmod{n}$. Since $S$ is a CRS, its elements are pairwise incongruent, so this can only be true if $i=j$. Thus, the elements of $S+c$ are also pairwise incongruent, and $S+c$ is a CRS. This holds for any integer $c$, irrespective of its relationship with $n$ [@problem_id:3083601].

**Scaling**: The effect of scaling a CRS is more nuanced. Let $S$ be a CRS and $k$ be an integer. The scaled set is $kS = \{ks \mid s \in S\}$. The set $kS$ is a [complete residue system](@entry_id:188246) modulo $n$ if and only if the [greatest common divisor](@entry_id:142947) $\gcd(k,n)=1$ [@problem_id:3083601].

To see why, first assume $\gcd(k,n)=1$. This means $k$ has a multiplicative inverse modulo $n$, an integer $k^{-1}$ such that $kk^{-1} \equiv 1 \pmod{n}$. If we suppose $ks_i \equiv ks_j \pmod{n}$ for $s_i, s_j \in S$, we can multiply by $k^{-1}$ to find $s_i \equiv s_j \pmod{n}$. As before, this implies $i=j$. So, the elements of $kS$ are pairwise incongruent, and $kS$ is a CRS.

Conversely, assume $kS$ is a CRS. We must show $\gcd(k,n)=1$. Suppose for contradiction that $\gcd(k,n) = d > 1$. Let $S = \{0, 1, \dots, n-1\}$. The elements $s_1=0$ and $s_2=n/d$ are distinct elements of $S$ since $1 \le n/d  n$. However, when scaled by $k$, we find $ks_1 = 0$ and $ks_2 = k(n/d) = (k/d)n \equiv 0 \pmod{n}$. Thus, two distinct elements of $S$ are mapped to the same congruence class, which means $kS$ cannot represent all $n$ distinct classes. This contradicts the assumption that $kS$ is a CRS. Therefore, we must have $\gcd(k,n)=1$.

This principle is powerfully illustrated by considering a set like $S = \{21k + 7 \mid 0 \le k \le 104\}$ modulo $n=105$ [@problem_id:3083424]. This set has $105$ elements. We can analyze it as a translation of the scaled set $\{21k\}$. Here, the scaling factor is $a=21$. Since $\gcd(21, 105) = 21 \neq 1$, the set $\{21k \mid 0 \le k \le 104\}$ is not a CRS. The congruence $21k_1 \equiv 21k_2 \pmod{105}$ simplifies to $105 \mid 21(k_1-k_2)$, which further simplifies to $5 \mid (k_1-k_2)$, or $k_1 \equiv k_2 \pmod 5$. This means that the residues of the elements repeat every 5 values of $k$. Consequently, the set only represents $105/21 = 5$ distinct [residue classes](@entry_id:185226), namely $\{7, 28, 49, 70, 91\}$, each appearing $21$ times.

### Reduced Residue Systems

While a CRS represents all integers modulo $n$, a **[reduced residue system](@entry_id:635195) (RRS)** represents only those integers that are invertible modulo $n$.

#### Definition and Relation to Units

An integer $a$ is invertible modulo $n$ if and only if $\gcd(a,n)=1$. These [congruence classes](@entry_id:635978) form a group under multiplication, known as the **[group of units](@entry_id:140130)** of $\mathbb{Z}/n\mathbb{Z}$, denoted $(\mathbb{Z}/n\mathbb{Z})^{\times}$. The order of this group is given by **Euler's totient function**, $\varphi(n)$, which counts the number of positive integers up to $n$ that are [relatively prime](@entry_id:143119) to $n$.

A **[reduced residue system](@entry_id:635195) modulo $n$** is a set of $\varphi(n)$ integers, each [relatively prime](@entry_id:143119) to $n$ and pairwise incongruent modulo $n$ [@problem_id:3084975]. In essence, an RRS is any set of integer representatives for the elements of the group of units, $(\mathbb{Z}/n\mathbb{Z})^{\times}$ [@problem_id:3083581]. The mapping from an RRS, $R$, to the [group of units](@entry_id:140130), $(\mathbb{Z}/n\mathbb{Z})^{\times}$, given by $r \mapsto [r]_n$ is a bijection [@problem_id:3083581].

For example, let $n=8$. The integers from $1$ to $8$ that are coprime to $8$ are $1, 3, 5, 7$. Thus, $\varphi(8)=4$.
- A CRS for $n=8$ could be $\{0, 1, 2, 3, 4, 5, 6, 7\}$, with size $n=8$.
- An RRS for $n=8$ could be $\{1, 3, 5, 7\}$, with size $\varphi(8)=4$. Another valid RRS would be $\{-3, -1, 1, 3\}$, as these are congruent to $\{5, 7, 1, 3\}$ modulo 8 and are all coprime to 8 [@problem_id:3084905].

It is critical to distinguish an RRS from a CRS. An RRS contains only integers coprime to $n$, while a CRS must contain representatives for all classes, including non-invertible ones (like $[0]_n, [2]_n, [4]_n, [6]_n$ for $n=8$). The only case where a CRS and RRS are nearly the same is when $n$ is prime. For a prime $p$, an RRS has size $\varphi(p)=p-1$, while a CRS has size $p$. The CRS contains a representative for $[0]_p$, which the RRS excludes.

The ratio of the size of an RRS to a CRS is $\varphi(n)/n$. This value has a remarkable product formula over the distinct prime divisors of $n$:
$$ \frac{\varphi(n)}{n} = \prod_{p | n} \left(1 - \frac{1}{p}\right) $$
This formula, derivable from the [principle of inclusion-exclusion](@entry_id:276055), quantifies the density of invertible elements modulo $n$ [@problem_id:3084975].

While the set of residues of an RRS forms a group under modular multiplication, it is important to note that the set of integer representatives itself is generally not closed under standard multiplication. For example, with $n=5$, a valid RRS is $R = \{1, 2, 3, 4\}$. The product of two elements, $2 \times 3 = 6$, is not in $R$. Of course, $6 \equiv 1 \pmod 5$, and $[1]_5$ is an element of the [group of units](@entry_id:140130) [@problem_id:3083581].

#### Transformations of Reduced Residue Systems

The behavior of an RRS under transformations reveals deeper structural properties connected to the [group of units](@entry_id:140130).

**Scaling**: If $R$ is a [reduced residue system](@entry_id:635195) modulo $n$ and $a$ is an integer with $\gcd(a,n)=1$, then the scaled set $aR = \{ar \mid r \in R\}$ is also a [reduced residue system](@entry_id:635195) modulo $n$. This is a direct consequence of group theory. Since $R$ represents the [group of units](@entry_id:140130) $(\mathbb{Z}/n\mathbb{Z})^{\times}$ and $a$ represents an element of this group, multiplication by $[a]_n$ is a permutation of the group elements. This permutation property is the cornerstone of many results in number theory, including Euler's theorem [@problem_id:3084932].

**Translation**: In sharp contrast to a CRS, translating an RRS does not generally preserve it. If $R$ is an RRS, the set $R+c$ is often not an RRS. For instance, for $n=4$, an RRS is $R=\{1, 3\}$. If we translate by $c=1$, we get $R+1=\{2, 4\}$. Neither element is coprime to 4, so the result is definitively not an RRS [@problem_id:3010587].

A more profound question is: for which integers $c$ is $R+c$ an RRS for *every* RRS $R$ modulo $n$? The answer hinges on the **radical of n**, denoted $\mathrm{rad}(n)$, which is the product of the distinct prime divisors of $n$. A translate $R+c$ is an RRS for every RRS $R$ if and only if $c$ is a multiple of $\mathrm{rad}(n)$ [@problem_id:3010587].
- If $c \equiv 0 \pmod{\mathrm{rad}(n)}$, then $c$ is a multiple of every prime $p$ that divides $n$. For any $r \in R$, $\gcd(r,n)=1$, so $p \nmid r$. Then $r+c \equiv r \not\equiv 0 \pmod p$. Since this holds for all prime factors $p$ of $n$, $\gcd(r+c, n)=1$, and $R+c$ is an RRS.
- Conversely, if $c \not\equiv 0 \pmod{\mathrm{rad}(n)}$, there exists a prime $p | n$ such that $c \not\equiv 0 \pmod p$. Since the natural map from $(\mathbb{Z}/n\mathbb{Z})^{\times}$ to $(\mathbb{Z}/p\mathbb{Z})^{\times}$ is surjective, there must be an element $r$ in any RRS $R$ such that $r \equiv -c \pmod p$. For this $r$, we have $r+c \equiv 0 \pmod p$, implying $\gcd(r+c, n) \ge p > 1$. Thus, $R+c$ would not be an RRS.

### Structural Insights and Applications

#### The Chinese Remainder Theorem and RRS Structure

The **Chinese Remainder Theorem (CRT)** provides a powerful tool for understanding the structure of residue systems. If $n$ has the prime factorization $n = p_1^{\alpha_1} p_2^{\alpha_2} \cdots p_t^{\alpha_t}$, the CRT establishes a [ring isomorphism](@entry_id:147982):
$$ \mathbb{Z}/n\mathbb{Z} \cong \mathbb{Z}/p_1^{\alpha_1}\mathbb{Z} \times \cdots \times \mathbb{Z}/p_t^{\alpha_t}\mathbb{Z} $$
This isomorphism induces a [group isomorphism](@entry_id:147371) on the groups of units:
$$ (\mathbb{Z}/n\mathbb{Z})^{\times} \cong (\mathbb{Z}/p_1^{\alpha_1}\mathbb{Z})^{\times} \times \cdots \times (\mathbb{Z}/p_t^{\alpha_t}\mathbb{Z})^{\times} $$
This decomposition is tremendously useful. It implies that an integer $a$ is a unit modulo $n$ if and only if it is a unit modulo each prime [power factor](@entry_id:270707) $p_i^{\alpha_i}$. Structurally, it means we can construct an RRS for $n$ by choosing an RRS, $R_i$, for each prime [power factor](@entry_id:270707) $p_i^{\alpha_i}$, and then forming all possible tuples $(r_1, \dots, r_t)$ where each $r_i \in R_i$. For each such tuple, the CRT guarantees the existence of a unique residue class modulo $n$ that corresponds to it. The collection of these $\prod \varphi(p_i^{\alpha_i}) = \varphi(n)$ resulting integers forms an RRS modulo $n$ [@problem_id:3083592].

#### Application: The Rearrangement Proof of Euler's Theorem

The properties of reduced residue systems provide an elegant proof of **Euler's Theorem**, which states that if $\gcd(a,n)=1$, then $a^{\varphi(n)} \equiv 1 \pmod{n}$. The "rearrangement proof" proceeds as follows [@problem_id:3084932]:

1.  Let $R = \{r_1, r_2, \dots, r_{\varphi(n)}\}$ be an RRS modulo $n$.
2.  Consider the set $aR = \{ar_1, ar_2, \dots, ar_{\varphi(n)}\}$. As established previously, because $\gcd(a,n)=1$, multiplication by $a$ permutes the reduced [residue classes](@entry_id:185226). Therefore, the set of residues of $aR$ is identical to the set of residues of $R$.
3.  Since the sets of residues are the same, the product of their elements must be congruent modulo $n$:
    $$ \prod_{i=1}^{\varphi(n)} r_i \equiv \prod_{i=1}^{\varphi(n)} (ar_i) \pmod{n} $$
4.  Rearranging the right side gives:
    $$ \prod_{i=1}^{\varphi(n)} r_i \equiv a^{\varphi(n)} \prod_{i=1}^{\varphi(n)} r_i \pmod{n} $$
5.  Let $P = \prod_{i=1}^{\varphi(n)} r_i$. The [congruence](@entry_id:194418) is $P \equiv a^{\varphi(n)} P \pmod{n}$. To complete the proof, we must cancel $P$. This step is only valid if $P$ is invertible modulo $n$, i.e., if $\gcd(P,n)=1$. Since each $r_i$ in the product is coprime to $n$, their product $P$ must also be coprime to $n$. Thus, $P$ is a unit and can be cancelled [@problem_id:3084932].
6.  Cancelling $P$ from both sides yields the final result: $1 \equiv a^{\varphi(n)} \pmod{n}$.

### A Special Case: The Modulus n=1

It is instructive to consider how these definitions apply to the degenerate case $n=1$ [@problem_id:3083426].
The [congruence](@entry_id:194418) $a \equiv b \pmod 1$ means $1 \mid (a-b)$, which is true for any integers $a$ and $b$. Thus, there is only one congruence class modulo 1.

-   A **[complete residue system](@entry_id:188246)** must contain $n=1$ element. Since all integers belong to the same class, any singleton set $\{a\}$ where $a \in \mathbb{Z}$ is a valid CRS.
-   A **[reduced residue system](@entry_id:635195)** must contain $\varphi(1)$ elements. By convention, $\varphi(1)=1$. The condition for an element $a$ to be in an RRS is $\gcd(a,1)=1$. Since the gcd of any integer with 1 is 1, this condition is satisfied by all integers.

Therefore, for $n=1$, any singleton set $\{a\}$ is simultaneously a complete and a [reduced residue system](@entry_id:635195). This edge case confirms the robustness of the definitions.