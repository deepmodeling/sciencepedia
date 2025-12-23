## Introduction
Analyzing the dynamic, time-varying behavior of Metal-Oxide-Semiconductor Field-Effect Transistors (MOSFETs) requires a model that goes beyond steady-state currents. The charging and discharging of internal device capacitances are paramount, and an accurate model must correctly describe the charge stored at each terminal. Early, simplistic approaches to partitioning the mobile channel charge between the source and drain often violated fundamental physical laws, leading to significant errors in circuit simulations. This created a critical knowledge gap: the need for a physically consistent framework that guarantees both [charge conservation](@entry_id:151839) and reciprocity.

This article provides a comprehensive exploration of the Ward-Dutton charge partitioning scheme, the definitive solution to this problem. In the first chapter, **Principles and Mechanisms**, you will learn the theoretical underpinnings of the scheme, including the quasi-static approximation and the justification for its unique linear weighting functions. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the model's essential role in modern [circuit simulation](@entry_id:271754), its robustness across operating regimes, and its extension to advanced devices like FinFETs. Finally, the **Hands-On Practices** section will allow you to solidify your understanding by applying these concepts to solve practical device modeling problems.

## Principles and Mechanisms

The analysis of Metal-Oxide-Semiconductor Field-Effect Transistors (MOSFETs) for steady-state, direct-current (DC) applications primarily focuses on terminal currents as a function of terminal voltages. However, for dynamic applications involving time-varying signals, such as in analog, radio-frequency (RF), or digital switching circuits, this DC view is insufficient. The dynamic behavior is governed by the charging and discharging of the inherent capacitances within the device. A physically accurate model must therefore account for the charge stored at each terminal, as the terminal currents are fundamentally the time derivatives of these stored charges, $I_k(t) = dQ_k/dt$. The Ward-Dutton charge partitioning scheme provides a robust and physically consistent framework for modeling these terminal charges.

### The Quasi-Static Approximation

Charge-based models like the Ward-Dutton scheme are typically formulated under the **quasi-static (QS) approximation**. This core assumption posits that at any given instant in time, the distribution of mobile and fixed charges within the transistor is identical to the steady-state (DC) distribution that would exist for the instantaneous values of the terminal voltages at that moment. In effect, the model assumes that the charge carriers in the channel can redistribute themselves instantaneously in response to changes in the applied voltages.

This approximation simplifies the analysis immensely, as it allows the use of DC-derived equations to describe the [charge distribution](@entry_id:144400) at any point in time. However, this simplification has its limits. In reality, it takes a finite amount of time for carriers to travel across the channel. This characteristic time is known as the **channel transit time**, $\tau_{\mathrm{tr}}$, which can be approximated as the ratio of the effective channel length, $L_{\mathrm{eff}}$, to a characteristic carrier velocity, $v$. The [quasi-static assumption](@entry_id:1130450) is valid only when the time scale of the signal variation is much longer than the channel transit time. For a sinusoidal signal with period $T_s$ and [angular frequency](@entry_id:274516) $\omega = 2\pi/T_s$, the validity condition for the quasi-static approximation is given by:

$$ \tau_{\mathrm{tr}} \ll T_s \quad \text{or equivalently} \quad \omega \tau_{\mathrm{tr}} \ll 1 $$

When this condition is met, the internal charge distribution can "keep up" with the external voltage changes. When the [signal frequency](@entry_id:276473) becomes comparable to or higher than the transit frequency ($f_T \approx 1/(2\pi \tau_{\mathrm{tr}})$), the QS approximation breaks down, and more complex **non-quasi-static (NQS)** effects must be considered . For the remainder of this chapter, we will operate within the domain of validity of the QS approximation.

### The Imperatives of a Physical Charge Model: Conservation and Reciprocity

To be physically meaningful and suitable for reliable [circuit simulation](@entry_id:271754), any terminal charge model must satisfy two fundamental principles: [charge conservation](@entry_id:151839) and reciprocity.

**Charge conservation** dictates that for an electrically isolated multi-terminal device, the total charge must remain constant. In the context of a four-terminal MOSFET (gate, drain, source, bulk), this means that the sum of all terminal charges must be zero (assuming the device is initially neutral):

$$ Q_G + Q_D + Q_S + Q_B = 0 $$

