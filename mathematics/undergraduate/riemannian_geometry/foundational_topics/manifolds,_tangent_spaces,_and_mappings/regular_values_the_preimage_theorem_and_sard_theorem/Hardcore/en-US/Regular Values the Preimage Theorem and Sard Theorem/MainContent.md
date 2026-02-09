## Introduction
How do we describe complex shapes in mathematics? Often, they arise as the solution sets to equations. In the language of differential geometry, these solution sets are known as the level sets or preimages of a smooth map. A central question is: when is such a set a well-behaved geometric object, a "smooth manifold," rather than a complicated, singular space? This article addresses this fundamental problem by exploring a powerful trio of theorems that provide a clear and practical answer.

This article is structured to build your understanding from foundational principles to powerful applications.
- **Chapter 1: Principles and Mechanisms** will introduce the core concepts, starting with the local picture via the Implicit Function Theorem and expanding to the global setting of manifolds with the Preimage Theorem and the crucial genericity result of Sard's Theorem.
- **Chapter 2: Applications and Interdisciplinary Connections** will demonstrate how these theorems are not just abstract theory but active tools used to construct manifolds, probe topology through Morse theory, define invariants like degree, and establish the generic nature of geometric intersections via transversality.
- **Chapter 3: Hands-On Practices** will provide a series of guided problems, allowing you to apply these concepts to concrete examples and solidify your intuition.

By navigating these chapters, you will gain a robust understanding of how differential topology provides rigorous methods for identifying and analyzing the elegant structures hidden within the solutions to systems of equations.

## Principles and Mechanisms

The preceding chapter introduced the fundamental concepts of smooth manifolds and maps between them. We now turn to a central question in differential topology: given a smooth map $f \colon M \to N$, what can be said about the structure of its **level sets**, which are the preimages of points in the codomain, $f^{-1}(y)$? While for an arbitrary map this set can be a pathologically complex object, a powerful collection of theorems reveals that under a common and easily verifiable condition, these level sets are themselves well-behaved smooth manifolds. This chapter will develop the three pillars of this theory: the Implicit Function Theorem, the Preimage Theorem, and Sard's Theorem.

### The Local Picture: Regularity and the Implicit Function Theorem

Our inquiry begins in the familiar setting of Euclidean space. Let $F \colon \mathbb{R}^n \to \mathbb{R}^k$ be a continuously differentiable map, and consider the level set defined by the equation $F(x) = y$ for some fixed $y \in \mathbb{R}^k$. The key to understanding the local geometry of this level set lies in the behavior of the derivative of $F$, the $k \times n$ Jacobian matrix $DF_x$.

The crucial condition is that of **full rank**. We say the derivative $DF_{x_0}$ at a point $x_0$ has full rank if its rank is equal to the dimension of the codomain, $\operatorname{rank}(DF_{x_0}) = k$. This is equivalent to stating that the linear transformation $DF_{x_0} \colon \mathbb{R}^n \to \mathbb{R}^k$ is **surjective**. The **Implicit Function Theorem** is the definitive statement about the structure of a level set near such a point.

**Theorem (Implicit Function Theorem).** Let $F \colon \mathbb{R}^n \to \mathbb{R}^k$ be a $C^r$ map (for $r \ge 1$), and let $x_0 \in \mathbb{R}^n$ be a point such that $F(x_0) = y$. If the derivative $DF_{x_0}$ is surjective, then the level set $F^{-1}(y)$ is locally a $C^r$ submanifold of $\mathbb{R}^n$ of dimension $n-k$.

More explicitly, the surjectivity of the $k \times n$ Jacobian matrix $DF_{x_0}$ implies that some $k$ of its columns are linearly independent. After a possible reordering of the coordinates of $\mathbb{R}^n$ to $(u_1, \dots, u_{n-k}, v_1, \dots, v_k)$, we can assume that the $k \times k$ submatrix of partial derivatives with respect to the $v$ variables is invertible at $x_0 = (u_0, v_0)$. The theorem then guarantees the existence of open neighborhoods $U \subset \mathbb{R}^{n-k}$ of $u_0$ and $V \subset \mathbb{R}^k$ of $v_0$, and a unique $C^r$ map $g \colon U \to V$, such that within the neighborhood $U \times V$, the level set $F^{-1}(y)$ is precisely the graph of $g$:
$$ F^{-1}(y) \cap (U \times V) = \{ (u, g(u)) \mid u \in U \} $$
This local graph representation is the heart of the theorem [@problem_id:3062796]. Since the graph of a $C^r$ function defined on an open set of $\mathbb{R}^{n-k}$ is a $C^r$ submanifold of dimension $n-k$, the theorem establishes the desired geometric structure for the level set.

