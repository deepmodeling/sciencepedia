## Introduction
The question of when an integer is a [perfect square](@entry_id:635622) modulo a prime number is a central problem in elementary number theory. Solving congruences of the form $x^2 \equiv a \pmod{p}$ without resorting to trial and error reveals deep structural properties of our number system. This article provides a comprehensive exploration of the theory developed to answer this question, a journey that culminates in one of the most celebrated results in mathematics: the Law of Quadratic Reciprocity. You will gain a thorough understanding of the principles, discover their surprising connections to other fields, and learn to apply them to concrete problems.

To achieve this, we will first build the necessary theoretical machinery in the "Principles and Mechanisms" chapter, defining [quadratic residues](@entry_id:180432) and the Legendre symbol, and proving the main law and its supplements. Next, in "Applications and Interdisciplinary Connections," we will see how this elegant theory becomes a powerful tool in [modern cryptography](@entry_id:274529), [algebraic number](@entry_id:156710) theory, and beyond. Finally, the "Hands-On Practices" section will provide an opportunity to solidify your knowledge by working through targeted exercises that highlight key concepts and computational techniques.

## Principles and Mechanisms

The study of [quadratic congruences](@entry_id:199460), specifically of the form $x^2 \equiv a \pmod{n}$, represents a cornerstone of number theory. It probes the very structure of multiplicative groups in modular arithmetic and serves as an entry point into deeper algebraic concepts. This chapter systematically develops the theoretical machinery required to analyze and solve such congruences, focusing on the case where the modulus is an odd prime. We will define the fundamental concepts of [quadratic residues](@entry_id:180432), introduce the powerful notation of the Legendre symbol, and build towards the celebrated Law of Quadratic Reciprocity and its supplements.

### Quadratic Residues and the Structure of $(\mathbb{Z}/p\mathbb{Z})^\times$

Let $p$ be an odd prime. An integer $a$ is called a **[quadratic residue](@entry_id:199089) modulo $p$** if the [congruence](@entry_id:194418) $x^2 \equiv a \pmod{p}$ has a solution. If $p \nmid a$ and the congruence has no solution, $a$ is called a **quadratic nonresidue modulo $p$**.

This definition applies to any residue class in $\mathbb{Z}/p\mathbb{Z}$. A natural first question concerns the residue class of $0$. The [congruence](@entry_id:194418) $x^2 \equiv 0 \pmod{p}$ has the solution $x \equiv 0 \pmod{p}$, so $0$ is always a [quadratic residue](@entry_id:199089). [@problem_id:3089027]

The more intricate structure emerges when we consider the nonzero [residue classes](@entry_id:185226), which form the [multiplicative group](@entry_id:155975) $(\mathbb{Z}/p\mathbb{Z})^\times$. This is a [cyclic group](@entry_id:146728) of order $p-1$. To understand which elements are [quadratic residues](@entry_id:180432), we can examine the squaring homomorphism $\phi: (\mathbb{Z}/p\mathbb{Z})^\times \to (\mathbb{Z}/p\mathbb{Z})^\times$ defined by $\phi(x) = x^2$. The set of nonzero [quadratic residues](@entry_id:180432) is precisely the image of this map, which we denote $R^\times$.

By the First Isomorphism Theorem for groups, the order of the image is the order of the domain divided by the order of the kernel. The kernel of $\phi$ consists of all elements $x$ such that $x^2 \equiv 1 \pmod{p}$. This is equivalent to $(x-1)(x+1) \equiv 0 \pmod{p}$. Since $\mathbb{Z}/p\mathbb{Z}$ is a field, this implies $x \equiv 1 \pmod{p}$ or $x \equiv -1 \pmod{p}$. As $p$ is an odd prime, $1 \not\equiv -1 \pmod{p}$, so the kernel contains exactly two elements, $\{1, -1\}$.

Therefore, the number of nonzero [quadratic residues](@entry_id:180432) is:
$$ |R^\times| = \frac{|(\mathbb{Z}/p\mathbb{Z})^\times|}{|\ker(\phi)|} = \frac{p-1}{2} $$
The set of quadratic nonresidues consists of the elements in $(\mathbb{Z}/p\mathbb{Z})^\times$ that are not in $R^\times$. Their count is $(p-1) - \frac{p-1}{2} = \frac{p-1}{2}$. Thus, among the nonzero elements modulo an odd prime $p$, there are exactly as many [quadratic residues](@entry_id:180432) as quadratic nonresidues. [@problem_id:3089027]

