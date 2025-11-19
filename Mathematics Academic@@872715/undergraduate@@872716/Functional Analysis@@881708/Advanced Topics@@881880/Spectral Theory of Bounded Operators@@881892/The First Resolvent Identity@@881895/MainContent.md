## Introduction
In the study of linear operators, the [resolvent operator](@entry_id:271964)—the inverse of $(A - \lambda I)$—is a tool of fundamental importance. While its definition is simple, its properties reveal the deep structural and spectral characteristics of the original operator A. The key that unlocks this deeper understanding is a simple but powerful algebraic relation known as the First Resolvent Identity. This article addresses the need to move beyond the resolvent as a mere computational inverse and explore the rich framework it provides. By mastering this identity, you will gain a powerful lens through which to analyze operators and their behavior across diverse scientific fields.

This article is structured to guide you from foundational principles to practical application. The first chapter, **"Principles and Mechanisms"**, will walk you through the derivation of the First Resolvent Identity and uncover its immediate consequences, including the [commutativity](@entry_id:140240) and analyticity of resolvent operators. The second chapter, **"Applications and Interdisciplinary Connections"**, will demonstrate the identity's far-reaching impact in areas like numerical analysis, dynamical systems, and quantum theory, where it appears as the famous Dyson equation. Finally, the **"Hands-On Practices"** section will provide you with concrete problems to solidify your understanding and apply the identity in different contexts.

## Principles and Mechanisms

In the study of linear operators, the concepts of spectrum and resolvent are foundational. While the spectrum, $\sigma(A)$, delineates the set of scalars $\lambda$ for which the operator $A - \lambda I$ is not invertible in a suitable sense, the [resolvent set](@entry_id:261708), $\rho(A) = \mathbb{C} \setminus \sigma(A)$, captures the region where this inversion is possible. The operator resulting from this inversion, known as the **[resolvent operator](@entry_id:271964)**, is not merely a computational tool; it possesses a rich structure that reveals deep properties of the original operator $A$. This chapter explores the central algebraic relation governing the resolvent—the [first resolvent identity](@entry_id:272370)—and uncovers its profound consequences for the analytic behavior of the resolvent and its connection to the spectral properties of $A$.

### The First Resolvent Identity

Let $A$ be a [bounded linear operator](@entry_id:139516) on a complex Banach space $X$. For any complex number $\lambda$ in the [resolvent set](@entry_id:261708) $\rho(A)$, the [resolvent operator](@entry_id:271964) is defined as the bounded inverse of $(A - \lambda I)$. Throughout this chapter, we will adopt the convention:
$$ R(\lambda, A) = (A - \lambda I)^{-1} $$
It is important to note that an alternative convention, $(\lambda I - A)^{-1}$, is also common in the literature. The two definitions differ only by a sign, and all results can be translated between them.

The power of [resolvent analysis](@entry_id:754283) stems from a simple yet fundamental algebraic relationship that connects the resolvent operators at two different points in the [resolvent set](@entry_id:261708). This relationship is known as the **[first resolvent identity](@entry_id:272370)** or **Hilbert's identity**.

To derive this identity, consider two distinct points $\lambda, \mu \in \rho(A)$. The key insight is to relate the operators $(A - \lambda I)$ and $(A - \mu I)$ via a simple algebraic manipulation:
$$ A - \lambda I = A - \mu I - \lambda I + \mu I = (A - \mu I) - (\lambda - \mu)I $$
This identity is trivial, yet it becomes powerful when we involve the resolvent operators. Since $\lambda \in \rho(A)$, the operator $R(\lambda, A) = (A - \lambda I)^{-1}$ exists. Let us left-multiply the identity by $R(\lambda, A)$:
$$ R(\lambda, A) (A - \lambda I) = R(\lambda, A)(A - \mu I) - (\lambda - \mu)R(\lambda, A)I $$
By the definition of an inverse, the left-hand side simplifies to the identity operator $I$:
$$ I = R(\lambda, A)(A - \mu I) - (\lambda - \mu)R(\lambda, A) $$
Now, since $\mu \in \rho(A)$, we can right-multiply the entire equation by $R(\mu, A) = (A - \mu I)^{-1}$:
$$ I R(\mu, A) = \left( R(\lambda, A)(A - \mu I) \right)R(\mu, A) - (\lambda - \mu)R(\lambda, A)R(\mu, A) $$
$$ R(\mu, A) = R(\lambda, A)\left( (A - \mu I)R(\mu, A) \right) - (\lambda - \mu)R(\lambda, A)R(\mu, A) $$
The term in the parentheses is again the [identity operator](@entry_id:204623), so we have:
$$ R(\mu, A) = R(\lambda, A) - (\lambda - \mu)R(\lambda, A)R(\mu, A) $$
Rearranging this equation gives the standard form of the [first resolvent identity](@entry_id:272370) [@problem_id:1890653]:
$$ R(\lambda, A) - R(\mu, A) = (\lambda - \mu)R(\lambda, A)R(\mu, A) $$
This equation is remarkable. It states that the difference between the resolvents at two points is proportional to their product, with the constant of proportionality being the scalar difference between the points themselves.

