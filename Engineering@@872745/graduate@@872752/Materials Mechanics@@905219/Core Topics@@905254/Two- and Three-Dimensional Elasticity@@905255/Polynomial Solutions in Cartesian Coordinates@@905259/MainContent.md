## Introduction
Solving [boundary value problems](@entry_id:137204) in linear elasticity is a central challenge in [solid mechanics](@entry_id:164042), yet closed-form analytical solutions are often elusive for all but the simplest geometries. A powerful and systematic approach to bridge this gap involves representing the displacement or stress fields with polynomials. This strategy transforms the governing partial differential equations into a tractable system of algebraic equations, providing a pathway to both exact solutions for canonical problems and the foundational principles of modern computational methods. This article explores the theory and application of polynomial solutions in Cartesian coordinates, offering a comprehensive understanding of this essential technique.

The following chapters will guide you through this topic in a structured manner. In **Principles and Mechanisms**, we will delve into the governing equations of elasticity and demonstrate how a polynomial [ansatz](@entry_id:184384) systematically simplifies them. Next, **Applications and Interdisciplinary Connections** will showcase the method's power by deriving exact solutions for classic problems, explaining its foundational role in the Finite Element Method, and revealing connections to other scientific fields. Finally, **Hands-On Practices** will provide opportunities to apply these concepts to practical engineering problems, solidifying your understanding of this versatile tool.

## Principles and Mechanisms

The solution of [boundary value problems](@entry_id:137204) in [linear elasticity](@entry_id:166983) is fundamentally concerned with finding a displacement, strain, and stress field that simultaneously satisfies the governing [equations of equilibrium](@entry_id:193797), [kinematics](@entry_id:173318), and material constitution throughout a body, while also respecting prescribed boundary conditions. While analytical solutions in [closed form](@entry_id:271343) are available for only a limited set of problems with simple geometries and loadings, a powerful and systematic semi-analytical approach involves positing that the solution can be represented or approximated by polynomials. This chapter elucidates the principles and mechanisms by which the search for a polynomial solution transforms a system of [partial differential equations](@entry_id:143134) into a more tractable system of linear algebraic equations.

### The Governing Equations of Linear Elasticity

The theory of linear elasticity for a homogeneous, isotropic solid rests upon three foundational pillars: [kinematics](@entry_id:173318), kinetics, and [constitutive relations](@entry_id:186508). In a Cartesian coordinate system, these are expressed as follows.

First, the **kinematic relationship** connects the displacement field $\boldsymbol{u}(\boldsymbol{x})$ to the [infinitesimal strain tensor](@entry_id:167211) $\boldsymbol{\varepsilon}(\boldsymbol{x})$. Assuming small displacements and gradients, the strain tensor is the symmetric part of the [displacement gradient](@entry_id:165352):
$$
\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})
$$
where the comma notation $u_{i,j}$ denotes the partial derivative $\partial u_i / \partial x_j$.

Second, the **[balance of linear momentum](@entry_id:193575)**, or kinetics, dictates that in the absence of inertial effects (the quasi-static case), the [internal forces](@entry_id:167605) must be in equilibrium. This leads to the [equilibrium equations](@entry_id:172166):
$$
\sigma_{ij,j} + b_i = 0
$$
where $\boldsymbol{\sigma}$ is the symmetric Cauchy stress tensor and $\boldsymbol{b}$ is the [body force](@entry_id:184443) vector per unit volume [@problem_id:2672520].

Third, the **[constitutive law](@entry_id:167255)** for a homogeneous, isotropic, linearly elastic material is given by Hooke's law, which relates stress to strain via two material constants, the Lamé parameters $\lambda$ and $\mu$:
$$
\sigma_{ij} = \lambda \varepsilon_{kk} \delta_{ij} + 2\mu \varepsilon_{ij}
$$
Here, $\delta_{ij}$ is the Kronecker delta and $\varepsilon_{kk} = \text{tr}(\boldsymbol{\varepsilon})$ is the trace of the strain tensor, representing the [volumetric strain](@entry_id:267252).

