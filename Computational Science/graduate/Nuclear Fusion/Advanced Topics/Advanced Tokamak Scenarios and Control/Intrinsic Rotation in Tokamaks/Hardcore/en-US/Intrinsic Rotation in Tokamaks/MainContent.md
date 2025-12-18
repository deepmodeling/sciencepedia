## Introduction
The spontaneous, self-generated spinning of plasma in a [tokamak](@entry_id:160432), known as intrinsic rotation, represents a fascinating example of [self-organization](@entry_id:186805) in a complex system. This phenomenon, where the plasma rotates without any external momentum input, is not just a scientific curiosity but a critical factor influencing the stability and performance of fusion devices. The central challenge lies in understanding how this rotation originates from the intricate interplay of turbulence and magnetic geometry, and developing predictive models for its behavior. This article provides a comprehensive overview of intrinsic rotation, guiding the reader from fundamental principles to practical applications. The **Principles and Mechanisms** chapter lays the theoretical foundation, examining macroscopic momentum balance and the microscopic kinetic theory to reveal how breaking fundamental symmetries in turbulence generates the "residual stress" that drives the flow. The **Applications and Interdisciplinary Connections** chapter explores the profound impact of this rotation on MHD stability, its link to energy confinement, and its measurement. Finally, the **Hands-On Practices** chapter offers a chance to apply these concepts through guided problems, connecting abstract theory to concrete calculations. We begin by exploring the core principles that govern this remarkable phenomenon.

## Principles and Mechanisms

The phenomenon of intrinsic rotation, where a [tokamak](@entry_id:160432) plasma spontaneously spins without external momentum input, is a direct manifestation of the complex interplay between [plasma turbulence](@entry_id:186467) and the magnetic geometry in which it resides. Understanding the principles governing this self-organization requires a multi-scale approach, connecting macroscopic [transport equations](@entry_id:756133) to the microscopic symmetries of the underlying kinetic theory. This chapter elucidates these principles, beginning with the macroscopic framework of [momentum transport](@entry_id:139628) and culminating in the symmetry-breaking mechanisms that generate intrinsic rotation at the kinetic level.

### The Macroscopic Framework: Toroidal Momentum Balance

The starting point for any transport analysis is a conservation law. For toroidal rotation, we consider the conservation of toroidal angular momentum. In a steady-state, axisymmetric [tokamak](@entry_id:160432), the net local torque density must be zero. This balance involves the divergence of the radial flux of toroidal angular momentum and the sum of all volumetric torque [sources and sinks](@entry_id:263105). After averaging over a [magnetic flux surface](@entry_id:751622), this principle is expressed through the **toroidal torque balance equation** .

Let $\Pi_{\psi\varphi}$ be the flux-surface-averaged radial flux of toroidal angular momentum, where $\psi$ is the poloidal magnetic flux (a [radial coordinate](@entry_id:165186)) and $\varphi$ is the toroidal angle. Let $\tau_k$ represent the various volumetric torque densities. The steady-state balance equation is:

$$
\frac{1}{V'} \frac{\partial}{\partial\psi} \left( V' \langle \Pi_{\psi\varphi} \rangle \right) = \langle \sum_k \tau_k \rangle
$$

where $V'$ is the differential volume of a flux shell, and $\langle \cdot \rangle$ denotes a flux-surface average. The left-hand side represents the divergence of the [momentum flux](@entry_id:199796), which acts as a torque source or sink due to momentum redistribution. The right-hand side represents direct, local sources and sinks of momentum.

The [momentum flux](@entry_id:199796) $\Pi_{\psi\varphi}$ and the torque sources $\tau_k$ arise from distinct physical processes. It is crucial to properly categorize these processes. The total momentum flux itself is a combination of several turbulent and collisional transport channels . We can decompose it as:

$$
\Pi_{\psi\varphi} = \Pi_{\psi\varphi}^{(\mathrm{d})} + \Pi_{\psi\varphi}^{(\mathrm{p})} + \Pi_{\psi\varphi}^{(\mathrm{res})}
$$

Here, the components are:

*   **Diffusive Flux ($\Pi_{\psi\varphi}^{(\mathrm{d})}$):** This is the viscous part of the transport, driven by the gradient of the toroidal rotation. Following Fick's law, it acts to flatten the rotation profile and is modeled as $\Pi_{\psi\varphi}^{(\mathrm{d})} = - m_i n_i \chi_\phi \frac{\partial V_\phi}{\partial r}$, where $m_i$ and $n_i$ are the ion mass and density, $V_\phi$ is the toroidal velocity, and $\chi_\phi$ is the **toroidal [momentum diffusivity](@entry_id:275614)**. This term represents the irreversible transport of momentum down its gradient.

*   **Convective Flux or "Pinch" ($\Pi_{\psi\varphi}^{(\mathrm{p})}$):** This is a flux proportional to the [momentum density](@entry_id:271360) itself, rather than its gradient, often modeled as $\Pi_{\psi\varphi}^{(\mathrm{p})} = m_i n_i V_{\text{pinch}} V_\phi$. A pinch can transport momentum "uphill" against a gradient, leading to peaked profiles.

*   **Residual Stress ($\Pi_{\psi\varphi}^{(\mathrm{res})}$):** This is the most critical component for intrinsic rotation. It is a non-diffusive, non-convective turbulent momentum flux that can exist even when both the toroidal velocity and its gradient are zero. This "stress" arises from broken symmetries in the underlying turbulence, as we will explore in detail.

The torque sources on the right-hand side of the balance equation typically include:
*   **External Torque ($\tau_{\mathrm{NBI}}$):** From sources like Neutral Beam Injection (NBI).
*   **Neoclassical Toroidal Viscosity ($\tau_{\mathrm{NTV}}$):** A braking torque from plasma interaction with non-axisymmetric magnetic fields (e.g., error fields or ripple).
*   **Edge Torques ($\tau_{\mathrm{edge}}$):** Momentum loss at the plasma boundary due to interactions with neutral particles and material surfaces.

The [residual stress](@entry_id:138788) $\Pi_{\psi\varphi}^{(\mathrm{res})}$ is a flux, but its divergence acts as an effective torque source. It is standard practice to move this term to the right-hand side of the balance equation by defining the **intrinsic torque density** as its negative divergence :

$$
\tau_{\mathrm{int}} \equiv -\frac{1}{V'} \frac{\partial}{\partial\psi} \left( V' \langle \Pi_{\psi\varphi}^{(\mathrm{res})} \rangle \right)
$$

With this definition, the steady-state momentum balance equation takes its conventional form, separating diffusive/[convective transport](@entry_id:149512) from the various torque sources:

$$
\frac{1}{V'}\frac{\partial}{\partial \psi}\left(V'\langle \Pi_{\psi\varphi}^{(\mathrm{d})} + \Pi_{\psi\varphi}^{(\mathrm{p})} \rangle\right) = \langle \tau_{\mathrm{NBI}} + \tau_{\mathrm{int}} + \tau_{\mathrm{NTV}} + \tau_{\mathrm{edge}} \rangle
$$

In a plasma with no external torque ($\tau_{\mathrm{NBI}}=0$) and negligible NTV and [edge effects](@entry_id:183162), the equation simplifies. A steady-state rotation profile can only be maintained if the intrinsic torque, $\tau_{\mathrm{int}}$, drives a rotation profile whose gradient is then balanced by the [diffusive flux](@entry_id:748422). This is the essence of intrinsic rotation.

To connect these abstract coefficients to measurable plasma properties, we define the **[momentum confinement time](@entry_id:752134), $\tau_\phi$**. This global parameter quantifies how effectively the plasma confines angular momentum. One definition arises from considering the total stored angular momentum $L_\phi = \int \ell dV$ and the total power input $P_\phi = \int S_\phi dV$ in a driven steady state, giving $\tau_\phi = L_\phi / P_\phi$. In a simplified cylindrical model with a uniform torque source, this leads to a direct relationship with the [momentum diffusivity](@entry_id:275614): $\tau_\phi = a^2/(8\chi_\phi)$, where $a$ is the minor radius . An alternative definition considers the decay time of a rotation profile after the source is turned off, yielding a similar scaling, $\tau_\phi \propto a^2/\chi_\phi$. These relations highlight that a smaller diffusivity implies better momentum confinement.

