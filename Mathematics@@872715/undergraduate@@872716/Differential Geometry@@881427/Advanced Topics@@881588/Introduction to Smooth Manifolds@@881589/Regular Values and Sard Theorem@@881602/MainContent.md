## Introduction
In [differential geometry](@entry_id:145818), an understanding of the structure of [smooth maps between manifolds](@entry_id:190665) is paramount. A fundamental question arises when we consider the solution sets of equations: when does an equation like $F(x) = c$ define a "nice" geometric object, such as a smooth curve or surface, and when does it result in singularities like corners or self-intersections? The theory of [regular values](@entry_id:161151) and Sard's theorem provides the definitive answer, offering powerful tools to classify the behavior of [smooth maps](@entry_id:203730) and the structure of their [level sets](@entry_id:151155).

This article provides a comprehensive exploration of these foundational concepts. We will begin in the **Principles and Mechanisms** chapter by defining critical points, regular points, and their corresponding values, culminating in the statement of the Regular Value Theorem and Sard's Theorem. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate the remarkable utility of this theory, showing how it provides deep insights into geometry, topology, linear algebra, and even the stability of physical systems. Finally, to solidify your understanding, the **Hands-On Practices** section offers guided problems that move from basic calculations to applications on curved manifolds.

## Principles and Mechanisms

In the study of smooth manifolds, our primary objects of interest are [smooth maps](@entry_id:203730) between them. To understand the geometric structure of these maps and the manifolds they relate, we must develop tools to analyze their local and global behavior. This chapter introduces a fundamental classification scheme for points in both the domain and [codomain](@entry_id:139336) of a [smooth map](@entry_id:160364), culminating in one of the most powerful results in [differential topology](@entry_id:157662): Sard's Theorem. This framework allows us to understand when the solutions to a system of equations form a well-behaved geometric object, a concept with far-reaching implications across mathematics and the sciences.

### The Differential and Local Behavior

The central analytical tool for studying a [smooth map](@entry_id:160364) $F: M \to N$ between two manifolds is its **differential**. At each point $p \in M$, the differential of $F$ at $p$, denoted $dF_p$, is a [linear map](@entry_id:201112) between the tangent spaces $dF_p: T_pM \to T_{F(p)}N$. It represents the [best linear approximation](@entry_id:164642) of the map $F$ in the vicinity of $p$. The properties of this linear map dictate the local behavior of $F$.

For maps between Euclidean spaces, the differential has a familiar [matrix representation](@entry_id:143451).

- If $f: \mathbb{R}^m \to \mathbb{R}$ is a [smooth function](@entry_id:158037), its differential at a point $p \in \mathbb{R}^m$ is a linear functional $df_p: \mathbb{R}^m \to \mathbb{R}$ represented by the gradient vector $\nabla f(p)$. The action of the differential on a tangent vector $v \in T_p\mathbb{R}^m \cong \mathbb{R}^m$ is given by the dot product: $df_p(v) = \nabla f(p) \cdot v$.

- More generally, for a [smooth map](@entry_id:160364) $F: \mathbb{R}^m \to \mathbb{R}^n$, the differential $dF_p: \mathbb{R}^m \to \mathbb{R}^n$ is represented by the $n \times m$ **Jacobian matrix**, $J_F(p)$, whose entries are the [partial derivatives](@entry_id:146280) of the component functions of $F$. The action on a vector $v \in \mathbb{R}^m$ is given by matrix multiplication: $dF_p(v) = J_F(p)v$.

Understanding the properties of this [linear map](@entry_id:201112), specifically its rank, is the key to classifying points and understanding the structure of the map $F$.

### Critical Points and Regular Points: A Fundamental Dichotomy

The behavior of the differential allows us to partition the domain of a [smooth map](@entry_id:160364) into two fundamental types of points. A point $p \in M$ is called a **critical point** of a [smooth map](@entry_id:160364) $F: M \to N$ if the differential $dF_p: T_pM \to T_{F(p)}N$ is **not surjective** (i.e., its image does not cover the entire [codomain](@entry_id:139336) [tangent space](@entry_id:141028) $T_{F(p)}N$). If $dF_p$ is surjective, the point $p$ is called a **regular point**.

