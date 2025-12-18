## Introduction
In the field of [computational electrochemistry](@entry_id:747611), the development of predictive and efficient battery models is paramount for advancing energy storage technology. The Single-Particle Model (SPM) stands as a cornerstone in this endeavor, striking a powerful balance between physical fidelity and [computational tractability](@entry_id:1122814). It addresses the critical need for models that are simple enough for real-time control and diagnostics yet are fundamentally rooted in the underlying electrochemical principles, a gap often left by purely empirical or overly complex models. By idealizing a porous electrode as an ensemble of [identical particles](@entry_id:153194), the SPM provides deep insights into battery behavior without the prohibitive computational cost of full-scale porous electrode models.

This article offers a graduate-level exploration of the Single-Particle Model across three comprehensive chapters. First, in **"Principles and Mechanisms,"** we will deconstruct the model's core tenets, rigorously justifying its assumptions through scaling analysis and deriving the governing equations for [solid-state diffusion](@entry_id:161559) and [interfacial kinetics](@entry_id:1126605). Next, **"Applications and Interdisciplinary Connections"** will demonstrate the model's practical utility in simulation, experimental [parameter identification](@entry_id:275485), multi-physics coupling for aging and safety analysis, and its ultimate role as a digital twin within advanced Battery Management Systems. Finally, **"Hands-On Practices"** will present targeted problems to bridge theory with practical implementation, focusing on [numerical stability](@entry_id:146550), mass conservation, and control-theoretic analysis. We begin by laying the theoretical groundwork, exploring the foundational physics and mathematical structure that make the SPM such a versatile tool.

## Principles and Mechanisms

The Single-Particle Model (SPM) serves as a foundational framework in [computational electrochemistry](@entry_id:747611), offering a potent balance between physical fidelity and [computational tractability](@entry_id:1122814). It achieves its efficiency by simplifying the complex, multi-scale architecture of a porous electrode into a more manageable, idealized system. This chapter delineates the core principles, governing equations, and underlying mechanisms of the SPM, providing a rigorous basis for its application and interpretation. We begin by examining the model's foundational assumptions and their domain of validity before deconstructing the physics of the constituent particle and, finally, assembling the components into a complete cell model.

### The Single-Particle Model: Core Tenets and Justification

The central idealization of the SPM is the representation of an entire porous electrode—comprising a vast number of active material grains embedded in a conductive matrix and permeated by electrolyte—as an ensemble of identical, non-interacting spherical particles. It is further assumed that the electrochemical reaction occurs uniformly over the surface of these representative particles. The most consequential assumption, however, is the **neglect of transport limitations in the electrolyte phase**. This implies that the electrolyte concentration, $c_e$, and the electrolyte potential, $\phi_e$, are spatially uniform throughout the thickness of the porous electrode.

The validity of this uniform-electrolyte approximation hinges on the [separation of timescales](@entry_id:191220) and the magnitude of transport-induced polarization relative to other potential scales in the system. For the SPM to be a reasonable approximation, any spatial variations in electrolyte concentration and potential must be negligible. We can rigorously assess this using [scaling arguments](@entry_id:273307) derived from fundamental transport laws.

#### Justification: Electrolyte Concentration Gradients

During operation, ion consumption and production at the particle surfaces create concentration gradients in the electrolyte. Porous electrode theory shows that the maximum concentration difference, $\Delta c_e$, across an electrode of thickness $L$ subject to an areal current density $I_{app}$ scales as:
$$
\Delta c_e \propto \frac{I_{app} L (1-t_+^0)}{F D_e^{\mathrm{eff}}}
$$
where $t_+^0$ is the cation transference number, $F$ is Faraday's constant, and $D_e^{\mathrm{eff}}$ is the effective electrolyte diffusivity. A dimensionless parameter, $\Pi_c$, can be defined to quantify the magnitude of this [concentration polarization](@entry_id:266906) relative to the bulk concentration $c_{e,0}$ :
$$
\Pi_c = \frac{I_{app} L (1-t_+^0)}{F c_{e,0} D_e^{\mathrm{eff}}}
$$
The SPM assumption of uniform electrolyte concentration is justified when $\Pi_c \ll 1$. For a typical positive electrode ($L=70\,\mu\mathrm{m}$, $D_e^{\mathrm{eff}}=8\times 10^{-11}\,\mathrm{m^2/s}$), this condition may hold at a moderate rate like $0.5\text{C}$ (where $\Pi_c \approx 0.08$) but begin to fail at higher rates like $1\text{C}$ (where $\Pi_c \approx 0.16$), where a $16\%$ concentration variation is no longer negligible.

