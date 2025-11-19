## Introduction
In [commutative algebra](@entry_id:149047), understanding the relationship between a ring and its extensions is a central pursuit. When one ring, $R$, is a subring of another, $S$, a fundamental question arises: how do the structures of their [prime ideals](@entry_id:154026) correspond? Specifically, if we have a prime ideal in $R$, can we be certain to find a prime ideal in $S$ that "lies over" it? This problem of lifting [prime ideals](@entry_id:154026) is not always solvable and highlights a crucial knowledge gap in the general theory of ring extensions.

This article addresses this gap by introducing the concept of **integrality**, a condition on the extension $R \subseteq S$ that provides the missing link. You will learn how integrality gives rise to two of the most powerful results in the field: the Lying Over and Going Up theorems. Across three main sections, we will build a comprehensive understanding of this theory. The first section, "Principles and Mechanisms," will establish the formal statements of the theorems, explore the logic behind their proofs, and illustrate why integrality is the necessary condition. Following this, "Applications and Interdisciplinary Connections" will demonstrate the theorems' power by exploring their profound impact on [algebraic number](@entry_id:156710) theory and algebraic geometry. Finally, "Hands-On Practices" will provide guided problems to help you apply these abstract concepts to concrete computational examples, solidifying your grasp of the material.

## Principles and Mechanisms

In our study of [ring theory](@entry_id:143825), a central theme is the relationship between a ring $R$ and an extension ring $S$. When we have a subring $R \subseteq S$, a natural and fundamental question arises: how does the algebraic structure of $S$ relate to that of $R$? Specifically, we are interested in the correspondence between their [prime ideals](@entry_id:154026). Given a prime ideal $\mathfrak{p}$ in $R$, can we find a [prime ideal](@entry_id:149360) $\mathfrak{q}$ in $S$ whose "shadow" in $R$ is precisely $\mathfrak{p}$? Formally, we ask if there exists a [prime ideal](@entry_id:149360) $\mathfrak{q} \subseteq S$ such that $\mathfrak{q} \cap R = \mathfrak{p}$. When such a $\mathfrak{q}$ exists, we say that $\mathfrak{q}$ **lies over** $\mathfrak{p}$.

This chapter explores the conditions under which we can guarantee the existence of such ideals. We will discover that a property called **integrality** provides the crucial link, giving rise to powerful results known as the Lying Over and Going Up theorems. These theorems form the bedrock of [integral extension](@entry_id:150735) theory and have profound implications in both algebraic geometry and [algebraic number](@entry_id:156710) theory.

### The Integral Condition: Why It Matters

The guarantee that we can always find a [prime ideal](@entry_id:149360) lying over another is not universal. It depends critically on the nature of the extension $R \subseteq S$. The key property is that of an **[integral extension](@entry_id:150735)**. We say that $S$ is an [integral extension](@entry_id:150735) of $R$ if every element $s \in S$ is **integral over** $R$; that is, for each $s \in S$, there exists a [monic polynomial](@entry_id:152311) $f(x) \in R[x]$ such that $f(s) = 0$.

To appreciate the necessity of this condition, let us examine two extensions that are *not* integral.

First, consider the extension $\mathbb{Z} \subseteq \mathbb{Z}[1/5]$ [@problem_id:1836434]. The element $1/5 \in \mathbb{Z}[1/5]$ is not integral over $\mathbb{Z}$, as the only rational numbers integral over $\mathbb{Z}$ are the integers themselves. Now, let's consider the prime ideal $\mathfrak{p} = (5)$ in $\mathbb{Z}$. Can we find a [prime ideal](@entry_id:149360) $\mathfrak{q}$ in $\mathbb{Z}[1/5]$ that lies over $(5)$? The answer is no. In the ring $\mathbb{Z}[1/5]$, the element $5$ is a unit, since its inverse, $1/5$, is an element of the ring by definition. If an ideal contains a unit, it must be the entire ring. Therefore, any ideal $\mathfrak{q}$ containing $5$ would be $\mathbb{Z}[1/5]$ itself, which is not a prime ideal. Consequently, for any [prime ideal](@entry_id:149360) $\mathfrak{q}$ in $\mathbb{Z}[1/5]$, we must have $5 \notin \mathfrak{q}$. This means that $\mathfrak{q} \cap \mathbb{Z}$ cannot be $(5)$, because $5 \in (5)$. Thus, the Lying Over property fails for the prime ideal $(5)$.

