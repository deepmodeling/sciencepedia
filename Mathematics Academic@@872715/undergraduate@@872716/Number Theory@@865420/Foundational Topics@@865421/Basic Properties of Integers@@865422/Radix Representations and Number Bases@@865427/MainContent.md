## Introduction
The way we write numbers is a cornerstone of mathematics, yet the familiar base-ten system is just one of countless possibilities. Understanding how numbers can be represented in different bases, or radices, unlocks a deeper appreciation of number theory and is a prerequisite for tackling advanced problems in algorithm design, [cryptography](@entry_id:139166), and [scientific computing](@entry_id:143987). While we use decimal numbers daily, this system is not always the most efficient or insightful. The limitations of a single-base perspective create a knowledge gap that can hinder innovation and problem-solving in more technical domains.

This article provides a comprehensive exploration of [radix representation](@entry_id:636584), moving from foundational principles to abstract structures and practical applications. Across three chapters, you will gain a robust understanding of this fundamental concept. We will begin in "Principles and Mechanisms" by formalizing the positional system, analyzing its deep algebraic properties, and venturing into fascinating generalizations like negative bases and the powerful [p-adic numbers](@entry_id:145867). Following this theoretical groundwork, the "Applications and Interdisciplinary Connections" chapter will showcase how these concepts are leveraged in computer science, number theory, and even computational biology to create efficient algorithms and solve complex problems. Finally, "Hands-On Practices" will provide a chance to engage directly with the material through guided problems, solidifying your grasp of these essential mathematical tools.

## Principles and Mechanisms

The representation of numbers is a foundational concept in mathematics, providing the language for both theoretical inquiry and practical computation. While the base-ten system is ubiquitous in daily life, a deeper understanding of number theory and its applications requires a more general perspective. This chapter delves into the principles and mechanisms of **[radix representation](@entry_id:636584)**, exploring how integers and real numbers can be expressed in various bases. We will formalize the standard positional system, analyze its algebraic structure, and venture into more abstract generalizations, including negative bases, non-integer bases, and the fascinating world of $p$-adic numbers.

### The Standard Positional System for Integers

The ability to represent any non-negative integer using a small, [finite set](@entry_id:152247) of symbols is a cornerstone of modern arithmetic. This is achieved through a **[positional numeral system](@entry_id:753607)**, where the value of a digit depends on its position within a string. In a system with an integer base (or **[radix](@entry_id:754020)**) $b \ge 2$, we use a set of digits $D = \{0, 1, \dots, b-1\}$.

The theoretical underpinning for this system is the **Division Algorithm**, which states that for any integer $N \ge 0$ and a positive integer $b$, there exist unique integers $q$ (the quotient) and $r$ (the remainder) such that $N = qb + r$ and $0 \le r  b$. The remainder $r$ provides the least significant digit of $N$ in base $b$. By repeatedly applying this algorithm to the successive quotients, we can generate all the digits of the number.

For instance, let $N_0 = N$. We have:
$N_0 = q_0 b + d_0$
$q_0 = q_1 b + d_1$
$q_1 = q_2 b + d_2$
...and so on, until we reach a quotient $q_k = 0$. Since the sequence of non-negative quotients is strictly decreasing, this process is guaranteed to terminate. By substituting back, we see that $N = d_k b^k + \dots + d_1 b^1 + d_0 b^0$. This is the **base-$b$ expansion** of $N$, written as the digit string $(d_k d_{k-1} \dots d_0)_b$. The uniqueness of the quotient and remainder at each step guarantees that this representation is unique.

To illustrate, consider the task of representing the integer $N=987{,}654{,}321{,}098$ in the unusual base $b=999$ [@problem_id:3089133].
Applying the [division algorithm](@entry_id:156013):
1.  $987{,}654{,}321{,}098 = (988{,}642{,}964) \times 999 + 62$. So, $d_0 = 62$.
2.  $988{,}642{,}964 = (989{,}632) \times 999 + 596$. So, $d_1 = 596$.
3.  $989{,}632 = (990) \times 999 + 622$. So, $d_2 = 622$.
4.  $990 = (0) \times 999 + 990$. So, $d_3 = 990$.
The process terminates as the quotient is now $0$. The base-$999$ representation of $N$ is therefore $(990, 622, 596, 62)_{999}$.