This definition's meaning depends critically on the relative dimensions of the domain and codomain.

**Case 1: Maps to $\mathbb{R}$ (codimension one)**

For a map $f: M \to \mathbb{R}$, the [codomain](@entry_id:139336) [tangent space](@entry_id:141028) is $T_{f(p)}\mathbb{R} \cong \mathbb{R}$, which is one-dimensional. A linear map to a one-dimensional space is surjective if and only if it is not the zero map. Therefore, for such functions, a point $p$ is a critical point if and only if $d f_p$ is the zero map. For a function on Euclidean space, this is equivalent to its gradient vanishing.

For instance, consider the [smooth function](@entry_id:158037) $f: \mathbb{R}^3 \to \mathbb{R}$ defined by $f(x,y,z) = x^2 + y^2$. The Jacobian of this map is the row vector $[2x, 2y, 0]$. This matrix represents the zero map if and only if $2x=0$ and $2y=0$. The variable $z$ can be any real number. Consequently, the set of critical points is the entire $z$-axis, i.e., the set $\{(0,0,z) \mid z \in \mathbb{R}\}$ [@problem_id:1660404]. Similarly, for the function $g: \mathbb{R}^2 \to \mathbb{R}$ given by $g(x,y) = x^2 + xy$, the gradient is $\nabla g = (2x+y, x)$. This vector is zero only when $x=0$ and subsequently $y=0$. Thus, the origin $(0,0)$ is the unique critical point of $g$ [@problem_id:1660411].

**Case 2: Dimension of Domain is less than Dimension of Codomain ($\dim M  \dim N$)**

Let $F: M \to N$ be a [smooth map](@entry_id:160364) where $\dim M = m  n = \dim N$. The differential $dF_p$ is a [linear map](@entry_id:201112) from an $m$-dimensional vector space to an $n$-dimensional one. By the [rank-nullity theorem](@entry_id:154441), the dimension of the image of $dF_p$ (its rank) cannot exceed the dimension of its domain. That is, $\text{rank}(dF_p) \le m$. Since $m  n$, the image of $dF_p$ can never be the entire $n$-dimensional tangent space $T_{F(p)}N$. Therefore, the differential $dF_p$ is **never surjective**.

This has a striking consequence: for any [smooth map](@entry_id:160364) from a lower-dimensional manifold to a higher-dimensional one, **every point in the domain is a critical point**. This observation is crucial for an important application of Sard's theorem discussed later [@problem_id:1660418].

A related concept arises for curves, i.e., maps from $\mathbb{R}$ to $\mathbb{R}^n$. For a map $f: \mathbb{R} \to \mathbb{R}^n$, the differential is represented by the velocity vector $f'(t) \in \mathbb{R}^n$. While all points are critical by the [surjectivity](@entry_id:148931) definition (since $1  n$ for $n \ge 2$), it is common to refine the terminology. We say a point $t_0$ is a critical point if the [rank of the differential](@entry_id:635728) is not maximal. For a map from $\mathbb{R}$, the maximal rank is 1. Thus, $t_0$ is critical if $\text{rank}(df_{t_0})  1$, which means $df_{t_0}$ is the zero map, or $f'(t_0) = 0$. For the classic cuspidal cubic curve $f(t) = (t^2, t^3)$, the derivative is $f'(t) = (2t, 3t^2)$. This vector is zero if and only if $t=0$. Thus, $t=0$ is the unique critical point in this sense, and it corresponds to the geometric singularity (a cusp) at the origin in the image curve [@problem_id:1660414].

**Case 3: Dimension of Domain equals Dimension of Codomain ($\dim M = \dim N$)**

If $F: M \to N$ is a [smooth map](@entry_id:160364) between manifolds of the same dimension, the differential $dF_p$ is a linear map between [vector spaces](@entry_id:136837) of equal dimension. From linear algebra, such a map is surjective if and only if it is injective, which is equivalent to it being an [isomorphism](@entry_id:137127). For maps between Euclidean spaces, this is equivalent to the Jacobian matrix being invertible, or its determinant being non-zero. Therefore, for maps $F: \mathbb{R}^n \to \mathbb{R}^n$, a point $p$ is critical if and only if the determinant of the Jacobian matrix at $p$ is zero, i.e., $\det(J_F(p)) = 0$.

