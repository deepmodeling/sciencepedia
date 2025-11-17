## Introduction
In the fields of solid mechanics and [structural engineering](@entry_id:152273), the ability to predict how a body will deform under applied loads is paramount. This predictive power relies on the concept of a well-posed mathematical model, which requires that a solution not only exists but is also unique. Without uniqueness, any simulation or analytical calculation could yield multiple, contradictory results for the same physical setup, rendering the model unreliable. This article addresses the fundamental question: under what conditions can we be certain that the solution to an elastostatic problem is unique?

We will journey from the physical statement of the problem to its abstract mathematical underpinnings, uncovering the crucial interplay between material properties, boundary conditions, and analytical theorems. This exploration will provide a rigorous foundation for formulating and solving problems in mechanics with confidence.

Across three chapters, this article will build a comprehensive understanding of uniqueness. The first chapter, **"Principles and Mechanisms,"** establishes the theoretical framework, transitioning from the strong and weak forms of the governing equations to the [principle of minimum potential energy](@entry_id:173340) and the critical role of [coercivity](@entry_id:159399) and Korn's inequality. The second chapter, **"Applications and Interdisciplinary Connections,"** explores the practical consequences of this theory in engineering design, numerical methods like FEM, and the analysis of complex systems, while also examining scenarios such as [buckling](@entry_id:162815) where uniqueness breaks down. Finally, **"Hands-On Practices"** will solidify these concepts through guided problems that probe the limits of the uniqueness theorem.

## Principles and Mechanisms

The analysis of elastostatic problems hinges on establishing that a solution not only exists but is also unique under a given set of loads and constraints. Without uniqueness, a mathematical model loses its predictive power. This chapter delves into the fundamental principles and mathematical mechanisms that govern the uniqueness of solutions in linear [elastostatics](@entry_id:198298). We will transition from the physical statement of the problem to its abstract variational formulations and uncover the critical roles played by material properties, boundary conditions, and the mathematical structure of the governing equations.

### The Elastostatic Boundary Value Problem: Strong and Weak Forms

A rigorous discussion of uniqueness begins with a precise formulation of the problem itself. In [continuum mechanics](@entry_id:155125), this is achieved through a set of partial differential equations and associated boundary conditions, collectively known as the strong form of the [boundary value problem](@entry_id:138753).

#### The Strong Formulation

The strong form of the linear elastostatic problem for a body occupying a domain $\Omega \subset \mathbb{R}^d$ is built upon three pillars: balance of momentum, [kinematics](@entry_id:173318), and constitutive response.

1.  **Balance of Linear Momentum:** In the absence of inertial effects (i.e., in a static state), the internal forces within the body must be in equilibrium with any externally applied body forces. This principle is expressed locally by the [equilibrium equation](@entry_id:749057):
    $$ \nabla \cdot \boldsymbol{\sigma} + \boldsymbol{f} = \boldsymbol{0} \quad \text{in } \Omega $$
    Here, $\boldsymbol{\sigma}$ is the symmetric Cauchy stress tensor, which represents the [internal forces](@entry_id:167605), and $\boldsymbol{f}$ is the prescribed body force per unit volume (e.g., gravity).

2.  **Kinematic Relation:** For the class of problems considered in linear elasticity, deformations are assumed to be small. This allows the strain, which measures the local deformation, to be linearly related to the [displacement field](@entry_id:141476) $\boldsymbol{u}$. The appropriate measure is the [infinitesimal strain tensor](@entry_id:167211) $\boldsymbol{\varepsilon}$, defined as the symmetric part of the [displacement gradient](@entry_id:165352):
    $$ \boldsymbol{\varepsilon}(\boldsymbol{u}) = \frac{1}{2} \left( \nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top} \right) $$
    This definition ensures that strain is zero for any [rigid body motion](@entry_id:144691) (translation or rotation), which is a physical necessity as such motions do not deform the body.

