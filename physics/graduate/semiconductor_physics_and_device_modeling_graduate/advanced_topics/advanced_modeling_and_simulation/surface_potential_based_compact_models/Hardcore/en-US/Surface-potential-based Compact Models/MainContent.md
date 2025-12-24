## Introduction
Accurate and efficient compact models are the essential bridge between [semiconductor device physics](@entry_id:191639) and integrated circuit design. For decades, the development of these models has been crucial for predicting transistor behavior and enabling the simulation of complex circuits. Among the various modeling philosophies, the surface-potential-based approach stands out as a particularly powerful and physically insightful paradigm. It addresses the key limitation of older, threshold-voltage-based models: the need for separate, piecewise equations for different operating regimes, which often leads to inaccuracies and convergence issues in circuit simulators. By establishing a single, continuous description rooted in fundamental electrostatics, surface-potential models provide a more robust and scalable solution for modern semiconductor technologies.

This article provides a graduate-level exploration of surface-potential-based compact models. We will construct the model from the ground up, starting with core physical principles before moving to its diverse applications and hands-on implementation. The reader will gain a deep understanding of:

*   **Principles and Mechanisms:** How the model is derived from the fundamental electrostatics of the MOS capacitor, establishing the core relationship between external voltages, the internal surface potential, and device currents.
*   **Applications and Interdisciplinary Connections:** How this theoretical framework is applied to solve real-world engineering challenges, including [parameter extraction](@entry_id:1129331), dynamic and RF modeling, and its extension to advanced multi-gate devices like FinFETs.
*   **Hands-On Practices:** How to apply the core concepts to analyze experimental data and model state-of-the-art transistor architectures.

We begin our journey by dissecting the electrostatic heart of the transistor, laying the groundwork for the entire modeling framework.

## Principles and Mechanisms

The conceptual foundation of a surface-potential-based compact model rests on replacing the traditional, regime-dependent description of a MOSFET with a unified framework built around a single, continuous internal variable: the **surface potential**, $\psi_s$. This chapter elucidates the core principles and physical mechanisms that link this internal variable to the external terminal voltages and, subsequently, to the device's terminal currents and charges. We will construct the model from first principles, beginning with the fundamental electrostatics of the [metal-oxide-semiconductor](@entry_id:187381) (MOS) capacitor and systematically extending it to describe a non-ideal, four-terminal transistor.

### The Electrostatic Core: The MOS Capacitor

The behavior of a MOSFET is dominated by the electrostatics of the MOS structure oriented perpendicular to the channel. Understanding this one-dimensional MOS capacitor is therefore the essential first step.

#### Governing Equations and Boundary Conditions

Consider a one-dimensional MOS stack, with a semiconductor occupying the region $x \ge 0$, a gate oxide of thickness $t_{ox}$ in the region $0 \le x \le t_{ox}$, and a metal gate for $x \ge t_{ox}$. The electrostatic behavior of this system is governed by Maxwell's equations. Specifically, the relationship between the electrostatic potential, $\psi(x)$, and the local charge density, $\rho(x)$, is given by Poisson's equation. Assuming the material permittivities are piecewise constant—$\epsilon_{si}$ in the semiconductor and $\epsilon_{ox}$ in the oxide—we can write the governing equations for each region .

In the semiconductor ($x \ge 0$), where a space-charge region can form due to the presence of mobile carriers (electrons and holes) and ionized dopant atoms, the potential $\psi_{si}(x)$ must satisfy **Poisson's equation**:

$$
\frac{d^2\psi_{si}}{dx^2} = -\frac{\rho_{si}(x)}{\epsilon_{si}}
$$

In the oxide layer ($0 \le x \le t_{ox}$), we assume an ideal dielectric with no [free charge](@entry_id:264392), so $\rho_{ox}(x) = 0$. Poisson's equation simplifies to **Laplace's equation**:

$$
\frac{d^2\psi_{ox}}{dx^2} = 0
$$

This implies that the electric field in the oxide, $E_{ox} = -d\psi_{ox}/dx$, is constant. These two regions are coupled by boundary conditions at the oxide-[semiconductor interface](@entry_id:1131449) ($x=0$). The potential is continuous, $\psi_{si}(0^-) = \psi_{ox}(0^+)$. More critically, in the absence of a free sheet of charge at the interface, Gauss's law dictates that the normal component of the [electric displacement field](@entry_id:203286), $D = \epsilon E$, must also be continuous:

$$
\epsilon_{si}E_{si}(0^-) = \epsilon_{ox}E_{ox}(0^+)
$$

This boundary condition is the lynchpin connecting the charge within the semiconductor to the electric field in the oxide and, ultimately, to the voltage on the gate electrode .