Finally, we can compare [momentum transport](@entry_id:139628) to the well-studied topic of heat transport by defining the **turbulent Prandtl number**, $\mathrm{Pr} = \chi_\phi / \chi_i$, where $\chi_i$ is the ion thermal diffusivity . This dimensionless ratio quantifies the [relative efficiency](@entry_id:165851) of [turbulent mixing](@entry_id:202591) of momentum versus heat. For turbulence driven by the Ion Temperature Gradient (ITG) mode, theoretical and computational studies find that $\mathrm{Pr}$ is typically of order unity, often in the range of $0.3$ to $0.7$. This indicates that the same turbulent eddies responsible for anomalous [heat loss](@entry_id:165814) are also comparably effective at transporting momentum.

### The Microscopic Origin: Turbulence and Symmetry

The existence of a non-zero residual stress, $\Pi_\phi^{\mathrm{res}}$, is the central mystery of intrinsic rotation. Standard [transport theory](@entry_id:143989), based on simple Fickian diffusion, would predict $\Pi_\phi^{\mathrm{res}}=0$. The origin of this stress lies in the kinetic nature of [plasma turbulence](@entry_id:186467) and, most profoundly, in the breaking of [fundamental symmetries](@entry_id:161256).

The residual stress is a manifestation of the turbulent **Reynolds stress**, specifically the correlation between fluctuating [radial velocity](@entry_id:159824), $\tilde{v}_r$, and fluctuating parallel velocity, $\tilde{v}_\parallel$. The radial flux of toroidal momentum is dominated by the radial flux of parallel momentum:

$$
\Pi_\phi^{\mathrm{res}} \propto \langle \tilde{v}_r \tilde{v}_\parallel \rangle
$$

where the average is over turbulent fluctuations. The [radial velocity](@entry_id:159824) is primarily the fluctuating $\boldsymbol{E}\times\boldsymbol{B}$ drift, $\tilde{v}_r \propto -\partial_\theta \tilde{\phi}$, where $\tilde{\phi}$ is the fluctuating electrostatic potential. The question thus becomes: under what conditions can a net correlation between $\tilde{v}_r$ and $\tilde{v}_\parallel$ develop?

The answer begins with a powerful [null result](@entry_id:264915). In an idealized [tokamak](@entry_id:160432)—one that is perfectly axisymmetric and **up-down symmetric**, and described by a **local** kinetic model (the flux-tube approximation)—the residual stress is exactly zero  . This arises because the governing **gyrokinetic equations** possess a fundamental [parity symmetry](@entry_id:153290) .

In this idealized system, the [equations of motion](@entry_id:170720) are invariant under a combined transformation that simultaneously flips the sign of the poloidal angle relative to the midplane ($\theta \to -\theta$), the parallel velocity ($v_\parallel \to -v_\parallel$), and the radial [wavenumber](@entry_id:172452) ($k_r \to -k_r$). Any statistically stationary turbulent state must also respect this symmetry. A consequence of this symmetry is that the local [momentum flux](@entry_id:199796) generated at a poloidal angle $\theta$ is exactly cancelled by the flux generated at $-\theta$. Averaged over the entire flux surface, the net flux vanishes.

This can be stated more formally: the symmetry of the governing equations forces the momentum flux contribution from a turbulent mode with radial wavenumber $k_r$ to be exactly opposite to that of a mode with $-k_r$. Summing over all modes results in a perfect cancellation: $\Pi_\phi^{\mathrm{res}}=0$.

This [null result](@entry_id:264915) is profound. It demonstrates that **intrinsic rotation is fundamentally a symmetry-breaking phenomenon**. The highly symmetric, local models that are often sufficient for calculating heat transport completely fail to capture intrinsic rotation. To generate a finite [residual stress](@entry_id:138788), some physical mechanism must break this underlying [parity symmetry](@entry_id:153290).

### Mechanisms for Symmetry Breaking

Real tokamaks are never perfectly symmetric. Several mechanisms, absent in the idealized model, act to break the [parity symmetry](@entry_id:153290) and generate a finite [residual stress](@entry_id:138788).

