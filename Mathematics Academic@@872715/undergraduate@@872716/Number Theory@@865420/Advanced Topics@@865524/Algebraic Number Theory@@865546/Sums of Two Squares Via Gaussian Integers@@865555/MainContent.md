## Introduction
The question of which integers can be written as the [sum of two squares](@entry_id:634766) is a classic problem in number theory, dating back to antiquity. While early results were found using elementary methods, the problem's full elegance and structure are only revealed when we step outside the familiar realm of integers, $\mathbb{Z}$, and into the richer world of Gaussian integers. Attempting to solve this problem solely within the integers obscures the underlying reasons for the patterns observed. The introduction of the algebraic structure $\mathbb{Z}[i]$ provides the key, transforming a difficult Diophantine equation into a more transparent question of factorization and norms.

This article will guide you through this powerful approach. In the first chapter, **Principles and Mechanisms**, we will establish the fundamental connection between [sums of two squares](@entry_id:154791) and the norm of Gaussian integers, explore the unique factorization property of $\mathbb{Z}[i]$, and use these tools to prove Fermat's celebrated theorem. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how this theory leads to concrete computational algorithms for finding representations and connects the problem to abstract algebra, geometry, and other areas of mathematics. Finally, the **Hands-On Practices** section will allow you to apply these concepts to solve specific problems, solidifying your understanding of this beautiful piece of number theory.

## Principles and Mechanisms

The question of which integers can be expressed as the [sum of two squares](@entry_id:634766) is a classical problem in number theory, with a history stretching back to antiquity. The complete and elegant solution to this problem, first stated by Pierre de Fermat and later proved by Leonhard Euler, finds its most natural and insightful explanation through the lens of a broader algebraic structure: the ring of Gaussian integers. By extending our arithmetic from the familiar integers $\mathbb{Z}$ to this new domain, the properties of [sums of two squares](@entry_id:154791) become transparent consequences of unique factorization.

### The Bridge from Integers to Gaussian Integers

The **ring of Gaussian integers**, denoted $\mathbb{Z}[i]$, consists of all complex numbers of the form $a+bi$ where $a$ and $b$ are ordinary integers and $i^2 = -1$. This set forms a ring under the [standard addition](@entry_id:194049) and multiplication of complex numbers. The key to connecting this structure to our problem is the **norm function**. For any Gaussian integer $\alpha = a+bi$, its norm $N(\alpha)$ is defined as:

$N(a+bi) = a^2 + b^2$

Geometrically, the norm is the square of the distance from the origin to the point $(a,b)$ in the complex plane. Notice that the norm of a Gaussian integer is always a non-negative integer. The crucial observation is that an integer $n$ can be written as a [sum of two squares](@entry_id:634766), $n = a^2+b^2$, if and only if $n$ is the norm of some Gaussian integer $a+bi$. This single observation transforms the Diophantine equation in $\mathbb{Z}$ into a question about norms in $\mathbb{Z}[i]$.

The norm has a fundamental multiplicative property: for any two Gaussian integers $\alpha$ and $\beta$, we have $N(\alpha\beta) = N(\alpha)N(\beta)$. This can be seen by letting $\alpha = a+bi$ and $\beta = c+di$. Their product is $\alpha\beta = (ac-bd) + i(ad+bc)$. The norm of this product is:

$N(\alpha\beta) = (ac-bd)^2 + (ad+bc)^2$

Expanding this and rearranging shows it is equal to $(a^2+b^2)(c^2+d^2) = N(\alpha)N(\beta)$. This identity, known as the **Brahmagupta-Fibonacci identity**, demonstrates that the set of integers that can be written as a [sum of two squares](@entry_id:634766) is closed under multiplication [@problem_id:3089709]. If $m$ and $n$ are [sums of two squares](@entry_id:154791), they are norms of some Gaussian integers, say $m=N(\alpha)$ and $n=N(\beta)$. Their product $mn$ is then the norm of $\alpha\beta$, and is therefore also a [sum of two squares](@entry_id:634766). This property suggests that the question can be broken down by studying the prime factors of an integer $n$.

### The Arithmetic of Gaussian Integers: Units, Associates, and Primes