#### The Fundamental Voltage Balance

The primary goal is to relate the externally applied gate voltage, $V_g$, to the internal state of the semiconductor. The key internal variable is the **surface potential**, $\psi_s$, defined as the total potential drop across the semiconductor's space-charge region, referenced to the neutral bulk. If we set the potential in the bulk to zero, then $\psi_s$ is simply the potential at the semiconductor surface: $\psi_s \equiv \psi_{si}(0^-)$.

An applied gate voltage $V_g$ must account for any built-in potentials and then distribute the remaining potential across the oxide and the semiconductor. For an ideal MOS capacitor (with no oxide or interface charges), the voltage balance is given by:

$$
V_g = \phi_{ms} + \psi_s + V_{ox}
$$

Here, $\phi_{ms}$ is the **work-function difference** between the gate metal and the semiconductor, representing the [built-in potential](@entry_id:137446) of the device that must be overcome. $V_{ox}$ is the voltage drop across the oxide. From the constant electric field in the oxide, $E_{ox}$, we have $V_{ox} = E_{ox} t_{ox}$. The interfacial boundary condition relates this field to the total charge per unit area in the semiconductor, $Q_s$. By applying Gauss's law, we find that the displacement field at the oxide side of the interface, $D_{ox}(0^+) = \epsilon_{ox} E_{ox}$, must be equal to the total charge it terminates, which by [charge neutrality](@entry_id:138647) of the capacitor is $-Q_s$. Thus, $\epsilon_{ox} E_{ox} = -Q_s$.

Substituting this into the expression for $V_{ox}$ and using the definition of oxide capacitance per unit area, $C_{ox} = \epsilon_{ox}/t_{ox}$, we find that the voltage drop across the oxide is:

$$
V_{ox} = \frac{-Q_s t_{ox}}{\epsilon_{ox}} = -\frac{Q_s}{C_{ox}}
$$

Substituting this back into the voltage balance ($V_g = \phi_{ms} + \psi_s + V_{ox}$) and rearranging gives the **fundamental voltage balance equation** for an ideal MOS structure :

$$
V_g - \phi_{ms} = \psi_s - \frac{Q_s}{C_{ox}}
$$

This elegant equation forms one half of the core system of a [surface-potential model](@entry_id:1132662). It states that the effective gate voltage, $V_g' = V_g - \phi_{ms}$, is partitioned between the potential drop in the semiconductor ($\psi_s$) and the potential drop across the oxide induced by the semiconductor charge ($-Q_s/C_{ox}$).

#### The Charge-Potential Relationship

The fundamental voltage balance equation relates three variables: $V_g$, $\psi_s$, and $Q_s$. To solve for the internal state ($\psi_s, Q_s$) for a given external bias ($V_g$), we need a second, independent relationship between $\psi_s$ and $Q_s$. This relationship is intrinsic to the semiconductor and is derived by solving Poisson's equation.

For a [p-type semiconductor](@entry_id:145767) with a uniform acceptor doping concentration $N_A$, the charge density $\rho_{si}$ includes contributions from ionized acceptors ($-qN_A$), mobile holes ($+qp(x)$), and mobile electrons ($-qn(x)$). Assuming non-degenerate Maxwell-Boltzmann statistics, the carrier concentrations vary exponentially with the local potential $\psi(x)$:

$$
p(x) = p_0 \exp\left(-\frac{\psi(x)}{\varphi_t}\right) \quad \text{and} \quad n(x) = n_0 \exp\left(\frac{\psi(x)}{\varphi_t}\right)
$$

where $p_0 \approx N_A$ and $n_0 = n_i^2/N_A$ are the bulk concentrations, and $\varphi_t = k_B T / q$ is the [thermal voltage](@entry_id:267086). Integrating Poisson's equation once from the bulk (where $E=0, \psi=0$) to the surface gives the surface electric field, $E_s$. The total semiconductor charge is then found via Gauss's law, $Q_s = -\epsilon_{si}E_s$. This procedure yields a single, continuous expression for $Q_s$ as a function of $\psi_s$, valid for all operating regimes—accumulation, depletion, and inversion :

$$
Q_s(\psi_s) = -\operatorname{sgn}(\psi_s)\sqrt{2\epsilon_{si}q\varphi_t\left\{p_0\left[\exp\left(-\frac{\psi_s}{\varphi_t}\right) - 1 + \frac{\psi_s}{\varphi_t}\right] + n_0\left[\exp\left(\frac{\psi_s}{\varphi_t}\right) - 1\right]\right\}}
$$

This equation, while complex, has a clear physical interpretation. The term proportional to $p_0$ represents the contribution of majority carriers (holes) and the fixed acceptor ions. The term proportional to $n_0$ represents the contribution of minority carriers (electrons). Together, the fundamental voltage balance and this charge-potential relationship form a complete, implicit system that can be solved numerically to find $\psi_s$ for any given gate voltage.

