## Introduction
Modeling the initiation and propagation of fractures remains one of the most significant challenges in solid mechanics. Classical continuum mechanics, which relies on spatial derivatives, is inherently ill-posed at the sharp discontinuities of a crack, necessitating complex, supplementary theories to describe failure. Peridynamics offers a fundamental paradigm shift, reformulating mechanics using an integral-based, nonlocal framework that remains valid everywhere, even in the presence of cracks. This article provides a comprehensive overview of the peridynamic theory for fracture, designed for graduate-level researchers and engineers.

Across the following chapters, you will gain a deep understanding of this powerful computational method. We will begin by exploring the 'Principles and Mechanisms' of peridynamics, contrasting its integral equation of motion with classical approaches and detailing the evolution from simple bond-based models to general state-based correspondence theories. Next, under 'Applications and Interdisciplinary Connections', we will demonstrate the theory's versatility in modeling complex fracture phenomena and its seamless integration into multiphysics simulations involving thermal, chemical, and fluid-driven processes. Finally, the 'Hands-On Practices' section will provide targeted computational exercises to solidify theoretical concepts and build practical implementation skills.

## Principles and Mechanisms

Peridynamics (PD) is a nonlocal reformulation of continuum mechanics, particularly advantageous for modeling material failure. This chapter delves into the foundational principles and mechanical formulations that underpin the theory. We will move from the fundamental equation of motion to the specific constitutive models for elastic deformation and fracture, illuminating how peridynamics provides a robust framework for problems involving discontinuities.

### The Peridynamic Equation of Motion: An Integral Formulation

Classical Continuum Mechanics (CCM) describes the internal forces within a body through the divergence of the Cauchy stress tensor, $\boldsymbol{\sigma}$. The equation of motion for a material point at position $\mathbf{x}$ with mass density $\rho(\mathbf{x})$ and displacement $\mathbf{u}(\mathbf{x}, t)$ is thus a partial differential equation:

$$ \rho(\mathbf{x}) \frac{\partial^2 \mathbf{u}(\mathbf{x}, t)}{\partial t^2} = \nabla \cdot \boldsymbol{\sigma}(\mathbf{x}, t) + \mathbf{b}(\mathbf{x}, t) $$

where $\mathbf{b}(\mathbf{x}, t)$ is an external body force density. This formulation relies on the existence of spatial derivatives of the displacement field, as the stress itself is a function of the strain tensor, which contains first derivatives of $\mathbf{u}$. At the site of a crack, where the displacement field is discontinuous, these derivatives are mathematically undefined. Consequently, the classical equation of motion is ill-posed at crack tips and surfaces, necessitating supplementary theories like Linear Elastic Fracture Mechanics (LEFM) to describe crack propagation.

Peridynamics elegantly circumvents this limitation by postulating that internal forces arise from direct, long-range interactions between material points, rather than through local stress fields. It replaces the spatial derivatives of CCM with a spatial integral. The peridynamic equation of motion is an integro-differential equation given by [@problem_id:3793723]:

$$ \rho(\mathbf{x}) \frac{\partial^2 \mathbf{u}(\mathbf{x}, t)}{\partial t^2} = \int_{\mathcal{H}_{\mathbf{x}}} \mathbf{f}(\mathbf{u}(\mathbf{x}', t) - \mathbf{u}(\mathbf{x}, t), \mathbf{x}' - \mathbf{x}) \, dV_{\mathbf{x}'} + \mathbf{b}(\mathbf{x}, t) $$

Here, the term representing the internal force density is a nonlocal operator. It is the integral of **pairwise force functions**, $\mathbf{f}$, which represent the force per unit volume squared that a point at position $\mathbf{x}'$ exerts on the point at $\mathbf{x}$. Crucially, this integral is taken over a finite neighborhood $\mathcal{H}_{\mathbf{x}}$ of the point $\mathbf{x}$, typically a ball of radius $\delta$. This radius, $\delta$, is known as the **peridynamic horizon**. The horizon defines the extent of nonlocality and acts as an intrinsic material length scale [@problem_id:3793719].

The pairwise force function $\mathbf{f}$ depends on the relative displacement of the two interacting points, $\boldsymbol{\eta} = \mathbf{u}(\mathbf{x}', t) - \mathbf{u}(\mathbf{x}, t)$, and their initial relative position, $\boldsymbol{\xi} = \mathbf{x}' - \mathbf{x}$. Because the integrand only involves differences of the displacement field at distinct points, it remains well-defined even when $\mathbf{u}$ has jump discontinuities. This is the fundamental reason why the peridynamic equation of motion is applicable everywhere in the body, including at cracks [@problem_id:3793770]. For conservation of linear momentum, the pairwise force function must satisfy Newton's third law, which implies the antisymmetry condition $\mathbf{f}(\boldsymbol{\eta}, \boldsymbol{\xi}) = -\mathbf{f}(-\boldsymbol{\eta}, -\boldsymbol{\xi})$ [@problem_id:3793723].

Despite its nonlocal nature, peridynamics maintains consistency with classical mechanics. For sufficiently smooth displacement fields, it can be shown that in the limit of a vanishing horizon ($\delta \to 0$), and with appropriate scaling of the force function, the peridynamic internal force operator converges to the classical divergence of the stress tensor, $\nabla \cdot \boldsymbol{\sigma}$. This ensures that peridynamics recovers classical elasticity as a special case, lending it multiscale consistency [@problem_id:3793770] [@problem_id:3793719].

### Bond-Based Peridynamics

The simplest and most intuitive formulation of peridynamics is **bond-based peridynamics**. In this framework, the interaction between any two material points is modeled independently of all other points.

#### Kinematics and Bond Stretch

The fundamental measure of deformation in bond-based PD is the **bond stretch**, $s$. A bond is the conceptual line segment connecting two material points, $\mathbf{x}$ and $\mathbf{x}'$, in the undeformed reference configuration. The initial vector describing this bond is the relative position vector, $\boldsymbol{\xi} = \mathbf{x}' - \mathbf{x}$. After deformation, the new positions are $\mathbf{y} = \mathbf{x} + \mathbf{u}(\mathbf{x}, t)$ and $\mathbf{y}' = \mathbf{x}' + \mathbf{u}(\mathbf{x}', t)$. The deformed bond vector is $\mathbf{y}' - \mathbf{y} = (\mathbf{x}'-\mathbf{x}) + (\mathbf{u}(\mathbf{x}', t)-\mathbf{u}(\mathbf{x}, t)) = \boldsymbol{\xi} + \boldsymbol{\eta}$, where $\boldsymbol{\eta}$ is the relative displacement vector.

The bond stretch is defined as the fractional change in the bond's length. The initial length is $\|\boldsymbol{\xi}\|$ and the final length is $\|\boldsymbol{\xi}+\boldsymbol{\eta}\|$. Therefore, the stretch $s$ is given by [@problem_id:3793759]:

$ s = \frac{\|\boldsymbol{\xi} + \boldsymbol{\eta}\| - \|\boldsymbol{\xi}\|}{\|\boldsymbol{\xi}\|} $

A positive stretch ($s>0$) indicates tension, while a negative stretch ($s0$) indicates compression.

#### Microelastic Constitutive Model and Its Limitations

In a microelastic material, the pairwise force is derived from a scalar potential energy stored in the bond, which depends only on the bond's stretch. For a simple model where the potential is quadratic in stretch, $w = \frac{1}{2} c(\|\boldsymbol{\xi}\|) s^2$, the magnitude of the pairwise force is $c(\|\boldsymbol{\xi}\|) s$. Here, $c(\|\boldsymbol{\xi}\|)$ is a **micromodulus function** that prescribes the stiffness of bonds of different initial lengths.

A key assumption in bond-based PD is that the pairwise force is a **central force**, meaning the force vector is always parallel to the deformed bond vector. The pairwise force function is thus [@problem_id:3793767]:

$ \mathbf{f}(\boldsymbol{\eta}, \boldsymbol{\xi}) = c(\|\boldsymbol{\xi}\|) s \frac{\boldsymbol{\xi} + \boldsymbol{\eta}}{\|\boldsymbol{\xi} + \boldsymbol{\eta}\|} $

While this model is simple and computationally efficient, the central-force assumption imposes a severe constraint on the elastic properties of the material. When the peridynamic strain energy density is matched with that of classical isotropic linear elasticity, it is found that the Lamé parameters are constrained such that $\lambda = \mu$. This fixes the effective Poisson's ratio of the material. For three-dimensional models, this constraint forces $\nu = 1/4$, and for two-dimensional plane stress models, it forces $\nu = 1/3$. Bond-based peridynamics is therefore unable to model materials with other Poisson's ratios, a significant limitation that motivated the development of more general theories [@problem_id:3793767].

### State-Based Peridynamics: A General Framework

To overcome the limitations of the bond-based model, **state-based peridynamics** was introduced. This is a more general formulation where the force in a particular bond can depend on the collective deformation of all bonds within the horizon.

In this framework, we introduce the concepts of **states**. A **deformation state**, denoted by the operator $\mathbf{Y}$, is a function that maps each bond vector $\boldsymbol{\xi}$ in the horizon to its deformed counterpart: $\mathbf{Y}\langle \boldsymbol{\xi} \rangle = \boldsymbol{\xi} + \boldsymbol{\eta}$. A **force state**, denoted $\mathbf{T}$, is a function that returns the force vector associated with each bond in the horizon: $\mathbf{T}\langle \boldsymbol{\xi} \rangle$ [@problem_id:3793725]. The equation of motion is then written using these force states.

The power of this formulation lies in how the force state is determined. One powerful method is the **correspondence principle**, which builds a bridge between the nonlocal peridynamic description and classical constitutive models. In this approach, one first computes a nonlocal approximation of the deformation gradient tensor, $\mathbf{F}$, at each point $\mathbf{x}$ by finding the tensor that best maps the initial bond vectors $\{\boldsymbol{\xi}\}$ to the deformed bond vectors $\{\mathbf{Y}\langle \boldsymbol{\xi} \rangle\}$ in a weighted least-squares sense. From this nonlocal $\mathbf{F}$, one can compute a standard strain tensor (e.g., $\boldsymbol{\varepsilon} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$) and then use any classical constitutive law (e.g., Hooke's law, $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}$) to find a corresponding stress tensor $\boldsymbol{\sigma}$. The force state $\mathbf{T}$ is then constructed from this stress tensor.

This procedure effectively allows the wealth of classical material models, including those for anisotropic materials, to be used within the peridynamic framework. Because the force state is no longer constrained to be collinear with the bond vector, the restriction on Poisson's ratio is removed, and state-based models can represent arbitrary elastic constants [@problem_id:3793725].

### The Mechanism of Fracture

The most compelling application of peridynamics is its ability to model fracture initiation and propagation in a natural and autonomous way.

#### The Critical Stretch Criterion and Autonomous Crack Growth

In peridynamics, fracture is a direct consequence of the constitutive law, not an additional criterion. For brittle materials, this is typically modeled via a **critical stretch criterion**. Each bond is assumed to have a critical stretch, $s_c$. If the stretch in a bond ever exceeds this value, the bond is considered irreversibly broken [@problem_id:3793731].

$ s(\mathbf{x}, \mathbf{x}', t) > s_c \implies \text{Bond is broken} $

Once a bond is broken, the pairwise force function $\mathbf{f}$ (or force state $\mathbf{T}$) for that bond is set to zero for all subsequent time. A crack is therefore not a predefined geometric entity, but an emergent feature of the simulation, represented by a collection of broken bonds. As the body deforms, bonds reach their critical stretch and break, and the load they once carried is redistributed to their neighbors. This can cause a cascade of failures, leading to the spontaneous nucleation and growth of cracks. The peridynamic equation of motion automatically handles the new, traction-free surfaces created by these broken bonds without any need for complex tracking algorithms or supplementary crack-tip equations like the Griffith criterion [@problem_id:3793740].

This autonomous nature contrasts sharply with other methods. For example, classical Cohesive Zone Models (CZMs) require the pre-specification of potential crack paths, while Phase-Field Models (PFMs), though also offering autonomous crack evolution, do so by solving an additional partial differential equation for a continuous damage field, which is conceptually different from the discrete bond-breaking mechanism in PD [@problem_id:3793740].

#### Quantifying Damage

The extent of fracture at a material point $\mathbf{x}$ can be quantified by a local **damage** variable, $D(\mathbf{x}, t)$. This is typically defined as the weighted fraction of broken bonds within the point's horizon. Using a history-dependent indicator variable $\mu(\mathbf{x}, \mathbf{x}', t)$ which is $1$ if the bond is intact and $0$ if it is broken, the damage is defined as [@problem_id:3793731]:

$ D(\mathbf{x}, t) = \frac{\int_{\mathcal{H}_{\mathbf{x}}} (1 - \mu(\mathbf{x}, \mathbf{x}', t)) \, dV'}{\int_{\mathcal{H}_{\mathbf{x}}} dV'} $

The damage variable ranges from $D=0$ for undamaged material to $D=1$ for a fully disconnected point. Because bond breaking is irreversible, $D(\mathbf{x}, t)$ is a non-decreasing function of time. The peridynamic horizon $\delta$ provides a natural regularization for this damage field. The transition from fully intact ($D=0$) to fully broken ($D=1$) material must occur over a region with a width on the order of $\delta$. This region is the peridynamic representation of the fracture process zone, and its finite size is a direct consequence of the model's intrinsic length scale [@problem_id:3793719].

### Calibration and Practical Considerations

To be a predictive tool, the microscopic parameters of a peridynamic model must be related to macroscopic, experimentally measurable material properties.

#### From Fracture Energy to Critical Stretch

One of the most important macroscopic properties for fracture is the material's fracture energy or critical energy release rate, $G_c$. This is the energy required to create a unit area of new crack surface. In peridynamics, this energy corresponds to the sum of the potential energies stored in all the bonds that are broken as a crack advances.

By equating the energy released per unit crack area in the peridynamic model to the macroscopic $G_c$, one can derive a relationship between the microscopic critical stretch $s_c$ and the macroscopic $G_c$. The exact relationship depends on the specific form of the micromodulus function $c(r)$ and the horizon size $\delta$. For instance, for a 3D model with a linearly decaying "cone-shaped" micromodulus $c(r) = c_0 (1 - r/\delta)$, the calculation yields [@problem_id:3793745]:

$ G_c = \frac{\pi c_0 \delta^5 s_c^2}{60} \implies s_c = \sqrt{\frac{60 G_c}{\pi c_0 \delta^5}} $

This calibration is crucial, as it connects the microscopic failure criterion to a measurable macroscopic property, enabling peridynamics to make quantitative predictions about fracture.

#### The Surface Effect and Correction Methods

A practical challenge in peridynamics arises near the boundaries of a body. A material point located near a free surface has a **truncated horizon**; it interacts with fewer neighbors than a point in the interior. This leads to an artificial reduction in stiffness, an unphysical phenomenon often called the "surface effect" or "skin effect".

To mitigate this, correction schemes are often employed. A common approach is to modify the constitutive parameters for points near a surface. For example, one can introduce a correction factor for the micromodulus to ensure that the strain energy density under a given uniform deformation is the same for a boundary point as it is for an interior point. A calculation for a 2D model with a point on a straight free boundary (a half-disk horizon) shows that to maintain stiffness consistency under uniaxial strain, the micromodulus for that point's bonds must be doubled ($c_{\mathrm{corr}} = 2c$) to compensate for the "missing" half of its neighborhood [@problem_id:3793714]. Such corrections are vital for achieving accurate results in simulations of finite-sized components.