To fully leverage the norm correspondence, we must understand the arithmetic structure of $\mathbb{Z}[i]$, particularly its concepts of [divisibility](@entry_id:190902) and [prime factorization](@entry_id:152058). Like the ordinary integers, $\mathbb{Z}[i]$ is a **Unique Factorization Domain (UFD)**. This means every non-zero, non-unit Gaussian integer can be factored into a product of Gaussian primes, and this factorization is unique up to the order of the primes and multiplication by units.

First, we must identify the **units** of $\mathbb{Z}[i]$. A unit is an element with a multiplicative inverse in the ring. An element $u=a+bi$ is a unit if and only if its norm is $1$. The equation $a^2+b^2=1$ has exactly four integer solutions for $(a,b)$: $(1,0), (-1,0), (0,1),$ and $(0,-1)$. These correspond to the four units: $\{1, -1, i, -i\}$.

Two Gaussian integers $\alpha$ and $\beta$ are called **associates** if one is a unit multiple of the other, i.e., $\alpha = u\beta$ for some unit $u$. Since there are four units, any non-zero Gaussian integer $\pi$ has exactly four distinct associates: $\pi, -\pi, i\pi,$ and $-i\pi$ [@problem_id:3090015]. These four associates all share the same norm, as $N(u\pi) = N(u)N(\pi) = 1 \cdot N(\pi) = N(\pi)$. This group of four units is the source of a factor of 4 that appears when counting representations [@problem_id:3090029].

A **Gaussian prime** is an irreducible element of $\mathbb{Z}[i]$: a non-unit $\pi$ that cannot be written as a product of two non-units. Since $\mathbb{Z}[i]$ is a UFD, the concepts of "prime" and "irreducible" are equivalent. This means that if a Gaussian prime $\pi$ divides a product $\alpha\beta$, then $\pi$ must divide $\alpha$ or $\pi$ must divide $\beta$. This property is the cornerstone of unique factorization and is essential to the proof of the main theorem [@problem_id:3090017].

### The Fate of Rational Primes in $\mathbb{Z}[i]$

The structure of Gaussian primes is revealed by examining how ordinary primes from $\mathbb{Z}$ (which we will call **rational primes**) behave when considered as elements of $\mathbb{Z}[i]$. A rational prime $p$ might remain prime in $\mathbb{Z}[i]$, or it might factor. There are three distinct possibilities, determined by the [congruence](@entry_id:194418) class of the prime modulo 4.

**1. The Ramified Prime: $p=2$**

The prime $2$ is special. In $\mathbb{Z}[i]$, we can factor it as $2 = (1+i)(1-i)$. The factors $1+i$ and $1-i$ have norm $N(1+i) = 1^2+1^2=2$ and $N(1-i) = 1^2+(-1)^2=2$. Since their norms are not $1$, they are not units. An element whose norm is a rational prime is necessarily a Gaussian prime. Furthermore, note that $1-i = -i(1+i)$, meaning $1+i$ and $1-i$ are associates. Thus, the factorization of $2$ is, up to a unit, the square of a single Gaussian prime: $2 = -i(1+i)^2$. A rational prime that is an associate of the square of a Gaussian prime is said to be **ramified**. This unique behavior for $2$ implies that any [power of 2](@entry_id:150972), $2^n$, is a [sum of two squares](@entry_id:634766), as it is the norm of $(1+i)^n$ [@problem_id:3090033].

**2. The Split Primes: $p \equiv 1 \pmod{4}$**

A rational prime $p$ such that $p \equiv 1 \pmod{4}$ is always a [sum of two squares](@entry_id:634766) in $\mathbb{Z}$ (a result we take for now, also provable with this machinery). This means there exist integers $a, b$ such that $p = a^2+b^2$. In $\mathbb{Z}[i]$, this translates directly to a factorization:

$p = (a+bi)(a-bi)$