### Immediate Consequences of the Identity

The compact form of the resolvent identity belies its far-reaching implications. Several fundamental properties of the [resolvent operator](@entry_id:271964) can be deduced directly from it.

#### Commutativity of Resolvents

A foundational result that follows immediately from the identity is that resolvent operators at different points in the [resolvent set](@entry_id:261708) commute. While it is not true in general that if two operators $B$ and $C$ have inverses, their inverses commute, the resolvent operators of a *single* operator $A$ form a commuting family.

To see this, we can write the identity by swapping the roles of $\lambda$ and $\mu$:
$$ R(\mu, A) - R(\lambda, A) = (\mu - \lambda)R(\mu, A)R(\lambda, A) $$
Factoring out $-1$ from both sides, we get:
$$ -(R(\lambda, A) - R(\mu, A)) = -(\lambda - \mu)R(\mu, A)R(\lambda, A) $$
$$ R(\lambda, A) - R(\mu, A) = (\lambda - \mu)R(\mu, A)R(\lambda, A) $$
Comparing this with our original derivation, we have two expressions for the same quantity:
$$ (\lambda - \mu)R(\lambda, A)R(\mu, A) = (\lambda - \mu)R(\mu, A)R(\lambda, A) $$
Since we assumed $\lambda \neq \mu$, we can divide by the scalar $(\lambda - \mu)$ to conclude:
$$ R(\lambda, A)R(\mu, A) = R(\mu, A)R(\lambda, A) $$
This [commutativity](@entry_id:140240) is essential. It simplifies many calculations and is a cornerstone of the [functional calculus](@entry_id:138358). For instance, if we construct new operators from powers of resolvents, they will also commute. Consider the operators $P = R(\lambda_1, A)^2$ and $Q = R(\lambda_2, A)^3$ for distinct $\lambda_1, \lambda_2 \in \rho(A)$. Because $R(\lambda_1, A)$ and $R(\lambda_2, A)$ commute, any power of one will commute with any power of the other. Thus, $PQ = QP$. This means their commutator, $[Q, P] = QP - PQ$, is the zero operator. Consequently, algebraic expressions simplify, e.g., $(P+Q)^2 = P^2 + 2PQ + Q^2$, which is only true for [commuting operators](@entry_id:149529) [@problem_id:1890629].

#### Algebraic Interrelations

The resolvent identity provides a powerful tool for proving more complex algebraic relations among resolvent operators. Consider three distinct points $\lambda, \mu, \nu \in \rho(A)$. We can use the identity to establish a cyclic relationship. From the identity, we can write:
$$ (\lambda - \mu)R(\lambda, A)R(\mu, A) = R(\lambda, A) - R(\mu, A) $$
And similarly for the pairs $(\mu, \nu)$ and $(\nu, \lambda)$:
$$ (\mu - \nu)R(\mu, A)R(\nu, A) = R(\mu, A) - R(\nu, A) $$
$$ (\nu - \lambda)R(\nu, A)R(\lambda, A) = R(\nu, A) - R(\lambda, A) $$
Summing these three equations yields:
$$ (\lambda - \mu)R(\lambda, A)R(\mu, A) + (\mu - \nu)R(\mu, A)R(\nu, A) + (\nu - \lambda)R(\nu, A)R(\lambda, A) $$
$$ = (R(\lambda, A) - R(\mu, A)) + (R(\mu, A) - R(\nu, A)) + (R(\nu, A) - R(\lambda, A)) $$
The terms on the right-hand side cancel out in pairs, leaving the zero operator. This leads to the elegant cyclic relation [@problem_id:1890676]:
$$ (\lambda - \mu)R(\lambda, A)R(\mu, A) + (\mu - \nu)R(\mu, A)R(\nu, A) + (\nu - \lambda)R(\nu, A)R(\lambda, A) = 0 $$
This identity is another manifestation of the deep structural consistency of the resolvent map.

