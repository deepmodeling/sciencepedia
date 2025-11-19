## Introduction
In the design and safety assessment of engineering structures, determining the ultimate load-[carrying capacity](@entry_id:138018) is a critical task. While a complete elasto-plastic analysis can trace the evolution of [stress and strain](@entry_id:137374) up to failure, this process is often complex and computationally intensive. Limit analysis offers a more direct and powerful alternative, providing tools to calculate the [plastic collapse load](@entry_id:201548) by focusing solely on the ultimate failure state. This approach bypasses the intricacies of deformation history, allowing engineers to efficiently assess [structural integrity](@entry_id:165319) against catastrophic failure.

This article provides a thorough grounding in the theory and application of plastic [limit analysis](@entry_id:188743), structured to build from foundational concepts to practical implementation. The first chapter, **Principles and Mechanisms**, will introduce the idealized [rigid-perfectly plastic](@entry_id:195711) material model and delve into the two cornerstones of the theory: the lower and upper bound theorems. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these theorems are applied to solve real-world problems in [structural engineering](@entry_id:152273), [mechanical design](@entry_id:187253), and geomechanics. Finally, the **Hands-On Practices** chapter will offer a series of guided problems to solidify your understanding and develop practical problem-solving skills.

## Principles and Mechanisms

The analysis of [plastic collapse](@entry_id:191981) is founded upon a set of powerful principles that allow for the direct determination of a structure's ultimate load-[carrying capacity](@entry_id:138018). This is achieved by bypassing the complexities of a full, history-dependent elasto-plastic analysis. The methodology rests on an idealized material model and two fundamental theorems, known as the lower and upper bound theorems, which provide dual perspectives on the collapse state. This chapter elucidates these core principles and the underlying mechanisms that govern them.

### The Idealized Material Model: Rigid-Perfectly Plastic Solids

The foundation of [limit analysis](@entry_id:188743) is the **[rigid-perfectly plastic](@entry_id:195711)** material model. This is an idealization of the behavior of ductile materials, such as metals, designed to capture the essential features of [plastic collapse](@entry_id:191981) while discarding aspects that are of secondary importance at the ultimate load state. In this model, the total strain rate, $\dot{\boldsymbol{\varepsilon}}$, which is generally decomposed into an elastic part, $\dot{\boldsymbol{\varepsilon}}^{e}$, and a plastic part, $\dot{\boldsymbol{\varepsilon}}^{p}$, is simplified by assuming the material is perfectly rigid prior to yielding [@problem_id:2897681].

This "rigid" assumption implies that the [elastic strain](@entry_id:189634) rate is identically zero, $\dot{\boldsymbol{\varepsilon}}^{e} = \mathbf{0}$, for any stress state within the material's yield limit. Consequently, the material exhibits no deformation whatsoever under these conditions, as if its [elastic moduli](@entry_id:171361) (e.g., Young's modulus $E$ and Poisson's ratio $\nu$) were infinite.

The "perfectly plastic" aspect of the model stipulates that the material possesses a well-defined [yield strength](@entry_id:162154), encapsulated by a **yield criterion**. This criterion defines a **[yield surface](@entry_id:175331)** in stress space, represented by a function $f(\boldsymbol{\sigma}) \le 0$, which delineates the boundary of all permissible stress states. Once the stress state reaches this surface (i.e., $f(\boldsymbol{\sigma}) = 0$), [plastic deformation](@entry_id:139726) can occur. The term "perfectly" signifies that there is no strain hardening; the yield surface remains fixed and does not expand with increasing plastic strain. At this point of yielding, the stress remains constant while [plastic flow](@entry_id:201346) proceeds, with the total strain rate being equal to the plastic [strain rate](@entry_id:154778), $\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^{p}$.

This idealization is powerful because the collapse load of a structure is determined solely by its geometry and the plastic properties (i.e., the yield strength) of its material. The elastic properties, which govern deformations prior to collapse, are rendered irrelevant in this framework [@problem_id:2897681].

### The Goal of Limit Analysis: The Collapse Load

To appreciate the purpose of [limit analysis](@entry_id:188743), it is crucial to distinguish between the onset of yielding and the ultimate collapse of a structure. Consider a structure subjected to a [proportional loading](@entry_id:191744), where all external forces are scaled by a single [load factor](@entry_id:637044), $\lambda$. As $\lambda$ increases from zero, the structure initially behaves elastically. The **elastic [proportional limit](@entry_id:196760)**, denoted $\lambda_e$, is the [load factor](@entry_id:637044) at which the yield criterion is first satisfied at some point in the structure [@problem_id:2897730].

For a statically determinate structure, the first yield often signifies collapse, as there are no alternative load paths. However, for most engineering structures, which are statically indeterminate, the onset of local yielding does not imply immediate failure. Instead, as the [load factor](@entry_id:637044) increases beyond $\lambda_e$, the yielded region begins to flow plastically, but it continues to carry its yield-level stress. This allows for a **redistribution of stress** to other parts of the structure that are still behaving elastically. The structure can thus withstand additional load until a sufficient number of regions have yielded to form a **collapse mechanism**, which allows for unbounded (or very large) deformation at a constant load.

