## Introduction
Predicting the transition from reversible elastic deformation to permanent plastic deformation is a cornerstone of engineering design, ensuring the safety and integrity of structures made from ductile metals. Isotropic [yield criteria](@entry_id:178101) are the fundamental mathematical tools used in solid mechanics to define the precise stress conditions under which this transition, known as yielding, occurs. These models provide a critical link between the complex, multiaxial stress state within a component and a simple, measurable material property like its tensile yield strength. This article demystifies the theoretical underpinnings and practical applications of the most important [isotropic yield criteria](@entry_id:204294).

This exploration is structured to build a robust understanding from first principles to real-world relevance. The first chapter, **"Principles and Mechanisms,"** delves into the foundational concepts governing the formulation of any [yield criterion](@entry_id:193897), including objectivity and [isotropy](@entry_id:159159). It will establish the physical basis for pressure-insensitivity in ductile metals and show how this leads to the development of the two most prominent models: the von Mises and Tresca criteria. Next, **"Applications and Interdisciplinary Connections"** bridges theory and practice. It demonstrates how these criteria are calibrated and applied in canonical engineering problems, from analyzing rotating shafts to designing pressure vessels. This chapter also explores the boundaries of these models, revealing their connections to advanced fields like fracture mechanics, [damage mechanics](@entry_id:178377), and [cyclic plasticity](@entry_id:176411). Finally, the **"Hands-On Practices"** section provides a series of targeted problems designed to solidify your understanding through direct application of the concepts discussed. By navigating these chapters, you will gain a comprehensive understanding of how to model the onset of plasticity in ductile metals, a skill essential for any advanced study in [materials mechanics](@entry_id:189503). We begin by examining the core principles that shape these powerful predictive tools.

## Principles and Mechanisms

The transition from elastic to [plastic deformation](@entry_id:139726) in ductile metals is a fundamental phenomenon in [solid mechanics](@entry_id:164042), marking the onset of permanent, irrecoverable strain. A yield criterion is a mathematical rule, expressed as a scalar function of the stress state, that defines the boundary of the elastic domain in [stress space](@entry_id:199156). For a material to yield, the stress state must lie on a specific surface known as the [yield surface](@entry_id:175331). This chapter delineates the foundational principles and physical mechanisms that underpin the formulation of [isotropic yield criteria](@entry_id:204294) for ductile metals.

### Fundamental Constraints on Yield Functions

The formulation of any constitutive law, including a [yield criterion](@entry_id:193897), is governed by fundamental physical principles. For a yield function $f$ that depends on the Cauchy stress tensor $\boldsymbol{\sigma}$, these principles impose significant constraints on its mathematical form.

#### Objectivity and Isotropy

A [constitutive model](@entry_id:747751) must be independent of the observer's frame of reference, a principle known as **[material frame-indifference](@entry_id:178419)** or **objectivity**. For a scalar-valued function like the [yield criterion](@entry_id:193897), this means that its value must be unchanged by a superposed [rigid body rotation](@entry_id:167024). If $\mathbf{Q}$ is a proper orthogonal tensor representing such a rotation, the Cauchy stress tensor transforms as $\boldsymbol{\sigma} \mapsto \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\top}$. Objectivity thus demands that $f(\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\top}) = f(\boldsymbol{\sigma})$ for all such $\mathbf{Q}$ [@problem_id:2896249].

Furthermore, for an **isotropic** material, there are no preferred material directions. This implies that the material response should be identical if the material is rotated relative to the loading axes. For a scalar function of the stress tensor, this property imposes the same mathematical constraint as objectivity.

#### Representation Theorems and Stress Invariants

A central result from [continuum mechanics](@entry_id:155125), known as the [representation theorem](@entry_id:275118) for isotropic scalar functions, states that any function satisfying the objectivity and isotropy conditions can depend on its tensor argument only through its **[principal invariants](@entry_id:193522)**. A symmetric second-order tensor like $\boldsymbol{\sigma}$ has three [principal invariants](@entry_id:193522), which are independent of the coordinate system chosen. They can be expressed in several equivalent forms.

One representation is through the eigenvalues, or **[principal stresses](@entry_id:176761)** $(\sigma_1, \sigma_2, \sigma_3)$, of the stress tensor. The [yield function](@entry_id:167970) must be a symmetric function of these eigenvalues [@problem_id:2896249]:
$$
f(\boldsymbol{\sigma}) = G(\sigma_1, \sigma_2, \sigma_3)
$$
where $G$ is invariant under any permutation of its arguments.

