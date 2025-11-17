## Introduction
The simple-looking equation $x^2 \equiv a \pmod{n}$ opens the door to one of the most elegant and foundational topics in number theory: the study of [quadratic residues](@entry_id:180432). Determining for which values of 'a' this [congruence](@entry_id:194418) has a solution is a fundamental problem that has fascinated mathematicians for centuries, from Euler to Gauss. The challenge lies in developing methods that are more efficient than brute-force testing, especially as the numbers involved become astronomically large. This article provides a systematic exploration of this rich subject. The first section, **Principles and Mechanisms**, will build the theoretical framework from the ground up, introducing the Legendre symbol, Euler's Criterion, and the celebrated Law of Quadratic Reciprocity. Following this, the **Applications and Interdisciplinary Connections** section will demonstrate the profound impact of these ideas on modern fields like cryptography, computer science, and algorithm design. Finally, **Hands-On Practices** will offer a chance to solidify your understanding by tackling concrete problems. We begin our journey by establishing the core principles and mechanisms that govern the world of [quadratic residues](@entry_id:180432).

## Principles and Mechanisms

### The Fundamental Definition of Quadratic Residues

The study of [quadratic congruences](@entry_id:199460), equations of the form $x^2 \equiv a \pmod{n}$, is a cornerstone of number theory. The central question is simple: for which values of $a$ and $n$ does this [congruence](@entry_id:194418) have a solution? This question leads to a fundamental classification of integers modulo $n$.

An integer $a$ is called a **[quadratic residue](@entry_id:199089) modulo n** if the congruence $x^2 \equiv a \pmod{n}$ has a solution for some integer $x$. If the congruence has no solution, $a$ is called a **quadratic non-residue modulo n**. When $\gcd(a, n) > 1$, the situation can be complex. However, if $\gcd(a,n)=1$, we say $a$ is a **reduced [quadratic residue](@entry_id:199089)** if it is a [quadratic residue](@entry_id:199089). For instance, modulo $10$, the squares of the integers are $0^2 \equiv 0$, $1^2 \equiv 1$, $2^2 \equiv 4$, $3^2 \equiv 9$, $4^2 \equiv 16 \equiv 6$, and $5^2 \equiv 25 \equiv 5$. The integers $0, 1, 4, 5, 6, 9$ are [quadratic residues](@entry_id:180432) modulo $10$. The integers $2, 3, 7, 8$ are [quadratic non-residues](@entry_id:201109) modulo $10$.

It is essential to distinguish this property from the concept of a residue class. The set of integers is partitioned into equivalence classes by the [congruence relation](@entry_id:272002), where the **residue class** of $a$ modulo $n$ is the set $[a]_n = \{a + kn : k \in \mathbb{Z}\}$. The collection of all such classes forms the [ring of integers](@entry_id:155711) modulo $n$, denoted $\mathbb{Z}/n\mathbb{Z}$. The property of being a [quadratic residue](@entry_id:199089) modulo $n$ can be elegantly rephrased in this language: an integer $a$ is a [quadratic residue](@entry_id:199089) modulo $n$ if its residue class $[a]_n$ is in the image of the squaring map $s: [x]_n \mapsto [x^2]_n$ on the ring $\mathbb{Z}/n\mathbb{Z}$ [@problem_id:3089082]. It is not required that every integer in the class $[a]_n$ be a perfect square in $\mathbb{Z}$, which is a much stronger and generally false condition.

### The Case of Prime Moduli: The Legendre Symbol

The theory becomes significantly more elegant and structured when the modulus $n$ is an odd prime, which we will denote by $p$. In this case, $\mathbb{Z}/p\mathbb{Z}$ is a field, denoted $\mathbb{F}_p$. This field structure allows us to use powerful algebraic tools. To [streamline](@entry_id:272773) the classification of integers modulo an odd prime $p$, Adrien-Marie Legendre introduced a notation that has become central to the subject.