### The Analytic Nature of the Resolvent

Perhaps the most significant consequence of the [first resolvent identity](@entry_id:272370) is that it endows the [resolvent operator](@entry_id:271964) $R(\lambda, A)$ with analytic properties as a function of the complex variable $\lambda$.

#### The Neumann Series Expansion

The [first resolvent identity](@entry_id:272370) allows us to express the resolvent at one point, $\lambda$, in terms of the resolvent at a nearby point, $\mu$. Let's rearrange the identity $R(\lambda, A) - R(\mu, A) = (\lambda - \mu)R(\lambda, A)R(\mu, A)$ to solve for $R(\lambda, A)$:
$$ R(\lambda, A) - (\lambda - \mu)R(\lambda, A)R(\mu, A) = R(\mu, A) $$
Factoring out $R(\lambda, A)$ on the left (using right-distributivity):
$$ R(\lambda, A) [I - (\lambda - \mu)R(\mu, A)] = R(\mu, A) $$
If the operator $[I - (\lambda - \mu)R(\mu, A)]$ is invertible, we can write an explicit formula for $R(\lambda, A)$ [@problem_id:1890619]:
$$ R(\lambda, A) = R(\mu, A) [I - (\lambda - \mu)R(\mu, A)]^{-1} $$
This expression is exact. Its utility comes from the theory of **Neumann series**. For a [bounded operator](@entry_id:140184) $T$ with operator norm $\|T\|  1$, the operator $(I-T)$ is invertible, and its inverse is given by the convergent geometric series: $(I-T)^{-1} = \sum_{n=0}^{\infty} T^n$.

Applying this to our situation, if the scalar $|\lambda - \mu|$ is small enough such that $\|(\lambda - \mu)R(\mu, A)\| = |\lambda - \mu| \|R(\mu, A)\|  1$, then we can expand the inverse term as a power series:
$$ R(\lambda, A) = R(\mu, A) \sum_{n=0}^{\infty} [(\lambda - \mu)R(\mu, A)]^n $$
Distributing the leading $R(\mu, A)$ and using the [commutativity](@entry_id:140240) of resolvents, we obtain the Taylor-like expansion for $R(\lambda, A)$ around the point $\mu$ [@problem_id:1890636]:
$$ R(\lambda, A) = \sum_{n=0}^{\infty} (\lambda - \mu)^n R(\mu, A)^{n+1} $$
This expansion is fundamental. It shows that for any point $\mu \in \rho(A)$, the resolvent $R(\lambda, A)$ can be represented by a convergent [power series](@entry_id:146836) in a neighborhood of $\mu$ (specifically, the open disk of radius $1/\|R(\mu, A)\|$). This is the definition of an **operator-valued analytic function**. Two immediate consequences follow:
1.  The [resolvent set](@entry_id:261708) $\rho(A)$ is an **open subset** of the complex plane.
2.  The resolvent $R(\lambda, A)$ is infinitely differentiable with respect to $\lambda$ everywhere in $\rho(A)$.

#### Differentiability of the Resolvent

We can find the derivative of the resolvent directly from the first principles using the identity. The derivative is defined as the limit:
$$ \frac{d}{d\lambda} R(\lambda, A) = \lim_{h \to 0} \frac{R(\lambda+h, A) - R(\lambda, A)}{h} $$
Using the resolvent identity with $\lambda$ and $\mu=\lambda+h$, we have:
$$ R(\lambda, A) - R(\lambda+h, A) = (\lambda - (\lambda+h)) R(\lambda, A)R(\lambda+h, A) = -h R(\lambda, A)R(\lambda+h, A) $$
Multiplying by $-1$ gives $R(\lambda+h, A) - R(\lambda, A) = h R(\lambda, A)R(\lambda+h, A)$. Substituting this into the definition of the derivative:
$$ \frac{d}{d\lambda} R(\lambda, A) = \lim_{h \to 0} \frac{h R(\lambda, A)R(\lambda+h, A)}{h} = \lim_{h \to 0} R(\lambda, A)R(\lambda+h, A) $$
Because the resolvent function is continuous (a consequence of being analytic), the limit can be evaluated by substitution:
$$ \frac{d}{d\lambda} R(\lambda, A) = R(\lambda, A)R(\lambda, A) = R(\lambda, A)^2 $$
This remarkably simple formula, $\frac{d}{d\lambda} R(\lambda, A) = R(\lambda, A)^2$, is incredibly powerful [@problem_id:1890665]. (Note that if the convention $R(\lambda, A) = (\lambda I - A)^{-1}$ is used, the derivative becomes $-R(\lambda, A)^2$). This result is the gateway to using complex analysis tools, such as [contour integration](@entry_id:169446), on operator-valued functions, leading to the development of the holomorphic [functional calculus](@entry_id:138358).

