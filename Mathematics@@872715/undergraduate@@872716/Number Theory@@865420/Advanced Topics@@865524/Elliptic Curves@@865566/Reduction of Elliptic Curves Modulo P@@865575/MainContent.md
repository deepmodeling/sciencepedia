## Introduction
Elliptic curves, simple in their cubic formulation, are objects of profound arithmetic depth. A central challenge in their study lies in understanding the structure of their rational points, $E(\mathbb{Q})$, which form a [finitely generated abelian group](@entry_id:196575). A powerful strategy to unravel the global structure of this group is the "[local-to-global principle](@entry_id:160553)": assembling information gleaned from studying the curve over simpler, [local fields](@entry_id:195717). The most fundamental application of this principle is the process of reducing an elliptic curve modulo a prime $p$, which transforms a problem in continuous arithmetic over $\mathbb{Q}$ into one in discrete arithmetic over a [finite field](@entry_id:150913) $\mathbb{F}_p$. This reduction reveals crucial data about the curve's intrinsic properties.

This article provides a comprehensive overview of the theory and application of reducing [elliptic curves](@entry_id:152409) modulo $p$.
- **Principles and Mechanisms** will introduce the core concepts, explaining the process of reduction, the distinction between [good and bad reduction](@entry_id:635877), the [classification of singularities](@entry_id:194333), and the deep structural results like Hasse's Theorem and the Néron-Ogg-Shafarevich criterion.
- **Applications and Interdisciplinary Connections** will demonstrate the power of this theory, showing how it is used to compute fundamental invariants like the conductor, determine the rational [torsion subgroup](@entry_id:139454), and how it forms the bedrock for applications in [cryptography](@entry_id:139166) and the proof of Fermat's Last Theorem.
- Finally, **Hands-On Practices** will offer guided exercises to apply these concepts to concrete examples.

The journey begins by exploring the mechanics of this reduction process and the fundamental dichotomy it introduces.

## Principles and Mechanisms

The study of elliptic curves over the rational numbers is deeply enriched by examining their behavior when reduced modulo a prime number $p$. This process transforms an object of continuous arithmetic over $\mathbb{Q}$ into one of discrete arithmetic over a finite field $\mathbb{F}_p$, creating a powerful bridge between two worlds. The nature of this reduced curve reveals profound information about the original curve's arithmetic structure. This chapter explores the principles governing this reduction and the mechanisms by which we classify and understand its outcomes.

### The Reduction Modulo *p* Process

Let $E$ be an elliptic curve defined over the rational numbers $\mathbb{Q}$. It can be described by a **Weierstrass equation**. While a general form exists, for primes $p \ge 5$, any such curve is isomorphic over $\mathbb{Q}$ to one given by a **short Weierstrass equation**:
$$ E: y^2 = x^3 + Ax + B $$
where $A, B \in \mathbb{Q}$. An [elliptic curve](@entry_id:163260) is a *smooth* curve, a condition guaranteed by the non-vanishing of its **[discriminant](@entry_id:152620)**. For the short Weierstrass equation, the discriminant is given by the quantity $\Delta = -16(4A^3 + 27B^2)$. The condition for $E$ to be an [elliptic curve](@entry_id:163260) is precisely that $\Delta \neq 0$ [@problem_id:3089584]. This is equivalent to the cubic polynomial $x^3+Ax+B$ having distinct roots.

To study the reduction of $E$ modulo a prime $p$, we first need an integral model, i.e., an equation where the coefficients $A$ and $B$ are integers. This can always be achieved by a suitable change of variables. Once we have such a model with $A, B \in \mathbb{Z}$, the **reduction of E modulo p**, denoted $\widetilde{E}$, is the curve over the finite field $\mathbb{F}_p$ defined by the same equation, where the coefficients are interpreted as elements of $\mathbb{F}_p$:
$$ \widetilde{E}: y^2 = x^3 + \bar{A}x + \bar{B} \quad \text{over } \mathbb{F}_p $$
where $\bar{A} = A \pmod{p}$ and $\bar{B} = B \pmod{p}$.

