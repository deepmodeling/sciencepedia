## Introduction
In the study of geometry and physics, our ability to describe vectors and physical quantities is fundamental. While Cartesian coordinates offer a simple starting point, the true power of [tensor analysis](@entry_id:184019) is its capacity to operate in any generalized or curvilinear coordinate system. This requires a move beyond fixed basis vectors to a more flexible and intrinsic concept. The central idea that facilitates this transition is the **[coordinate basis](@entry_id:270149) of the tangent space**—a set of basis vectors naturally derived from the coordinate system itself at every point on a surface or in a space.

This article addresses the fundamental challenge of defining and working with vectors in arbitrary coordinate systems. We will move beyond the intuition of flat space to build a robust framework applicable to curved manifolds and diverse physical theories. By mastering the [coordinate basis](@entry_id:270149), you will gain a deeper understanding of the geometric structure of space and the language used in modern physics.

Across the following sections, we will construct this concept from the ground up. In **"Principles and Mechanisms,"** we will formally define the [coordinate basis](@entry_id:270149) vectors, explore their properties through the metric tensor, and introduce the powerful alternative view of vectors as derivative operators. Then, in **"Applications and Interdisciplinary Connections,"** we will see how this framework is essential in fields ranging from general relativity and fluid dynamics to Hamiltonian mechanics. Finally, **"Hands-On Practices"** will offer concrete problems to solidify your computational skills and conceptual understanding.

## Principles and Mechanisms

In our exploration of manifolds and [tensor analysis](@entry_id:184019), the ability to describe vectors and other geometric objects is paramount. While we often begin our studies in the familiar comfort of Cartesian coordinates, the true power of [tensor calculus](@entry_id:161423) lies in its ability to function within any valid coordinate system. This requires us to generalize our notion of basis vectors. This chapter introduces the **[coordinate basis](@entry_id:270149)**, a set of vectors intrinsically tied to a chosen coordinate system, which forms the foundation of the [tangent space](@entry_id:141028) at every point on a manifold.

### The Geometric Definition of Coordinate Basis Vectors

Imagine a point in space. Its position can be described by a set of numbers, the coordinates. In a flat, two-dimensional plane, we might use Cartesian coordinates $(x,y)$. The position vector from the origin to this point is $\mathbf{r} = x\hat{\mathbf{i}} + y\hat{\mathbf{j}}$, where $\hat{\mathbf{i}}$ and $\hat{\mathbf{j}}$ are fixed, orthonormal basis vectors.

Now, let us introduce a new, curvilinear coordinate system, such as the [parabolic coordinates](@entry_id:166304) $(\sigma, \tau)$. The relationship between the Cartesian and [parabolic systems](@entry_id:170606) is given by a set of transformation equations, for instance:
$$
x = \sigma \tau \\
y = \frac{1}{2}(\tau^2 - \sigma^2)
$$
The [position vector](@entry_id:168381) $\mathbf{r}$ can now be seen as a function of these new coordinates, $\mathbf{r}(\sigma, \tau)$.

How do we define basis vectors for this new system? We seek vectors that naturally describe the directions of change along the coordinate grid lines. The most direct way to capture this is through [partial differentiation](@entry_id:194612). We define the **[coordinate basis](@entry_id:270149) vectors**, denoted $\mathbf{e}_\sigma$ and $\mathbf{e}_\tau$, as the [partial derivatives](@entry_id:146280) of the [position vector](@entry_id:168381) with respect to the corresponding coordinates:

$$ \mathbf{e}_{\sigma} = \frac{\partial \mathbf{r}}{\partial \sigma} \quad \text{and} \quad \mathbf{e}_{\tau} = \frac{\partial \mathbf{r}}{\partial \tau} $$

Geometrically, the vector $\mathbf{e}_\sigma$ is tangent to the curve along which $\sigma$ varies while $\tau$ is held constant. Its magnitude indicates how much the [position vector](@entry_id:168381) changes for an infinitesimal change in the coordinate $\sigma$.

