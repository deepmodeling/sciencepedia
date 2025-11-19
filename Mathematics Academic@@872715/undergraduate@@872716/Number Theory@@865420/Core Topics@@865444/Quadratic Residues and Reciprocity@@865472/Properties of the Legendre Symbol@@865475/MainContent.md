## Introduction
In number theory, determining the solvability of [quadratic congruences](@entry_id:199460) of the form $x^2 \equiv a \pmod{p}$ is a foundational question. While simple for small numbers, this problem requires a systematic and efficient framework for larger primes. The Legendre symbol, introduced by Adrien-Marie Legendre, provides precisely this framework, offering an elegant language to classify integers as [quadratic residues](@entry_id:180432) or nonresidues.

This article bridges the gap between the definition of [quadratic residues](@entry_id:180432) and their powerful applications. It unpacks the theory behind the Legendre symbol, revealing the deep structural properties that make it a cornerstone of modern number theory.

You will first learn the core principles and mechanisms governing the Legendre symbol, from its definition and basic properties to the celebrated Law of Quadratic Reciprocity. Next, we will explore its diverse applications and interdisciplinary connections, showing how it serves as a critical tool in fields like [cryptography](@entry_id:139166) and algebraic number theory. Finally, a series of hands-on practices will allow you to apply these concepts and solidify your understanding. This journey begins with a deep dive into the foundational concepts that make the Legendre symbol such a powerful tool.

## Principles and Mechanisms

In the study of [quadratic congruences](@entry_id:199460), a central question is to determine, for a given integer $a$ and a prime modulus $p$, whether the [congruence](@entry_id:194418) $x^2 \equiv a \pmod{p}$ admits a solution. The theoretical and computational framework for answering this question is built upon the elegant properties of the Legendre symbol. This chapter elucidates the principles that govern this symbol, from its fundamental definition to the profound law of [quadratic reciprocity](@entry_id:184657).

### Definition and Core Interpretation

Let $p$ be an odd prime. An integer $a$ not divisible by $p$ is called a **[quadratic residue](@entry_id:199089) modulo $p$** if the [congruence](@entry_id:194418) $x^2 \equiv a \pmod{p}$ has a solution. If it has no solution, $a$ is called a **quadratic nonresidue modulo $p$**. This [binary classification](@entry_id:142257) forms the basis of our inquiry.

To formalize this concept, Adrien-Marie Legendre introduced a notational device. The **Legendre symbol**, denoted $\left(\frac{a}{p}\right)$, is a function of an integer $a$ and an odd prime $p$ defined as follows [@problem_id:3088812] [@problem_id:3088792]:
$$
\left(\frac{a}{p}\right) = 
\begin{cases} 
1  \text{if } a \text{ is a quadratic residue modulo } p \\
-1  \text{if } a \text{ is a quadratic nonresidue modulo } p \\
0  \text{if } p \mid a 
\end{cases}
$$

The value of the symbol directly informs us about the solvability and the number of solutions to the [congruence](@entry_id:194418) $x^2 \equiv a \pmod{p}$.
*   If $\left(\frac{a}{p}\right) = 1$, there are exactly **two** solutions modulo $p$. If $x_0$ is one solution, so $x_0^2 \equiv a \pmod{p}$, then $(-x_0)^2 \equiv a \pmod{p}$ as well. These two solutions, $x_0$ and $-x_0$, are distinct because $p$ is an odd prime, which ensures $x_0 \not\equiv -x_0 \pmod{p}$ unless $x_0 \equiv 0 \pmod{p}$ (a case ruled out since $p \nmid a$).
*   If $\left(\frac{a}{p}\right) = -1$, there are, by definition, **no** solutions.
*   If $\left(\frac{a}{p}\right) = 0$, the [congruence](@entry_id:194418) is $x^2 \equiv 0 \pmod{p}$. Since $p$ is prime, this implies $p \mid x$, yielding the single unique solution $x \equiv 0 \pmod{p}$.

An elegant summary is that the number of solutions to $x^2 \equiv a \pmod{p}$ is precisely $1 + \left(\frac{a}{p}\right)$ [@problem_id:3088792].

