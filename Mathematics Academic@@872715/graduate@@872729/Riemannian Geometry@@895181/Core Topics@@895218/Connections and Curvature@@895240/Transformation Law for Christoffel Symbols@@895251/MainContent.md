## Introduction
In the study of [differential geometry](@entry_id:145818), an [affine connection](@entry_id:160152) provides a coordinate-independent method for differentiating vector fields on a manifold. However, for practical calculations, we must work in [local coordinates](@entry_id:181200), where the connection is represented by a set of functions called the Christoffel symbols. A central, and often subtle, question arises: how do these symbols behave when we change our coordinate system? This article addresses the crucial fact that Christoffel symbols do not transform as tensors, a property that is fundamental to the entire framework of [covariant differentiation](@entry_id:263981).

In the following chapters, you will gain a deep understanding of this topic. First, under "Principles and Mechanisms," we will define the Christoffel symbols and derive their unique transformation law step-by-step, analyzing why the presence of a second-derivative term makes them non-tensorial. Next, in "Applications and Interdisciplinary Connections," we will explore the far-reaching consequences of this law, showing how it is used to define geometry in [curvilinear coordinates](@entry_id:178535) and how it forms the mathematical basis for Einstein's Equivalence Principle in general relativity. Finally, the "Hands-On Practices" section will allow you to apply these principles directly, solidifying your computational skills through guided problems.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of an [affine connection](@entry_id:160152) $\nabla$ as a means of differentiating vector fields on a smooth manifold $M$. This operator provides a coordinate-independent way to quantify the change in a vector field as it is transported from one point to another. However, to perform concrete computations, we must express this abstract operator in terms of its components within a [local coordinate system](@entry_id:751394). These components, known as the **Christoffel symbols**, are the central focus of this chapter. While they are indispensable for calculation, their nature is subtle; they are not the components of a tensor field. Understanding their unique transformation properties under a change of coordinates is fundamental to mastering the language of differential geometry.

### The Connection Coefficients in a Local Chart

Let $(U, x)$ be a [coordinate chart](@entry_id:263963) on an $n$-dimensional manifold $M$, with coordinates $x = (x^1, \dots, x^n)$. This chart provides a basis for the [tangent space](@entry_id:141028) $T_pM$ at any point $p \in U$, consisting of the [coordinate basis](@entry_id:270149) vectors $\{\partial_1, \dots, \partial_n\}$, where $\partial_i = \frac{\partial}{\partial x^i}$.

An [affine connection](@entry_id:160152) $\nabla$ allows us to take the covariant derivative of one vector field with respect to another. In particular, we can evaluate the [covariant derivative](@entry_id:152476) of one [basis vector](@entry_id:199546) field, $\partial_j$, with respect to another, $\partial_i$. The result, $\nabla_{\partial_i} \partial_j$, must be a vector field, and therefore can be expressed as a linear combination of the basis vectors $\{\partial_k\}$ at each point. We define the **Christoffel symbols** of the connection $\nabla$ (of the second kind) in this [coordinate chart](@entry_id:263963) as the coefficients of this [linear combination](@entry_id:155091).

**Definition:** The Christoffel symbols $\Gamma^k_{ij}$ in the [coordinate chart](@entry_id:263963) $(U, x)$ are the $n^3$ [smooth functions](@entry_id:138942) on $U$ defined by the relation:
$$
\nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k
$$
In this expression, we employ the Einstein [summation convention](@entry_id:755635), where a repeated index (one upper, one lower) implies summation over all its possible values, from $1$ to $n$. The symbol $\Gamma^k_{ij}$ should be understood as the $k$-th component of the covariant derivative of the basis vector $\partial_j$ in the direction of the basis vector $\partial_i$. They encapsulate how the [coordinate basis](@entry_id:270149) itself twists and turns as measured by the connection $\nabla$.

It is essential to recognize from the outset that the Christoffel symbols are tied to the specific coordinate system in which they are defined. If we were to choose a different coordinate system, the basis vectors would be different, and consequently, the coefficients describing their covariant derivatives would also change. The central task is to determine the precise mathematical rule governing this change.

### The Transformation Law for Christoffel Symbols

