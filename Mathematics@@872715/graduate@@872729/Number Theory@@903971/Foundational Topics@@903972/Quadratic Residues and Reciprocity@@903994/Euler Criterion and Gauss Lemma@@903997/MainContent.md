## Introduction
The question of which numbers are perfect squares is elementary in standard arithmetic, but it becomes a rich and complex problem when considered within the finite systems of modular arithmetic. Determining whether an integer $a$ is a [quadratic residue](@entry_id:199089) modulo a prime $p$—that is, whether the [congruence](@entry_id:194418) $x^2 \equiv a \pmod{p}$ has a solution—is a central problem in number theory. This article explores two landmark results that provide elegant and efficient answers: Euler's Criterion and Gauss's Lemma. We will journey through the theoretical heart of these tools, see their power in action, and apply our understanding to concrete problems.

The first chapter, "Principles and Mechanisms," lays the foundation by introducing the Legendre symbol and dissecting the algebraic and [combinatorial proofs](@entry_id:261407) of Euler's Criterion and Gauss's Lemma. Following this, "Applications and Interdisciplinary Connections" broadens our perspective, revealing how these concepts are applied in algorithms, [cryptography](@entry_id:139166), and serve as a gateway to advanced topics like [class field theory](@entry_id:155687) and representation theory. Finally, the "Hands-On Practices" section will challenge you to solidify your understanding by using these theorems to solve computational problems and verify their predictions.

## Principles and Mechanisms

In the preceding chapter, we introduced the fundamental problem of identifying square numbers within the finite arithmetic systems of integers modulo $p$. This chapter delves into the principal theoretical tools developed to solve this problem: Euler's Criterion and Gauss's Lemma. We will explore their algebraic and combinatorial underpinnings, demonstrate their utility, and investigate the crucial distinctions that arise when generalizing these ideas from prime to [composite moduli](@entry_id:189955).

### The Legendre Symbol: A Language for Quadratic Residuosity

Let $p$ be an odd prime. The central question of quadratic residuosity is: for a given integer $a$, does the [congruence](@entry_id:194418) $x^2 \equiv a \pmod{p}$ have an integer solution for $x$? If a solution exists, we say that $a$ is a **[quadratic residue](@entry_id:199089)** modulo $p$. If $a \not\equiv 0 \pmod{p}$ and no such solution exists, $a$ is called a **quadratic non-residue** modulo $p$. The set of all [quadratic residues](@entry_id:180432) modulo $p$ is formally the set $\{x^2 \pmod{p} : x \in \mathbb{Z}\}$. This naturally includes $0$, since $0 \equiv 0^2 \pmod{p}$. [@problem_id:3013388]

To [streamline](@entry_id:272773) our discussion, we introduce a powerful notation devised by Adrien-Marie Legendre. The **Legendre symbol**, denoted $\left(\frac{a}{p}\right)$, is a function that encapsulates the quadratic character of $a$ with respect to the odd prime $p$. It is defined as follows:
$$
\left(\frac{a}{p}\right) = 
\begin{cases} 
1  \text{if } a \text{ is a quadratic residue modulo } p \text{ and } a \not\equiv 0 \pmod{p} \\
-1  \text{if } a \text{ is a quadratic non-residue modulo } p \\
0  \text{if } a \equiv 0 \pmod{p} 
\end{cases}
$$
This compact notation transforms the question of solvability into the problem of evaluating a specific arithmetic function. For example, stating that $\left(\frac{a}{p}\right) = 1$ is synonymous with stating that $x^2 \equiv a \pmod{p}$ is solvable for some $x \not\equiv 0 \pmod p$. [@problem_id:3013374]

The definition of $\left(\frac{0}{p}\right) = 0$ is a deliberate and crucial choice. While $0$ is technically a [quadratic residue](@entry_id:199089), assigning it a value of $0$ preserves several elegant properties of the symbol. Most notably, it ensures that the Legendre symbol is a **[completely multiplicative function](@entry_id:635567)** in its top argument; that is, $\left(\frac{ab}{p}\right) = \left(\frac{a}{p}\right)\left(\frac{b}{p}\right)$ for all integers $a$ and $b$. To see why $\left(\frac{0}{p}\right)$ must be $0$ for this property to hold, consider a non-residue $b$ such that $\left(\frac{b}{p}\right)=-1$. If the multiplicative property is to hold for $a=0$, we must have $\left(\frac{0 \cdot b}{p}\right) = \left(\frac{0}{p}\right)\left(\frac{b}{p}\right)$. This simplifies to $\left(\frac{0}{p}\right) = \left(\frac{0}{p}\right)(-1)$, which implies $2\left(\frac{0}{p}\right) = 0$, forcing the conclusion that $\left(\frac{0}{p}\right) = 0$. [@problem_id:3013376]

