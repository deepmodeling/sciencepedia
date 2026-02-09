## Introduction
The field of computational solid mechanics is undergoing a paradigm shift, moving from classical phenomenological constitutive models to more flexible and powerful data-driven frameworks. These machine learning approaches promise to capture complex material behaviors directly from experimental or simulation data, bypassing the need for handcrafted analytical functions. However, this flexibility comes with a significant challenge: without explicit guidance, a data-driven model can easily learn non-physical behaviors, violating fundamental laws of thermodynamics and mechanics. This article addresses this critical knowledge gap by providing a comprehensive guide to building physically robust and predictive data-driven constitutive models.

This guide is structured to build your expertise progressively. In the first chapter, **Principles and Mechanisms**, we will delve into the core theoretical constraints that govern all constitutive models, including thermodynamic consistency, frame indifference, and material symmetry, and explore how these principles can be embedded into machine learning architectures by construction. Next, the chapter on **Applications and Interdisciplinary Connections** will showcase how these physically-informed models are applied to solve real-world challenges in multiscale modeling, damage mechanics, and their integration into finite element simulations. Finally, the **Hands-On Practices** section will bridge theory and application, offering practical exercises to solidify your understanding of enforcing thermodynamic admissibility, objectivity, and ensuring compatibility with numerical solvers.

## Principles and Mechanisms

The transition from classical, phenomenologically-derived constitutive models to data-driven and machine learning frameworks does not represent a departure from physical principles. On the contrary, it necessitates an even more rigorous and explicit enforcement of the foundational laws of mechanics and thermodynamics. A data-driven model, unconstrained by prior physical knowledge, has the freedom to learn non-physical behaviors from finite or noisy data. Therefore, the central challenge in this field is to design model architectures and learning algorithms that embed these fundamental principles by construction or enforce them during training. This chapter elucidates the core principles and mechanisms that ensure data-driven constitutive models are not merely correlative but are predictive, robust, and physically consistent.

### Thermodynamic Consistency: The Foundational Constraint

The most fundamental constraint on any constitutive model is that it must obey the laws of thermodynamics. For isothermal processes, this is captured by the **Clausius-Duhem inequality**, which states that the rate of mechanical dissipation must be non-negative. For a material element described by a state comprising the strain tensor and a set of internal variables, this principle provides a powerful and systematic framework for developing consistent constitutive laws.

Consider a small-strain solid whose state is defined by the symmetric strain tensor $\boldsymbol{\varepsilon}$ and a set of internal variables $\boldsymbol{\alpha}$ that capture the material's history-dependent microstructure (e.g., plastic strain, damage variables, or viscous flow). The **Helmholtz free energy** density, denoted by $\psi(\boldsymbol{\varepsilon}, \boldsymbol{\alpha})$, represents the reversibly stored energy in the material. The Clausius-Duhem inequality for an isothermal process can be expressed as the non-negativity of the mechanical dissipation rate per unit volume, $\mathcal{D}$ [@problem_id:3557096]:

$$
\mathcal{D} = \boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}} - \dot{\psi}(\boldsymbol{\varepsilon}, \boldsymbol{\alpha}) \ge 0
$$

Here, $\boldsymbol{\sigma}$ is the Cauchy stress tensor, the superposed dot denotes the material time derivative, and the term $\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}$ represents the **stress power**—the rate of work done on the material element by the stress field. The term $\dot{\psi}$ represents the rate at which this work is stored reversibly as free energy. Consequently, $\mathcal{D}$ is the portion of the work rate that is not stored and is instead irreversibly converted into other forms, primarily heat.

By applying the chain rule to the rate of change of free energy, $\dot{\psi} = (\partial\psi/\partial\boldsymbol{\varepsilon}):\dot{\boldsymbol{\varepsilon}} + (\partial\psi/\partial\boldsymbol{\alpha})\cdot\dot{\boldsymbol{\alpha}}$, and substituting it into the inequality, we obtain:

$$
\left( \boldsymbol{\sigma} - \frac{\partial\psi}{\partial\boldsymbol{\varepsilon}} \right) : \dot{\boldsymbol{\varepsilon}} - \frac{\partial\psi}{\partial\boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} \ge 0
$$

