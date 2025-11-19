## Introduction
How can we measure distances, angles, and areas on a curved surface like a sphere or a torus? While these objects exist in three-dimensional space, their most essential geometric properties are those that could be measured by an observer living entirely within the surface itself. This concept of "[intrinsic geometry](@entry_id:158788)" is fundamental to modern mathematics and physics, but it poses a significant challenge: we need a language to describe these properties without relying on the external, [ambient space](@entry_id:184743).

This article introduces the solution to this problem: the **first fundamental form**. This powerful mathematical object, also known as the surface's metric tensor, provides a complete recipe for performing all local geometric measurements. It is the intrinsic ruler and protractor for any curved surface.

Throughout this exploration, you will gain a comprehensive understanding of this cornerstone of [differential geometry](@entry_id:145818). We will begin in **Principles and Mechanisms** by defining the first fundamental form through its coefficients—E, F, and G—and demonstrating how to calculate them for various surfaces. You will learn how these coefficients directly translate into formulas for arc length, angles, and surface area. Next, in **Applications and Interdisciplinary Connections**, we will see the first fundamental form in action, exploring its role in defining "straight lines" (geodesics), understanding Gauss's celebrated Theorema Egregium, and modeling physical systems in mechanics and engineering. Finally, the **Hands-On Practices** section provides an opportunity to apply your knowledge through guided problems, solidifying your ability to compute and interpret the intrinsic [geometry of surfaces](@entry_id:271794).

## Principles and Mechanisms

In our study of surfaces, a fundamental challenge is to describe their geometric properties—such as length, angle, and area—in a way that is independent of how the surface is situated in the ambient three-dimensional space. We seek a language to describe the geometry as it would be perceived by an observer constrained to the surface itself. This "intrinsic" geometry is entirely encoded within a mathematical object known as the **[first fundamental form](@entry_id:274022)**. It serves as the metric tensor of the surface, providing the essential tool for all local geometric measurements.

### Defining the Metric: The First Fundamental Form

Consider a regular [parametric surface](@entry_id:260739) in $\mathbb{R}^3$, defined by a vector function $\mathbf{x}(u, v)$ over some domain in the $uv$-plane. At any point $p = \mathbf{x}(u_0, v_0)$ on the surface, the partial derivative vectors,
$$ \mathbf{x}_u = \frac{\partial \mathbf{x}}{\partial u} \quad \text{and} \quad \mathbf{x}_v = \frac{\partial \mathbf{x}}{\partial v} $$
are tangent to the surface. Since the surface is regular, these two vectors are [linearly independent](@entry_id:148207) and thus form a basis for the **tangent plane** at point $p$. Any [tangent vector](@entry_id:264836) $\mathbf{w}$ at $p$ can be expressed as a linear combination of these basis vectors.

The first fundamental form is built upon the standard Euclidean dot product of these basis vectors in the [ambient space](@entry_id:184743) $\mathbb{R}^3$. We define three coefficients, traditionally denoted by $E$, $F$, and $G$, which are functions of the parameters $(u, v)$:

*   $E(u, v) = \mathbf{x}_u \cdot \mathbf{x}_u = \|\mathbf{x}_u\|^2$
*   $F(u, v) = \mathbf{x}_u \cdot \mathbf{x}_v$
*   $G(u, v) = \mathbf{x}_v \cdot \mathbf{x}_v = \|\mathbf{x}_v\|^2$

The coefficient $E$ is the squared length of the [tangent vector](@entry_id:264836) along a curve of constant $v$, while $G$ is the squared length of the tangent vector along a curve of constant $u$. The coefficient $F$ measures the interaction between these two directions; specifically, it is related to the angle between the coordinate curves.

These three coefficients are the components of a symmetric $2 \times 2$ matrix, which represents the metric tensor of the surface in the $(u,v)$ coordinate system:
$$ g = \begin{pmatrix} E(u,v) & F(u,v) \\ F(u,v) & G(u,v) \end{pmatrix} $$