By substituting the kinematic and [constitutive relations](@entry_id:186508) into the [equilibrium equation](@entry_id:749057), we can derive a governing equation purely in terms of the [displacement field](@entry_id:141476) $\boldsymbol{u}$. This procedure yields the celebrated **Navier-Cauchy equations** of elasticity:
$$
\mu \nabla^2 \boldsymbol{u} + (\lambda + \mu)\nabla(\nabla \cdot \boldsymbol{u}) + \boldsymbol{b} = \boldsymbol{0}
$$
where $\nabla^2$ is the vector Laplacian. These equations form a system of coupled, second-order, [linear partial differential equations](@entry_id:171085) for the components of the [displacement field](@entry_id:141476) [@problem_id:2672444].

For this system to be mathematically well-posed and physically meaningful, the operator must be **strongly elliptic**. This property is ensured if the Lamé parameters satisfy the conditions $\mu > 0$ and $\lambda + 2\mu > 0$. The parameter $\mu$ is the [shear modulus](@entry_id:167228), and its positivity ensures resistance to shear deformation. The combination $\lambda + 2\mu$ is the P-wave modulus, and its positivity ensures resistance to uniaxial compressive strain. These conditions guarantee that the strain energy stored in the material is positive for any non-zero strain state [@problem_id:2672444].

An alternative [solution path](@entry_id:755046) begins with the stress field. In this approach, one proposes a stress field that satisfies the [equilibrium equations](@entry_id:172166). However, an arbitrary stress field will not necessarily correspond to a physically possible deformation. For the strain field derived from the stresses (via the inverted [constitutive law](@entry_id:167255)) to be integrable into a single-valued, continuous displacement field, it must satisfy the **Saint-Venant compatibility equations**. In Cartesian coordinates, these are a set of 81 (though only 6 are independent) equations relating the second derivatives of the strain components [@problem_id:2672482]:
$$
\varepsilon_{ij,kl} + \varepsilon_{kl,ij} - \varepsilon_{ik,jl} - \varepsilon_{jl,ik} = 0
$$
If a proposed strain field is a polynomial of total degree $n$, each term in the compatibility equations involves second derivatives, resulting in a polynomial of degree $n-2$. Therefore, satisfying compatibility imposes algebraic constraints on the coefficients of the strain polynomial. For $n \le 1$, the compatibility equations are trivially satisfied [@problem_id:2672482].

### The Polynomial Ansatz: From PDEs to Algebra

The central strategy of the polynomial solution method is to assume that each component of the displacement vector $\boldsymbol{u}$ can be expressed as a polynomial of a certain degree in the spatial coordinates. This assumption is known as a **polynomial ansatz**. For a displacement field in $d$ dimensions, we can write each component $u_i$ as a general polynomial of total degree at most $n$:
$$
u_{i}(\boldsymbol{x}) = \sum_{|\alpha| \le n} c_{i\alpha} \boldsymbol{x}^{\alpha}
$$
where $\alpha = (\alpha_1, \dots, \alpha_d)$ is a multi-index of non-negative integers, $|\alpha| = \sum \alpha_j$ is its magnitude (the degree of the monomial), $\boldsymbol{x}^{\alpha} = x_1^{\alpha_1} \cdots x_d^{\alpha_d}$, and $c_{i\alpha}$ are the unknown scalar coefficients we seek to determine [@problem_id:2672472].