The Coleman-Noll procedure argues that this inequality must hold for all admissible thermodynamic processes. As we can conceive of processes with arbitrary strain rates $\dot{\boldsymbol{\varepsilon}}$, the term multiplying $\dot{\boldsymbol{\varepsilon}}$ must vanish to prevent violations of the inequality. This yields a profound constitutive restriction: the stress must be derivable from the free energy potential [@problem_id:3557096]:

$$
\boldsymbol{\sigma} = \frac{\partial\psi}{\partial\boldsymbol{\varepsilon}}
$$

This relationship is the hallmark of **hyperelasticity**. A material whose stress is the gradient of a scalar potential is guaranteed to have a path-independent work response in the absence of internal variable evolution. This leads to several critical consequences for constitutive modeling [@problem_id:3557102]. First, because $\boldsymbol{\varepsilon}$ is symmetric, the stress derived in this way is automatically symmetric ($\boldsymbol{\sigma} = \boldsymbol{\sigma}^\top$), satisfying the balance of angular momentum by construction. A direct, "black-box" model $\boldsymbol{\sigma} = \hat{\boldsymbol{\sigma}}(\boldsymbol{\varepsilon})$ offers no such guarantee and can easily predict non-symmetric stresses unless symmetry is explicitly enforced. Second, the **algorithmic consistent tangent modulus**, $\mathbb{C} := \partial\boldsymbol{\sigma}/\partial\boldsymbol{\varepsilon}$, becomes the Hessian of the potential, $\mathbb{C} = \partial^2\psi/\partial\boldsymbol{\varepsilon}\partial\boldsymbol{\varepsilon}$. This ensures the major symmetry $\mathbb{C}_{ijkl} = \mathbb{C}_{klij}$, a property that is highly beneficial for the efficiency of numerical solvers in finite element analysis.

With the stress relation established, the dissipation inequality reduces to the **reduced dissipation inequality**:

$$
\mathcal{D} = \boldsymbol{Y} \cdot \dot{\boldsymbol{\alpha}} \ge 0 \quad \text{where} \quad \boldsymbol{Y} = -\frac{\partial\psi}{\partial\boldsymbol{\alpha}}
$$

Here, $\boldsymbol{Y}$ is the set of **thermodynamic forces** conjugate to the internal variables $\boldsymbol{\alpha}$. This inequality constrains the evolution laws for the internal variables. A common and powerful way to satisfy it is to postulate the existence of a convex **dissipation potential**, $\phi(\dot{\boldsymbol{\alpha}})$, and define the evolution via a normality rule, such that $\boldsymbol{Y}$ lies in the subdifferential of $\phi$. This structured, potential-based approach—learning a free energy potential $\psi$ and a dissipation potential $\phi$—is a cornerstone of physics-informed machine learning, as it embeds thermodynamic consistency directly into the model's architecture [@problem_id:3557096] [@problem_id:3557102].

### Material Frame Indifference and Isotropy: Embedding Symmetries

Constitutive laws must be independent of the observer's reference frame, a principle known as **material frame indifference** or objectivity. For finite deformation, where the deformation is described by the deformation gradient $\mathbf{F}$, a superposed rigid body rotation $\mathbf{Q}$ transforms the deformation to $\mathbf{QF}$. To ensure objectivity, the constitutive model must be formulated using variables that are invariant to such rotations. Tensors defined in the material's reference configuration, such as the right Cauchy-Green tensor $\mathbf{C} = \mathbf{F}^\top\mathbf{F}$, are naturally objective, as $\mathbf{C} \to (\mathbf{QF})^\top(\mathbf{QF}) = \mathbf{F}^\top\mathbf{Q}^\top\mathbf{QF} = \mathbf{F}^\top\mathbf{F} = \mathbf{C}$. Therefore, expressing the strain energy as a function of $\mathbf{C}$, i.e., $W(\mathbf{C})$, is the standard method for satisfying frame indifference.