Furthermore, as the image of a [group homomorphism](@entry_id:140603), $R^\times$ is a subgroup of $(\mathbb{Z}/p\mathbb{Z})^\times$. Its index is $\frac{|(\mathbb{Z}/p\mathbb{Z})^\times|}{|R^\times|} = \frac{p-1}{(p-1)/2} = 2$. This means the group of nonzero [quadratic residues](@entry_id:180432) is a subgroup of index 2, partitioning the group $(\mathbb{Z}/p\mathbb{Z})^\times$ into two cosets: the residues themselves and the nonresidues. [@problem_id:3089027]

### The Legendre Symbol and Euler's Criterion

To [streamline](@entry_id:272773) the discussion of [quadratic residues](@entry_id:180432), Adrien-Marie Legendre introduced a compact and powerful notation.

**Definition: The Legendre Symbol**
For an odd prime $p$ and an integer $a$, the Legendre symbol $\left(\frac{a}{p}\right)$ is defined as:
$$
\left(\frac{a}{p}\right) =
\begin{cases}
1  &\text{if } a \text{ is a nonzero quadratic residue modulo } p, \\
-1 &\text{if } a \text{ is a quadratic nonresidue modulo } p, \\
0  &\text{if } p \mid a.
\end{cases}
$$
This simple notation elegantly encodes the answer to our initial question. The [congruence](@entry_id:194418) $x^2 \equiv a \pmod{p}$ has a solution if and only if $\left(\frac{a}{p}\right) \neq -1$. [@problem_id:3089062]

We can be even more precise about the number of solutions.
- If $\left(\frac{a}{p}\right) = 1$, there exists a solution $x_0$. Then $-x_0$ is also a solution, and since $p$ is odd and $a \not\equiv 0 \pmod p$, we have $x_0 \not\equiv -x_0 \pmod p$. By Lagrange's theorem, a quadratic polynomial can have at most two [roots modulo a prime](@entry_id:635040), so there are exactly **two** solutions.
- If $\left(\frac{a}{p}\right) = -1$, there are by definition **zero** solutions.
- If $\left(\frac{a}{p}\right) = 0$, then $a \equiv 0 \pmod p$. The congruence is $x^2 \equiv 0 \pmod p$, which has exactly **one** solution, $x \equiv 0 \pmod p$.

Remarkably, the number of solutions to $x^2 \equiv a \pmod{p}$ can be expressed by the single formula $1 + \left(\frac{a}{p}\right)$. [@problem_id:3089021]

The first major result that facilitates the computation of the Legendre symbol is Euler's Criterion.

