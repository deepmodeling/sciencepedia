## Introduction
In the realm of [solid mechanics](@entry_id:164042), understanding how materials deform permanently under load is crucial for the design and analysis of countless engineering applications, especially in [metal forming](@entry_id:188560) and structural safety. While comprehensive elasto-plastic models offer high fidelity, their complexity can be prohibitive. The theory of [rigid-perfectly plastic](@entry_id:195711) flow provides a powerful and simplified alternative, focusing on scenarios where plastic deformation is the dominant mechanism. This article addresses the need for a foundational understanding of this model by developing it from first principles, culminating in the celebrated Lévy-Mises equations.

This article will guide you through the core tenets of this essential theory across three comprehensive chapters. We will begin in **Principles and Mechanisms** by constructing the model from the ground up, starting with the [rigid-perfectly plastic](@entry_id:195711) idealization, introducing the von Mises [yield criterion](@entry_id:193897), and deriving the Lévy-Mises equations via the [associative flow rule](@entry_id:163391). Next, **Applications and Interdisciplinary Connections** will bridge theory and practice by demonstrating how these principles are applied to analyze [metal forming](@entry_id:188560) processes, incorporated into [limit analysis theorems](@entry_id:183403), and connected to advanced fields like [computational plasticity](@entry_id:171377) and fluid mechanics. Finally, the **Hands-On Practices** section provides targeted problems to solidify your understanding of the key computational steps involved in applying the theory. By the end, you will have a robust conceptual and practical grasp of the Lévy-Mises equations and their role in modern mechanics.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanics that constitute the classical theory of [rigid-perfectly plastic](@entry_id:195711) flow. We will construct this framework from first principles, beginning with the idealizations that define the model and proceeding to the constitutive laws that govern material response. Our focus will be on the celebrated Lévy-Mises equations, which arise from the combination of the von Mises yield criterion and an [associative flow rule](@entry_id:163391).

### The Rigid-Perfectly Plastic Idealization

The theory of [rigid-perfectly plastic](@entry_id:195711) flow is a powerful idealization used to model phenomena, such as large-scale [metal forming](@entry_id:188560), where plastic deformations are dominant. The framework rests upon a set of foundational assumptions and governing equations. The primary idealization is the neglect of elastic strains. In a general elasto-plastic material, the total [strain rate tensor](@entry_id:198281), $\dot{\boldsymbol{\varepsilon}}$, is additively decomposed into an elastic part, $\dot{\boldsymbol{\varepsilon}}^{e}$, and a plastic part, $\dot{\boldsymbol{\varepsilon}}^{p}$. The rigid-plastic model assumes the material is perfectly rigid prior to yielding, meaning $\dot{\boldsymbol{\varepsilon}}^{e} = \boldsymbol{0}$. Consequently, the total [strain rate](@entry_id:154778) is identical to the plastic strain rate:

$$
\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^{p}
$$

This simplification is most appropriate for monotonic loading processes where the accumulated plastic strain is significantly larger than the [elastic strain](@entry_id:189634), i.e., $|\boldsymbol{\varepsilon}^{p}| \gg |\boldsymbol{\varepsilon}^{e}|$.

For a body undergoing deformation, the governing unknowns are typically the [velocity field](@entry_id:271461), $\boldsymbol{v}(\boldsymbol{x}, t)$, and the Cauchy stress [tensor field](@entry_id:266532), $\boldsymbol{\sigma}(\boldsymbol{x}, t)$. These fields are constrained by the universal balance laws and kinematic definitions [@problem_id:2654506]. In the absence of inertial effects (i.e., for quasi-static processes), the [balance of linear momentum](@entry_id:193575) reduces to the [equilibrium equation](@entry_id:749057):

$$
\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0}
$$

where $\boldsymbol{b}$ represents [body forces](@entry_id:174230) per unit volume. The [balance of angular momentum](@entry_id:181848) further requires the Cauchy stress tensor to be symmetric, $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\top}$.

