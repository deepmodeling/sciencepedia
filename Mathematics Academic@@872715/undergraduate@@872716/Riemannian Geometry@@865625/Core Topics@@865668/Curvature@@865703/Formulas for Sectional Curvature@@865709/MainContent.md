## Introduction
In the landscape of Riemannian geometry, the Riemann [curvature tensor](@entry_id:181383) stands as the ultimate arbiter of a manifold's local geometry. However, its nature as a multilinear tensor can make direct geometric interpretation challenging. To bridge the gap between this abstract algebraic object and our geometric intuition, mathematicians developed the concept of sectional curvature. This powerful invariant distills the complex information of the Riemann tensor into a single, understandable number for every two-dimensional "slice" of the space, effectively generalizing the classical notion of Gaussian curvature from surfaces to manifolds of any dimension.

This article addresses the fundamental need for concrete formulas to define, compute, and apply [sectional curvature](@entry_id:159738). It demystifies this core concept by systematically deriving its defining equations and exploring their profound consequences. Over the next three chapters, you will gain a robust understanding of this geometric tool. The journey begins in "Principles and Mechanisms," where we will rigorously define [sectional curvature](@entry_id:159738), establish its key formulas, and explore the underlying algebraic properties that ensure its consistency. Following this, "Applications and Interdisciplinary Connections" will showcase the utility of these formulas by using them to classify the fundamental spaces of geometry, build new manifolds, and describe the structure of spacetime in physics. Finally, "Hands-On Practices" will provide opportunities to apply this knowledge through guided computational exercises on canonical examples.

## Principles and Mechanisms

In the study of Riemannian manifolds, the Riemann [curvature tensor](@entry_id:181383) encapsulates the notion of curvature. While this tensor provides a complete description, its multilinear nature makes it abstract. A more intuitive and geometric understanding is achieved through the concept of **sectional curvature**, which describes the curvature of two-dimensional slices, or "sections," of the tangent space at each point. This chapter will formally define sectional curvature, establish its fundamental properties, and explore key formulas that govern its behavior in various geometric settings.

### The Definition of Sectional Curvature

The [sectional curvature](@entry_id:159738) at a point $p$ on a Riemannian manifold $(M,g)$ is a real-valued function $K(\sigma)$ that assigns a number to each two-dimensional subspace $\sigma$ (a 2-plane) of the tangent space $T_pM$. This number generalizes the notion of Gaussian curvature for surfaces. Intuitively, if we imagine a surface within $M$ whose tangent plane at $p$ is $\sigma$, the sectional curvature $K(\sigma)$ is the Gaussian curvature of this surface at $p$.

The formal definition is built from the Riemann curvature tensor $R$. For the simplest case, let us consider an **orthonormal basis** $\{u, v\}$ for the 2-plane $\sigma$. The [sectional curvature](@entry_id:159738) of $\sigma$ is defined as:

$K(\sigma) = \langle R(u,v)v, u \rangle$

where $\langle \cdot, \cdot \rangle$ is the inner product on $T_pM$ induced by the metric $g$, and $R(u,v)v$ is the curvature endomorphism $R(u,v)$ applied to the vector $v$.

While this definition is simple, it relies on the choice of an orthonormal basis. A more general and powerful formula is required for an arbitrary basis $\{u,v\}$ of $\sigma$. Such a formula can be derived by applying the Gram-Schmidt process to an arbitrary basis $\{u,v\}$ to obtain an [orthonormal basis](@entry_id:147779) and then expressing the result in terms of the original vectors [@problem_id:3046598]. This procedure yields the general definition of sectional curvature:

$K(\sigma) = \frac{\langle R(u,v)v, u \rangle}{\|u\|^2\|v\|^2 - \langle u,v\rangle^2}$

Here, $\{u,v\}$ is any pair of [linearly independent](@entry_id:148207) vectors spanning the plane $\sigma$. The expression in the numerator, $\langle R(u,v)v, u \rangle$, is often written as $R(u,v,v,u)$ using the $(0,4)$-version of the Riemann tensor. The denominator is a normalization factor that ensures the final value depends only on the plane $\sigma$ and not on the specific vectors chosen to span it.

