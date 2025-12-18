## Introduction
Legendrian [submanifolds](@entry_id:159439) are central objects of study in contact geometry, serving as a critical bridge to the world of symplectic geometry and a foundational concept in [mathematical physics](@entry_id:265403). Their significance lies not only in their rich intrinsic structure but also in their remarkable ability to model physical phenomena, from wavefront propagation in optics to the dynamics of Hamiltonian systems. However, their abstract definition—as submanifolds on which the contact form vanishes—can be challenging to work with directly. This necessitates the development of more tangible tools for their visualization, construction, and analysis.

This article addresses this gap by providing a comprehensive overview of the theory and application of Legendrian submanifolds. It is structured to guide the reader from core principles to advanced applications. First, the chapter on **"Principles and Mechanisms"** will demystify the abstract definition by introducing the two canonical projections—Lagrangian and front—which transform the defining condition into concrete geometric properties. We will explore systematic construction methods, such as Legendrian lifts and generating families, and analyze characteristic invariants. Next, the chapter on **"Applications and Interdisciplinary Connections"** will showcase the power of this framework by connecting it to Hamiltonian dynamics, [singularity theory](@entry_id:160612), and the construction of sophisticated algebraic invariants. Finally, a series of **"Hands-On Practices"** will offer opportunities to solidify these concepts through concrete calculations and examples.

## Principles and Mechanisms

Having introduced the foundational concepts of contact geometry, we now delve into the principles and mechanisms governing the central objects of our study: Legendrian submanifolds. This chapter will elucidate their defining properties, explore canonical methods for their construction, and analyze their characteristic geometric and topological features. We will focus primarily on the standard contact structure on Euclidean space, which serves as the principal local model for all contact manifolds.

### Defining Properties and Projections

Let us consider the standard [contact manifold](@entry_id:1122958) $(\mathbb{R}^{2n+1}, \alpha)$, where the space is equipped with coordinates $(x, y, z)$ with $x=(x_1, \dots, x_n)$, $y=(y_1, \dots, y_n)$, and $z \in \mathbb{R}$. The canonical **contact form** is given by
$$
\alpha = dz - \sum_{i=1}^{n} y_i dx_i
$$
An $n$-dimensional [submanifold](@entry_id:262388) $\Lambda \subset \mathbb{R}^{2n+1}$ is defined as a **Legendrian submanifold** if its [tangent space](@entry_id:141028) at every point is contained within the kernel of the contact form. That is, for every point $p \in \Lambda$, the [tangent space](@entry_id:141028) $T_p\Lambda$ is a subspace of the **contact [hyperplane](@entry_id:636937)** $\xi_p = \ker(\alpha_p)$. This condition is succinctly written as $\alpha|_{T\Lambda} = 0$.

While this intrinsic definition is precise, it is not conducive to visualization. To study Legendrian submanifolds, we employ two canonical projections to lower-dimensional spaces, which transform the abstract condition $\alpha|_{T\Lambda} = 0$ into more tangible geometric properties.

#### The Lagrangian Projection

The **Lagrangian projection** is the map $\pi_L: \mathbb{R}^{2n+1} \to \mathbb{R}^{2n}$ defined by simply forgetting the $z$-coordinate:
$$
\pi_L(x, y, z) = (x, y)
$$
The [target space](@entry_id:143180) $\mathbb{R}^{2n}$ is the standard symplectic vector space, endowed with the symplectic form $\omega = d\lambda = \sum_{i=1}^n dx_i \wedge dy_i$, where $\lambda = \sum_{i=1}^n y_i dx_i$ is the Liouville form. When we project a Legendrian submanifold $\Lambda$ via $\pi_L$, the resulting image possesses a remarkable structure.

A key result is that for any Legendrian submanifold $\Lambda$, its Lagrangian projection $\pi_L(\Lambda)$ is the image of an **exact Lagrangian immersion** into $(\mathbb{R}^{2n}, \omega)$ . Let us unpack this statement. First, the map $\pi_L|_\Lambda: \Lambda \to \mathbb{R}^{2n}$ is an immersion, meaning its differential is everywhere injective. This is because the kernel of $d\pi_L$ is spanned by the vector field $\frac{\partial}{\partial z}$, and the Legendrian condition $\alpha(\frac{\partial}{\partial z})=1 \neq 0$ ensures that this vector field can never be tangent to $\Lambda$.

