## Introduction
The Riemann zeta function, defined by the simple [infinite series](@entry_id:143366) $\zeta(s) = \sum(1/n^s)$, stands as a cornerstone of number theory and analysis, holding profound secrets about the [distribution of prime numbers](@entry_id:637447). A fascinating dichotomy exists within its study: while the values of the function at positive odd integers (like $\zeta(3)$) are shrouded in mystery, its values at positive even integers (like $\zeta(2)$) were conquered by Leonhard Euler in the 18th century. This article demystifies the case of even integers, revealing how these sums, against all intuition, are elegantly related to the number $\pi$.

This exploration will guide you through the elegant world of zeta values at even integers. The journey unfolds across the following chapters, each building upon the last:
*   **Principles and Mechanisms** will introduce Euler's seminal formula, explore the famous Basel problem ($\zeta(2)$), and present multiple elegant derivations for the general case, $\zeta(2k)$, revealing the deep connection to Bernoulli numbers.
*   **Applications and Interdisciplinary Connections** will demonstrate the surprising ubiquity of these values, showing how they appear as fundamental constants in physics, probability theory, and the study of [lattices](@entry_id:265277) and [modular forms](@entry_id:160014).
*   **Hands-On Practices** will provide you with opportunities to apply these concepts, solidifying your understanding through targeted problem-solving.

We begin by delving into the foundational principles and mechanisms that govern these remarkable numbers.

## Principles and Mechanisms

Following our introduction to the Riemann zeta function, we now delve into the principles and mechanisms that allow for the exact determination of its values at positive even integers. While the values at odd integers remain one of the most profound open problems in mathematics, the case for even integers, $s = 2k$ where $k$ is a positive integer, was resolved by Leonhard Euler in the 18th century. This chapter will explore the seminal formula he discovered, present several distinct and elegant derivations from different branches of mathematics, and touch upon the deep algebraic structures that these values exhibit.

### The Zeta Function at Even Integers: Euler's Formula

The central result concerning the values of the Riemann zeta function at positive even integers is **Euler's formula**. This remarkable equation establishes a direct connection between the zeta function, $\zeta(s) = \sum_{n=1}^{\infty} \frac{1}{n^s}$, and a sequence of rational numbers known as the **Bernoulli numbers**.

The **Bernoulli numbers**, denoted $B_m$, are defined by their [exponential generating function](@entry_id:270200):
$$
\frac{x}{\exp(x) - 1} = \sum_{m=0}^{\infty} B_m \frac{x^m}{m!}
$$
The first few Bernoulli numbers are $B_0 = 1$, $B_1 = -\frac{1}{2}$, $B_2 = \frac{1}{6}$, $B_3 = 0$, $B_4 = -\frac{1}{30}$, $B_5 = 0$, $B_6 = \frac{1}{42}$, and so on. A key property is that for all odd integers $m \ge 3$, $B_m = 0$.

Euler's formula states that for any positive integer $k$, the value of $\zeta(2k)$ is given by:
$$
\zeta(2k) = (-1)^{k+1} \frac{(2\pi)^{2k} B_{2k}}{2(2k)!}
$$
This equation reveals a profound truth: the sum of the inverse even powers of all positive integers is not a random [transcendental number](@entry_id:155894) but is always a rational multiple of $\pi^{2k}$. The remainder of this chapter is dedicated to understanding how this formula arises and exploring its consequences.

### A Foundational Case Study: The Basel Problem and $\zeta(2)$

The first and most famous result of this type was the solution to the **Basel problem**, which asked for the exact value of the sum $\sum_{n=1}^{\infty} \frac{1}{n^2}$. Euler's solution, $\zeta(2) = \frac{\pi^2}{6}$, brought him great fame. We will explore two of the many known proofs, each highlighting a different powerful mathematical technique.

#### The Sine Product Formula

One of Euler's most brilliant insights was to treat an [infinite series](@entry_id:143366) as an infinite polynomial and relate its roots to its coefficients. Consider the function $f(z) = \frac{\sin(\pi z)}{\pi z}$. The roots of $\sin(\pi z)$ occur at all integers $z=n$. The root at $z=0$ is removed by the division by $\pi z$, so the roots of $f(z)$ are at $z = \pm 1, \pm 2, \pm 3, \dots$.

