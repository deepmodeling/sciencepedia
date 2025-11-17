## Introduction
In the study of Riemannian geometry, the Riemann [curvature tensor](@entry_id:181383) stands as the ultimate measure of how a space deviates from being flat. This tensor, however, is not an arbitrary collection of functions; its structure is governed by a set of profound [internal symmetries](@entry_id:199344) known as the Bianchi identities. This article focuses on the first of these, the algebraic Bianchi identity, to uncover its fundamental role in the architecture of curved spaces. We will address the knowledge gap between simply stating the identity and truly understanding its origin and far-reaching consequences. By exploring this topic, you will gain a deeper appreciation for the intricate and self-consistent nature of [differential geometry](@entry_id:145818).

The journey begins in the "Principles and Mechanisms" chapter, where we will rigorously derive the identity from the definitions of connection and torsion, establishing its deep link to the torsion-free property. Next, in "Applications and Interdisciplinary Connections," we will explore its powerful consequences, from determining the [degrees of freedom of curvature](@entry_id:637907) to ensuring the symmetry of the Ricci tensor and its foundational role in General Relativity. Finally, the "Hands-On Practices" section will provide concrete exercises to solidify your understanding through direct calculation and application.

## Principles and Mechanisms

In our study of Riemannian geometry, the curvature of a manifold is the central object of interest. It encapsulates the manner in which the geometry deviates from that of flat Euclidean space. The Riemann curvature tensor is not an arbitrary object; it is constrained by a set of fundamental relations known as the Bianchi identities. These identities are not arbitrary rules but are profound consequences of the very definitions of curvature and connection. This chapter will focus on the first of these, often called the **algebraic Bianchi identity**, exploring its origins, its various mathematical formulations, and the precise conditions under which it holds.

### The Geometric Stage: Connection, Torsion, and Curvature

Before stating the identity itself, we must clearly define the primary actors. A [smooth manifold](@entry_id:156564) $M$ is endowed with a **linear connection** $\nabla$, an operator that allows us to differentiate [vector fields](@entry_id:161384) along other [vector fields](@entry_id:161384). From this connection, two fundamental tensors arise: the torsion and the curvature.

The **[torsion tensor](@entry_id:204137)** $T$ is a measure of the asymmetry of the connection. For any two [vector fields](@entry_id:161384) $X$ and $Y$, it is defined as:
$$
T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y]
$$
where $[X,Y]$ is the Lie bracket of the [vector fields](@entry_id:161384). The [torsion tensor](@entry_id:204137) is skew-symmetric in its arguments, meaning $T(X,Y) = -T(Y,X)$ [@problem_id:3070490]. A connection is said to be **torsion-free** if $T(X,Y) = 0$ for all vector fields $X$ and $Y$. In this crucial case, the connection becomes symmetric in the sense that the order of [covariant differentiation](@entry_id:263981) is related simply to the Lie bracket: $[X,Y] = \nabla_X Y - \nabla_Y X$.

The **Riemann [curvature tensor](@entry_id:181383)** (or [curvature operator](@entry_id:198006)) $R$ measures the non-commutativity of second covariant derivatives. It quantifies how a vector changes as it is parallel-transported around an infinitesimal loop. For any vector fields $X$, $Y$, and $Z$, the [curvature operator](@entry_id:198006) is defined as:
$$
R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]} Z
$$
From its very definition, the [curvature operator](@entry_id:198006) is skew-symmetric in its first two arguments for any linear connection, with or without torsion: $R(X,Y)Z = -R(Y,X)Z$ [@problem_id:3070490].

In the specific context of a Riemannian manifold $(M,g)$, the **Levi-Civita connection** is the unique connection that is both torsion-free and **[metric-compatible](@entry_id:160255)**, the latter meaning that the metric is preserved under [parallel transport](@entry_id:160671), expressed as $\nabla g = 0$. While many important curvature symmetries rely on both properties, we will discover that the first Bianchi identity has a more fundamental origin.

### The First Bianchi Identity: Statement and Derivation

The first Bianchi identity is a purely algebraic relation that the components of the Riemann [curvature tensor](@entry_id:181383) must satisfy at every point on the manifold. To state it concisely, we use the notation $\mathfrak{S}_{X,Y,Z}$ to denote a cyclic sum over the [vector fields](@entry_id:161384) $X, Y, Z$. That is, for any expression $A(X,Y,Z)$, we have:
$$
\mathfrak{S}_{X,Y,Z} A(X,Y,Z) = A(X,Y,Z) + A(Y,Z,X) + A(Z,X,Y)
$$
For example, applying this to the [curvature operator](@entry_id:198006) $R(X,Y)Z$, the cyclic sum expands as $R(X,Y)Z + R(Y,Z)X + R(Z,X)Y$ [@problem_id:3070507].