3.  **Constitutive Law:** The material's mechanical response is described by a [constitutive law](@entry_id:167255) that relates stress to strain. For a linear elastic material, this relationship is given by the generalized Hooke's Law:
    $$ \boldsymbol{\sigma}(\boldsymbol{u}) = \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{u}) $$
    where $\mathbb{C}$ is the [fourth-order elasticity tensor](@entry_id:188318). This tensor encapsulates the material's stiffness properties. We assume it possesses minor symmetries ($\mathbb{C}_{ijkl} = \mathbb{C}_{jikl} = \mathbb{C}_{ijlk}$) and [major symmetry](@entry_id:198487) ($\mathbb{C}_{ijkl} = \mathbb{C}_{klij}$). The minor symmetries, together with the symmetry of the [strain tensor](@entry_id:193332), ensure that the resulting stress tensor $\boldsymbol{\sigma}$ is symmetric, satisfying the [balance of angular momentum](@entry_id:181848).

To complete the problem description, we must specify boundary conditions on the boundary $\partial\Omega$. Typically, the boundary is partitioned into a region $\Gamma_D$ where displacements are prescribed, and a region $\Gamma_N$ where tractions (forces per unit area) are prescribed [@problem_id:2708890].

-   **Displacement (Dirichlet) Boundary Condition:** On $\Gamma_D$, the displacement is set to a known function $\boldsymbol{u}_D$:
    $$ \boldsymbol{u} = \boldsymbol{u}_D \quad \text{on } \Gamma_D $$
    This is termed an **essential** boundary condition because it must be explicitly enforced on the space of admissible solutions in the variational formulations we will soon discuss.

-   **Traction (Neumann) Boundary Condition:** On $\Gamma_N$, the traction vector $\boldsymbol{t}$ is prescribed. The traction is related to the [internal stress](@entry_id:190887) state via Cauchy's formula, $\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$, where $\boldsymbol{n}$ is the outward [unit normal vector](@entry_id:178851) to the boundary:
    $$ \boldsymbol{\sigma}(\boldsymbol{u})\boldsymbol{n} = \boldsymbol{t} \quad \text{on } \Gamma_N $$
    This is known as a **natural** boundary condition, as it will emerge "naturally" from the mathematical procedure used to derive the [weak form](@entry_id:137295), rather than being directly imposed on the choice of functions.

#### The Weak (Variational) Formulation

The strong form requires finding a displacement field $\boldsymbol{u}$ that is twice differentiable, which is often too restrictive for problems with complex geometries or loading. The weak, or variational, formulation relaxes these smoothness requirements and provides the foundation for powerful numerical methods like the Finite Element Method.

To derive the [weak form](@entry_id:137295), we multiply the [equilibrium equation](@entry_id:749057) by an arbitrary "virtual" displacement, or **test function**, $\boldsymbol{v}$ and integrate over the domain $\Omega$. The [test functions](@entry_id:166589) are chosen from a suitable function space, typically the Sobolev space $H^1(\Omega)^d$. To handle the Dirichlet condition, we require that the [test functions](@entry_id:166589) vanish on the part of the boundary where displacements are prescribed, i.e., $\boldsymbol{v}=\boldsymbol{0}$ on $\Gamma_D$.

Starting with $\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{f}) \cdot \boldsymbol{v} \, d\Omega = 0$, we apply the divergence theorem (a form of integration by parts) to the stress term:
$$ \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, d\Omega - \int_{\Omega} \boldsymbol{\sigma} : \nabla \boldsymbol{v} \, d\Omega + \int_{\partial\Omega} (\boldsymbol{\sigma}\boldsymbol{n}) \cdot \boldsymbol{v} \, d\Gamma = 0 $$
The boundary integral splits over $\Gamma_D$ and $\Gamma_N$. It vanishes on $\Gamma_D$ because we chose $\boldsymbol{v}=\boldsymbol{0}$ there. On $\Gamma_N$, we substitute the traction condition $\boldsymbol{\sigma}\boldsymbol{n}=\boldsymbol{t}$. The term $\boldsymbol{\sigma} : \nabla\boldsymbol{v}$ simplifies to $\boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\boldsymbol{v})$ because $\boldsymbol{\sigma}$ is a symmetric tensor, and the contraction of a [symmetric tensor](@entry_id:144567) with an antisymmetric one is zero.