Let us consider two overlapping [coordinate charts](@entry_id:262338), $(U, x)$ with coordinates $x = (x^1, \dots, x^n)$ and $(V, \tilde{x})$ with coordinates $\tilde{x} = (\tilde{x}^1, \dots, \tilde{x}^n)$, such that their intersection $U \cap V$ is non-empty. Let the Christoffel symbols in the $x$-chart be denoted by $\Gamma^k_{ij}$ and in the $\tilde{x}$-chart by $\tilde{\Gamma}^m_{ab}$.

Our goal is to derive the relationship between $\tilde{\Gamma}^m_{ab}$ and $\Gamma^k_{ij}$ on the overlap region. The derivation proceeds directly from the definition of the [connection coefficients](@entry_id:157618) and the properties of the connection itself, principally its linearity and its adherence to the Leibniz rule [@problem_id:3005709] [@problem_id:3005741].

By definition, in the $\tilde{x}$-chart, we have:
$$
\nabla_{\tilde{\partial}_a} \tilde{\partial}_b = \tilde{\Gamma}^m_{ab} \tilde{\partial}_m
$$
where $\tilde{\partial}_a = \frac{\partial}{\partial \tilde{x}^a}$. The key is to express the left-hand side of this equation entirely in terms of the $x$-coordinate system. The basis vectors of the two systems are related by the chain rule:
$$
\tilde{\partial}_a = \frac{\partial x^i}{\partial \tilde{x}^a} \partial_i \quad \text{and} \quad \tilde{\partial}_b = \frac{\partial x^j}{\partial \tilde{x}^b} \partial_j
$$
Substituting these into the defining equation for $\tilde{\Gamma}^m_{ab}$:
$$
\nabla_{\left(\frac{\partial x^i}{\partial \tilde{x}^a} \partial_i\right)} \left(\frac{\partial x^j}{\partial \tilde{x}^b} \partial_j\right) = \tilde{\Gamma}^m_{ab} \tilde{\partial}_m
$$
Using the $C^\infty(M)$-linearity of the connection $\nabla$ in its first argument, we can factor out the function $\frac{\partial x^i}{\partial \tilde{x}^a}$:
$$
\frac{\partial x^i}{\partial \tilde{x}^a} \nabla_{\partial_i} \left(\frac{\partial x^j}{\partial \tilde{x}^b} \partial_j\right) = \tilde{\Gamma}^m_{ab} \tilde{\partial}_m
$$
Next, we apply the Leibniz rule ([product rule](@entry_id:144424)) for connections to the term in the parentheses, treating $\frac{\partial x^j}{\partial \tilde{x}^b}$ as a scalar function and $\partial_j$ as a vector field:
$$
\nabla_{\partial_i} \left(\frac{\partial x^j}{\partial \tilde{x}^b} \partial_j\right) = \left(\partial_i \left(\frac{\partial x^j}{\partial \tilde{x}^b}\right)\right) \partial_j + \frac{\partial x^j}{\partial \tilde{x}^b} \nabla_{\partial_i} \partial_j
$$
Substituting this back and distributing the leading factor $\frac{\partial x^i}{\partial \tilde{x}^a}$:
$$
\frac{\partial x^i}{\partial \tilde{x}^a} \frac{\partial}{\partial x^i} \left(\frac{\partial x^j}{\partial \tilde{x}^b}\right) \partial_j + \frac{\partial x^i}{\partial \tilde{x}^a} \frac{\partial x^j}{\partial \tilde{x}^b} \nabla_{\partial_i} \partial_j = \tilde{\Gamma}^m_{ab} \tilde{\partial}_m
$$
We can simplify the first term by again applying the chain rule: $\frac{\partial x^i}{\partial \tilde{x}^a} \frac{\partial}{\partial x^i} = \frac{\partial}{\partial \tilde{x}^a} = \tilde{\partial}_a$. This term becomes $\frac{\partial^2 x^j}{\partial \tilde{x}^a \partial \tilde{x}^b} \partial_j$. For the second term, we use the definition $\nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k$. The equation now reads:
$$
\frac{\partial^2 x^j}{\partial \tilde{x}^a \partial \tilde{x}^b} \partial_j + \frac{\partial x^i}{\partial \tilde{x}^a} \frac{\partial x^j}{\partial \tilde{x}^b} \Gamma^k_{ij} \partial_k = \tilde{\Gamma}^m_{ab} \tilde{\partial}_m
$$
To compare coefficients, all terms must be expressed in the same basis. We choose the $\tilde{x}$-basis. Using the inverse transformation $\partial_k = \frac{\partial \tilde{x}^m}{\partial x^k} \tilde{\partial}_m$, and renaming dummy indices for clarity, we get:
$$
\left( \frac{\partial^2 x^k}{\partial \tilde{x}^a \partial \tilde{x}^b} \frac{\partial \tilde{x}^m}{\partial x^k} \right) \tilde{\partial}_m + \left( \frac{\partial x^i}{\partial \tilde{x}^a} \frac{\partial x^j}{\partial \tilde{x}^b} \Gamma^k_{ij} \frac{\partial \tilde{x}^m}{\partial x^k} \right) \tilde{\partial}_m = \tilde{\Gamma}^m_{ab} \tilde{\partial}_m
$$
By equating the coefficients of the [basis vector](@entry_id:199546) $\tilde{\partial}_m$ on both sides, we arrive at the fundamental transformation law for Christoffel symbols:
$$
\tilde{\Gamma}^m_{ab} = \frac{\partial \tilde{x}^m}{\partial x^k} \frac{\partial x^i}{\partial \tilde{x}^a} \frac{\partial x^j}{\partial \tilde{x}^b} \Gamma^k_{ij} + \frac{\partial \tilde{x}^m}{\partial x^k} \frac{\partial^2 x^k}{\partial \tilde{x}^a \partial \tilde{x}^b}
$$

