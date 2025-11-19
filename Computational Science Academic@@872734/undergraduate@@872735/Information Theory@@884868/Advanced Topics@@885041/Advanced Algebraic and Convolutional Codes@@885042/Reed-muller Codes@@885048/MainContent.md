## Introduction
In the quest for [reliable communication](@entry_id:276141) over noisy channels, error-correcting codes are an indispensable tool. Among the earliest and most elegant families of such codes are the Reed-Muller (RM) codes. Valued for their deep algebraic structure and historical significance, RM codes bridge the gap between abstract algebra and practical engineering, providing a foundational framework for understanding how to encode and protect information. They address the fundamental problem of correcting errors introduced during transmission by adding structured redundancy to data.

This article provides a thorough exploration of Reed-Muller codes, structured to build understanding from the ground up. We will begin in "Principles and Mechanisms" by delving into the core of RM codes, uncovering their three primary constructions—via polynomials, recursion, and matrices—and deriving their fundamental parameters. Next, in "Applications and Interdisciplinary Connections," we will see how this rich structure enables their use in fields ranging from [deep-space communication](@entry_id:264623) and modern 5G standards to quantum error correction and [theoretical computer science](@entry_id:263133). Finally, the "Hands-On Practices" section will solidify these concepts through practical exercises in encoding, parameter calculation, and decoding, allowing you to apply the theory directly.

## Principles and Mechanisms

Following our introduction to the broad landscape of [error-correcting codes](@entry_id:153794), we now delve into the specific principles and mechanisms of one of the oldest and most structured families of codes: the Reed-Muller (RM) codes. These codes are not only of historical importance but also serve as a foundational topic, illustrating deep connections between algebra, [combinatorics](@entry_id:144343), and information theory. Their elegant constructions lend them to a variety of applications, from [deep-space communication](@entry_id:264623) to modern theoretical computer science.

In this chapter, we will explore the three primary ways to define and construct Reed-Muller codes: through Boolean polynomials, recursive concatenation, and matrix-based Kronecker products. Each perspective unveils unique properties of these codes, including their parameters, nested structure, and duality.

### The Polynomial Construction

The most intuitive construction of Reed-Muller codes is rooted in the algebra of multivariate polynomials over the binary field $\mathbb{F}_2 = \{0, 1\}$. An $r$-th order Reed-Muller code in $m$ variables, denoted $RM(r, m)$, is the set of all binary vectors of length $n = 2^m$ obtained by evaluating Boolean polynomials.

A **Boolean polynomial** in $m$ variables, $f(x_1, x_2, \ldots, x_m)$, is a polynomial where both the coefficients and the variables belong to $\mathbb{F}_2$. A key feature of arithmetic in $\mathbb{F}_2$ is that $x^2 = x$ for any variable $x$. Consequently, any Boolean polynomial can be uniquely written in a multilinear form, where each variable appears at most to the power of one. The **degree** of a monomial like $x_{i_1}x_{i_2}\cdots x_{i_k}$ is $k$, and the degree of the polynomial is the maximum degree of its monomials.

The code $RM(r, m)$ is formally defined as the set of all evaluation vectors of Boolean polynomials in $m$ variables with a degree of at most $r$. An **evaluation vector** is created by taking a specific polynomial and evaluating it at all $2^m$ possible input vectors in $\mathbb{F}_2^m$. To ensure consistency, the input vectors are ordered lexicographically, from $(0, 0, \ldots, 0)$ to $(1, 1, \ldots, 1)$.

For example, to construct a codeword in $RM(2, 3)$, one could choose a polynomial of degree at most 2, such as $f(x_1, x_2, x_3) = x_1 x_2$. Evaluating this polynomial at all 8 input vectors from $(0,0,0)$ to $(1,1,1)$ yields the codeword. The first six inputs result in $0$ since at least one of $x_1$ or $x_2$ is zero. Only for inputs $(1,1,0)$ and $(1,1,1)$ is the product $x_1x_2=1$. This produces the codeword $\begin{pmatrix} 0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 \end{pmatrix}$ [@problem_id:1653156]. Since the sum of two polynomials of degree at most $r$ is also a polynomial of degree at most $r$, the set of all such evaluation vectors forms a linear subspace of $\mathbb{F}_2^n$, making $RM(r, m)$ a [linear code](@entry_id:140077).

### Structure and Parameters