To make this concrete, let's examine the [quadratic residues](@entry_id:180432) for the prime $p=11$ [@problem_id:3088821]. We compute the squares of the non-zero elements modulo $11$:
$1^2 \equiv 1$, $2^2 \equiv 4$, $3^2 \equiv 9$, $4^2 \equiv 16 \equiv 5$, $5^2 \equiv 25 \equiv 3$.
Since $(-x)^2 \equiv x^2$, the squares of $6, 7, 8, 9, 10$ will produce the same values. The set of [quadratic residues](@entry_id:180432) modulo $11$ is $\{1, 3, 4, 5, 9\}$. The quadratic nonresidues are the remaining elements: $\{2, 6, 7, 8, 10\}$.
Thus, for example, $\left(\frac{5}{11}\right)=1$ because $x^2 \equiv 5 \pmod{11}$ is solvable (by $x=\pm 4$), while $\left(\frac{6}{11}\right)=-1$ because $x^2 \equiv 6 \pmod{11}$ is not solvable.

### Fundamental Properties

The Legendre symbol possesses several properties that are essential for its computation and theoretical application.

#### Periodicity
The value of $\left(\frac{a}{p}\right)$ depends only on the residue class of $a$ modulo $p$. That is, if $a \equiv b \pmod{p}$, then $\left(\frac{a}{p}\right) = \left(\frac{b}{p}\right)$. This follows directly from the definition: if $a \equiv b \pmod{p}$, then the [congruence](@entry_id:194418) $x^2 \equiv a \pmod{p}$ is equivalent to $x^2 \equiv b \pmod{p}$, meaning they have the same solutions and thus the same solvability status. Similarly, $p \mid a$ if and only if $p \mid b$. This property allows us to always reduce the "numerator" of the symbol modulo the "denominator" before proceeding with other calculations [@problem_id:3088793].

For example, to compute $\left(\frac{57}{17}\right)$, we first note that $57 = 3 \times 17 + 6$, so $57 \equiv 6 \pmod{17}$. Therefore, $\left(\frac{57}{17}\right) = \left(\frac{6}{17}\right)$. We can then determine if $6$ is a square modulo $17$ by checking the squares of integers from $1$ to $8$. None of these squares is congruent to $6$, so $6$ is a nonresidue, and $\left(\frac{6}{17}\right)=-1$. Thus, $\left(\frac{57}{17}\right) = -1$.

#### Complete Multiplicativity
For any integers $a$ and $b$, the Legendre symbol is completely multiplicative in its top argument:
$$ \left(\frac{ab}{p}\right) = \left(\frac{a}{p}\right)\left(\frac{b}{p}\right) $$
This property establishes the Legendre symbol as a character of the [multiplicative group](@entry_id:155975) $(\mathbb{Z}/p\mathbb{Z})^\times$. A direct and important consequence is that the product of two [quadratic residues](@entry_id:180432) is a residue, the product of a residue and a nonresidue is a nonresidue, and the product of two nonresidues is a residue.

From this, it follows that for any integer $b$ not divisible by $p$, the square $b^2$ is always a [quadratic residue](@entry_id:199089), so $\left(\frac{b^2}{p}\right) = 1$. This leads to a useful identity [@problem_id:3088819]:
$$ \left(\frac{ab^2}{p}\right) = \left(\frac{a}{p}\right)\left(\frac{b^2}{p}\right) = \left(\frac{a}{p}\right) \cdot 1 = \left(\frac{a}{p}\right) $$
This shows that the value of the Legendre symbol is unchanged when its numerator is multiplied by a non-zero square. In the language of group theory, this means the Legendre symbol is well-defined on the square classes of the multiplicative group $(\mathbb{Z}/p\mathbb{Z})^\times$.

### Criteria for Calculation

While the definition of the Legendre symbol is clear, testing for solvability by checking all possible squares can be inefficient. Two major results, Euler's Criterion and Gauss's Lemma, provide powerful algorithms for computing the symbol's value.

#### Euler's Criterion
This criterion provides a direct formula for the Legendre symbol. For an odd prime $p$ and an integer $a$ with $p \nmid a$, Euler's Criterion states:
$$ \left(\frac{a}{p}\right) \equiv a^{\frac{p-1}{2}} \pmod{p} $$
Since the values of both sides of the [congruence](@entry_id:194418) must be in the set $\{-1, 1\}$, and since $p > 2$ implies $1 \not\equiv -1 \pmod p$, the [congruence](@entry_id:194418) is in fact an equality. This criterion arises from the structure of the cyclic group $(\mathbb{Z}/p\mathbb{Z})^\times$, where an element is a square if and only if its exponent in terms of a primitive root is even [@problem_id:3088812]. The elements satisfying $y^{(p-1)/2} \equiv 1 \pmod p$ are precisely the [quadratic residues](@entry_id:180432) [@problem_id:3088821].