The [load factor](@entry_id:637044) at which this occurs is the **[plastic collapse load](@entry_id:201548)**, $\lambda_c$. In general, for [statically indeterminate structures](@entry_id:185344), we have $\lambda_e \le \lambda_c$. Limit analysis provides the tools to calculate $\lambda_c$ directly, without needing to trace the complex evolution of stress and strain from $\lambda=0$ to $\lambda_c$.

### The Fundamental Theorems of Plastic Collapse

The core of [limit analysis](@entry_id:188743) consists of two powerful theorems that "bracket" the true collapse load, $\lambda_c$, from below and above. These are the static (lower bound) and kinematic (upper bound) theorems.

#### The Lower Bound (Static) Theorem

The [lower bound theorem](@entry_id:186840), also known as the safe load theorem, provides a means to determine a load that a structure can safely carry without collapsing. It is stated as follows:

**Any [load factor](@entry_id:637044) corresponding to a [statically admissible stress field](@entry_id:199919) is less than or equal to the true collapse [load factor](@entry_id:637044).**

A stress field $\boldsymbol{\sigma}$ is defined as **statically admissible** if it satisfies three fundamental conditions [@problem_id:2897725]:
1.  **Equilibrium:** The stress field must be in equilibrium with the applied [body forces](@entry_id:174230) at every point within the body.
2.  **Traction Boundary Conditions:** The stress field must balance the prescribed tractions on the boundaries of the body.
3.  **Yield Condition:** The stress at every point in the body must not violate the yield criterion; that is, the stress state must lie within or on the yield surface, $f(\boldsymbol{\sigma}) \le 0$.

If a stress field satisfying these three conditions can be found for a given [load factor](@entry_id:637044) $\lambda_s$, then the theorem guarantees that $\lambda_s \le \lambda_c$. This means the structure will not collapse at load $\lambda_s$. The proof of this theorem is elegant and relies on the properties of a convex yield set. If one assumes for contradiction that collapse occurs at a load $\lambda_{actual}  \lambda_s$, one can simply scale down the known admissible stress field for $\lambda_s$ by the factor $\frac{\lambda_{actual}}{\lambda_s}$. Because the yield set is convex and contains the origin, this scaled-down stress field remains within the yield set while satisfying equilibrium for the load $\lambda_{actual}$, thus contradicting the assumption of collapse [@problem_id:2897725].

The practical application of this theorem involves constructing a trial stress field that satisfies equilibrium and boundary conditions, often through the use of stress potentials like the Airy stress function for 2D problems. Then, one finds the maximum [load factor](@entry_id:637044) $\lambda$ for which this stress field can be adjusted to satisfy the [yield criterion](@entry_id:193897) everywhere. This process provides the best possible lower bound for the given trial field [@problem_id:2897690].

#### The Upper Bound (Kinematic) Theorem

The [upper bound theorem](@entry_id:185343), also known as the unsafe load theorem, approaches the problem from the perspective of motion and energy. It provides a load that is greater than or equal to the true collapse load. The theorem is stated as:

**For any [kinematically admissible velocity field](@entry_id:186813) (collapse mechanism), the [load factor](@entry_id:637044) calculated by equating the rate of work done by external forces to the rate of internal energy dissipation is greater than or equal to the true collapse [load factor](@entry_id:637044).**

This calculation yields an estimated collapse load $\lambda_U$, and the theorem guarantees that $\lambda_U \ge \lambda_c$. To find the best estimate for the true collapse load, one seeks the mechanism that *minimizes* this upper bound. The proof of this theorem relies on the principle of virtual power and the energetic principles of [plastic flow](@entry_id:201346) [@problem_id:2897695].

A **[kinematically admissible velocity field](@entry_id:186813)** $\mathbf{v}$ is a postulated motion of the body at the point of collapse. To be admissible, this trial field must satisfy several conditions [@problem_id:2897705]:
1.  **Velocity Boundary Conditions:** It must satisfy any prescribed velocities on the boundaries (e.g., zero velocity at fixed supports).
2.  **Compatibility and Discontinuities:** The field must be kinematically compatible. This does not require global smoothness. The field can be piecewise smooth, allowing for velocity discontinuities (jumps) across internal surfaces. These jumps represent slip lines or [shear bands](@entry_id:183352), which are common features of [plastic collapse](@entry_id:191981).
3.  **Material Constraints:** The [velocity field](@entry_id:271461) must respect the kinematic constraints imposed by the material's [flow rule](@entry_id:177163). For many metals modeled by von Mises or Tresca criteria, plastic flow is incompressible (volume-preserving). This requires the velocity field to be [divergence-free](@entry_id:190991), $\nabla \cdot \mathbf{v} = 0$. Across a discontinuity surface with normal $\mathbf{n}$, this implies that the normal component of the velocity jump must be zero, $\llbracket \mathbf{v} \rrbracket \cdot \mathbf{n} = 0$.
4.  **Finite Dissipation:** The trial [velocity field](@entry_id:271461) must produce a finite, positive rate of internal energy dissipation.