### Euler's Criterion: An Algebraic Approach

While the Legendre symbol provides the language to state the problem, it does not, by itself, provide a method of computation more efficient than trial-and-error. The first major computational breakthrough is **Euler's Criterion**, which connects the Legendre symbol to [modular exponentiation](@entry_id:146739).

To understand this criterion, we must first appreciate the structure of the [multiplicative group of units](@entry_id:184288) modulo $p$, denoted $(\mathbb{Z}/p\mathbb{Z})^{\times}$. This is the set of non-zero [residue classes](@entry_id:185226) modulo $p$, $\{1, 2, \dots, p-1\}$, under multiplication. A foundational result in number theory states that for any prime $p$, the group $(\mathbb{Z}/p\mathbb{Z})^{\times}$ is cyclic. This means there exists at least one element $g$, called a **[primitive root](@entry_id:138841)**, that generates the entire group. Every non-zero residue $a$ can be uniquely written as $a \equiv g^k \pmod{p}$ for some integer $k$ in the range $0 \le k \le p-2$. The integer $k$ is known as the [discrete logarithm](@entry_id:266196) of $a$ to the base $g$. [@problem_id:3013402]

Within this cyclic structure, the [quadratic residues](@entry_id:180432) are precisely the elements that are even powers of the generator $g$. If $a \equiv x^2 \pmod{p}$ and $x \equiv g^m$, then $a \equiv (g^m)^2 = g^{2m}$. Conversely, any element of the form $g^{2m} = (g^m)^2$ is a square. The [quadratic non-residues](@entry_id:201109) are the odd powers of $g$. This reveals that exactly half of the elements in $(\mathbb{Z}/p\mathbb{Z})^{\times}$ are [quadratic residues](@entry_id:180432), and the other half are non-residues. The set of [quadratic residues](@entry_id:180432) forms a subgroup of index 2 within $(\mathbb{Z}/p\mathbb{Z})^{\times}$. [@problem_id:3013402]

This structure leads directly to Euler's Criterion. For any integer $a$ with $\gcd(a,p)=1$:
$$ \left(\frac{a}{p}\right) \equiv a^{\frac{p-1}{2}} \pmod{p} $$
The condition $\gcd(a,p)=1$ is paramount. If it holds, then $a \in (\mathbb{Z}/p\mathbb{Z})^{\times}$. By Fermat's Little Theorem, $a^{p-1} \equiv 1 \pmod{p}$. Letting $x = a^{(p-1)/2}$, we have $x^2 \equiv 1 \pmod{p}$, whose only solutions in the field $\mathbb{Z}/p\mathbb{Z}$ are $x \equiv 1 \pmod{p}$ and $x \equiv -1 \pmod{p}$ (since $p$ is odd). [@problem_id:3013406] The specific value is determined by the parity of the [discrete logarithm](@entry_id:266196) of $a$. If $a \equiv g^k \pmod p$, then
$$ a^{\frac{p-1}{2}} \equiv (g^k)^{\frac{p-1}{2}} = (g^{\frac{p-1}{2}})^k \pmod{p} $$
Since $g$ is a [primitive root](@entry_id:138841), its order is $p-1$, so $g^{\frac{p-1}{2}} \not\equiv 1 \pmod{p}$. As its square is $1$, it must be that $g^{\frac{p-1}{2}} \equiv -1 \pmod{p}$. Therefore, $a^{\frac{p-1}{2}} \equiv (-1)^k \pmod{p}$. This is $1$ if $k$ is even (i.e., $a$ is a [quadratic residue](@entry_id:199089)) and $-1$ if $k$ is odd (i.e., $a$ is a non-residue), perfectly matching the values of the Legendre symbol. [@problem_id:3013374] [@problem_id:3013402]