### The Resolvent Identity and the Spectrum

The resolvent identity not only describes the behavior of $R(\lambda, A)$ within the [resolvent set](@entry_id:261708) but also characterizes it and illuminates its behavior near the boundary—the spectrum $\sigma(A)$.

#### Characterization of Resolvent Functions

The [first resolvent identity](@entry_id:272370) is not just a property of resolvents; it is their defining characteristic. That is, if an operator-valued function $F(\lambda)$ defined on some open domain $D \subset \mathbb{C}$ satisfies the identity $F(\lambda) - F(\mu) = (\lambda - \mu)F(\lambda)F(\mu)$ for all $\lambda, \mu \in D$, and if $F(\lambda)$ is invertible for at least one $\lambda \in D$, then $F(\lambda)$ must be the resolvent of some fixed operator $A$.

To prove this, we first establish a simpler identity for the inverse operators. Using the general relation $X^{-1} - Y^{-1} = X^{-1}(Y-X)Y^{-1}$ with $X=F(\lambda)$ and $Y=F(\mu)$, we have:
$$ F(\lambda)^{-1} - F(\mu)^{-1} = F(\lambda)^{-1}(F(\mu) - F(\lambda))F(\mu)^{-1} $$
From the given identity, $F(\mu) - F(\lambda) = -(\lambda - \mu)F(\lambda)F(\mu) = (\mu - \lambda)F(\lambda)F(\mu)$. Substituting this in gives:
$$ F(\lambda)^{-1} - F(\mu)^{-1} = F(\lambda)^{-1} ((\mu - \lambda)F(\lambda)F(\mu)) F(\mu)^{-1} = (\mu - \lambda) I $$
Rearranging this yields $F(\lambda)^{-1} + \lambda I = F(\mu)^{-1} + \mu I$. This shows that the operator expression $A = F(\lambda)^{-1} + \lambda I$ is independent of the choice of $\lambda \in D$. Therefore, $A$ is a constant operator. From this definition, we have $F(\lambda)^{-1} = A - \lambda I$, and by taking the inverse, we find:
$$ F(\lambda) = (A - \lambda I)^{-1} $$
This confirms that $F(\lambda)$ is precisely the resolvent of the operator $A$.

For the alternative convention where the identity is $\tilde{F}(\mu) - \tilde{F}(\lambda) = (\lambda - \mu)\tilde{F}(\lambda)\tilde{F}(\mu)$, a similar argument shows that $\tilde{F}(\lambda)^{-1} - \lambda I = -A$ is a constant operator, leading to $\tilde{F}(\lambda) = (\lambda I - A)^{-1}$. For example, given the [matrix-valued function](@entry_id:199897) $F(\lambda) = \frac{1}{\lambda^2 - 4\lambda + 3} \begin{pmatrix} \lambda - 2  1 \\ 1  \lambda - 2 \end{pmatrix}$, one can find its inverse and show that $T = \lambda I - F(\lambda)^{-1}$ is the constant matrix $\begin{pmatrix} 2  1 \\ 1  2 \end{pmatrix}$ [@problem_id:1890634].

#### Behavior Near the Spectrum