Drawing an analogy with a finite polynomial $P(z)$ with roots $r_1, \dots, r_N$, which can be written as $P(z) = C \prod (1 - z/r_i)$, the Weierstrass [factorization theorem](@entry_id:749213) provides a rigorous foundation for writing $f(z)$ as an infinite product over its roots:
$$
\frac{\sin(\pi z)}{\pi z} = \prod_{n=1}^{\infty} \left(1 - \frac{z}{n}\right)\left(1 + \frac{z}{n}\right) = \prod_{n=1}^{\infty} \left(1 - \frac{z^2}{n^2}\right)
$$
This gives us one representation of our function. Another representation is its Maclaurin series, obtained from the well-known series for $\sin(x)$:
$$
\sin(\pi z) = (\pi z) - \frac{(\pi z)^3}{3!} + \frac{(\pi z)^5}{5!} - \dots
$$
Dividing by $\pi z$ gives:
$$
\frac{\sin(\pi z)}{\pi z} = 1 - \frac{\pi^2 z^2}{6} + \frac{\pi^4 z^4}{120} - \dots
$$
We now have two valid expressions for the same function. If we expand the infinite product just to the term with $z^2$, we must select the $-z^2/n^2$ term from one factor in the product and the $1$ from all other factors, and sum these possibilities over all $n$:
$$
\prod_{n=1}^{\infty} \left(1 - \frac{z^2}{n^2}\right) = \left(1 - \frac{z^2}{1^2}\right)\left(1 - \frac{z^2}{2^2}\right)\left(1 - \frac{z^2}{3^2}\right)\dots = 1 - \left(\frac{1}{1^2} + \frac{1}{2^2} + \frac{1}{3^2} + \dots\right)z^2 + O(z^4)
$$
By equating the coefficients of the $z^2$ term from the Maclaurin series and the [infinite product](@entry_id:173356) expansion, we arrive at a remarkable conclusion [@problem_id:794071]:
$$
-\frac{\pi^2}{6} = -\sum_{n=1}^{\infty} \frac{1}{n^2} \quad \Longrightarrow \quad \zeta(2) = \frac{\pi^2}{6}
$$

#### A Perspective from Fourier Analysis

An entirely different path to $\zeta(2)$ comes from the theory of Fourier series. Consider a simple periodic function, such as a [sawtooth wave](@entry_id:159756) defined on $(0, 2\pi)$ by $f(x) = \pi - x$, and extended periodically. The Fourier sine [series representation](@entry_id:175860) of this function is known to be:
$$
\pi - x = \sum_{n=1}^{\infty} \frac{2}{n} \sin(nx)
$$
While this series itself relates to sums of reciprocals, we can uncover a relationship for sums of squared reciprocals by integrating. Performing a [term-by-term integration](@entry_id:138696) from $0$ to $x$ is permissible and yields a new identity [@problem_id:794151]. The integral of the left side is:
$$
\int_0^x (\pi - t) dt = \left[\pi t - \frac{t^2}{2}\right]_0^x = \pi x - \frac{x^2}{2}
$$
Integrating the right side gives:
$$
\sum_{n=1}^{\infty} \int_0^x \frac{2}{n} \sin(nt) dt = \sum_{n=1}^{\infty} \frac{2}{n} \left[-\frac{\cos(nt)}{n}\right]_0^x = \sum_{n=1}^{\infty} \frac{2}{n^2}(1 - \cos(nx))
$$
Equating the integrated expressions gives us a Fourier series for the parabolic function on the left:
$$
\pi x - \frac{x^2}{2} = 2\zeta(2) - 2\sum_{n=1}^{\infty} \frac{\cos(nx)}{n^2}
$$
This identity holds for $x \in [0, 2\pi]$. The constant term of a Fourier series is equal to the mean value of the function over its period. The mean value of the right side is $2\zeta(2)$, as the average of each cosine term is zero. Therefore, we can find $\zeta(2)$ by calculating the mean value of the left side:
$$
2\zeta(2) = \frac{1}{2\pi} \int_0^{2\pi} \left(\pi x - \frac{x^2}{2}\right) dx = \frac{1}{2\pi} \left[\frac{\pi x^2}{2} - \frac{x^3}{6}\right]_0^{2\pi} = \frac{1}{2\pi}\left(2\pi^3 - \frac{8\pi^3}{6}\right) = \frac{\pi^2}{3}
$$
This gives $2\zeta(2) = \pi^2/3$, and thus $\zeta(2) = \pi^2/6$. This elegant method confirms Euler's result through the powerful machinery of [orthogonal functions](@entry_id:160936).

