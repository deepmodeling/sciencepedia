## Introduction
From the static axioms that define a measure—non-negativity, the measure of the [empty set](@entry_id:261946), and [countable additivity](@entry_id:141665)—emerge powerful dynamic properties that govern how measures behave under limiting operations. Chief among these is the principle of [continuity of measure](@entry_id:159818), which provides a crucial bridge between finite, well-understood scenarios and the complexities of the infinite. It addresses a fundamental question: how does the measure of a [limit of a sequence](@entry_id:137523) of sets relate to the limit of their measures? This principle allows us to handle [infinite sets](@entry_id:137163) and processes by systematically approximating them with simpler, finite ones.

This article explores one of the two forms of this principle: [continuity from below](@entry_id:203239). Across the following chapters, you will gain a comprehensive understanding of this cornerstone of measure theory. The first chapter, **"Principles and Mechanisms,"** will formally introduce the theorem of [continuity from below](@entry_id:203239), walk through its elegant proof, and illustrate its mechanics with foundational examples. Next, **"Applications and Interdisciplinary Connections"** will showcase the theorem's far-reaching impact, demonstrating how it is used to calculate the area of fractals, provide the theoretical bedrock for modern probability, and prove fundamental results in analysis. Finally, **"Hands-On Practices"** will provide a set of guided problems to help you solidify your knowledge and apply the theory to concrete scenarios.

## Principles and Mechanisms

In our exploration of [measure theory](@entry_id:139744), we move from the foundational axioms of measures—non-negativity, the measure of the empty set, and [countable additivity](@entry_id:141665)—to their dynamic consequences. One of the most fundamental and powerful of these consequences is the principle of **[continuity of measure](@entry_id:159818)**. This principle describes how the measure of a [limit of a sequence](@entry_id:137523) of sets relates to the limit of their individual measures. It comes in two forms: [continuity from below](@entry_id:203239) for increasing sequences of sets, and continuity from above for decreasing sequences. This chapter will focus primarily on [continuity from below](@entry_id:203239), as it holds with greater generality and serves as a cornerstone for many key results in analysis and probability theory.

### The Core Principle: Continuity from Below

At its heart, the continuity of a measure provides a vital bridge between finite operations and infinite processes. It allows us to determine the measure of a potentially complex infinite set by examining a sequence of simpler, "approximating" sets.

Let us consider a [measure space](@entry_id:187562) $(X, \mathcal{M}, \mu)$. A sequence of measurable sets $\{A_n\}_{n=1}^{\infty}$ is called an **increasing sequence** if each set in the sequence is a subset of the next one, that is, $A_n \subseteq A_{n+1}$ for all $n \in \mathbb{N}$. The limit of such a sequence is their union, which we can denote as $A = \bigcup_{n=1}^{\infty} A_n$. The property of [continuity from below](@entry_id:203239) formally states the relationship between the measure of this limit set and the measures of the sets in the sequence.

**Theorem (Continuity of Measure from Below):** Let $(X, \mathcal{M}, \mu)$ be a [measure space](@entry_id:187562). If $\{A_n\}_{n=1}^{\infty}$ is an increasing sequence of measurable sets in $\mathcal{M}$, then the measure of their union is the limit of their measures:
$$
\mu\left(\bigcup_{n=1}^{\infty} A_n\right) = \lim_{n \to \infty} \mu(A_n)
$$

This theorem is a direct consequence of the axiom of [countable additivity](@entry_id:141665). To see the connection, we can cleverly rewrite the union of the increasing sets $A_n$ as a union of pairwise [disjoint sets](@entry_id:154341). Let $B_1 = A_1$, and for $n > 1$, define $B_n = A_n \setminus A_{n-1}$. Since the sequence $\{A_n\}$ is increasing, the sets $\{B_n\}_{n=1}^{\infty}$ are pairwise disjoint. Furthermore, the union of these disjoint "rings" is the same as the union of the original increasing sets: $\bigcup_{n=1}^{\infty} B_n = \bigcup_{n=1}^{\infty} A_n$.

