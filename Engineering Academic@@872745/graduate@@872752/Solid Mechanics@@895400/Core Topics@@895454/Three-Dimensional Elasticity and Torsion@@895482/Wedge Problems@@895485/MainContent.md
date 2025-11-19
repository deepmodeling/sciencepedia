## Introduction
Wedge-shaped geometries are ubiquitous in engineering components, from simple notches and fillets to complex interfaces in [composite materials](@entry_id:139856). The presence of sharp corners often leads to significant stress concentrations, which can govern the failure and fatigue life of a structure. Understanding and quantifying these stress fields is therefore a critical task in solid mechanics. This article provides a comprehensive theoretical framework for analyzing elastic wedge problems, addressing the challenge of characterizing the stress state, particularly the singular behavior that arises at the wedge vertex.

The following chapters will guide you through this complex topic in a structured manner. First, in **Principles and Mechanisms**, we will establish the mathematical foundation, introducing the Airy stress function, deriving the governing [biharmonic equation](@entry_id:165706), and exploring the powerful Michell solution. Next, **Applications and Interdisciplinary Connections** will demonstrate the practical utility of this theory, showing how it underpins [fracture mechanics](@entry_id:141480), explains failure in [composite materials](@entry_id:139856), and shares deep connections with problems in heat transfer, fluid dynamics, and even atomic physics. Finally, **Hands-On Practices** will offer a series of guided problems to solidify your understanding and bridge the gap between analytical theory and practical implementation.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mathematical mechanisms that govern the behavior of elastic wedges. Building upon the introductory concepts of plane elasticity, we will systematically develop the theoretical framework used to analyze stress and displacement fields in wedge-shaped domains, with a particular focus on the behavior near the wedge vertex, where stress concentrations and singularities often arise.

### The Airy Stress Function in Polar Coordinates

In two-dimensional [linear elasticity](@entry_id:166983), when [body forces](@entry_id:174230) are negligible, the equations of [static equilibrium](@entry_id:163498) can be satisfied identically by introducing a [potential function](@entry_id:268662) known as the **Airy stress function**, denoted by $\Phi$. This powerful mathematical device reduces the problem of finding three stress components to that of finding a single scalar function. For wedge problems, which possess a natural radial and angular geometry, it is most convenient to work in polar coordinates $(r, \theta)$.

In this system, the in-plane stress components—[radial stress](@entry_id:197086) $\sigma_{rr}$, [hoop stress](@entry_id:190931) $\sigma_{\theta\theta}$, and shear stress $\sigma_{r\theta}$—are defined as derivatives of the Airy stress function $\Phi(r, \theta)$ as follows [@problem_id:2711180]:

$$
\sigma_{rr} = \frac{1}{r} \frac{\partial \Phi}{\partial r} + \frac{1}{r^2} \frac{\partial^2 \Phi}{\partial \theta^2}
$$

$$
\sigma_{\theta\theta} = \frac{\partial^2 \Phi}{\partial r^2}
$$

$$
\sigma_{r\theta} = -\frac{\partial}{\partial r} \left( \frac{1}{r} \frac{\partial \Phi}{\partial \theta} \right) = \frac{1}{r^2} \frac{\partial \Phi}{\partial \theta} - \frac{1}{r} \frac{\partial^2 \Phi}{\partial r \partial \theta}
$$

A direct substitution of these definitions into the polar [equilibrium equations](@entry_id:172166) confirms that they are satisfied for any sufficiently [smooth function](@entry_id:158037) $\Phi$.

It is evident from these definitions that the stress field is invariant to the addition of certain terms to $\Phi$. Specifically, since the stresses depend only on second-order derivatives, adding any function that is at most linear in Cartesian coordinates, $\Psi(x,y) = a + b_x x + b_y y$, will leave the stress field entirely unchanged. In [polar coordinates](@entry_id:159425), this corresponds to adding terms of the form $a + r(b_x \cos\theta + b_y \sin\theta)$. These terms, which correspond to rigid-body motions in the associated displacement field, are considered **pure gauge** contributions to $\Phi$ and cannot be determined from [traction boundary conditions](@entry_id:167112) alone [@problem_id:2711192].

Furthermore, consider adding a quadratic term $\Psi = c(x^2+y^2) = cr^2$. This addition produces a uniform, or **hydrostatic**, stress state where $\sigma_{rr} = \sigma_{\theta\theta} = 2c$ and $\sigma_{r\theta} = 0$. This term is not a gauge term, as it generates stress. However, its value is directly fixed by boundary conditions. For instance, in a wedge with traction-free faces, the normal stress $\sigma_{\theta\theta}$ must be zero on the boundaries, which immediately requires that $c=0$. If a uniform pressure $p_0$ were applied, the condition $\sigma_{\theta\theta} = -p_0$ would fix $c = -p_0/2$ [@problem_id:2711192].