#### Justification: Electrolyte Potential Gradients

The electrolyte potential $\phi_e(x)$ varies across the electrode due to two primary effects: ohmic resistance to ion flow and concentration gradients (diffusion potential). The generalized Ohm's law in the electrolyte phase captures both:
$$
i_e(x) = -\kappa_e^{\mathrm{eff}} \frac{d\phi_e}{dx} - \frac{\kappa_e^{\mathrm{eff}} 2RT(1-t_+^0)}{F} \frac{d\ln c_e}{dx}
$$
Integrating this across the electrode thickness $L$ gives the total potential drop $\Delta\phi_e$. The approximation of uniform $\phi_e$ is valid if this drop is small compared to a characteristic potential scale of the reaction, such as a [kinetic overpotential](@entry_id:1126930) scale $\eta_k$. This requires two conditions to be met simultaneously :
1.  The ohmic drop must be small: $| \Delta\phi_{e,\text{ohm}} | \sim \frac{I_{app}L}{\kappa_e^{\mathrm{eff}}} \ll \eta_k$.
2.  The concentration-induced potential drop must be small: $| \Delta\phi_{e,\text{conc}} | \sim \frac{2RT(1-t_+^0)}{F} |\Delta\ln c_e| \ll \eta_k$.

For a typical electrode, the [ohmic drop](@entry_id:272464) is often in the order of a few millivolts, which is indeed negligible compared to typical reaction overpotentials (tens to hundreds of millivolts). The concentration-induced drop's relevance is tied to the magnitude of the concentration gradient, reinforcing the primary importance of maintaining $\Pi_c \ll 1$.

#### Justification: Timescale Analysis

An alternative perspective is gained by comparing the [characteristic timescales](@entry_id:1122280) of the different transport processes occurring in the cell . The three key timescales are:
1.  **Electrolyte Diffusion Time ($t_e$)**: The time required for ions to diffuse across the electrode thickness, $t_e = L^2/D_e^{\mathrm{eff}}$.
2.  **Solid Diffusion Time ($t_s$)**: The time required for lithium to diffuse across the particle radius, $t_s = R_p^2/D_s$, where $R_p$ is the particle radius and $D_s$ is the solid-state diffusivity.
3.  **Discharge Time ($t_{dis}$)**: The total time for the discharge process, which is inversely proportional to the C-rate (e.g., $3600\,\mathrm{s}$ at $1\text{C}$).

The uniform-electrolyte assumption holds if the electrolyte phase equilibrates much faster than the other processes. That is, the condition is $t_e \ll t_s$ and $t_e \ll t_{dis}$. For typical Li-ion battery parameters ($L=70\,\mu\mathrm{m}$, $R_p=5\,\mu\mathrm{m}$, $D_e^{\mathrm{eff}}\approx 5\times 10^{-11}\,\mathrm{m^2/s}$, $D_s\approx 1\times 10^{-14}\,\mathrm{m^2/s}$), we find $t_e \approx 100\,\mathrm{s}$ while $t_s \approx 2500\,\mathrm{s}$ and $t_{dis}$ is $1800-3600\,\mathrm{s}$ for $1-2\text{C}$ rates. The clear [separation of timescales](@entry_id:191220) ($t_e \ll t_s, t_{dis}$) provides a strong justification for the SPM's core assumption under these conditions. Conversely, for very thick electrodes or extremely [fast charging](@entry_id:1124848), $t_e$ may become comparable to $t_{dis}$, invalidating the SPM and requiring a more complex [porous electrode model](@entry_id:1129960).