As an example, let's compute $\left(\frac{5}{23}\right)$ using Euler's Criterion [@problem_id:3088817]. We have $p=23$ and $a=5$. The exponent is $\frac{23-1}{2}=11$. We need to compute $5^{11} \pmod{23}$. Using [binary exponentiation](@entry_id:276203):
$5^1 \equiv 5 \pmod{23}$
$5^2 = 25 \equiv 2 \pmod{23}$
$5^4 \equiv 2^2 \equiv 4 \pmod{23}$
$5^8 \equiv 4^2 \equiv 16 \pmod{23}$
Since $11 = 8+2+1$, we have $5^{11} = 5^8 \cdot 5^2 \cdot 5^1 \equiv 16 \cdot 2 \cdot 5 = 160 \pmod{23}$. As $160 = 6 \cdot 23 + 22$, we get $5^{11} \equiv 22 \equiv -1 \pmod{23}$.
Therefore, $\left(\frac{5}{23}\right) = -1$.

#### Gauss's Lemma
Gauss's Lemma offers an alternative computational method based on counting. Let $p$ be an odd prime and $a$ be an integer with $p \nmid a$. Consider the set $S = \{a, 2a, 3a, \dots, \frac{p-1}{2}a\}$. Reduce each element of $S$ modulo $p$ to its least absolute residue, i.e., an integer in the interval $[-(p-1)/2, (p-1)/2]$. Let $n$ be the number of these residues that are negative. Gauss's Lemma states:
$$ \left(\frac{a}{p}\right) = (-1)^n $$

For example, to compute $\left(\frac{3}{11}\right)$ using Gauss's Lemma [@problem_id:3088779], we have $p=11$, $a=3$, and $(p-1)/2 = 5$. The set is $S = \{3 \cdot 1, 3 \cdot 2, 3 \cdot 3, 3 \cdot 4, 3 \cdot 5\} = \{3, 6, 9, 12, 15\}$. We find the least absolute residues modulo $11$ (in the range $[-5, 5]$):
*   $3 \equiv 3 \pmod{11}$
*   $6 \equiv -5 \pmod{11}$
*   $9 \equiv -2 \pmod{11}$
*   $12 \equiv 1 \pmod{11}$
*   $15 \equiv 4 \pmod{11}$
The resulting set of residues is $\{3, -5, -2, 1, 4\}$. There are $n=2$ negative residues. According to Gauss's Lemma, $\left(\frac{3}{11}\right) = (-1)^2 = 1$.

### The Law of Quadratic Reciprocity

The properties and criteria discussed so far culminate in one of the most celebrated results in elementary number theory: the Law of Quadratic Reciprocity. This law, first conjectured by Euler and Legendre and later proven by Gauss, reveals a stunning symmetry in the relationship between Legendre symbols. It is comprised of a main law and two supplements.

#### The First and Second Supplements
The supplements provide explicit formulas for the Legendre symbols $\left(\frac{-1}{p}\right)$ and $\left(\frac{2}{p}\right)$, which frequently appear in calculations. They can be derived from Euler's Criterion and Gauss's Lemma, respectively [@problem_id:3088786].

The **first supplement** concerns the residuosity of $-1$:
$$ \left(\frac{-1}{p}\right) = (-1)^{\frac{p-1}{2}} $$
This implies that $-1$ is a [quadratic residue](@entry_id:199089) modulo $p$ if and only if $p \equiv 1 \pmod{4}$.

The **second supplement** addresses the residuosity of $2$:
$$ \left(\frac{2}{p}\right) = (-1)^{\frac{p^2-1}{8}} $$
This shows that $2$ is a [quadratic residue](@entry_id:199089) modulo $p$ if and only if $p \equiv 1 \text{ or } 7 \pmod{8}$.

#### The Main Law
The main law relates the value of $\left(\frac{p}{q}\right)$ to that of $\left(\frac{q}{p}\right)$ for distinct odd primes $p$ and $q$:
$$ \left(\frac{p}{q}\right)\left(\frac{q}{p}\right) = (-1)^{\frac{p-1}{2}\frac{q-1}{2}} $$
This remarkable result connects the solvability of $x^2 \equiv p \pmod q$ with that of $x^2 \equiv q \pmod p$. The right-hand side is $1$ unless both $(p-1)/2$ and $(q-1)/2$ are odd, which occurs if and only if both $p \equiv 3 \pmod 4$ and $q \equiv 3 \pmod 4$.
Thus, the law can be stated as:
*   $\left(\frac{p}{q}\right) = \left(\frac{q}{p}\right)$ if either $p$ or $q$ (or both) is congruent to $1 \pmod 4$.
*   $\left(\frac{p}{q}\right) = -\left(\frac{q}{p}\right)$ if both $p$ and $q$ are congruent to $3 \pmod 4$.