An even more striking failure occurs with the extension $\mathbb{Z} \subseteq \mathbb{Q}$ [@problem_id:1836469]. This extension is also not integral. The ring of rational numbers $\mathbb{Q}$ is a field, which means its only ideals are the zero ideal $(0)$ and the entire ring $\mathbb{Q}$. Since a prime ideal must be a proper ideal, the only [prime ideal](@entry_id:149360) in $\mathbb{Q}$ is $\mathfrak{q} = (0)$. If we contract this to $\mathbb{Z}$, we find that $\mathfrak{q} \cap \mathbb{Z} = (0) \cap \mathbb{Z} = (0)$. This means that the only prime ideal of $\mathbb{Z}$ that has a prime of $\mathbb{Q}$ lying over it is the zero ideal. For any non-zero prime ideal in $\mathbb{Z}$, such as $(2)$, $(3)$, or $(5)$, there is no [prime ideal](@entry_id:149360) in $\mathbb{Q}$ that lies over it.

These examples strongly suggest that the Lying Over property is not a general feature of ring extensions. In contrast, consider the [integral extension](@entry_id:150735) $\mathbb{Z} \subseteq \mathbb{Z}[\phi]$, where $\phi = \frac{1+\sqrt{5}}{2}$ is the golden ratio. The element $\phi$ is integral over $\mathbb{Z}$ because it is a root of the [monic polynomial](@entry_id:152311) $x^2 - x - 1 = 0$. It can be shown that this extension *does* satisfy the Lying Over property for all [prime ideals](@entry_id:154026) of $\mathbb{Z}$, including $(5)$ [@problem_id:1836434]. This contrast motivates our focus on [integral extensions](@entry_id:149214) as the correct setting for these theorems.

### The Lying Over Theorem

The insight from the previous examples is formalized in the first major result of this chapter.

**The Lying Over Theorem:** Let $R \subseteq S$ be an [integral extension](@entry_id:150735) of [commutative rings](@entry_id:148261). For any prime ideal $\mathfrak{p}$ of $R$, there exists a [prime ideal](@entry_id:149360) $\mathfrak{q}$ of $S$ such that $\mathfrak{q} \cap R = \mathfrak{p}$.

This theorem provides a powerful guarantee. Geometrically, it can be interpreted in the language of prime spectra. For any [commutative ring](@entry_id:148075) $A$, its **prime spectrum**, denoted $\mathrm{Spec}(A)$, is the set of all its [prime ideals](@entry_id:154026). A [ring homomorphism](@entry_id:153804) $R \to S$ induces a continuous map $f: \mathrm{Spec}(S) \to \mathrm{Spec}(R)$ defined by $f(\mathfrak{q}) = \mathfrak{q} \cap R$. The Lying Over Theorem is precisely the statement that if $R \subseteq S$ is an [integral extension](@entry_id:150735), this [induced map](@entry_id:271712) is surjective [@problem_id:1836467]. For every point $\mathfrak{p}$ in the "base space" $\mathrm{Spec}(R)$, there is at least one point $\mathfrak{q}$ in the "[covering space](@entry_id:139261)" $\mathrm{Spec}(S)$ that maps to it.

#### Proof Sketch and Key Lemmas

The standard proof of the Lying Over Theorem is elegant and instructive, relying on the technique of localization and two fundamental lemmas. The strategy is as follows:

1.  Given a [prime ideal](@entry_id:149360) $\mathfrak{p} \subset R$, we localize both rings at the multiplicative set $U = R \setminus \mathfrak{p}$. This yields an extension of local rings $R_\mathfrak{p} \subseteq S_\mathfrak{p}$, which is also an [integral extension](@entry_id:150735). The unique [maximal ideal](@entry_id:151331) of $R_\mathfrak{p}$ is $\mathfrak{p}R_\mathfrak{p}$.
2.  We show that there must exist a prime ideal $\mathfrak{M}$ in $S_\mathfrak{p}$ that lies over $\mathfrak{p}R_\mathfrak{p}$.
3.  The contraction of this ideal $\mathfrak{M}$ back to $S$ gives the desired prime ideal $\mathfrak{q}$.

The core of the argument lies in step 2. First, one must show that $\mathfrak{p}S_\mathfrak{p} \neq S_\mathfrak{p}$. This is often proven by contradiction using **Nakayama's Lemma**. If one assumes $\mathfrak{p}S_\mathfrak{p} = S_\mathfrak{p}$, Nakayama's Lemma can be used to imply that $S_\mathfrak{p} = \{0/1\}$ [@problem_id:1836472]. This is a contradiction, as it would imply that some element of $R \setminus \mathfrak{p}$ annihilates $1 \in S$, which is impossible. Since $\mathfrak{p}S_\mathfrak{p}$ is a proper ideal of $S_\mathfrak{p}$, it must be contained in some [maximal ideal](@entry_id:151331) $\mathfrak{M}$ of $S_\mathfrak{p}$.