Alternatively, the invariants can be expressed directly in terms of the tensor components:
- First invariant: $I_1 = \operatorname{tr}(\boldsymbol{\sigma}) = \sigma_{kk}$
- Second invariant: $I_2 = \frac{1}{2}[(\operatorname{tr}\boldsymbol{\sigma})^2 - \operatorname{tr}(\boldsymbol{\sigma}^2)]$
- Third invariant: $I_3 = \det(\boldsymbol{\sigma})$

Thus, an isotropic [yield function](@entry_id:167970) can always be written as $f(\boldsymbol{\sigma}) = \hat{F}(I_1, I_2, I_3)$. These fundamental principles provide a general mathematical structure, but they do not specify the precise form of the function. To develop specific, predictive models, we must incorporate the physical mechanisms of plastic deformation.

### The Physics of Yielding in Ductile Metals

The most crucial experimental observation for ductile metals at moderate temperatures is that their yielding is largely unaffected by the application of a uniform hydrostatic pressure. This property is known as **pressure-insensitivity**.

#### The Hydrostatic-Deviatoric Decomposition

To mathematically analyze pressure-insensitivity, we decompose the stress tensor into two physically distinct parts: a **hydrostatic** (or spherical) part that tends to change the volume of the material, and a **deviatoric** part that tends to change its shape (distortion). Any symmetric stress tensor $\boldsymbol{\sigma}$ can be uniquely decomposed as [@problem_id:2896244]:
$$
\boldsymbol{\sigma} = \boldsymbol{s} + p\boldsymbol{I}
$$
where $\boldsymbol{I}$ is the identity tensor, $p$ is the **mean stress** or **[hydrostatic pressure](@entry_id:141627)**, and $\boldsymbol{s}$ is the **[deviatoric stress tensor](@entry_id:267642)**. The [mean stress](@entry_id:751819) is defined as one-third of the trace of the stress tensor:
$$
p = \frac{1}{3} \operatorname{tr}(\boldsymbol{\sigma}) = \frac{1}{3}I_1 = \frac{1}{3}(\sigma_1 + \sigma_2 + \sigma_3)
$$
The [deviatoric stress](@entry_id:163323) is the remainder, $\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$. By its construction, the [deviatoric stress tensor](@entry_id:267642) is always traceless, i.e., $\operatorname{tr}(\boldsymbol{s}) = 0$.

The experimental observation of pressure-insensitivity directly implies that the [yield function](@entry_id:167970) should not depend on the hydrostatic part of the stress, $p\boldsymbol{I}$. This means the yield condition must depend only on the [deviatoric stress tensor](@entry_id:267642) $\boldsymbol{s}$. Since $\boldsymbol{s}$ is itself an [isotropic tensor](@entry_id:189108) function of $\boldsymbol{\sigma}$, the [yield function](@entry_id:167970) for a pressure-insensitive material can be expressed in terms of the invariants of $\boldsymbol{s}$ [@problem_id:2896219]. The [principal invariants](@entry_id:193522) of $\boldsymbol{s}$ are conventionally denoted $J_1$, $J_2$, and $J_3$.
- First deviatoric invariant: $J_1 = \operatorname{tr}(\boldsymbol{s}) = 0$ (by definition).
- Second deviatoric invariant: $J_2 = \frac{1}{2}\operatorname{tr}(\boldsymbol{s}^2) = \frac{1}{2}s_{ij}s_{ji}$.
- Third deviatoric invariant: $J_3 = \det(\boldsymbol{s}) = \frac{1}{3}\operatorname{tr}(\boldsymbol{s}^3)$.

Therefore, the general form of a pressure-insensitive, isotropic yield criterion simplifies to $\Phi(J_2, J_3) = 0$ [@problem_id:2896282]. The dependence on $I_1$ is dropped. This is a modeling choice based on experimental evidence, not a consequence of objectivity or [isotropy](@entry_id:159159) alone [@problem_id:2896249].

#### Physical Rationale for Pressure-Insensitivity

This macroscopic observation has a firm basis in both microscopic physics and macroscopic thermodynamics.