**Theorem (Euler's Criterion)**
If $p$ is an odd prime and $p \nmid a$, then
$$ \left(\frac{a}{p}\right) \equiv a^{(p-1)/2} \pmod p $$
Since the left side is either $1$ or $-1$, and the right side must be congruent to one of these values, this congruence implies equality in the integers for $p>2$. This theorem connects the quadratic character of $a$ to the group structure of $(\mathbb{Z}/p\mathbb{Z})^\times$, as the exponent $(p-1)/2$ is half the order of the group.

#### The First Supplement to Quadratic Reciprocity

Euler's Criterion provides the most [direct proof](@entry_id:141172) of the first major structural result, known as the First Supplement to the Law of Quadratic Reciprocity, which determines whether $-1$ is a square modulo $p$.

By setting $a=-1$ in Euler's Criterion, we obtain:
$$ \left(\frac{-1}{p}\right) = (-1)^{(p-1)/2} $$
The value of the exponent depends on the parity of $(p-1)/2$.
- If $p \equiv 1 \pmod 4$, then $p = 4k+1$ for some integer $k$. The exponent is $\frac{(4k+1)-1}{2} = 2k$, which is even. Thus, $\left(\frac{-1}{p}\right) = 1$.
- If $p \equiv 3 \pmod 4$, then $p = 4k+3$ for some integer $k$. The exponent is $\frac{(4k+3)-1}{2} = 2k+1$, which is odd. Thus, $\left(\frac{-1}{p}\right) = -1$.

For example, $-1$ is a square modulo $p=5$ and $p=13$ (both $ \equiv 1 \pmod 4$), but not modulo $p=3, 7, 11$ (all $ \equiv 3 \pmod 4$). [@problem_id:3089016] This result, determining the quadratic character of $-1$, is of fundamental importance.

### Gauss's Lemma and the Second Supplement

While Euler's Criterion is theoretically profound, Carl Friedrich Gauss provided a different, and in some ways deeper, criterion. It forms the basis for many elementary proofs of the main law of [quadratic reciprocity](@entry_id:184657). [@problem_id:3089049]

**Theorem (Gauss's Lemma)**
Let $p$ be an odd prime and let $a$ be an integer with $p \nmid a$. Consider the set of integers $S = \{a, 2a, 3a, \dots, \frac{p-1}{2}a\}$. Reduce each element of $S$ modulo $p$ to its least absolute residue, i.e., the unique integer in the interval $(-\frac{p}{2}, \frac{p}{2})$. Let $n$ be the number of negative residues in this set. Then
$$ \left(\frac{a}{p}\right) = (-1)^n $$

Though seemingly more complex, Gauss's Lemma provides a combinatorial or geometric path to evaluating Legendre symbols. Its most famous application is the derivation of the Second Supplement.

#### The Second Supplement to Quadratic Reciprocity

This law determines when $2$ is a [quadratic residue](@entry_id:199089). Applying Gauss's Lemma with $a=2$, we consider the set $S = \{2, 4, 6, \dots, p-1\}$. We need to count how many of these elements, $2k$ for $1 \le k \le \frac{p-1}{2}$, have their least positive residues modulo $p$ lie in the interval $(\frac{p}{2}, p)$. This is equivalent to counting integers $k$ such that $\frac{p}{4}  k \le \frac{p-1}{2}$.

A careful case-by-case analysis based on the residue of $p$ modulo $8$ reveals the pattern for the parity of $n$:
- If $p \equiv 1 \text{ or } 7 \pmod 8$, $n$ is even, so $\left(\frac{2}{p}\right)=1$.
- If $p \equiv 3 \text{ or } 5 \pmod 8$, $n$ is odd, so $\left(\frac{2}{p}\right)=-1$.

This can be expressed compactly:
$$ \left(\frac{2}{p}\right) = (-1)^{(p^2-1)/8} $$
This result, known as the Second Supplement, shows that the quadratic character of $2$ depends only on the class of $p$ modulo $8$. [@problem_id:3089057]

### The Main Law of Quadratic Reciprocity

The "crown jewel" of elementary number theory is the Law of Quadratic Reciprocity. It establishes a surprising and beautiful relationship between the symbols $\left(\frac{p}{q}\right)$ and $\left(\frac{q}{p}\right)$ for distinct odd primes $p$ and $q$.

**Theorem (The Law of Quadratic Reciprocity)**
Let $p$ and $q$ be distinct odd primes. Then
$$ \left(\frac{p}{q}\right)\left(\frac{q}{p}\right) = (-1)^{\frac{p-1}{2}\frac{q-1}{2}} $$

The exponent is odd if and only if both $\frac{p-1}{2}$ and $\frac{q-1}{2}$ are odd, which occurs if and only if both $p \equiv 3 \pmod 4$ and $q \equiv 3 \pmod 4$. This gives a more descriptive formulation:
- If $p \equiv 1 \pmod 4$ or $q \equiv 1 \pmod 4$ (or both), then $\left(\frac{p}{q}\right) = \left(\frac{q}{p}\right)$.
- If $p \equiv 3 \pmod 4$ and $q \equiv 3 \pmod 4$, then $\left(\frac{p}{q}\right) = -\left(\frac{q}{p}\right)$.

[@problem_id:3089012] The law's power lies in its ability to "flip" the Legendre symbol, allowing one to reduce the size of the numerator and eventually arrive at a symbol that is easy to evaluate. Together with the two supplements and the multiplicative property $\left(\frac{ab}{p}\right) = \left(\frac{a}{p}\right)\left(\frac{b}{p}\right)$, this law provides a complete algorithm for computing any Legendre symbol.

For instance, to find the [quadratic residues](@entry_id:180432) modulo $23$, we must compute $\left(\frac{a}{23}\right)$ for $a \in \{1, \dots, 22\}$. To find $\left(\frac{3}{23}\right)$, we use the main law. Since $3 \equiv 3 \pmod 4$ and $23 \equiv 3 \pmod 4$, we have:
$$ \left(\frac{3}{23}\right) = -\left(\frac{23}{3}\right) = -\left(\frac{2}{3}\right) $$
Since $1^2 \equiv 1$ and $2^2 \equiv 1 \pmod 3$, $2$ is not a square modulo $3$, so $\left(\frac{2}{3}\right) = -1$. Therefore, $\left(\frac{3}{23}\right) = -(-1) = 1$, and $3$ is a [quadratic residue](@entry_id:199089) modulo $23$. By systematically applying these laws, one can determine the full set of [quadratic residues](@entry_id:180432). [@problem_id:3089028]

As another example, Gauss's Lemma can be used to show that $\left(\frac{3}{p}\right)=1$ if $p \equiv \pm 1 \pmod{12}$ and $\left(\frac{3}{p}\right)=-1$ if $p \equiv \pm 5 \pmod{12}$. This result can also be derived using the main law, demonstrating the consistency and interconnectedness of these principles. [@problem_id:3089051]

### The Jacobi Symbol: A Computational Extension

While the Legendre symbol is defined only for prime moduli, its properties inspire a powerful generalization for [composite moduli](@entry_id:189955), known as the **Jacobi symbol**.

**Definition: The Jacobi Symbol**
Let $n$ be an odd positive integer with prime factorization $n = p_1^{e_1} p_2^{e_2} \cdots p_k^{e_k}$. For any integer $a$, the Jacobi symbol is defined as:
$$ \left(\frac{a}{n}\right) = \prod_{i=1}^k \left(\frac{a}{p_i}\right)^{e_i} $$
where $\left(\frac{a}{p_i}\right)$ is the Legendre symbol. If $n$ is prime, the Jacobi symbol is identical to the Legendre symbol. [@problem_id:3089022]

The remarkable fact is that the main law and its two supplements hold for the Jacobi symbol as well. For odd, positive, coprime integers $m$ and $n$:
- $\left(\frac{m}{n}\right)\left(\frac{n}{m}\right) = (-1)^{\frac{m-1}{2}\frac{n-1}{2}}$
- $\left(\frac{-1}{n}\right) = (-1)^{\frac{n-1}{2}}$
- $\left(\frac{2}{n}\right) = (-1)^{\frac{n^2-1}{8}}$

[@problem_id:3089022] The primary use of the Jacobi symbol is computational. It allows us to apply the "flipping" rule of reciprocity without having to factor the denominator. For example, to compute $\left(\frac{1001}{9907}\right)$, one would have to factor $1001$ but not $9907$ (which is prime). Using the Jacobi symbol allows repeated flips until a simple symbol remains.

There is, however, a critical and subtle distinction. For the Legendre symbol, $\left(\frac{a}{p}\right)=1$ is equivalent to $a$ being a [quadratic residue](@entry_id:199089) modulo $p$. This is **not** true for the Jacobi symbol. If $n$ is composite, **$\left(\frac{a}{n}\right)=1$ does not imply that $a$ is a [quadratic residue](@entry_id:199089) modulo $n$**.

The reason is clear from the definition. The Jacobi symbol can be $1$ if an even number of its constituent Legendre symbols are $-1$. For example, consider $\left(\frac{2}{15}\right)$:
$$ \left(\frac{2}{15}\right) = \left(\frac{2}{3}\right)\left(\frac{2}{5}\right) = (-1)(-1) = 1 $$
Despite this, $2$ is not a [quadratic residue](@entry_id:199089) modulo $15$, because the [congruence](@entry_id:194418) $x^2 \equiv 2 \pmod{15}$ would require solutions to both $x^2 \equiv 2 \pmod 3$ and $x^2 \equiv 2 \pmod 5$. Since $\left(\frac{2}{3}\right) = -1$, the first of these has no solution. [@problem_id:3089022]

Thus, the Jacobi symbol is a powerful computational tool that generalizes the mechanics of the Legendre symbol, but it loses the direct equivalence to the solvability of [quadratic congruences](@entry_id:199460) when the denominator is composite. It serves as an efficient sieve: if $\left(\frac{a}{n}\right) = -1$, we know for certain that $a$ is not a [quadratic residue](@entry_id:199089) modulo $n$. If $\left(\frac{a}{n}\right) = 1$, the question of solvability remains open and requires further investigation.