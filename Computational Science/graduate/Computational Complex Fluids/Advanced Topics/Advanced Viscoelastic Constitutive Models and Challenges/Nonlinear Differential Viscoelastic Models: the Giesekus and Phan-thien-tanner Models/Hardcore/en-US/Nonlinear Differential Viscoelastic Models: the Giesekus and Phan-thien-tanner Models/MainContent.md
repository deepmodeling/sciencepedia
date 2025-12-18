## Introduction
The behavior of [complex fluids](@entry_id:198415) like polymer melts and solutions often defies simple description. While linear [viscoelastic models](@entry_id:192483) provide a crucial starting point, they fail to capture the rich and technologically significant phenomena—such as [shear-thinning](@entry_id:150203) and normal stress differences—that emerge under the strong flow conditions typical of industrial processing and biological systems. This limitation creates a knowledge gap, necessitating the use of more sophisticated theoretical frameworks that account for the inherent nonlinearity of [polymer dynamics](@entry_id:146985).

This article delves into two of the most successful and widely used nonlinear differential [constitutive equations](@entry_id:138559): the Giesekus model and the Phan-Thien–Tanner (PTT) model. By introducing distinct physical mechanisms to the foundational Upper-Convected Maxwell model, these theories provide a powerful lens for understanding and predicting complex rheology. The reader will embark on a structured exploration of these models. The first chapter, **Principles and Mechanisms**, will deconstruct the physical origins and mathematical forms of the Giesekus model's anisotropic drag and the PTT model's stress-dependent relaxation. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these models are used to interpret experimental data, guide computational simulations, and solve problems in fields ranging from polymer engineering to biofluid mechanics. Finally, **Hands-On Practices** will offer guided problems to solidify the theoretical concepts and build practical analytical skills.

We begin by examining the theoretical underpinnings of these models, starting from their common ancestor, the Upper-Convected Maxwell model, to understand how nonlinearity is mathematically and physically introduced.

## Principles and Mechanisms

While linear [viscoelastic models](@entry_id:192483), such as the Upper-Convected Maxwell (UCM) model, provide a foundational understanding of the time-dependent mechanical response of polymeric fluids, they are fundamentally limited to the regime of small and slow deformations. Many of the most characteristic and technologically important behaviors of complex fluids—such as [shear-thinning](@entry_id:150203) viscosity, stress overshoot in transient flows, and the emergence of [normal stress differences](@entry_id:191914) in steady shear—are inherently nonlinear phenomena. To capture this rich rheology, we must extend our theoretical framework to include nonlinear [constitutive equations](@entry_id:138559). This chapter elucidates the principles and mechanisms underpinning two of the most influential classes of nonlinear differential [viscoelastic models](@entry_id:192483): the Giesekus model and the Phan-Thien–Tanner (PTT) model.

### The Upper-Convected Maxwell Model as a Baseline

The starting point for developing many nonlinear models is the Upper-Convected Maxwell (UCM) model. It represents the simplest description of a fluid with elastic memory, often conceptualized through a microscopic picture of Hookean dumbbells suspended in a Newtonian solvent. Its [constitutive equation](@entry_id:267976) for the polymer extra stress tensor, $\boldsymbol{\tau}$, is given by:

$$
\lambda \overset{\nabla}{\boldsymbol{\tau}} + \boldsymbol{\tau} = 2 \eta_p \boldsymbol{D}
$$

Here, $\lambda$ is the characteristic relaxation time of the polymer, $\eta_p$ is the polymer contribution to the viscosity, and $\boldsymbol{D}$ is the symmetric [rate-of-deformation tensor](@entry_id:184787), defined as $\boldsymbol{D} = \frac{1}{2}(\nabla\boldsymbol{v} + (\nabla\boldsymbol{v})^{\mathrm{T}})$, where $\boldsymbol{v}$ is the velocity field.

A crucial element of this equation is the use of the **upper-convected time derivative**, $\overset{\nabla}{\boldsymbol{\tau}}$. For a generic second-order tensor $\boldsymbol{T}$, it is defined as:

$$
\overset{\nabla}{\boldsymbol{T}} = \frac{\mathrm{D}\boldsymbol{T}}{\mathrm{D}t} - (\nabla\boldsymbol{v})\cdot\boldsymbol{T} - \boldsymbol{T}\cdot(\nabla\boldsymbol{v})^{\mathrm{T}}
$$