The kinematic link between the [velocity field](@entry_id:271461) and the [strain rate](@entry_id:154778) is provided by the [rate-of-deformation tensor](@entry_id:184787), defined for small strains as:

$$
\dot{\boldsymbol{\varepsilon}} = \frac{1}{2} \left( \nabla \boldsymbol{v} + (\nabla \boldsymbol{v})^{\top} \right)
$$

These equations of balance and kinematics must be supplemented by a [constitutive model](@entry_id:747751) that describes the material's specific response, connecting the stress $\boldsymbol{\sigma}$ to the [strain rate](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$.

### The von Mises Yield Criterion and Pressure-Insensitivity

A cornerstone of [metal plasticity](@entry_id:176585) is the observation that the onset of [plastic flow](@entry_id:201346) is largely independent of the applied hydrostatic pressure. Plastic deformation in crystalline metals is driven by shear stresses that cause [dislocation motion](@entry_id:143448), a process that inherently conserves volume. To capture this behavior mathematically, the Cauchy stress tensor $\boldsymbol{\sigma}$ is decomposed into its hydrostatic and deviatoric parts:

$$
\boldsymbol{\sigma} = \boldsymbol{s} + p \boldsymbol{I}
$$

Here, $p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$ is the hydrostatic stress (or [mean stress](@entry_id:751819)), and $\boldsymbol{s}$ is the [deviatoric stress tensor](@entry_id:267642), which is, by definition, traceless: $\mathrm{tr}(\boldsymbol{s}) = 0$.

The **von Mises [yield criterion](@entry_id:193897)** formalizes this pressure-insensitivity by positing that yielding occurs when a scalar measure of the [deviatoric stress](@entry_id:163323) reaches a critical value. This measure is the **von Mises [equivalent stress](@entry_id:749064)**, $\sigma_{\mathrm{eq}}$, defined as:

$$
\sigma_{\mathrm{eq}} = \sqrt{\frac{3}{2} \boldsymbol{s}:\boldsymbol{s}}
$$

The term $\boldsymbol{s}:\boldsymbol{s} = s_{ij}s_{ij}$ is twice the second invariant of the [deviatoric stress](@entry_id:163323), $J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$. The yield condition is expressed via a yield function, $f(\boldsymbol{\sigma})$, such that the material remains rigid for $f  0$ and [plastic flow](@entry_id:201346) is possible when $f = 0$. For a perfectly plastic material with a uniaxial [yield strength](@entry_id:162154) $\sigma_y$, the von Mises yield function is:

$$
f(\boldsymbol{\sigma}) = \sigma_{\mathrm{eq}} - \sigma_y \le 0
$$

The condition $f(\boldsymbol{\sigma})=0$ defines the **[yield surface](@entry_id:175331)** in the nine-dimensional space of stress components. Since $f$ depends only on $\boldsymbol{s}$, it is independent of the [hydrostatic stress](@entry_id:186327) $p$. Consequently, a purely hydrostatic state of stress (i.e., one with $\boldsymbol{s}=\boldsymbol{0}$) gives $\sigma_{\mathrm{eq}}=0$, and the yield function becomes $f = -\sigma_y  0$. This confirms that a von Mises material cannot be made to yield under [hydrostatic pressure](@entry_id:141627) alone, regardless of its magnitude [@problem_id:2654568].

In the three-dimensional space of [principal stresses](@entry_id:176761) $(\sigma_1, \sigma_2, \sigma_3)$, the equation $f=0$ defines a right circular cylinder whose axis is the hydrostatic line $\sigma_1 = \sigma_2 = \sigma_3$ [@problem_id:2654560]. This geometry reflects that adding any amount of [hydrostatic pressure](@entry_id:141627) to a given stress state simply shifts the point along a line parallel to the cylinder's axis, never causing it to reach or cross the [yield surface](@entry_id:175331). The crucial feature of the von Mises [yield surface](@entry_id:175331) is its smoothness; it has no corners or edges. This is a direct consequence of its definition via the [smooth function](@entry_id:158037) $J_2$ [@problem_id:2654560]. This smoothness contrasts with other criteria, such as the Tresca (maximum shear stress) criterion, which corresponds to a hexagonal prism in [principal stress space](@entry_id:184388). The presence of edges and vertices on the Tresca surface leads to ambiguities in defining the direction of [plastic flow](@entry_id:201346), a complication not present in the von Mises formulation.