### The General Formula for $\zeta(2k)$

The methods for $\zeta(2)$ are beautiful but not easily generalizable. To find the values for all even integers, we must establish a more systematic connection, which is achieved by relating the cotangent function to both Bernoulli numbers and zeta values.

#### A Tale of Two Series

Consider the function $\pi z \coth(\pi z)$. The hyperbolic cotangent can be expressed using exponentials, which connects it to the generating function of the Bernoulli numbers:
$$
\pi z \coth(\pi z) = \pi z \frac{\exp(\pi z) + \exp(-\pi z)}{\exp(\pi z) - \exp(-\pi z)} = \pi z \frac{\exp(2\pi z) + 1}{\exp(2\pi z) - 1}
$$
A slight manipulation, by setting $x = 2\pi z$, reveals the connection:
$$
\pi z \coth(\pi z) = \frac{x}{2} \frac{\exp(x) + 1}{\exp(x) - 1} = \frac{x}{2} \left( \frac{\exp(x) - 1 + 2}{\exp(x) - 1} \right) = \frac{x}{2} \left(1 + \frac{2}{\exp(x) - 1}\right) = \frac{x}{2} + \frac{x}{\exp(x)-1}
$$
Using the [generating function](@entry_id:152704) for $B_m$ and the fact that $B_1 = -1/2$, this becomes:
$$
\pi z \coth(\pi z) = \sum_{m=0}^{\infty} B_m \frac{(2\pi z)^m}{m!} = 1 + \sum_{k=1}^{\infty} B_{2k} \frac{(2\pi z)^{2k}}{(2k)!}
$$
since all odd Bernoulli numbers $B_m$ for $m \ge 3$ are zero.

A second representation for this function comes from its Mittag-Leffler expansion, which expresses a [meromorphic function](@entry_id:195513) as a sum over its poles. Using the identity $\coth(z) = i \cot(iz)$ and the known expansion for $\pi\cot(\pi z)$, one can derive the expansion for $\pi z \coth(\pi z)$:
$$
\pi z \coth(\pi z) = 1 + 2z^2 \sum_{n=1}^{\infty} \frac{1}{z^2+n^2}
$$
For $|z|1$, we can expand the fraction in the sum as a geometric series:
$$
\frac{1}{z^2+n^2} = \frac{1}{n^2(1+z^2/n^2)} = \frac{1}{n^2} \sum_{j=0}^{\infty} (-1)^j \left(\frac{z^2}{n^2}\right)^j = \sum_{j=0}^{\infty} \frac{(-1)^{j} z^{2j}}{n^{2j+2}}
$$
Substituting this back into the expansion and swapping the order of summation gives:
$$
\pi z \coth(\pi z) = 1 + 2z^2 \sum_{n=1}^{\infty} \sum_{j=0}^{\infty} \frac{(-1)^{j} z^{2j}}{n^{2j+2}} = 1 + 2 \sum_{j=0}^{\infty} (-1)^{j} \left(\sum_{n=1}^{\infty} \frac{1}{n^{2j+2}}\right) z^{2j+2}
$$
Letting $k=j+1$, this simplifies to:
$$
\pi z \coth(\pi z) = 1 + 2 \sum_{k=1}^{\infty} (-1)^{k-1} \zeta(2k) z^{2k}
$$
By equating the coefficients of $z^{2k}$ in our two series expansions [@problem_id:794120], we obtain the celebrated formula:
$$
B_{2k} \frac{(2\pi)^{2k}}{(2k)!} = 2(-1)^{k-1} \zeta(2k)
$$
Rearranging for $\zeta(2k)$ gives us Euler's formula in its full glory.

#### Computing Higher-Order Values