This algorithm establishes the existence and uniqueness of a base-$b$ expansion for any non-negative integer. To formalize this, we can define a set of canonical representations $L_b$ as the set of all finite digit strings over $D$ that are either the single symbol '0' or do not begin with '0'. We can then define a **value map** $v: L_b \to \mathbb{N}$ by $v((d_k \dots d_0)_b) = \sum_{i=0}^k d_i b^i$. This map is a [bijection](@entry_id:138092), establishing a one-to-one correspondence between canonical digit strings and the non-negative integers [@problem_id:3089119].

This positional property is fundamentally different from that of **additive systems**, such as Roman numerals, where a symbol's value is largely independent of its position. In a pure additive system, the value of a string of symbols is simply the sum of the values of the individual symbols, making the order irrelevant [@problem_id:3089119]. In contrast, in a positional system, permuting digits dramatically changes the value: $(123)_{10} = 123$, but $(321)_{10} = 321$.

### The Algebraic Structure of Radix Notation

A powerful way to understand [positional notation](@entry_id:172992) is to view a number's base-$b$ representation as the evaluation of a polynomial. For an integer $N$ with base-$b$ digits $(d_k d_{k-1} \dots d_0)_b$, we can define its **digit-polynomial** as $P(x) = \sum_{i=0}^k d_i x^i$. The value of the integer is then simply $N = P(b)$ [@problem_id:3089109]. This perspective illuminates many properties of arithmetic.

A simple operation on digit strings is **[concatenation](@entry_id:137354)**. If we have two integers, $U$ with digit string length $m$ and $V$ with digit string length $n$, concatenating them does not correspond to addition. Instead, it corresponds to "shifting" $U$ to the left by $n$ places and adding $V$. Algebraically, the resulting value is $U \cdot b^n + V$ [@problem_id:3089109]. A special case of this is appending a single digit $d$ to a number represented by string $S$, which yields a new value of $b \cdot v(S) + d$ [@problem_id:3089119].

Multiplication provides a deeper example. The product of two integers $U = P_U(b)$ and $V = P_V(b)$ is, of course, $U \cdot V = P_U(b) \cdot P_V(b)$. This suggests that we can find the product by first multiplying their digit-polynomials, $P_{prod}(x) = P_U(x) \cdot P_V(x)$, and then evaluating at $x=b$. While this is correct, the coefficients of the resulting polynomial $P_{prod}(x)$ are not, in general, valid base-$b$ digits; they can be larger than $b-1$. To find the final base-$b$ digits of the product, one must perform **carry normalization**. Starting from the least significant coefficient (the constant term), we find its value modulo $b$ to get the final digit, and the integer quotient becomes a "carry" that is added to the next coefficient. This process is repeated for all coefficients [@problem_id:3089117]. This is, in fact, the precise mechanism underlying the familiar long multiplication algorithm taught in elementary school.

The polynomial viewpoint also provides elegant proofs for [divisibility](@entry_id:190902) rules. An integer $N = P(b)$ is divisible by an integer $m$ if and only if $N \equiv 0 \pmod{m}$. By using [modular arithmetic](@entry_id:143700) on the polynomial expression:

-   **Divisibility by $b-1$**: Since $b \equiv 1 \pmod{b-1}$, we have $N = P(b) \equiv P(1) \pmod{b-1}$. The value $P(1)$ is simply the sum of the coefficients of the polynomial, which are the digits of $N$. Thus, $N \equiv \sum d_i \pmod{b-1}$. An integer is divisible by $b-1$ if and only if the sum of its digits is divisible by $b-1$ [@problem_id:3089109]. For base 10, this is the familiar rule for divisibility by 9.

-   **Divisibility by $b+1$**: Since $b \equiv -1 \pmod{b+1}$, we have $N = P(b) \equiv P(-1) \pmod{b+1}$. The value $P(-1)$ is the alternating sum of the digits, $\sum (-1)^i d_i = d_0 - d_1 + d_2 - \dots$. Therefore, an integer is divisible by $b+1$ if and only if the alternating sum of its digits is divisible by $b+1$ [@problem_id:3089123] [@problem_id:3089109]. For base 10, this is the rule for [divisibility](@entry_id:190902) by 11.

