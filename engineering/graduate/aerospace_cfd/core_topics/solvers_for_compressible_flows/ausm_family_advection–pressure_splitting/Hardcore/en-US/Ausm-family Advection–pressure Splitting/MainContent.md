## Introduction
The development of accurate and robust numerical methods for [hyperbolic conservation laws](@entry_id:147752) is a cornerstone of modern computational fluid dynamics (CFD). Among the most successful and versatile approaches are the schemes belonging to the Advection Upstream Splitting Method (AUSM) family. These methods address a fundamental challenge in CFD: how to design a [numerical flux](@entry_id:145174) that accurately reflects the distinct physical phenomena of convective transport and acoustic wave propagation. By moving beyond a monolithic treatment of the flux vector, the AUSM framework provides a physically intuitive and computationally powerful alternative. This article provides a comprehensive overview of the AUSM family, from its theoretical underpinnings to its practical implementation. In the following chapters, you will explore the **Principles and Mechanisms** that define the advection-pressure split and the construction of the numerical flux. You will then discover its broad utility through various **Applications and Interdisciplinary Connections**, from [aerospace engineering](@entry_id:268503) to [relativistic astrophysics](@entry_id:275429). Finally, a series of **Hands-On Practices** will solidify your understanding by guiding you through key calculations and conceptual problems.

## Principles and Mechanisms

The Advection Upstream Splitting Method (AUSM) family of schemes represents a significant development in the field of computational fluid dynamics for [hyperbolic conservation laws](@entry_id:147752). These schemes are founded on a physical-phenomenological approach that decomposes the [numerical flux](@entry_id:145174) into distinct components representing different physical transport mechanisms. This chapter elucidates the core principles and mechanisms that underpin the AUSM family, from its fundamental [advection-pressure splitting](@entry_id:1120840) to the sophisticated refinements that ensure its accuracy and robustness across a wide range of [flow regimes](@entry_id:152820).

### The Fundamental Principle: Advection-Pressure Splitting

The foundation of the AUSM family lies in the decomposition of the inviscid flux vector into two parts: a **convective** (or **advective**) part, which accounts for the transport of [fluid properties](@entry_id:200256) by the bulk motion of the flow, and a **pressure** part, which represents the effects of pressure forces. To understand this, let us consider the one-dimensional Euler equations, where the state vector of [conserved variables](@entry_id:747720) is $\boldsymbol{U} = [\rho, \rho u, \rho E]^T$ and the corresponding physical [flux vector](@entry_id:273577) is $\boldsymbol{F}(\boldsymbol{U}) = [\rho u, \rho u^2+p, u(\rho E+p)]^T$.

The AUSM splitting aims to isolate terms that scale with the convective velocity $u$ from those that do not. A key insight is to express the energy flux using the total [specific enthalpy](@entry_id:140496), $H = E + p/\rho$. The total energy flux, $u(\rho E+p)$, can be rewritten as $u(\rho E + \rho(p/\rho)) = u\rho(E+p/\rho) = u\rho H$. With this substitution, the Euler [flux vector](@entry_id:273577) becomes $\boldsymbol{F}(\boldsymbol{U}) = [\rho u, \rho u^2+p, u\rho H]^T$.

This form lends itself naturally to the advection-pressure split. The advective flux, $\boldsymbol{F}^{adv}$, collects all terms representing the transport of quantities by the mass flux $\rho u$. The pressure flux, $\boldsymbol{F}^{press}$, isolates the pressure force term in the momentum equation. This decomposition is as follows :

$$
\boldsymbol{F}(\boldsymbol{U}) = \boldsymbol{F}^{adv}(\boldsymbol{U}) + \boldsymbol{F}^{press}(\boldsymbol{U}) = \underbrace{
\begin{pmatrix}
\rho u \\
\rho u^2 \\
\rho u H
\end{pmatrix}
}_{\text{Advective Flux}} +
\underbrace{
\begin{pmatrix}
0 \\
p \\
0
\end{pmatrix}
}_{\text{Pressure Flux}}
$$

