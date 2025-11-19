## Introduction
In solid mechanics, understanding and predicting the behavior of materials under complex loading is paramount. While elasticity describes recoverable deformation, [plasticity theory](@entry_id:177023) provides the framework for permanent, irreversible changes. A fundamental component of this theory is the yield criterion, which defines the stress limit for elastic behavior. However, knowing *when* a material yields is only half the story; predicting the *direction* and evolution of the subsequent plastic flow is equally critical for accurate [structural analysis](@entry_id:153861). This is where the concept of the [plastic flow rule](@entry_id:189597) becomes essential, leading to a crucial distinction between 'associated' and 'non-associated' models.

This article provides a comprehensive exploration of these two foundational concepts. We will begin in the **Principles and Mechanisms** chapter by laying out the theoretical groundwork of plasticity, introducing the yield function, [plastic potential](@entry_id:164680), and the loading-unloading conditions that govern material response. From there, we will delve into the critical distinction between associated and [non-associated flow](@entry_id:202786), examining the profound implications of this choice on [material stability](@entry_id:183933) and [thermodynamic consistency](@entry_id:138886). The second chapter, **Applications and Interdisciplinary Connections**, will bridge theory and practice by demonstrating how experimental observations in [geomechanics](@entry_id:175967), materials science, and [structural engineering](@entry_id:152273) dictate the use of one rule over the other, highlighting its impact on modeling everything from soil [dilatancy](@entry_id:201001) to metal anisotropy. Finally, the **Hands-On Practices** chapter will offer a series of guided problems designed to reinforce these concepts, providing practical experience in calculating flow directions and evaluating the trade-offs between different modeling approaches. Through this structured journey, you will gain a deep, functional understanding of one of the most important dichotomies in modern [plasticity theory](@entry_id:177023).

## Principles and Mechanisms

The behavior of rate-independent elastoplastic materials is governed by a set of principles that define the onset of irreversible deformation, the direction of plastic flow, and the evolution of the material's internal state. This chapter delineates the fundamental mechanisms of plasticity, starting from the foundational postulates and culminating in the distinction between associated and [non-associated flow](@entry_id:202786) rules, a concept of paramount importance in both theoretical and applied solid mechanics.

### The Foundational Framework of Plasticity

At its core, the theory of small-strain, [rate-independent plasticity](@entry_id:754082) rests on three pillars: a kinematic assumption, a thermodynamic constraint, and a criterion for yield.

First, the total strain tensor, $\boldsymbol{\varepsilon}$, is assumed to be additively decomposable into an elastic part, $\boldsymbol{\varepsilon}^e$, and a plastic part, $\boldsymbol{\varepsilon}^p$:
$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p
$$
The [elastic strain](@entry_id:189634) is related to the stress, $\boldsymbol{\sigma}$, through a constitutive law, typically derived from a stored energy potential, while the plastic strain represents permanent, irrecoverable deformation.

Second, all [constitutive models](@entry_id:174726) must adhere to the [second law of thermodynamics](@entry_id:142732). For isothermal processes, this is expressed through the Clausius-Duhem inequality, which mandates that the rate of internal dissipation must be non-negative. Within the standard framework, this leads to the requirement of non-negative **[plastic dissipation](@entry_id:201273)**, $\mathcal{D}^p \ge 0$. In its most general form, accounting for energy stored due to changes in the material's internal structure, the [plastic dissipation](@entry_id:201273) is given by:
$$
\mathcal{D}^p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p + \boldsymbol{X} \cdot \dot{\boldsymbol{\alpha}} \ge 0
$$
Here, $\dot{\boldsymbol{\varepsilon}}^p$ is the rate of plastic straining, $\boldsymbol{\alpha}$ represents a set of [internal state variables](@entry_id:750754) that describe [material hardening](@entry_id:175896), and $\boldsymbol{X}$ are the [thermodynamic forces](@entry_id:161907) conjugate to $\boldsymbol{\alpha}$. In simpler models without energy storage in hardening mechanisms, this inequality reduces to the condition that the [plastic work](@entry_id:193085) rate must be non-negative: $\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p \ge 0$.

Third, the transition from elastic to plastic behavior is governed by a **[yield function](@entry_id:167970)**, $f(\boldsymbol{\sigma}, \boldsymbol{\alpha})$, which defines a convex region in stress space known as the **elastic domain**, $\mathcal{E}$. A stress state is admissible only if it lies within or on the boundary of this domain. By convention, this is expressed as:
$$
f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0
$$
The boundary of this domain, defined by $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0$, is called the **[yield surface](@entry_id:175331)**. The internal variables $\boldsymbol{\alpha}$ parameterize the state of the [yield surface](@entry_id:175331), allowing it to change in size ([isotropic hardening](@entry_id:164486)), position ([kinematic hardening](@entry_id:172077)), or shape as [plastic deformation](@entry_id:139726) accumulates [@2616059].