Let's make this concrete by calculating these basis vectors for our parabolic coordinate system [@problem_id:1499494]. Using the chain rule, we have:
$$ \mathbf{e}_{\sigma} = \frac{\partial \mathbf{r}}{\partial \sigma} = \frac{\partial x}{\partial \sigma}\hat{\mathbf{i}} + \frac{\partial y}{\partial \sigma}\hat{\mathbf{j}} $$
$$ \mathbf{e}_{\tau} = \frac{\partial \mathbf{r}}{\partial \tau} = \frac{\partial x}{\partial \tau}\hat{\mathbf{i}} + \frac{\partial y}{\partial \tau}\hat{\mathbf{j}} $$

The required partial derivatives are:
$$ \frac{\partial x}{\partial \sigma} = \tau, \quad \frac{\partial y}{\partial \sigma} = -\sigma $$
$$ \frac{\partial x}{\partial \tau} = \sigma, \quad \frac{\partial y}{\partial \tau} = \tau $$

Substituting these back gives the [coordinate basis](@entry_id:270149) vectors in terms of the original Cartesian basis:
$$ \mathbf{e}_{\sigma} = \tau\hat{\mathbf{i}} - \sigma\hat{\mathbf{j}} $$
$$ \mathbf{e}_{\tau} = \sigma\hat{\mathbf{i}} + \tau\hat{\mathbf{j}} $$

Notice a crucial difference from the Cartesian basis: the [coordinate basis](@entry_id:270149) vectors $\mathbf{e}_\sigma$ and $\mathbf{e}_\tau$ are not constant. Their components, and therefore their direction and magnitude, depend on the point $(\sigma, \tau)$ in space. This is a general and fundamental feature of [curvilinear coordinate systems](@entry_id:172561). This same procedure can be used to find the basis vectors for any coordinate system, such as polar, cylindrical [@problem_id:1499507], or [spherical coordinates](@entry_id:146054) [@problem_id:1499516].

### The Tangent Space and Vector Components

At any given point $P$ on our manifold (or in our space), the set of all [coordinate basis](@entry_id:270149) vectors $\{\mathbf{e}_a\}$ forms a complete basis for a vector space called the **[tangent space](@entry_id:141028)** at $P$, denoted $T_P M$. Any vector $\mathbf{V}$ located at point $P$ can be expressed as a unique linear combination of these basis vectors:
$$ \mathbf{V} = V^1 \mathbf{e}_1 + V^2 \mathbf{e}_2 + \dots + V^n \mathbf{e}_n = V^a \mathbf{e}_a $$
Here, we have introduced the **Einstein [summation convention](@entry_id:755635)**, where a repeated index, one upper and one lower, implies summation over all its possible values. The coefficients $V^a$ are called the **contravariant components** of the vector $\mathbf{V}$ in this basis.

A prime example comes from [kinematics](@entry_id:173318). Consider a particle moving along a trajectory $\mathbf{r}(t)$. Its velocity vector is $\mathbf{v} = \frac{d\mathbf{r}}{dt}$. If the particle's path is described by coordinates $u^a(t)$, the chain rule gives:
$$ \mathbf{v} = \frac{\partial \mathbf{r}}{\partial u^a} \frac{du^a}{dt} = \frac{du^a}{dt} \mathbf{e}_a $$
Comparing this to the general form $\mathbf{v} = v^a \mathbf{e}_a$, we find a profound result: the contravariant components of the velocity vector are simply the time derivatives of the coordinates, $v^a = \frac{du^a}{dt}$ [@problem_id:1499500].

This relationship is immensely practical. For example, if a particle's motion is constrained to the surface of a sphere of radius $R$ ($r=R$) and also to a plane $z=Cy$, we can use these constraints to find a relationship between the velocity components. The constraints in [spherical coordinates](@entry_id:146054) become $r=R$ and $R\cos\theta = C(R\sin\theta\sin\phi)$, or $\cos\theta = C\sin\theta\sin\phi$. By differentiating this constraint with respect to time, one can derive a relationship between $\frac{d\theta}{dt}$ and $\frac{d\phi}{dt}$, which directly gives the ratio of the contravariant velocity components $|v^\phi / v^\theta|$ [@problem_id:1499500].