The denominator has a profound geometric and algebraic meaning. It is precisely the square of the area of the parallelogram spanned by the vectors $u$ and $v$ [@problem_id:3046612]. This can be seen by recalling that the area is given by $\|u\|\|v\||\sin\theta|$, where $\theta$ is the angle between $u$ and $v$. Squaring this and using the relation $\langle u,v \rangle = \|u\|\|v\|\cos\theta$ gives:

$\text{Area}^2 = \|u\|^2\|v\|^2\sin^2\theta = \|u\|^2\|v\|^2(1-\cos^2\theta) = \|u\|^2\|v\|^2 - \langle u,v\rangle^2$

This expression is also recognizable as the determinant of the **Gram matrix** of the vectors $u$ and $v$:

$\det \begin{pmatrix} \langle u,u \rangle & \langle u,v \rangle \\ \langle v,u \rangle & \langle v,v \rangle \end{pmatrix} = \|u\|^2\|v\|^2 - \langle u,v\rangle^2$

In the language of [exterior algebra](@entry_id:201164), this quantity is the squared norm of the simple 2-vector (or [bivector](@entry_id:204759)) $u \wedge v \in \Lambda^2 T_pM$ that represents the oriented plane $\sigma$. The inner product on $\Lambda^2 T_pM$ is induced from the metric $g$ on $T_pM$, and for a simple [bivector](@entry_id:204759), its norm is defined as the area of the parallelogram it represents [@problem_id:3046627]. Thus, the most compact and elegant form of the definition is:

$K(\sigma) = \frac{\langle R(u,v)v, u \rangle}{\|u \wedge v\|^2}$

### Fundamental Properties and Well-Definedness

A crucial feature of sectional curvature is that it is an [intrinsic property](@entry_id:273674) of the 2-plane itself, independent of the choice of basis. This **basis-independence** is guaranteed by the structure of the formula. If we choose a different basis $\{u', v'\}$ for $\sigma$, related to $\{u,v\}$ by a linear transformation with matrix $A$, such that $u' = au+bv$ and $v'=cu+dv$, then both the numerator and the denominator of the formula transform by the same factor of $(\det A)^2$. The [bivector](@entry_id:204759) transforms as $u' \wedge v' = (\det A) (u \wedge v)$, so the denominator $\|u' \wedge v'\|^2$ is scaled by $(\det A)^2$. A careful calculation using the multilinearity and skew-symmetry of the Riemann tensor shows that the numerator $R(u',v',v',u')$ is also scaled by $(\det A)^2$. Consequently, the ratio remains unchanged [@problem_id:3046606]:

$K(\sigma) = \frac{R(u',v',v',u')}{\|u' \wedge v'\|^2} = \frac{(\det A)^2 R(u,v,v,u)}{(\det A)^2 \|u \wedge v\|^2} = \frac{R(u,v,v,u)}{\|u \wedge v\|^2}$

This remarkable invariance is not accidental; it is a direct consequence of the fundamental algebraic symmetries of the Riemann [curvature tensor](@entry_id:181383). For a Levi-Civita connection, these symmetries arise from its defining properties of being [metric-compatible](@entry_id:160255) and torsion-free [@problem_id:3046622].
Specifically:
1.  **Skew-symmetry in the first two arguments**: $R(u,v,w,z) = -R(v,u,w,z)$, which is intrinsic to the definition of the [curvature operator](@entry_id:198006) $R(u,v) = \nabla_u\nabla_v - \nabla_v\nabla_u - \nabla_{[u,v]}$.
2.  **Skew-symmetry in the last two arguments**: $R(u,v,w,z) = -R(u,v,z,w)$. This property is a direct consequence of the **metric-compatibility** of the Levi-Civita connection. It is equivalent to the statement that the endomorphism $R(u,v)$ is skew-adjoint with respect to the metric.
3.  **First Bianchi Identity**: $R(u,v,w,z) + R(v,w,u,z) + R(w,u,v,z) = 0$. This identity follows from the **torsion-free** property of the connection.