### The Governing Biharmonic Equation

While the Airy stress function elegantly satisfies equilibrium, it must also yield a strain field that is compatible, meaning that the strains can be integrated to produce a single-valued, continuous displacement field. For a homogeneous, isotropic, linearly elastic material, this **compatibility condition**, when expressed in terms of stresses, takes the form:

$$
\nabla^2 (\sigma_{rr} + \sigma_{\theta\theta}) = 0
$$

where $\nabla^2$ is the Laplacian operator. By substituting the definitions of the stress components in terms of $\Phi$, we find a remarkable simplification:

$$
\sigma_{rr} + \sigma_{\theta\theta} = \left( \frac{1}{r} \frac{\partial \Phi}{\partial r} + \frac{1}{r^2} \frac{\partial^2 \Phi}{\partial \theta^2} \right) + \frac{\partial^2 \Phi}{\partial r^2} = \nabla^2 \Phi
$$

The sum of the normal stresses is simply the Laplacian of the Airy stress function. Consequently, the [compatibility condition](@entry_id:171102) becomes a single [partial differential equation](@entry_id:141332) for $\Phi$:

$$
\nabla^2 (\nabla^2 \Phi) = \nabla^4 \Phi = 0
$$

This is the celebrated **[biharmonic equation](@entry_id:165706)**. It is the central governing equation for the Airy stress function in 2D [isotropic elasticity](@entry_id:203237) without body forces [@problem_id:2711180]. Crucially, its derivation relies only on equilibrium and compatibility, not on the specific form of the constitutive law that distinguishes [plane stress](@entry_id:172193) from [plane strain](@entry_id:167046). As a result, the [biharmonic equation](@entry_id:165706) and its entire family of solutions are identical for both [plane stress and plane strain](@entry_id:172357) conditions. This has a profound consequence: the stress distribution in a 2D body under specified [traction boundary conditions](@entry_id:167112) is independent of whether the body is in a state of plane stress or [plane strain](@entry_id:167046) [@problem_id:2711211].

### The Michell Solution: A General Framework for Wedges

The solution to the [biharmonic equation](@entry_id:165706) in [polar coordinates](@entry_id:159425) for domains like wedges or the regions around holes was famously provided by J.H. Michell. The **Michell solution** provides a complete set of basis functions, constructed through [separation of variables](@entry_id:148716), that can be superposed to solve any plane elasticity problem in such a domain.

By seeking solutions of the form $\Phi(r, \theta) = r^k g(\theta)$ and requiring single-valued stresses and displacements (which implies $g(\theta)$ is periodic), we find that $g(\theta)$ takes the form of Fourier harmonics, $\cos(n\theta)$ and $\sin(n\theta)$, for integer $n$. This leads to an [indicial equation](@entry_id:165955) for the radial exponent $k$: $(k^2 - n^2)((k-2)^2 - n^2) = 0$. The four roots for $k$ are $n, -n, n+2, -n+2$.

For integers $n \ge 2$, these four roots are distinct. This gives four families of radial dependence: $r^n$, $r^{-n}$, $r^{n+2}$, and $r^{-n+2}$. However, for $n=0$ and $n=1$, the roots coalesce, leading to [repeated roots](@entry_id:151486) and the emergence of logarithmic terms. The complete general solution, encompassing all harmonics, is [@problem_id:2711218]:

$$
\begin{aligned}
\Phi(r,\theta) = (A_{0}\, r^{2}\ln r + B_{0}\, r^{2} + C_{0}\, \ln r + D_0) + (K_0 \theta + K_1 r^2 \theta) \\
+ \big(\alpha_1 r^{3} + \beta_1 r\ln r + \gamma_1 r + \delta_1 r^{-1}\big)\cos\theta + \big(\alpha'_1 r^{3} + \beta'_1 r\ln r + \gamma'_1 r + \delta'_1 r^{-1}\big)\sin\theta \\
+ \sum_{n=2}^{\infty} \Big[ \big(a_{n} r^{n+2} + b_{n} r^{-n+2} + c_{n} r^{n} + d_{n} r^{-n}\big)\cos(n\theta) + \big(a'_{n} r^{n+2} + b'_{n} r^{-n+2} + c'_{n} r^{n} + d'_{n} r^{-n}\big)\sin(n\theta) \Big]
\end{aligned}
$$