### Key Operating Regimes and Parameters

The continuous nature of the [surface-potential model](@entry_id:1132662) is one of its greatest strengths, but it is still instructive to examine key operating points and regimes defined by specific values of $\psi_s$.

#### Flatband and Threshold Conditions

Two of the most important reference points in MOSFET operation are flatband and threshold .

The **flatband condition** occurs when there is no band bending in the semiconductor, meaning the surface potential is zero: $\psi_s = 0$. At this point, the semiconductor charge is also zero ($Q_s=0$). The gate voltage required to achieve this is the **flatband voltage**, $V_{FB}$. For an ideal device, this simply counteracts the work-function difference, $V_{FB} = \phi_{ms}$. For a non-ideal device with oxide charge $Q_f$, this becomes $V_{FB} = \phi_{ms} - Q_f/C_{ox}$. $V_{FB}$ serves as the fundamental zero-point for the device's electrostatic response.

The **threshold condition** marks the onset of **[strong inversion](@entry_id:276839)**. This is physically defined as the point where the [surface concentration](@entry_id:265418) of minority carriers (electrons in a p-type substrate) becomes equal to the bulk concentration of majority carriers. This corresponds to a surface potential of:

$$
\psi_s = 2\phi_F
$$

where $\phi_F = \varphi_t \ln(N_A/n_i)$ is the **bulk Fermi potential**. The gate voltage required to reach this condition is the **threshold voltage**, $V_T$. At this point, the semiconductor charge consists almost entirely of the depletion charge required to support the [band bending](@entry_id:271304) of $2\phi_F$.

#### The Physics of the Inversion Layer

The behavior of the inversion charge, $Q_i$, is central to transistor action.

In **[weak inversion](@entry_id:272559)** (or the subthreshold regime), where $\phi_F \le \psi_s \le 2\phi_F$, the inversion charge is small but not zero. It is this charge that gives rise to the [subthreshold current](@entry_id:267076). The concentration of inversion electrons at the surface, $n_s$, depends exponentially on the surface potential, $n_s \propto \exp(\psi_s/\varphi_t)$. The total inversion charge per unit area, $Q_i$, is the integral of this concentration over the thin inversion layer. Because the potential decays away from the surface, the charge is confined to a very thin layer. The effective thickness of this layer is determined by the balance between the confining surface electric field $E_s$ and thermal diffusion, resulting in a characteristic depth of approximately $W = \varphi_t/E_s$. This leads to an exponential dependence of the total inversion charge on the surface potential :

$$
Q_i(\psi_s) \propto -\exp\left(\frac{\psi_s}{\varphi_t}\right)
$$

In **strong inversion** ($\psi_s > 2\phi_F$), the inversion charge concentration becomes very large and grows exponentially with further increases in $\psi_s$. This vast supply of mobile charge becomes extremely effective at screening the electric field from the gate. As a result, applying a higher gate voltage primarily serves to increase the inversion charge $Q_i$, while the surface potential $\psi_s$ increases only very slowly (logarithmically). This phenomenon is known as **surface potential pinning** . The surface potential is effectively "pinned" near $2\phi_F$, providing the physical basis for simpler threshold-voltage-based models which assume this pinning is perfect.

### From Capacitor to Transistor: Modeling the Channel

To model a transistor, we must extend the 1D vertical MOS model to account for the channel extending from source to drain.

#### Core State Variables for the MOSFET

The **gradual channel approximation (GCA)** is the key simplifying assumption. It posits that the electric field perpendicular to the channel is much stronger than the field parallel to it. This allows us to treat the device as a series of infinitesimal 1D MOS capacitors along the channel, from the source ($x=0$) to the drain ($x=L$). At each point $x$, the local 1D electrostatics hold, but they are modulated by the local channel potential, $V(x)$.

A one-dimensional transport problem, like current flow along the channel, is uniquely defined by its boundary conditions. Therefore, to determine the state of the entire channel (e.g., the charge and potential profiles $Q_i(x)$ and $\psi_s(x)$), we only need to know the conditions at the two endpoints: the source and the drain. This leads to a profound insight: a minimal and sufficient set of [internal state variables](@entry_id:750754) for the entire transistor consists of the surface potentials at the source and drain ends, $(\psi_{s,source}, \psi_{s,drain})$ . Alternatively, due to the unique relationship between charge and potential, one can use the inversion charge densities at the ends, $(Q_{i,source}, Q_{i,drain})$, or a normalized version thereof. Once these two boundary values are known, the current and the integrated terminal charges ($Q_g, Q_d, Q_s, Q_b$) can all be calculated. This is the core principle that makes surface-potential-based compact models computationally efficient.