These three symmetries together imply a fourth, the **[pair interchange symmetry](@entry_id:268419)**:
$R(u,v,w,z) = R(w,z,u,v)$

This full set of symmetries is what ensures the well-behaved transformation of the numerator, making sectional curvature a coherent geometric concept. This symmetry structure allows the Riemann tensor to be viewed as a [self-adjoint operator](@entry_id:149601) on the space of 2-forms $\Lambda^2 T_pM$, and the [sectional curvature](@entry_id:159738) is the value of the associated [quadratic form](@entry_id:153497) on unit simple [2-forms](@entry_id:188008).

#### A Note on Sign Conventions
It is important to be aware that there are two common sign conventions for the Riemann curvature tensor in the literature. The convention used in this text, often called the Spencer convention, is:
$R(X,Y)Z = \nabla_X\nabla_Y Z - \nabla_Y\nabla_X Z - \nabla_{[X,Y]}Z$

An alternative convention simply flips the sign:
$R'(X,Y)Z = \nabla_Y\nabla_X Z - \nabla_X\nabla_Y Z + \nabla_{[X,Y]}Z = -R(X,Y)Z$

This choice directly impacts the sign of the sectional curvature. If $K(\sigma)$ is the sectional curvature in our convention, the alternative convention yields $K'(\sigma) = -K(\sigma)$. For example, in our convention, the standard unit sphere $S^n$ has [constant sectional curvature](@entry_id:272200) $+1$. In the alternative convention, it has [constant sectional curvature](@entry_id:272200) $-1$ [@problem_id:3046619]. It is crucial to be mindful of the convention used when consulting different sources.

### Sectional Curvature in Special Dimensions and Geometries

The significance of [sectional curvature](@entry_id:159738) varies with the dimension of the manifold.

#### Dimension Two: Identity with Gaussian Curvature
For a 2-dimensional Riemannian manifold (a surface), the situation simplifies dramatically. At any point $p$, there is only one possible 2-plane in the tangent space: $T_pM$ itself. Therefore, the [sectional curvature](@entry_id:159738) at $p$ is a single number, $K(p)$. This value is precisely the classical **Gaussian curvature** of the surface at that point [@problem_id:3046614].

This can be understood from two perspectives. Algebraically, the space of [2-forms](@entry_id:188008) $\Lambda^2 T_pM$ on a 2-dimensional vector space $T_pM$ is 1-dimensional. The [curvature operator](@entry_id:198006), being a [linear map](@entry_id:201112) from this space to itself, must be simple multiplication by a scalar. This scalar is exactly the [sectional curvature](@entry_id:159738) $K(p)$. Alternatively, by examining the traces of the Riemann tensor, one finds a direct relationship between the scalar curvature $S$ and the sectional curvature $K(p)$:

$S(p) = 2K(p)$

Since the scalar curvature $S$ is an intrinsic invariant determined by the metric, so too is $K(p)$. This is a modern restatement of Gauss's famous *Theorema Egregium*.

#### Spaces of Constant Sectional Curvature
A Riemannian manifold $(M^n, g)$ is said to be a **space of [constant sectional curvature](@entry_id:272200)** if the sectional curvature $K(\sigma)$ is the same for all 2-planes $\sigma$ at all points $p \in M$. If this constant value is $k$, we can derive simple expressions for the Ricci and scalar curvatures. By choosing an [orthonormal basis](@entry_id:147779) and summing the sectional curvatures of planes containing a given vector, we find the Ricci tensor is proportional to the metric [@problem_id:3046633]:

$\mathrm{Ric} = (n-1)k g$

Taking the trace of this equation gives the [scalar curvature](@entry_id:157547):

$S = \mathrm{tr}_g(\mathrm{Ric}) = \sum_{i=1}^n (n-1)k g(e_i, e_i) = n(n-1)k$

These formulas are fundamental in Riemannian geometry. They show that for these highly symmetric spaces, the entire curvature tensor is determined by a single number $k$. The model [spaces of constant curvature](@entry_id:161841) are the sphere $S^n$ (for $k>0$), Euclidean space $\mathbb{R}^n$ (for $k=0$), and hyperbolic space $\mathbb{H}^n$ (for $k<0$).