### The Associative Flow Rule and the Principle of Maximum Dissipation

Once the stress state reaches the [yield surface](@entry_id:175331), plastic deformation begins. The **[flow rule](@entry_id:177163)** is the [constitutive equation](@entry_id:267976) that determines the direction of the plastic [strain rate tensor](@entry_id:198281) $\dot{\boldsymbol{\varepsilon}}^p$. A profoundly important concept in plasticity is the **[associative flow rule](@entry_id:163391)**, which postulates that the direction of [plastic flow](@entry_id:201346) is normal (orthogonal) to the [yield surface](@entry_id:175331) in stress space.

This rule, also known as the [normality rule](@entry_id:182635), is not an arbitrary choice but can be derived from the more fundamental **principle of maximum [plastic dissipation](@entry_id:201273)** [@problem_id:2654620]. For an isothermal rigid-plastic material, the Clausius-Duhem inequality for [thermodynamic consistency](@entry_id:138886) reduces to the requirement that the rate of [plastic work](@entry_id:193085), or dissipation density, $\mathcal{D}^p$, must be non-negative:

$$
\mathcal{D}^p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p \ge 0
$$

The principle of maximum [plastic dissipation](@entry_id:201273) states that for a given plastic [strain rate](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p$, the true stress state $\boldsymbol{\sigma}$ is the one within the admissible elastic domain $\mathcal{E} = \{\boldsymbol{\sigma}^* | f(\boldsymbol{\sigma}^*) \le 0\}$ that maximizes this dissipation [@problem_id:2654579]. This can be formulated as a constrained optimization problem, the solution of which, via the Karush-Kuhn-Tucker (KKT) conditions, yields the [flow rule](@entry_id:177163):

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$

where $\dot{\lambda} \ge 0$ is a scalar known as the [plastic multiplier](@entry_id:753519). This equation is the mathematical statement of associativity: $\dot{\boldsymbol{\varepsilon}}^p$ is proportional to the gradient of the [yield function](@entry_id:167970), which is, by definition, a vector normal to the level sets of $f$.

This concept can be framed with greater generality using the tools of convex analysis. The principle of maximum [plastic dissipation](@entry_id:201273) is equivalent to stating that the plastic [strain rate](@entry_id:154778) lies in the [normal cone](@entry_id:272387) to the convex elastic domain, $\dot{\boldsymbol{\varepsilon}}^p \in \partial I_{\mathcal{E}}(\boldsymbol{\sigma})$, where $I_{\mathcal{E}}$ is the indicator function of the set $\mathcal{E}$ and $\partial I_{\mathcal{E}}$ denotes its [subdifferential](@entry_id:175641) [@problem_id:2654540].

### The Lévy-Mises Equations

The Lévy-Mises equations are the specific form of the [associative flow rule](@entry_id:163391) for a material obeying the von Mises yield criterion. To derive them, we compute the gradient of the von Mises yield function, $\partial f / \partial \boldsymbol{\sigma}$. Using the chain rule, and the fact that $\partial J_2 / \partial \boldsymbol{\sigma} = \boldsymbol{s}$, we find:

$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{\partial}{\partial \boldsymbol{\sigma}} \left(\sqrt{\frac{3}{2} \boldsymbol{s}:\boldsymbol{s}} - \sigma_y\right) = \frac{3}{2 \sigma_{\mathrm{eq}}} \boldsymbol{s}
$$

Substituting this gradient into the [associative flow rule](@entry_id:163391) gives the Lévy-Mises equations:

$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{3}{2 \sigma_{\mathrm{eq}}} \boldsymbol{s}
$$

This elegantly simple relationship states that the plastic [strain rate tensor](@entry_id:198281) is directly proportional to the [deviatoric stress tensor](@entry_id:267642). This has two immediate and profound consequences:

1.  **Plastic Incompressibility**: The trace of the plastic [strain rate tensor](@entry_id:198281) represents the rate of volume change. Taking the trace of the Lévy-Mises equation gives:
    $$
    \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \dot{\lambda} \frac{3}{2 \sigma_{\mathrm{eq}}} \mathrm{tr}(\boldsymbol{s}) = 0
    $$
    This is because the [deviatoric stress tensor](@entry_id:267642) is traceless. Therefore, plastic flow governed by the Lévy-Mises equations is isochoric (volume-preserving) [@problem_id:2654540]. This provides a deep connection between the physical observation of pressure-insensitivity and the kinematic outcome of [incompressibility](@entry_id:274914). It also explains why the hydrostatic part of the stress does no [plastic work](@entry_id:193085): $(p\boldsymbol{I}):\dot{\boldsymbol{\varepsilon}}^p = p\,\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = 0$ [@problem_id:2654555].

2.  **Coaxiality**: Since $\dot{\boldsymbol{\varepsilon}}^p$ is a scalar multiple of $\boldsymbol{s}$, the two tensors are coaxial. This means they share the same principal axes. If one knows the principal directions of the strain rate, one immediately knows the principal directions of the [deviatoric stress](@entry_id:163323), and vice versa. For example, in a material point where the [rate-of-deformation tensor](@entry_id:184787) $\boldsymbol{D} = \dot{\boldsymbol{\varepsilon}}^p$ is known, the orientation of the principal axes of the stress deviator $\boldsymbol{s}$ is identical to that of $\boldsymbol{D}$ [@problem_id:2654582].

### Scalar Measures and Work Conjugacy

While the Lévy-Mises equations provide a tensorial relationship, it is often useful to work with scalar measures of stress and strain. We have already defined the [equivalent stress](@entry_id:749064) $\sigma_{\mathrm{eq}}$. An energetically consistent scalar measure for the plastic strain rate is the **equivalent plastic strain rate**, $\dot{\bar{\varepsilon}}^p$, defined as:

$$
\dot{\bar{\varepsilon}}^p = \sqrt{\frac{2}{3} \dot{\boldsymbol{\varepsilon}}^p : \dot{\boldsymbol{\varepsilon}}^p}
$$

The factor $\sqrt{2/3}$ is chosen specifically to ensure consistency. By substituting the Lévy-Mises equation into this definition, we can find a direct relationship between the [plastic multiplier](@entry_id:753519) $\dot{\lambda}$ and the equivalent plastic strain rate. For the [yield function](@entry_id:167970) $f = \sigma_{\mathrm{eq}} - \sigma_y$, this relationship is simply [@problem_id:2654568]:

$$
\dot{\bar{\varepsilon}}^p = \dot{\lambda}
$$

This allows us to write the Lévy-Mises equations in an alternative and common form by replacing $\dot{\lambda}$ with $\dot{\bar{\varepsilon}}^p$. Most importantly, these scalar measures are **work-conjugate**. The [plastic dissipation](@entry_id:201273) density, $\mathcal{D}^p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$, can be expressed purely in terms of these scalar quantities [@problem_id:2654608]:

$$
\mathcal{D}^p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p = (\boldsymbol{s} + p\boldsymbol{I}) : \dot{\boldsymbol{\varepsilon}}^p = \boldsymbol{s} : \dot{\boldsymbol{\varepsilon}}^p = \sigma_{\mathrm{eq}} \dot{\bar{\varepsilon}}^p
$$

This elegant result confirms that the [equivalent stress](@entry_id:749064) and equivalent plastic strain rate form a proper work-conjugate pair, simplifying energy and dissipation calculations.

### The Complete Constitutive Framework: Loading-Unloading Conditions

The full theory of [rigid-perfectly plastic](@entry_id:195711) flow combines the equilibrium and [kinematic equations](@entry_id:173032) with the complete [constitutive law](@entry_id:167255). This law is not just the [flow rule](@entry_id:177163), but also a set of logical conditions that govern when [plastic flow](@entry_id:201346) occurs. These are encapsulated by the **Karush-Kuhn-Tucker (KKT)** conditions, derived from the principle of maximum dissipation [@problem_id:2654649]:

1.  **Yield Condition**: $f(\boldsymbol{\sigma}) \le 0$. The stress state must always remain within or on the boundary of the elastic (rigid) domain. Stress states outside the yield surface are inadmissible.

2.  **Flow Rule**: $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}$, with $\dot{\lambda} \ge 0$. The [plastic multiplier](@entry_id:753519) must be non-negative, ensuring that [plastic dissipation](@entry_id:201273) is non-negative.