### Good and Bad Reduction

The most fundamental question about the reduced curve $\widetilde{E}$ is whether it retains the essential geometric property of the original curve: smoothness. Just as for $E$, the curve $\widetilde{E}$ is smooth, and thus an [elliptic curve](@entry_id:163260) over $\mathbb{F}_p$, if its [discriminant](@entry_id:152620) is non-zero in the field $\mathbb{F}_p$. The [discriminant](@entry_id:152620) of $\widetilde{E}$ is $\widetilde{\Delta} = -16(4\bar{A}^3 + 27\bar{B}^2)$.

Since we assume $p \ge 5$, the factor $-16$ is non-zero modulo $p$. Therefore, $\widetilde{\Delta} \not\equiv 0 \pmod{p}$ if and only if $4\bar{A}^3 + 27\bar{B}^2 \not\equiv 0 \pmod{p}$. This latter expression is simply the reduction of the integer $4A^3+27B^2$ modulo $p$. Consequently, for a prime $p \ge 5$, the reduced curve $\widetilde{E}$ is an elliptic curve if and only if $p$ does not divide the [discriminant](@entry_id:152620) $\Delta$ of the integral model we started with [@problem_id:3089560], [@problem_id:3089584].

This leads to a crucial dichotomy:

-   **Good Reduction**: We say that $E$ has **good reduction** at $p$ if the reduced curve $\widetilde{E}$ is smooth (i.e., is an [elliptic curve](@entry_id:163260) over $\mathbb{F}_p$).

-   **Bad Reduction**: We say that $E$ has **bad reduction** at $p$ if the reduced curve $\widetilde{E}$ is singular.

A potential ambiguity arises: does the property of having good or bad reduction depend on the specific integral Weierstrass model we choose for $E$? Indeed it does. For example, if we start with a model $y^2 = x^3+Ax+B$ having good reduction at $p$, we can perform a change of variables $x=p^2x'$ and $y=p^3y'$ and clear denominators to obtain a new integral model $y'^2 = x'^3 + Ap^{-4}x' + Bp^{-6}$ which, when scaled to have integer coefficients, will have a discriminant divisible by a high power of $p$, and thus have bad reduction.

To resolve this, we must consider all possible integral models. The discriminants of any two integral models for $E$ are related by $\Delta' = u^{12}\Delta$ for some $u \in \mathbb{Q}^\times$. This implies that the set of $p$-adic valuations $\{v_p(\Delta)\}$ for all integral models of $E$ has a well-defined minimum, $v_p(\Delta_{\min})$. An integral model that achieves this minimum is called a **[minimal model](@entry_id:268530)** at $p$. The property of good reduction can then be defined invariantly:

An [elliptic curve](@entry_id:163260) $E/\mathbb{Q}$ has **good reduction** at a prime $p$ if and only if the [discriminant](@entry_id:152620) of a [minimal model](@entry_id:268530) at $p$, $\Delta_{\min}$, is not divisible by $p$. That is, $v_p(\Delta_{\min}) = 0$ [@problem_id:3089627].

Equivalently, and more practically, $E$ has good reduction at $p$ if there exists *any* integral Weierstrass model for $E$ whose [discriminant](@entry_id:152620) is not divisible by $p$ [@problem_id:3089610].

### Classification of Bad Reduction

When an elliptic curve $E$ has bad reduction at a prime $p \ge 5$, its reduction $\widetilde{E}$ is a singular cubic curve. A singular cubic curve over a field has exactly one singular point over the [algebraic closure](@entry_id:151964) of that field [@problem_id:3089584]. The local geometry at this [singular point](@entry_id:171198) provides a refined classification of bad reduction [@problem_id:3089585].