Second, the image is **Lagrangian**. This means that the [pullback](@entry_id:160816) of the symplectic form $\omega$ to $\Lambda$ vanishes. We can see this through a beautiful identity. The [exterior derivative](@entry_id:161900) of the contact form $\alpha$ relates directly to $\omega$:
$$
d\alpha = d(dz - \sum y_i dx_i) = -\sum dy_i \wedge dx_i = \sum dx_i \wedge dy_i = \pi_L^*\omega
$$
Since $\Lambda$ is Legendrian, the pullback of $\alpha$ to $\Lambda$ is zero. The [pullback](@entry_id:160816) of $d\alpha$ to $\Lambda$ is therefore also zero, as $d$ commutes with [pullbacks](@entry_id:160469): $(\pi_L|_\Lambda)^*\omega = d(\alpha|_\Lambda) = d(0) = 0$.

Third, the immersion is **exact**. This means the pullback of the Liouville form $\lambda$ to $\Lambda$ is an exact 1-form. The Legendrian condition $\alpha|_\Lambda=0$ implies $(dz - \sum y_i dx_i)|_{T\Lambda} = 0$, which can be rearranged to state that on [tangent vectors](@entry_id:265494) to $\Lambda$, $dz = \sum y_i dx_i$. In terms of [pullbacks](@entry_id:160469), this is precisely $(\pi_L|_\Lambda)^*\lambda = d(z|_\Lambda)$. The 1-form is not just closed, but exact, with the function defined by the $z$-coordinate on $\Lambda$ serving as its primitive. However, knowledge of the image $\pi_L(\Lambda)$ as a mere subset of $\mathbb{R}^{2n}$ is insufficient to reconstruct $\Lambda$; one requires the full data of the immersion to integrate this 1-form correctly, particularly across self-intersections .

#### The Front Projection

The second, and in many ways more powerful, projection is the **front projection**. This is the map $\pi_F: \mathbb{R}^{2n+1} \to \mathbb{R}^{n+1}$ defined by forgetting the $y$-coordinates:
$$
\pi_F(x, y, z) = (x, z)
$$
The front projection provides a direct "picture" of the Legendrian in $(x,z)$-space. Its most crucial property is that the "forgotten" coordinates can be recovered from the geometry of the front itself. At any smooth point of the front $\pi_F(\Lambda)$ where we can locally express $z$ as a function of $x$, say $z=f(x)$, the Legendrian condition yields a simple relation. A tangent vector to the graph of $f$ is of the form $v = (v_x, v_z) = (v_x, df \cdot v_x)$. The corresponding tangent vector to $\Lambda$ is $\tilde{v} = (v_x, v_y, df \cdot v_x)$. Applying the [contact form](@entry_id:1122954):
$$
\alpha(\tilde{v}) = (df \cdot v_x) - y \cdot v_x = (df - y) \cdot v_x = 0
$$
For this to hold for all [tangent vectors](@entry_id:265494) $v_x$, we must have $y = df$. In coordinates, this is:
$$
y_i = \frac{\partial z}{\partial x_i}
$$
This relationship is fundamental: the $y$-coordinates of a Legendrian submanifold are the slopes of its front projection . Unlike the Lagrangian projection, the front projection $\pi_F(\Lambda)$ of a generic Legendrian uniquely determines $\Lambda$. One is given the $(x,z)$ coordinates, and the $y$ coordinates can be recovered as derivatives.

A vital distinction between the two projections lies in their singularity structure. While $\pi_L$ is always an immersion, $\pi_F$ is generically not. The points where $\pi_F$ fails to be an immersion are where the [tangent space](@entry_id:141028) $T_p\Lambda$ contains a vector in the kernel of $d\pi_F$, i.e., a "vertical" vector in the $y$-directions. These singularities are not arbitrary; for a generic Legendrian, they are highly structured and are classified by [singularity theory](@entry_id:160612). In the simplest case of a Legendrian curve in $\mathbb{R}^3$ ($n=1$), the generic singularity is a **semicubical cusp**. For instance, the [parametric curve](@entry_id:136303) $(x,z) = (t^2, t^3)$ in the plane is the front of a Legendrian curve, and it exhibits a cusp at the origin . Higher-dimensional Legendrians exhibit singularities such as **swallowtails** and other forms cataloged in Arnold's classification. These singularities are a hallmark of Legendrian geometry.