Let $\pi = a+bi$. Then its conjugate is $\bar{\pi} = a-bi$. The factors $\pi$ and $\bar{\pi}$ are Gaussian primes because their norm is $N(\pi) = a^2+b^2=p$, a rational prime. Since $p \equiv 1 \pmod 4$ implies $p$ is odd, $a$ and $b$ cannot be equal, nor can one be zero, so $\pi$ is not an associate of $\bar{\pi}$. Such a prime is said to **split** in $\mathbb{Z}[i]$. For any $k \geq 1$, $p^k = N(\pi^k)$, meaning any power of a prime congruent to $1 \pmod 4$ is a [sum of two squares](@entry_id:634766) [@problem_id:3090030].

**3. The Inert Primes: $p \equiv 3 \pmod{4}$**

A rational prime $p$ such that $p \equiv 3 \pmod{4}$ cannot be written as a [sum of two squares](@entry_id:634766). (A simple proof: squares modulo 4 can only be 0 or 1, so a [sum of two squares](@entry_id:634766) can only be 0, 1, or 2 modulo 4, but never 3). This implies there is no Gaussian integer with norm $p$. If $p$ were to factor in $\mathbb{Z}[i]$ as $p=\alpha\beta$ with non-units $\alpha, \beta$, then taking norms gives $N(p) = p^2 = N(\alpha)N(\beta)$. Since $\alpha$ and $\beta$ are not units, their norms must be greater than 1, forcing $N(\alpha)=p$. This is a contradiction. Therefore, a rational prime $p \equiv 3 \pmod 4$ cannot be factored into non-units in $\mathbb{Z}[i]$. It remains irreducible, and is thus a Gaussian prime. Such a prime is said to be **inert**. The Gaussian primes that are also rational integers are precisely these [inert primes](@entry_id:196337) (and their negatives) [@problem_id:3090038] [@problem_id:3089682].

### The Sum of Two Squares Theorem

We now have all the tools to state and prove the full characterization of which positive integers are [sums of two squares](@entry_id:154791). This is often called **Fermat's Theorem on Sums of Two Squares**.

**Theorem:** A positive integer $n$ can be written as a [sum of two squares](@entry_id:634766) if and only if in the prime factorization of $n$, every prime factor of the form $4k+3$ appears with an even exponent. [@problem_id:3081207] [@problem_id:3090028]

**Proof:**

The proof consists of two parts: necessity and sufficiency.

(Necessity $\Rightarrow$) Suppose $n$ is a [sum of two squares](@entry_id:634766). Then $n=N(\alpha)$ for some $\alpha = a+bi \in \mathbb{Z}[i]$. Let $q$ be a rational prime such that $q \equiv 3 \pmod 4$ and $q$ divides $n$. From our classification, we know $q$ is also a prime in $\mathbb{Z}[i]$. Since $q$ divides $n=\alpha\bar{\alpha}$ and $\mathbb{Z}[i]$ is a UFD, $q$ must divide either $\alpha$ or its conjugate $\bar{\alpha}$. Suppose $q$ divides $\alpha$. Then $\alpha = q\beta$ for some $\beta \in \mathbb{Z}[i]$. Taking the conjugate, we get $\bar{\alpha} = \overline{q\beta} = \bar{q}\bar{\beta}$. Since $q$ is a real number, $\bar{q}=q$, so $\bar{\alpha} = q\bar{\beta}$. This means $q$ also divides $\bar{\alpha}$.
Now, consider the [prime factorization](@entry_id:152058) of $n$ in $\mathbb{Z}[i]$. The exponent of the Gaussian prime $q$ in the factorization of $n=\alpha\bar{\alpha}$ is the sum of its exponents in $\alpha$ and $\bar{\alpha}$. The argument above shows that if $q^k$ is the highest power of $q$ dividing $\alpha$, then $q^k$ is also the highest power of $q$ dividing $\bar{\alpha}$. Thus, the exponent of $q$ in the factorization of $n$ must be $k+k=2k$, which is an even number. This argument is critically dependent on the unique factorization property of $\mathbb{Z}[i]$ [@problem_id:3090017].