This can be expressed more suggestively as:

$$
\boldsymbol{F}(\boldsymbol{U}) = u \begin{pmatrix} \rho \\ \rho u \\ \rho H \end{pmatrix} + \begin{pmatrix} 0 \\ p \\ 0 \end{pmatrix}
$$

This decomposition is physically appealing. The advective part represents the transport of mass (per unit volume, $\rho$), momentum (per unit volume, $\rho u$), and total enthalpy (per unit mass, $H$) by the flow velocity $u$. The pressure part represents the force exerted by pressure, which acts solely on the momentum equation. In multiple dimensions, this principle is extended: the pressure force $p\boldsymbol{n}$ acts only in the direction normal to a control surface, while tangential momentum is passively advected with the mass flux . Specifically, the advective flux of momentum $\dot{m}\boldsymbol{u}$ can be decomposed into a normal component $\dot{m} u_n \boldsymbol{n}$ and a tangential component $\dot{m} \boldsymbol{u}_t$. The pressure flux $p\boldsymbol{n}$ has no tangential component.

### Physical Motivation from Characteristic Theory

While the advection-pressure split is intuitive, its profound justification comes from the characteristic theory of [hyperbolic systems](@entry_id:260647). The Euler equations propagate information through waves, and the speeds and properties of these waves are given by the [eigenvalues and eigenvectors](@entry_id:138808) of the flux Jacobian matrix, $\boldsymbol{A} = \partial \boldsymbol{F}/\partial \boldsymbol{U}$. For the one-dimensional Euler equations, the eigenvalues are:

$$
\lambda_1 = u - a, \quad \lambda_2 = u, \quad \lambda_3 = u + a
$$

where $a$ is the local speed of sound. These eigenvalues represent the speeds of three distinct types of waves that carry information through the fluid  :

1.  **The Convective Wave ($\lambda = u$):** This wave travels at the local fluid velocity $u$. Analysis of the corresponding eigenvector shows that it carries disturbances in entropy and, in multiple dimensions, shear (tangential velocity). Across a pure convective wave (a [contact discontinuity](@entry_id:194702)), pressure and normal velocity are continuous, while density and temperature can jump. This wave represents the [passive transport](@entry_id:143999) of fluid properties and identities.

2.  **The Acoustic Waves ($\lambda = u \pm a$):** These two waves travel at the speed of sound relative to the fluid, one moving upstream ($u-a$) and one downstream ($u+a$). They are responsible for propagating disturbances in pressure and normal velocity. These waves represent the mechanism by which pressure signals are transmitted through the fluid.

The AUSM philosophy is to design a numerical scheme that respects this physical dichotomy. The advective part of the flux is designed to model the physics of the convective wave, while the pressure part models the physics of the acoustic waves . This separation allows for the application of different, more appropriate numerical treatments to each part, leading to improved accuracy and robustness compared to schemes that treat the [flux vector](@entry_id:273577) as a monolithic entity.

### Construction of the AUSM Numerical Flux

In a [finite volume method](@entry_id:141374), the goal is to define a [numerical flux](@entry_id:145174), $\boldsymbol{F}_{1/2}$, at the interface between two cells with reconstructed states $\boldsymbol{U}_L$ and $\boldsymbol{U}_R$. Following the [splitting principle](@entry_id:158035), the AUSM [numerical flux](@entry_id:145174) is constructed as the sum of a [numerical advection](@entry_id:1128962) flux and a numerical pressure flux:

$$
\boldsymbol{F}_{1/2} = \boldsymbol{F}^{adv}_{1/2} + \boldsymbol{F}^{press}_{1/2}
$$

The construction of these two numerical components is guided by upwinding principles derived from the characteristic wave structure.

#### The Advective Flux