The **Legendre symbol**, denoted $\left(\frac{a}{p}\right)$, is defined for an odd prime $p$ and any integer $a$:
$$
\left(\frac{a}{p}\right) =
\begin{cases}
1  \text{if } a \text{ is a quadratic residue modulo } p \text{ and } p \nmid a \\
-1  \text{if } a \text{ is a quadratic non-residue modulo } p \\
0  \text{if } p \mid a
\end{cases}
$$
This symbol provides a compact way to answer the question of whether $a$ is a square modulo $p$ [@problem_id:3089083]. For example, modulo $p=7$, the squares of the non-zero elements are $1^2 \equiv 1$, $2^2 \equiv 4$, $3^2 \equiv 2$, $4^2 \equiv 2$, $5^2 \equiv 4$, and $6^2 \equiv 1$. The [quadratic residues](@entry_id:180432) are $\{1, 2, 4\}$, and the non-residues are $\{3, 5, 6\}$. Thus, we would write $\left(\frac{2}{7}\right) = 1$ and $\left(\frac{3}{7}\right) = -1$.

The Legendre symbol does more than just classify; it also counts. The number of solutions to the congruence $x^2 \equiv a \pmod{p}$ for an odd prime $p$ is given by the remarkably simple formula $1 + \left(\frac{a}{p}\right)$. Let us verify this [@problem_id:3021781]:
- If $a \equiv 0 \pmod{p}$, then $x^2 \equiv 0 \pmod{p}$ implies $x \equiv 0 \pmod{p}$ (since $\mathbb{F}_p$ is a field). There is exactly one solution. The formula gives $1 + \left(\frac{0}{p}\right) = 1+0=1$.
- If $a$ is a quadratic non-residue modulo $p$, there are by definition no solutions. The formula gives $1 + \left(\frac{a}{p}\right) = 1 + (-1) = 0$.
- If $a$ is a non-zero [quadratic residue](@entry_id:199089) modulo $p$, there exists a solution $x_0$. Then $(-x_0)^2 = x_0^2 \equiv a \pmod{p}$, so $-x_0$ is also a solution. As $p$ is odd, $x_0 \not\equiv -x_0 \pmod{p}$ (otherwise $2x_0 \equiv 0 \pmod{p}$, which implies $p \mid x_0$, contradicting $a \not\equiv 0$). Thus there are exactly two solutions. The formula gives $1 + \left(\frac{a}{p}\right) = 1+1=2$.

### A Structural Viewpoint: The Group of Units

A deeper understanding of [quadratic residues](@entry_id:180432) comes from examining the algebraic structure of the set of units modulo $n$, denoted $(\mathbb{Z}/n\mathbb{Z})^{\times}$. This is the group of [residue classes](@entry_id:185226) coprime to $n$ under multiplication.

When $n=p$ is an odd prime, the group $(\mathbb{Z}/p\mathbb{Z})^{\times}$ is a cyclic group of order $p-1$. Consider the squaring map $s: (\mathbb{Z}/p\mathbb{Z})^{\times} \to (\mathbb{Z}/p\mathbb{Z})^{\times}$ defined by $s(x) = x^2$. Since the group is abelian, $s$ is a [group homomorphism](@entry_id:140603).
- The **image** of this map, $\operatorname{im}(s)$, is the set of all squares of units, which is precisely the set of non-zero [quadratic residues](@entry_id:180432). As the image of a homomorphism, this set is a subgroup of $(\mathbb{Z}/p\mathbb{Z})^{\times}$.
- The **kernel** of this map, $\ker(s)$, consists of elements $x$ such that $x^2 \equiv 1 \pmod{p}$. In a field, this polynomial equation has at most two roots, which are clearly $1$ and $-1$. Since $p$ is odd, $1 \not\equiv -1 \pmod{p}$, so $|\ker(s)| = 2$ [@problem_id:3089099] [@problem_id:3089086].

By the First Isomorphism Theorem for groups, the order of the image is the order of the group divided by the order of the kernel:
$$ |\operatorname{im}(s)| = \frac{|(\mathbb{Z}/p\mathbb{Z})^{\times}|}{|\ker(s)|} = \frac{p-1}{2} $$
This elegantly proves that among the $p-1$ non-zero [residue classes](@entry_id:185226) modulo an odd prime $p$, exactly half are [quadratic residues](@entry_id:180432) and the other half are [quadratic non-residues](@entry_id:201109) [@problem_id:3089099] [@problem_id:3089086]. The subgroup of squares $Q = \operatorname{im}(s)$ has index $[(\mathbb{Z}/p\mathbb{Z})^{\times}:Q] = 2$. This implies that there is a unique nontrivial [group homomorphism](@entry_id:140603) from $(\mathbb{Z}/p\mathbb{Z})^{\times}$ to the group $\{\pm 1\}$, known as the **quadratic character** modulo $p$. This homomorphism is precisely the Legendre symbol.