The final piece of the puzzle is to show that this [maximal ideal](@entry_id:151331) $\mathfrak{M}$ lies over $\mathfrak{p}R_\mathfrak{p}$. This step relies on a beautiful result connecting integrality and field structures [@problem_id:1836439].

**Lemma:** If $R \subseteq S$ is an [integral extension](@entry_id:150735) of [integral domains](@entry_id:155321) and $S$ is a field, then $R$ is also a field.

*Proof:* Let $r \in R$ be a non-zero element. Since $S$ is a field, $r$ has an inverse $r^{-1} \in S$. Because the extension is integral, $r^{-1}$ must satisfy a [monic polynomial](@entry_id:152311) equation with coefficients in $R$:
$$(r^{-1})^n + a_{n-1}(r^{-1})^{n-1} + \dots + a_1 r^{-1} + a_0 = 0, \quad \text{where } a_i \in R.$$
Multiplying the entire equation by $r^{n-1}$, we get:
$$r^{-1} + a_{n-1} + a_{n-2}r + \dots + a_1 r^{n-2} + a_0 r^{n-1} = 0.$$
Solving for $r^{-1}$, we find:
$$r^{-1} = -(a_{n-1} + a_{n-2}r + \dots + a_0 r^{n-1}).$$
The right-hand side is a [sum of products](@entry_id:165203) of elements of $R$, so it is itself an element of $R$. Thus, the inverse of $r$ is in $R$. Since every non-zero element of $R$ has an inverse in $R$, $R$ must be a field.

This lemma is applied to the [quotient rings](@entry_id:148632). Since $\mathfrak{M}$ is a [maximal ideal](@entry_id:151331) of $S_\mathfrak{p}$, the quotient $S_\mathfrak{p}/\mathfrak{M}$ is a field. This field is an [integral extension](@entry_id:150735) of the integral domain $R_\mathfrak{p} / (\mathfrak{M} \cap R_\mathfrak{p})$. By the lemma, $R_\mathfrak{p} / (\mathfrak{M} \cap R_\mathfrak{p})$ must also be a field. This implies that $\mathfrak{M} \cap R_\mathfrak{p}$ is a [maximal ideal](@entry_id:151331) in $R_\mathfrak{p}$. But $R_\mathfrak{p}$ is a local ring with a unique [maximal ideal](@entry_id:151331), $\mathfrak{p}R_\mathfrak{p}$. Therefore, we must have $\mathfrak{M} \cap R_\mathfrak{p} = \mathfrak{p}R_\mathfrak{p}$, completing the proof.

#### A Concrete Example in Number Theory

Let's see the Lying Over Theorem in action. Consider the ring of integers $\mathbb{Z}$ and the [integral extension](@entry_id:150735) $S = \mathbb{Z}[\omega]$, where $\omega = \frac{1+\sqrt{-7}}{2}$ [@problem_id:1836419]. Let's take the prime ideal $\mathfrak{p} = (11)$ in $\mathbb{Z}$. The theorem guarantees that at least one prime ideal of $S$ lies over $(11)$. In algebraic number theory, we can find these ideals by factoring the [minimal polynomial](@entry_id:153598) of $\omega$, which is $x^2 - x + 2 = 0$, modulo $11$.
$$x^2 - x + 2 \equiv (x-5)(x-7) \pmod{11}.$$
This factorization tells us that the ideal $(11)$ splits into two distinct [prime ideals](@entry_id:154026) in $S$. A more direct calculation shows that $(2+\sqrt{-7})(2-\sqrt{-7}) = 4 - (-7) = 11$. This implies that the principal ideals $Q_1 = (2+\sqrt{-7})$ and $Q_2 = (2-\sqrt{-7})$ both divide the ideal $(11)S$. One can verify that these are distinct [prime ideals](@entry_id:154026) and that their contraction to $\mathbb{Z}$ is precisely $(11)$. For example, if an integer $n \in Q_1$, then $n = (2+\sqrt{-7})(a+b\omega)$ for some $a,b \in \mathbb{Z}$. Taking the norm gives $n^2 = N(n) = N(2+\sqrt{-7})N(a+b\omega) = 11 \cdot N(a+b\omega)$, which implies that $11$ must divide $n^2$, and thus $11$ divides $n$. Hence, $Q_1 \cap \mathbb{Z} = (11)$.

### Consequences of Integrality