Furthermore, we can precisely identify the tangent space to this submanifold. A tangent vector to the level set at $x_0$ is the velocity vector $\gamma'(0)$ of a curve $\gamma(t)$ that lies in the level set and passes through $x_0$ at $t=0$. Since $F(\gamma(t)) = y$ for all $t$, the chain rule implies $DF_{x_0}(\gamma'(0)) = 0$. This means any tangent vector to the level set must lie in the kernel of the derivative, $T_{x_0}(F^{-1}(y)) \subseteq \ker(DF_{x_0})$. The dimension of the submanifold is $n-k$. By the **Rank-Nullity Theorem** from linear algebra, the dimension of the kernel of the surjective map $DF_{x_0}$ is also $\dim(\mathbb{R}^n) - \operatorname{rank}(DF_{x_0}) = n-k$. Since the two vector spaces have the same dimension, we must have equality:
$$ T_{x_0}(F^{-1}(y)) = \ker(DF_{x_0}) $$
This provides a complete and powerful justification for the dimension of the level set [@problem_id:3062848].

### From Local to Global: The Preimage Theorem

The Implicit Function Theorem provides the blueprint for understanding level sets on general manifolds. By working in local charts, we can translate the problem from manifolds back to Euclidean space.

Let $f \colon M \to N$ be a smooth map between smooth manifolds of dimensions $m$ and $n$, respectively. For any point $p \in M$, the **differential** of $f$ at $p$ is the linear map $df_p \colon T_p M \to T_{f(p)} N$. In local coordinates, this map is represented by the Jacobian matrix of the coordinate representation of $f$. A fundamental property is that the **rank** of $df_p$, defined as the dimension of its image, is an intrinsic property that does not depend on the choice of local coordinates. A change of charts corresponds to multiplying the Jacobian matrix on the left and right by invertible matrices (the Jacobians of the transition maps), an operation which preserves rank [@problem_id:3062821].

This allows us to define regularity in a chart-independent way.
*   A point $p \in M$ is a **regular point** of $f$ if the differential $df_p$ is surjective. This is equivalent to $\operatorname{rank}(df_p) = n$, the dimension of the target manifold $N$.
*   A point $p \in M$ is a **critical point** of $f$ if it is not a regular point, i.e., if $df_p$ is not surjective, or $\operatorname{rank}(df_p)  n$.

Based on these definitions for points in the domain, we classify values in the codomain:
*   A value $y \in N$ is a **critical value** if it is the image of at least one critical point.
*   A value $y \in N$ is a **regular value** if it is not a critical value. This means that for every point $p$ in the preimage $f^{-1}(y)$, the point $p$ is a regular point of $f$. It is important to note that if a value $y$ is not in the image of $f$ at all, its preimage $f^{-1}(y)$ is empty. In this case, the condition is vacuously satisfied, and $y$ is automatically a regular value [@problem_id:3062884].

The distinction between these concepts is crucial. A value $y$ being critical requires only *one* of its preimages to be a critical point; for $y$ to be regular, *all* of its preimages must be regular points [@problem_id:3062884].

We can now state the global version of the Implicit Function Theorem, known as the **Preimage Theorem** or **Regular Value Theorem**.

**Theorem (Preimage Theorem).** Let $f \colon M^m \to N^n$ be a smooth map. If $y \in N$ is a regular value of $f$, then the preimage $f^{-1}(y)$ is a properly embedded smooth submanifold of $M$ of dimension $m-n$ [@problem_id:3062868].

The proof of this theorem proceeds by applying the Implicit Function Theorem in local charts around each point $p \in f^{-1}(y)$. The condition that $y$ is a regular value guarantees that the hypothesis of the Implicit Function Theorem (surjectivity of the derivative) is met at every point of the level set. These local graph representations can then be patched together to show that the entire level set $f^{-1}(y)$ is a submanifold. The dimension of this submanifold is, as before, determined by the Rank-Nullity Theorem:
$$ \dim(f^{-1}(y)) = \dim(T_p(f^{-1}(y))) = \dim(\ker(df_p)) = \dim(T_p M) - \operatorname{rank}(df_p) = m - n $$
This result is remarkably powerful. It allows us to construct submanifolds simply by finding regular values of smooth maps. For example, the unit sphere $S^{n-1} \subset \mathbb{R}^n$ can be viewed as the preimage of the regular value $1$ for the smooth map $F \colon \mathbb{R}^n \to \mathbb{R}$ given by $F(x) = \|x\|^2$.

### The Power of Genericity: Sard's Theorem

The Preimage Theorem provides a powerful machine for constructing submanifolds, but its usefulness hinges on a crucial question: how common are regular values? If regular values were rare or pathologically difficult to find, the theorem would be of limited practical use. The answer is provided by another landmark result, **Sard's Theorem**, which asserts that regular values are, in fact, the norm.

To state the theorem, we first need a notion of "size" for subsets of a manifold. A subset $A \subset N$ is said to have **measure zero** if for any chart $(U, \phi)$ in an atlas for $N$, the coordinate image $\phi(A \cap U) \subset \mathbb{R}^n$ has Lebesgue measure zero. This definition is robust; it does not depend on the choice of atlas because transition maps are diffeomorphisms, which map sets of measure zero to sets of measure zero [@problem_id:3062795].