By the [countable additivity](@entry_id:141665) of $\mu$, we have:
$$
\mu\left(\bigcup_{n=1}^{\infty} A_n\right) = \mu\left(\bigcup_{n=1}^{\infty} B_n\right) = \sum_{n=1}^{\infty} \mu(B_n)
$$
The right-hand side is, by definition, the limit of the partial sums:
$$
\sum_{n=1}^{\infty} \mu(B_n) = \lim_{N \to \infty} \sum_{n=1}^{N} \mu(B_n) = \lim_{N \to \infty} \mu\left(\bigcup_{n=1}^{N} B_n\right)
$$
But the finite union $\bigcup_{n=1}^{N} B_n$ is precisely the set $A_N$. Therefore, we arrive at the conclusion:
$$
\mu\left(\bigcup_{n=1}^{\infty} A_n\right) = \lim_{N \to \infty} \mu(A_N)
$$
This result is profound. It requires no assumption about the finiteness of the measure of any of the sets involved, making it a universally applicable tool.

### Foundational Illustrations

The principle of [continuity from below](@entry_id:203239) is most clearly understood through simple, illustrative examples that show how it allows us to handle [infinite sets](@entry_id:137163) by treating them as limits of finite ones.

A canonical example involves the counting measure. Consider the [measure space](@entry_id:187562) $(\mathbb{N}, \mathcal{P}(\mathbb{N}), \mu_c)$, where $\mu_c$ is the [counting measure](@entry_id:188748). To determine the measure of the entire set of natural numbers $\mathbb{N}$, we can express it as the limit of an increasing sequence of finite sets. Let $A_n = \{1, 2, \dots, n\}$ for each $n \in \mathbb{N}$ [@problem_id:1412429]. This is clearly an increasing sequence, as $A_n \subset A_{n+1}$, and their union is the entire set $\mathbb{N}$, i.e., $\bigcup_{n=1}^{\infty} A_n = \mathbb{N}$. The measure of each set $A_n$ is simply its [cardinality](@entry_id:137773), $\mu_c(A_n) = n$. Applying [continuity from below](@entry_id:203239), we find:
$$
\mu_c(\mathbb{N}) = \mu_c\left(\bigcup_{n=1}^{\infty} A_n\right) = \lim_{n \to \infty} \mu_c(A_n) = \lim_{n \to \infty} n = \infty
$$
This confirms the expected result that the counting measure of the infinite set $\mathbb{N}$ is infinity, but it does so by rigorously building up from [finite sets](@entry_id:145527).

This principle is equally powerful for sets of infinite measure in Euclidean space. Consider a physical model where a quantity is distributed over a region $E = \{(x,y) \in \mathbb{R}^2 : x \ge 1, 0 \le y \le 1/x\}$. The total amount is given by the Lebesgue measure of $E$, $m(E)$. We can approximate this unbounded set with a sequence of bounded, increasing subsets $E_n = E \cap ([1, n] \times \mathbb{R})$, which corresponds to the region where $1 \le x \le n$ [@problem_id:1412384]. The measure of each $E_n$ is given by an integral:
$$
m(E_n) = \int_1^n \frac{1}{x} \, dx = [\ln(x)]_1^n = \ln(n)
$$
The sequence $\{E_n\}$ is increasing and $\bigcup_{n=1}^{\infty} E_n = E$. By [continuity from below](@entry_id:203239):
$$
m(E) = \lim_{n \to \infty} m(E_n) = \lim_{n \to \infty} \ln(n) = \infty
$$
This not only demonstrates that the set $E$ has infinite measure, but it also reveals a deeper truth: for any [measurable set](@entry_id:263324) $F$ with $\mu(F) = \infty$, we can always find a sequence of subsets $F_n \subset F$ with [finite measure](@entry_id:204764) such that $\lim_{n \to \infty} \mu(F_n) = \infty$. This implies that for any arbitrarily large number $M$, we can find a bounded subset of $F$ whose measure exceeds $M$. For instance, in the example above, to find a subset with measure at least 4, we solve $\ln(n) \ge 4$, which gives $n \ge \exp(4) \approx 54.6$. The smallest integer is $n=55$.

