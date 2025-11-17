## Introduction
Understanding the relationships between different function spaces is a central goal in analysis. A key question for the family of Lebesgue, or $L^p$, spaces is whether membership in one space implies membership in another. The answer, which depends critically on the underlying [measure space](@entry_id:187562), reveals a beautiful and rigid hierarchy under certain conditions. This article delves into the fundamental inclusion principle for $L^p$ spaces on [finite measure](@entry_id:204764) domains, a cornerstone of [functional analysis](@entry_id:146220).

## Principles and Mechanisms

In the study of [function spaces](@entry_id:143478), a primary objective is to understand their structure and the relationships between them. For the family of Lebesgue spaces, or $L^p$ spaces, a natural question arises: if a function belongs to one space, say $L^q(X)$, what can be said about its membership in another, $L^p(X)$? The answer, as we will see, depends critically on the properties of the underlying [measure space](@entry_id:187562) $(X, \mathcal{M}, \mu)$, and in particular, on whether the total measure $\mu(X)$ is finite. This chapter will establish the fundamental inclusion principle for $L^p$ spaces on [finite measure spaces](@entry_id:198109), explore the mechanism behind it, and examine its most important consequences.

### The Hierarchy of $L^p$ Spaces on a Finite Measure Domain

Let us begin by stating the central theorem. For a [measure space](@entry_id:187562) $(X, \mathcal{M}, \mu)$ with finite total measure, $\mu(X) < \infty$, the $L^p$ spaces are nested. Specifically, for any two exponents $p$ and $q$ such that $1 \le p < q \le \infty$, the following inclusion holds:

$L^q(X, \mu) \subseteq L^p(X, \mu)$

This relationship dictates that on a [finite measure space](@entry_id:142653), integrability with a higher exponent is a stronger condition, yielding a smaller space of functions. A function that is, for example, square-integrable (in $L^2$) is not guaranteed to be fourth-power-integrable (in $L^4$). Conversely, any function in $L^4$ must also be in $L^2$. This creates a clear hierarchy.

For instance, consider the interval $X = [0, \pi]$ with the standard Lebesgue measure. Since $\mu(X) = \pi$ is finite, the inclusion principle applies. If we examine the spaces $S_1 = L^1(X, \mu)$, $S_2 = L^2(X, \mu)$, $S_\pi = L^\pi(X, \mu)$, and $S_\infty = L^\infty(X, \mu)$, the exponents are ordered as $1 < 2 < \pi < \infty$. The inclusion theorem therefore implies a reversed nesting of the corresponding spaces [@problem_id:1421994]:

$S_\infty \subseteq S_\pi \subseteq S_2 \subseteq S_1$

This hierarchy is a cornerstone of [functional analysis](@entry_id:146220) on finite domains. Its proof, and the quantitative relationship it implies between the norms, reveals a deeper connection mediated by one of the most powerful tools in analysis.

### The Mechanism of Inclusion: Hölder's Inequality

The inclusion $L^q \subseteq L^p$ is not merely a set-theoretic curiosity; it is a direct consequence of a fundamental integral inequality. The mechanism that enforces this structure is **Hölder's inequality**. To see how, let us assume $f \in L^q(X, \mu)$ for $1 \le p < q < \infty$ and our goal is to show that $f \in L^p(X, \mu)$. This means we must demonstrate that the integral $\int_X |f|^p \,d\mu$ is finite.

The key insight is to express the integrand $|f|^p$ as a product of two functions and apply Hölder's inequality. We can write $|f(x)|^p = |f(x)|^p \cdot 1$. Hölder's inequality states that for [conjugate exponents](@entry_id:138847) $r, s > 1$ (i.e., $\frac{1}{r} + \frac{1}{s} = 1$), we have $\int |gh| \,d\mu \le \|g\|_r \|h\|_s$.

To relate the integral of $|f|^p$ to the known finite quantity $\|f\|_q$, we must choose our exponents cleverly. Let us apply Hölder's inequality to the functions $|f|^p$ and $1$. We choose an exponent $r$ such that integrating $(|f|^p)^r$ yields an expression related to the $L^q$-norm. Setting $p \cdot r = q$ achieves this, which gives $r = \frac{q}{p}$. Since $q > p$, we have $r > 1$, a valid choice. The [conjugate exponent](@entry_id:192675) $s$ is then determined by the relation $\frac{1}{s} = 1 - \frac{1}{r} = 1 - \frac{p}{q} = \frac{q-p}{q}$, which gives $s = \frac{q}{q-p}$.

Applying Hölder's inequality with these exponents yields:
$$
\int_X |f|^p \,d\mu = \int_X |f|^p \cdot 1 \,d\mu \le \left( \int_X (|f|^p)^r \,d\mu \right)^{1/r} \left( \int_X 1^s \,d\mu \right)^{1/s}
$$
Substituting $r=q/p$ and $s=q/(q-p)$:
$$
\int_X |f|^p \,d\mu \le \left( \int_X |f|^q \,d\mu \right)^{p/q} \left( \int_X 1 \,d\mu \right)^{(q-p)/q}
$$
The first term on the right is $(\|f\|_q^q)^{p/q} = \|f\|_q^p$. The second term is $(\mu(X))^{(q-p)/q}$. Thus, we have:
$$
\|f\|_p^p = \int_X |f|^p \,d\mu \le \|f\|_q^p \cdot (\mu(X))^{(q-p)/q}
$$
Since $f \in L^q(X, \mu)$, $\|f\|_q$ is finite. As $\mu(X)$ is also finite, the right-hand side is finite. This proves that $\|f\|_p$ must be finite, so $f \in L^p(X, \mu)$, establishing the inclusion $L^q \subseteq L^p$.