Another interesting algebraic property relates to reversing the digits of a number. If $N$ has the digit polynomial $P(x) = \sum_{i=0}^k d_i x^i$, the number $N^{\text{rev}}$ with reversed digits $(d_0 d_1 \dots d_k)_b$ has the value $\sum_{i=0}^k d_i b^{k-i}$. This can be elegantly expressed using the polynomial as $N^{\text{rev}} = b^k P(b^{-1})$ [@problem_id:3089109].

### Fractional and Real Numbers

The positional system naturally extends to numbers that are not integers by introducing negative powers of the base. A real number $x \in [0, 1)$ can be represented by an infinite series $x = \sum_{n=1}^\infty d_n b^{-n}$, written as $0.d_1 d_2 d_3 \dots_b$.

A fundamental result connects rationality to the pattern of digits: a number $x$ is rational if and only if its base-$b$ expansion is **eventually periodic**. This means the sequence of digits eventually consists of a repeating block. For example, in base 13 (with digits $0, \dots, 9, \text{A}, \text{B}, \text{C}$), a number like $x = 0.\overline{\text{A}7\text{C}}_{13}$ is rational [@problem_id:3089137].

We can convert such a repeating fraction to a rational number $p/q$ by recognizing it as a [geometric series](@entry_id:158490). For $x = 0.\overline{d_1 \dots d_k}_b$, we can form a linear equation. Multiplying by $b^k$ shifts the decimal point by $k$ places:
$b^k x = (d_1 \dots d_k)_b + 0.\overline{d_1 \dots d_k}_b = N_{block} + x$
where $N_{block}$ is the integer value of the repeating block. Solving for $x$ gives $x = \frac{N_{block}}{b^k - 1}$. For instance, $x=0.\overline{\text{A}7\text{C}}_{13}$ becomes $x = \frac{(\text{A}7\text{C})_{13}}{13^3-1} = \frac{1793}{2196}$ [@problem_id:3089137].

Conversely, to find the base-$b$ expansion of a rational number $p/q$ (where $\gcd(b,q)=1$), we can use a similar algebraic setup to find the integer value of its repeating block, $N_{block} = (b^k-1) \frac{p}{q}$, where $k$ is the length of the period. This length $k$ is precisely the **[multiplicative order](@entry_id:636522)** of $b$ modulo $q$; that is, the smallest positive integer $k$ such that $b^k \equiv 1 \pmod q$ [@problem_id:3089137].

For any infinite expansion, we can approximate its value by a **truncation**, or partial sum. For $x = \sum_{n=1}^\infty d_n b^{-n}$, the $N$-th truncation is $x_N = \sum_{n=1}^N d_n b^{-n}$. The **[truncation error](@entry_id:140949)** $R_N = x - x_N$ is the tail of the series. Using the fact that digits are bounded ($d_n \le b-1$), we can bound the error by a geometric series:
$|R_N| = |\sum_{n=N+1}^\infty d_n b^{-n}| \le \sum_{n=N+1}^\infty (b-1)b^{-n} = b^{-N}$
This error bound is crucial for [numerical analysis](@entry_id:142637), as it tells us how many digits are needed to achieve a desired level of accuracy [@problem_id:3089130] [@problem_id:3089111].

### Generalizations and Alternative Representations

The standard base-$b$ system can be generalized in several fascinating ways, leading to numeration systems with unique properties.

#### Negabase: Using a Negative Radix

Instead of a positive base $b$, we can use a [negative base](@entry_id:634916) $-b$, where $b \ge 2$. Any integer (positive or negative) has a unique representation of the form $N = \sum_{i=0}^k d_i (-b)^i$, where the digits $d_i$ are still in the standard set $\{0, 1, \dots, b-1\}$. A remarkable feature of **negabase** systems is that they can represent all integers without needing a separate minus sign. For example, in base $-10$, the number $-9$ is represented as $(19)_{-10}$, since $1 \cdot (-10)^1 + 9 \cdot (-10)^0 = -10 + 9 = -1$.

The algebraic properties and [divisibility](@entry_id:190902) rules change in interesting ways. To test for [divisibility](@entry_id:190902), we again inspect the expansion $N=\sum d_i(-b)^i$ modulo some integer.
-   **Divisibility by $b+1$**: Modulo $b+1$, we have $-b \equiv 1$. Therefore, $N \equiv \sum d_i (-b)^i \equiv \sum d_i (1)^i = \sum d_i \pmod{b+1}$. In negabase, [divisibility](@entry_id:190902) by $b+1$ is tested by the **simple sum of digits** [@problem_id:3089123].
-   **Divisibility by $b-1$**: Modulo $b-1$, we have $-b \equiv -1$. Therefore, $N \equiv \sum d_i (-b)^i \equiv \sum d_i (-1)^i \pmod{b-1}$. Divisibility by $b-1$ is tested by the **alternating sum of digits** [@problem_id:3089123].
These rules are the reverse of those for a positive base $b$.