With Euler's formula established, computing any $\zeta(2k)$ becomes a matter of finding the corresponding Bernoulli number. For example, to find $\zeta(8)$, we set $k=4$ in the formula [@problem_id:794027]:
$$
\zeta(8) = (-1)^{4+1} \frac{(2\pi)^8 B_8}{2(8!)} = -\frac{256 \pi^8 B_8}{2 \cdot 40320}
$$
Given the known value $B_8 = -\frac{1}{30}$, the calculation proceeds:
$$
\zeta(8) = -\frac{256 \pi^8}{80640} \left(-\frac{1}{30}\right) = \frac{256 \pi^8}{2419200}
$$
Reducing the fraction $\frac{256}{2419200}$ gives $\frac{1}{9450}$. Thus, we find the exact value:
$$
\zeta(8) = \frac{\pi^8}{9450}
$$

### Interdisciplinary Derivations of Zeta Values

The beauty of the [zeta function values](@entry_id:195573) is underscored by the variety of ways they can be derived, each offering a different conceptual viewpoint.

#### An L²-Norm Approach via Parseval's Theorem

Fourier analysis offers another powerful tool in the form of **Parseval's theorem**. For a function $g(x)$ on $[0,1]$ with Fourier coefficients $a_n$ and $b_n$, the theorem states:
$$
\int_0^1 |g(x)|^2 dx = \left(\frac{a_0}{2}\right)^2 + \frac{1}{2} \sum_{n=1}^{\infty} (a_n^2 + b_n^2)
$$
This theorem equates the total energy of a signal (the integral of its square) to the sum of the energies of its harmonic components. We can leverage this to calculate $\zeta(4)$. Consider the polynomial $P(x) = x^2 - x + \frac{1}{6}$, which is the second **Bernoulli polynomial**, $B_2(x)$. The Fourier series for this polynomial on $[0,1]$ is a pure cosine series:
$$
x^2 - x + \frac{1}{6} = \sum_{n=1}^{\infty} \frac{\cos(2\pi nx)}{2\pi^2 n^2}
$$
Here, the coefficients are $a_0=0$, $a_n = \frac{1}{\pi^2 n^2}$, and $b_n=0$ for $n \ge 1$. Applying Parseval's theorem to $P(x)$ [@problem_id:794175]:

The left-hand side is a direct integral of a polynomial:
$$
\int_0^1 \left(x^2 - x + \frac{1}{6}\right)^2 dx = \int_0^1 \left(x^4 - 2x^3 + \frac{4}{3}x^2 - \frac{1}{3}x + \frac{1}{36}\right) dx = \left[\frac{x^5}{5} - \frac{x^4}{2} + \frac{4x^3}{9} - \frac{x^2}{6} + \frac{x}{36}\right]_0^1 = \frac{1}{5} - \frac{1}{2} + \frac{4}{9} - \frac{1}{6} + \frac{1}{36} = \frac{1}{180}
$$
The right-hand side is a sum over the squared Fourier coefficients:
$$
\left(\frac{a_0}{2}\right)^2 + \frac{1}{2} \sum_{n=1}^{\infty} a_n^2 = 0 + \frac{1}{2} \sum_{n=1}^{\infty} \left(\frac{1}{\pi^2 n^2}\right)^2 = \frac{1}{2} \sum_{n=1}^{\infty} \frac{1}{\pi^4 n^4} = \frac{1}{2\pi^4} \sum_{n=1}^{\infty} \frac{1}{n^4} = \frac{\zeta(4)}{2\pi^4}
$$
Equating the two sides gives us the value of $\zeta(4)$:
$$
\frac{1}{180} = \frac{\zeta(4)}{2\pi^4} \quad \Longrightarrow \quad \zeta(4) = \frac{2\pi^4}{180} = \frac{\pi^4}{90}
$$

#### Zeta Values from Definite Integrals

