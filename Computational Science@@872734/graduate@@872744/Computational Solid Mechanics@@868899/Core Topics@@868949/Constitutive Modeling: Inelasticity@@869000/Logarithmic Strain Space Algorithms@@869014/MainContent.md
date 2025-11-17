## Introduction
Logarithmic strain space algorithms represent a cornerstone of modern [computational solid mechanics](@entry_id:169583), providing a powerful and elegant framework for analyzing materials undergoing large deformations. Standard engineering theories are often limited to small strains, but in many real-world scenarios—from [metal forming](@entry_id:188560) to [soft tissue mechanics](@entry_id:199866)—deformations are significant, rendering these simpler models inadequate. The primary challenge lies in handling the complex, nonlinear [kinematics](@entry_id:173318) of [finite strain](@entry_id:749398) and developing [constitutive models](@entry_id:174726), particularly for inelastic behaviors like plasticity, that remain physically meaningful and computationally tractable. The [logarithmic strain](@entry_id:751438), or Hencky strain, offers a unique solution to this problem by creating a space where many of the complexities of [finite deformation](@entry_id:172086) are linearized, allowing for the extension of well-understood small-strain concepts.

This article provides a comprehensive guide to the theory, implementation, and application of [logarithmic strain](@entry_id:751438) space algorithms. Across the following three chapters, you will gain a deep, practical understanding of this essential topic. We will cover:
1.  **Principles and Mechanisms:** A rigorous exploration of the mathematical definition and key properties of [logarithmic strain](@entry_id:751438), its decomposition, and its role in the kinematic framework of [elasto-plasticity](@entry_id:748865).
2.  **Applications and Interdisciplinary Connections:** A survey of how these algorithms are applied to solve complex problems in solid mechanics, material failure, [computer graphics](@entry_id:148077), and multi-physics modeling.
3.  **Hands-On Practices:** A set of guided problems to solidify your understanding by implementing the core computational components of these algorithms.

To build a robust understanding of these powerful techniques, we will begin by exploring the foundational principles and kinematic mechanisms that define the [logarithmic strain](@entry_id:751438) space.

## Principles and Mechanisms

This chapter delves into the fundamental principles and kinematic mechanisms that underpin [logarithmic strain](@entry_id:751438) space algorithms. We will begin by rigorously defining the [logarithmic strain](@entry_id:751438) measure and exploring its fundamental properties. Subsequently, we will examine its decomposition into volumetric and deviatoric parts, a cornerstone for [constitutive modeling](@entry_id:183370). The discussion will then shift to the application of [logarithmic strain](@entry_id:751438) in the challenging context of [finite strain](@entry_id:749398) [elasto-plasticity](@entry_id:748865), elucidating the rationale behind the additive [strain decomposition](@entry_id:186005) and the structure of the associated [numerical algorithms](@entry_id:752770). Finally, we will address key practical aspects of the implementation, including the choice of reference frame and the numerical computation of the [matrix logarithm](@entry_id:169041) itself.

### The Logarithmic Strain Tensor: Definition and Properties

At the heart of any discussion on [finite deformation](@entry_id:172086) is the **[deformation gradient](@entry_id:163749)** $F$, a two-point tensor that maps material line elements from the reference configuration to the current configuration. A fundamental result in [continuum mechanics](@entry_id:155125) is the **[polar decomposition theorem](@entry_id:753554)**, which uniquely splits the deformation gradient into a pure rotation and a pure stretch. Two forms exist:

1.  The **right polar decomposition**, $F = R U$, where $U$ is the **[right stretch tensor](@entry_id:193756)** and $R$ is a [proper rotation](@entry_id:141831) tensor. $U$ is a [symmetric positive-definite](@entry_id:145886) (SPD) tensor that acts on vectors in the reference configuration. It is computed as $U = \sqrt{F^T F}$.

2.  The **left [polar decomposition](@entry_id:149541)**, $F = V R$, where $V$ is the **[left stretch tensor](@entry_id:197330)**. $V$ is also an SPD tensor, but it acts on vectors in the current configuration. It is related to the [right stretch tensor](@entry_id:193756) by the [similarity transformation](@entry_id:152935) $V = R U R^T$.