Let's compute these coefficients for a concrete example. Consider the surface parameterized by $\mathbf{x}(u, v) = (u - v, u + v, 2uv)$ [@problem_id:1674279]. First, we find the tangent basis vectors:
$$ \mathbf{x}_u = (1, 1, 2v) $$
$$ \mathbf{x}_v = (-1, 1, 2u) $$
Next, we compute their dot products:
$$ E = \mathbf{x}_u \cdot \mathbf{x}_u = 1^2 + 1^2 + (2v)^2 = 2 + 4v^2 $$
$$ F = \mathbf{x}_u \cdot \mathbf{x}_v = (1)(-1) + (1)(1) + (2v)(2u) = 4uv $$
$$ G = \mathbf{x}_v \cdot \mathbf{x}_v = (-1)^2 + 1^2 + (2u)^2 = 2 + 4u^2 $$
Thus, the matrix of the first fundamental form for this surface is:
$$ g = \begin{pmatrix} 2 + 4v^2 & 4uv \\ 4uv & 2 + 4u^2 \end{pmatrix} $$
Notice that the coefficients, and therefore the local geometry, vary from point to point on the surface.

A particularly common and useful type of [parametrization](@entry_id:272587) is the **Monge patch**, where a surface is given as the [graph of a function](@entry_id:159270), $z = f(x, y)$. We can naturally parametrize this surface by letting $u=x$ and $v=y$, so that $\mathbf{x}(x, y) = (x, y, f(x, y))$. The [tangent vectors](@entry_id:265494) are $\mathbf{x}_x = (1, 0, f_x)$ and $\mathbf{x}_y = (0, 1, f_y)$, where $f_x = \frac{\partial f}{\partial x}$ and $f_y = \frac{\partial f}{\partial y}$. The coefficients of the first fundamental form take a simple and elegant form [@problem_id:1674236]:
$$ E = 1 + f_x^2 $$
$$ F = f_x f_y $$
$$ G = 1 + f_y^2 $$
This shows directly how the "steepness" of the surface, captured by the [partial derivatives](@entry_id:146280) of $f$, determines its local metric properties.

### Geometric Applications: Measuring on a Surface

The true power of the [first fundamental form](@entry_id:274022) lies in its ability to quantify all intrinsic geometric properties. Once $E$, $F$, and $G$ are known, we can perform measurements of length, angle, and area without any further reference to the [ambient space](@entry_id:184743) $\mathbb{R}^3$.

#### Length of a Tangent Vector

Consider an arbitrary tangent vector $\mathbf{w}$ at a point on the surface. As it lies in the [tangent plane](@entry_id:136914), it can be written as a [linear combination](@entry_id:155091) of the basis vectors, $\mathbf{w} = a \mathbf{x}_u + b \mathbf{x}_v$, for some scalars $a$ and $b$. Its squared length is given by the dot product $\mathbf{w} \cdot \mathbf{w}$:
$$ \|\mathbf{w}\|^2 = (a \mathbf{x}_u + b \mathbf{x}_v) \cdot (a \mathbf{x}_u + b \mathbf{x}_v) $$
$$ \|\mathbf{w}\|^2 = a^2 (\mathbf{x}_u \cdot \mathbf{x}_u) + 2ab (\mathbf{x}_u \cdot \mathbf{x}_v) + b^2 (\mathbf{x}_v \cdot \mathbf{x}_v) $$
$$ \|\mathbf{w}\|^2 = a^2 E + 2ab F + b^2 G $$
This expression is a quadratic form, often written as $I(\mathbf{w})$, and can be expressed in matrix notation:
$$ I(\mathbf{w}) = \begin{pmatrix} a & b \end{pmatrix} \begin{pmatrix} E & F \\ F & G \end{pmatrix} \begin{pmatrix} a \\ b \end{pmatrix} $$
This fundamental equation tells us how to calculate the length of any vector specified in the $(u, v)$ coordinate system. For example, to find the length of the [tangent vector](@entry_id:264836) $\mathbf{w} = 2 \mathbf{x}_u + \mathbf{x}_v$ at a specific point on an ellipsoid, we would first compute the values of $E, F, G$ at that point and then evaluate $\|\mathbf{w}\|^2 = 2^2 E + 2(2)(1) F + 1^2 G = 4E + 4F + G$ [@problem_id:1674253]. This procedure is entirely intrinsic; it relies only on the coordinates $(a, b)$ and the metric coefficients $(E, F, G)$.