At the micro-scale, [plastic deformation](@entry_id:139726) in crystalline metals is primarily driven by the motion of dislocations on [slip planes](@entry_id:158709), a process known as **[dislocation glide](@entry_id:275474)**. The force that drives this motion is the **[resolved shear stress](@entry_id:201022)** on the [slip system](@entry_id:155264). A state of pure [hydrostatic pressure](@entry_id:141627), $\boldsymbol{\sigma}=p\boldsymbol{I}$, produces a traction vector $p\boldsymbol{n}$ on any plane with normal $\boldsymbol{n}$. This traction is purely normal to the plane; there is no shear component. Consequently, hydrostatic pressure produces zero [resolved shear stress](@entry_id:201022) on any [slip system](@entry_id:155264) and cannot, by itself, cause [dislocation glide](@entry_id:275474) [@problem_id:2711750].

At the macro-scale, we consider the rate of plastic work dissipation per unit volume, $\dot{D}^p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$, where $\dot{\boldsymbol{\varepsilon}}^p$ is the plastic [strain rate tensor](@entry_id:198281). Experiments show that plastic flow in metals is nearly **isochoric** (volume-preserving), meaning $\operatorname{tr}(\dot{\boldsymbol{\varepsilon}}^p) \approx 0$. Substituting the [stress decomposition](@entry_id:272862) into the dissipation expression gives:
$$
\dot{D}^p = (\boldsymbol{s} + p\boldsymbol{I}) : \dot{\boldsymbol{\varepsilon}}^p = \boldsymbol{s} : \dot{\boldsymbol{\varepsilon}}^p + p (\boldsymbol{I} : \dot{\boldsymbol{\varepsilon}}^p) = \boldsymbol{s} : \dot{\boldsymbol{\varepsilon}}^p + p \operatorname{tr}(\dot{\boldsymbol{\varepsilon}}^p)
$$
Since $\operatorname{tr}(\dot{\boldsymbol{\varepsilon}}^p) \approx 0$, the [plastic dissipation](@entry_id:201273) reduces to $\dot{D}^p \approx \boldsymbol{s} : \dot{\boldsymbol{\varepsilon}}^p$. The hydrostatic component of stress does no [plastic work](@entry_id:193085). It is therefore reasonable to assume that it does not influence the onset of yielding [@problem_id:2896219].

The invariance of key quantities to hydrostatic stress can be explicitly verified. Consider a stress state $\boldsymbol{\sigma}^{(a)}$ and a second state $\boldsymbol{\sigma}^{(b)} = \boldsymbol{\sigma}^{(a)} + C\boldsymbol{I}$ formed by superposing a hydrostatic stress of magnitude $C$. The [deviatoric stress tensor](@entry_id:267642) is unchanged: $\boldsymbol{s}^{(b)} = \boldsymbol{s}^{(a)}$. Consequently, its invariants $J_2$ and $J_3$ are also unchanged. Likewise, the [principal stresses](@entry_id:176761) are simply shifted, $\sigma_i^{(b)} = \sigma_i^{(a)} + C$. The differences between principal stresses remain the same, e.g., $\sigma_1^{(b)} - \sigma_3^{(b)} = (\sigma_1^{(a)} + C) - (\sigma_3^{(a)} + C) = \sigma_1^{(a)} - \sigma_3^{(a)}$. This means the maximum shear stress, $\tau_{\max} = (\sigma_{\max} - \sigma_{\min})/2$, is also invariant under hydrostatic shifts [@problem_id:2896271].

### The von Mises Yield Criterion (Distortion Energy Criterion)

The most widely used yield criterion for ductile metals is the **von Mises criterion**, also known as the $J_2$ or maximum [distortion energy](@entry_id:198925) criterion.

#### Formulation and Energetic Basis

The von Mises criterion arises from the hypothesis that yielding begins when the **elastic [distortion energy](@entry_id:198925) density**, $U_d$, reaches a critical value characteristic of the material. The total [elastic strain energy](@entry_id:202243) density in an isotropic body can be decomposed into a volumetric part, $U_v$, associated with volume change, and a distortional part, $U_d$, associated with shape change. For a linear elastic material with shear modulus $G$, the [distortion energy](@entry_id:198925) density is given by [@problem_id:2711750]:
$$
U_d = \frac{1}{2G} J_2
$$
The hypothesis that yielding occurs when $U_d$ equals a critical value is therefore equivalent to stating that yielding occurs when $J_2$ reaches a critical value. The von Mises [yield criterion](@entry_id:193897) is thus:
$$
J_2 = k^2
$$
where $k$ is a material constant. This formulation inherently assumes that the yield behavior is independent of $J_3$ and thus of the Lode angle, which describes the "shape" of the [deviatoric stress](@entry_id:163323) state [@problem_id:2896282].