The first step in understanding this approach is to appreciate the size of the approximation space. The number of distinct monomials $\boldsymbol{x}^{\alpha}$ of degree at most $n$ in $d$ dimensions is given by the combinatorial formula $\binom{n+d}{d}$. Since the [displacement field](@entry_id:141476) has $d$ components, each with its own set of independent coefficients, the total number of unknown coefficients in the [ansatz](@entry_id:184384) is $d \binom{n+d}{d}$. For common cases in [solid mechanics](@entry_id:164042), this gives:
-   In two dimensions ($d=2$): a total of $2 \binom{n+2}{2} = (n+1)(n+2)$ coefficients.
-   In three dimensions ($d=3$): a total of $3 \binom{n+3}{3} = \frac{1}{2}(n+1)(n+2)(n+3)$ coefficients [@problem_id:2672472].

The power of the polynomial ansatz lies in its effect on the governing PDEs. When a polynomial displacement field is substituted into the Navier-Cauchy equations, all derivatives are also polynomials. The result is a polynomial expression that must equal zero everywhere in the domain. A polynomial is identically zero if and only if the coefficient of each of its monomial terms is zero. This principle transforms the problem from solving a system of PDEs to solving a system of linear algebraic equations for the coefficients $c_{i\alpha}$.

Let us illustrate this mechanism with a concrete example. Consider a 2D problem in the absence of body forces, with a polynomial ansatz of total degree at most $n=2$ [@problem_id:2672411]. The displacement components are:
$$
u(x,y) = a_{00} + a_{10}x + a_{01}y + a_{20}x^2 + a_{11}xy + a_{02}y^2
$$
$$
v(x,y) = b_{00} + b_{10}x + b_{01}y + b_{20}x^2 + b_{11}xy + b_{02}y^2
$$
The 2D Navier-Cauchy equations are:
$$
\mu \nabla^2 u + (\lambda + \mu) \frac{\partial}{\partial x} (\nabla \cdot \boldsymbol{u}) = 0
$$
$$
\mu \nabla^2 v + (\lambda + \mu) \frac{\partial}{\partial y} (\nabla \cdot \boldsymbol{u}) = 0
$$
Substituting the quadratic polynomials into these equations results in expressions that are polynomials of degree zero (i.e., constants). For the first equation, we obtain:
$$
\mu(2a_{20} + 2a_{02}) + (\lambda + \mu)(2a_{20} + b_{11}) = 0
$$
For the second equation:
$$
\mu(2b_{20} + 2b_{02}) + (\lambda + \mu)(a_{11} + 2b_{02}) = 0
$$
These two linear equations are the algebraic constraints that the coefficients of the quadratic terms must satisfy for the polynomial field to be a valid solution. The coefficients of the linear and constant terms ($a_{00}, a_{10}, a_{01}, b_{00}, b_{10}, b_{01}$) do not appear in these constraints and remain unconstrained by the [equilibrium equations](@entry_id:172166) themselves. Initially, the [ansatz](@entry_id:184384) has 12 unknown coefficients. The two derived constraints reduce the dimension of the [solution space](@entry_id:200470) to $12 - 2 = 10$ [@problem_id:2672411].

### Structural Properties of Polynomial Solutions

The space of polynomial solutions possesses a rich internal structure. A particularly useful concept is that of **homogeneous polynomials**. A polynomial field is homogeneous of degree $m$ if it scales as $\lambda^m$ under a dilation of coordinates $\boldsymbol{x} \to \lambda \boldsymbol{x}$. Since spatial differentiation reduces the degree of a polynomial by one, it follows that if the [displacement field](@entry_id:141476) $\boldsymbol{u}$ is a [homogeneous polynomial](@entry_id:178156) of degree $n$, the resulting strain and stress fields, $\boldsymbol{\varepsilon}$ and $\boldsymbol{\sigma}$, will be homogeneous polynomials of degree $n-1$ [@problem_id:2672430].