A profound connection exists between the zeta function and a class of [definite integrals](@entry_id:147612) that appear frequently in physics, particularly in the theory of [black-body radiation](@entry_id:136552) and Bose-Einstein statistics. This link is forged by the **Gamma function**, $\Gamma(s) = \int_0^\infty t^{s-1} e^{-t} dt$. The key identity is:
$$
\Gamma(s)\zeta(s) = \int_0^{\infty} \frac{x^{s-1}}{\exp(x) - 1} dx
$$
This formula can be derived by expanding the denominator of the integrand as a geometric series, $\frac{1}{e^x-1} = \frac{e^{-x}}{1-e^{-x}} = \sum_{n=1}^\infty e^{-nx}$, and integrating term by term. This integral representation allows us to evaluate certain integrals if the corresponding zeta values are known. For instance, consider the integral [@problem_id:794033]:
$$
I = \int_0^\infty \frac{x^5}{\exp(x) - 1} dx
$$
From the identity, we recognize this corresponds to the case $s-1=5$, or $s=6$. Therefore, the value of the integral is $I = \Gamma(6)\zeta(6)$. Since $\Gamma(n)=(n-1)!$ for integer $n$, we have $\Gamma(6) = 5! = 120$. Using the known value $\zeta(6) = \frac{\pi^6}{945}$, we find:
$$
I = 120 \cdot \frac{\pi^6}{945} = \frac{8 \times 15}{63 \times 15} \pi^6 = \frac{8\pi^6}{63}
$$