1.  **Profile Gradients and Intensity Gradients:** The local flux-[tube model](@entry_id:140303) assumes that background plasma profiles (of temperature, density, etc.) are uniform. In reality, these profiles have curvature. A turbulent eddy with a finite radial width will therefore experience a different environment on its inner side compared to its outer side. For instance, the turbulence drive (e.g., from the temperature gradient) or its suppression (e.g., from $\boldsymbol{E}\times\boldsymbol{B}$ shear) may vary across the radial extent of the eddy. This radial variation in the turbulence "background" breaks the symmetry between positive and negative radial positions relative to the eddy center. Due to the coupling between radial position and parallel [wavenumber](@entry_id:172452) ($k_\parallel$) via magnetic shear, this spatial asymmetry translates into a spectral asymmetry in the turbulence, i.e., the fluctuation intensity $I(k_\parallel)$ is no longer equal to $I(-k_\parallel)$. This allows the integral for the Reynolds stress to be non-zero . This mechanism, often termed the **intensity gradient mechanism** or **profile shearing residual stress**, is a direct consequence of relaxing the "local" assumption.

2.  **Finite Orbit Width (FOW) Effects:** The profile gradient mechanism is intrinsically linked to FOW effects. It is because ions have finite Larmor radii ($\rho_i$) that they "sample" the radial variation of profiles. Global simulations, which retain the full radial dependence of profiles and work with a finite normalized [gyroradius](@entry_id:261534) $\rho_* = \rho_i/a$, naturally include this symmetry-breaking channel . The resulting residual stress often scales with $\rho_*$, highlighting its "global" or non-local nature .

3.  **Up-Down Geometric Asymmetry:** Real tokamaks often have a magnetic geometry that is not perfectly symmetric about the equatorial midplane, for instance in single-null [divertor](@entry_id:748611) configurations. This geometric asymmetry directly breaks the $\theta \to -\theta$ part of the fundamental [parity symmetry](@entry_id:153290). The magnetic drift frequencies and other geometric coefficients in the gyrokinetic equation no longer possess a definite parity. This provides a robust, "zeroth-order" mechanism for generating residual stress, which scales with the degree of geometric asymmetry  .

These mechanisms illustrate that intrinsic rotation is not an exotic phenomenon but an inevitable consequence of turbulence existing in the complex, spatially non-uniform, and imperfectly symmetric environment of a real [tokamak](@entry_id:160432).

### Predicting the Direction of Rotation: ITG vs. TEM Turbulence

The theory of [symmetry breaking](@entry_id:143062) not only explains the existence of intrinsic rotation but can also predict its direction (co-current or counter-current). The direction of the [momentum flux](@entry_id:199796) depends on the detailed phase relationships between the turbulent fluctuations, which are determined by the nature of the dominant instability.

Two of the most common micro-instabilities in [tokamak](@entry_id:160432) cores are the Ion Temperature Gradient (ITG) mode and the Trapped Electron Mode (TEM). These modes have distinct characteristics that lead to oppositely signed residual stresses :

*   **ITG-driven Turbulence:** These modes are driven by a steep [ion temperature](@entry_id:191275) gradient. They propagate in the **ion diamagnetic direction**. In a typical scenario with a radially decreasing turbulence intensity, the symmetry breaking mechanisms discussed above lead to a net **inward flux of co-current momentum** ($\Pi_\phi^{\mathrm{res}}  0$). This inward flux accumulates momentum in the plasma core, driving a **co-current** intrinsic rotation.

*   **TEM-driven Turbulence:** These modes are driven by the gradient of the trapped electron population. They propagate in the **electron diamagnetic direction**. The change in the resonant particle population (from passing ions in ITG to trapped electrons in TEM) fundamentally alters the kinetic response and the resulting [phase shifts](@entry_id:136717) within the turbulent eddies. This "reverses" the direction of the eddy tilt, leading to a net **outward flux of co-current momentum** ($\Pi_\phi^{\mathrm{res}} > 0$). This outward flux depletes momentum from the core, driving a **counter-current** intrinsic rotation.

This remarkable result provides a direct link between the underlying turbulent state and the observed macroscopic rotation. It explains experimental observations where the direction of core rotation can flip from co- to counter-current when plasma conditions are changed in a way that shifts the dominant turbulence from ITG to TEM. This predictive power is a major triumph of the [gyrokinetic theory](@entry_id:186998) of intrinsic rotation.