This structure is especially revealing for low-degree polynomials. The kernel of the strain operator, $\boldsymbol{\varepsilon}(\boldsymbol{u})=\boldsymbol{0}$, defines the set of **[rigid body motions](@entry_id:200666)**—displacements that do not cause any deformation. These motions are affine polynomials (degree $\le 1$) [@problem_id:2672427]:
-   **Translations:** $\boldsymbol{u}(\boldsymbol{x}) = \boldsymbol{c}$, where $\boldsymbol{c}$ is a constant vector (a [homogeneous polynomial](@entry_id:178156) of degree 0).
-   **Infinitesimal Rotations:** $\boldsymbol{u}(\boldsymbol{x}) = \boldsymbol{W}\boldsymbol{x}$, where $\boldsymbol{W}$ is a constant [skew-symmetric matrix](@entry_id:155998) (a [homogeneous polynomial](@entry_id:178156) of degree 1).

In 2D, this gives three [rigid body modes](@entry_id:754366): two translations and one rotation, spanned by $\begin{pmatrix} 1 \\ 0 \end{pmatrix}$, $\begin{pmatrix} 0 \\ 1 \end{pmatrix}$, and $\begin{pmatrix} -y \\ x \end{pmatrix}$. In 3D, there are six modes: three translations and three rotations [@problem_id:2672427].

Since [rigid body motions](@entry_id:200666) produce no strain, they also produce no [strain energy](@entry_id:162699). They form the [nullspace](@entry_id:171336) of the [stiffness matrix](@entry_id:178659) $\boldsymbol{K}$ in numerical formulations like the Finite Element Method. For a problem with no (or insufficient) prescribed [displacement boundary conditions](@entry_id:203261), the stiffness matrix will be singular, or **rank-deficient**, with the dimension of the deficiency equal to the number of unconstrained [rigid body modes](@entry_id:754366) [@problem_id:2672436]. To obtain a unique solution, these modes must be eliminated by imposing a minimal set of constraints. For a 2D body, three independent constraints are required. For example, fixing the displacement at one point ($u(0,0)=0$, $v(0,0)=0$) removes the two translational modes, and fixing a single displacement component at a second point (e.g., $u(0,L_y)=0$) prevents rotation, thus restoring the [stiffness matrix](@entry_id:178659) to full rank [@problem_id:2672436].

The mapping from the space of [homogeneous polynomial](@entry_id:178156) displacements of degree $n$ to the space of [homogeneous polynomial](@entry_id:178156) stresses of degree $n-1$ is injective (one-to-one) for $n \ge 2$. This is because the kernel of this mapping corresponds to [rigid body motions](@entry_id:200666), which are polynomials of degree at most 1. A non-zero polynomial cannot be simultaneously homogeneous of degree $n \ge 2$ and have degree $\le 1$. This injectivity implies that the dimension of the space of valid stress fields of degree $n-1$ is equal to the dimension of the space of displacement fields of degree $n$ [@problem_id:2672430].

### Specialization to Two-Dimensional Problems

Many engineering problems can be idealized as two-dimensional. The two primary models are **plane strain** and **[plane stress](@entry_id:172193)**. While both assume fields are independent of the $z$-coordinate, their underlying assumptions and resulting governing equations differ.

-   **Plane Strain:** Assumes zero out-of-plane displacement, leading to the kinematic constraint $\varepsilon_{zz} = \varepsilon_{xz} = \varepsilon_{yz} = 0$. The governing Navier-Cauchy equations retain the same form as the 3D equations, using the original Lamé parameters $(\lambda, \mu)$ [@problem_id:2672440].

-   **Plane Stress:** Assumes zero out-of-[plane stress](@entry_id:172193) components, $\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0$. This is typical for thin plates loaded in their plane. This stress condition implies a non-zero out-of-plane strain $\varepsilon_{zz} = -\frac{\lambda}{\lambda+2\mu}(\varepsilon_{xx}+\varepsilon_{yy})$. When this is substituted back into the [constitutive law](@entry_id:167255), it yields an effective 2D stress-strain relationship of the same form as plane strain, but with a modified first Lamé parameter:
$$
\lambda^* = \frac{2\lambda\mu}{\lambda+2\mu}
$$
The [shear modulus](@entry_id:167228) $\mu$ remains unchanged. The governing operator for [plane stress](@entry_id:172193) is therefore different from that for [plane strain](@entry_id:167046). The two models become identical only when $\lambda = \lambda^*$, which occurs only if $\lambda=0$, corresponding to a Poisson's ratio of $\nu=0$ [@problem_id:2672440].