The advective flux is defined as the product of a numerical mass flux across the interface, $\dot{m}_{1/2}$, and a vector of advected quantities, $\boldsymbol{\Psi}_{1/2}$.

$$
\boldsymbol{F}^{adv}_{1/2} = \dot{m}_{1/2} \boldsymbol{\Psi}_{1/2}
$$

The vector $\boldsymbol{\Psi}$ contains the quantities transported by convection, typically defined as $\boldsymbol{\Psi} = [1, u_n, \boldsymbol{u}_t, H]^T$ in a face-normal coordinate system, where $u_n$ is the normal velocity and $\boldsymbol{u}_t$ is the tangential velocity vector. The [upwinding](@entry_id:756372) decision for $\boldsymbol{\Psi}$ is based on the direction of the mass flux. If $\dot{m}_{1/2} > 0$, the flow is from left to right, and $\boldsymbol{\Psi}_{1/2}$ should be based on the left state $\boldsymbol{\Psi}_L$. If $\dot{m}_{1/2}  0$, it should be based on the right state $\boldsymbol{\Psi}_R$.

The numerical mass flux $\dot{m}_{1/2}$ itself must be constructed from the left and right states. This is achieved through **Mach number splitting**. The face-normal Mach numbers for the left and right states are defined as $M_L = u_{n,L}/a_{1/2}$ and $M_R = u_{n,R}/a_{1/2}$, where $a_{1/2}$ is a suitable interface speed of sound . The Mach number is then split into positive- and negative-going parts using smooth [splitting functions](@entry_id:161308), $M^+(M)$ and $M^-(M)$, which satisfy $M = M^+(M) + M^-(M)$. For example, in supersonic flow ($|M| \ge 1$), these reduce to the simple velocity splitting $M^+ = \frac{1}{2}(M+|M|)$ and $M^- = \frac{1}{2}(M-|M|)$. The numerical mass flux is then constructed as a weighted sum:

$$
\dot{m}_{1/2} = a_{1/2} \left( M^+_L \rho_L + M^-_R \rho_R \right)
$$

where $M^+_L = M^+(M_L)$ and $M^-_R = M^-(M_R)$. This formulation provides a smooth, upwind-biased mass flux that correctly defaults to the upwind state in [supersonic flow](@entry_id:262511). Some advanced schemes may use a more complex construction for the full advective [flux vector](@entry_id:273577) rather than factoring out a single $\dot{m}_{1/2}$ , but the principle of Mach number-based upwinding remains central.

#### The Pressure Flux

The numerical pressure flux is given by $\boldsymbol{F}^{press}_{1/2} = [0, p_{1/2}\boldsymbol{n}, 0]^T$, where $\boldsymbol{n}$ is the [face normal vector](@entry_id:749211). The critical component is the numerical interface pressure, $p_{1/2}$. Naively upwinding the pressure based on the sign of the flow velocity $u_n$ is physically incorrect for subsonic flow. In subsonic flow ($|M_n|  1$), the acoustic eigenvalues $u_n-a$ and $u_n+a$ have opposite signs, meaning pressure information propagates to the interface from *both* the left and right sides.

To model this correctly, the AUSM family constructs the interface pressure using a separate set of Mach number-based [splitting functions](@entry_id:161308), $P^+(M)$ and $P^-(M)$:

$$
p_{1/2} = P^+_L p_L + P^-_R p_R
$$

These functions are designed to satisfy several constraints . In supersonic flow ($|M_n| \ge 1$), where all characteristics propagate from one direction, they must recover pure upwinding (e.g., $P_L^+=1, P_R^-=0$ for $M_n \ge 1$). In subsonic flow, they provide a smooth blend of $p_L$ and $p_R$ that models the bidirectional propagation of [acoustic waves](@entry_id:174227).

### Advanced Design Considerations and Refinements