### Systematic Construction of Legendrian Submanifolds

To develop a rich theory, one needs a robust library of examples. We now turn to two systematic methods for constructing Legendrian submanifolds.

#### The Legendrian Lift from Exact Lagrangians

The first method formalizes the intimate connection between Lagrangian and Legendrian geometry. We begin with an $n$-dimensional manifold $L$ and an exact Lagrangian immersion $i: L \to (\mathbb{R}^{2n}, \omega)$, where the [exactness](@entry_id:268999) is witnessed by a primitive function $f: L \to \mathbb{R}$ such that $i^*\lambda = df$. We can "lift" this object into the contact space $\mathbb{R}^{2n+1}$ to form a Legendrian [submanifold](@entry_id:262388).

The **Legendrian lift** of $(L, i, f)$ is the image of the map $\iota: L \to \mathbb{R}^{2n+1}$ defined by:
$$
\iota(x) = (i(x), f(x))
$$
In this construction, the base coordinates are given by the Lagrangian immersion, and the $z$-coordinate is prescribed by the primitive function. A direct computation confirms that the image is indeed Legendrian . We verify this by pulling back the [contact form](@entry_id:1122954) $\alpha = dz - \lambda$ (using a coordinate system $(q,p,z)$ where $\lambda = \sum p_i dq_i$):
$$
\iota^*\alpha = \iota^*(dz - \lambda) = \iota^*(dz) - \iota^*\lambda
$$
The first term is $\iota^*(dz) = d(\iota^*z) = d(f \circ \iota^{-1}) = df$. For the second term, we note that the map $\iota$ followed by the projection $\pi_L$ back to $\mathbb{R}^{2n}$ is just the original immersion $i$. Thus, $\iota^*\lambda = (\pi_L \circ \iota)^*\lambda = i^*\lambda$. The pullback is therefore:
$$
\iota^*\alpha = df - i^*\lambda
$$
By our initial assumption of exactness, $i^*\lambda = df$, so we conclude that $\iota^*\alpha = df - df = 0$. This confirms the image is Legendrian. This construction provides a direct bridge from the world of symplectic geometry to contact geometry.

#### Construction via Generating Families

A more powerful and flexible method for constructing Legendrians, especially those with intricate front singularities, is through **generating families**. A generating family is a [smooth function](@entry_id:158037) $S: M \times \mathbb{R}^k \to \mathbb{R}$, where $M$ is the $n$-dimensional base manifold (with coordinates $x$) and $\mathbb{R}^k$ is a fiber space (with coordinates $\eta$). The Legendrian [submanifold](@entry_id:262388) $\Lambda_S \subset J^1(M) \cong \mathbb{R}^{2n+1}$ is constructed from the locus where $S$ is critical with respect to the fiber variables. Specifically, $\Lambda_S$ is the set of points $(x, p, z)$ satisfying the relations:
$$
\frac{\partial S}{\partial \eta}(x, \eta) = 0, \quad p = \frac{\partial S}{\partial x}(x, \eta), \quad z = S(x, \eta)
$$
for some $(x, \eta)$ that solves the first equation. The validity of this construction typically requires a non-degeneracy condition on the Hessian of $S$ with respect to $\eta$.

To see why this produces a Legendrian, one can compute the [pullback](@entry_id:160816) of $\alpha = dz - p \cdot dx$ to the fiber-critical locus. The total differential of $z = S(x, \eta)$ is $dz = \frac{\partial S}{\partial x}dx + \frac{\partial S}{\partial \eta}d\eta$. When restricted to the critical set where $\frac{\partial S}{\partial \eta} = 0$, this becomes $dz = \frac{\partial S}{\partial x}dx$. Substituting the relations for $p$ and $z$ into the [contact form](@entry_id:1122954) gives $\alpha = (\frac{\partial S}{\partial x}dx) - (\frac{\partial S}{\partial x})dx = 0$.

The simplest type of Legendrian [submanifold](@entry_id:262388), the 1-jet of a function $f: M \to \mathbb{R}$, denoted $j^1f = \{(x, df_x, f(x)) \mid x \in M\}$, can be realized via a generating family of a particularly simple form: a **quadratic generating family** . Consider the family $F(x, \eta) = f(x) + \frac{1}{2}\|\eta\|^2$. The fiber-critical condition is $\frac{\partial F}{\partial \eta} = \eta = 0$. Substituting $\eta=0$ into the defining relations for the Legendrian gives $p = \frac{\partial F}{\partial x}(x,0) = df_x$ and $z = F(x,0) = f(x)$. This recovers exactly $j^1f$. The front of this Legendrian is simply the graph of $f$, $\{(x, f(x)) \mid x \in M\}$, which is a smooth [submanifold](@entry_id:262388) of $M \times \mathbb{R}$ and has no singularities.