3.  **Complementary Slackness**: $\dot{\lambda} f(\boldsymbol{\sigma}) = 0$. This condition provides the logical switch for plasticity. If the stress state is strictly within the [yield surface](@entry_id:175331) ($f  0$), then the multiplier must be zero ($\dot{\lambda}=0$), and no plastic flow occurs. Conversely, if plastic flow occurs ($\dot{\lambda}>0$), the stress state must be exactly on the yield surface ($f=0$).

For a perfectly plastic material, one more condition is crucial. During [plastic flow](@entry_id:201346) ($\dot{\lambda}>0, f=0$), the stress state must remain on the [yield surface](@entry_id:175331). This requires the time rate of change of the yield function to be zero. This is the **Prager consistency condition**:

$$
\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} = 0 \quad \text{if} \quad \dot{\lambda} > 0
$$

This condition constrains the admissible stress rates during [plastic loading](@entry_id:753518). Taken together, these conditions provide a complete and self-consistent mathematical model for [rigid-perfectly plastic](@entry_id:195711) flow under the von Mises criterion [@problem_id:2654506].

### Scope and Limitations of the Rigid-Plastic Model

It is vital to recognize that the rigid-plastic model, while powerful, is an idealization. Its validity is confined to specific physical regimes, and its limitations must be understood to avoid unphysical predictions [@problem_id:2654592].