To determine the constant $k$, we calibrate the criterion using a simple [uniaxial tension test](@entry_id:195375). At yield, the stress state is $\sigma_1 = \sigma_Y$ and $\sigma_2 = \sigma_3 = 0$, where $\sigma_Y$ is the material's yield strength in tension. For this state, $p = \sigma_Y/3$, and the [deviatoric stress](@entry_id:163323) components are $s_1 = 2\sigma_Y/3$, $s_2 = s_3 = -\sigma_Y/3$. The value of $J_2$ is:
$$
J_2 = \frac{1}{2}(s_1^2 + s_2^2 + s_3^2) = \frac{1}{2}\left[\left(\frac{2\sigma_Y}{3}\right)^2 + \left(-\frac{\sigma_Y}{3}\right)^2 + \left(-\frac{\sigma_Y}{3}\right)^2\right] = \frac{1}{3}\sigma_Y^2
$$
Thus, the critical value is $k^2 = \sigma_Y^2/3$. The von Mises yield condition is $J_2 = \sigma_Y^2/3$.

It is convenient to define the **von Mises [equivalent stress](@entry_id:749064)**, $\sigma_{\mathrm{eq}}$ (or $\sigma_v$), such that yielding occurs when $\sigma_{\mathrm{eq}} = \sigma_Y$. By setting $J_2 = \sigma_{\mathrm{eq}}^2/3$, we find:
$$
\sigma_{\mathrm{eq}} = \sqrt{3J_2}
$$
The von Mises criterion is simply $\sigma_{\mathrm{eq}} = \sigma_Y$. Using the relation between $J_2$ and principal stresses, we can write the [equivalent stress](@entry_id:749064) as:
$$
\sigma_{\mathrm{eq}} = \sqrt{\frac{1}{2}[(\sigma_1 - \sigma_2)^2 + (\sigma_2 - \sigma_3)^2 + (\sigma_3 - \sigma_1)^2]}
$$
For a general plane stress state in the $x-y$ plane, this becomes $\sigma_{\mathrm{eq}} = \sqrt{\sigma_x^2 - \sigma_x\sigma_y + \sigma_y^2 + 3\tau_{xy}^2}$.

#### Geometric Interpretation and Properties

In the 3D space of [principal stresses](@entry_id:176761) $(\sigma_1, \sigma_2, \sigma_3)$, the equation $\sigma_{\mathrm{eq}} = \sigma_Y$ describes a **right circular cylinder** whose central axis is the hydrostatic line $\sigma_1 = \sigma_2 = \sigma_3$. The cross-section of this cylinder in the **deviatoric plane** (the plane orthogonal to the hydrostatic axis, also known as the $\pi$-plane) is a **circle**. This circular shape reflects the criterion's independence from the third deviatoric invariant, $J_3$ [@problem_id:2896264].

A key prediction of the von Mises criterion concerns yielding in pure shear. For this state, the [principal stresses](@entry_id:176761) are $(\tau_Y, 0, -\tau_Y)$, where $\tau_Y$ is the shear [yield stress](@entry_id:274513). The [equivalent stress](@entry_id:749064) is $\sigma_{\mathrm{eq}} = \sqrt{3\tau_Y^2} = \tau_Y\sqrt{3}$. At yield, $\sigma_{\mathrm{eq}} = \sigma_Y$, which gives the prediction:
$$
\tau_Y = \frac{\sigma_Y}{\sqrt{3}} \approx 0.577\sigma_Y
$$

### The Tresca Yield Criterion (Maximum Shear Stress Criterion)

An alternative, historically earlier criterion was proposed by Henri Tresca based on a more direct physical hypothesis.

#### Formulation and Calibration

The **Tresca criterion** postulates that yielding initiates when the **maximum shear stress**, $\tau_{\max}$, at any point reaches a critical value, $k$. The maximum shear stress in a body is half the difference between the largest and smallest [principal stresses](@entry_id:176761):
$$
\tau_{\max} = \frac{\sigma_{\max} - \sigma_{\min}}{2} = \frac{\sigma_1 - \sigma_3}{2} \quad (\text{assuming } \sigma_1 \ge \sigma_2 \ge \sigma_3)
$$
The yield criterion is simply $\tau_{\max} = k$.