To analyze the singularity, we translate the singular point to the origin $(0,0)$ and examine the lowest-degree terms of the transformed equation. These terms define the **tangent cone** at the singularity. For a singular cubic, the [tangent cone](@entry_id:159686) is given by a homogeneous quadratic polynomial. The nature of its roots determines the type of singularity:

1.  **Node**: If the tangent cone consists of two distinct lines, the singularity is a **node**. This type of bad reduction is called **multiplicative reduction**.
2.  **Cusp**: If the tangent cone consists of a single line with [multiplicity](@entry_id:136466) two, the singularity is a **cusp**. This type of bad reduction is called **additive reduction**.

For a short Weierstrass equation $y^2 = x^3 + \bar{A}x + \bar{B}$ over $\mathbb{F}_p$ with $p \ge 5$, these geometric criteria correspond to a simple algebraic condition on the coefficients [@problem_id:3089606]:
-   The singularity is a **cusp** (additive reduction) if and only if the singular curve is $y^2=x^3$. This occurs if and only if $\bar{A}=0$ and $\bar{B}=0$.
-   The singularity is a **node** (multiplicative reduction) if and only if the curve is singular (i.e., $4\bar{A}^3+27\bar{B}^2=0$) but it is not the case that both $\bar{A}=0$ and $\bar{B}=0$.

Multiplicative reduction can be further subdivided. The two tangent lines at a node may have slopes that are defined over $\mathbb{F}_p$, or they may be defined only over the [quadratic extension](@entry_id:152175) $\mathbb{F}_{p^2}$.

-   **Split Multiplicative Reduction**: The [tangent lines](@entry_id:168168) at the node are rational over $\mathbb{F}_p$. This occurs when the quadratic equation for the slopes has solutions in $\mathbb{F}_p$.
-   **Non-split Multiplicative Reduction**: The [tangent lines](@entry_id:168168) at the node are not rational over $\mathbb{F}_p$ and are interchanged by the Frobenius [automorphism](@entry_id:143521). This occurs when the quadratic equation for the slopes has no solutions in $\mathbb{F}_p$.

**Example:** Consider the curve $E: y^2 = x^3 + 8x + 2$ and its reduction at $p=11$. The reduced curve is $\widetilde{E}: y^2 = x^3+8x+2$ over $\mathbb{F}_{11}$. One can verify that $(1,0)$ is the unique singular point. Translating this point to the origin via $X=x-1, Y=y$, the equation becomes $Y^2 = X^3+3X^2$. The tangent cone is given by $Y^2 = 3X^2$. The slopes of the tangent lines are the solutions to $m^2 = 3$ in $\mathbb{F}_{11}$. Since $5^2 = 25 \equiv 3 \pmod{11}$, the slopes are $m = \pm 5$, which are distinct elements of $\mathbb{F}_{11}$. Thus, the singularity is a node with tangents defined over $\mathbb{F}_{11}$. The curve $E$ has **split multiplicative reduction** at $p=11$ [@problem_id:3089629].

### Properties of Good Reduction

When $E$ has good reduction at $p$, the reduced curve $\widetilde{E}$ is an [elliptic curve](@entry_id:163260) over the [finite field](@entry_id:150913) $\mathbb{F}_p$. A central object of study is the set of its rational points, $\widetilde{E}(\mathbb{F}_p)$, which forms a finite [abelian group](@entry_id:139381). The size of this group is constrained by a fundamental result. We define the **trace of Frobenius** $a_p$ as the integer
$$ a_p = p + 1 - \#\widetilde{E}(\mathbb{F}_p) $$
The number of points does not wildly fluctuate but is always close to $p+1$, the number of points on the projective line over $\mathbb{F}_p$. The precise statement is **Hasse's Theorem**.

**Theorem (Hasse):** For an elliptic curve over a [finite field](@entry_id:150913) $\mathbb{F}_p$, the trace of Frobenius $a_p$ satisfies the bound $|a_p| \le 2\sqrt{p}$.