### The Non-Tensorial Nature of the Christoffel Symbols

A brief inspection of the transformation law reveals a crucial feature. To appreciate it, let us first recall how the components of actual [tensor fields](@entry_id:190170) transform. Let $V$ be a vector field (a contravariant tensor of rank 1) and $W$ be a [covector field](@entry_id:186855) (a [covariant tensor](@entry_id:198677) of rank 1). Their components transform as follows [@problem_id:3005723]:
$$
\tilde{V}^i = \frac{\partial \tilde{x}^i}{\partial x^m} V^m
$$
$$
\tilde{W}_i = \frac{\partial x^m}{\partial \tilde{x}^i} W_m
$$
These transformation laws are **linear** and **homogeneous** in the components of the tensor. They involve only the first derivatives of the coordinate transformation functions (the Jacobian matrices). A general tensor of type $(p,q)$ transforms similarly, with $p$ factors of the Jacobian $\frac{\partial \tilde{x}}{\partial x}$ and $q$ factors of the inverse Jacobian $\frac{\partial x}{\partial \tilde{x}}$.

Now, compare this to the Christoffel symbol transformation law. The first term, $\frac{\partial \tilde{x}^m}{\partial x^k} \frac{\partial x^i}{\partial \tilde{x}^a} \frac{\partial x^j}{\partial \tilde{x}^b} \Gamma^k_{ij}$, has precisely the structure of a tensor of type $(1,2)$. If this were the entire law, the Christoffel symbols would constitute a tensor field.

However, the presence of the second term, $\frac{\partial \tilde{x}^m}{\partial x^k} \frac{\partial^2 x^k}{\partial \tilde{x}^a \partial \tilde{x}^b}$, fundamentally changes the situation. This term is **inhomogeneous**; it is an additive term that does not depend on the original Christoffel symbols $\Gamma^k_{ij}$ at all. Instead, it depends on the **second derivatives** of the [coordinate transformation](@entry_id:138577) functions [@problem_id:1880432]. Because of this additive, inhomogeneous term, the Christoffel symbols are not the components of a tensor field [@problem_id:3005722].

This non-tensorial character has a profound and useful consequence. For a true tensor field, if all its components are zero at a point in one coordinate system, they must be zero in all [coordinate systems](@entry_id:149266) at that point. This is not true for Christoffel symbols. It is always possible to find a special coordinate system (e.g., a **Riemannian normal coordinate system**) centered at any point $p$ such that all Christoffel symbols vanish at that specific point, $\Gamma^k_{ij}(p) = 0$. If we then transform to a general, curvilinear coordinate system $\tilde{x}$, the transformation law gives:
$$
\tilde{\Gamma}^m_{ab}(p) = \frac{\partial \tilde{x}^m}{\partial x^k} \frac{\partial x^i}{\partial \tilde{x}^a} \frac{\partial x^j}{\partial \tilde{x}^b} (0) + \left. \frac{\partial \tilde{x}^m}{\partial x^k} \frac{\partial^2 x^k}{\partial \tilde{x}^a \partial \tilde{x}^b} \right|_p
$$
Unless the coordinate transformation is affine (meaning its second derivatives are zero), the new symbols $\tilde{\Gamma}^m_{ab}(p)$ will be non-zero.