It is crucial to note that while electrolyte diffusion is assumed to be fast, the same is not true for [solid-state diffusion](@entry_id:161559). The fact that $t_s$ is comparable to $t_{dis}$ implies that significant concentration gradients *will* develop within the active material particles, and a model that explicitly resolves this intra-particle diffusion is necessary. This is precisely what the SPM is designed to do.

### Physics of the Single Particle

With the electrode-scale assumptions established, the model's focus shifts to the physics occurring within and on the surface of a single, representative spherical particle.

#### Solid-State Diffusion

The evolution of the lithium concentration, $c_s(r, t)$, inside the spherical particle of radius $R_p$ is governed by Fick's second law of diffusion. For a spherically symmetric system with constant diffusivity $D_s$, this is expressed by the following partial differential equation (PDE) :
$$
\frac{\partial c_s}{\partial t} = D_s \nabla^2 c_s = D_s \frac{1}{r^2} \frac{\partial}{\partial r} \left( r^2 \frac{\partial c_s}{\partial r} \right)
$$
This equation describes how the concentration at any radial position $r$ changes over time due to the net influx or outflux of diffusing species. To solve this PDE, two boundary conditions are required:

1.  **Symmetry at the center ($r=0$)**: Due to the [spherical symmetry](@entry_id:272852) of the problem, the concentration profile must be flat at the origin, implying a zero-gradient (zero-flux) condition:
    $$
    \left. \frac{\partial c_s}{\partial r} \right|_{r=0} = 0
    $$

2.  **Flux at the surface ($r=R_p$)**: The diffusive flux of lithium at the particle surface must be equal to the [molar flux](@entry_id:156263) generated by the electrochemical reaction. The reaction rate is quantified by the local interfacial current density, $j$ (in A/m²). By Faraday's law, the [molar flux](@entry_id:156263) is $j/F$. Equating this to the outward Fickian flux, $-D_s (\partial c_s / \partial r)$, gives the surface boundary condition:
    $$
    -D_s \left. \frac{\partial c_s}{\partial r} \right|_{r=R_p} = \frac{j(t)}{F}
    $$
    The sign convention is critical: a positive current density $j>0$ (deintercalation or oxidation) corresponds to an outward flux, which requires a negative concentration gradient at the surface ($\partial c_s/\partial r  0$).

#### Thermodynamic Formalism: From Ideal Diffusion to Chemical Potential

The Fickian formulation presented above is, strictly speaking, a simplification. In concentrated systems, such as lithium intercalated in a host solid, the true thermodynamic driving force for diffusion is not the concentration gradient but the gradient of the **chemical potential**, $\mu_s(c_s)$. The [molar flux](@entry_id:156263), $j_r$, is more fundamentally expressed as:
$$
j_r = - \frac{D_s c_s}{RT} \frac{\partial \mu_s}{\partial r}
$$
where $D_s$ represents the tracer diffusivity, related to the random motion of individual atoms. By relating the chemical potential to concentration via the chain rule, $\partial \mu_s / \partial r = (\partial \mu_s / \partial c_s) (\partial c_s / \partial r)$, we can recover a Fickian-like form, $j_r = -D_{\text{chem}} (\partial c_s / \partial r)$, where the **[chemical diffusion coefficient](@entry_id:197568)**, $D_{\text{chem}}$, is defined as :
$$
D_{\text{chem}}(\theta) = \frac{D_s(\theta) c_s}{RT} \frac{\partial \mu_s}{\partial c_s} = D_s(\theta) \frac{\partial \ln a_s}{\partial \ln c_s}
$$
Here, $a_s$ is the activity of the intercalated species, and the term $\Gamma(\theta) = \partial \ln a_s / \partial \ln c_s$ is known as the **[thermodynamic factor](@entry_id:189257)**. This factor quantifies the deviation from ideal thermodynamic behavior. For an [ideal solution](@entry_id:147504), $a_s \propto c_s$, so $\Gamma=1$ and $D_{\text{chem}} = D_s$. However, for many real electrode materials, interactions between intercalated ions and vacant sites lead to $\Gamma \neq 1$. In such cases, using the tracer diffusivity $D_s$ in a simple Fickian model is an approximation; a more accurate model must use the [chemical diffusivity](@entry_id:1122331) $D_{\text{chem}}$ .