We calibrate this criterion using the same [uniaxial tension test](@entry_id:195375) where $\sigma_1 = \sigma_Y$, $\sigma_2 = 0$, $\sigma_3 = 0$. The maximum shear stress is $\tau_{\max} = (\sigma_Y - 0)/2 = \sigma_Y/2$. Thus, the critical shear stress is $k = \sigma_Y/2$. The Tresca criterion is therefore [@problem_id:2896225]:
$$
\tau_{\max} = \frac{\sigma_Y}{2}
$$
This can be written in terms of a [yield function](@entry_id:167970) $f_{\mathrm{Tr}}$ as:
$$
f_{\mathrm{Tr}}(\boldsymbol{\sigma}) = \max\{|\sigma_i - \sigma_j|\} - \sigma_Y = 0
$$

#### Geometric Interpretation and Properties

In [principal stress space](@entry_id:184388), the Tresca criterion is defined by six [linear equations](@entry_id:151487): $\sigma_1 - \sigma_2 = \pm\sigma_Y$, $\sigma_2 - \sigma_3 = \pm\sigma_Y$, and $\sigma_3 - \sigma_1 = \pm\sigma_Y$. These equations describe six planes that form a **right, regular hexagonal prism** whose axis is the hydrostatic line. Consequently, the yield locus in the deviatoric plane is a **regular hexagon**.

Unlike the smooth circle of the von Mises criterion, the Tresca hexagon has sharp corners and flat sides. This non-circular shape indicates that the Tresca criterion has a non-trivial dependence on the third deviatoric invariant, $J_3$, or equivalently, the Lode angle [@problem_id:2896282].

For the case of pure shear $(\tau_Y, 0, -\tau_Y)$, the [principal stresses](@entry_id:176761) are $\sigma_1 = \tau_Y$ and $\sigma_3 = -\tau_Y$. The maximum shear stress is $\tau_{\max} = (\tau_Y - (-\tau_Y))/2 = \tau_Y$. At yield, this must equal $\sigma_Y/2$. The Tresca criterion therefore predicts:
$$
\tau_Y = \frac{\sigma_Y}{2} = 0.5\sigma_Y
$$

### Comparison and Application

The von Mises and Tresca criteria are the two most common models for isotropic ductile metals. They offer different predictions that can be compared.

- **Conservatism:** In the deviatoric plane, the Tresca hexagon is inscribed within the von Mises circle. This means the Tresca locus always lies on or inside the von Mises locus. Therefore, for any stress state other than [uniaxial tension](@entry_id:188287) (where they agree), the **Tresca criterion is more conservative**, predicting yield at a lower or equal stress level than von Mises.

- **Shear Yield Prediction:** von Mises predicts $\tau_Y \approx 0.577\sigma_Y$, while Tresca predicts $\tau_Y = 0.5\sigma_Y$. Most experimental data for ductile metals fall between these two values, often closer to the von Mises prediction.

**Illustrative Example:**
Let's analyze a specific plane stress state to see the difference in predictions [@problem_id:2896242]. Consider the stress tensor:
$$
\boldsymbol{\sigma}=\begin{pmatrix} 120 & 30 & 0 \\ 30 & 80 & 0 \\ 0 & 0 & 40 \end{pmatrix} \text{ MPa}
$$
First, we find the [principal stresses](@entry_id:176761) by finding the eigenvalues of $\boldsymbol{\sigma}$. One eigenvalue is clearly $\sigma=40$ MPa. The other two are found from the $2\times2$ submatrix, yielding $\lambda^2 - 200\lambda + 8700 = 0$, which gives $\lambda = 100 \pm 10\sqrt{13}$. Ordering them, we have:
$\sigma_1 = 100 + 10\sqrt{13} \approx 136.06$ MPa
$\sigma_2 = 100 - 10\sqrt{13} \approx 63.94$ MPa
$\sigma_3 = 40$ MPa

Now, let's assume this stress state is applied proportionally, $\alpha\boldsymbol{\sigma}$, where $\alpha$ is a load multiplier. We want to find the value of $\alpha$ that causes yield according to each criterion.

- **Tresca Criterion:** Yield occurs when $\alpha \tau_{\max} = \sigma_Y/2$.
$\tau_{\max} = \frac{\sigma_1 - \sigma_3}{2} = \frac{(100 + 10\sqrt{13}) - 40}{2} = \frac{60 + 10\sqrt{13}}{2} = 30 + 5\sqrt{13}$.
Yield occurs when $\alpha_T (30 + 5\sqrt{13}) = \sigma_Y/2$, so $\alpha_T = \frac{\sigma_Y}{60 + 10\sqrt{13}}$.