For a general [composite modulus](@entry_id:180993) $n$, the structure is more complex. The size of the kernel of the squaring map on $(\mathbb{Z}/n\mathbb{Z})^{\times}$ depends on the [prime factorization](@entry_id:152058) of $n$. If $n = 2^k p_1^{e_1} \cdots p_r^{e_r}$, the number of solutions to $x^2 \equiv 1 \pmod{n}$ can be found using the Chinese Remainder Theorem. This number, $|\ker(s)|$, determines the number of reduced [quadratic residues](@entry_id:180432), $|\operatorname{im}(s)| = \varphi(n)/|\ker(s)|$ [@problem_id:3089099].

### Euler's Criterion: A Computational Test

While the definition of the Legendre symbol is clear, it does not provide an efficient way to compute its value for large primes. The first major breakthrough in this direction was **Euler's criterion**, which connects the Legendre symbol to [modular exponentiation](@entry_id:146739).

For any odd prime $p$ and any integer $a$ not divisible by $p$, the following [congruence](@entry_id:194418) holds:
$$ \left(\frac{a}{p}\right) \equiv a^{\frac{p-1}{2}} \pmod{p} $$
This criterion provides a direct algorithm for computing $\left(\frac{a}{p}\right)$ [@problem_id:3091006]. The proof is a beautiful application of the group theory discussed above. If $a$ is a [quadratic residue](@entry_id:199089), $a \equiv x^2 \pmod{p}$ for some $x \in (\mathbb{Z}/p\mathbb{Z})^{\times}$. By Fermat's Little Theorem, $x^{p-1} \equiv 1 \pmod{p}$. Thus, $a^{\frac{p-1}{2}} \equiv (x^2)^{\frac{p-1}{2}} = x^{p-1} \equiv 1 \pmod{p}$. If $a$ is a quadratic non-residue, one can show that $a^{\frac{p-1}{2}} \equiv -1 \pmod{p}$ by considering a generator of the [cyclic group](@entry_id:146728) $(\mathbb{Z}/p\mathbb{Z})^{\times}$.

It is crucial to recognize that Euler's criterion is a congruence, not an equality of integers. For example, for $p=5$ and $a=2$, we have $\left(\frac{2}{5}\right) = -1$. Euler's criterion states that $-1 \equiv 2^{(5-1)/2} = 2^2 = 4 \pmod 5$, which is true. Confusing this with an equality would lead to the absurd statement $-1=4$ [@problem_id:3089083].

### The Law of Quadratic Reciprocity

While Euler's criterion is a powerful tool, the true jewel of this theory is the **Law of Quadratic Reciprocity**, discovered by Euler and first proven rigorously by Gauss. This law reveals a stunningly deep and symmetric relationship between the Legendre symbols $\left(\frac{p}{q}\right)$ and $\left(\frac{q}{p}\right)$ for two distinct odd primes $p$ and $q$.

#### Gauss's Lemma

A key step in many proofs of [quadratic reciprocity](@entry_id:184657) is another of Gauss's profound contributions: **Gauss's Lemma**. It provides a combinatorial method for computing the Legendre symbol.

**Gauss's Lemma**: Let $p$ be an odd prime and let $a$ be an integer with $\gcd(a,p)=1$. Consider the set of integers $S = \{a, 2a, 3a, \dots, \frac{p-1}{2}a\}$. Reduce each element of $S$ to its least absolute residue modulo $p$, which is the unique representative in the interval $(-\frac{p}{2}, \frac{p}{2})$. Let $N$ be the number of these least absolute residues that are negative. Then $\left(\frac{a}{p}\right) = (-1)^N$.

