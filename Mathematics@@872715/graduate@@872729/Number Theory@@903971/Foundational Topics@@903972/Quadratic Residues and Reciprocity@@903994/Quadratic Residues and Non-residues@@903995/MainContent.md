## Introduction
The question of whether an integer is a [perfect square](@entry_id:635622) modulo a prime number is a simple one to state, yet its answer unveils a rich and intricate structure at the heart of number theory. This concept of "quadratic residuosity" is not merely a curiosity but a foundational principle with far-reaching consequences. For centuries, mathematicians have sought efficient methods to solve [quadratic congruences](@entry_id:199460), moving beyond brute-force checks to uncover deeper, more elegant laws. This article addresses this fundamental problem by providing a thorough exploration of [quadratic residues](@entry_id:180432) and non-residues. In the first chapter, "Principles and Mechanisms," we will build the theory from the ground up, defining [quadratic residues](@entry_id:180432), introducing the powerful Legendre symbol, and culminating in Gauss's celebrated Law of Quadratic Reciprocity. Next, in "Applications and Interdisciplinary Connections," we will see how these principles provide essential tools in abstract algebra, [cryptography](@entry_id:139166), and coding theory. Finally, "Hands-On Practices" will offer you the opportunity to solidify your understanding through guided computational problems, from evaluating Legendre symbols to implementing algorithms for finding square roots.

## Principles and Mechanisms

This chapter delves into the foundational principles governing [quadratic residues](@entry_id:180432). We will begin by defining [quadratic residues](@entry_id:180432) and exploring their basic structural properties within [finite fields](@entry_id:142106). We will then introduce the Legendre symbol as a powerful notational and conceptual tool, culminating in the celebrated Law of Quadratic Reciprocity. Finally, we will explore significant generalizations and applications of these ideas, including the Jacobi symbol, quadratic Gauss sums, and the Hilbert symbol, which connect the theory to broader areas of number theory and algebra.

### The Structure of Squares in a Finite Field

Let $p$ be an odd prime. The finite field with $p$ elements, denoted $\mathbb{F}_p$, consists of the [residue classes](@entry_id:185226) of integers modulo $p$. The nonzero elements form a multiplicative group, $\mathbb{F}_p^\times$, which is a [cyclic group](@entry_id:146728) of order $p-1$.

A nonzero element $a \in \mathbb{F}_p^\times$ is called a **[quadratic residue](@entry_id:199089) modulo $p$** if it is a square of some element in $\mathbb{F}_p^\times$; that is, if the [congruence](@entry_id:194418) $x^2 \equiv a \pmod{p}$ has a solution $x \in \mathbb{F}_p^\times$. If no such solution exists, $a$ is called a **quadratic non-residue modulo $p$**.

To understand the structure of these sets, consider the squaring map $\phi: \mathbb{F}_p^\times \to \mathbb{F}_p^\times$ defined by $\phi(x) = x^2$. This map is a [group homomorphism](@entry_id:140603), since $\phi(xy) = (xy)^2 = x^2y^2 = \phi(x)\phi(y)$ due to the commutativity of multiplication in $\mathbb{F}_p$. The image of this homomorphism, $\text{Im}(\phi)$, is precisely the set of [quadratic residues](@entry_id:180432).

By the First Isomorphism Theorem for groups, the order of the image is the order of the group divided by the order of the kernel. The kernel of $\phi$ consists of all elements $x \in \mathbb{F}_p^\times$ such that $x^2 \equiv 1 \pmod{p}$. This [congruence](@entry_id:194418), $x^2 - 1 \equiv 0 \pmod{p}$, factors as $(x-1)(x+1) \equiv 0 \pmod{p}$. Since $\mathbb{F}_p$ is a field, the only solutions are $x \equiv 1 \pmod{p}$ and $x \equiv -1 \pmod{p}$. As $p$ is an odd prime, $1 \not\equiv -1 \pmod{p}$, so the kernel has exactly two elements: $\ker(\phi) = \{1, -1\}$.

Consequently, the number of [quadratic residues](@entry_id:180432) is $|\text{Im}(\phi)| = |\mathbb{F}_p^\times| / |\ker(\phi)| = (p-1)/2$. The remaining $(p-1) - (p-1)/2 = (p-1)/2$ elements of $\mathbb{F}_p^\times$ are the [quadratic non-residues](@entry_id:201109). The squaring map is a two-to-one map from $\mathbb{F}_p^\times$ onto the set of [quadratic residues](@entry_id:180432). Specifically, for any [quadratic residue](@entry_id:199089) $a$, the equation $x^2 \equiv a \pmod{p}$ has exactly two solutions, $x_0$ and $-x_0$.