#### Relating Surface Potential to Gate Voltage: The Subthreshold Swing

The gate's control over the surface potential is not perfect. A change in gate voltage, $dV_g$, is partitioned between the oxide and the semiconductor. The small-signal coupling is described by a capacitive voltage divider. Differentiating the voltage balance equation reveals this relationship:

$$
\frac{d\psi_s}{dV_g} = \frac{C_{ox}}{C_{ox} + C_{dep}}
$$

where $C_{dep} = -\partial Q_{dep}/\partial \psi_s$ is the depletion capacitance. In the subthreshold regime, the drain current is proportional to the inversion charge, which is exponential in $\psi_s$. This means $I_D \propto \exp(\psi_s/\varphi_t)$. The relationship between current [and gate](@entry_id:166291) voltage then becomes $I_D \propto \exp(V_g/(n\varphi_t))$, where $n$ is the **subthreshold slope factor** (or [body effect coefficient](@entry_id:265189)) :

$$
n = \left(\frac{d\psi_s}{dV_g}\right)^{-1} = 1 + \frac{C_{dep}}{C_{ox}}
$$

This factor quantifies the "gate control." An ideal device would have $n=1$, but the presence of depletion capacitance ($C_{dep}>0$) always makes $n>1$, leading to a subthreshold swing greater than the ideal limit of $\approx 60$ mV/decade at room temperature.

### Incorporating Physical Non-Idealities

Real devices are not ideal. A robust model must account for charges in the oxide and at the interface, as well as multi-dimensional electrostatic effects.

#### Interface and Oxide Charges

Real MOS structures contain **[fixed oxide charge](@entry_id:1125047)** ($Q_f$), typically located near the interface, and **interface traps** ($Q_{it}$), which can trap and release charge as the surface potential changes. These charges must be included in the [charge neutrality condition](@entry_id:1122298). The fundamental voltage balance equation becomes :

$$
V_g - \phi_{ms} = \psi_s - \frac{Q_s + Q_f + Q_{it}(\psi_s)}{C_{ox}}
$$

The fixed charge $Q_f$ is constant and causes a simple rigid shift in the voltage characteristics, directly affecting the flatband and threshold voltages by an amount $\Delta V = -Q_f/C_{ox}$. A positive $Q_f$ in an n-channel device, for example, helps to attract electrons, thus lowering the threshold voltage.

Interface traps are more complex. The charge they hold, $Q_{it}$, depends on $\psi_s$. This has two effects. First, the charge stored at threshold, $Q_{it}(2\phi_F)$, contributes a static shift to $V_T$. Second, the traps contribute their own capacitance, $C_{it} = -\partial Q_{it}/\partial \psi_s$, which acts in parallel with the depletion capacitance. This further weakens the gate's control over the surface potential. The subthreshold slope factor is modified to include this term  :

$$
n = 1 + \frac{C_{dep} + C_{it}}{C_{ox}}
$$

This leads to a degradation of the subthreshold swing, a key performance metric for modern transistors.

#### Short-Channel Effects: Drain-Induced Barrier Lowering (DIBL)

In short-channel devices, the GCA begins to break down. The drain voltage can electrostatically influence the potential barrier at the source end of the channel, a 2D effect known as **Drain-Induced Barrier Lowering (DIBL)**. From a surface-potential perspective, applying a drain voltage $V_{ds}$ raises the source-end surface potential, $\psi_{s,source}$, for a fixed gate voltage. To restore the threshold condition ($\psi_{s,source} = 2\phi_F$), the gate voltage must be reduced. This manifests as a drain-voltage-dependent threshold voltage shift, $\Delta V_{th}(V_{ds})$.

The influence of the drain potential decays exponentially into the channel with a characteristic **electrostatic scaling length**, $\lambda$, which depends on the device geometry (e.g., oxide thickness, depletion width). The magnitude of the barrier lowering at the source is thus proportional to $V_{ds}$ and $\exp(-L/\lambda)$. The required compensating gate voltage change is this potential shift amplified by the body effect factor, $n$. This leads to a leading-order expression for the DIBL-induced threshold shift :

$$
\Delta V_{th}(V_{ds}) \approx -n \exp\left(-\frac{L}{\lambda}\right) V_{ds} = - \left(1 + \frac{C_{dep}}{C_{ox}}\right) \exp\left(-\frac{L}{\lambda}\right) V_{ds}
$$

The negative sign confirms that DIBL lowers the threshold voltage, making it easier to turn the device on. The ability of the surface-potential framework to naturally incorporate and provide physical insight into such complex 2D effects is a testament to its power and versatility.