### The Metric Tensor: Encoding Geometry

The [coordinate basis](@entry_id:270149) vectors are generally not orthonormal; they may not be of unit length, nor are they necessarily perpendicular. All information about lengths and angles is encoded in the dot products of these basis vectors. This collection of inner products defines the components of the **metric tensor**.

The components of the metric tensor $g$ in the [coordinate basis](@entry_id:270149) $\{ \mathbf{e}_a \}$ are defined as:
$$ g_{ab} = \mathbf{e}_a \cdot \mathbf{e}_b = \frac{\partial \mathbf{r}}{\partial u^a} \cdot \frac{\partial \mathbf{r}}{\partial u^b} $$
The metric tensor is fundamental because it endows the space with a notion of distance and geometry. The diagonal components, $g_{aa}$ (no sum), give the squared magnitude of the corresponding [basis vector](@entry_id:199546): $|\mathbf{e}_a|^2 = \mathbf{e}_a \cdot \mathbf{e}_a = g_{aa}$. The off-diagonal components, $g_{ab}$ for $a \neq b$, are related to the angle between the basis vectors. Specifically, if $g_{ab}=0$, then the vectors $\mathbf{e}_a$ and $\mathbf{e}_b$ are orthogonal.

Let's return to the parabolic coordinate system to calculate a metric component [@problem_id:1499517]. We found $\mathbf{e}_\sigma = \tau\hat{\mathbf{i}} - \sigma\hat{\mathbf{j}}$. The component $g_{\sigma\sigma}$ is then:
$$ g_{\sigma\sigma} = \mathbf{e}_\sigma \cdot \mathbf{e}_\sigma = (\tau\hat{\mathbf{i}} - \sigma\hat{\mathbf{j}}) \cdot (\tau\hat{\mathbf{i}} - \sigma\hat{\mathbf{j}}) = \tau^2(\hat{\mathbf{i}} \cdot \hat{\mathbf{i}}) + \sigma^2(\hat{\mathbf{j}} \cdot \hat{\mathbf{j}}) = \tau^2 + \sigma^2 $$
This result, $g_{\sigma\sigma} = \sigma^2 + \tau^2$, confirms that the length of the basis vector $\mathbf{e}_\sigma$ varies with position.

As another important example, consider the cylindrical coordinates $(\rho, \phi, z)$ [@problem_id:1499507]. A full calculation of the metric tensor components reveals a diagonal matrix:
$$ g_{ab} = \begin{pmatrix} 1  & 0  & 0 \\ 0  & \rho^2  & 0 \\ 0  & 0  & 1 \end{pmatrix} $$
The fact that the off-diagonal components are zero tells us that the [coordinate basis](@entry_id:270149) vectors $\{\mathbf{e}_\rho, \mathbf{e}_\phi, \mathbf{e}_z\}$ are mutually orthogonal at every point. The components on the diagonal show that while $\mathbf{e}_\rho$ and $\mathbf{e}_z$ are [unit vectors](@entry_id:165907), the magnitude of $\mathbf{e}_\phi$ is $|\mathbf{e}_\phi| = \sqrt{g_{\phi\phi}} = \rho$. The determinant of the metric tensor, $\det(g) = \rho^2$, is related to the volume element for integration in these coordinates, $dV = \sqrt{\det(g)} \,d\rho \,d\phi \,dz = \rho \,d\rho \,d\phi \,dz$.

### Tangent Vectors as Derivative Operators

There is a more abstract and ultimately more powerful way to view [tangent vectors](@entry_id:265494). Instead of geometric arrows, we can define them as **directional derivative operators** that act on scalar functions (or fields).

From this perspective, the [coordinate basis](@entry_id:270149) vector, now denoted $\partial_a$, is simply the partial derivative operator with respect to the coordinate $u^a$:
$$ \partial_a \equiv \frac{\partial}{\partial u^a} $$
The action of this operator on a scalar function $f(u^1, \dots, u^n)$ gives the rate of change of $f$ along the $u^a$ coordinate curve. A general vector $\mathbf{V} = V^a \partial_a$ acts on a function $f$ to produce its [directional derivative](@entry_id:143430) along $\mathbf{V}$:
$$ \mathbf{V}(f) = (V^a \partial_a)f = V^a \frac{\partial f}{\partial u^a} $$