While several [finite strain measures](@entry_id:185716) can be defined from these tensors, the **Hencky strain**, or **[logarithmic strain](@entry_id:751438)**, has gained prominence in [computational solid mechanics](@entry_id:169583) due to a set of uniquely favorable properties.

#### Definition via Spectral Decomposition

The **Lagrangian [logarithmic strain](@entry_id:751438)** is defined as the principal [matrix logarithm](@entry_id:169041) of the [right stretch tensor](@entry_id:193756) $U$:

$E = \log U$

To understand this definition, we must first address the existence and uniqueness of the [matrix logarithm](@entry_id:169041) [@problem_id:3579087]. The [right stretch tensor](@entry_id:193756) $U$, being symmetric and positive-definite, is guaranteed by the [spectral theorem](@entry_id:136620) to be orthogonally diagonalizable. This means it can be written as:

$U = \sum_{i=1}^{3} \lambda_i \mathbf{N}_i \otimes \mathbf{N}_i$

Here, $\lambda_i$ are the eigenvalues of $U$, known as the **[principal stretches](@entry_id:194664)**, and $\mathbf{N}_i$ form an [orthonormal set](@entry_id:271094) of eigenvectors, representing the **principal directions** of stretch in the reference configuration. A critical property of an SPD tensor is that all its eigenvalues are real and strictly positive ($\lambda_i > 0$).

The principal [matrix logarithm](@entry_id:169041) is then defined via [functional calculus](@entry_id:138358) on this spectral basis. The scalar logarithm function is applied to each of the eigenvalues:

$E = \log U = \sum_{i=1}^{3} (\ln \lambda_i) \mathbf{N}_i \otimes \mathbf{N}_i$

Since all $\lambda_i$ are positive, their natural logarithms are unique, real numbers. This ensures that for any physically admissible deformation, the [logarithmic strain](@entry_id:751438) tensor $E$ is a unique, real, and symmetric tensor. The eigenvalues of $E$ are the logarithmic [principal strains](@entry_id:197797), $e_i = \ln \lambda_i$. This spectral definition provides a direct and robust method for its computation, as will be discussed later [@problem_id:3579153].

#### Key Properties of Logarithmic Strain

The [logarithmic strain](@entry_id:751438) possesses several properties that make it particularly well-suited for both theoretical and computational modeling.

First, it exhibits **additivity for coaxial stretches** [@problem_id:3579088]. If a material undergoes a sequence of pure stretch deformations that share the same principal directions (coaxiality), the total [logarithmic strain](@entry_id:751438) is simply the sum of the logarithmic strains from each step. For a sequence of two such stretches with principal stretch ratios $\lambda_i^{(1)}$ and $\lambda_i^{(2)}$, the total stretch is $\lambda_i = \lambda_i^{(1)}\lambda_i^{(2)}$. The total [logarithmic strain](@entry_id:751438) in this principal direction is $E_i = \ln(\lambda_i) = \ln(\lambda_i^{(1)}\lambda_i^{(2)}) = \ln(\lambda_i^{(1)}) + \ln(\lambda_i^{(2)})$. This intuitive additivity is a feature not shared by other common [finite strain measures](@entry_id:185716), such as the Green-Lagrange strain.

Second, the Lagrangian [logarithmic strain](@entry_id:751438) $E$ is **objective**, or frame-indifferent [@problem_id:3579088]. This means it is unaffected by a [rigid body motion](@entry_id:144691) superposed on the deformed configuration. If the deformation is altered by a rotation $Q$, such that the new [deformation gradient](@entry_id:163749) is $F^{\star} = QF$, the new [right stretch tensor](@entry_id:193756) $U^{\star}$ remains identical to $U$. Consequently, the [logarithmic strain](@entry_id:751438) $E^{\star} = \log U^{\star}$ is also unchanged. This property is crucial, as [constitutive laws](@entry_id:178936) describing intrinsic material behavior must be independent of the observer's reference frame.