For example, consider a map $F$ from a 2-torus $T^2$ to a 2-sphere $S^2$. A point $(\theta, \phi)$ on the torus is a critical point if the Jacobian determinant of the map, expressed in [local coordinates](@entry_id:181200), is zero. For the map given by $\psi = \pi\sin^2(\theta)$ and $\xi = \phi + 2\sin(\theta)$, the Jacobian determinant is $\pi\sin(2\theta)$. This determinant is zero when $\theta$ is a multiple of $\pi/2$. These are precisely the [critical points](@entry_id:144653) of the map on the torus [@problem_id:1660399].

### Regular Values and the Structure of Level Sets

The classification of points in the domain naturally leads to a classification of values in the codomain. A value $c \in N$ is called a **critical value** if it is the image of at least one critical point. That is, the set of critical values is the image of the set of [critical points](@entry_id:144653). Any value $c \in N$ that is not a critical value is called a **[regular value](@entry_id:188218)**. An equivalent and often more useful definition of a [regular value](@entry_id:188218) is a value $c \in N$ such that for every point $p$ in its preimage $F^{-1}(c)$, $p$ is a regular point. Note that if the [preimage](@entry_id:150899) $F^{-1}(c)$ is empty, $c$ is vacuously a [regular value](@entry_id:188218).

The distinction between regular and critical values is of paramount importance due to the **Regular Value Theorem** (also known as the Regular Level Set Theorem).

**Theorem (Regular Value Theorem):** Let $F: M \to N$ be a [smooth map](@entry_id:160364) between [smooth manifolds](@entry_id:160799), and let $c \in N$ be a [regular value](@entry_id:188218) of $F$. Then the preimage (or [level set](@entry_id:637056)) $F^{-1}(c)$ is a smooth submanifold of $M$ with dimension $\dim(F^{-1}(c)) = \dim M - \dim N$.

This theorem provides the rigorous justification for defining smooth geometric objects (curves, surfaces, etc.) as solution sets of equations. As long as the value on the right-hand side of the equation $F(p)=c$ is regular, the [solution set](@entry_id:154326) is guaranteed to be a smooth manifold.

Let's examine this theorem through examples:
- Consider the function $f(x,y,z) = x^2 + y^2 - z^2$. Its gradient $\nabla f = (2x, 2y, -2z)$ vanishes only at the origin $(0,0,0)$. The image of this single critical point is $f(0,0,0) = 0$. Thus, $c=0$ is the only critical value. By the Regular Value Theorem, for any $c \neq 0$, the [level set](@entry_id:637056) $f^{-1}(c)$ defined by the equation $x^2 + y^2 - z^2 = c$ is a smooth 2-dimensional submanifold (a surface) in $\mathbb{R}^3$. Geometrically, for $c > 0$, these are hyperboloids of one sheet, and for $c  0$, they are hyperboloids of two sheets. For the critical value $c=0$, the [level set](@entry_id:637056) $x^2+y^2-z^2=0$ is a double cone, which is not a smooth manifold at the origin—precisely the location of the critical point in its preimage [@problem_id:1660412].

- Consider the function $f(x,y) = y^2 - x^3 + 6x^2 - 12x + 13$. To find which level sets might not be smooth curves, we search for critical values. The gradient is $\nabla f = (-3(x-2)^2, 2y)$. This vanishes only at the point $(2,0)$. The corresponding critical value is $c = f(2,0) = 5$. Therefore, $c=5$ is the only value for which the [level set](@entry_id:637056) $f^{-1}(c)$ is not guaranteed to be a smooth curve. For any other value $c \neq 5$, the level set is a smooth 1-dimensional manifold in $\mathbb{R}^2$ [@problem_id:1660403].