Another powerful integration technique involves expanding an integrand into a series and swapping the order of summation and integration. For instance, $\zeta(2)$ can be derived from the integral $\int_0^1 \int_0^1 (1-xy)^{-1} dx dy$. A more advanced application of this method yields $\zeta(4)$ [@problem_id:794101]. Consider the double integral:
$$
I = \int_0^1 \int_0^1 \frac{\ln(x)\ln(y)}{1-xy} dx dy
$$
We expand the denominator as a [geometric series](@entry_id:158490) for $|xy|  1$:
$$
\frac{1}{1-xy} = \sum_{n=0}^\infty (xy)^n
$$
Swapping the integral and sum (justified by Fubini's theorem) gives:
$$
I = \sum_{n=0}^\infty \int_0^1 \int_0^1 x^n y^n \ln(x) \ln(y) dx dy = \sum_{n=0}^\infty \left(\int_0^1 x^n \ln(x) dx\right) \left(\int_0^1 y^n \ln(y) dy\right)
$$
The inner integral can be evaluated using integration by parts:
$$
\int_0^1 x^n \ln(x) dx = \left[\frac{x^{n+1}}{n+1}\ln(x)\right]_0^1 - \int_0^1 \frac{x^{n+1}}{n+1} \frac{1}{x} dx = 0 - \int_0^1 \frac{x^n}{n+1} dx = \left[-\frac{x^{n+1}}{(n+1)^2}\right]_0^1 = -\frac{1}{(n+1)^2}
$$
Substituting this result back into the expression for $I$:
$$
I = \sum_{n=0}^\infty \left(-\frac{1}{(n+1)^2}\right) \left(-\frac{1}{(n+1)^2}\right) = \sum_{n=0}^\infty \frac{1}{(n+1)^4} = \sum_{m=1}^\infty \frac{1}{m^4} = \zeta(4)
$$
Thus, the value of the integral is precisely $\zeta(4) = \frac{\pi^4}{90}$. This method beautifully transforms a problem in analysis into a direct summation for a zeta value.

### The Algebraic Structure of Zeta Values

The values $\zeta(2k)$ are not merely a sequence of numbers; they possess a deep and intricate algebraic structure. This structure manifests as various identities and relationships between them, often mediated by the Bernoulli numbers.

#### Relations Among Zeta Values

The Bernoulli numbers themselves satisfy convolution identities. One such identity for even-indexed Bernoulli numbers is, for $n \ge 2$:
$$
\sum_{k=1}^{n-1} \binom{2n}{2k} B_{2k} B_{2n-2k} = -(2n+1)B_{2n}
$$
Using Euler's formula to substitute for the Bernoulli numbers in terms of zeta values, one can derive complex relations purely between zeta values. This shows that not all $\zeta(2k)$ are algebraically independent. For instance, one can prove relationships like the one for the ratio $\frac{\zeta(2)\zeta(4)}{\zeta(6)} = \frac{7}{4}$ [@problem_id:794142] by applying such identities.

An even more profound structure emerges from the theory of **[modular forms](@entry_id:160014)**, a central topic in modern number theory. The values of $\zeta(2k)$ are directly related to the coefficients of **Eisenstein series**, which are a [fundamental class](@entry_id:158335) of [modular forms](@entry_id:160014). This connection gives rise to remarkable identities involving the **[divisor function](@entry_id:191434)**, $\sigma_k(n) = \sum_{d|n} d^k$. For example, the following convolution identity holds:
$$
\frac{20}{B_{10}} \sigma_9(n) = \frac{12}{B_6} \sigma_5(n) + \frac{8}{B_4} \sigma_3(n) - \frac{96}{B_4 B_6} \sum_{k=1}^{n-1} \sigma_3(k)\sigma_5(n-k)
$$
This seemingly arcane identity provides a powerful recursive tool. By setting $n=1$, the [convolution sum](@entry_id:263238) vanishes, and since $\sigma_k(1)=1$ for any $k$, we obtain a direct relation between Bernoulli numbers [@problem_id:794100]:
$$
\frac{20}{B_{10}} = \frac{12}{B_6} + \frac{8}{B_4}
$$
Given $B_4 = -1/30$ and $B_6 = 1/42$, we can solve for $B_{10}$:
$$
\frac{20}{B_{10}} = 12(42) + 8(-30) = 504 - 240 = 264 \quad \Longrightarrow \quad B_{10} = \frac{20}{264} = \frac{5}{66}
$$
From this, we can compute $\zeta(10)$ using Euler's formula:
$$
\zeta(10) = (-1)^{5+1} \frac{(2\pi)^{10} B_{10}}{2(10!)} = \frac{1024 \pi^{10}}{2 \cdot 3628800} \cdot \frac{5}{66} = \frac{\pi^{10}}{93555}
$$

#### An Introduction to Multiple Zeta Values

The study of zeta values extends to more complex objects known as **Multiple Zeta Values** (MZVs). For a set of positive integers $s_1, s_2, \dots, s_k$ with $s_1  1$, an MZV is defined as the nested sum:
$$
\zeta(s_1, s_2, \dots, s_k) = \sum_{n_1  n_2  \dots  n_k \ge 1} \frac{1}{n_1^{s_1} n_2^{s_2} \dots n_k^{s_k}}
$$
These objects possess a rich algebraic structure of their own. One of the fundamental relations they satisfy comes from considering the product of two single-variable zeta functions. The product of two series can be decomposed based on the relative order of their summation indices. For $p, q  1$, this leads to the identity:
$$
\zeta(p)\zeta(q) = \sum_{n=1}^\infty \frac{1}{n^p} \sum_{m=1}^\infty \frac{1}{m^q} = \sum_{nm\ge 1} \frac{1}{n^p m^q} + \sum_{mn\ge 1} \frac{1}{n^p m^q} + \sum_{n=m\ge 1} \frac{1}{n^p m^q}
$$
This translates directly into the MZV identity:
$$
\zeta(p)\zeta(q) = \zeta(p,q) + \zeta(q,p) + \zeta(p+q)
$$
This allows us to evaluate sums of certain MZVs. For example, to find the value of $\zeta(2,4) + \zeta(4,2)$, we can set $p=2$ and $q=4$ [@problem_id:794021]:
$$
\zeta(2,4) + \zeta(4,2) = \zeta(2)\zeta(4) - \zeta(6)
$$
Substituting the known values $\zeta(2)=\frac{\pi^2}{6}$, $\zeta(4)=\frac{\pi^4}{90}$, and $\zeta(6)=\frac{\pi^6}{945}$:
$$
\zeta(2,4) + \zeta(4,2) = \left(\frac{\pi^2}{6}\right)\left(\frac{\pi^4}{90}\right) - \frac{\pi^6}{945} = \frac{\pi^6}{540} - \frac{\pi^6}{945}
$$
Finding a common denominator of 3780, we get:
$$
\zeta(2,4) + \zeta(4,2) = \pi^6 \left(\frac{7 - 4}{3780}\right) = \frac{3\pi^6}{3780} = \frac{\pi^6}{1260}
$$
These examples illustrate that the seemingly simple values of $\zeta(2k)$ are gateways to a vast and interconnected world of number theory, analysis, and algebra, a world that continues to be an active and fruitful area of mathematical research.