(Sufficiency $\Leftarrow$) Suppose the [prime factorization](@entry_id:152058) of $n$ in $\mathbb{Z}$ is $n = 2^k \prod p_i^{e_i} \prod q_j^{2f_j}$, where each $p_i \equiv 1 \pmod 4$ and each $q_j \equiv 3 \pmod 4$. We wish to show $n$ is a [sum of two squares](@entry_id:634766). We can do this by showing that each prime [power factor](@entry_id:270707) is the norm of some Gaussian integer.
-   $2 = N(1+i)$, so $2^k = N((1+i)^k)$.
-   Each $p_i \equiv 1 \pmod 4$ splits as $p_i = \pi_i\bar{\pi_i} = N(\pi_i)$. Thus, $p_i^{e_i} = N(\pi_i)^{e_i} = N(\pi_i^{e_i})$.
-   Each $q_j \equiv 3 \pmod 4$ is a Gaussian prime. Its norm is $N(q_j) = q_j^2$. Thus, $q_j^{2f_j} = (q_j^2)^{f_j} = N(q_j)^{f_j} = N(q_j^{f_j})$.
Since the norm is multiplicative, we can combine these:
$n = N((1+i)^k) \prod N(\pi_i^{e_i}) \prod N(q_j^{f_j}) = N\left( (1+i)^k \prod \pi_i^{e_i} \prod q_j^{f_j} \right)$
Since $n$ is the norm of a Gaussian integer, it must be a [sum of two squares](@entry_id:634766). This constructive approach can be used in practice. For instance, to find a representation for $130 = 2 \cdot 5 \cdot 13$, we find Gaussian integers whose norms are the prime factors: $N(1+i)=2$, $N(2+i)=5$, and $N(3+2i)=13$. Their product is $(1+i)(2+i)(3+2i) = -3+11i$. The norm is $N(-3+11i) = (-3)^2+11^2 = 9+121 = 130$. Thus, a representation for 130 is $3^2+11^2$ [@problem_id:3090018].

### Counting the Representations

We can go further and count the number of distinct representations. Let $r_2(n)$ be the number of [ordered pairs](@entry_id:269702) of integers $(x,y)$ such that $x^2+y^2=n$. This is equivalent to counting the number of Gaussian integers $\alpha = x+iy$ such that $N(\alpha)=n$.

Based on the proof of sufficiency, we found that an $\alpha$ with $N(\alpha)=n$ must be of the form:
$\alpha = U \cdot (1+i)^{v_2(n)} \cdot \prod_{q_l} q_l^{v_{q_l}(n)/2} \cdot \prod_{p_j} \pi_j^{c_j} \overline{\pi_j}^{v_{p_j}(n)-c_j}$
where $v_p(n)$ is the exponent of the prime $p$ in the factorization of $n$. For this to be possible, all exponents $v_{q_l}(n)$ must be even. If this condition is met, we can count the number of possible $\alpha$.

1.  There are 4 choices for the unit $U$.
2.  The exponents for the ramified prime ($1+i$) and [inert primes](@entry_id:196337) ($q_j$) are fixed.
3.  For each split prime $p_j$, we must choose the exponent $c_j$ for $\pi_j$. The exponent for $\overline{\pi_j}$ is then determined as $v_{p_j}(n) - c_j$. The exponent $c_j$ can be any integer from $0$ to $v_{p_j}(n)$, giving $v_{p_j}(n)+1$ choices for each $j$.

Since each combination of these choices gives a distinct $\alpha$ (by unique factorization), the total number of representations is:

$r_2(n) = 4 \prod_{p \equiv 1 \pmod 4} (v_p(n)+1)$

This formula holds if all exponents of primes $q \equiv 3 \pmod 4$ are even; otherwise, $r_2(n)=0$.

This result can be expressed more compactly using the non-trivial **Dirichlet character modulo 4**, denoted $\chi$. This function is defined as $\chi(m)=1$ if $m \equiv 1 \pmod 4$, $\chi(m)=-1$ if $m \equiv 3 \pmod 4$, and $\chi(m)=0$ if $m$ is even. A remarkable theorem, which can be proven by showing it holds for [prime powers](@entry_id:636094) and using multiplicativity, states:

$r_2(n) = 4 \sum_{d|n} \chi(d)$

where the sum is over all positive divisors $d$ of $n$. These two formulas provide a complete and beautiful answer to the problem of counting the ways an integer can be written as a [sum of two squares](@entry_id:634766) [@problem_id:3090048] [@problem_id:3089682].