Substituting the [constitutive law](@entry_id:167255) $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}(\boldsymbol{u})$, we arrive at the [weak formulation](@entry_id:142897): Find a [displacement field](@entry_id:141476) $\boldsymbol{u}$ (satisfying $\boldsymbol{u}=\boldsymbol{u}_D$ on $\Gamma_D$) such that for all admissible [test functions](@entry_id:166589) $\boldsymbol{v}$, the following holds:
$$ \int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{v}) : \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{u}) \, d\Omega = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, d\Omega + \int_{\Gamma_N} \boldsymbol{t} \cdot \boldsymbol{v} \, d\Gamma $$
This equation represents a balance of virtual work: the virtual work done by the internal stresses equals the virtual work done by the external loads. It is common to write this in the abstract form $a(\boldsymbol{u}, \boldsymbol{v}) = \ell(\boldsymbol{v})$, where:
-   $a(\boldsymbol{u}, \boldsymbol{v}) := \int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{v}) : \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{u}) \, d\Omega$ is a **bilinear form** representing the [internal virtual work](@entry_id:172278).
-   $\ell(\boldsymbol{v}) := \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, d\Omega + \int_{\Gamma_N} \boldsymbol{t} \cdot \boldsymbol{v} \, d\Gamma$ is a **[linear functional](@entry_id:144884)** representing the external virtual work.

This weak formulation is equivalent to the strong form under sufficient regularity assumptions on the solution [@problem_id:2708892]. It serves as our primary mathematical arena for analyzing uniqueness.

### The Principle of Minimum Potential Energy

An alternative and physically intuitive route to the [equilibrium equations](@entry_id:172166) is through a [variational principle](@entry_id:145218). For elastic materials, this is the **Principle of Minimum Potential Energy**, which states that among all kinematically admissible displacement fields, the one that satisfies equilibrium minimizes the [total potential energy](@entry_id:185512) of the system.

The [total potential energy](@entry_id:185512) functional, $\Pi(\boldsymbol{u})$, is the sum of the stored elastic strain energy and the potential energy of the applied loads:
$$ \Pi(\boldsymbol{u}) := \frac{1}{2}\int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{u}) : \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{u})\,d\Omega - \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{u} \,d\Omega - \int_{\Gamma_N} \boldsymbol{t} \cdot \boldsymbol{u} \,d\Gamma $$
The first term represents the strain energy. The second two terms represent the work done by body forces and [surface tractions](@entry_id:169207), respectively.

A necessary condition for a displacement field $\boldsymbol{u}$ to be a minimizer of $\Pi$ is that the [first variation](@entry_id:174697) of $\Pi$ must vanish for any admissible perturbation. This is analogous to setting the derivative of a function to zero to find its minimum. This condition, $\delta\Pi = 0$, leads directly to the [weak form](@entry_id:137295) $a(\boldsymbol{u}, \boldsymbol{v}) = \ell(\boldsymbol{v})$, provided that the [bilinear form](@entry_id:140194) $a(\cdot, \cdot)$ is symmetric [@problem_id:2708900]. The symmetry of $a(\boldsymbol{u}, \boldsymbol{v})$ is guaranteed by the **[major symmetry](@entry_id:198487)** of the elasticity tensor, $\mathbb{C}_{ijkl} = \mathbb{C}_{klij}$ [@problem_id:2708888]. Materials described by such a tensor are known as hyperelastic. For these materials, the problems of finding a [weak solution](@entry_id:146017) and finding a minimizer of the potential energy are one and the same.

This equivalence is powerful. Proving the uniqueness of the equilibrium solution becomes equivalent to proving that the potential energy functional $\Pi$ has a unique minimizer.

### The Mathematical Foundation of Uniqueness

#### The Role of Strict Convexity

In calculus, a strictly [convex function](@entry_id:143191) (shaped like a simple bowl) has at most one minimum. The same principle applies to functionals. The uniqueness of an elastostatic solution is guaranteed if the total potential energy functional $\Pi(\boldsymbol{u})$ is **strictly convex**.

The functional $\Pi(\boldsymbol{u})$ is the sum of the [strain energy](@entry_id:162699) term, which is quadratic in $\boldsymbol{u}$, and the load potential, which is linear in $\boldsymbol{u}$. Linear terms do not affect [convexity](@entry_id:138568), so the character of $\Pi$ is determined entirely by the [strain energy](@entry_id:162699) term, $J(\boldsymbol{u}) = \frac{1}{2}a(\boldsymbol{u},\boldsymbol{u})$.