A crucial prerequisite for this entire framework is the smoothness of the map. The Regular Value Theorem relies on the existence of the differential at every point. If a function is not smooth, the theorem cannot be applied. For example, the function $f(x,y) = |x|$ is not differentiable along the line $x=0$. Therefore, it is not a [smooth map](@entry_id:160364) on $\mathbb{R}^2$. We cannot use the Regular Value Theorem to analyze its level sets, such as $f^{-1}(1)$, even though that particular [level set](@entry_id:637056) happens to be a smooth manifold (the union of two vertical lines) [@problem_id:1660384].

### Sard's Theorem: The Scarcity of Critical Values

The Regular Value Theorem is a powerful tool, but its utility depends on the existence of [regular values](@entry_id:161151). Are [regular values](@entry_id:161151) common or rare? A remarkable result by Arthur Sard provides a definitive answer.

**Theorem (Sard's Theorem):** For any [smooth map](@entry_id:160364) $F: M \to N$ between smooth manifolds, the set of critical values of $F$ has **Lebesgue measure zero** in $N$.

Intuitively, a set of measure zero is "small." In $\mathbb{R}$, a set has [measure zero](@entry_id:137864) if it can be covered by a countable collection of intervals whose total length is arbitrarily small. Countable sets of points are examples. In $\mathbb{R}^2$, a set has [measure zero](@entry_id:137864) if it can be covered by a countable collection of rectangles of arbitrarily small total area. Any smooth curve is an example.

Sard's Theorem tells us that critical values are exceptional. If the [codomain](@entry_id:139336) $N$ has positive measure (such as $\mathbb{R}^n$ itself), the set of critical values cannot be all of $N$. This implies that **[regular values](@entry_id:161151) are abundant**; in fact, "almost every" point in the [codomain](@entry_id:139336) is a [regular value](@entry_id:188218). This ensures that the Regular Value Theorem is a widely applicable and not an empty statement.

Let's explore two profound consequences of Sard's Theorem.

First, consider any [smooth function](@entry_id:158037) on a compact manifold, such as $f: S^2 \to \mathbb{R}$. The Extreme Value Theorem guarantees that $f$ must attain a maximum and a minimum, and these are necessarily [critical points](@entry_id:144653). Thus, the set of critical values is non-empty. However, Sard's Theorem asserts that this set of critical values has [measure zero](@entry_id:137864) in $\mathbb{R}$. A [set of measure zero](@entry_id:198215) cannot be the entire real line. This provides a deep and general reason why not every real number can be a critical value of such a map, a reason that is more fundamental than simply observing that the image of a compact set must be bounded [@problem_id:1660388].

Second, recall our analysis of maps from lower to higher dimensions, like a [smooth map](@entry_id:160364) $f: \mathbb{R} \to \mathbb{R}^2$. We established that for such a map, *every* point in the domain is a critical point. This means the set of critical values is precisely the entire image of the map, $f(\mathbb{R})$. According to Sard's Theorem, this set of critical values must have [measure zero](@entry_id:137864) in the codomain $\mathbb{R}^2$. Therefore, the image of any [smooth map](@entry_id:160364) from $\mathbb{R}$ to $\mathbb{R}^2$ must be a set of area zero. A smooth curve can be intricate, but it can never "fill" a region of the plane [@problem_id:1660418].

This result highlights the importance of the smoothness condition in Sard's Theorem. There exist continuous, surjective maps from the interval $[0,1]$ to the square $[0,1]^2$, known as [space-filling curves](@entry_id:161184). The image of such a curve is the entire square, which has an area of 1, not zero. This seems to contradict our conclusion. However, there is no contradiction because these [space-filling curves](@entry_id:161184) are famously continuous but **not differentiable**, and therefore not smooth. Sard's Theorem simply does not apply to them, demonstrating the sharpness of its hypotheses [@problem_id:1660366].

In summary, the concepts of [critical points](@entry_id:144653) and [regular values](@entry_id:161151), governed by the properties of the differential, allow us to probe the structure of [smooth maps](@entry_id:203730). The Regular Value Theorem connects this analytic classification to the geometric properties of level sets, while Sard's Theorem guarantees that the "well-behaved" case (preimages of [regular values](@entry_id:161151)) is the generic one, making this a robust and powerful theory.