#### Angle Between Vectors

The first fundamental form also determines the angles between [tangent vectors](@entry_id:265494). The dot product of two vectors $\mathbf{w}_1 = a_1 \mathbf{x}_u + b_1 \mathbf{x}_v$ and $\mathbf{w}_2 = a_2 \mathbf{x}_u + b_2 \mathbf{x}_v$ is:
$$ \mathbf{w}_1 \cdot \mathbf{w}_2 = a_1 a_2 E + (a_1 b_2 + a_2 b_1) F + b_1 b_2 G $$
The angle $\alpha$ between them is then found from the familiar formula $\cos \alpha = \frac{\mathbf{w}_1 \cdot \mathbf{w}_2}{\|\mathbf{w}_1\| \|\mathbf{w}_2\|}$.

A particularly important case is the angle between the coordinate curves themselves, whose tangents are $\mathbf{x}_u$ and $\mathbf{x}_v$. The angle $\alpha$ between them is given by:
$$ \cos \alpha = \frac{\mathbf{x}_u \cdot \mathbf{x}_v}{\|\mathbf{x}_u\| \|\mathbf{x}_v\|} = \frac{F}{\sqrt{EG}} $$
From this, we see a crucial geometric interpretation of the coefficient $F$: the coordinate curves are orthogonal at a point if and only if $F(u, v) = 0$.

A classic example is the standard spherical coordinate parametrization of a sphere. The coordinate curves correspond to lines of longitude and latitude. A direct calculation shows that for a sphere of radius $R$, $E=R^2\sin^2\phi$, $G=R^2$, and, most importantly, $F=0$ everywhere (except at the poles where the [parametrization](@entry_id:272587) is singular), where $\phi$ is the [polar angle](@entry_id:175682) and the parametrization is with respect to $(\theta, \phi)$ (azimuthal, polar) [@problem_id:1674246]. The fact that $F=0$ proves mathematically that lines of longitude and latitude are always perpendicular to each other, a familiar fact from [cartography](@entry_id:276171). Parametrizations where $F=0$ are called **orthogonal parametrizations**.

#### Area of a Surface Patch

To find the area of a small patch of the surface corresponding to an infinitesimal rectangle $du \, dv$ in the [parameter plane](@entry_id:195289), we consider the parallelogram spanned by the vectors $\mathbf{x}_u du$ and $\mathbf{x}_v dv$. Its area, denoted $dA$, is the magnitude of their [cross product](@entry_id:156749):
$$ dA = \|\mathbf{x}_u du \times \mathbf{x}_v dv\| = \|\mathbf{x}_u \times \mathbf{x}_v\| \, du \, dv $$
To express this intrinsically, we use **Lagrange's identity** from [vector algebra](@entry_id:152340), which states that for any two vectors $\mathbf{a}, \mathbf{b} \in \mathbb{R}^3$, $\|\mathbf{a} \times \mathbf{b}\|^2 = \|\mathbf{a}\|^2 \|\mathbf{b}\|^2 - (\mathbf{a} \cdot \mathbf{b})^2$. Applying this to our [tangent vectors](@entry_id:265494):
$$ \|\mathbf{x}_u \times \mathbf{x}_v\|^2 = \|\mathbf{x}_u\|^2 \|\mathbf{x}_v\|^2 - (\mathbf{x}_u \cdot \mathbf{x}_v)^2 = EG - F^2 $$
The quantity $EG-F^2$ is precisely the determinant of the metric tensor matrix $g$. Since our surface is regular, $\mathbf{x}_u$ and $\mathbf{x}_v$ are [linearly independent](@entry_id:148207), so $EG - F^2 > 0$. The surface [area element](@entry_id:197167) is therefore:
$$ dA = \sqrt{EG - F^2} \, du \, dv $$
The function $\Sigma(u,v) = \sqrt{EG - F^2}$ acts as a local **area scaling factor**. It measures how much the area is stretched or compressed when mapping from the flat $uv$-plane to the curved surface. In cartography, where one maps the curved surface of the Earth to a flat plane, this factor describes the map's area distortion. For instance, in the [stereographic projection](@entry_id:142378) of a sphere, one can calculate $\sqrt{EG - F^2}$ and find the specific locations where this factor equals 1, identifying the circle on the map where the projection is locally area-preserving [@problem_id:1674255].