For $J(\boldsymbol{u})$ to be strictly convex, we require that for any two distinct admissible displacements $\boldsymbol{u}_1$ and $\boldsymbol{u}_2$, and any $\lambda \in (0,1)$, the following strict inequality holds:
$$ J(\lambda \boldsymbol{u}_1 + (1-\lambda)\boldsymbol{u}_2)  \lambda J(\boldsymbol{u}_1) + (1-\lambda)J(\boldsymbol{u}_2) $$
The material property that ensures this is the **[positive definiteness](@entry_id:178536)** of the elasticity tensor $\mathbb{C}$ on the space of [symmetric tensors](@entry_id:148092). This property, also called **[strong ellipticity](@entry_id:755529)**, means that the [strain energy density](@entry_id:200085) $W(\boldsymbol{\varepsilon}) = \frac{1}{2}\boldsymbol{\varepsilon} : \mathbb{C} : \boldsymbol{\varepsilon}$ is a strictly positive quantity for any non-zero strain $\boldsymbol{\varepsilon}$. This makes the function $W$ strictly convex in $\boldsymbol{\varepsilon}$.

However, for the functional $J(\boldsymbol{u})$ to be strictly convex in $\boldsymbol{u}$, we need one more condition: the mapping from displacement $\boldsymbol{u}$ to strain $\boldsymbol{\varepsilon}(\boldsymbol{u})$ must be **injective**. That is, if $\boldsymbol{u}_1 \neq \boldsymbol{u}_2$, then we must have $\boldsymbol{\varepsilon}(\boldsymbol{u}_1) \neq \boldsymbol{\varepsilon}(\boldsymbol{u}_2)$. If this holds, the [strict convexity](@entry_id:193965) of the [strain energy density](@entry_id:200085) $W$ carries over to the integrated strain energy functional $J(\boldsymbol{u})$, which in turn makes $\Pi(\boldsymbol{u})$ strictly convex and guarantees a unique minimizer [@problem_id:2708910].

#### Rigid Body Motions: The Source of Non-Uniqueness

The injectivity of the map $\boldsymbol{u} \mapsto \boldsymbol{\varepsilon}(\boldsymbol{u})$ is not guaranteed on all function spaces. The kernel of the strain operator—the set of all displacement fields that produce zero strain—is the space of **[rigid body motions](@entry_id:200666)** $\mathcal{R}$. A [rigid body motion](@entry_id:144691) is a displacement of the form:
$$ \boldsymbol{r}(\boldsymbol{x}) = \boldsymbol{a} + \boldsymbol{R}\boldsymbol{x} $$
where $\boldsymbol{a}$ is a constant translation vector and $\boldsymbol{R}$ is a constant [skew-symmetric matrix](@entry_id:155998) representing an infinitesimal rotation. For any such non-zero motion $\boldsymbol{r}$, we have $\boldsymbol{\varepsilon}(\boldsymbol{r})=\boldsymbol{0}$. This has a profound consequence: the strain energy $a(\boldsymbol{r}, \boldsymbol{r}) = 0$.

If the space of admissible solutions contains these [rigid body motions](@entry_id:200666), the strain energy functional $J(\boldsymbol{u})$ cannot be strictly convex, and uniqueness is lost. If $\boldsymbol{u}^\star$ is a solution, then $\boldsymbol{u}^\star + \boldsymbol{r}$ is also a solution for any $\boldsymbol{r} \in \mathcal{R}$, since adding a rigid motion does not change the strain and thus does not change the stress or the [strain energy](@entry_id:162699).

#### Securing Uniqueness: Eliminating Rigid Body Motions

To guarantee a unique solution, we must formulate the problem in a way that excludes non-trivial [rigid body motions](@entry_id:200666) from the space of possible solutions (or solution differences). The primary physical mechanism for this is to constrain the body's movement using Dirichlet boundary conditions.