**Theorem (Sard's Theorem).** Let $f \colon M \to N$ be a smooth map between smooth manifolds. The set of critical values of $f$ has measure zero in $N$.

The implications of this theorem are profound. It means that the "bad" values—the critical ones whose preimages might not be manifolds—form a negligible set. Conversely, the "good" values—the regular ones—are abundant. The set of regular values, being the complement of a measure-zero set, has **full measure** and is **dense** in the codomain $N$ [@problem_id:3062808]. This means that for any point in the target manifold, there are regular values arbitrarily close to it. In colloquial terms, Sard's theorem tells us that "almost every" value is a regular value.

This has a powerful philosophical and practical consequence: we can often prove the existence of a desired geometric object (like a particular kind of submanifold) by showing that it can be realized as the preimage of a regular value of some map. Sard's theorem guarantees that we will have a plentiful supply of such values to work with.

A simple but important corollary is that any set of measure zero must have an empty interior. Therefore, Sard's theorem implies that the set of critical values of a smooth map cannot contain any open set [@problem_id:3062808].

### Clarifications and Applications

To solidify these abstract principles, we examine them through a canonical example and clarify some common points of confusion.

#### Illustrative Example: The Height Function on the Sphere

Consider the unit $2$-sphere $S^2 \subset \mathbb{R}^3$ and the smooth map $h \colon S^2 \to \mathbb{R}$ defined by projecting onto the third coordinate: $h(x_1, x_2, x_3) = x_3$. This is often called the **height function**.

1.  **Critical Points and Values:** A point $p \in S^2$ is critical if $dh_p \colon T_pS^2 \to \mathbb{R}$ is the zero map. The tangent plane $T_pS^2$ is horizontal (i.e., all its tangent vectors have a zero third component) only at the North Pole $(0,0,1)$ and the South Pole $(0,0,-1)$. These are the only two critical points. The critical values are the images of these points: $h(0,0,1) = 1$ and $h(0,0,-1) = -1$. The set of critical values is $\{-1, 1\}$, a finite set which, as Sard's Theorem predicts, has measure zero in $\mathbb{R}$.

2.  **Regular Values and Preimages:** Any value $y \in (-1, 1)$ is a regular value. By the Preimage Theorem, the level set $h^{-1}(y)$ must be a smooth submanifold of $S^2$ of dimension $\dim(S^2) - \dim(\mathbb{R}) = 2-1=1$. Indeed, the preimage $h^{-1}(y)$ is the set of points $(x_1, x_2, y)$ such that $x_1^2 + x_2^2 + y^2 = 1$, which defines a circle of radius $\sqrt{1-y^2}$ at height $y$. This circle is a "circle of latitude" and is diffeomorphic to $S^1$, confirming the theorem's conclusion [@problem_id:3062802]. For any $|y|  1$, the preimage is empty, and $y$ is also a regular value.

This single example beautifully illustrates the entire logical chain: we identify critical points, find the measure-zero set of critical values, and then use the Preimage Theorem to describe the geometry of the level sets for the abundant regular values [@problem_id:3062802].

#### Common Misconceptions and Subtleties

**Critical Points vs. Critical Values.** A frequent error is to assume that the set of *critical points* must have measure zero. This is false. Sard's theorem concerns the image of this set, not the set itself. Consider two simple counterexamples [@problem_id:3062799]:
1.  The constant map $f \colon M \to N$ given by $f(p) = y_0$ for all $p \in M$. If $\dim N  0$, the differential $df_p$ is the zero map for all $p$, so *every* point in $M$ is a critical point. The set of critical points is $M$ itself, which certainly does not have measure zero. However, the set of critical values is the singleton $\{y_0\}$, which has measure zero in $N$.
2.  An immersion $f \colon M^m \to N^n$ where $m  n$. The differential $df_p$ is always injective, but it can never be surjective, as the dimension of its image is $m$, which is less than $n$. Thus, *every* point in $M$ is again a critical point. The set of critical values is the entire image $f(M)$, which is an $m$-dimensional submanifold in an $n$-dimensional space. A standard result of measure theory is that such a lower-dimensional submanifold has measure zero in the larger ambient space.

In both cases, the set of critical points can be large, but its image, the set of critical values, is small, just as Sard's theorem predicts.

**The Role of Differentiability.** The theorems discussed in this chapter are stated for "smooth" ($C^\infty$) maps. This high degree of regularity is essential for the strongest form of Sard's Theorem. The theorem is sharp; it requires the map $f \colon M^m \to N^n$ to be of class $C^r$ where the regularity $r$ satisfies $r  \max(0, m-n)$. If the regularity is too low, the conclusion can fail. The classic counterexample, constructed by Hassler Whitney, is a $C^1$ function $f \colon \mathbb{R}^2 \to \mathbb{R}$. Here, $m=2$ and $n=1$, so the condition is $r  2-1 = 1$. A $C^1$ map does not satisfy this. Whitney showed that one can construct such a $C^1$ map for which the set of critical values is a non-trivial interval in $\mathbb{R}$, which has positive measure. This demonstrates that the $C^\infty$ or at least $C^2$ assumption is not merely for convenience but is a necessary ingredient for the theorem to hold in this dimensional setting [@problem_id:3062871].