The chemical potential of the intercalated lithium, $\mu_s(\theta)$, is not just a theoretical construct; it is directly related to the measurable **Open-Circuit Potential (OCP)** of the electrode, $U(\theta)$. Under equilibrium conditions, the OCP measured against a lithium metal reference is given by :
$$
U(\theta) = -\frac{\mu_s(\theta)}{F} + \text{constant}
$$
This fundamental relationship allows us to probe the thermodynamics of the host material by measuring its OCP. For many materials, the OCP curve is not monotonic. This behavior is a hallmark of **phase separation**, where the material coexists in two distinct phases (e.g., a lithium-poor phase and a lithium-rich phase) over a range of average stoichiometries. This can be explained using thermodynamic models like the **regular solution model**. This model describes the Gibbs free energy of the host material, including an enthalpic [interaction parameter](@entry_id:195108), $\Omega$. Analysis shows that if repulsive interactions are strong enough ($\Omega > 2RT$), the chemical potential (and thus the OCP) becomes non-monotonic with respect to [stoichiometry](@entry_id:140916). The system then becomes unstable in the region where $dU/d\theta > 0$, leading to phase separation and a flat voltage plateau in the measured OCP curve .

#### Interfacial Charge-Transfer Kinetics

The electrochemical reaction at the solid-electrolyte interface is governed by charge-transfer kinetics, typically described by the **Butler-Volmer equation**. This equation relates the local current density, $j$, to the **surface overpotential**, $\eta_s$, which is the thermodynamic driving force for the reaction. For a one-electron reaction, the equation is :
$$
j = i_0 \left[ \exp\left(\frac{\alpha_a F \eta_s}{RT}\right) - \exp\left(-\frac{\alpha_c F \eta_s}{RT}\right) \right]
$$
Here, $\alpha_a$ and $\alpha_c$ are the anodic and cathodic transfer coefficients, which describe the symmetry of the activation energy barrier. The **exchange current density**, $i_0$, is a crucial parameter that sets the intrinsic rate of the reaction at equilibrium. It is not a constant but depends on the concentrations of the species involved in the reaction at the interface. For a typical intercalation reaction $\text{Li}^+ + e^- + \text{S} \rightleftharpoons \text{LiS}$ (where S is a vacant site), $i_0$ is a function of the electrolyte concentration $c_e$, the [surface concentration](@entry_id:265418) of vacant sites ($c_{s,\max} - c_{s,\text{surf}}$), and the surface concentration of occupied sites ($c_{s,\text{surf}}$):
$$
i_0 = k_0 F c_e^{\alpha_a} (c_{s,\max} - c_{s,\text{surf}})^{\alpha_a} c_{s,\text{surf}}^{\alpha_c}
$$
where $k_0$ is a rate constant.

The driving force, $\eta_s$, is defined as the deviation of the actual [interfacial potential](@entry_id:750736) difference, $\phi_s - \phi_e$, from its equilibrium value, which is the OCP, $U(\theta_s)$. The OCP must be evaluated at the **surface [stoichiometry](@entry_id:140916)**, $\theta_s$, because the reaction is an interfacial phenomenon. A rigorous derivation from the balance of electrochemical potentials at the interface confirms this definition :
$$
\eta_s = (\phi_s - \phi_e) - U(\theta_s(t))
$$
A positive overpotential ($\eta_s > 0$) drives the anodic (oxidation) reaction, while a negative overpotential ($\eta_s  0$) drives the cathodic (reduction) reaction.

### Assembling the Full Cell Model

The principles described above apply to a single particle. To model a full electrochemical cell, we combine two such models—one for the positive electrode (cathode) and one for the negative electrode (anode)—and couple them through [conservation of charge](@entry_id:264158).

#### State Variables and Their Roles