### The Plastic Flow Rule

While the [yield function](@entry_id:167970) determines *when* [plastic deformation](@entry_id:139726) occurs, it does not specify the *direction* or *magnitude* of the resulting plastic strain rate. This is the role of the **[flow rule](@entry_id:177163)**. The classical theory of plasticity postulates the existence of a second scalar function of state, known as the **[plastic potential](@entry_id:164680)**, $g(\boldsymbol{\sigma}, \boldsymbol{\alpha})$. The direction of the plastic [strain rate tensor](@entry_id:198281), $\dot{\boldsymbol{\varepsilon}}^p$, is assumed to be normal to the [level surfaces](@entry_id:196027) of this [plastic potential](@entry_id:164680) in [stress space](@entry_id:199156). This postulate is expressed mathematically as:
$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$
This fundamental equation, the **[flow rule](@entry_id:177163)**, decomposes the plastic strain rate into two components with distinct physical interpretations [@2867127]:

-   The tensor $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ is the gradient of the [plastic potential](@entry_id:164680) with respect to stress. Geometrically, it represents the vector normal to the surface defined by $g(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = \text{constant}$ at the current stress point. It therefore dictates the **direction** of plastic flow.

-   The scalar $\dot{\lambda}$ is the **[plastic multiplier](@entry_id:753519)**. It is a non-negative quantity ($\dot{\lambda} \ge 0$) that determines the **magnitude** of the plastic [strain rate](@entry_id:154778). The constraint of non-negativity is crucial, as it enforces the physical principle of **[irreversibility](@entry_id:140985)**—plastic strain cannot be spontaneously recovered during a loading process.

### Loading-Unloading Conditions and Consistency

The complete logic governing whether a material behaves elastically or plastically is elegantly captured by a set of relations known as the **Karush-Kuhn-Tucker (KKT) conditions**. These conditions, which arise naturally from the mathematics of constrained evolution, connect the yield function $f$ and the [plastic multiplier](@entry_id:753519) $\dot{\lambda}$ [@2867094] [@2616077]:

1.  **Admissibility**: $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0$
2.  **Non-negative plastic flow**: $\dot{\lambda} \ge 0$
3.  **Complementary Slackness**: $\dot{\lambda} f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) = 0$

The [complementary slackness](@entry_id:141017) condition provides the switching logic. If the stress state is strictly within the elastic domain ($f  0$), the condition requires that $\dot{\lambda} = 0$, meaning the behavior is purely elastic ($\dot{\boldsymbol{\varepsilon}}^p = \boldsymbol{0}$). Conversely, for [plastic flow](@entry_id:201346) to occur ($\dot{\lambda} > 0$), the stress state must lie exactly on the [yield surface](@entry_id:175331) ($f = 0$).

When [plastic loading](@entry_id:753518) occurs, the stress state must remain on the (potentially evolving) yield surface. For a continuous loading process, this requires that the rate of change of the yield function is zero. This is known as the **consistency condition**:
$$
\dot{f}(\boldsymbol{\sigma}(t), \boldsymbol{\alpha}(t)) = 0 \quad \text{if } \dot{\lambda} > 0
$$
Applying the chain rule gives the explicit form of this condition [@2616077] [@2867094]:
$$
\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} = 0
$$
It is this equation that allows for the determination of the magnitude of the [plastic multiplier](@entry_id:753519) $\dot{\lambda}$ during a plastic increment. It is critical to recognize that the [consistency condition](@entry_id:198045) is always based on the yield function $f$, as it is the constraint that must be maintained. This holds true regardless of the choice of the [plastic potential](@entry_id:164680) $g$.

The full set of loading-unloading conditions can be written in a compact form that also includes the consistency requirement:
$$
f \le 0, \quad \dot{\lambda} \ge 0, \quad \dot{\lambda} f = 0, \quad \dot{\lambda} \dot{f} = 0
$$
This formulation correctly distinguishes between [plastic loading](@entry_id:753518) ($\dot{\lambda} > 0$, $f=0$, $\dot{f}=0$), neutral loading ($\dot{\lambda} = 0$, $f=0$, $\dot{f}=0$), and elastic unloading from a yield state ($\dot{\lambda}=0$, $f=0$, $\dot{f}  0$) [@2616077].

### Associated versus Non-Associated Flow Rules