### Intrinsic Geometry and Invariance

The most profound consequence of the [first fundamental form](@entry_id:274022) is the distinction between [intrinsic and extrinsic geometry](@entry_id:161677). Intrinsic properties are those that depend only on $E, F$, and $G$.

#### Isometry and Intrinsic Properties

Two surfaces, $S_1$ and $S_2$, are said to be **locally isometric** if there exists a mapping between them that preserves the first fundamental form. This means that if point $p \in S_1$ is mapped to point $q \in S_2$, the metric tensor at $p$ is identical to the metric tensor at $q$ (under the corresponding [change of coordinates](@entry_id:273139)). Consequently, all intrinsic measurements—lengths of curves, angles between curves, areas of regions—are identical on both surfaces. An inhabitant of the surface could not tell them apart.

A striking example of this is the relationship between a flat plane and a cylinder [@problem_id:1674234]. A flat sheet of paper can be parametrized by $\mathbf{x}_1(u,v) = (u,v,0)$, for which we find $(E_1, F_1, G_1) = (1, 0, 1)$. If we roll this sheet into a cylinder of radius $R$, we can use the [parametrization](@entry_id:272587) $\mathbf{x}_2(u,v) = (R \cos(u/R), R \sin(u/R), v)$. A direct calculation reveals that the coefficients for the cylinder are also $(E_2, F_2, G_2) = (1, 0, 1)$. Since their first fundamental forms are identical, the plane and the cylinder are locally isometric. This is the mathematical reason why paper can be rolled into a cylinder without stretching or tearing: its [intrinsic geometry](@entry_id:158788) does not change. Such surfaces, which are locally isometric to the Euclidean plane, are called **[developable surfaces](@entry_id:269064)**.

#### Theorema Egregium and the Limits of Isometry

This raises a natural question: is a sphere also a [developable surface](@entry_id:151049)? Can we find a [parametrization](@entry_id:272587) of a sphere for which $(E,F,G)$ are constants, which would make it locally isometric to a flat plane? This would be equivalent to creating a perfect, distortion-free map of the Earth.

The answer is no, and the reason lies at the heart of differential geometry. A surface with constant $E, F, G$ is demonstrably "flat" in an intrinsic sense—its curvature is zero. However, a sphere has inherent curvature that cannot be removed. This was formalized by Carl Friedrich Gauss in his **Theorema Egregium** (Remarkable Theorem). The theorem states that the **Gaussian curvature** $K$ of a surface at a point can be calculated using only the coefficients $E, F, G$ and their partial derivatives. Because $K$ depends only on the first fundamental form, it is an [intrinsic property](@entry_id:273674).