More complex generating families give rise to fronts with singularities. The singularities of the front projection correspond to points where the generating family is degenerate. Consider the family $F(x, \theta) = x\cos\theta + \cos(2\theta)$ over $M=\mathbb{R}$ with fiber $\mathbb{S}^1$ . The fiber-critical condition is $\frac{\partial F}{\partial \theta} = -x\sin\theta - 2\sin(2\theta) = 0$. The front projection fails to be an immersion (i.e., has a [singular point](@entry_id:171198)) when, in addition to the critical condition, the map from the critical locus to the front is singular. For a 1-dimensional fiber, this occurs when $\frac{\partial^2 F}{\partial \theta^2} = 0$. For our example, this second condition is $-x\cos\theta - 4\cos(2\theta) = 0$. Solving this system of two equations for $x$ and $\theta$ reveals the $x$-coordinates above which singularities appear. A calculation shows this occurs only when $x^2 - 16 = 0$, i.e., at $x = \pm 4$. These are the points of the **base [discriminant](@entry_id:152620)** or **[caustic](@entry_id:164959)**.

### Characteristic Features and Invariants

With methods of construction in hand, we can analyze the [intrinsic geometry](@entry_id:158788) and topology of Legendrian [submanifolds](@entry_id:159439).

#### Reeb Chords and Lagrangian Crossings

The dynamics of the [contact manifold](@entry_id:1122958) itself leave an imprint on the Legendrians within it. A key dynamical feature is the **Reeb vector field**, $R$, uniquely defined by the conditions $i_R d\alpha = 0$ and $\alpha(R) = 1$. For the standard form $\alpha=dz - \sum y_i dx_i$, we found $d\alpha = \sum dx_i \wedge dy_i$. The condition $i_R d\alpha = 0$ forces the $x$ and $y$ components of $R$ to be zero, while $\alpha(R)=1$ forces its $z$-component to be 1. Thus, the Reeb vector field is simply:
$$
R = \frac{\partial}{\partial z}
$$
The [integral curves](@entry_id:161858) of $R$ are the vertical lines in $\mathbb{R}^{2n+1}$. A **Reeb chord** of a Legendrian $\Lambda$ is an [integral curve](@entry_id:276251) of $R$ connecting two distinct points of $\Lambda$.

The existence of a Reeb chord has a direct geometric interpretation in the Lagrangian projection. If a Reeb chord connects $p_1 = (x_0, y_0, z_1)$ and $p_2 = (x_0, y_0, z_2)$ in $\Lambda$ (with $z_1 \neq z_2$), then their Lagrangian projections are identical: $\pi_L(p_1) = \pi_L(p_2) = (x_0, y_0)$. This means that a Reeb chord corresponds precisely to a self-intersection point (a double point) of the immersed Lagrangian projection $\pi_L(\Lambda)$ .

The length of a Reeb chord, $T = |z_2 - z_1|$, is a fundamentally important quantity known as its **action**. For example, consider the Legendrian curve in $\mathbb{R}^3$ given by the [parametrization](@entry_id:272587) $x(t) = t^3 - 3t$ and $y(t) = t^2-1$, with $z(t)$ determined by the Legendrian condition $\dot{z} = y\dot{x}$ and $z(0)=0$. This leads to $z(t) = \frac{3}{5}t^5 - 2t^3 + 3t$. A double point in the $(x,y)$ projection occurs for parameter values $t_1, t_2$ where $t_1 \neq t_2$ but $(x(t_1), y(t_1)) = (x(t_2), y(t_2))$. This system yields solutions $t_1 = -t_2$. For instance, $t_1=\sqrt{3}$ and $t_2=-\sqrt{3}$ both give the point $(x,y)=(0,2)$. The endpoints of the corresponding Reeb chord on $\Lambda$ are $(\gamma(\sqrt{3}), \gamma(-\sqrt{3}))$. The action of this chord is $|z(\sqrt{3}) - z(-\sqrt{3})| = |\frac{12\sqrt{3}}{5} - (-\frac{12\sqrt{3}}{5})| = \frac{24\sqrt{3}}{5}$ .