The choice of the [plastic potential](@entry_id:164680) $g$ relative to the [yield function](@entry_id:167970) $f$ gives rise to two distinct classes of plasticity models. This choice has profound consequences for the theoretical structure and practical application of the model.

#### The Associated Flow Rule: Normality and Stability

The simplest and most theoretically convenient choice is to postulate that the [plastic potential](@entry_id:164680) is identical to the [yield function](@entry_id:167970), i.e., $g = f$. This is known as an **[associated flow rule](@entry_id:201731)**. The [flow rule](@entry_id:177163) then takes the specific form:
$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$
This leads to a crucial geometric property: the plastic strain rate vector is normal to the [yield surface](@entry_id:175331) itself. This is often referred to as the **[normality rule](@entry_id:182635)**.

The [associated flow rule](@entry_id:201731) is not merely a convenient assumption; it is deeply connected to [material stability](@entry_id:183933). It can be derived from **Drucker's stability postulate**, which states that for any external agency that applies a set of stresses to a stable material and then removes them, the [net work](@entry_id:195817) done by the agency is non-negative. For [rate-independent plasticity](@entry_id:754082), this implies $(\boldsymbol{\sigma} - \boldsymbol{\sigma}^*) : \dot{\boldsymbol{\varepsilon}}^p \ge 0$ for any stress state $\boldsymbol{\sigma}^*$ inside the elastic domain. When the elastic domain is convex and contains the origin, the choice of an [associated flow rule](@entry_id:201731) is a sufficient condition to satisfy Drucker's postulate and, consequently, the thermodynamic requirement of non-negative [plastic dissipation](@entry_id:201273) $\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p \ge 0$ [@2867094]. This inherent stability and theoretical elegance make associated plasticity the default choice for many materials, particularly metals.

#### The Non-Associated Flow Rule: Capturing Complex Behaviors

While theoretically appealing, the [associated flow rule](@entry_id:201731) imposes a strict coupling between the [yield criterion](@entry_id:193897) and the [plastic flow](@entry_id:201346) direction. For many materials, this coupling is not observed experimentally. For instance, in frictional materials such as soils, rocks, and concrete, the strength is highly dependent on pressure, but the plastic volume change (**[dilatancy](@entry_id:201001)**) observed during shear is often much smaller than what an [associated flow rule](@entry_id:201731) would predict.

To model such behavior, it is necessary to decouple the yield condition from the flow direction by choosing a [plastic potential](@entry_id:164680) $g$ that is different from the [yield function](@entry_id:167970) $f$. This is a **[non-associated flow rule](@entry_id:172454)**. A classic example is the Drucker-Prager model for [geomaterials](@entry_id:749838), where the [yield function](@entry_id:167970) and [plastic potential](@entry_id:164680) might be [@2867131]:
$$
f(\boldsymbol{\sigma}) = q + \alpha p - k \quad \text{(Yield Function)}
$$
$$
g(\boldsymbol{\sigma}) = q + \beta p \quad \text{(Plastic Potential)}
$$
Here, $p$ is the mean stress (pressure), $q$ is the [deviatoric stress](@entry_id:163323) invariant, $\alpha$ is related to the material's friction angle (strength), and $\beta$ is related to its [dilatancy angle](@entry_id:748435) (flow). An associated model would require $\beta = \alpha$, which often over-predicts the [volumetric expansion](@entry_id:144241) of dense [granular materials](@entry_id:750005). By choosing $\beta  \alpha$, a non-associated model can accurately capture both the frictional strength and the observed dilatancy. In the limit of plastically incompressible flow, as is often assumed for metals, one sets $\beta = 0$, leading to a purely deviatoric potential $g=q$, which ensures $\dot{\varepsilon}_{v}^{p} = \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = 0$ [@2867131].

### Thermodynamic Admissibility of Non-Associated Models

The flexibility of non-associated models comes at a cost: they are not guaranteed to be thermodynamically consistent or stable. The requirement for non-negative [plastic dissipation](@entry_id:201273), $\mathcal{D}^p \ge 0$, must be explicitly verified. Substituting the [non-associated flow rule](@entry_id:172454) into the [dissipation inequality](@entry_id:188634) gives:
$$
\mathcal{D}^p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \left( \boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \right) \ge 0
$$
Since $\dot{\lambda} \ge 0$, stability demands that the term $\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}}$ be non-negative for every possible stress state $\boldsymbol{\sigma}$ on the [yield surface](@entry_id:175331) $f=0$. The tightest condition for stability is therefore that the minimum value of this quantity over the entire yield surface must be non-negative [@2616043]:
$$
\min_{\boldsymbol{\sigma} \in \{ \boldsymbol{s} | f(\boldsymbol{s})=0 \}} \left( \boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \right) \ge 0
$$
Failure to satisfy this condition for a chosen $g$ implies that the model allows for scenarios where the material generates energy during [plastic flow](@entry_id:201346), a violation of the [second law of thermodynamics](@entry_id:142732) [@2867094]. For example, in the context of a Mohr-Coulomb material, Drucker's stability postulate imposes a strict limit on the non-associativity. An analysis shows that the dilation angle $\psi$ must be less than or equal to the friction angle $\varphi$ ($\psi \le \varphi$) to ensure stability [@2616070].