From a more abstract viewpoint, the map $\chi(a) = a^{(p-1)/2} \pmod{p}$ defines a [group homomorphism](@entry_id:140603) from $(\mathbb{Z}/p\mathbb{Z})^{\times}$ to the subgroup $\{\pm 1\}$. The kernel of this homomorphism is the set of elements for which $\chi(a)=1$, which, as we have seen, is precisely the subgroup of [quadratic residues](@entry_id:180432). This map $\chi$ is the unique nontrivial character of order 2 on the cyclic group $(\mathbb{Z}/p\mathbb{Z})^{\times}$. [@problem_id:3013402]

If we do not impose the condition $\gcd(a,p)=1$, then $a \equiv 0 \pmod p$. In this case, since $p \ge 3$, the exponent $\frac{p-1}{2}$ is a positive integer, so $a^{\frac{p-1}{2}} \equiv 0^{\frac{p-1}{2}} \equiv 0 \pmod p$. For the [congruence](@entry_id:194418) in Euler's Criterion to hold, we must have $\left(\frac{a}{p}\right) \equiv 0 \pmod p$, which confirms the consistency of our definition $\left(\frac{0}{p}\right) = 0$. [@problem_id:3013376]

### Gauss's Lemma: A Combinatorial Approach

While Euler's criterion provides an algebraic formula, Carl Friedrich Gauss discovered a remarkable alternative based on a simple counting argument. **Gauss's Lemma** offers a combinatorial method for determining the value of $\left(\frac{a}{p}\right)$.

Let $p$ be an odd prime and $a$ be an integer with $\gcd(a,p)=1$. Consider the following set of $\frac{p-1}{2}$ integers:
$$ S = \left\{ a, 2a, 3a, \dots, \left(\frac{p-1}{2}\right)a \right\} $$
The lemma has two common but equivalent formulations based on how we analyze the residues of these numbers modulo $p$.

**First Formulation: Least Positive Residues**

Let $r_j$ be the least positive residue of $ja$ modulo $p$ for each $j \in \{1, 2, \dots, \frac{p-1}{2}\}$. This means $ja \equiv r_j \pmod p$ and $1 \le r_j \le p-1$. Let $N$ be the number of these residues that are greater than $\frac{p}{2}$. Gauss's Lemma states:
$$ \left(\frac{a}{p}\right) = (-1)^N $$
Thus, $a$ is a [quadratic residue](@entry_id:199089) if and only if an even number of these first half-multiples of $a$ fall into the "upper half" of the [residue system](@entry_id:637054) $\{1, \dots, p-1\}$. [@problem_id:3013373] [@problem_id:3013390]

The proof involves comparing the product of the elements in $S$ with the product of their residues. The key insight is that the set $\{r_j\}$ can be partitioned into those less than $p/2$ and those greater than $p/2$. By replacing each residue $v_j > p/2$ with the value $p-v_j$, one can show that the set of modified residues forms a permutation of $\{1, 2, \dots, \frac{p-1}{2}\}$. Tracking the sign changes introduced by this modification—one for each of the $N$ residues greater than $p/2$—leads to the result $a^{(p-1)/2} \equiv (-1)^N \pmod p$. Combining this with Euler's Criterion yields the lemma.

**Second Formulation: Least Absolute Residues**

Alternatively, for each $ja \in S$, let $s_j$ be its unique representative in the symmetric set of residues $\left\{-\frac{p-1}{2}, \dots, -1, 1, \dots, \frac{p-1}{2}\right\}$. Let $m$ be the number of these representatives that are negative. Gauss's Lemma can then be stated as:
$$ \left(\frac{a}{p}\right) = (-1)^m $$
This formulation is often more convenient for proofs and computations. The core of its proof is very similar: one shows that the set of absolute values $\{|s_1|, |s_2|, \dots, |s_{(p-1)/2}|\}$ is a permutation of $\{1, 2, \dots, \frac{p-1}{2}\}$. Then, by taking the product of the congruences $ja \equiv s_j \pmod p$, one arrives at $a^{(p-1)/2} \equiv (-1)^m \pmod p$. [@problem_id:3013394]

Both formulations of Gauss's Lemma fundamentally depend on the condition $\gcd(a,p)=1$. If this condition fails, then $a \equiv 0 \pmod p$, and the set $S$ becomes $\{0, 0, \dots, 0\}$ modulo $p$. The entire counting argument, which relies on permutations of non-zero residues, collapses. [@problem_id:3013406]

### Generalization to Composite Moduli: The Jacobi Symbol

A natural question is whether we can extend the Legendre symbol to [composite moduli](@entry_id:189955). The **Jacobi symbol**, denoted $\left(\frac{a}{n}\right)$, provides such a generalization for any positive odd integer $n$.