### Applications in Geometric Measure Theory

Continuity from below is an indispensable tool for calculating the measures of geometric objects, especially open sets and unbounded regions, which are otherwise difficult to tackle directly.

A classic application is finding the measure of an open set by approximating it from within by compact sets. Consider the open unit disk in $\mathbb{R}^2$, $D = \{ (x,y) \in \mathbb{R}^2 : x^2 + y^2 \lt 1 \}$ [@problem_id:1412383]. While intuitively its area should be $\pi$, proving this from first principles using, for example, coverings by rectangles is complex. Instead, we can define an increasing sequence of closed disks $D_n$ that "fill up" the open disk $D$. Let $D_n$ be the [closed disk](@entry_id:148403) of radius $r_n = 1 - \frac{1}{n+1}$. The sequence of radii $\{r_n\}$ increases towards 1, so the sequence of disks $\{D_n\}$ is increasing, and their union is exactly the open disk $D$. Given that the Lebesgue measure of a disk of radius $r$ is $\pi r^2$, we have $m(D_n) = \pi(1 - \frac{1}{n+1})^2$. Applying [continuity from below](@entry_id:203239) yields the elegant result:
$$
m(D) = \lim_{n \to \infty} m(D_n) = \lim_{n \to \infty} \pi \left(1 - \frac{1}{n+1}\right)^2 = \pi(1)^2 = \pi
$$

This method also provides a rigorous measure-theoretic foundation for the concept of **[improper integrals](@entry_id:138794)** from calculus. Let's calculate the measure of the unbounded region $A$ under the curve $y=1/(1+x^2)$ for $x \ge 0$ [@problem_id:1412364]. We define an increasing sequence of [bounded sets](@entry_id:157754) $A_n = \{ (x, y) \in \mathbb{R}^2 \mid 0 \le x \le n \text{ and } 0 \le y \le \frac{1}{1+x^2} \}$. The union $\bigcup_{n=1}^{\infty} A_n$ is the entire region $A$. The Lebesgue measure $\lambda(A_n)$ is simply the [definite integral](@entry_id:142493):
$$
\lambda(A_n) = \int_0^n \frac{1}{1+x^2} \, dx = [\arctan(x)]_0^n = \arctan(n)
$$
Using [continuity from below](@entry_id:203239), the measure of the infinite region $A$ becomes the limit of these [definite integrals](@entry_id:147612):
$$
\lambda(A) = \lim_{n \to \infty} \lambda(A_n) = \lim_{n \to \infty} \arctan(n) = \frac{\pi}{2}
$$
This demonstrates that the value of the [improper integral](@entry_id:140191) $\int_0^\infty \frac{1}{1+x^2} dx$ is precisely the measure of the corresponding geometric region, a connection made rigorous by the [continuity of measure](@entry_id:159818).

Similarly, this principle can be applied to sets formed by an infinite process of additions. Consider the complement of the Cantor set within $[0,1]$, which is the union of all [open intervals](@entry_id:157577) removed during its construction [@problem_id:1412418]. Let $C_k$ be the union of the $2^{k-1}$ [open intervals](@entry_id:157577) of length $3^{-k}$ removed at stage $k$. Let $U_n = \bigcup_{k=1}^n C_k$ be the set of all intervals removed up to stage $n$. The sequence $\{U_n\}$ is an increasing sequence of open sets. The total removed set, $R$, is the union $\bigcup_{n=1}^\infty U_n$. By [continuity from below](@entry_id:203239):
$$
m(R) = \lim_{n \to \infty} m(U_n) = \lim_{n \to \infty} \sum_{k=1}^n m(C_k) = \sum_{k=1}^\infty 2^{k-1} 3^{-k} = 1
$$
Here, continuity provides the justification for equating the measure of the [infinite union](@entry_id:275660) with the value of the infinite series.