The structural connection established by the Lying Over Theorem has several important corollaries that describe how properties of ideals are preserved or reflected in [integral extensions](@entry_id:149214).

#### Preservation of Maximality

One of the most direct consequences concerns [maximal ideals](@entry_id:151370). The same lemma used to prove Lying Over gives us a stronger result about the "fibers" over [maximal ideals](@entry_id:151370) [@problem_id:1836438].

**Theorem:** Let $R \subseteq S$ be an [integral extension](@entry_id:150735). A [prime ideal](@entry_id:149360) $\mathfrak{q}$ of $S$ is maximal if and only if its contraction $\mathfrak{p} = \mathfrak{q} \cap R$ is maximal in $R$.

*Proof:*
($\Rightarrow$) Suppose $\mathfrak{q}$ is maximal in $S$. Then $S/\mathfrak{q}$ is a field. The extension $R/\mathfrak{p} \subseteq S/\mathfrak{q}$ is an [integral extension](@entry_id:150735) of [integral domains](@entry_id:155321). Since $S/\mathfrak{q}$ is a field, our key lemma implies that $R/\mathfrak{p}$ must also be a field. Therefore, $\mathfrak{p}$ is a [maximal ideal](@entry_id:151331) in $R$.

($\Leftarrow$) Suppose $\mathfrak{p}$ is maximal in $R$. Then $R/\mathfrak{p}$ is a field. Consider an element $\bar{s} \neq 0$ in the integral domain $S/\mathfrak{q}$. Since $S/\mathfrak{q}$ is integral over the field $R/\mathfrak{p}$, $\bar{s}$ is algebraic over $R/\mathfrak{p}$. It is a standard result from field theory that if an [integral domain](@entry_id:147487) is algebraic over a field, it is itself a field. Thus, $S/\mathfrak{q}$ is a field, which means $\mathfrak{q}$ is a [maximal ideal](@entry_id:151331) in $S$.

#### Behavior with Respect to Quotients

The Lying Over property is compatible with taking quotients. Suppose we have an ideal $I \subseteq R$ and consider the [quotient rings](@entry_id:148632) $\bar{R} = R/I$ and $\bar{S} = S/IS$. The extension $\bar{R} \subseteq \bar{S}$ is also integral. The prime ideals of $\bar{R}$ are of the form $\mathfrak{p}/I$ for primes $\mathfrak{p} \subseteq R$ containing $I$. Similarly, primes of $\bar{S}$ are of the form $\mathfrak{q}/IS$ for primes $\mathfrak{q} \subseteq S$ containing $IS$.

A prime ideal $\mathfrak{q}/IS$ lies over $\mathfrak{p}/I$ if and only if $(\mathfrak{q}/IS) \cap (R/I) = \mathfrak{p}/I$. This condition is equivalent to $\mathfrak{q} \cap R = \mathfrak{p}$ [@problem_id:1836455]. Therefore, finding a prime in $S$ lying over $\mathfrak{p}$ (and containing $IS$) is the same as finding a prime in the quotient $S/IS$ lying over $\mathfrak{p}/I$. This correspondence is extremely useful, as it allows us to reduce problems about chains of ideals to a simpler case by modding out by the lowest ideal in the chain.

### The Going Up Theorem: Lifting Chains of Ideals

The Lying Over Theorem guarantees that the map $\mathrm{Spec}(S) \to \mathrm{Spec}(R)$ is surjective. But what can we say about ascending chains of prime ideals? If we have a chain $\mathfrak{p}_0 \subsetneq \mathfrak{p}_1$ in $R$ and a prime $\mathfrak{q}_0$ in $S$ lying over $\mathfrak{p}_0$, can we find a prime $\mathfrak{q}_1$ in $S$ that lies over $\mathfrak{p}_1$ and also satisfies $\mathfrak{q}_0 \subsetneq \mathfrak{q}_1$? The affirmative answer is given by the Going Up Theorem.

**The Going Up Theorem:** Let $R \subseteq S$ be an [integral extension](@entry_id:150735). Let $\mathfrak{p}_0 \subsetneq \mathfrak{p}_1 \subsetneq \dots \subsetneq \mathfrak{p}_n$ be a chain of prime ideals in $R$, and let $\mathfrak{q}_0$ be a prime ideal in $S$ such that $\mathfrak{q}_0 \cap R = \mathfrak{p}_0$. Then there exists a chain of prime ideals $\mathfrak{q}_0 \subsetneq \mathfrak{q}_1 \subsetneq \dots \subsetneq \mathfrak{q}_n$ in $S$ such that $\mathfrak{q}_i \cap R = \mathfrak{p}_i$ for all $i=0, \dots, n$.