This global conservation law must hold true for all bias conditions. A model that violates this principle will also violate Kirchhoff's Current Law at the terminal level, as $\sum I_k = d/dt (\sum Q_k) \neq 0$, leading to unphysical simulation results .

**Reciprocity** is a more subtle but equally crucial requirement for any passive device. It is embodied in the symmetry of the small-signal [capacitance matrix](@entry_id:187108). The transcapacitance $C_{ij}$ is defined as the change in charge at terminal $i$ with respect to a change in voltage at terminal $j$:

$$ C_{ij} = \frac{\partial Q_i}{\partial V_j} $$

Reciprocity requires that $C_{ij} = C_{ji}$ for any pair of terminals $i$ and $j$. This symmetry is a mathematical consequence of the existence of a scalar state function, the electrostatic co-energy $\Psi(\mathbf{V})$, from which all terminal charges can be derived as partial derivatives: $Q_i = \partial \Psi / \partial V_i$. If such a function exists, the equality of [mixed partial derivatives](@entry_id:139334) ($\partial^2\Psi/\partial V_i \partial V_j = \partial^2\Psi/\partial V_j \partial V_i$) guarantees reciprocity .

A partitioning scheme that is "non-conservative" in the sense that the charge definitions are arbitrarily voltage-dependent or do not sum correctly can break this condition. Such a non-reciprocal model does not correspond to a passive physical system. In an AC simulation, it can exhibit spurious energy generation or dissipation, leading to incorrect predictions of gain or loss and potentially causing severe convergence and stability problems in the simulator .

### The Partitioning Problem: Assigning Channel Charge

In a MOSFET, the charge associated with the gate electrode ($Q_G$) and the depletion charge in the semiconductor bulk ($Q_B$) can be assigned to their respective terminals in a relatively straightforward manner based on electrostatics. The key challenge lies in partitioning the mobile inversion charge in the channel, $Q_{ch}$, between the source and drain terminals, which act as the entry and exit points for these carriers.

A total mobile channel charge $Q_{ch}$ gives rise to a source-assigned charge $Q_S$ and a drain-assigned charge $Q_D$, such that $Q_S + Q_D = Q_{ch}$. A simple, intuitive approach is the **naive equal split** or **Meyer model**, where the charge is divided equally: $Q_S = Q_D = Q_{ch}/2$. While this method respects charge conservation, it fails the test of reciprocity. When a drain-source voltage $V_{DS}$ is applied, the channel charge distribution becomes non-uniform, skewing towards the source. The equal-split model ignores this physical reality, and as a consequence, it can be shown that $\partial Q_S / \partial V_D \neq \partial Q_D / \partial V_S$, violating reciprocity and rendering the model unphysical for dynamic analysis . This failure motivates the need for a more sophisticated, position-aware partitioning scheme.

### The Ward-Dutton Charge Partitioning Scheme

The Ward-Dutton scheme provides a physically grounded method for partitioning the channel charge that guarantees both charge conservation and reciprocity. It achieves this by assigning the charge based on its position along the channel.

Let us define a coordinate $x$ running from the source ($x=0$) to the drain ($x=L$). The mobile charge per unit length at position $x$ is denoted by $q(x)$. Under the gradual channel approximation for an n-channel MOSFET in strong inversion, this local charge is given by:

$$ q(x) = -W C_{ox} [V_{GS} - V_{TH} - V(x)] $$

where $W$ is the channel width, $C_{ox}$ is the gate oxide capacitance per unit area, $V_{GS}$ is the gate-source voltage, $V_{TH}$ is the threshold voltage, and $V(x)$ is the local channel potential at position $x$ .

The Ward-Dutton scheme partitions an infinitesimal element of charge $q(x)dx$ at position $x$ between the source and drain using linear **weighting functions**.
- The source weighting function is $w_S(x) = 1 - x/L$.
- The drain weighting function is $w_D(x) = x/L$.

Notice that these weights are purely geometric and bias-independent. The weight for the source is $1$ at the source end ($x=0$) and falls linearly to $0$ at the drain end ($x=L$), and vice versa for the drain weight. This captures the intuition that charge near the source is "owned" by the source, and charge near the drain is "owned" by the drain. The sum of the weights is $w_S(x) + w_D(x) = (1-x/L) + (x/L) = 1$ everywhere in the channel, which ensures that the entire channel charge is accounted for.