#### Energetic Foundations and Constitutive Requirements

The validity of the upper and lower bound theorems, particularly their duality, depends on the underlying constitutive assumptions about [plastic flow](@entry_id:201346). The key quantity is the **[plastic dissipation](@entry_id:201273) rate**, defined as the [stress power](@entry_id:182907) per unit volume expended in [plastic deformation](@entry_id:139726), $\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$ [@problem_id:2897707]. The total [stress power](@entry_id:182907), $\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}$, is partitioned into a recoverable rate of elastic [energy storage](@entry_id:264866), $\dot{\psi}^e$, and this irreversible dissipation: $\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} = \dot{\psi}^e + \mathcal{D}$.

The [upper bound theorem](@entry_id:185343) is deeply connected to the **Principle of Maximum Plastic Dissipation**. This principle, which holds for a stable material, states that for a given plastic strain rate $\dot{\boldsymbol{\varepsilon}}^p$, the actual stress state $\boldsymbol{\sigma}$ on the yield surface is the one that maximizes the [plastic dissipation](@entry_id:201273) rate among all possible stress states $\boldsymbol{\tau}$ within the yield set $K$ [@problem_id:2897710]:
$$
\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p = \sup_{\boldsymbol{\tau} \in K} (\boldsymbol{\tau} : \dot{\boldsymbol{\varepsilon}}^p)
$$
This principle is equivalent to the **[associated flow rule](@entry_id:201731)**, which postulates that the plastic [strain rate](@entry_id:154778) vector $\dot{\boldsymbol{\varepsilon}}^p$ is normal to the yield surface $f(\boldsymbol{\sigma})=0$ at the current stress state. For a smooth [yield surface](@entry_id:175331), this is written as:
$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$
where $\dot{\lambda} \ge 0$ is the [plastic multiplier](@entry_id:753519). The non-negativity of [plastic dissipation](@entry_id:201273), $\mathcal{D} \ge 0$, is a direct consequence of this rule for a [convex yield surface](@entry_id:203690) containing the origin [@problem_id:2897707].

The requirement of an [associated flow rule](@entry_id:201731) (or the more general Drucker's stability postulate) is essential for the [upper bound theorem](@entry_id:185343) to provide a rigorous upper bound. Without it, the variational structure of the proof fails [@problem_id:2897654]. Importantly, the [lower bound theorem](@entry_id:186840) is independent of the [flow rule](@entry_id:177163); it relies only on equilibrium and the yield criterion. This means that for a material with a [non-associated flow rule](@entry_id:172454), one can still find a guaranteed safe load, but one cannot find a guaranteed unsafe load using the standard kinematic theorem [@problem_id:2897654].

### Mathematical Foundations: Properties of the Yield Set

The rigorous validity of the classical limit theorems and the equality of the lower and upper bounds (i.e., the absence of a "[duality gap](@entry_id:173383)") depend on three key properties of the yield set $Y$ in stress space [@problem_id:2897700]:

1.  **Convexity:** The yield set must be convex. This mathematical property ensures that if two stress states are safe, any stress state on the line segment connecting them is also safe. Convexity is fundamental to the principle of maximum [plastic dissipation](@entry_id:201273) and underpins the convex duality that links the static (primal) and kinematic (dual) [optimization problems](@entry_id:142739). A non-[convex yield surface](@entry_id:203690) can lead to material instabilities and invalidates the proofs of the theorems.

2.  **Closedness:** The yield set must be closed, meaning it includes its boundary. This ensures that a stress state lying exactly on the yield surface is considered admissible. From a mathematical standpoint, this property is necessary for the existence of solutions to the [variational problems](@entry_id:756445) posed by the theorems; it ensures that suprema and infima can be attained.

3.  **Inclusion of the Origin:** The yield set must contain the zero-stress state ($\boldsymbol{\sigma} = \mathbf{0}$). This is a physical necessity, as it asserts that a body can exist in an unloaded state without yielding. This property anchors the entire analysis, ensuring that the set of safe loads is non-empty (as it contains $\lambda=0$) and that the problem of finding the collapse load is well-posed.

In summary, the two theorems of [limit analysis](@entry_id:188743) provide a powerful framework for structural safety assessment. The [lower bound theorem](@entry_id:186840) offers a conservative estimate of strength by constructing a stress field that is demonstrably safe. The [upper bound theorem](@entry_id:185343) provides an unconservative estimate by calculating the energy dissipated by a postulated failure mechanism. When applied to a [rigid-perfectly plastic](@entry_id:195711) material with a [convex yield surface](@entry_id:203690) and an [associated flow rule](@entry_id:201731), these two bounds converge on the exact collapse load, providing a complete and direct solution for the ultimate capacity of the structure.