where $\frac{\mathrm{D}}{\mathrm{D}t}$ is the material derivative and $\nabla\boldsymbol{v}$ is the [velocity gradient tensor](@entry_id:270928). The use of an [objective time derivative](@entry_id:1129024) like the upper-convected derivative is essential to ensure that the constitutive law is independent of the observer's frame of reference, a principle known as **[material frame indifference](@entry_id:166014)**. The specific form of the upper-convected derivative arises naturally from the kinematic description of deforming microstructures, such as the end-to-end vector of a polymer chain. Any valid nonlinear generalization built upon this microstructural foundation must retain this objective character and, in the limit of small deformations where nonlinear effects are negligible, should revert back to the UCM form.

### The Giesekus Model: Anisotropic Hydrodynamic Drag

The first major path to a physically motivated nonlinear model involves introducing a more sophisticated description of the dissipative forces acting on the polymer chains. The UCM model implicitly assumes that the hydrodynamic drag experienced by the polymer microstructure is isotropic—that is, the resistance to motion is the same in all directions. However, as a polymer chain becomes oriented and stretched by a flow, it presents an anisotropic profile to the surrounding solvent. It is physically plausible that the drag force would be different for motion parallel to the chain's backbone versus perpendicular to it. This concept of **anisotropic drag** or **anisotropic mobility** is the central mechanism of the Giesekus model.

This physical idea is translated into the mathematical framework by adding a new term to the UCM equation that is quadratic in the stress tensor. The general form of the single-mode Giesekus model is:

$$
\lambda \overset{\nabla}{\boldsymbol{\tau}} + \boldsymbol{\tau} + \alpha \frac{\lambda}{\eta_p} \boldsymbol{\tau}\cdot\boldsymbol{\tau} = 2\eta_p \boldsymbol{D}
$$

The new term, $\alpha \frac{\lambda}{\eta_p} \boldsymbol{\tau}\cdot\boldsymbol{\tau}$, accounts for the additional dissipation arising from the anisotropic drag. The dimensionless parameter $\alpha$ is known as the **anisotropy factor** or **mobility parameter**.

From a thermodynamic perspective, the rate of [energy dissipation](@entry_id:147406) must be non-negative. This fundamental constraint imposes limits on the value of $\alpha$. A detailed analysis of the underlying kinetic theory, where the hydrodynamic mobility tensor must remain positive-definite, reveals that the mobility parameter must lie in the range $0 \le \alpha \le 1$. When $\alpha = 0$, the quadratic term vanishes, and we recover the UCM model. The other limit, $\alpha=1$, corresponds to the maximum physically permissible anisotropy in this formulation. Models with a negative sign on the quadratic term would imply an unphysical decrease in dissipation and are thus thermodynamically inadmissible. The Giesekus model, with its quadratic stress nonlinearity, provides a robust framework for describing phenomena like shear-thinning and non-zero second normal stress differences.

### The Phan-Thien–Tanner (PTT) Model: Stress-Dependent Relaxation

An alternative approach to nonlinearity focuses not on the [dissipative forces](@entry_id:166970) but on the elastic relaxation mechanism. In concentrated solutions or melts, polymers form a transient network. Under flow, network junctions can be created and destroyed, and chains can slip past one another. The Phan-Thien–Tanner (PTT) model captures this by postulating that the rate of [stress relaxation](@entry_id:159905) is not constant, but instead increases as the polymer chains are stretched. The more deformed the network, the higher the probability of [disentanglement](@entry_id:637294) or "slip," leading to an accelerated return to equilibrium.

This mechanism is incorporated into the UCM framework by multiplying the elastic stress term, $\boldsymbol{\tau}$, by a scalar function, $f$, that depends on the magnitude of the stress. Since the function must be independent of the coordinate system, it is typically chosen to depend on an invariant of the stress tensor, most commonly its trace, $\mathrm{tr}(\boldsymbol{\tau})$. The general form of the PTT model is thus:

$$
\lambda \overset{\nabla}{\boldsymbol{\tau}} + f(\mathrm{tr}\,\boldsymbol{\tau}) \boldsymbol{\tau} = 2\eta_p \boldsymbol{D}
$$

For the model to be consistent with [linear viscoelasticity](@entry_id:181219), the function $f$ must approach unity as the stress vanishes, i.e., $f(s) \to 1$ as $s \to 0$. Common choices for this function include:

-   **Linear PTT model:** $f(\mathrm{tr}\,\boldsymbol{\tau}) = 1 + \varepsilon \frac{\lambda}{\eta_p} \mathrm{tr}(\boldsymbol{\tau})$
-   **Exponential PTT model:** $f(\mathrm{tr}\,\boldsymbol{\tau}) = \exp\left(\varepsilon \frac{\lambda}{\eta_p} \mathrm{tr}(\boldsymbol{\tau})\right)$