### Key Theoretical Consequences

Beyond concrete calculations, [continuity from below](@entry_id:203239) is the engine driving several deeper theoretical results in measure theory.

One such result concerns the measure of the **[limit inferior](@entry_id:145282)** of a [sequence of sets](@entry_id:184571). For any sequence of [measurable sets](@entry_id:159173) $\{E_k\}$, the [limit inferior](@entry_id:145282), denoted $\liminf E_k$, is the set of points that belong to all but a finite number of the $E_k$. It has the formal definition:
$$
\liminf_{k \to \infty} E_k = \bigcup_{n=1}^\infty \bigcap_{k=n}^\infty E_k
$$
To find its measure, we can define an auxiliary [sequence of sets](@entry_id:184571) $F_n = \bigcap_{k=n}^\infty E_k$ [@problem_id:1412403]. A key observation is that this sequence $\{F_n\}$ is increasing. Indeed, if a point $x$ is in $F_n$, it belongs to $E_k$ for all $k \ge n$. This implies it also belongs to $E_k$ for all $k \ge n+1$, and thus $x$ is in $F_{n+1}$. So, $F_n \subseteq F_{n+1}$. Since $\liminf E_k = \bigcup_{n=1}^\infty F_n$, we can directly apply [continuity from below](@entry_id:203239):
$$
\mu(\liminf_{k \to \infty} E_k) = \mu\left(\bigcup_{n=1}^\infty F_n\right) = \lim_{n \to \infty} \mu(F_n)
$$
This identity, often called Fatou's Lemma for sets, is a critical step in the proof of Fatou's Lemma for integrals and other convergence theorems.

Another profound consequence relates to the structure of [integrable functions](@entry_id:191199). A function $f$ is in $L^1(\mu)$ if $\int_X |f| \, d\mu  \infty$. What can we say about its **support**, the set $S = \{x \in X : f(x) \neq 0\}$? The measure of the support, $\mu(S)$, can be infinite. However, the support must have a special structure: it must be **$\sigma$-finite**. A set is $\sigma$-finite if it can be written as a countable union of sets of [finite measure](@entry_id:204764).

To prove this, we express the support $S$ as an increasing union of sets [@problem_id:1412422]. A point $x$ is in $S$ if and only if $|f(x)| > 0$, which is true if and only if there exists some positive integer $n$ such that $|f(x)| > 1/n$. This allows us to write:
$$
S = \bigcup_{n=1}^\infty E_n, \quad \text{where} \quad E_n = \{x \in X : |f(x)| > 1/n\}
$$
The sequence $\{E_n\}$ is increasing since if $|f(x)| > 1/n$, then for any $m > n$, $|f(x)| > 1/m$. The crucial step is to show that each set $E_n$ has [finite measure](@entry_id:204764). By Markov's inequality:
$$
\mu(E_n) = \mu(\{x : |f(x)| > 1/n\}) \le \frac{1}{1/n} \int_X |f| \, d\mu = n \int_X |f| \, d\mu
$$
Since $f$ is integrable, $\int_X |f| \, d\mu$ is a finite constant. Thus, $\mu(E_n)  \infty$ for every $n$. We have successfully expressed the support $S$ as a countable union of sets of [finite measure](@entry_id:204764). This demonstrates that any function in $L^1(\mu)$ must have a $\sigma$-finite support, a non-obvious fact that restricts where an integrable function can be "active."

In summary, the principle of [continuity from below](@entry_id:203239) is far more than a technical lemma. It is a dynamic tool that allows us to extend our reach from the finite to the infinite, providing both a practical method for calculating measures and a theoretical key to unlocking the deeper structure of [measure spaces](@entry_id:191702) and the functions defined upon them.