The derivation of this law, for example via Eisenstein's geometric interpretation of Gauss's Lemma, reveals a deep parity structure governing the residues [@problem_id:3088795]. For the case where $p \equiv 3 \pmod 4$ and $q \equiv 3 \pmod 4$, both exponents $\frac{p-1}{2}$ and $\frac{q-1}{2}$ are odd. Their product is odd, making the exponent in the [reciprocity law](@entry_id:185655) odd, and thus $\left(\frac{p}{q}\right)\left(\frac{q}{p}\right) = -1$.

### Generalization: The Jacobi Symbol

The Legendre symbol is defined only for prime moduli. For computational purposes, it is convenient to generalize this to [composite moduli](@entry_id:189955). The **Jacobi symbol**, denoted $\left(\frac{a}{n}\right)$, serves this purpose for any odd integer $n > 1$.

If $n$ has the [prime factorization](@entry_id:152058) $n = p_1^{e_1} p_2^{e_2} \cdots p_r^{e_r}$, the Jacobi symbol is defined as the product of the corresponding Legendre symbols [@problem_id:3088813]:
$$ \left(\frac{a}{n}\right) = \prod_{i=1}^{r} \left(\frac{a}{p_i}\right)^{e_i} $$

The Jacobi symbol inherits many properties of the Legendre symbol, including complete multiplicativity in both its upper and lower arguments, and it satisfies analogous laws of reciprocity. However, there is one crucial distinction.

While for a prime $p$, $\left(\frac{a}{p}\right)=1$ is equivalent to $a$ being a [quadratic residue](@entry_id:199089) modulo $p$, this equivalence breaks down for the Jacobi symbol. If $a$ is a [quadratic residue](@entry_id:199089) modulo a composite $n$, then it must be a [quadratic residue](@entry_id:199089) modulo each prime factor $p_i$ of $n$. This means $\left(\frac{a}{p_i}\right)=1$ for all $i$, which implies $\left(\frac{a}{n}\right)=1$. So, if $\left(\frac{a}{n}\right) \neq 1$, then $a$ cannot be a [quadratic residue](@entry_id:199089).

However, the converse is false. A Jacobi symbol value of $1$ does **not** guarantee that $a$ is a [quadratic residue](@entry_id:199089) modulo $n$. The product defining the symbol can be $1$ if an even number of its terms are $-1$. If even one of these terms is $-1$, say $\left(\frac{a}{p_j}\right)=-1$, then the congruence $x^2 \equiv a \pmod{p_j}$ is unsolvable, which by the Chinese Remainder Theorem makes $x^2 \equiv a \pmod n$ unsolvable.

Let us find a concrete example for $n=77=7 \times 11$ [@problem_id:3088799]. We seek the smallest positive integer $a$ such that $\left(\frac{a}{77}\right)=1$ but $x^2 \equiv a \pmod{77}$ is unsolvable.
For unsolvability, we require that $a$ is a nonresidue for at least one of the prime factors. For $\left(\frac{a}{77}\right) = \left(\frac{a}{7}\right)\left(\frac{a}{11}\right)$ to be $1$, the only way for unsolvability is if both factors are $-1$.
So we need the smallest $a$ such that $\left(\frac{a}{7}\right)=-1$ and $\left(\frac{a}{11}\right)=-1$.
*   Quadratic nonresidues mod 7 are $\{3, 5, 6\}$.
*   Quadratic nonresidues mod 11 are $\{2, 6, 7, 8, 10\}$.
We test small integers:
*   $a=1,2,3,4,5$: at least one symbol is $1$.
*   $a=6$: $\left(\frac{6}{7}\right) = \left(\frac{-1}{7}\right) = (-1)^{(7-1)/2}=-1$. Also, $6$ is a nonresidue mod $11$, so $\left(\frac{6}{11}\right)=-1$.
Thus for $a=6$, we have $\left(\frac{6}{77}\right) = (-1)(-1)=1$, but $x^2 \equiv 6 \pmod{77}$ is unsolvable because $x^2 \equiv 6 \pmod 7$ is unsolvable. The integer $a=6$ is the smallest such example. This vividly illustrates the subtle but critical difference between the Legendre and Jacobi symbols.