The polynomial definition provides a direct path to understanding the fundamental parameters of RM codes: length ($n$), dimension ($k$), and minimum distance ($d$).

#### Basis and Dimension

The set of all Boolean polynomials in $m$ variables of degree at most $r$ forms a vector space over $\mathbb{F}_2$. A natural basis for this space is the set of all monomials of degree at most $r$. The evaluation vectors corresponding to these basis monomials form a basis for the code $RM(r, m)$. The dimension of the code, $k$, is therefore equal to the number of such monomials.

The number of distinct monomials of a specific degree $i$ in $m$ variables is given by the [binomial coefficient](@entry_id:156066) $\binom{m}{i}$, as this corresponds to choosing which $i$ variables to include in the product. To find the total dimension of $RM(r, m)$, we sum the number of monomials for all degrees from 0 (the constant monomial '1') up to $r$.

This gives the fundamental formula for the dimension of an RM code:
$$ k = \sum_{i=0}^{r} \binom{m}{i} $$

To illustrate this, consider the first-order code $RM(1, 4)$. The degree is at most $r=1$. The basis monomials are the single monomial of degree 0 (the constant 1) and the $\binom{4}{1}=4$ monomials of degree 1 ($x_1, x_2, x_3, x_4$). The complete set of basis monomials is thus $\{1, x_1, x_2, x_3, x_4\}$, and the dimension is $k = \binom{4}{0} + \binom{4}{1} = 1 + 4 = 5$ [@problem_id:1653163].

This formula is a powerful tool for analyzing code properties. For instance, if we need to find the dimension of $RM(2, 4)$, we simply compute the sum:
$$ k = \sum_{i=0}^{2} \binom{4}{i} = \binom{4}{0} + \binom{4}{1} + \binom{4}{2} = 1 + 4 + 6 = 11 $$
Thus, $RM(2, 4)$ is an $[n=2^4, k=11, d]$ code, capable of encoding 11 bits of information [@problem_id:1653164].

Conversely, knowing the dimension allows us to determine the order of the code. Suppose a code is constructed using polynomials in $m=5$ variables and is known to have a dimension of $k=26$. By summing the [binomial coefficients](@entry_id:261706) for $m=5$, we find $\sum_{i=0}^0 \binom{5}{i} = 1$, $\sum_{i=0}^1 \binom{5}{i} = 1+5=6$, $\sum_{i=0}^2 \binom{5}{i} = 6+10=16$, and $\sum_{i=0}^3 \binom{5}{i} = 16+10=26$. This reveals that the code must be $RM(3, 5)$, using all polynomials of degree at most 3 [@problem_id:1653165].

#### Minimum Distance

While the polynomial construction makes the dimension transparent, the minimum distance is less obvious to derive. It is a classical result that the minimum Hamming distance of an $RM(r, m)$ code is given by:
$$ d = 2^{m-r} $$
This property is crucial for determining the error-correcting capability of the code. A larger distance implies a greater ability to correct errors. Notice the trade-off: for a fixed $m$, increasing the order $r$ increases the dimension $k$ (more information can be encoded) but decreases the minimum distance $d$ ([error correction](@entry_id:273762) capability is reduced).

#### Nested Structure and Duality

The polynomial construction immediately reveals a **nested structure**. Since the set of polynomials of degree at most $r$ is a subset of the polynomials of degree at most $s$ for any $r  s$, it follows that the corresponding codes are also nested:
$$ RM(r, m) \subset RM(s, m) \quad \text{for } r  s $$
This means that every codeword in $RM(r,m)$ is also a valid codeword in $RM(s,m)$. The codeword $\begin{pmatrix} 0  0  0  0  0  0  1  1 \end{pmatrix}$ from our earlier example is the evaluation of the degree-2 polynomial $x_1x_2$. It is therefore a member of $RM(2,3)$ but, as can be shown, cannot be generated by any polynomial of degree 1 or less, and thus is not in $RM(1,3)$ [@problem_id:1653156].