A perfect illustration is the Euclidean plane, $\mathbb{R}^2$ [@problem_id:2968175]. In standard Cartesian coordinates $(x^1, x^2) = (x, y)$, the metric is constant and the Levi-Civita connection has Christoffel symbols that are all zero: $\Gamma^k_{ij} = 0$. Now, let's transform to [polar coordinates](@entry_id:159425) $(\tilde{x}^1, \tilde{x}^2) = (r, \theta)$, where $x = r \cos\theta$ and $y = r \sin\theta$. Since the original $\Gamma^k_{ij}$ are zero, the new symbols are given purely by the inhomogeneous term:
$$
\tilde{\Gamma}^m_{ab} = \frac{\partial \tilde{x}^m}{\partial x^k} \frac{\partial^2 x^k}{\partial \tilde{x}^a \partial \tilde{x}^b}
$$
Let us compute the component $\tilde{\Gamma}^r_{\theta\theta}$. We have $m=r, a=\theta, b=\theta$. The sum is over $k=x, y$.
$$
\tilde{\Gamma}^r_{\theta\theta} = \frac{\partial r}{\partial x} \frac{\partial^2 x}{\partial \theta^2} + \frac{\partial r}{\partial y} \frac{\partial^2 y}{\partial \theta^2}
$$
The necessary [partial derivatives](@entry_id:146280) are:
- $\frac{\partial x}{\partial \theta} = -r\sin\theta \implies \frac{\partial^2 x}{\partial \theta^2} = -r\cos\theta = -x$
- $\frac{\partial y}{\partial \theta} = r\cos\theta \implies \frac{\partial^2 y}{\partial \theta^2} = -r\sin\theta = -y$
- $r = \sqrt{x^2+y^2} \implies \frac{\partial r}{\partial x} = \frac{x}{r} = \cos\theta$ and $\frac{\partial r}{\partial y} = \frac{y}{r} = \sin\theta$

Substituting these into the expression:
$$
\tilde{\Gamma}^r_{\theta\theta} = (\cos\theta)(-r\cos\theta) + (\sin\theta)(-r\sin\theta) = -r(\cos^2\theta + \sin^2\theta) = -r
$$
Thus, even in a perfectly [flat space](@entry_id:204618), simply choosing a non-rectilinear coordinate system induces non-zero Christoffel symbols. This powerfully demonstrates their coordinate-dependent, non-tensorial nature.

### The Role of the Transformation Law in Ensuring Geometric Consistency

The non-tensorial transformation law is not a defect, but a necessary feature for constructing a consistent theory of differentiation on manifolds. This can be seen from two alternative perspectives.

#### Invariance of the Covariant Derivative

The [covariant derivative](@entry_id:152476) of a vector field, $\nabla V$, is a tensor of type $(1,1)$. Its components in the $x$-chart are $(\nabla V)^k_i = \partial_i V^k + \Gamma^k_{ij} V^j$. The transformation law for the Christoffel symbols is precisely what's required to make $(\nabla V)$ transform as a tensor. That is, the components must satisfy [@problem_id:3005739]:
$$
(\tilde{\nabla} \tilde{V})^m_a = \frac{\partial \tilde{x}^m}{\partial x^k} \frac{\partial x^i}{\partial \tilde{x}^a} (\nabla V)^k_i
$$
If we expand both sides using the component formula for the [covariant derivative](@entry_id:152476) and the transformation law for the vector components $\tilde{V}^m$, we find that the non-tensorial behavior of the partial derivative $\partial_a \tilde{V}^m$ is exactly cancelled by the inhomogeneous term in the transformation of $\tilde{\Gamma}^m_{ab}$, leaving a purely tensorial result.

#### Invariance of the Geodesic Equation