- **von Mises Criterion:** Yield occurs when $\alpha \sigma_{\mathrm{eq}} = \sigma_Y$.
$\sigma_{\mathrm{eq}}^2 = \frac{1}{2}[(\sigma_1-\sigma_2)^2 + (\sigma_2-\sigma_3)^2 + (\sigma_3-\sigma_1)^2]$.
$\sigma_1-\sigma_2 = 20\sqrt{13}$
$\sigma_2-\sigma_3 = 60-10\sqrt{13}$
$\sigma_3-\sigma_1 = -60-10\sqrt{13}$
$\sigma_{\mathrm{eq}}^2 = \frac{1}{2}[(20\sqrt{13})^2 + (60-10\sqrt{13})^2 + (-60-10\sqrt{13})^2] = \frac{1}{2}[5200 + 2(3600+1300)] = 7500$.
So, $\sigma_{\mathrm{eq}} = \sqrt{7500} = 50\sqrt{3}$ MPa.
Yield occurs when $\alpha_{vM} (50\sqrt{3}) = \sigma_Y$, so $\alpha_{vM} = \frac{\sigma_Y}{50\sqrt{3}}$.

The ratio of predicted load multipliers is $\frac{\alpha_{vM}}{\alpha_T} = \frac{60+10\sqrt{13}}{50\sqrt{3}} = \frac{6+\sqrt{13}}{5\sqrt{3}} \approx 1.109$. This shows that for this specific stress state, the Tresca criterion predicts yielding at a load about 10% lower than the von Mises criterion.

### Advanced Topics: Flow Rules and Hardening

Yield criteria define the onset of plasticity. To describe the subsequent evolution of plastic strain, we need a **[flow rule](@entry_id:177163)** and a **hardening rule**.

#### The Associated Flow Rule

For [rate-independent plasticity](@entry_id:754082), the **[associated flow rule](@entry_id:201731)** is a standard assumption that states the direction of the plastic [strain rate tensor](@entry_id:198281) $\dot{\boldsymbol{\varepsilon}}^p$ is normal to the [yield surface](@entry_id:175331) at the current stress point:
$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\gamma} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$
where $\dot{\gamma} \ge 0$ is the [plastic multiplier](@entry_id:753519).

For the smooth, circular von Mises surface, the normal direction $\partial f / \partial \boldsymbol{\sigma} \propto \boldsymbol{s}$ is unique at every point. This guarantees a unique direction for plastic flow for any stress state on the yield surface.

The Tresca surface, however, is non-differentiable at its corners and edges. At a corner, where two faces meet, the normal is not unique. The [flow rule](@entry_id:177163) is generalized (Koiter's rule) to state that the [plastic flow](@entry_id:201346) vector can lie anywhere within the convex cone formed by the normals of the adjacent intersecting faces. This means the direction of [plastic flow](@entry_id:201346) is not uniquely determined by the stress state alone at a corner, a feature with significant theoretical and computational consequences [@problem_id:2896228].

#### Hardening Rules

As a material deforms plastically, its resistance to further yielding typically changes. This phenomenon is called **hardening**. The evolution of the yield surface is described by hardening rules.
- **Isotropic Hardening:** The yield surface expands uniformly in all directions, without changing its shape or center. The size of the surface is controlled by a scalar internal variable, $\kappa$ (e.g., equivalent plastic strain), so the yield condition becomes $\sigma_{\mathrm{eq}} - \sigma_Y(\kappa) = 0$. The center of the yield surface remains at the origin in deviatoric stress space [@problem_id:2896251].
- **Kinematic Hardening:** The yield surface translates in deviatoric stress space without changing its size or shape. This is used to model phenomena like the Bauschinger effect. The translation is described by a tensorial internal variable called the **backstress**, $\boldsymbol{\alpha}$. The yield condition is expressed in terms of a **relative stress**, $\boldsymbol{\eta} = \boldsymbol{s} - \boldsymbol{\alpha}$, as $f(\boldsymbol{\eta}) = \sqrt{J_2(\boldsymbol{\eta})} - k_0 = 0$. The plastic flow direction is now normal to the translated surface, i.e., in the direction of $\boldsymbol{\eta}$ [@problem_id:2896251].

These concepts form the basis for [computational plasticity](@entry_id:171377), where algorithms like the **[radial return](@entry_id:754007) method** are used to integrate these equations and predict material behavior under complex loading paths.