In these forms, $\varepsilon$ is a dimensionless parameter related to the chain slip or network destruction mechanism. Thermodynamic consistency requires that the function $f$ be non-negative. For rheological stability, such as ensuring that the shear stress is a monotonic function of the shear rate, it is also typically required that $f$ be a [non-decreasing function](@entry_id:202520) of its argument, which implies $\varepsilon \ge 0$ for the standard forms. The PTT model is particularly successful at describing the extensional properties of polymer melts and solutions.

### Rheological Fingerprints in Steady Simple Shear

The ultimate test of a [constitutive model](@entry_id:747751) is its ability to predict rheological behavior observed in [canonical flows](@entry_id:188303). Steady [simple shear](@entry_id:180497), with a velocity field $\boldsymbol{v} = (\dot{\gamma}y, 0, 0)$, provides a crucial testbed for evaluating and distinguishing these nonlinear models. In this flow, a viscoelastic fluid exhibits not only a shear stress, $\tau_{12}$ (where 1 is the flow direction and 2 is the gradient direction), but also **normal stress differences**. These are defined as:

-   **First Normal Stress Difference:** $N_1 = \tau_{11} - \tau_{22}$
-   **Second Normal Stress Difference:** $N_2 = \tau_{22} - \tau_{33}$

These quantities represent tensions along the streamlines that are a hallmark of [viscoelasticity](@entry_id:148045). To analyze the predictions of the Giesekus and PTT models, we can perform an [asymptotic expansion](@entry_id:149302) for small shear rates, or equivalently, for small Weissenberg numbers, $\mathrm{Wi} = \lambda\dot{\gamma}$. This approach reveals the leading-order behavior of the models and provides a powerful consistency check.

For steady [simple shear](@entry_id:180497), the component form of the Giesekus and PTT model equations can be solved perturbatively. At the lowest order in shear rate, $\mathcal{O}(\dot{\gamma})$, both models correctly predict a linear relationship between shear stress and shear rate, $\tau_{12} = \eta_p \dot{\gamma}$. The nonlinearities manifest at higher orders.

At the second order, $\mathcal{O}(\dot{\gamma}^2)$, we find the leading-order expressions for the normal stresses. A systematic expansion yields distinct results for the two models:

**Giesekus Model:**
-   $N_1 = 2 \eta_p \lambda \dot{\gamma}^2 + \mathcal{O}(\dot{\gamma}^4)$
-   $N_2 = -\alpha \eta_p \lambda \dot{\gamma}^2 + \mathcal{O}(\dot{\gamma}^4)$

**Linear PTT Model:**
-   $N_1 = 2 \eta_p \lambda \dot{\gamma}^2 + \mathcal{O}(\dot{\gamma}^4)$
-   $N_2 = 0 + \mathcal{O}(\dot{\gamma}^4)$

These results are highly instructive. First, both models predict the same leading-order behavior for the first normal stress difference, $N_1$, which is positive and quadratic in the shear rate. This result is consistent with the simpler UCM model and serves as a fundamental check on their shared theoretical basis.

The crucial distinction lies in the prediction for the second [normal stress difference](@entry_id:199507), $N_2$. The Giesekus model predicts a non-zero, negative $N_2$ that is directly proportional to the mobility parameter $\alpha$. This is a significant success, as a negative $N_2$ is experimentally observed for many polymer solutions. In the limit of small shear rates, the Giesekus model predicts a constant ratio between the two normal stress differences:

$$
\lim_{\dot{\gamma} \to 0} \frac{N_2}{N_1} = \frac{-\alpha \eta_p \lambda \dot{\gamma}^2}{2 \eta_p \lambda \dot{\gamma}^2} = -\frac{\alpha}{2}
$$

This remarkable result provides a direct rheological interpretation of the microscopic mobility parameter $\alpha$. By measuring the ratio of normal stress differences in the low-shear limit, one can directly estimate the degree of hydrodynamic anisotropy in the system as described by the Giesekus model. In contrast, the [linear form](@entry_id:751308) of the PTT model predicts a zero second normal stress difference at this order of approximation, indicating that its specific nonlinear mechanism does not generate this particular rheological feature in the same direct manner. This highlights how different physical assumptions embedded within the models lead to distinct and experimentally distinguishable "fingerprints" in the fluid's mechanical response.