The proof proceeds by induction, reducing the problem at each step to a Lying Over problem in a [quotient ring](@entry_id:155460), leveraging the principle discussed previously. For the step from $\mathfrak{p}_0$ to $\mathfrak{p}_1$, one considers the [integral extension](@entry_id:150735) $R/\mathfrak{p}_0 \subseteq S/\mathfrak{q}_0$ and applies the Lying Over Theorem to the prime ideal $\mathfrak{p}_1/\mathfrak{p}_0$.

#### A Major Application: Krull Dimension

The Going Up Theorem has a profound consequence for the **Krull dimension** of a ring, which is defined as the supremum of lengths of chains of prime ideals. For an [integral extension](@entry_id:150735) of [integral domains](@entry_id:155321), the Krull dimension is preserved [@problem_id:1836447].

**Theorem:** Let $R \subseteq S$ be an [integral extension](@entry_id:150735) of [integral domains](@entry_id:155321). Then $\dim(R) = \dim(S)$.

The proof is a beautiful combination of two properties:

1.  **Incomparability:** If $\mathfrak{q}_0 \subsetneq \mathfrak{q}_1$ are two [prime ideals](@entry_id:154026) in $S$, then their contractions are also strictly ordered: $\mathfrak{q}_0 \cap R \subsetneq \mathfrak{q}_1 \cap R$. (This is proven by localizing and using Nakayama's Lemma). This property immediately implies that any chain of primes in $S$ contracts to a chain of the same length in $R$. Therefore, $\dim(S) \le \dim(R)$.

2.  **Going Up:** Conversely, let $\mathfrak{p}_0 \subsetneq \mathfrak{p}_1 \subsetneq \dots \subsetneq \mathfrak{p}_n$ be any chain of [prime ideals](@entry_id:154026) in $R$. By the Lying Over Theorem, there exists a prime $\mathfrak{q}_0$ lying over $\mathfrak{p}_0$. By the Going Up Theorem, we can lift the entire chain to a chain $\mathfrak{q}_0 \subsetneq \mathfrak{q}_1 \subsetneq \dots \subsetneq \mathfrak{q}_n$ in $S$. This guarantees that for any chain in $R$, we can find a chain of at least the same length in $S$. Therefore, $\dim(R) \le \dim(S)$.

Combining these two inequalities gives the remarkable result that $\dim(R) = \dim(S)$. Geometrically, this means that an [integral extension](@entry_id:150735) cannot "squash" the dimension of the prime spectrum.

### A Look Ahead: The Failure of Going Down

Having established theorems for "lying over" and "going up," a natural question is whether a "going down" property holds. That is, given a chain $\mathfrak{p}_1 \subsetneq \mathfrak{p}_0$ in $R$ and a prime $\mathfrak{q}_0$ lying over $\mathfrak{p}_0$, can we always find a prime $\mathfrak{q}_1 \subsetneq \mathfrak{q}_0$ in $S$ that lies over $\mathfrak{p}_1$?

Perhaps surprisingly, the answer is no. Integrality alone is not sufficient to guarantee the Going Down property. A famous counterexample illustrates this failure [@problem_id:1836428]. Let $k$ be a field, and consider the subring $A = k[x^2, xy]$ of the polynomial ring $B = k[x,y]$. The extension $A \subseteq B$ is integral. Now, consider the chain of prime ideals $p_2 = (xy) \subsetneq p_1 = (x^2, xy)$ in $A$. Let's choose the [prime ideal](@entry_id:149360) $P_1 = (x, y-1)$ in $B$. One can verify that its contraction is $P_1 \cap A = (x^2, xy) = p_1$. The Going Down property would ask for a [prime ideal](@entry_id:149360) $P_2 \subset P_1$ in $B$ that contracts to $p_2 = (xy)$. However, a careful analysis shows that no such [prime ideal](@entry_id:149360) $P_2$ exists. Any prime $P_2$ contracting to $(xy)$ must contain the element $xy$ but not $x^2$. This forces $y \in P_2$. But if $y \in P_2$, then for the inclusion $P_2 \subset P_1 = (x, y-1)$ to hold, we would need $y \in (x, y-1)$, which is impossible since $y \equiv 1 \pmod{(x, y-1)}$.

This counterexample demonstrates that for the Going Down property to hold, we need stronger hypotheses, typically involving the ring $R$ being integrally closed in its [field of fractions](@entry_id:148415). This sets the stage for a deeper exploration of the landscape of [commutative ring](@entry_id:148075) extensions.