The neglect of elasticity renders the model unsuitable for problems where elastic deformation is significant. This includes:
*   **Springback**: The analysis of part-shape changes after load removal is entirely dependent on the recovery of elastic strains. A rigid-plastic model predicts zero springback.
*   **Wave Propagation**: In high-rate dynamics, such as impact, stress waves propagate at speeds determined by [elastic moduli](@entry_id:171361). The rigid-plastic model assumes infinite wave speeds, making it incapable of capturing wave-mediated stress transients.
*   **Volumetric Changes**: Even though plastic flow in metals is isochoric, the material still experiences elastic volume changes under pressure according to its [bulk modulus](@entry_id:160069). If predicting density or thickness changes under high [hydrostatic stress](@entry_id:186327) is important, an elasto-plastic model is necessary.

Furthermore, the formulation presented here is based on infinitesimal [kinematics](@entry_id:173318). This assumption breaks down in scenarios involving [large deformations](@entry_id:167243):
*   **Large Strains and Rotations**: For processes involving large shear strains or significant material rotation, a finite-strain kinematic framework is required. This involves using [objective stress rates](@entry_id:199282) and appropriate [work-conjugate stress](@entry_id:182069)-[strain measures](@entry_id:755495) to ensure the model's predictions remain physically meaningful.

The rigid-plastic Lévy-Mises model is therefore most accurate and useful for analyzing quasi-static, monotonic forming processes where the final shape is determined primarily by large plastic strains, and unloading effects are of secondary concern. In these domains, it provides an excellent balance of physical fidelity and computational tractability.