The specific forms of the [splitting functions](@entry_id:161308) $M^\pm$ and $P^\pm$ are not arbitrary. They are carefully engineered to address several well-known challenges in numerical methods for compressible flows, ensuring the scheme is not only accurate but also robust.

#### The Sonic Point Problem and the Entropy Condition

A notorious failure of simpler [upwind schemes](@entry_id:756378), such as the Steger-Warming [flux vector splitting](@entry_id:749491), is the production of non-physical **expansion shocks** at sonic points. This occurs because a naive splitting based on the sign of the eigenvalues leads to zero numerical dissipation precisely where an eigenvalue crosses zero (e.g., at $\lambda=u-a=0$). This lack of dissipation allows the scheme to converge to a solution that violates the [second law of thermodynamics](@entry_id:142732) .

The AUSM family, along with schemes like van Leer's, resolves this by using smooth, continuously differentiable polynomial or [rational functions](@entry_id:154279) for the splitting. These functions ensure that the numerical dissipation does not vanish abruptly at sonic points, effectively acting as an **[entropy fix](@entry_id:749021)**. This guarantees that [rarefaction waves](@entry_id:168428) are resolved as smooth fans rather than collapsing into unphysical shocks.

#### Low-Mach Number Consistency

As the Mach number $M$ approaches zero, the compressible Euler equations should asymptotically recover the incompressible Euler equations. However, the pressure gradient term in the nondimensional momentum equation is scaled by $1/M^2$, making the system numerically stiff in this limit. Asymptotic analysis reveals that for a smooth flow, pressure fluctuations must scale as $O(M^2)$ .

A numerical scheme that is not designed with this limit in mind can introduce spurious pressure oscillations that are much larger, e.g., $O(M)$ or $O(1)$. When these errors are multiplied by the $1/M^2$ factor in the discretized momentum equation, they generate catastrophic, unphysical forces that destroy the solution. To be **low-Mach consistent**, a scheme's inherent numerical dissipation for the pressure field must be scaled appropriately. Specifically, the coefficient of any artificial pressure diffusion term must vanish at least as fast as $O(M)$ as $M \to 0$. The pressure [splitting functions](@entry_id:161308) $P^\pm$ in modern AUSM variants are carefully designed to satisfy this condition, often reducing to a nearly centered average for pressure at very low speeds, which correctly reflects the elliptic nature of pressure in incompressible flow.

#### Multi-Dimensional Stability: Carbuncle and Odd-Even Decoupling

In multiple dimensions, certain "exactly" [upwind schemes](@entry_id:756378) like Roe's approximate Riemann solver can suffer from debilitating instabilities such as the **[carbuncle phenomenon](@entry_id:747140)**, where a strong, grid-aligned [normal shock](@entry_id:271582) develops spurious, unphysical protrusions . This instability is caused by the vanishing of numerical dissipation for shear waves, which are decoupled from the acoustic field in Roe's characteristic-based model. At a stationary shock, the flow velocity $u$ is nearly zero, and since shear wave dissipation is proportional to $|u|$, it vanishes, leaving transverse perturbations undamped.

A related issue is **odd-even decoupling** or [checkerboarding](@entry_id:747311), where spurious oscillations in the pressure field can persist in the transverse direction to a stationary shock . Modern AUSM schemes, such as AUSM$^+$-up, demonstrate superior robustness against these instabilities. They achieve this by introducing a controlled amount of pressure-based dissipation that is scaled by the local speed of sound, $a$. For a strong shock, while the post-shock velocity $u$ is small, the temperature and pressure are high, so the speed of sound $a$ remains large. This pressure-based dissipation, active in subsonic regions, provides a robust coupling mechanism between adjacent cells that effectively [damps](@entry_id:143944) the unstable [transverse modes](@entry_id:163265), preventing both [carbuncle](@entry_id:894495) formation and odd-even decoupling. This highlights how the careful design of the pressure flux is critical not only for accuracy but for the fundamental stability of the numerical method in multiple dimensions.