This derivation gives us more than just the inclusion; it provides a quantitative bound on the norms. Taking the $p$-th root of both sides gives the celebrated norm inequality [@problem_id:1422020]:
$$
\|f\|_p \le (\mu(X))^{\frac{1}{p} - \frac{1}{q}} \|f\|_q
$$
This inequality is sharp. Equality is achieved for any [constant function](@entry_id:152060) $f(x)=c$, demonstrating that the constant $C = (\mu(X))^{\frac{1}{p} - \frac{1}{q}}$ is the best possible [@problem_id:1422020].

As a concrete example, consider a space $(Y, \mathcal{A}, \nu)$ with total measure $\nu(Y) = 16$. If a function $g$ has an $L^2$-norm $\|g\|_2 = 10$, we can find the sharpest upper bound for its $L^1$-norm. Here, $p=1$ and $q=2$. The inequality becomes $\|g\|_1 \le (\nu(Y))^{\frac{1}{1} - \frac{1}{2}} \|g\|_2$. Plugging in the values, we get [@problem_id:1422001] [@problem_id:1422034]:
$$
\|g\|_1 \le (16)^{1/2} \cdot 10 = 4 \cdot 10 = 40
$$
The tightest possible upper bound for the $L^1$-norm is 40.

The case where $q=\infty$ follows a simpler, but related, argument. If $f \in L^\infty(X, \mu)$, then by definition, $|f(x)| \le \|f\|_\infty$ for almost every $x \in X$. Then, for any $p \ge 1$:
$$
\int_X |f(x)|^p \,d\mu \le \int_X \|f\|_\infty^p \,d\mu = \|f\|_\infty^p \mu(X)
$$
Taking the $p$-th root gives $\|f\|_p \le (\mu(X))^{1/p} \|f\|_\infty$. Since both terms on the right are finite, $\|f\|_p$ is finite, proving that $L^\infty(X, \mu) \subseteq L^p(X, \mu)$ for all $p \ge 1$.

### Strict Inclusions and the Failure of Nesting on Infinite Measure Spaces

We have established the inclusion $L^q \subseteq L^p$ for $p < q$ on [finite measure spaces](@entry_id:198109). A natural follow-up question is whether this inclusion is ever an equality. In general, it is not; the inclusions are strict. This means we can always find functions that belong to the larger space $L^p$ but not to the smaller one $L^q$.

Functions with singularities are canonical examples. Consider the interval $[0,1]$ with Lebesgue measure. Let's look for a function $f(x)=x^{-a}$ that belongs to $L^2([0,1])$ but not $L^4([0,1])$. The [integrability](@entry_id:142415) of $|f(x)|^p = x^{-ap}$ on $[0,1]$ depends on the behavior near $x=0$. The integral $\int_0^1 x^{-ap} dx$ is finite if and only if the exponent $-ap$ is greater than $-1$, which means $ap < 1$.
- For $f$ to be in $L^2$, we need $2a < 1$, or $a < \frac{1}{2}$.
- For $f$ to not be in $L^4$, we need $4a \ge 1$, or $a \ge \frac{1}{4}$.
Therefore, any function $f(x) = x^{-a}$ with $\frac{1}{4} \le a < \frac{1}{2}$ will be in $L^2([0,1])$ but not in $L^4([0,1])$. For example, the function $f(x)=x^{-1/3}$ satisfies this condition, as $a=1/3$ falls within the required range [@problem_id:1421996]. This demonstrates that $L^4([0,1])$ is a [proper subset](@entry_id:152276) of $L^2([0,1])$.

The finiteness of the measure $\mu(X)$ is the linchpin of this entire framework. If the [measure space](@entry_id:187562) is infinite, such as $\mathbb{R}$ with the Lebesgue measure, the nesting property breaks down completely. In fact, for $p \neq q$, neither of the spaces $L^p(\mathbb{R})$ and $L^q(\mathbb{R})$ is a subset of the other.

1.  **To show $L^q(\mathbb{R}) \not\subseteq L^p(\mathbb{R})$ for $p < q$**: We need a function that is in $L^q$ but not $L^p$. Such a function must decay slowly at infinity. Consider the function $f(x) = (1+|x|)^{-1/p}$. Its integral to the power of $p$ is $\int_{-\infty}^\infty (1+|x|)^{-1} dx$, which diverges. Thus, $f \notin L^p(\mathbb{R})$. However, its integral to the power of $q$ is $\int_{-\infty}^\infty (1+|x|)^{-q/p} dx$. Since $q > p$, the exponent $q/p > 1$, and this integral converges. Therefore, $f \in L^q(\mathbb{R})$.

2.  **To show $L^p(\mathbb{R}) \not\subseteq L^q(\mathbb{R})$ for $p < q$**: We need a function that is in $L^p$ but not $L^q$. Such a function must have a sufficiently strong singularity. Consider the function $g(x) = x^{-1/q}$ on the interval $(0, 1)$ and $g(x)=0$ otherwise. Its integral to the power of $p$ is $\int_0^1 x^{-p/q} dx$. Since $p < q$, the exponent $p/q < 1$, and this integral converges. Thus, $g \in L^p(\mathbb{R})$. However, its integral to the power of $q$ is $\int_0^1 x^{-1} dx$, which diverges. Therefore, $g \notin L^q(\mathbb{R})$.

These counterexamples illustrate that the behavior of functions at infinity (decay) and at singularities are decoupled on infinite [measure spaces](@entry_id:191702), preventing any nested structure.