#### Non-Integer Bases: β-expansions

It is also possible to represent numbers using a non-integer base $\beta  1$. For any real number $x \in [0, 1)$, a **$\beta$-expansion** is a representation $x = \sum_{n=1}^\infty d_n \beta^{-n}$, where the digits are integers satisfying $0 \le d_n \le \lfloor \beta \rfloor$. The standard way to generate these digits is via the **greedy algorithm**. We define a sequence of remainders starting with $r_0=x$. For each step $n \ge 1$, we choose the largest possible digit and find the next remainder:
$d_n = \lfloor \beta r_{n-1} \rfloor$
$r_n = \beta r_{n-1} - d_n$
This iterative process generates a sequence of digits $(d_n)$ that represents $x$. A key property is that if we start with $r_0 \in [0, 1)$, this choice guarantees that all subsequent remainders $r_n$ also lie in $[0, 1)$, ensuring the process can continue indefinitely [@problem_id:3089121]. For example, for $\beta = 3/2$ and $x=9/10$, the greedy algorithm yields the digit sequence $(1, 0, 0, \dots)$ [@problem_id:3089121]. Unlike integer bases, $\beta$-expansions for rational numbers are not necessarily periodic.

#### Number-Theoretic Bases: Ostrowski Numeration

Radix representation can be generalized even further by abandoning a constant base altogether. **Ostrowski numeration** is a system tied to the [continued fraction expansion](@entry_id:636208) of an irrational number $\alpha = [0; a_1, a_2, \dots]$. Instead of powers of a base, the place values are the denominators $q_k$ of the convergents of $\alpha$, which are generated by the recurrence $q_{k+1} = a_{k+1}q_k + q_{k-1}$.
The fundamental theorem of Ostrowski numeration states that every non-negative integer $n$ has a unique representation as a finite sum $n = \sum_{k=0}^m b_{k+1} q_k$. The uniqueness is guaranteed by a specific set of rules for the digits $b_{k+1}$:
1.  $0 \le b_1  a_1$.
2.  $0 \le b_{k+1} \le a_{k+1}$ for $k \ge 1$.
3.  **Adjacency Constraint**: If a digit reaches its maximum value, $b_{k+1} = a_{k+1}$ for some $k \ge 1$, then the preceding digit must be zero, i.e., $b_k = 0$.
This structure ensures that no two representations are equivalent, which would otherwise be possible via the [recurrence relation](@entry_id:141039) itself [@problem_id:3089129]. Zeckendorf's theorem, which represents integers as sums of non-consecutive Fibonacci numbers, is a special case of Ostrowski numeration for the golden ratio $\phi$.

### A Different Metric: p-adic Expansions

Our familiar concept of "closeness" is based on the real absolute value. However, in number theory, it is often fruitful to define closeness differently. The **$p$-adic** number systems, for a prime $p$, are built on such a different notion.

A number is considered "$p$-adically small" if it is divisible by a high power of $p$. This is formalized by the **$p$-adic valuation** $v_p(n)$, the exponent of $p$ in the [prime factorization](@entry_id:152058) of an integer $n$. This extends to rationals via $v_p(a/b) = v_p(a) - v_p(b)$. The **$p$-adic norm** is then defined as $|x|_p = p^{-v_p(x)}$ for $x \neq 0$, and $|0|_p=0$ [@problem_id:3089115]. For example, $|9|_3 = 3^{-2} = 1/9$, while $|10|_3 = 3^0 = 1$. The number 9 is smaller than 10 in the 3-adic norm.

This norm leads to a different form of series expansion. A **$p$-adic integer** is a number that can be written as a series $y = \sum_{n=0}^\infty c_n p^n$ with digits $c_n \in \{0, \dots, p-1\}$. In stark contrast to real numbers, this series involves non-negative powers of $p$. The series converges because the $p$-adic norm of the terms, $|c_n p^n|_p \le p^{-n}$, tends to zero as $n \to \infty$ [@problem_id:3089111]. Remarkably, in a non-Archimedean space like the $p$-adic numbers, this condition is sufficient for convergence.