To generate the set of [quadratic residues](@entry_id:180432) explicitly, we do not need to square all $p-1$ elements of $\mathbb{F}_p^\times$. Since $x^2 \equiv (p-x)^2 \pmod{p}$, we only need to square the integers from $1$ to $(p-1)/2$. The resulting values are all distinct, providing a complete list of the $(p-1)/2$ [quadratic residues](@entry_id:180432) [@problem_id:3021791].

For example:
- For $p=5$, we compute $1^2 \equiv 1$ and $2^2 \equiv 4$. The [quadratic residues](@entry_id:180432) are $\{1, 4\}$.
- For $p=7$, we compute $1^2 \equiv 1$, $2^2 \equiv 4$, and $3^2 \equiv 2$. The [quadratic residues](@entry_id:180432) are $\{1, 2, 4\}$.
- For $p=11$, we compute $1^2 \equiv 1$, $2^2 \equiv 4$, $3^2 \equiv 9$, $4^2 \equiv 5$, $5^2 \equiv 3$. The [quadratic residues](@entry_id:180432) are $\{1, 3, 4, 5, 9\}$.

A curious property emerges when we consider the product of all nonzero [quadratic residues](@entry_id:180432) modulo $p$. Let this set be $R_p$. The product is $\prod_{a \in R_p} a$. Using Wilson's Theorem, which states $(p-1)! \equiv -1 \pmod p$, and the fact that $R_p = \{1^2, 2^2, \dots, ((p-1)/2)^2\}$, one can derive that this product is congruent to $-(-1)^{(p-1)/2} \pmod p$ [@problem_id:3021791]. This means the product is $-1$ if $p \equiv 1 \pmod 4$ and $1$ if $p \equiv 3 \pmod 4$.

### The Legendre Symbol

To work efficiently with [quadratic residues](@entry_id:180432), Adrien-Marie Legendre introduced a compact notation. The **Legendre symbol**, denoted $\left(\frac{a}{p}\right)$, is defined for an odd prime $p$ and an integer $a$:
$$
\left(\frac{a}{p}\right) = 
\begin{cases}
1  & \text{if } a \text{ is a quadratic residue modulo } p \text{ and } p \nmid a \\
-1 & \text{if } a \text{ is a quadratic non-residue modulo } p \\
0  & \text{if } p \mid a
\end{cases}
$$

The Legendre symbol provides a remarkably elegant way to express the number of solutions to the congruence $x^2 \equiv a \pmod{p}$. Let $N_p(a)$ be this number of solutions in $\mathbb{F}_p$.
- If $a \equiv 0 \pmod p$, the [congruence](@entry_id:194418) is $x^2 \equiv 0 \pmod p$, which has the unique solution $x=0$. So, $N_p(0)=1$.
- If $a$ is a [quadratic residue](@entry_id:199089) modulo $p$, there are exactly two solutions. So, $N_p(a)=2$.
- If $a$ is a quadratic non-residue modulo $p$, there are no solutions. So, $N_p(a)=0$.

These three cases can be unified into a single formula:
$$ N_p(a) = 1 + \left(\frac{a}{p}\right) $$
This expression perfectly captures the case-by-case analysis and is a cornerstone of the theory of point counting on algebraic varieties over [finite fields](@entry_id:142106) [@problem_id:3021781].

One of the most important properties of the Legendre symbol is its complete multiplicativity: for any integers $a$ and $b$,
$$ \left(\frac{ab}{p}\right) = \left(\frac{a}{p}\right)\left(\frac{b}{p}\right) $$
This identity can be verified by explicit computation for small primes [@problem_id:3021798]. In modern language, it states that for $a \not\equiv 0 \pmod p$, the map $a \mapsto \left(\frac{a}{p}\right)$ is a [group homomorphism](@entry_id:140603) from $\mathbb{F}_p^\times$ to the [multiplicative group](@entry_id:155975) $\{\pm 1\}$. This is known as a **quadratic character**. This property implies that the product of two [quadratic residues](@entry_id:180432) is a residue, the product of a residue and a non-residue is a non-residue, and the product of two non-residues is a residue.

### Criteria for Evaluating the Legendre Symbol