Let's illustrate this with an example. Consider the computation of $\left(\frac{5}{2017}\right)$ using Gauss's Lemma, where $p=2017$ is a prime [@problem_id:3021797]. We must consider the set $\{5k : 1 \le k \le 1008\}$. A residue $5k \pmod{2017}$ will have a negative least absolute residue if and only if $5k \pmod{2017}$ falls in the interval $(1008.5, 2017)$. A careful count reveals:
- For $m=0$: $1008.5  5k  2017$ implies $201.7  k  403.4$. This gives $403 - 202 + 1 = 202$ values of $k$.
- For $m=1$: $3025.5  5k  4034$ implies $605.1  k  806.8$. This gives $806 - 606 + 1 = 201$ values of $k$.
- For $m \ge 2$, the intervals for $5k$ are beyond its range for $k \le 1008$.
The total count of negative residues is $N = 202 + 201 = 403$. Since $N$ is odd, Gauss's Lemma tells us that $\left(\frac{5}{2017}\right) = (-1)^{403} = -1$.

#### The Main Law and Its Supplements

The Law of Quadratic Reciprocity connects the solubility of $x^2 \equiv p \pmod q$ with that of $x^2 \equiv q \pmod p$.

**Law of Quadratic Reciprocity**: For distinct odd primes $p$ and $q$,
$$ \left(\frac{p}{q}\right)\left(\frac{q}{p}\right) = (-1)^{\frac{(p-1)}{2} \frac{(q-1)}{2}} $$

The exponent $\frac{(p-1)}{2} \frac{(q-1)}{2}$ is odd if and only if both factors are odd. The term $\frac{p-1}{2}$ is odd if and only if $p-1 = 2 \times (\text{odd})$, which means $p-1 \equiv 2 \pmod 4$, or $p \equiv 3 \pmod 4$. Therefore, the product $\left(\frac{p}{q}\right)\left(\frac{q}{p}\right)$ equals $-1$ if and only if both $p$ and $q$ are congruent to $3$ modulo $4$. In all other cases, the product is $1$, which means $\left(\frac{p}{q}\right) = \left(\frac{q}{p}\right)$ [@problem_id:3089073].

This main law is accompanied by two **supplementary laws** that handle the cases of $-1$ and $2$:
1.  $\left(\frac{-1}{p}\right) = (-1)^{\frac{p-1}{2}}$. This means $-1$ is a [quadratic residue](@entry_id:199089) modulo $p$ if and only if $p \equiv 1 \pmod 4$.
2.  $\left(\frac{2}{p}\right) = (-1)^{\frac{p^2-1}{8}}$. This means $2$ is a [quadratic residue](@entry_id:199089) modulo $p$ if and only if $p \equiv 1$ or $7 \pmod 8$.

#### Application of Quadratic Reciprocity

Together, these laws provide a highly efficient algorithm for computing any Legendre symbol. The strategy is to repeatedly use reciprocity to "flip" the symbol, reducing the magnitude of the numbers involved, until we reach a symbol that can be evaluated directly.

Let's compute $\left(\frac{239}{283}\right)$, where both 239 and 283 are prime [@problem_id:3089091].
1.  Check congruences modulo 4: $239 = 4 \cdot 59 + 3 \equiv 3 \pmod 4$ and $283 = 4 \cdot 70 + 3 \equiv 3 \pmod 4$. Since both are $3 \pmod 4$, reciprocity introduces a negative sign.
    $$ \left(\frac{239}{283}\right) = -\left(\frac{283}{239}\right) $$
2.  Reduce the numerator: $283 = 1 \cdot 239 + 44$.
    $$ -\left(\frac{283}{239}\right) = -\left(\frac{44}{239}\right) $$
3.  Factor the numerator: Use the multiplicative property $\left(\frac{ab}{p}\right) = \left(\frac{a}{p}\right)\left(\frac{b}{p}\right)$.
    $$ -\left(\frac{44}{239}\right) = -\left(\frac{4 \cdot 11}{239}\right) = -\left(\frac{2^2}{239}\right)\left(\frac{11}{239}\right) = -\left(\frac{11}{239}\right) $$
4.  Apply reciprocity again: $11 \equiv 3 \pmod 4$ and $239 \equiv 3 \pmod 4$. Again, both are $3 \pmod 4$.
    $$ -\left(\frac{11}{239}\right) = - \left( - \left(\frac{239}{11}\right) \right) = \left(\frac{239}{11}\right) $$