The **first Bianchi identity** states that for any [torsion-free connection](@entry_id:181337), this cyclic sum is identically zero:
$$
\mathfrak{S}_{X,Y,Z} R(X,Y)Z = R(X,Y)Z + R(Y,Z)X + R(Z,X)Y = 0
$$
This identity is algebraic because it relates the values of the tensor at a single point, without involving any differentiation of the tensor itself. This is in stark contrast to the second Bianchi identity, which is a differential identity involving $\nabla R$ [@problem_id:3070488].

The proof of this identity is a beautiful demonstration of how fundamental definitions interlock. The key ingredients are the definition of the [curvature tensor](@entry_id:181383), the torsion-free condition, and the Jacobi identity for the Lie bracket of [vector fields](@entry_id:161384), which states $\mathfrak{S}_{X,Y,Z} [X,[Y,Z]] = 0$ [@problem_id:3070519].

**Derivation:**
Let's begin by writing out the cyclic sum of the [curvature operator](@entry_id:198006):
$$
\mathfrak{S}_{X,Y,Z} R(X,Y)Z = \mathfrak{S}_{X,Y,Z} (\nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]} Z)
$$
We can split this into two parts: a sum of [second-order derivative](@entry_id:754598) terms and a sum of Lie bracket terms. Let's analyze the first part. Using the torsion-free condition $[U,V] = \nabla_U V - \nabla_V U$, we can regroup the terms as follows:
$$
\begin{align*}
\mathfrak{S}_{X,Y,Z} (\nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z)  = (\nabla_X \nabla_Y Z - \nabla_X \nabla_Z Y) + (\nabla_Y \nabla_Z X - \nabla_Y \nabla_X Z) + (\nabla_Z \nabla_X Y - \nabla_Z \nabla_Y X) \\
 = \nabla_X (\nabla_Y Z - \nabla_Z Y) + \nabla_Y (\nabla_Z X - \nabla_X Z) + \nabla_Z (\nabla_X Y - \nabla_Y X) \\
 = \nabla_X [Y,Z] + \nabla_Y [Z,X] + \nabla_Z [X,Y] \\
 = \mathfrak{S}_{X,Y,Z} \nabla_X [Y,Z]
\end{align*}
$$
Substituting this back, the full cyclic sum becomes:
$$
\mathfrak{S}_{X,Y,Z} R(X,Y)Z = \mathfrak{S}_{X,Y,Z} \nabla_X [Y,Z] - \mathfrak{S}_{X,Y,Z} \nabla_{[X,Y]} Z
$$
Now, we can relate this expression directly to the Jacobi identity. For a [torsion-free connection](@entry_id:181337), we have for any [vector fields](@entry_id:161384) $U$ and $V$: $\nabla_U V - \nabla_V U = [U,V]$. Applying this with $U=X$ and $V=[Y,Z]$ gives $\nabla_X[Y,Z] - \nabla_{[Y,Z]}X = [X,[Y,Z]]$. Taking the cyclic sum of this equation yields:
$$
\mathfrak{S}_{X,Y,Z} (\nabla_X[Y,Z] - \nabla_{[Y,Z]}X) = \mathfrak{S}_{X,Y,Z} [X,[Y,Z]]
$$
The right-hand side is zero by the Jacobi identity. The left-hand side is precisely the expression we found for $\mathfrak{S}_{X,Y,Z} R(X,Y)Z$, since the second term $\mathfrak{S}_{X,Y,Z} \nabla_{[Y,Z]}X$ is the same as $\mathfrak{S}_{X,Y,Z} \nabla_{[X,Y]}Z$ due to the cyclic nature of the sum. Thus, we conclude:
$$
\mathfrak{S}_{X,Y,Z} R(X,Y)Z = 0
$$
It is critical to observe that this entire derivation relied only on the connection being torsion-free. The metric $g$ and the condition of metric-compatibility ($\nabla g = 0$) were never used [@problem_id:3070474] [@problem_id:3070454] [@problem_id:3070476]. This reveals that the first Bianchi identity is a more fundamental property of symmetric connections than of Riemannian geometry itself. Since the Levi-Civita connection is, by definition, torsion-free, the identity is automatically satisfied on any Riemannian manifold.

### The Crucial Role of Torsion

Understanding why the proof works is as important as the proof itself. The essential ingredient is the torsion-free condition. What happens if we consider a general connection with non-zero torsion $T \neq 0$?

In this case, the cancellations that led to our result fail systematically [@problem_id:3070522]. The relationship $[U,V] = \nabla_U V - \nabla_V U$ no longer holds; instead, we have $[U,V] = \nabla_U V - \nabla_V U - T(U,V)$. Every step in the derivation where we used the simpler relation would now pick up an extra term involving $T$.