The [resolvent operator](@entry_id:271964) $R(\lambda, A)$ is defined only for $\lambda \in \rho(A)$. What happens as $\lambda$ approaches a point $\lambda_0$ in the spectrum $\sigma(A)$? The Neumann series provides a powerful insight. We saw that for any $\mu \in \rho(A)$, the [resolvent set](@entry_id:261708) contains an open disk $B(\mu, r)$ where $r = 1/\|R(\mu, A)\|$. This means the distance from $\mu$ to the nearest point in the spectrum must be at least this radius:
$$ \operatorname{dist}(\mu, \sigma(A)) \ge \frac{1}{\|R(\mu, A)\|} $$
This can be rearranged into a fundamental inequality:
$$ \|R(\mu, A)\| \ge \frac{1}{\operatorname{dist}(\mu, \sigma(A))} $$
Now, let $\lambda$ approach a point $\lambda_0 \in \sigma(A)$. Since the spectrum $\sigma(A)$ is a [closed set](@entry_id:136446), the distance $\operatorname{dist}(\lambda, \sigma(A))$ will approach $0$. The inequality above then implies that the norm of the resolvent must grow without bound:
$$ \lim_{\lambda \to \lambda_0} \|R(\lambda, A)\| = \infty $$
This proves that the [resolvent operator](@entry_id:271964) cannot have a limit in the [operator norm](@entry_id:146227) as $\lambda$ approaches the spectrum. The resolvent "blows up" at the spectral boundary, a behavior that is central to spectral theory [@problem_id:1890626].

### Advanced Application: Spectral Projections

The analyticity of the resolvent allows the use of [contour integration](@entry_id:169446) to define operators associated with parts of the spectrum. If the spectrum $\sigma(A)$ can be separated into two disjoint [compact sets](@entry_id:147575), $\sigma_1$ and $\sigma_2$, we can choose contours $\gamma_1$ and $\gamma_2$ in the [resolvent set](@entry_id:261708) such that $\gamma_1$ encloses $\sigma_1$ (but not $\sigma_2$) and $\gamma_2$ encloses $\sigma_2$ (but not $\sigma_1$). The **Riesz spectral projections** are then defined by:
$$ P_1 = -\frac{1}{2\pi i} \oint_{\gamma_1} R(z, A) \, dz \quad \text{and} \quad P_2 = -\frac{1}{2\pi i} \oint_{\gamma_2} R(z, A) \, dz $$
(The sign convention here is consistent with $R(z, A) = (A-zI)^{-1}$).

The [first resolvent identity](@entry_id:272370) can be used to show a remarkable property of these projections: they are mutually orthogonal, meaning their product is the zero operator. Let's examine the product $P_1 P_2$:
$$ P_1 P_2 = \left(-\frac{1}{2\pi i}\right)^2 \oint_{\gamma_1} R(z, A) \, dz \oint_{\gamma_2} R(w, A) \, dw $$
$$ P_1 P_2 = -\frac{1}{4\pi^2} \oint_{\gamma_1} \oint_{\gamma_2} R(z, A) R(w, A) \, dw \, dz $$
Using the resolvent identity, $R(z, A)R(w, A) = \frac{R(z, A) - R(w, A)}{z-w}$, we can rewrite the integrand:
$$ P_1 P_2 = -\frac{1}{4\pi^2} \oint_{\gamma_1} \oint_{\gamma_2} \frac{R(z, A) - R(w, A)}{z-w} \, dw \, dz $$
We can split this into two parts:
$$ P_1 P_2 = -\frac{1}{4\pi^2} \left( \oint_{\gamma_1} R(z, A) \left( \oint_{\gamma_2} \frac{1}{z-w} \, dw \right) dz - \oint_{\gamma_2} R(w, A) \left( \oint_{\gamma_1} \frac{1}{z-w} \, dz \right) dw \right) $$
Let's analyze the inner integrals. For the first term, $z$ lies on $\gamma_1$ and $w$ on $\gamma_2$. Since $\gamma_1$ and the region it encloses are entirely outside of $\gamma_2$, the function $f(w) = \frac{1}{z-w}$ is holomorphic inside and on $\gamma_2$. By Cauchy's Integral Theorem, its integral is zero: $\oint_{\gamma_2} \frac{1}{z-w} \, dw = 0$.
For the second term, $w$ is on $\gamma_2$ and $z$ is on $\gamma_1$. The point $w$ is outside the contour $\gamma_1$. By Cauchy's Integral Formula, $\oint_{\gamma_1} \frac{1}{z-w} \, dz = 2\pi i \cdot 0 = 0$.
Since both inner integrals are zero, the entire expression collapses to zero [@problem_id:1890649].
$$ P_1 P_2 = 0 $$
This result demonstrates that spectral projections corresponding to disjoint parts of the spectrum are orthogonal, allowing for the decomposition of the space $X$ into a direct [sum of subspaces](@entry_id:180324) on which the operator $A$ acts independently. This powerful technique, built upon the simple algebraic foundation of the [first resolvent identity](@entry_id:272370), is a cornerstone of modern [operator theory](@entry_id:139990) and its applications in quantum mechanics and differential equations.