Beyond this universal requirement, models must reflect the specific symmetries of the material. A particularly important case is **isotropy**, where the material has no preferential directions. For an isotropic hyperelastic material, the strain energy function must be invariant under any rotation of the reference configuration, meaning $W(\mathbf{C}) = W(\mathbf{Q}^\top\mathbf{C}\mathbf{Q})$ for all orthogonal $\mathbf{Q}$. The representation theorems for isotropic functions state that this condition is met if and only if $W$ is a function of the **principal invariants** of $\mathbf{C}$ [@problem_id:3557101]:

$$
I_1 = \mathrm{tr}(\mathbf{C}), \quad I_2 = \frac{1}{2}[(\mathrm{tr}\mathbf{C})^2 - \mathrm{tr}(\mathbf{C}^2)], \quad I_3 = \det(\mathbf{C})
$$

This provides a direct recipe for constructing isotropic data-driven models: instead of learning a function of the six independent components of $\mathbf{C}$, one learns a function of these three scalar invariants, $W = \hat{W}(I_1, I_2, I_3)$. This reduces the dimensionality of the input space and hard-codes the isotropy constraint into the model architecture.

The stress can then be derived using the chain rule, for instance, for the second Piola-Kirchhoff stress $\mathbf{S} = 2\partial W/\partial\mathbf{C}$. Alternatively, a general isotropic tensor function $\mathbf{S}(\mathbf{C})$ can be expressed via the Cayley-Hamilton theorem as a polynomial in $\mathbf{C}$:

$$
\mathbf{S} = \beta_0(I_1, I_2, I_3)\mathbf{I} + \beta_1(I_1, I_2, I_3)\mathbf{C} + \beta_2(I_1, I_2, I_3)\mathbf{C}^2
$$

In a data-driven context, one could train a neural network to map the invariants $(I_1, I_2, I_3)$ to the coefficients $(\beta_0, \beta_1, \beta_2)$. While a spectral representation based on the eigenvalues of $\mathbf{C}$ is also possible, it is numerically problematic. When eigenvalues of $\mathbf{C}$ are repeated, their corresponding eigenvectors are not unique, leading to instabilities and non-differentiability in the computational graph. The polynomial representation, which depends only on the tensor invariants, is smooth and well-defined regardless of eigenvalue multiplicities, making it the preferred approach for robust implementation [@problem_id:3557101].

### Mathematical Well-Posedness: Ensuring Stable Solutions

A physically plausible constitutive model must also be mathematically well-posed when used in a boundary value problem. For hyperelastic materials, this typically means the total potential energy of the body must admit a stable minimizer. The absence of such a minimizer can lead to non-physical material instabilities or the failure of numerical simulations to converge.

A key condition for ensuring the existence of minimizers in nonlinear elasticity is **polyconvexity**. A strain energy function $W(\mathbf{F})$ is defined as polyconvex if it can be written as a convex function $g$ of the deformation gradient $\mathbf{F}$, its cofactor matrix $\mathrm{cof}(\mathbf{F})$, and its determinant $J = \det(\mathbf{F})$ [@problem_id:3557131] [@problem_id:3557092]:

$$
W(\mathbf{F}) = g(\mathbf{F}, \mathrm{cof}(\mathbf{F}), J)
$$

The cofactor matrix is related to area changes, while the determinant is related to volume changes. Polyconvexity is a stronger condition than rank-one convexity (a necessary condition for material stability) but weaker than full convexity in $\mathbf{F}$. Its mathematical power stems from the fact that it ensures the **weak lower semicontinuity** of the total energy functional. In the direct method of the calculus of variations, this property, combined with coercivity (energy grows to infinity with large deformations), guarantees the existence of an energy-minimizing solution [@problem_id:3557131].

To build data-driven models that are polyconvex by construction, one can employ **Input-Convex Neural Networks (ICNNs)**. An ICNN is a special architecture designed to represent a convex function of its inputs. By constructing a neural network $\Phi(\cdot;\theta)$ that is provably convex and feeding it the augmented input vector $(\mathbf{F}, \mathrm{cof}(\mathbf{F}), J)$, the resulting strain energy model $W(\mathbf{F}) = \Phi(\mathbf{F}, \mathrm{cof}(\mathbf{F}), J; \theta)$ is guaranteed to be polyconvex [@problem_id:3557092]. A common and effective architecture enforces an additive split into a part that depends on $(\mathbf{F}, \mathrm{cof}(\mathbf{F}))$ and a volumetric part that depends only on $J$, with each part represented by a convex function:

$$
W(\mathbf{F}) = \Psi(\mathbf{F}, \mathrm{cof}(\mathbf{F}); \theta_{iso}) + \phi(J; \theta_{vol})
$$

Here, both $\Psi$ and $\phi$ can be realized by ICNNs, ensuring the sum is convex and the overall model is polyconvex. The volumetric term $\phi(J)$ is typically designed to diverge to infinity as $J \to 0^+$, thereby penalizing material self-penetration.

### Modeling Inelasticity and Path-Dependence

While hyperelasticity provides the foundation, many engineering materials exhibit inelasticity and history-dependence, such as plasticity and viscoelasticity. Data-driven methods must also be able to capture these more complex behaviors.

#### Rate-Independent Plasticity

The framework of rate-independent plasticity is built upon a **yield function**, $f(\boldsymbol{\sigma}, \boldsymbol{\kappa})$, which defines the boundary of the elastic domain in the space of stress $\boldsymbol{\sigma}$ and internal hardening variables $\boldsymbol{\kappa}$. Plastic flow occurs only when the stress state lies on the yield surface, i.e., $f=0$. The evolution of the plastic strain $\boldsymbol{\varepsilon}^p$ is governed by a **flow rule**, and the evolution of the hardening variables is described by a **hardening law** [@problem_id:3557106].

These rules are encapsulated by the Karush-Kuhn-Tucker (KKT) conditions:
1.  Yield Condition: $f(\boldsymbol{\sigma}, \boldsymbol{\kappa}) \le 0$
2.  Non-negative Plastic Multiplier: $\dot{\lambda} \ge 0$
3.  Complementarity: $\dot{\lambda} f(\boldsymbol{\sigma}, \boldsymbol{\kappa}) = 0$

The flow rule distinguishes between two important cases. In **associative plasticity**, the direction of plastic flow is normal to the yield surface:

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial\boldsymbol{\sigma}}
$$

In this case, the yield function also serves as the plastic potential. If $f$ is convex, this structure automatically satisfies the dissipation inequality. In **non-associative plasticity**, the flow direction is governed by a separate **plastic potential** $g(\boldsymbol{\sigma}, \boldsymbol{\kappa}) \ne f$, such that $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} (\partial g/\partial\boldsymbol{\sigma})$. Machine learning models can be used to learn the functional forms of $f$ and $g$ from experimental data, providing a flexible way to capture complex yield surfaces and flow behaviors that are difficult to model with analytical functions [@problem_id:3557106].

#### Rate-Dependent History Effects

Materials like polymers exhibit viscoelasticity, where the current stress depends on the entire history of strain. This relationship can be framed as an operator $\mathcal{G}$ that maps a strain history function $\boldsymbol{\varepsilon}(s)|_{s=0}^t$ to the current stress vector $\boldsymbol{\sigma}(t)$. For linear, time-translation-invariant materials, this operator takes the form of a Volterra convolution integral, also known as the Boltzmann superposition principle [@problem_id:3557159]:

$$
\boldsymbol{\sigma}(t) = \int_0^t \mathbb{G}(t-s) : \dot{\boldsymbol{\varepsilon}}(s) ds
$$

where $\mathbb{G}$ is the relaxation tensor. Learning such operators from data is the domain of **neural operators**. Two prominent architectures are:
-   **Deep Operator Networks (DeepONets)**, which use a "branch" network to encode the input function (strain history) and a "trunk" network to evaluate the output at a specific query time $t$. DeepONets are well-suited for irregularly sampled histories but must be queried point-wise to generate an output sequence [@problem_id:3557159].
-   **Fourier Neural Operators (FNOs)**, which learn the operator's kernel in the Fourier domain. By leveraging the convolution theorem and Fast Fourier Transforms, FNOs can efficiently process entire sequences on a uniform grid in a single pass. A key advantage is their ability to generalize across different time resolutions (zero-shot super-resolution) [@problem_id:3557159].

For both architectures, enforcing **causality**—that the stress at time $t$ cannot depend on future strains—is a critical physical constraint that must be built into the learning process.

### From Principles to Practice: Training and Identification