Geometrically, a geodesic is the "straightest possible path" on a manifold. A curve $x^i(\lambda)$ parameterized by an affine parameter $\lambda$ is a geodesic if it satisfies the **[geodesic equation](@entry_id:136555)**:
$$
\frac{d^2 x^i}{d\lambda^2} + \Gamma^i_{jk} \frac{dx^j}{d\lambda} \frac{dx^k}{d\lambda} = 0
$$
The property of being a geodesic must be independent of the coordinate system used. If we transform the coordinates to $\tilde{x}^m(\lambda)$, the curve must satisfy the same form of equation, $\frac{d^2 \tilde{x}^m}{d\lambda^2} + \tilde{\Gamma}^m_{ab} \frac{d\tilde{x}^a}{d\lambda} \frac{d\tilde{x}^b}{d\lambda} = 0$.

When we transform the term $\frac{d^2 x^i}{d\lambda^2}$ using the chain rule, a second derivative term naturally appears due to the potential non-linearity of the [coordinate map](@entry_id:154545):
$$
\frac{d^2 x^i}{d\lambda^2} = \frac{\partial x^i}{\partial \tilde{x}^m} \frac{d^2 \tilde{x}^m}{d\lambda^2} + \frac{\partial^2 x^i}{\partial \tilde{x}^a \partial \tilde{x}^b} \frac{d\tilde{x}^a}{d\lambda} \frac{d\tilde{x}^b}{d\lambda}
$$
Substituting this into the original geodesic equation and rearranging reveals that the Christoffel symbols must transform in their specific, non-tensorial way. The inhomogeneous term in their transformation law is precisely what is needed to absorb the second-derivative term generated by the chain rule, ensuring that the geodesic equation maintains its form in any coordinate system [@problem_id:3005700].

### Advanced Considerations

#### Regularity Requirements

For the theory to be well-defined, we must pay attention to the smoothness class of our structures.
1.  **Metric Regularity:** For the Levi-Civita connection, the Christoffel symbols are calculated from the metric tensor components $g_{ij}$ and its inverse $g^{ij}$ via the formula $\Gamma^k_{ij} = \frac{1}{2} g^{kl} (\partial_i g_{lj} + \partial_j g_{il} - \partial_l g_{ij})$. This formula involves first derivatives of the metric. For the Christoffel symbols to be continuous functions ($C^0$), the metric components $g_{ij}$ must be at least of class $C^1$.
2.  **Atlas Regularity:** The transformation law for the Christoffel symbols involves second derivatives of the coordinate change functions. For this law to be well-defined and for the resulting $\tilde{\Gamma}^m_{ab}$ to be continuous, the coordinate transition maps must be at least of class $C^2$.

Therefore, the minimal requirement for the Christoffel symbols of a Levi-Civita connection and their transformation law to be well-defined is a **$C^2$ atlas** for the manifold and a **$C^1$ metric** [@problem_id:3005708]. In most advanced texts, manifolds are assumed to be smooth ($C^\infty$) for simplicity.

#### The Affine Space of Connections and 2-Jets

A deeper geometric understanding of the transformation law comes from viewing the space of all linear connections, $\mathcal{C}$, on the tangent bundle $TM$. This space is not a vector space, but an **affine space**. This means that while there is no natural "zero" connection, the *difference* between any two connections, $\nabla_1 - \nabla_2$, is a well-defined object. This difference is a tensor field of type $(1,2)$, whose components are $\Delta^k_{ij} = (\Gamma_1)^k_{ij} - (\Gamma_2)^k_{ij}$. When one transforms the components of $\Delta^k_{ij}$, the inhomogeneous terms from each connection's transformation law are identical and thus cancel, leaving a purely tensorial transformation law.

This structure can be elegantly described using the language of jets [@problem_id:3005696]. The value of the Christoffel symbols at a point $p$ depends not just on the first derivative of the coordinate transformation (the Jacobian matrix, an element of $GL(n,\mathbb{R})$), but on its second derivative as well. The collection of first and second derivatives defines the **2-jet** of the coordinate transformation at $p$. The transformation law for Christoffel symbols is precisely an affine action of the group of 2-jets of local diffeomorphisms on the space of [connection coefficients](@entry_id:157618). The linear part of the action is the tensorial part of the transformation, while the translational (inhomogeneous) part is determined by the second-derivative information in the jet. This perspective clarifies that the Christoffel symbols are not just a collection of functions, but represent a more complex geometric object known as a **connection object** or **[jet bundle](@entry_id:158903) section**, whose transformation properties are necessarily affine rather than linear.