This theorem, a special case of the Riemann Hypothesis for curves over finite fields, can be justified through advanced methods [@problem_id:3089586]. One approach considers the **Frobenius endomorphism** $\pi(x,y)=(x^p, y^p)$, whose characteristic polynomial is $T^2 - a_p T + p$. Its eigenvalues are complex conjugates $\alpha, \beta$ with absolute value $|\alpha|=|\beta|=\sqrt{p}$, from which the [triangle inequality](@entry_id:143750) gives $|a_p|=|\alpha+\beta| \le 2\sqrt{p}$. Another approach relates $a_p$ to a [character sum](@entry_id:192985), whose magnitude is bounded by the Weil bound.

The value of the trace of Frobenius $a_p$ leads to another important classification for primes of good reduction.

-   **Ordinary Reduction**: $E$ has **ordinary reduction** at $p$ if the trace of Frobenius $a_p$ is not divisible by $p$.
-   **Supersingular Reduction**: $E$ has **supersingular reduction** at $p$ if the trace of Frobenius $a_p$ is divisible by $p$.

Supersingularity is a rare and arithmetically significant phenomenon. It can be characterized in several equivalent ways, which reveal its deep structural implications [@problem_id:3089614]:
1.  The trace of Frobenius satisfies $a_p \equiv 0 \pmod p$.
2.  The group of $p$-[torsion points](@entry_id:192744) over the [algebraic closure](@entry_id:151964) is trivial: $\widetilde{E}(\overline{\mathbb{F}}_p)[p] = \{\mathcal{O}\}$.
3.  The multiplication-by-$p$ endomorphism $[p]: \widetilde{E} \to \widetilde{E}$ is a purely inseparable map.
4.  The ring of endomorphisms of $\widetilde{E}$ over $\overline{\mathbb{F}}_p$ is non-commutative; it is an order in a [quaternion algebra](@entry_id:193983).

In contrast, for an ordinary curve, the $p$-[torsion group](@entry_id:144787) is $\widetilde{E}(\overline{\mathbb{F}}_p)[p] \cong \mathbb{Z}/p\mathbb{Z}$, and the [endomorphism ring](@entry_id:185357) is a commutative order in an [imaginary quadratic field](@entry_id:203833).

### The Structure of Points over *p*-adic Fields

The reduction type of an [elliptic curve](@entry_id:163260) at a prime $p$ also dictates the structure of its group of points over the $p$-adic field $\mathbb{Q}_p$. Points on $E(\mathbb{Q}_p)$ can be filtered according to their behavior under the reduction map $\text{red}: E(\mathbb{Q}_p) \to \widetilde{E}(\mathbb{F}_p)$. We define a [filtration](@entry_id:162013) of subgroups:
$$ E(\mathbb{Q}_p) \supseteq E_0(\mathbb{Q}_p) \supseteq E_1(\mathbb{Q}_p) $$
where:
-   $E_0(\mathbb{Q}_p)$ is the subgroup of points that reduce to a non-[singular point](@entry_id:171198) of $\widetilde{E}$.
-   $E_1(\mathbb{Q}_p)$ is the subgroup of points that reduce to the identity element $\widetilde{\mathcal{O}} \in \widetilde{E}(\mathbb{F}_p)$. This is the **kernel of the reduction map**.

The structure of the [quotient groups](@entry_id:145113) in this [filtration](@entry_id:162013) is completely determined by the reduction type [@problem_id:3089605]:
-   **Good Reduction:** $\widetilde{E}$ is entirely non-singular, so $E_0(\mathbb{Q}_p) = E(\mathbb{Q}_p)$. The reduction map is surjective, yielding a fundamental [short exact sequence](@entry_id:137930):
    $$ 0 \to E_1(\mathbb{Q}_p) \to E(\mathbb{Q}_p) \to \widetilde{E}(\mathbb{F}_p) \to 0 $$