To see this in action, consider a [scalar field](@entry_id:154310) $f(x,y,z) = x^2 + zy$ and the [cylindrical coordinate system](@entry_id:266798) $(\rho, \phi, z)$ [@problem_id:1499482]. To find the action of $\partial_\rho$ on $f$, we first express $f$ in [cylindrical coordinates](@entry_id:271645):
$$ f(\rho, \phi, z) = (\rho \cos\phi)^2 + z(\rho \sin\phi) = \rho^2 \cos^2\phi + z\rho\sin\phi $$
Now, we apply the operator $\partial_\rho$, treating $\phi$ and $z$ as constants:
$$ \partial_\rho(f) = \frac{\partial}{\partial\rho}(\rho^2 \cos^2\phi + z\rho\sin\phi) = 2\rho\cos^2\phi + z\sin\phi $$
This gives the rate of change of the function $f$ as we move purely in the radial direction at any point.

This operator viewpoint beautifully reveals a cornerstone property of coordinate bases. The action of a basis operator $\partial_a$ on one of the coordinate functions $u^b$ of the same system is:
$$ \partial_a(u^b) = \frac{\partial u^b}{\partial u^a} = \delta^b_a $$
where $\delta^b_a$ is the **Kronecker delta**, which is 1 if $a=b$ and 0 otherwise. This may seem trivial by definition, but verifying it explicitly by working in a different coordinate system is highly instructive [@problem_id:1499511]. For example, one can confirm in [polar coordinates](@entry_id:159425) that $\partial_r(r)=1$ and $\partial_r(\theta)=0$ by expressing both the operator $\partial_r = \cos\theta \partial_x + \sin\theta \partial_y$ and the functions $r(x,y) = \sqrt{x^2+y^2}$ and $\theta(x,y)=\arctan(y/x)$ in a Cartesian framework and performing all the differentiations using the [multivariable chain rule](@entry_id:146671). The successful recovery of the Kronecker delta components provides a powerful consistency check on the entire formalism.

### Transformation Laws and Component Types

The essence of a tensor is defined by how its components transform under a [change of coordinates](@entry_id:273139). Let's consider a vector $\mathbf{V}$ and two coordinate systems, $\{u^a\}$ and $\{\bar{u}^i\}$. The vector itself is an invariant geometric object, but its components will be different in each basis.

The **contravariant components** $V^a$ are the coefficients of the basis vectors $\mathbf{e}_a$. They transform according to the **Jacobian matrix** of the [coordinate transformation](@entry_id:138577), $\frac{\partial \bar{u}^i}{\partial u^a}$.
$$ \bar{V}^i = \frac{\partial \bar{u}^i}{\partial u^a} V^a $$
We can also define **covariant components**, denoted with a lower index, by taking the dot product of the vector with the basis vectors:
$$ V_a = \mathbf{V} \cdot \mathbf{e}_a $$
These components have a different transformation rule; they transform with the **inverse Jacobian matrix**, $\frac{\partial u^a}{\partial \bar{u}^i}$ [@problem_id:1499452].
$$ \bar{V}_i = \frac{\partial u^a}{\partial \bar{u}^i} V_a $$

Consider a simple [linear transformation](@entry_id:143080) known as [anisotropic scaling](@entry_id:261477), where $\bar{x}^1 = \alpha_1 x^1$, $\bar{x}^2 = \alpha_2 x^2$, etc. [@problem_id:1499452]. If we have a vector field with constant Cartesian components $V^j$, its covariant components in the new scaled system $(\bar{V}_1, \bar{V}_2, \bar{V}_3)$ are found using the transformation law to be $(\frac{V^1}{\alpha_1}, \frac{V^2}{\alpha_2}, \frac{V^3}{\alpha_3})$.