Another profound property of Reed-Muller codes is **duality**. The dual of a [linear code](@entry_id:140077) $C$, denoted $C^{\perp}$, is the set of all vectors orthogonal to every codeword in $C$. For Reed-Muller codes, the dual is another Reed-Muller code, according to the beautiful identity:
$$ RM(r, m)^{\perp} = RM(m-r-1, m) \quad \text{for } 0 \le r \le m $$
This relationship allows us to easily determine the parameters of a [dual code](@entry_id:145082). For example, let's find the parameters $[n,k,d]$ for the dual of $C = RM(1, 5)$. The parameters of $C$ are $n = 2^5=32$, $k = \binom{5}{0} + \binom{5}{1} = 6$, and $d = 2^{5-1}=16$. Its dual, $C^\perp$, is $RM(5-1-1, 5) = RM(3, 5)$. The parameters for $RM(3, 5)$ are $n=32$, $k = \binom{5}{0} + \binom{5}{1} + \binom{5}{2} + \binom{5}{3} = 1+5+10+10 = 26$, and $d = 2^{5-3}=4$. Thus, the [dual code](@entry_id:145082) has parameters $[32, 26, 4]$ [@problem_id:1653130].

### Recursive Construction Methods

While the polynomial construction is conceptually clear, alternative constructions offer different insights and are often more convenient for proofs and implementation.

#### The Plotkin Construction

Reed-Muller codes can be built recursively. This method, often called the Plotkin construction, builds $RM(r, m)$ from two smaller RM codes. A codeword $c \in RM(r, m)$ of length $2^m$ can be formed by concatenating two vectors of length $2^{m-1}$:
$$ c = (\mathbf{u} \mid \mathbf{u} + \mathbf{v}) $$
where all additions are component-wise modulo 2. This structure arises naturally from the polynomial definition. Any polynomial $f(x_1, \ldots, x_m)$ of degree at most $r$ can be decomposed with respect to the last variable, $x_m$:
$$ f(x_1, \ldots, x_m) = f_0(x_1, \ldots, x_{m-1}) + x_m \cdot f_1(x_1, \ldots, x_{m-1}) $$
Here, $f_0$ consists of all monomials in $f$ that do not contain $x_m$, and $f_1$ is the polynomial factor multiplying $x_m$. The degree of $f_0$ is at most $r$, while the degree of $f_1$ must be at most $r-1$.

If we order the evaluation points such that the first half have $x_m=0$ and the second half have $x_m=1$, the evaluation of $f$ splits neatly. For the first half ($x_m=0$), $f$ evaluates to $f_0$. For the second half ($x_m=1$), $f$ evaluates to $f_0 + f_1$.
Let $\mathbf{u}$ be the evaluation vector of $f_0$ and $\mathbf{v}$ be the evaluation vector of $f_1$. Since $\deg(f_0) \le r$ and $\deg(f_1) \le r-1$, $\mathbf{u}$ must be a codeword in $RM(r, m-1)$ and $\mathbf{v}$ must be a codeword in $RM(r-1, m-1)$. This gives us the fundamental recursive relationship:
$$ RM(r, m) = \{ (\mathbf{u} \mid \mathbf{u} + \mathbf{v}) \mid \mathbf{u} \in RM(r, m-1), \mathbf{v} \in RM(r-1, m-1) \} $$
This construction provides a powerful analytical tool [@problem_id:1653150]. For example, consider "axially symmetric" codewords, where the first half of the codeword is identical to the second half. In the recursive formulation, this means $(\mathbf{u} \mid \mathbf{u}) = (\mathbf{u} \mid \mathbf{u} + \mathbf{v})$, which implies $\mathbf{v} = \mathbf{0}$. The fraction of such symmetric codewords is the number of ways to choose $\mathbf{u}$ (which is $|RM(r,m-1)|$) divided by the total number of codewords, $|RM(r,m-1)| \cdot |RM(r-1,m-1)|$. The fraction simplifies to $1 / |RM(r-1,m-1)|$, a value that can be directly calculated from the dimension formula [@problem_id:1653114].

#### Kronecker Product Construction

A third, purely matrix-algebraic, construction uses the Kronecker product. The [generator matrix](@entry_id:275809) for $RM(r, m)$ can be constructed by selecting specific rows from the $m$-th Kronecker power of the matrix $H_1 = \begin{pmatrix} 1  1 \\ 1  0 \end{pmatrix}$. The full matrix $H_1^{\otimes m}$ is a $2^m \times 2^m$ matrix whose rows and columns can be indexed by binary vectors of length $m$.

The [generator matrix](@entry_id:275809) for $RM(r,m)$ is formed by selecting all rows of $H_1^{\otimes m}$ whose index vector $u \in \{0,1\}^m$ has a Hamming weight $w(u)$ no greater than $r$. The number of such rows is $\sum_{i=0}^r \binom{m}{i}$, which correctly matches the dimension $k$.