For 2D problems without body forces, an elegant alternative to the displacement-based approach is the **Airy stress function**, $\phi(x,y)$. The in-[plane stress](@entry_id:172193) components are defined as derivatives of $\phi$:
$$
\sigma_{xx} = \frac{\partial^2\phi}{\partial y^2}, \quad \sigma_{yy} = \frac{\partial^2\phi}{\partial x^2}, \quad \sigma_{xy} = -\frac{\partial^2\phi}{\partial x \partial y}
$$
With these definitions, the [equilibrium equations](@entry_id:172166) are satisfied automatically. The problem then reduces to ensuring compatibility. When the stress definitions are substituted into the 2D compatibility equation, one finds that $\phi$ must satisfy the **[biharmonic equation](@entry_id:165706)**:
$$
\nabla^4\phi = \frac{\partial^4\phi}{\partial x^4} + 2\frac{\partial^4\phi}{\partial x^2 \partial y^2} + \frac{\partial^4\phi}{\partial y^4} = 0
$$
A remarkable feature of this equation is that any fourth-order derivative of a polynomial of total degree 3 or less is identically zero. Therefore, any bivariate polynomial $\phi(x,y)$ of total degree up to 3 is automatically a biharmonic function and thus generates a valid stress field in the absence of [body forces](@entry_id:174230) [@problem_id:2672452]. For instance, the quadratic polynomial $\phi(x,y) = \frac{T}{2}y^2$ yields the uniform uniaxial stress state $\sigma_{xx} = T$, $\sigma_{yy}=0$, $\sigma_{xy}=0$ [@problem_id:2672452].

### Admissibility and Well-Posedness of Polynomial Solutions

The use of polynomials as trial solutions is not merely a matter of convenience; it is rigorously supported by the mathematical theory of PDEs. The modern framework for analyzing elasticity problems is the **weak or [variational formulation](@entry_id:166033)**, which recasts the problem in an integral form. For the strain [energy integral](@entry_id:166228) to be well-defined and finite, the displacement field $\boldsymbol{u}$ must possess square-integrable first derivatives. The function space containing such fields is the Sobolev space $[H^1(\Omega)]^d$ [@problem_id:2672520].

A key advantage of polynomial functions is their inherent smoothness. On any bounded domain $\Omega$, a polynomial of any finite degree is infinitely differentiable ($C^\infty$) and all its derivatives are bounded. Consequently, any polynomial field automatically belongs to the required function space $[H^1(\Omega)]^d$, making polynomials an admissible choice for [trial functions](@entry_id:756165) in [variational methods](@entry_id:163656) like the Rayleigh-Ritz or Finite Element methods [@problem_id:2672520].

The well-posedness of the problem—the existence, uniqueness, and stability of the solution—is guaranteed by the Lax-Milgram theorem, provided the [bilinear form](@entry_id:140194) associated with the strain energy is coercive. Coercivity is established by Korn's inequality, which holds on spaces where [rigid body motions](@entry_id:200666) have been appropriately constrained. This reinforces the importance of imposing sufficient boundary conditions, such as fixing the displacement on a portion of the boundary with a positive measure, which eliminates all [rigid body modes](@entry_id:754366) and ensures a unique solution [@problem_id:2672520] [@problem_id:2672427].

In summary, the use of Cartesian polynomial solutions provides a robust bridge between the continuous physics of elasticity and the discrete world of algebra. By understanding the structure of the governing equations, the nature of [polynomial spaces](@entry_id:753582), and the role of special solutions like [rigid body modes](@entry_id:754366), one can effectively formulate and solve a wide range of problems in solid mechanics.