The metric tensor provides the bridge between contravariant and covariant components. We can "lower an index" or "raise an index" using the metric:
$$ V_a = g_{ab} V^b \quad \text{and} \quad V^a = g^{ab} V_b $$
where $g^{ab}$ are the components of the [inverse metric tensor](@entry_id:275529), defined by $g^{ac}g_{cb} = \delta^a_b$.

It is often convenient in physics and engineering to work with **physical components**, which are projections of a vector onto a set of local *unit* vectors. For a general [coordinate basis](@entry_id:270149) $\mathbf{e}_a$, the corresponding unit vector is $\hat{\mathbf{e}}_a = \mathbf{e}_a / |\mathbf{e}_a| = \mathbf{e}_a / \sqrt{g_{aa}}$ (no sum). The physical component $V_{(\hat{a})}$ is then $V_{(\hat{a})} = \mathbf{V} \cdot \hat{\mathbf{e}}_a$. The relationship between contravariant and physical components can be subtle when the basis is not orthogonal. However, for an [orthogonal basis](@entry_id:264024) like spherical coordinates, the relationship is simple: $V^a = V_{(\hat{a})} / \sqrt{g_{aa}}$ [@problem_id:1499516]. This distinction is vital for correctly interpreting the components of [vector fields](@entry_id:161384) in curvilinear systems.

### Advanced Properties: Commutation and Singularities

The operator view of basis vectors allows us to explore deeper properties. One such property is measured by the **Lie bracket**. For two [vector fields](@entry_id:161384) $X$ and $Y$, their Lie bracket, $[X, Y]$, is another vector field defined by its action on any scalar function $f$:
$$ [X, Y](f) = X(Y(f)) - Y(X(f)) $$
The Lie bracket measures the failure of the flows generated by the [vector fields](@entry_id:161384) to commute. A remarkable and defining property of a [coordinate basis](@entry_id:270149) is that the Lie bracket of any two of its basis vectors is always zero [@problem_id:1499479]:
$$ [\partial_a, \partial_b] = 0 $$
This is a direct consequence of the symmetry of [second partial derivatives](@entry_id:635213) (Clairaut's theorem), as $[\partial_a, \partial_b](f) = \frac{\partial^2 f}{\partial u^a \partial u^b} - \frac{\partial^2 f}{\partial u^b \partial u^a} = 0$ for any [smooth function](@entry_id:158037) $f$. Vector bases for which the Lie bracket does not vanish are called **anholonomic** and cannot be derived from a coordinate system.

Finally, we must acknowledge that not all [coordinate systems](@entry_id:149266) are perfect. A **[coordinate singularity](@entry_id:159160)** occurs at a point where the coordinate system breaks down. This breakdown is mathematically signaled by the [coordinate basis](@entry_id:270149) vectors ceasing to be linearly independent.

The most famous example is the $z$-axis in [spherical coordinates](@entry_id:146054) $(r, \theta, \phi)$ [@problem_id:1499490]. Along the $z$-axis, where $\theta=0$ or $\theta=\pi$, the [azimuthal angle](@entry_id:164011) $\phi$ is undefined. Let's examine the [basis vector](@entry_id:199546) associated with $\phi$:
$$ \partial_\phi = \frac{\partial \mathbf{r}}{\partial \phi} = (-r\sin\theta\sin\phi)\hat{\mathbf{i}} + (r\sin\theta\cos\phi)\hat{\mathbf{j}} $$
The magnitude of this vector is $|\partial_\phi| = \sqrt{g_{\phi\phi}} = r\sin\theta$. As a point approaches the $z$-axis (i.e., as $\theta \to 0^+$ or $\theta \to \pi^-$), the magnitude $|\partial_\phi|$ approaches zero. The basis vector $\partial_\phi$ vanishes, and the set $\{\partial_r, \partial_\theta, \partial_\phi\}$ can no longer span the three-dimensional [tangent space](@entry_id:141028). This [linear dependence](@entry_id:149638) is the hallmark of a [coordinate singularity](@entry_id:159160). It is a flaw in our description, our map, not in the underlying space itself. Understanding the behavior of the [coordinate basis](@entry_id:270149) is therefore essential for identifying the domains of validity for our chosen [coordinate systems](@entry_id:149266).