The structure of the rows of $H_1^{\otimes m}$ is particularly simple. The row indexed by a vector $u$ is a binary vector whose support (the set of positions with a '1') corresponds to the columns $v$ that satisfy $v_i = 0$ for all $i$ where $u_i = 1$. The size of this support is $2^{m-w(u)}$. A codeword is generated by summing a selection of these rows modulo 2. For example, if we create a codeword in $RM(2,4)$ by summing the rows corresponding to $u_A = (0101)$ and $u_B = (1010)$, the resulting codeword's weight is the size of the [symmetric difference](@entry_id:156264) of their supports. As $w(u_A) = w(u_B) = 2$, each row has weight $2^{4-2}=4$. Since their supports are nearly disjoint, the sum of the rows has a weight of $4+4 - 2 \cdot 1 = 6$ [@problem_id:1653125]. This construction is especially useful in contexts where matrix operations are natural, such as in signal processing and quantum computing.

### Key Properties and Asymptotic Behavior

#### Local Decodability of First-Order Codes

First-order Reed-Muller codes, $RM(1,m)$, possess a remarkable property related to decoding. A polynomial of degree at most 1 has the form $f(\mathbf{x}) = a_0 + a_1x_1 + \dots + a_m x_m$. There are $m+1$ coefficients to determine. These can be found by evaluating the polynomial at just $m+1$ specific points: the all-[zero vector](@entry_id:156189) $\mathbf{0}$ and the $m$ vectors of Hamming weight one (e.g., $(1,0,\dots,0)$, $(0,1,\dots,0)$, etc.).

- $f(\mathbf{0}) = a_0$
- $f(1,0,\dots,0) = a_0 + a_1$
- $f(0,1,\dots,0) = a_0 + a_2$
- ... and so on.

Knowing the codeword values at these $m+1$ positions allows one to solve for all the coefficients $(a_0, a_1, \dots, a_m)$ and thus reconstruct the entire generating polynomial. Once the polynomial is known, any bit of the codeword can be computed. For instance, given five specific values of a codeword in $RM(1,4)$, one can determine the coefficients $a_0, \ldots, a_4$ and then calculate the codeword value at any other point, such as $(1,1,1,1)$ [@problem_id:1653108]. This is a simple form of what is now known as **local decodability**.

#### Asymptotic Performance

Finally, it is instructive to consider the efficiency of RM codes as their block length grows infinitely large. The [code rate](@entry_id:176461), $R = k/n$, measures this efficiency. We consider two scenarios for the limit as $m \to \infty$.

1.  **Fixed Order $r$**: If $r$ is held constant, the dimension $k = \sum_{i=0}^r \binom{m}{i}$ is a polynomial in $m$ of degree $r$. The length $n=2^m$ grows exponentially. The rate $R = k/n$ is a ratio of a polynomial to an exponential function, which always tends to zero.
    $$ \lim_{m\to\infty} R(r, m) = 0 \quad (\text{for fixed } r) $$

2.  **Fixed Ratio $r/m = \rho$**: If the order grows proportionally to $m$, such that $r \approx \rho m$ for a constant $\rho \in (0,1)$, the behavior is governed by the Law of Large Numbers. The rate $R = (\sum_{i=0}^{\rho m} \binom{m}{i}) / 2^m$ corresponds to the [cumulative distribution function](@entry_id:143135) of a binomial distribution for $m$ fair coin flips. For large $m$, this distribution becomes sharply peaked around the mean of $m/2$ heads.
    - If $\rho  1/2$, we are summing the probabilities of outcomes far below the mean, which approaches 0.
    - If $\rho > 1/2$, we are summing over almost the entire probability mass, so the rate approaches 1.
    $$ \lim_{m\to\infty} R(\lfloor \rho m \rfloor, m) = \begin{cases} 0  \text{if } 0 \le \rho  1/2 \\ 1  \text{if } 1/2  \rho \le 1 \end{cases} $$
These results [@problem_id:1653112] show that, from the perspective of achieving a non-zero rate for a non-trivial [error correction](@entry_id:273762) capability, RM codes are not "good" codes in the sense of Shannon's theorem. However, their rich algebraic structure, multiple constructions, and properties like local decodability have made them indispensable tools and objects of study in [coding theory](@entry_id:141926) and beyond.