While the definition of the Legendre symbol is straightforward, determining its value for a given $a$ and $p$ by checking all squares modulo $p$ is impractical. The theory provides powerful computational criteria.

#### Euler's Criterion

The first such criterion connects the Legendre symbol to [modular exponentiation](@entry_id:146739). **Euler's criterion** states that for an odd prime $p$ and an integer $a$ not divisible by $p$:
$$ \left(\frac{a}{p}\right) \equiv a^{(p-1)/2} \pmod{p} $$
This result follows directly from the structure of the cyclic group $\mathbb{F}_p^\times$. If $a$ is a [quadratic residue](@entry_id:199089), say $a \equiv x^2 \pmod p$, then $a^{(p-1)/2} \equiv (x^2)^{(p-1)/2} \equiv x^{p-1} \equiv 1 \pmod p$ by Fermat's Little Theorem. The polynomial $y^{(p-1)/2} - 1$ has degree $(p-1)/2$ and we have just found $(p-1)/2$ roots: all the [quadratic residues](@entry_id:180432). Since a polynomial over a field cannot have more roots than its degree, these are all the roots. Therefore, if $a$ is a quadratic non-residue, it cannot be a root, so $a^{(p-1)/2} \not\equiv 1 \pmod p$. However, $(a^{(p-1)/2})^2 = a^{p-1} \equiv 1 \pmod p$, which implies $a^{(p-1)/2}$ must be a root of $y^2-1=0$. The only other root is $-1$, so $a^{(p-1)/2} \equiv -1 \pmod p$ [@problem_id:3021788].

Euler's criterion provides an algorithm for computing $\left(\frac{a}{p}\right)$ via [modular exponentiation](@entry_id:146739), which is computationally feasible. For instance, to compute $\left(\frac{123}{1009}\right)$, one would compute $123^{(1009-1)/2} = 123^{504} \pmod{1009}$. Using efficient algorithms like [binary exponentiation](@entry_id:276203), this evaluates to $1$, showing that $123$ is a [quadratic residue](@entry_id:199089) modulo $1009$ [@problem_id:3021788].

#### Gauss's Lemma

A second, more combinatorial criterion was developed by Carl Friedrich Gauss and was instrumental in his proofs of [quadratic reciprocity](@entry_id:184657). **Gauss's Lemma** provides a method to determine $\left(\frac{a}{p}\right)$ by counting. Consider the set of multiples of $a$:
$$ S = \left\{ a, 2a, 3a, \dots, \frac{p-1}{2}a \right\} $$
For each element in $S$, find its **least absolute residue** modulo $p$, which is the unique representative in the interval $(-p/2, p/2)$. Let $N$ be the number of these least absolute residues that are negative. Gauss's Lemma states that:
$$ \left(\frac{a}{p}\right) = (-1)^N $$
The proof involves comparing the product of the elements of $S$ modulo $p$ with $((p-1)/2)!$. A negative least absolute residue arises when a multiple $ka$ falls into an interval of the form $(mp + p/2, (m+1)p)$ for some integer $m$. Counting the number of $k \in \{1, \dots, (p-1)/2\}$ that satisfy this condition for any $m$ gives the value of $N$ [@problem_id:3021797]. For example, applying this intricate counting procedure for $\left(\frac{5}{2017}\right)$, one finds that $N=403$. Since $403$ is odd, $\left(\frac{5}{2017}\right) = (-1)^{403} = -1$.

### The Law of Quadratic Reciprocity

While Euler's criterion and Gauss's Lemma are powerful, the jewel of the theory is the **Law of Quadratic Reciprocity**. This profound law, first proven by Gauss, relates the value of $\left(\frac{p}{q}\right)$ to the value of $\left(\frac{q}{p}\right)$ for distinct odd primes $p$ and $q$.

**The Law of Quadratic Reciprocity**: If $p$ and $q$ are distinct odd primes, then
$$ \left(\frac{p}{q}\right)\left(\frac{q}{p}\right) = (-1)^{\frac{p-1}{2}\frac{q-1}{2}} $$
The exponent on the right is $1$ unless both $p$ and $q$ are of the form $4k+3$, in which case it is $-1$. This allows one to "flip" the Legendre symbol, reducing the "numerator" and "denominator" until a value can be determined.

The main law is accompanied by two **supplementary laws** that handle the cases of $-1$ and $2$:

**First Supplementary Law**: $\left(\frac{-1}{p}\right) = (-1)^{\frac{p-1}{2}}$.
This is an immediate consequence of Euler's criterion. It implies that $-1$ is a [quadratic residue](@entry_id:199089) modulo $p$ if and only if $p \equiv 1 \pmod 4$.

**Second Supplementary Law**: $\left(\frac{2}{p}\right) = (-1)^{\frac{p^2-1}{8}}$.
This is typically proven using Gauss's Lemma. It implies that $2$ is a [quadratic residue](@entry_id:199089) modulo $p$ if and only if $p \equiv 1$ or $7 \pmod 8$.

These laws combine to provide a highly efficient algorithm for computing any Legendre symbol. For instance, we may wish to determine if both $-1$ and $2$ are [quadratic residues](@entry_id:180432) modulo $p$. This requires $\left(\frac{-1}{p}\right) = 1$ and $\left(\frac{2}{p}\right) = 1$. The first condition implies $p \equiv 1 \pmod 4$, and the second implies $p \equiv 1 \text{ or } 7 \pmod 8$. The only way to satisfy both is if $p \equiv 1 \pmod 8$. Thus, the behavior of these two fundamental symbols is fully determined by the residue class of $p$ modulo $8$, making $m=8$ the minimal modulus for this classification [@problem_id:3021800].

As a comprehensive example of the law's power, consider computing $\left(\frac{a}{p}\right)$ for $a=-2^{5}\cdot 3^{2}\cdot 5\cdot 7^{3}\cdot 11\cdot 13^{2}\cdot 17$ and $p=1,000,003$. Using the multiplicativity and square-rules for the Legendre symbol, this reduces to computing a product of simpler symbols. Each of these can be evaluated using reciprocity, reducing a complex problem to a series of simple [modular arithmetic](@entry_id:143700) checks [@problem_id:3021777].

### Generalizations and Advanced Topics

The theory of [quadratic residues](@entry_id:180432) extends in several important directions, connecting it to algebraic number theory, harmonic analysis, and the theory of quadratic forms.

#### The Jacobi Symbol

The Legendre symbol is defined only for prime moduli. The **Jacobi symbol** $\left(\frac{a}{n}\right)$ extends the notation to any odd composite integer $n > 1$. If $n = p_1^{k_1} \cdots p_m^{k_m}$ is the prime factorization of $n$, the Jacobi symbol is defined as:
$$ \left(\frac{a}{n}\right) = \left(\frac{a}{p_1}\right)^{k_1} \cdots \left(\frac{a}{p_m}\right)^{k_m} $$
where the symbols on the right are Legendre symbols. The Jacobi symbol inherits properties like multiplicativity in both arguments and, remarkably, also obeys the same law of [quadratic reciprocity](@entry_id:184657). This makes it a powerful computational tool, as one can use the reciprocity algorithm without needing to factor the modulus.

However, there is a crucial caveat. If $\left(\frac{a}{p}\right)=1$, then $a$ is a [quadratic residue](@entry_id:199089) modulo $p$. But if $\left(\frac{a}{n}\right)=1$ for composite $n$, it **does not** imply that $a$ is a [quadratic residue](@entry_id:199089) modulo $n$. The [congruence](@entry_id:194418) $x^2 \equiv a \pmod n$ is solvable if and only if $x^2 \equiv a \pmod{p_i}$ is solvable for *every* prime factor $p_i$ of $n$. This requires $\left(\frac{a}{p_i}\right)=1$ for all $i$. The Jacobi symbol $\left(\frac{a}{n}\right)$ can be $1$ if an even number of its constituent Legendre symbols are $-1$. For example, for $n=77=7 \times 11$, consider $a=6$. We have $\left(\frac{6}{7}\right)=-1$ and $\left(\frac{6}{11}\right)=-1$. Thus, the Jacobi symbol $\left(\frac{6}{77}\right) = (-1)(-1) = 1$. However, since $\left(\frac{6}{7}\right)=-1$, the [congruence](@entry_id:194418) $x^2 \equiv 6 \pmod 7$ has no solution, and thus $x^2 \equiv 6 \pmod{77}$ has no solution [@problem_id:3021795].

#### Quadratic Gauss Sums