A sphere of radius $R$ has a constant positive Gaussian curvature of $K = 1/R^2$. A flat plane has $K=0$. Since an isometry must preserve all intrinsic properties, it must preserve Gaussian curvature. Because $1/R^2 \neq 0$, no mapping can exist between a patch of a sphere and a patch of a plane that preserves the [first fundamental form](@entry_id:274022). Therefore, a sphere is not locally isometric to a plane, and no local [parametrization](@entry_id:272587) of a sphere exists where $E$, $F$, and $G$ are all constant [@problem_id:1674270].

#### Invariance under Reparametrization

The geometric quantities we measure should not depend on the arbitrary choice of coordinates $(u, v)$. If we introduce a new set of parameters $(\tilde{u}, \tilde{v})$ through a smooth, invertible transformation, the surface itself does not change, and neither should its area. Under such a [reparametrization](@entry_id:176404), the new area element must be equal to the old one. This is guaranteed by the [change of variables](@entry_id:141386) formula from [multivariable calculus](@entry_id:147547). The area scaling factor transforms according to the rule [@problem_id:1674273]:
$$ \sqrt{E'G' - (F')^2} = \left|\det\left(J\right)\right| \sqrt{EG - F^2} $$
where $J$ is the Jacobian matrix of the coordinate transformation. The area [integral transforms](@entry_id:186209) as:
$$ \iint \sqrt{E'G' - (F')^2} \, d\tilde{u} \, d\tilde{v} = \iint \sqrt{EG - F^2} \left|\det\left(J\right)\right| \, d\tilde{u} \, d\tilde{v} = \iint \sqrt{EG - F^2} \, du \, dv $$
This confirms that the calculated area of a region is a true geometric invariant, independent of the parametrization used to compute it.

### Specialized Parametrizations and Further Concepts

#### Conformal Maps

While isometries are rare, a less restrictive and highly useful class of maps are **[conformal maps](@entry_id:271672)**, which preserve angles but not necessarily lengths. From the formula $\cos \alpha = F/\sqrt{EG}$, we see that angles between coordinate curves are preserved if $F$ remains zero. For general angles, the condition for conformality is that the metric must take the form:
$$ ds^2 = \lambda(u, v)(du^2 + dv^2) $$
This corresponds to having $E(u, v) = G(u, v)$ and $F(u, v) = 0$. In this case, the length of any [tangent vector](@entry_id:264836) is stretched by the same factor $\sqrt{\lambda(u,v)}$, regardless of its direction. The famous Mercator projection used in nautical charts is a prime example. By changing variables from spherical coordinates $(\phi, \theta)$ to Mercator coordinates $(u, v)$, one can show that the first fundamental form of the sphere becomes $ds^2 = \frac{1}{\cosh^2(v/R)} (du^2 + dv^2)$ [@problem_id:1674249]. This structure confirms its angle-preserving property, which was invaluable for navigation.

#### Regularity and Generalizations

Throughout this discussion, we have assumed our parametrizations are **regular**, meaning the tangent vectors $\mathbf{x}_u$ and $\mathbf{x}_v$ are [linearly independent](@entry_id:148207) at every point. This is crucial for forming a valid basis for the [tangent plane](@entry_id:136914). We have seen that this condition is equivalent to the positivity of the metric determinant:
$$ EG - F^2 > 0 $$
A point where $EG - F^2 = 0$ is a [singular point](@entry_id:171198) of the parametrization, where the coordinate system may break down. For instance, the poles of a sphere in standard [spherical coordinates](@entry_id:146054) are [singular points](@entry_id:266699).

Finally, it is important to note that the entire framework of the first fundamental form is not limited to surfaces in $\mathbb{R}^3$. The definitions of $E, F, G$ rely only on the dot product, which exists in any Euclidean space $\mathbb{R}^n$. Thus, we can analyze the intrinsic [geometry of surfaces](@entry_id:271794) embedded in higher-dimensional spaces, such as the Klein bottle embedded in $\mathbb{R}^4$, by computing its metric coefficients in exactly the same way [@problem_id:1674286]. This illustrates the generality and power of the first fundamental form as the foundational tool for the study of manifolds.