### Advanced Topics and Consequences

#### Flow at Non-Smooth Yield Surfaces

Many realistic [yield criteria](@entry_id:178101), such as the Tresca or Mohr-Coulomb criteria, feature corners or edges where the [yield surface](@entry_id:175331) is not smooth and the gradient $\nabla f$ is not uniquely defined. The concept of normality can be generalized to these points using the tools of convex analysis.

At a non-smooth point $\boldsymbol{\sigma}_0$ on a [convex yield surface](@entry_id:203690), the unique normal vector is replaced by a set of possible normal directions, called the **subdifferential**, denoted $\partial f(\boldsymbol{\sigma}_0)$. This set can be visualized as the cone of all outward-pointing vectors that form a non-acute angle with any vector pointing from $\boldsymbol{\sigma}_0$ into the elastic domain. For a corner formed by the intersection of several smooth surfaces $f_i$, the [subdifferential](@entry_id:175641) is the convex hull of the limiting gradients of those surfaces [@2616051]:
$$
\partial f(\boldsymbol{\sigma}_0) = \mathrm{co} \left\{ \nabla f_i(\boldsymbol{\sigma}_0) \mid f_i(\boldsymbol{\sigma}_0)=0 \right\}
$$
The [associated flow rule](@entry_id:201731) at such a corner, known as **Koiter's rule**, generalizes to state that the plastic strain rate vector must be a non-negative [linear combination](@entry_id:155091) of these limiting gradients. Equivalently, the plastic strain rate must lie in the **[normal cone](@entry_id:272387)** to the elastic set, $\dot{\boldsymbol{\varepsilon}}^p \in \mathcal{N}_{\mathcal{K}}(\boldsymbol{\sigma}_0)$, which ensures that the principle of maximum [plastic dissipation](@entry_id:201273) is upheld [@2616051].

#### Computational Implications of Non-Associativity

The distinction between associated and [non-associated flow](@entry_id:202786) has profound consequences for the numerical solution of plasticity problems, particularly within the Finite Element Method (FEM).

For models with an **[associated flow rule](@entry_id:201731)**, the constitutive structure admits an incremental variational principle. This means that the solution to an incremental step can be found by minimizing a single scalar potential function. This property arises because the **consistent (or algorithmic) tangent operator**, $\mathbb{C}^{ep} = \frac{\partial \boldsymbol{\sigma}}{\partial \boldsymbol{\varepsilon}}$, is **symmetric** [@2616040]. A symmetric tangent operator leads to a symmetric global tangent stiffness matrix $\mathbf{K}$ in the linearized FEM equations $\mathbf{K} \Delta \mathbf{u} = -\mathbf{r}$. This allows for the use of highly efficient symmetric solvers, such as the Conjugate Gradient method.

In stark contrast, for models with a **[non-associated flow rule](@entry_id:172454)** ($g \neq f$), the [consistent tangent operator](@entry_id:747733) $\mathbb{C}^{ep}$ is generally **unsymmetric**. Consequently, the [global stiffness matrix](@entry_id:138630) $\mathbf{K}$ is also unsymmetric [@2616093]. This has two major impacts:
1.  An incremental variational potential does not exist. The problem must be solved as a system of nonlinear equations rather than a minimization problem.
2.  The resulting linear system at each step of a Newton-Raphson procedure requires an **unsymmetric linear solver** (e.g., GMRES, LU decomposition).

Despite the loss of symmetry, if the exact (unsymmetric) [tangent stiffness matrix](@entry_id:170852) is computed and used, the celebrated **quadratic convergence** of the Newton-Raphson method is retained. A common but suboptimal practice is to use a symmetrized version of the tangent matrix to enable the use of symmetric solvers; however, this transforms the algorithm into a quasi-Newton method and typically degrades the convergence rate from quadratic to linear or superlinear [@2616093]. The need to handle [non-associated flow](@entry_id:202786) correctly is therefore not just a matter of theoretical fidelity but also a critical aspect of robust and efficient computational implementation.