A deep connection exists between [quadratic residues](@entry_id:180432) and Fourier analysis on [finite fields](@entry_id:142106). For a character $\psi: \mathbb{F}_p \to \mathbb{C}^\times$ of the [additive group](@entry_id:151801) and a character $\chi: \mathbb{F}_p^\times \to \mathbb{C}^\times$ of the [multiplicative group](@entry_id:155975), the **Gauss sum** is defined as $G(\chi, \psi) = \sum_{x \in \mathbb{F}_p^\times} \chi(x)\psi(x)$.

The canonical additive character is $\psi_1(x) = \exp(2\pi i x/p)$, and the quadratic character is $\chi_2(x) = \left(\frac{x}{p}\right)$. The associated **quadratic Gauss sum** is $G(\chi_2) = \sum_{t \in \mathbb{F}_p} \left(\frac{t}{p}\right) \exp(2\pi i t/p)$. This sum is fundamental. Gauss himself proved the remarkable identity $|G(\chi_2)| = \sqrt{p}$, and after much effort, determined its sign: $G(\chi_2) = \sqrt{p}$ if $p \equiv 1 \pmod 4$ and $G(\chi_2) = i\sqrt{p}$ if $p \equiv 3 \pmod 4$.

These sums appear naturally when evaluating more general quadratic [exponential sums](@entry_id:199860), such as $S(a,b;p) = \sum_{x \in \mathbb{F}_{p}} \exp( \frac{2\pi i}{p}\,(a x^{2} + b x) )$ for $a \not\equiv 0$. By completing the square in the exponent (which is possible since $p$ is odd), one can relate this sum directly to the fundamental quadratic Gauss sum. The derivation yields the elegant formula [@problem_id:3021796]:
$$ S(a,b;p) = \left(\frac{a}{p}\right) G(\chi_2) \exp\left(-\frac{2\pi i b^2 (4a)^{-1}}{p}\right) $$
This result is a prototype for many deeper results in analytic number theory concerning the evaluation of [exponential sums](@entry_id:199860).

#### The Hilbert Symbol

The theory of [quadratic residues](@entry_id:180432) serves as the foundation for the study of quadratic forms over [local fields](@entry_id:195717), such as the field of $p$-adic numbers $\mathbb{Q}_p$. For $a, b \in \mathbb{Q}_p^\times$, the **Hilbert symbol** $(a,b)_p$ is defined to be $1$ if the quadratic form $z^2 = ax^2 + by^2$ has a non-[trivial solution](@entry_id:155162) in $\mathbb{Q}_p$, and $-1$ otherwise. This is equivalent to $b$ being a norm from the field extension $\mathbb{Q}_p(\sqrt{a})$.

The Hilbert symbol can be computed via explicit formulas that depend on the $p$-adic valuation $v_p$ and the residue class of the numbers. Any $a \in \mathbb{Q}_p^\times$ can be written as $a = p^{v_p(a)} u$ where $u \in \mathbb{Z}_p^\times$ is a $p$-adic unit. Let $\alpha=v_p(a)$ and $\beta=v_p(b)$.

For an **odd prime** $p$, the formula is:
$$ (a,b)_p = (-1)^{\alpha\beta \frac{p-1}{2}} \left(\frac{u \pmod p}{p}\right)^\beta \left(\frac{v \pmod p}{p}\right)^\alpha $$
This formula beautifully illustrates that the solvability of a quadratic equation over $\mathbb{Q}_p$ is determined by the properties of [quadratic residues](@entry_id:180432) in the residue field $\mathbb{F}_p$.

For $p=2$, the situation is more subtle and depends on [residue classes](@entry_id:185226) modulo $8$. The formula is:
$$ (a,b)_2 = (-1)^{\frac{u-1}{2}\frac{v-1}{2} + \alpha \frac{v^2-1}{8} + \beta \frac{u^2-1}{8}} $$
These formulas, derived from first principles using Hensel's Lemma and properties of $p$-adic fields, are essential tools in the classification of [quadratic forms](@entry_id:154578) and in [class field theory](@entry_id:155687). For instance, one can compute $(7^2 \cdot 3, 7 \cdot 5)_7 = -1$ and $(2^3 \cdot 5, 2^2 \cdot 3)_2 = -1$ by direct application of these rules [@problem_id:3021792]. The Hilbert symbol thus encapsulates the "local" behavior of [quadratic extensions](@entry_id:204617), and its properties form the basis for the Hasse-Minkowski theorem, which relates the solvability of quadratic equations over $\mathbb{Q}$ to their solvability over all completions $\mathbb{Q}_p$ and $\mathbb{R}$.