If we prescribe the displacement $\boldsymbol{u}=\boldsymbol{0}$ on a portion of the boundary $\Gamma_D$, we are "pinning down" the body. For this pinning to be effective against all rigid translations and rotations, the set $\Gamma_D$ must be sufficiently large. In the context of Sobolev spaces, a single point is not enough. The standard requirement is that $\Gamma_D$ must have a positive **(d-1)-dimensional surface measure** [@problem_id:2708881]. For a 3D problem, this means $\Gamma_D$ must have a positive area; for a 2D problem, a positive length. A non-trivial [rigid body motion](@entry_id:144691) cannot be zero over a set of positive surface measure. Therefore, by imposing homogeneous Dirichlet conditions on such a set $\Gamma_D$, we ensure that the only [rigid body motion](@entry_id:144691) admissible in the solution space is the trivial one, $\boldsymbol{u}=\boldsymbol{0}$. This restores the injectivity of the strain operator and, with it, the uniqueness of the solution.

### Coercivity: The Bridge between Material Properties and Uniqueness

The concept of [strict convexity](@entry_id:193965) provides a clear physical and geometric picture for uniqueness. The modern mathematical theory of PDEs, however, frames the proof of [existence and uniqueness](@entry_id:263101) in the language of [functional analysis](@entry_id:146220), centered on the **Lax-Milgram theorem**. This theorem guarantees a unique solution to the weak problem $a(\boldsymbol{u}, \boldsymbol{v}) = \ell(\boldsymbol{v})$ if the [bilinear form](@entry_id:140194) $a(\cdot, \cdot)$ is continuous and **coercive** on the [solution space](@entry_id:200470).

#### Strong Ellipticity vs. Coercivity

It is crucial to distinguish between the material property of [strong ellipticity](@entry_id:755529) and the functional-analytic property of coercivity [@problem_id:2708895].

-   **Strong Ellipticity** is a pointwise property of the tensor $\mathbb{C}$. It ensures that for any [symmetric tensor](@entry_id:144567) $\boldsymbol{\eta}$, there exists a constant $\alpha  0$ such that $\boldsymbol{\eta} : \mathbb{C} : \boldsymbol{\eta} \ge \alpha |\boldsymbol{\eta}|^2$. Integrating this over the domain gives a lower bound on the strain energy in terms of the $L^2$-norm of the strain:
    $$ a(\boldsymbol{v}, \boldsymbol{v}) = \int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{v}) : \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, d\Omega \ge \alpha \|\boldsymbol{\varepsilon}(\boldsymbol{v})\|_{L^2}^2 $$

-   **Coercivity** (or V-[ellipticity](@entry_id:199972)) is a global property of the bilinear form $a(\cdot, \cdot)$ on a specific function space $V \subset H^1(\Omega)^d$. It requires that there exists a constant $\alpha_V  0$ such that for all $\boldsymbol{v} \in V$:
    $$ a(\boldsymbol{v}, \boldsymbol{v}) \ge \alpha_V \|\boldsymbol{v}\|_{H^1}^2 $$
    The $H^1$-norm, defined as $\|\boldsymbol{v}\|_{H^1}^2 = \|\boldsymbol{v}\|_{L^2}^2 + \|\nabla\boldsymbol{v}\|_{L^2}^2$, includes the displacement itself and its full gradient, not just the symmetric part.

Strong ellipticity provides control over the strain, but [coercivity](@entry_id:159399) requires control over the full $H^1$-norm. The gap between these two is bridged by a cornerstone result in mathematical elasticity: Korn's inequality.

#### Korn's Inequality: The Essential Link

**Korn's inequality** is the theorem that allows us to bound the full $H^1$-norm of a [displacement field](@entry_id:141476) by its strain, provided that [rigid body motions](@entry_id:200666) are controlled [@problem_id:2708893].

There are two key forms of the inequality for a bounded Lipschitz domain $\Omega$:

1.  **Korn's First Inequality:** For any [displacement field](@entry_id:141476) $\boldsymbol{u} \in H^1(\Omega)^d$, there exists a constant $C_K$ such that:
    $$ \|\boldsymbol{u}\|_{H^1} \le C_K \left( \|\boldsymbol{u}\|_{L^2} + \|\boldsymbol{\varepsilon}(\boldsymbol{u})\|_{L^2} \right) $$
    This form shows that the $L^2$-norm of the strain almost controls the full gradient, but with an additional term involving the $L^2$-norm of the displacement itself.