The total source- and drain-assigned charges are then found by integrating the weighted local charge along the channel :

$$ Q_S = \int_{0}^{L} w_S(x) q(x) \,dx = \int_{0}^{L} \left(1 - \frac{x}{L}\right) q(x) \,dx $$

$$ Q_D = \int_{0}^{L} w_D(x) q(x) \,dx = \int_{0}^{L} \frac{x}{L} q(x) \,dx $$

These definitions, combined with the electrostatic definitions for gate and bulk charge, form a complete and conservative set of terminal charges .

### Justification of the Linear Weighting

The choice of linear weighting functions is not arbitrary; it is precisely the form required to guarantee reciprocity. As shown in , if one imposes the reciprocity condition $\partial Q_S/\partial V_D = \partial Q_D/\partial V_S$ for an arbitrary channel charge profile (i.e., for any function $q(x)$), the only weighting functions that satisfy this condition, along with the boundary conditions and the conservation constraint $w_S(x) + w_D(x) = 1$, are uniquely determined to be $w_S(x) = 1 - x/L$ and $w_D(x) = x/L$.

This result can be justified from more fundamental physical principles:

1.  **Homogeneous Resistive Line Model:** If we model the MOSFET channel as a simple homogeneous resistive line, a current disturbance at position $x$ will split and flow towards the source and drain terminals. The current divides according to the conductances of the two path segments. This simple conductance divider model results directly in the linear weighting functions $1-x/L$ and $x/L$ .

2.  **Adjoint Electrostatic Problem:** A more rigorous justification comes from the theory of adjoint fields, related to the Shockley-Ramo theorem. The weighting function can be formally defined as the solution to a Laplace equation, $\nabla^2 \phi_w = 0$, within the device geometry, with boundary conditions of $\phi_w = 1$ at the "sensing" terminal (e.g., the source) and $\phi_w = 0$ at all other terminals. For an idealized long-channel rectangular geometry, the unique solution for the cross-sectionally averaged weighting potential is precisely the linear function $w(x) = 1 - x/L$. This shows that the linear partition is not just a convenient approximation but the exact solution for an idealized long-channel structure .

### Application and Bias Dependence

To see the model in action, we can calculate the terminal charges for a simplified case. Assume the channel potential varies linearly from source to drain, $V(x) = V_{DS} (x/L)$. This is a reasonable first approximation for a long-channel device in the [linear region](@entry_id:1127283). Substituting this and the expression for $q(x)$ into the integrals for $Q_S$ and $Q_D$ yields closed-form expressions :

$$ Q_S = -W L C_{ox} \left( \frac{V_{GS} - V_{TH}}{2} - \frac{V_{DS}}{6} \right) $$

$$ Q_D = -W L C_{ox} \left( \frac{V_{GS} - V_{TH}}{2} - \frac{V_{DS}}{3} \right) $$

From these results, we can observe the key consequences of the partitioning scheme.
-   At zero drain bias ($V_{DS}=0$), we find that $Q_S = Q_D$. The charge is split symmetrically, 50/50, as expected.
-   As $V_{DS}$ increases, the magnitude of $Q_D$ decreases faster than that of $Q_S$. This means a larger fraction of the total channel charge is attributed to the source. The partition becomes asymmetric.

This asymmetry is a key physical feature. As $V_{DS}$ increases, the inversion layer becomes weaker near the drain (a phenomenon known as channel pinch-off). The center of gravity of the channel [charge distribution](@entry_id:144400) shifts towards the source. The Ward-Dutton scheme correctly captures this shift. A more detailed analysis using a physically accurate, non-[linear potential](@entry_id:160860) profile derived from drift-[diffusion transport](@entry_id:1123719) equations shows that as the device approaches the saturation regime ($V_{DS} \to V_{GS} - V_{TH}$), the charge partition fractions approach a 60/40 split, with $f_s = Q_S / Q_{ch} \to 3/5$ and $f_d = Q_D / Q_{ch} \to 2/5$ . This non-symmetric partitioning is critical for accurately modeling the high-frequency transcapacitances of the device.

In summary, the Ward-Dutton charge partitioning scheme provides a framework that is simple, physically motivated, and computationally robust. By using bias-independent, linear weighting functions, it guarantees both charge conservation and reciprocity, correcting the fundamental flaws of simpler models and enabling accurate dynamic and AC simulation of MOS transistors.