A full calculation, which tracks all these additional terms, leads to the **generalized first Bianchi identity**:
$$
\mathfrak{S}_{X,Y,Z} R(X,Y)Z = \mathfrak{S}_{X,Y,Z} \left( (\nabla_X T)(Y,Z) + T(T(X,Y),Z) \right)
$$
Here, $(\nabla_X T)(Y,Z)$ is the covariant derivative of the [torsion tensor](@entry_id:204137). This equation shows that the failure of the cyclic sum of curvature to vanish is precisely quantified by terms involving the torsion and its derivative [@problem_id:3070490] [@problem_id:3070454]. When $T=0$, the right-hand side vanishes, and we recover the simpler identity. This demonstrates that torsion-freeness is the minimal and essential assumption for the algebraic Bianchi identity to hold in its classical form.

### Formulations in Components and Differential Forms

To apply the first Bianchi identity in calculations, it is essential to express it in different mathematical languages.

#### Component Form

Let $\{e_i\}$ be a local [frame field](@entry_id:161781) (e.g., a [coordinate basis](@entry_id:270149) $\{\partial_i\}$). The components of the $(1,3)$ [curvature tensor](@entry_id:181383) are defined by the relation $R(e_k, e_l)e_j = R^i{}_{jkl} e_i$. Substituting the basis vectors $e_j, e_k, e_l$ for $Z, X, Y$ into the identity $R(X,Y)Z + R(Y,Z)X + R(Z,X)Y = 0$, we find that the components must satisfy:
$$
R^i{}_{jkl} + R^i{}_{klj} + R^i{}_{ljk} = 0
$$
This shows that the components of the curvature tensor are cyclic in their last three indices [@problem_id:3070518].

We can also define the fully covariant $(0,4)$ curvature tensor by lowering the first index using the metric:
$$
R_{ijkl} = g(R(e_k, e_l)e_j, e_i) = g_{im} R^m{}_{jkl}
$$
The first Bianchi identity for this tensor then becomes:
$$
R_{ijkl} + R_{iklj} + R_{iljk} = 0
$$
This form of the identity should be carefully contrasted with other symmetries of the $(0,4)$ tensor. For instance, the skew-symmetry in the last two indices, $R_{ijkl} = -R_{ijlk}$, is a direct consequence of the connection being [metric-compatible](@entry_id:160255) ($\nabla g = 0$) and does not hold for a general [torsion-free connection](@entry_id:181337). Similarly, other identities, such as the contracted second Bianchi identity which leads to the conservation of the Einstein tensor ($\nabla^j G_{ij}=0$), also depend critically on metric-compatibility [@problem_id:3070476]. The first Bianchi identity stands apart in its sole dependence on the absence of torsion.

#### Differential Forms

An elegant and powerful perspective is provided by Cartan's formalism of [moving frames](@entry_id:175562). On the bundle of orthonormal frames over the manifold, we can define a set of differential forms: the coframe [1-forms](@entry_id:157984) $\theta^i$, the [connection 1-forms](@entry_id:185893) $\omega^i{}_j$, the torsion [2-forms](@entry_id:188008) $T^i$, and the curvature 2-forms $\Omega^i{}_j$. They are related by Cartan's structure equations:
$$
T^i = d\theta^i + \omega^i{}_j \wedge \theta^j
$$
$$
\Omega^i{}_j = d\omega^i{}_j + \omega^i{}_k \wedge \omega^k{}_j
$$
By taking the [exterior derivative](@entry_id:161900) of the first structure equation and substituting the structure equations into the result, one can derive the generalized first Bianchi identity in this language [@problem_id:3070453]:
$$
dT^i + \omega^i{}_j \wedge T^j = \Omega^i{}_j \wedge \theta^j
$$
The left side is the definition of the exterior covariant derivative of the torsion, $DT^i$. The condition for a connection to be torsion-free is simply $T^i=0$. In this case, the left side of the identity vanishes, and we are left with the remarkably simple statement of the first Bianchi identity in the language of forms [@problem_id:3070495]:
$$
\Omega^i{}_j \wedge \theta^j = 0
$$
This compact expression encapsulates the same algebraic constraint on the curvature tensor, demonstrating its fundamental nature across different mathematical formalisms.

In summary, the first Bianchi identity is a cornerstone of differential geometry. It emerges directly from the foundational definitions of [curvature and torsion](@entry_id:164322)-free connections, imposing a universal algebraic symmetry on the Riemann tensor. Its validity, independent of the metric, underscores its deep structural importance, setting it apart from other curvature identities that rely on the full structure of the Levi-Civita connection.