The logarithmic terms $r^2 \ln r$, $\ln r$, and $r \ln r$ arise as generalized solutions from the theory of ordinary differential equations when the [characteristic equation](@entry_id:149057) has [repeated roots](@entry_id:151486). Specifically, for the axisymmetric case ($n=0$), the [indicial equation](@entry_id:165955) has roots $0, 0, 2, 2$, yielding the radial functions $1, \ln r, r^2, r^2\ln r$. For the $n=1$ case, the roots are $3, 1, 1, -1$, yielding the radial functions $r^3, r, r\ln r, r^{-1}$ [@problem_id:2711164]. These terms are essential for the mathematical completeness of the solution.

### Physical Admissibility and Boundary Conditions

While the Michell solution provides an infinite set of mathematical possibilities, the physically admissible solution for a specific problem is constrained by boundary conditions and regularity requirements. A well-posed wedge problem requires specifying the domain (e.g., $0  r  R, -\alpha \le \theta \le \alpha$) and conditions on the wedge faces $\theta = \pm \alpha$. If these conditions are inhomogeneous (e.g., prescribed tractions), they must scale as a power law in $r$ to be compatible with a single term of the separated solution [@problem_id:2711197].

A critical consideration is the behavior at the wedge vertex, $r=0$. Depending on the physical situation, different **regularity conditions** are imposed.

- **Bounded Stresses:** A very strong condition is to demand that all stress components remain finite at the vertex. The stress components generated by a term $\Phi \sim r^k$ generally scale as $\sigma \sim r^{k-2}$. For stresses to be bounded as $r \to 0$, we require $k-2 \ge 0$, or $k \ge 2$. Applying this to the Michell solution, we must exclude all negative power terms ($r^{-n}, r^{-n+2}$), the logarithmic terms ($\ln r, r^2 \ln r$), and the $r^n$ family for $n=1$ (which produces singular stresses unless its coefficient is zero). This highly restrictive condition is appropriate for problems without geometric stress concentrators. [@problem_id:2711221]

- **Finite Strain Energy:** A more common and physically motivated condition for problems with sharp corners is to require that the total [strain energy](@entry_id:162699) stored in any small region around the vertex be finite. The [strain energy density](@entry_id:200085) is proportional to $\sigma^2$. For a dominant [eigenfunction](@entry_id:149030) with stress $\sigma \sim r^{\lambda-1}$, the energy density scales as $r^{2(\lambda-1)}$. Integrating over a small sector of radius $\epsilon$ ([area element](@entry_id:197167) $r dr d\theta$) requires the integral $\int_0^\epsilon r^{2(\lambda-1)} r dr = \int_0^\epsilon r^{2\lambda-1} dr$ to converge. This convergence is guaranteed if the exponent is greater than -1, which leads to the condition $\text{Re}(\lambda) > 0$ [@problem_id:2711197]. This is the famous **finite energy condition**. It is less restrictive than requiring bounded stress and allows for integrable stress singularities, which are fundamental to fracture mechanics and notch analysis.

The terms excluded by the bounded-stress condition but allowed by the finite-energy condition are not merely mathematical artifacts. They represent important physical idealizations. For example, a term giving $\sigma \sim r^{-1}$ (from $\lambda=1$ solutions) integrates to a finite force on a small circle around the vertex and thus models a **concentrated point force**. A term giving $\sigma \sim r^{-2}$ (from $\lambda=0$ solutions like $\ln r$) integrates to a finite moment and models a **concentrated couple** [@problem_id:2711221]. Admissibility is also a concern at infinity for exterior problems, where terms that grow, such as $r^2\ln r$, must be excluded to ensure bounded stresses far from the body [@problem_id:2711164].

### Eigenfunction Analysis at the Wedge Tip

For many wedge problems, particularly those with [homogeneous boundary conditions](@entry_id:750371) on the faces (e.g., traction-free), the analysis simplifies to an eigenvalue problem. The solution is sought as a series of [eigenfunctions](@entry_id:154705) of the form $\Phi(r,\theta) = r^{\lambda+1} f(\theta)$. Substituting this into the [biharmonic equation](@entry_id:165706) and applying the boundary conditions on $f(\theta)$ at the wedge faces leads to a [characteristic equation](@entry_id:149057) for the admissible eigenvalues $\lambda$.

The near-tip behavior is dominated by the term with the smallest admissible positive eigenvalue, $\lambda_{\text{min}}$. For this leading term, the stress components exhibit a characteristic power-law dependence [@problem_id:2711215]:

$$
\sigma_{rr} = r^{\lambda-1}\left( (\lambda+1)f(\theta) + f''(\theta) \right)
$$