Within the SPM framework, it is essential to distinguish between two key state variables for each electrode :
-   The **volume-averaged stoichiometry**, $\bar{\theta}(t)$, represents the overall state of charge of the electrode. Its evolution is governed by integrating the total applied current, $I(t)$, over time, according to Faraday's law. It reflects the total amount of lithium stored in the electrode.
-   The **surface [stoichiometry](@entry_id:140916)**, $\theta_s(t)$, is the concentration of lithium at the particle-electrolyte interface. It is determined by solving the diffusion PDE within the particle, with the boundary condition set by the applied current. Because the electrochemical reaction is an interfacial process, $\theta_s(t)$ is the variable that directly determines the instantaneous thermodynamic potential ($U(\theta_s)$) and kinetic parameters ($i_0(\theta_s)$, $\eta_s$). The difference between $\bar{\theta}(t)$ and $\theta_s(t)$ is a measure of the [solid-phase diffusion](@entry_id:1131915) limitation.

#### Cell Voltage and Current Conservation

The terminal voltage of the cell, $V(t)$, is the potential difference between the positive and negative current collectors, $V(t) = \phi_{s,p}(t) - \phi_{s,n}(t)$. By rearranging the definition of overpotential for both the positive ($p$) and negative ($n$) electrodes and combining them, we arrive at the central voltage equation for the SPM :
$$
V(t) = \left[ U_p(\theta_{p,\text{surf}}) - U_n(\theta_{n,\text{surf}}) \right] + \left[ \eta_p(t) - \eta_n(t) \right]
$$
This equation elegantly decomposes the cell voltage into two parts:
1.  **Thermodynamic Potential**: $U_p(\theta_{p,\text{surf}}) - U_n(\theta_{n,\text{surf}})$, the difference in the open-circuit potentials of the two electrodes, evaluated at their respective surface concentrations. This represents the ideal, equilibrium voltage of the cell under the given surface conditions.
2.  **Overpotentials**: $\eta_p(t) - \eta_n(t)$, the difference in the kinetic overpotentials required to drive the reaction at the desired rate. During discharge, the negative electrode is the anode (oxidation), so $\eta_n > 0$. The positive electrode is the cathode (reduction), so $\eta_p  0$ . The total voltage loss from kinetics is therefore $|\eta_p| + \eta_n$.

The two electrodes are coupled by the principle of charge conservation. The total current $I(t)$ flowing through the external circuit must be equal to the total reaction current at each electrode. If $A_{s,p}$ and $A_{s,n}$ are the total electrochemically active surface areas of the positive and negative electrodes, respectively, then the coupling is given by :
$$
I(t) = A_{s,p} j_p(t) = -A_{s,n} j_n(t)
$$
The negative sign reflects that one electrode is undergoing oxidation while the other undergoes reduction; the net current flows in opposite directions relative to the solid phase at each electrode.

### Extensions: Thermo-Electrochemical Coupling

The isothermal SPM can be extended to account for thermal effects, which are critical for predicting battery performance and safety. The key link is the temperature dependence of the open-circuit potential. From the Gibbs-Helmholtz relation, the temperature coefficient of the OCP is directly proportional to the [entropy change](@entry_id:138294) of the reaction, $\Delta S$ :
$$
\left( \frac{\partial U}{\partial T} \right)_{\theta} = \frac{\Delta S(\theta)}{nF}
$$
This entropic coefficient, which can be positive or negative and varies with [stoichiometry](@entry_id:140916), has two major consequences in a non-isothermal model:

1.  **Direct Voltage Dependence**: The OCP, and therefore the [cell voltage](@entry_id:265649), becomes a direct function of temperature, $U(\theta, T)$. Changes in cell temperature will cause the voltage to drift, even at constant [stoichiometry](@entry_id:140916).
2.  **Reversible Heat Generation**: When current flows, in addition to irreversible resistive and kinetic heating, there is a reversible heat effect associated with the reaction entropy. The rate of this entropic heat generation is given by:
    $$
    \dot{q}_{\text{rev}}(t) = I(t) T(t) \left( \frac{\partial U}{\partial T} \right)_{\theta}
    $$
This term creates a powerful thermo-electrochemical feedback loop: current flow generates heat, which changes the cell temperature, which in turn alters the cell's [electrochemical potential](@entry_id:141179) and voltage. A comprehensive battery model must often account for this intricate coupling.