#### Lagrangian and Eulerian Measures

Just as we have a right (Lagrangian) and left (Eulerian) [stretch tensor](@entry_id:193200), we can define a corresponding **Eulerian [logarithmic strain](@entry_id:751438)**, denoted by $\ell$:

$\ell = \log V$

The relationship between the Lagrangian strain $E$ and the Eulerian strain $\ell$ follows directly from the kinematic link $V = R U R^T$ [@problem_id:3579120]. Using the covariance property of the [matrix logarithm](@entry_id:169041) under similarity transformations, we find:

$\ell = \log(R U R^T) = R (\log U) R^T = R E R^T$

This equation represents the **push-forward** of the material [strain tensor](@entry_id:193332) $E$ from the reference configuration to the spatial current configuration. It demonstrates that $E$ and $\ell$ are not identical in general. They are related by the [rotation tensor](@entry_id:191990) $R$. As a direct consequence of this [similarity transformation](@entry_id:152935), $E$ and $\ell$ share the same [principal values](@entry_id:189577) (eigenvalues), which are the logarithmic [principal strains](@entry_id:197797) $e_i = \ln \lambda_i$. However, their principal directions are different: if $\mathbf{N}_i$ are the [principal directions](@entry_id:276187) of $E$ in the reference frame, then $\mathbf{n}_i = R \mathbf{N}_i$ are the principal directions of $\ell$ in the current frame. The two measures only coincide in special cases, such as when the deformation involves no rotation ($R=I$) or when the strain is purely isotropic ($E$ is a scalar multiple of the identity tensor) [@problem_id:3579120].

### Volumetric-Deviatoric Decomposition

For many engineering materials, particularly metals and geological materials, it is convenient to decouple the constitutive response into a volumetric part (related to changes in volume) and a deviatoric part (related to changes in shape at constant volume). The [logarithmic strain](@entry_id:751438) framework provides a particularly elegant and powerful way to achieve this split.

The foundation of this decomposition is a remarkable identity connecting the trace of the [logarithmic strain](@entry_id:751438) to the volume change of the deformation [@problem_id:3579117]. The volume ratio, or Jacobian, is given by $J = \det F$. From the polar decomposition, we have $J = \det(RU) = (\det R)(\det U)$. Since $R$ is a [proper rotation](@entry_id:141831), $\det R = 1$, which leaves us with $J = \det U$. The [determinant of a matrix](@entry_id:148198) is the product of its eigenvalues, so $J = \prod \lambda_i$. The trace of the [logarithmic strain](@entry_id:751438) $E$ is the sum of its eigenvalues, $\mathrm{tr}(E) = \sum e_i = \sum \ln \lambda_i$. Using the properties of logarithms, we arrive at the identity:

$\mathrm{tr}(E) = \sum \ln \lambda_i = \ln(\prod \lambda_i) = \ln(\det U) = \ln J$

This exact relationship states that the trace of the Hencky strain is the natural logarithm of the volume ratio.

With this identity, we can define the **volumetric part** of the [logarithmic strain](@entry_id:751438) as a purely spherical tensor:

$E_{\mathrm{vol}} = \frac{1}{3} \mathrm{tr}(E) I = \frac{1}{3} (\ln J) I$

The **deviatoric part**, which is trace-free by construction, is then defined as:

$E_{\mathrm{dev}} = E - E_{\mathrm{vol}} = E - \frac{1}{3} (\ln J) I$

This algebraic split has a direct kinematic interpretation. We can multiplicatively decompose the [right stretch tensor](@entry_id:193756) $U$ into a purely volumetric part and a purely isochoric (volume-preserving) part:

$U = (J^{1/3} I) (J^{-1/3} U) = U_{\mathrm{vol}} U_{\mathrm{iso}}$

Here, $U_{\mathrm{vol}} = J^{1/3} I$ represents a uniform spherical expansion, while $U_{\mathrm{iso}} = J^{-1/3} U$ represents the shape change, as $\det(U_{\mathrm{iso}}) = (J^{-1/3})^3 \det U = J^{-1} J = 1$. The [logarithmic strain](@entry_id:751438) corresponding to this isochoric stretch is:

$\log(U_{\mathrm{iso}}) = \log(J^{-1/3} U) = \log(J^{-1/3}) I + \log U = -\frac{1}{3}(\ln J) I + E = E_{\mathrm{dev}}$

Thus, the deviatoric part of the [logarithmic strain](@entry_id:751438) is precisely the logarithm of the isochoric part of the [stretch tensor](@entry_id:193200) [@problem_id:3579117]. This elegant correspondence is a key reason for the widespread use of Hencky strain in modern [constitutive modeling](@entry_id:183370).

### Logarithmic Strain in Elasto-Plasticity

The most significant application of [logarithmic strain](@entry_id:751438) algorithms is in the field of [finite strain](@entry_id:749398) [elasto-plasticity](@entry_id:748865). The standard kinematic framework begins with the [multiplicative decomposition](@entry_id:199514) of the deformation gradient into an elastic part, $F_e$, and a plastic part, $F_p$:

$F = F_e F_p$

This decomposition implies a conceptual intermediate configuration reached by the plastic deformation $F_p$, which is then elastically deformed by $F_e$ to the final configuration. Correspondingly, we can define elastic and plastic logarithmic strains, $E_e = \log U_e$ and $E_p = \log U_p$.

A central question arises: can the total [logarithmic strain](@entry_id:751438) $E$ be additively decomposed into its elastic and plastic parts, i.e., $E = E_e + E_p$? In general, the answer is no. The exact relationship is highly complex. However, under specific, restrictive conditions, exact additivity holds [@problem_id:3579097]. These conditions are:
1.  The [plastic deformation](@entry_id:139726) must be a pure stretch, implying no plastic rotation ($R_p = I$ in the [polar decomposition](@entry_id:149541) $F_p = R_p U_p$).
2.  The elastic and plastic stretches must be coaxial, meaning they share the same [principal directions](@entry_id:276187) ($[U_e, U_p] = 0$).

When these conditions are met, the total strain becomes $E = E_e + E_p$. In most general loading scenarios, these conditions are not satisfied. The [non-commutativity](@entry_id:153545) of the elastic and [plastic deformation](@entry_id:139726) processes introduces an error. This error can be formally characterized using the Baker-Campbell-Hausdorff (BCH) formula [@problem_id:3579100]. Assuming $R_p=I$ for simplicity, the total strain can be approximated as:

$E = \log(\exp(E_e) \exp(E_p)) \approx E_e + E_p + \frac{1}{2}[E_e, E_p] + \dots$

The approximation $E \approx E_e + E_p$ is therefore reasonable only when the commutator $[E_e, E_p]$ is small, which occurs if the strains themselves are small or if their principal axes are nearly aligned [@problem_id:3579097].

Despite this theoretical complexity, many successful algorithms for [computational plasticity](@entry_id:171377) are founded on an additive decomposition. A rigorous basis for this is found not in the total strains, but in their rates [@problem_id:3579088]. It has been shown that there exists a unique [spin tensor](@entry_id:187346), the **logarithmic spin**, such that the [corotational rate](@entry_id:193173) of the Eulerian log strain $\ell$ is exactly equal to the [rate of deformation tensor](@entry_id:182598) $d$. This powerful result, $\overset{\circ}{\ell} = d$, allows for a rigorous additive split of the rate of deformation into elastic and plastic parts in a corotating frame, forming the basis of so-called "[logarithmic strain](@entry_id:751438) space algorithms."

### Algorithmic Implementation and Practice

While the rate-based formulation is theoretically sound, many practical implementations are based on an elegant and efficient algorithm that works with the total [logarithmic strain](@entry_id:751438) over a [discrete time](@entry_id:637509) step. This approach is often called a **spectral [return mapping algorithm](@entry_id:173819)**.

#### The Return Mapping Algorithm