5.  Reduce the numerator: $239 = 21 \cdot 11 + 8$.
    $$ \left(\frac{239}{11}\right) = \left(\frac{8}{11}\right) $$
6.  Factor and use the supplementary law:
    $$ \left(\frac{8}{11}\right) = \left(\frac{2^3}{11}\right) = \left(\frac{2}{11}\right) $$
    Since $11 \equiv 3 \pmod 8$, the supplementary law gives $\left(\frac{2}{11}\right) = -1$.
Thus, the final result is $\left(\frac{239}{283}\right) = -1$.

### Generalization to Composite Moduli: The Jacobi Symbol

The Law of Quadratic Reciprocity requires the "denominator" of the Legendre symbol to be prime. This is restrictive. Carl Jacobi extended the definition to accommodate any odd composite denominator.

The **Jacobi symbol** $\left(\frac{a}{n}\right)$ is defined for any odd positive integer $n$ and any integer $a$. If the [prime factorization](@entry_id:152058) of $n$ is $n = p_1^{e_1} p_2^{e_2} \cdots p_k^{e_k}$, then the Jacobi symbol is defined as the product of the corresponding Legendre symbols:
$$ \left(\frac{a}{n}\right) = \prod_{i=1}^{k} \left(\frac{a}{p_i}\right)^{e_i} $$
This definition preserves the multiplicative properties. It is completely multiplicative in both the numerator and the denominator [@problem_id:3089081]:
- $\left(\frac{ab}{n}\right) = \left(\frac{a}{n}\right)\left(\frac{b}{n}\right)$
- $\left(\frac{a}{mn}\right) = \left(\frac{a}{m}\right)\left(\frac{a}{n}\right)$ for odd $m,n$.

Remarkably, the Law of Quadratic Reciprocity and its supplementary laws hold for the Jacobi symbol as well (provided $m,n$ are odd and coprime for reciprocity). This makes it a powerful computational tool, as one can use the reciprocity algorithm without needing to factor the denominator at each step.

#### A Crucial Caveat

There is a critical difference between the Legendre and Jacobi symbols. If the Jacobi symbol $\left(\frac{a}{n}\right) = -1$, then we know that for at least one prime factor $p_i$ of $n$, the Legendre symbol $\left(\frac{a}{p_i}\right)$ must be $-1$. This implies $a$ is a quadratic non-residue modulo $p_i$, and therefore $a$ must be a quadratic non-residue modulo $n$.

However, if $\left(\frac{a}{n}\right) = 1$, it **does not** imply that $a$ is a [quadratic residue](@entry_id:199089) modulo $n$. The reason is that the product of an even number of $-1$'s is $1$. For instance, if $n=p_1 p_2$, and $a$ is a non-residue modulo both $p_1$ and $p_2$, then $\left(\frac{a}{p_1}\right)=-1$ and $\left(\frac{a}{p_2}\right)=-1$. The Jacobi symbol would be:
$$ \left(\frac{a}{n}\right) = \left(\frac{a}{p_1}\right)\left(\frac{a}{p_2}\right) = (-1)(-1) = 1 $$
But since $a$ is a non-residue modulo $p_1$, the [congruence](@entry_id:194418) $x^2 \equiv a \pmod{p_1}$ has no solution, which means $x^2 \equiv a \pmod{n}$ cannot have a solution either. Thus, $a$ is a quadratic non-residue modulo $n$ despite its Jacobi symbol being $1$.

A classic example is for $n=21=3 \cdot 7$. Consider the integer $a=5$. We compute the Jacobi symbol:
$$ \left(\frac{5}{21}\right) = \left(\frac{5}{3}\right)\left(\frac{5}{7}\right) $$
Modulo 3, $5 \equiv 2$, which is a non-residue, so $\left(\frac{5}{3}\right)=-1$.
Modulo 7, the squares are 1, 4, 2. So 5 is a non-residue, and $\left(\frac{5}{7}\right)=-1$.
Therefore, $\left(\frac{5}{21}\right) = (-1)(-1) = 1$. However, since $5$ is a non-residue modulo $3$, it cannot be a residue modulo $21$. This illustrates the crucial limitation of the Jacobi symbol [@problem_id:3089071]. This subtlety is the basis for probabilistic primality tests like the Solovay-Strassen test.