2.  **Korn's Second Inequality:** On a function space $V$ that does not contain any non-trivial [rigid body motions](@entry_id:200666) (such as the space of functions vanishing on a boundary set $\Gamma_D$ of positive measure), the inequality takes a stronger form. There exists a constant $C  0$ such that for all $\boldsymbol{u} \in V$:
    $$ \|\boldsymbol{u}\|_{H^1} \le C \|\boldsymbol{\varepsilon}(\boldsymbol{u})\|_{L^2} $$
    This second form is precisely what is needed. It shows that on a space where [rigid motions](@entry_id:170523) are suppressed, the $L^2$-norm of the strain is equivalent to the full $H^1$-norm.

Combining [strong ellipticity](@entry_id:755529) with Korn's second inequality provides the complete argument for coercivity [@problem_id:2708888] [@problem_id:2708892]:
$$ a(\boldsymbol{u}, \boldsymbol{u}) \ge \alpha \|\boldsymbol{\varepsilon}(\boldsymbol{u})\|_{L^2}^2 \ge \alpha \left( \frac{1}{C} \|\boldsymbol{u}\|_{H^1} \right)^2 = \frac{\alpha}{C^2} \|\boldsymbol{u}\|_{H^1}^2 $$
With $\alpha_V = \alpha/C^2  0$, we establish coercivity. The Lax-Milgram theorem then guarantees that a unique solution exists.

### Special Cases and Further Implications

#### The Pure Neumann Problem

A particularly instructive case arises when no displacements are prescribed, i.e., $\Gamma_D = \emptyset$ [@problem_id:2708891]. In this pure traction problem, the space of admissible solutions $H^1(\Omega)^d$ contains all [rigid body motions](@entry_id:200666).

As a result, the [bilinear form](@entry_id:140194) $a(\cdot, \cdot)$ is not coercive on $H^1(\Omega)^d$, and the potential [energy functional](@entry_id:170311) $\Pi$ is only convex, not strictly convex. The solution for displacement $\boldsymbol{u}$ is not unique; if $\boldsymbol{u}^\star$ is a solution, then so is $\boldsymbol{u}^\star + \boldsymbol{r}$ for any [rigid body motion](@entry_id:144691) $\boldsymbol{r} \in \mathcal{R}$.

Furthermore, a solution exists only if the external loads are **self-equilibrated**. This [compatibility condition](@entry_id:171102) requires the net force and net moment from the body forces and tractions to be zero. Mathematically, this means the load functional must vanish for all rigid motions: $\ell(\boldsymbol{r}) = 0$ for all $\boldsymbol{r} \in \mathcal{R}$ [@problem_id:2708888].

#### Uniqueness of Displacement versus Stress

The non-uniqueness of displacement in the pure Neumann problem does not extend to the [stress and strain](@entry_id:137374) fields. This highlights an important distinction between primary and derived fields in the solution [@problem_id:2708913].

-   **Unique displacement implies unique stress:** If the displacement field $\boldsymbol{u}$ is unique, then its gradient $\nabla \boldsymbol{u}$ and its strain $\boldsymbol{\varepsilon}(\boldsymbol{u})$ are also unique. The linear [constitutive law](@entry_id:167255) $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}(\boldsymbol{u})$ then ensures that the stress field $\boldsymbol{\sigma}$ is also unique. This implication is always true and does not depend on the invertibility of $\mathbb{C}$.

-   **Unique stress and strain do not imply unique displacement:** If the strain field $\boldsymbol{\varepsilon}$ is unique, the displacement is determined only up to a [rigid body motion](@entry_id:144691). This is precisely what happens in the pure Neumann problem: although different solutions for $\boldsymbol{u}$ exist, they all correspond to the same unique strain field $\boldsymbol{\varepsilon}$ and thus the same unique stress field $\boldsymbol{\sigma}$. For the reverse implication (from unique stress to unique strain) to hold, the elasticity tensor $\mathbb{C}$ must be invertible on the space of [symmetric tensors](@entry_id:148092).

In summary, the uniqueness of a solution in linear [elastostatics](@entry_id:198298) is not an automatic guarantee but a consequence of a delicate interplay between the material law ([strong ellipticity](@entry_id:755529)), the boundary conditions (suppression of [rigid motions](@entry_id:170523)), and the deep mathematical structure of the underlying equations (as captured by Korn's inequality).