Let $n = p_1^{e_1} p_2^{e_2} \cdots p_k^{e_k}$ be the [prime factorization](@entry_id:152058) of a positive odd integer $n$. For any integer $a$, the Jacobi symbol is defined as the product of the Legendre symbols for each prime factor:
$$ \left(\frac{a}{n}\right) = \prod_{i=1}^{k} \left(\frac{a}{p_i}\right)^{e_i} $$
If $\gcd(a,n) > 1$, then at least one prime factor $p_i$ of $n$ also divides $a$. This makes the corresponding Legendre symbol $\left(\frac{a}{p_i}\right)=0$, and consequently $\left(\frac{a}{n}\right)=0$. If $\gcd(a,n)=1$, each Legendre symbol is $\pm 1$, and so the Jacobi symbol is also $\pm 1$. [@problem_id:3013408]

The primary utility of the Jacobi symbol lies in its role in the law of [quadratic reciprocity](@entry_id:184657), which provides an efficient algorithm for computing Legendre symbols. However, it is crucial to understand what the Jacobi symbol does *not* do. Unlike the Legendre symbol for a prime modulus, the Jacobi symbol is not a reliable indicator of quadratic solvability.

Specifically, the condition $\left(\frac{a}{n}\right)=1$ **does not** imply that $a$ is a [quadratic residue](@entry_id:199089) modulo $n$.

The reason for this failure is embedded in the definition of the symbol as a product. The product can be equal to $1$ if an even number of its factors are $-1$. For $a$ to be a [quadratic residue](@entry_id:199089) modulo $n$, the [congruence](@entry_id:194418) $x^2 \equiv a \pmod n$ must be solvable. By the Chinese Remainder Theorem, this is equivalent to the [system of congruences](@entry_id:148057) $x^2 \equiv a \pmod{p_i^{e_i}}$ being solvable for every prime [power factor](@entry_id:270707) of $n$. This, in turn, requires $\left(\frac{a}{p_i}\right)=1$ for every prime factor $p_i$. If for even one prime factor $p_j$ we have $\left(\frac{a}{p_j}\right)=-1$, then $a$ is not a [quadratic residue](@entry_id:199089) modulo $p_j$, and thus cannot be a [quadratic residue](@entry_id:199089) modulo $n$. [@problem_id:3013403]

A classic example illustrates this point perfectly. Consider $n=15$ and $a=2$. The Jacobi symbol is:
$$ \left(\frac{2}{15}\right) = \left(\frac{2}{3}\right)\left(\frac{2}{5}\right) = (-1)(-1) = 1 $$
Despite the Jacobi symbol being $1$, the [congruence](@entry_id:194418) $x^2 \equiv 2 \pmod{15}$ has no solution. This is because it would require a simultaneous solution to $x^2 \equiv 2 \pmod{3}$ and $x^2 \equiv 2 \pmod{5}$. The first of these has no solution, as $2$ is a quadratic non-residue modulo $3$. [@problem_id:3013403]

The Jacobi symbol is not without interpretative power, however. If $\left(\frac{a}{n}\right)=-1$, it guarantees that for at least one prime factor $p_i$ of $n$ (with an odd exponent $e_i$), we have $\left(\frac{a}{p_i}\right)=-1$. This is sufficient to conclude that $a$ is a quadratic non-residue modulo $n$. In summary:
- If $\left(\frac{a}{n}\right) = -1$, then $a$ is a quadratic non-residue modulo $n$.
- If $a$ is a [quadratic residue](@entry_id:199089) modulo $n$ (and $\gcd(a,n)=1$), then $\left(\frac{a}{n}\right) = 1$.
- If $\left(\frac{a}{n}\right) = 1$, we can draw no certain conclusion about the quadratic character of $a$ modulo $n$.

Finally, it is worth noting that Euler's criterion does not generalize to [composite moduli](@entry_id:189955) in the form $a^{(n-1)/2} \equiv \left(\frac{a}{n}\right) \pmod{n}$. For instance, with $n=15$ and $a=2$, we have $\left(\frac{2}{15}\right)=1$, but $2^{(15-1)/2} = 2^7 = 128 \equiv 8 \pmod{15}$, not $1$. [@problem_id:3013408] This highlights that the elegant equivalence between solvability, the Legendre symbol, and Euler's criterion is a special property of prime moduli, rooted in the cyclic structure of their multiplicative groups.