$$
\sigma_{\theta\theta} = \lambda(\lambda+1)r^{\lambda-1}f(\theta)
$$

$$
\sigma_{r\theta} = -\lambda r^{\lambda-1} f'(\theta)
$$

These equations show that all stress components scale as $r^{\lambda-1}$. If $\lambda1$, the stresses are singular. The amplitude of this singular field is a critical parameter that quantifies the severity of the stress concentration. This amplitude is called the **generalized notch [stress intensity factor](@entry_id:157604)**, $K_{\lambda}$. The asymptotic stress field is written as [@problem_id:2711223]:

$$
\sigma_{ij}(r,\theta) \sim K_{\lambda} r^{\lambda-1} g_{ij}(\theta) \quad \text{as } r \to 0
$$

Here, $g_{ij}(\theta)$ are dimensionless angular distribution functions derived from the eigenfunction $f(\theta)$. A [dimensional analysis](@entry_id:140259) of this relation reveals the physical units of $K_{\lambda}$:

$$
[K_{\lambda}] = [\text{stress}] \cdot [\text{length}]^{1-\lambda}
$$

For the classical crack problem, $\lambda = 1/2$, and the units become $[\text{stress}] \cdot [\text{length}]^{1/2}$, consistent with the standard stress intensity factor $K$ in [fracture mechanics](@entry_id:141480).

### Displacements and Symmetry Considerations

The analysis so far has focused on stress, which is independent of the plane stress versus [plane strain assumption](@entry_id:186003). However, the [displacement field](@entry_id:141476) depends directly on the [constitutive law](@entry_id:167255). The [strain-displacement relations](@entry_id:173321) in [polar coordinates](@entry_id:159425) are [@problem_id:2711172]:

$$
\varepsilon_{rr} = \frac{\partial u_r}{\partial r}, \quad \varepsilon_{\theta\theta} = \frac{u_r}{r} + \frac{1}{r}\frac{\partial u_\theta}{\partial \theta}, \quad \gamma_{r\theta} = \frac{1}{r}\frac{\partial u_r}{\partial \theta} + \frac{\partial u_\theta}{\partial r} - \frac{u_\theta}{r}
$$

The stress-strain (Hooke's law) relations differ for [plane stress and plane strain](@entry_id:172357), involving Young's modulus $E$ and Poisson's ratio $\nu$. This difference is often encapsulated in the **Kolosov constant** $\kappa$, where $\kappa = 3 - 4\nu$ for [plane strain](@entry_id:167046) and $\kappa = (3-\nu)/(1+\nu)$ for plane stress. For a given Airy function $\Phi$, the resulting displacement field $(u_r, u_\theta)$ will be different for the two assumptions. This means that if a problem involves [displacement boundary conditions](@entry_id:203261), the choice between [plane stress and plane strain](@entry_id:172357) is critical from the outset, as it will affect the coefficients determined for the Michell [series expansion](@entry_id:142878) [@problem_id:2711211] [@problem_id:2711172].

Finally, the solution process can be greatly simplified by exploiting symmetry. For a wedge symmetric about the line $\theta=0$, loading can be decomposed into a symmetric part (**Mode I-like**) and an antisymmetric part (**Mode II-like**) [@problem_id:2711224].

- **Mode I-like (Symmetric) Loading:** The deformation is symmetric with respect to the bisector. This implies that the radial displacement $u_r$ and the [normal stresses](@entry_id:260622) $\sigma_{rr}, \sigma_{\theta\theta}$ are **even** functions of $\theta$. The tangential displacement $u_\theta$ and the shear stress $\sigma_{r\theta}$ are **odd** functions of $\theta$. To produce this stress parity, the Airy stress function $\Phi$ must be an even function of $\theta$, meaning it should be constructed from a **cosine series**. A direct consequence is that on the symmetry line $\theta=0$, the [odd components](@entry_id:276582) must vanish: $u_\theta = 0$ and $\sigma_{r\theta}=0$.

- **Mode II-like (Antisymmetric) Loading:** The deformation is antisymmetric. The parities are reversed: $u_r, \sigma_{rr}, \sigma_{\theta\theta}$ are **odd**, while $u_\theta, \sigma_{r\theta}$ are **even**. This requires an Airy function $\Phi$ that is an odd function of $\theta$, constructed from a **sine series**. On the symmetry line $\theta=0$, the [odd components](@entry_id:276582) vanish: $u_r = 0$, $\sigma_{rr} = 0$, and $\sigma_{\theta\theta} = 0$.

By identifying the symmetry of the applied loading, one can pre-select only the relevant half of the Michell basis functions, significantly simplifying the algebraic effort required to satisfy boundary conditions.