-   **Multiplicative Reduction:** The group of non-[singular points](@entry_id:266699) $\widetilde{E}_{\text{ns}}(\mathbb{F}_p)$ is isomorphic to the [multiplicative group](@entry_id:155975) of the field, $\mathbb{F}_p^\times$. The quotient is:
    $$ E_0(\mathbb{Q}_p) / E_1(\mathbb{Q}_p) \cong \mathbb{F}_p^\times $$
-   **Additive Reduction:** The group of non-singular points $\widetilde{E}_{\text{ns}}(\mathbb{F}_p)$ is isomorphic to the [additive group](@entry_id:151801) of the field, $(\mathbb{F}_p, +)$. The quotient is:
    $$ E_0(\mathbb{Q}_p) / E_1(\mathbb{Q}_p) \cong (\mathbb{F}_p, +) $$

The kernel of reduction, $E_1(\mathbb{Q}_p)$, can be understood through the theory of **formal groups**. It is an infinite, compact pro-$p$ group. In the case of good reduction (for $p \ge 5$), it is isomorphic as a [topological group](@entry_id:154498) to the [additive group](@entry_id:151801) of $p$-adic integers $p\mathbb{Z}_p$, and is therefore torsion-free [@problem_id:3089605].

### The Néron-Ogg-Shafarevich Criterion

The discussion thus far reveals a deep relationship between the reduction type of an elliptic curve at $p$ and its arithmetic properties. The most profound formulation of this relationship is the **Néron-Ogg-Shafarevich criterion**, which connects good reduction to the behavior of the Galois representation associated with the curve.

For a prime $\ell \neq p$, the absolute Galois group $G_{\mathbb{Q}} = \text{Gal}(\overline{\mathbb{Q}}/\mathbb{Q})$ acts on the group of $\ell^n$-[torsion points](@entry_id:192744) $E[\ell^n]$ for all $n$. This defines a continuous [group homomorphism](@entry_id:140603), the **$\ell$-adic Galois representation**:
$$ \rho_{E,\ell}: G_{\mathbb{Q}} \to \text{Aut}(T_\ell(E)) \cong \text{GL}_2(\mathbb{Z}_\ell) $$
where $T_\ell(E)$ is the $\ell$-adic Tate module. When we consider the action of the local Galois group $G_{\mathbb{Q}_p} = \text{Gal}(\overline{\mathbb{Q}}_p/\mathbb{Q}_p)$, we can ask if this representation is **unramified**. This means that the **inertia subgroup** $I_p \subset G_{\mathbb{Q}_p}$, which corresponds to automorphisms fixing the residue field, acts trivially on the Tate module. The criterion provides a stunning equivalence.

**Theorem (Néron-Ogg-Shafarevich):** An elliptic curve $E/\mathbb{Q}$ has good reduction at a prime $p$ if and only if for some (and hence every) prime $\ell \neq p$, the Galois representation $\rho_{E,\ell}$ is unramified at $p$.

This theorem states that the geometric property of having a smooth reduction is perfectly mirrored by the representation-theoretic property of [the inertia group](@entry_id:200010) acting trivially on the [torsion points](@entry_id:192744) [@problem_id:3089627]. A refined version states that it is sufficient to check for a trivial inertia action on the $\ell$-[torsion points](@entry_id:192744) $E[\ell]$ for a single $\ell \neq p$.

This criterion distinguishes good reduction from **potential good reduction**, where the curve acquires good reduction over some finite extension of $\mathbb{Q}_p$. Potential good reduction is equivalent to the $j$-invariant of the curve being a $p$-adic integer ($v_p(j(E)) \ge 0$), and corresponds to [the inertia group](@entry_id:200010) $I_p$ acting through a finite quotient on the Tate module. Good reduction is the special case where this finite action is trivial.