### Curvature Decomposition and Advanced Formulas

In dimensions $n \ge 3$, knowing all sectional curvatures at a point is sufficient to determine the entire Riemann curvature tensor. However, the relationship is more complex than in the [constant curvature](@entry_id:162122) case.

#### The Algebraic Decomposition of Curvature
In dimensions $n \ge 4$, the Riemann tensor $\mathcal{R}$ admits a [canonical decomposition](@entry_id:634116) into three components with distinct geometric interpretations: the **Weyl tensor** $W$, the **traceless Ricci tensor** $\mathrm{Ric}_0$, and the **[scalar curvature](@entry_id:157547)** $S$. The [sectional curvature](@entry_id:159738) $K(\sigma)$ for an orthonormal plane $\sigma = \mathrm{span}\{u,v\}$ reflects this decomposition:

$K(\sigma) = W(u,v,v,u) + \frac{1}{n-2}(\mathrm{Ric}_0(u,u) + \mathrm{Ric}_0(v,v)) + \frac{S}{n(n-1)}$

This formula provides deep insights [@problem_id:3046617]:
- The [sectional curvature](@entry_id:159738) is generally not constant; it depends on the plane-dependent contributions from the Weyl and traceless Ricci tensors.
- A manifold has [constant sectional curvature](@entry_id:272200) at a point if and only if both the Weyl tensor and the traceless Ricci tensor vanish at that point ($W=0$ and $\mathrm{Ric}_0=0$).
- The Ricci curvature can be recovered by averaging sectional curvatures. For any unit vector $X$, the Ricci curvature in that direction is $(n-1)$ times the average of the sectional curvatures of all planes containing $X$:

$\mathrm{Ric}(X,X) = \sum_{i=1}^{n-1} K(\mathrm{span}\{X, e_i\}) = (n-1) \cdot \mathrm{Mean}_{e_i \perp X} K(\mathrm{span}\{X, e_i\})$

This shows that the Ricci tensor is independent of the Weyl tensor, as the averaging process cancels the contribution from the trace-free Weyl component.

#### Riemannian Submersions and O'Neill's Formula
A powerful method for calculating sectional curvatures of complex spaces involves viewing them as the total space of a **Riemannian [submersion](@entry_id:161795)** $\pi: (M, g) \to (B, \bar{g})$. This is a projection map that is a Riemannian [isometry](@entry_id:150881) on horizontal vectors. The [tangent space](@entry_id:141028) $TM$ splits orthogonally into a vertical distribution $\mathcal{V}$ (tangent to fibers) and a [horizontal distribution](@entry_id:196663) $\mathcal{H}$.

The sectional curvatures of the total space $M$ are related to those of the base space $B$ and the geometry of the fibers. A key tool is the **O'Neill [integrability](@entry_id:142415) tensor** $A$, defined for horizontal vector fields $X,Y$ as $A_X Y = v(\nabla_X Y)$, where $v$ denotes projection onto the vertical space $\mathcal{V}$. The tensor $A$ measures the failure of the [horizontal distribution](@entry_id:196663) to be integrable (i.e., whether $[X,Y]$ has a vertical component).

For a horizontal 2-plane in $M$ spanned by orthonormal basic vector fields $X, Y$ which project to $\bar{X}, \bar{Y}$ on $B$, O'Neill's formula gives the [sectional curvature](@entry_id:159738) [@problem_id:3060980]:

$K_M(X,Y) = K_B(\bar{X},\bar{Y}) - 3\|A_X Y\|^2$

This fundamental formula shows that the curvature of the total space $M$ is always less than or equal to the curvature of the base space $B$. The curvature is "pulled down" by an amount proportional to the square of the O'Neill tensor. This term, $-3\|A_X Y\|^2$, quantifies the geometric "twist" of the fibers. This formula is instrumental in computing the curvature of many important manifolds, such as Lie groups, [homogeneous spaces](@entry_id:271488), and complex [projective spaces](@entry_id:157963).