#### Topological Invariants

Beyond local geometric features, Legendrian submanifolds possess global [topological invariants](@entry_id:138526) that classify them up to deformation. For Legendrian knots (the case $n=1, \Lambda \cong S^1$), two classical invariants are the Maslov class and the writhe.

The **Maslov class** $\mu_\Lambda \in H^1(\Lambda; \mathbb{Z})$ measures the winding of the [tangent line](@entry_id:268870) $T_p\Lambda$ within the contact plane $\xi_p$ as $p$ traverses a loop in $\Lambda$. Formally, it is constructed from the **Gauss map** $G: \Lambda \to \text{Lag}(\xi)$, which assigns to each point $p \in \Lambda$ its tangent space $T_p\Lambda$, viewed as a Lagrangian plane in the fiber $\xi_p$. For any loop $\gamma$ in $\Lambda$, one obtains a loop of Lagrangian planes. After choosing a trivialization of the symplectic [vector bundle](@entry_id:157593) $\xi$ over the loop, this becomes a loop in a fixed Lagrangian Grassmannian $\text{Lag}(n)$. The homotopy class of this loop in $\pi_1(\text{Lag}(n)) \cong \mathbb{Z}$ gives an integer, the Maslov index, which is independent of the chosen trivialization. This assignment of an integer to each loop defines the Maslov class. It is an intrinsic invariant of the Legendrian, independent of the specific contact form (as long as the co-orientation is fixed) and any auxiliary structures . Crucially, the Maslov class can be non-zero even when the ambient contact bundle $\xi$ is trivial, as is the case for any Legendrian in $\mathbb{R}^{2n+1}$ .

The **writhe** of a front, $\text{wr}(F)$, is a simpler invariant adapted from [knot theory](@entry_id:141161). For a generic front projection $F$ of a Legendrian knot, the writhe is the sum of signs of all its transverse self-intersection points. The sign of a crossing of two strands with oriented [tangent vectors](@entry_id:265494) $v_1, v_2$ in the $(x,z)$-plane is given by $\text{sign}(\det[v_1, v_2])$. Cusps do not contribute to the writhe.

### Dynamics and Transformations: Legendrian Isotopy

The study of Legendrian [submanifolds](@entry_id:159439) includes understanding how they can be deformed into one another. A **Legendrian isotopy** is a path of Legendrian submanifolds. The projected image of such an isotopy is a "movie" of the front, where the diagram changes according to a set of rules known as **Legendrian Reidemeister moves**.

A sequence of such moves can alter the front's appearance and its writhe. For instance, consider a homotopy that begins with a flat segment of a front. A local "zig-zag" can be introduced by creating a pair of cusps (a Reidemeister I move). Initially, this adds no crossings. If this zig-zag is then pushed through the original segment, two crossings are created (a Reidemeister II move). If the first crossing is created by an upward-sloping branch crossing a [horizontal branch](@entry_id:157478), its sign will be negative. The full process of creating a zig-zag, passing it through a strand, and then annihilating it, forms a closed loop of transformations that ultimately leaves the writhe unchanged. However, the intermediate steps can involve transient changes in the writhe value, illustrating the dynamics of the front under deformations .

A fundamental transformation is **stabilization**, which corresponds to adding a small zig-zag to the front. At the level of generating families, this has a simple algebraic description: one adds a non-degenerate quadratic form in new fiber variables to the original generating family $S(x, \eta)$. For example, if we start with $S$ and form a new family $\widetilde{S}(x, \eta, u, v) = S(x, \eta) + \frac{1}{2}u^2 - \frac{1}{2}v^2$, this corresponds to a stabilization. This algebraic change has a geometric consequence. The co-orientation of the front discriminant at a non-degenerate point is determined by the sign of the determinant of the fiber Hessian. The addition of the [quadratic form](@entry_id:153497) $Q(u,v) = \frac{1}{2}u^2 - \frac{1}{2}v^2$ multiplies the determinant of the Hessian by $\det(\text{Hess}(Q)) = (1)(-1) = -1$. This means that stabilization reverses the co-orientation of the front discriminant . This interplay between algebraic modification of generating families and [geometric transformation](@entry_id:167502) of Legendrian submanifolds is a cornerstone of the modern theory.