Embedding physical principles into a data-driven model is achieved through a combination of "hard" architectural constraints and "soft" penalties in the training objective.

#### Physics-Informed Loss Functions

While principles like isotropy (via invariants) and polyconvexity (via ICNNs) can be hard-coded, others may be more conveniently enforced as soft constraints. A composite loss function for training a model with parameters $\theta$ typically includes a data-mismatch term and several physics-based penalty terms [@problem_id:3557171]:

$$
\mathcal{L}(\theta) = \lambda_{\mathrm{dat}}\mathcal{L}_{\mathrm{dat}} + \lambda_{\mathrm{obj}}\mathcal{L}_{\mathrm{obj}} + \lambda_{\mathrm{sym}}\mathcal{L}_{\mathrm{sym}} + \lambda_{\mathrm{dis}}\mathcal{L}_{\mathrm{dis}} + \dots
$$

Each term serves a specific purpose:
-   $\mathcal{L}_{\mathrm{dat}}$: A standard mean-squared error term that measures the discrepancy between model predictions and experimental data.
-   $\mathcal{L}_{\mathrm{obj}}$: A penalty for violating frame indifference, e.g., by checking if $\mathbf{P}_\theta(\mathbf{Q}\mathbf{F}) = \mathbf{Q}\mathbf{P}_\theta(\mathbf{F})$.
-   $\mathcal{L}_{\mathrm{sym}}$: A penalty for non-symmetric Cauchy stress, penalizing the norm of the anti-symmetric part of $\boldsymbol{\sigma}_\theta$.
-   $\mathcal{L}_{\mathrm{dis}}$: A penalty for violating the dissipation inequality, typically by penalizing negative values of the discrete dissipation over observed time increments.

The weights $\lambda_i$ balance the trade-off between fitting the data and satisfying the physical laws.

#### Model Identifiability and Experimental Design

A crucial practical consideration is **identifiability**: can the model parameters be uniquely determined from the available experimental data? **Structural identifiability** asks whether different parameter sets could produce identical predictions for the given experiments. If so, the parameters are non-identifiable, regardless of data quantity or quality. **Practical identifiability** concerns whether parameters can be estimated with sufficient precision from finite, noisy data [@problem_id:3557127].

A common pitfall is using an insufficiently rich dataset. For example, trying to identify the parameters of an anisotropic model using only uniaxial tension tests along the symmetry axes is often an ill-posed problem. Such tests may not activate certain deformation modes (like shear), rendering the parameters associated with those modes structurally non-identifiable [@problem_id:3557127]. For flexible machine learning models, training on limited data can lead to many different sets of network weights that fit the data perfectly but give wildly different predictions for unseen deformation paths. The solution is twofold: enrich the training dataset with diverse, **multiaxial experimental data** (e.g., biaxial tension, simple shear) and embed as much known physics as possible into the model architecture to act as a powerful regularizer.

#### An Alternative Paradigm: Data-Driven Solvers

Finally, it is worth noting an alternative paradigm that circumvents the need to identify an explicit constitutive model altogether. Methods like **Data-Driven Computational Mechanics (DDCM)** reframe the problem. Instead of fitting a model, they seek a solution to a boundary value problem that simultaneously satisfies the governing physical laws (kinematic compatibility and equilibrium) and is closest to a pre-existing database of material behavior [@problem_id:3557175].

The problem is cast as a constrained minimization: finding a state $(\boldsymbol{\varepsilon}, \boldsymbol{\sigma})$ in the set of all physically admissible states that minimizes its distance to the material data set. The "distance" metric itself must be physically meaningful, typically derived from energy principles. For instance, a suitable metric on the $(\boldsymbol{\varepsilon}, \boldsymbol{\sigma})$ space can be constructed using a reference elasticity tensor $\mathbb{C}_e$:

$$
d^2 = (\Delta\boldsymbol{\varepsilon}) : \mathbb{C}_e : (\Delta\boldsymbol{\varepsilon}) + (\Delta\boldsymbol{\sigma}) : \mathbb{C}_e^{-1} : (\Delta\boldsymbol{\sigma})
$$

This formulation elegantly bypasses the intermediate step of constitutive modeling, connecting data directly to the simulation of mechanical systems.