The algorithm proceeds in an elastic-predictor, plastic-corrector fashion [@problem_id:3579104]. Given the state at the beginning of an increment (e.g., the plastic strain $E_p^n$) and the total deformation at the end of the increment (represented by $E^{n+1}$), the goal is to find the updated state.

1.  **Elastic Predictor:** An elastic trial state is computed by assuming the entire increment is elastic. The trial [elastic strain](@entry_id:189634) is $E_e^{\mathrm{tr}} = E^{n+1} - E_p^n$.
2.  **Yield Check:** A trial stress is computed from $E_e^{\mathrm{tr}}$ using the elastic constitutive law (e.g., $\tau^{\mathrm{tr}} = \mathcal{C}:E_e^{\mathrm{tr}}$). This trial stress is then used to evaluate the [yield function](@entry_id:167970). If it lies within the elastic domain, the step is purely elastic, and the trial state is accepted as final.
3.  **Plastic Corrector:** If the [yield function](@entry_id:167970) is violated, [plastic flow](@entry_id:201346) occurs. The core simplification of the spectral algorithm is to perform the "return" to the [yield surface](@entry_id:175331) in the principal coordinate system of the trial state. The [principal directions](@entry_id:276187) of $E_e^{\mathrm{tr}}$ are computed and then held fixed during the correction. The problem is thus reduced from a complex tensor equation to a much simpler set of scalar equations for the principal stresses and strains. This structure is formally identical to the classical [radial return](@entry_id:754007) algorithms used in small strain plasticity, making it a "small-strain-like" procedure embedded within a [finite strain](@entry_id:749398) framework.

The main drawback of this highly efficient approach is that it is an approximation for general loading paths. By freezing the [principal directions](@entry_id:276187) during the corrector step, the algorithm implicitly neglects any rotation of the principal axes ([plastic spin](@entry_id:188692)) that occurs *within* the increment. This makes the algorithm exact for coaxial loading but introduces an error for non-coaxial loading paths, which can accumulate over time [@problem_id:3579104].

#### Choice of Reference Frame and Numerical Computation

Two final practical questions arise: why are these algorithms based on the Lagrangian strain $E$, and how is it computed?

The preference for the Lagrangian strain $E = \log U$ over the Eulerian strain $\ell = \log V$ for constitutive updates is rooted in the principle of **[material objectivity](@entry_id:177919)** [@problem_id:3579124]. The constitutive law should describe the material's response to pure deformation, isolated from any [rigid body motion](@entry_id:144691). The [right stretch tensor](@entry_id:193756) $U$ (and thus $E$) represents this pure [material deformation](@entry_id:169356) in the reference configuration and is frame-indifferent. By performing the constitutive update on $E$, we are effectively working in an "unrotated" configuration. This provides a fixed material basis for the update within a time step, greatly simplifying the algorithm and automatically satisfying objectivity. Using the spatial strain $\ell$ would require working in the current configuration, whose principal axes rotate with the body, making the algorithm significantly more complex.

Finally, the computation of $E = \log U$ itself is a critical step. While several numerical methods exist for the [matrix logarithm](@entry_id:169041), the **spectral algorithm** is the universally preferred choice in this context [@problem_id:3579099]. The procedure is to first compute the eigenvalues $\lambda_i$ and eigenvectors $\mathbf{N}_i$ of the SPD tensor $U$. The logarithm is then assembled directly from its spectral definition: $E = \sum (\ln \lambda_i) \mathbf{N}_i \otimes \mathbf{N}_i$. This method has three key advantages:
1.  It is numerically robust for SPD matrices.
2.  It inherently preserves the symmetry of the [strain tensor](@entry_id:193332), a property that general-purpose methods like scaling-and-squaring may fail to maintain in [finite-precision arithmetic](@entry_id:637673).
3.  Most importantly, it admits closed-form analytical expressions for its derivative. This allows for the computation of a mathematically **[consistent tangent modulus](@entry_id:168075)**, which is indispensable for achieving the quadratic convergence rate of the global Newton-Raphson solvers used in implicit finite element codes.