This structure allows us to find series representations for all ordinary integers and many rational numbers. Using the formula for a [geometric series](@entry_id:158490), which holds in the $p$-adic norm as long as the ratio $r$ satisfies $|r|_p  1$, we can find surprising expansions [@problem_id:3089115]:
-   $-1 = \frac{p-1}{1-p} = \sum_{n=0}^\infty (p-1)p^n = (p-1)(p-1)(p-1)\dots_p$.
-   $\frac{1}{1-p} = \sum_{n=0}^\infty p^n = 111\dots_p$.
-   In the 3-adic numbers, $\frac{1}{2} = \frac{-1}{1-3} = \sum_{n=0}^\infty (-1) \cdot 3^n$. This is not a standard expansion, but we can find one. A valid expansion is $\frac{1}{2} = 2 + 1 \cdot 3 + 1 \cdot 3^2 + \dots$, as its sum is $2 + \frac{3}{1-3} = 2 - \frac{3}{2} = \frac{1}{2}$ [@problem_id:3089115].

The difference between real and $p$-adic expansions is profound and is rooted in the **[triangle inequality](@entry_id:143750)**. The real norm satisfies $|u+v| \le |u|+|v|$, while the $p$-adic norm satisfies the stronger **[ultrametric inequality](@entry_id:146277)**: $|u+v|_p \le \max(|u|_p, |v|_p)$. A direct consequence is that if $|u|_p  |v|_p$, then $|u+v|_p = |u|_p$. This means the norm of a sum is determined by the norm of its largest term. This leads to a key difference in truncation error:
-   **Real error**: $|x - s_N| = |\sum_{n=N+1}^\infty a_n b^{-n}|$. The sum of many small terms can be significant. The error is only bounded: $|x - s_N| \le b^{-N}$.
-   **$p$-adic error**: $|y - t_N|_p = |\sum_{n=N+1}^\infty c_n p^n|_p$. Because the norms of the terms $p^{-(N+1)}, p^{-(N+2)}, \dots$ are strictly decreasing, the norm of the sum is exactly the norm of the first term. If $c_{N+1} \neq 0$, then $|y - t_N|_p = |c_{N+1}p^{N+1}|_p = p^{-(N+1)}$ [@problem_id:3089111].

### Statistical Properties of Digit Sequences: Normality

Beyond representing individual numbers, we can analyze the statistical properties of their digit sequences. A number $x$ is said to be **normal in base $b$** if its base-$b$ expansion is, in a sense, statistically random: for every positive integer $k$, every possible block of $k$ digits appears with a limiting frequency of $b^{-k}$ [@problem_id:3089127]. For example, in a base-10 normal number, the digit '7' appears $1/10$ of the time, the block '25' appears $1/100$ of the time, and '314' appears $1/1000$ of the time.

This property of a number's internal structure is deeply connected to its external behavior under iteration. Consider the sequence generated by repeatedly multiplying $x$ by the base $b$ and taking the [fractional part](@entry_id:275031): $(\{b^n x\})_{n \ge 0}$. The base-$b$ expansion of $\{b^n x\}$ is simply the expansion of $x$ with the first $n$ digits removed. A foundational theorem states that **a number $x$ is normal in base $b$ if and only if the sequence $(\{b^n x\})_{n \ge 0}$ is equidistributed in the interval $[0,1)$** [@problem_id:3089127]. Equidistribution means that the sequence "visits" every subinterval of $[0,1)$ with a limiting frequency equal to the length of that subinterval. Normality is the manifestation of this uniform distribution at the level of digit blocks.

The theory of [normal numbers](@entry_id:141052) is filled with profound results and equally profound open questions. It is known that rational numbers cannot be normal, as their digit sequences are periodic. It has also been proven that, in the sense of Lebesgue measure, "almost all" real numbers are normal in every integer base. However, proving normality for any specific, naturally occurring irrational number like $\pi$, $e$, or $\sqrt{2}$ remains an unsolved problem in mathematics. Mere irrationality is not enough to guarantee normality; there exist [irrational numbers](@entry_id:158320), like the Liouville number $\sum_{j=1}^\infty 10^{-j!}$, which are demonstrably not normal [@problem_id:3089127]. These questions highlight the deep and often mysterious relationship between the representation of a number and its intrinsic properties.