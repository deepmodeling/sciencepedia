## Introduction
In the world of semiconductor device modeling, accuracy and physical consistency are paramount. Charge-based compact models represent a foundational pillar of modern circuit simulation, providing the robust framework necessary to predict the behavior of transistors with high fidelity. These models arose from the critical need to overcome a fundamental flaw in earlier approaches: the failure to conserve electric charge, which led to significant errors in dynamic and transient simulations. By establishing terminal charge, rather than current or capacitance, as the primary state variable, the charge-based methodology ensures that simulations adhere to one of physics' most basic laws.

This article provides a comprehensive exploration of the theory and application of charge-based compact models. The first chapter, "Principles and Mechanisms," will delve into the core tenets, including charge conservation, the surface-potential approach for calculating charge, and the derivation of a consistent transcapacitance matrix. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these principles translate into tangible benefits for DC characterization, high-frequency modeling, and the design of analog, RF, and power electronics, as well as their extension to advanced devices like FinFETs. Finally, "Hands-On Practices" will offer practical problems that solidify the connection between theory and real-world device characterization and simulation.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and underlying mechanisms of charge-based compact models for semiconductor devices, focusing on the Metal-Oxide-Semiconductor Field-Effect Transistor (MOSFET). We will proceed from the foundational imperative of charge conservation to the detailed construction of terminal charges and the resultant properties of the device's capacitive network. This framework is essential for creating predictive and physically consistent models capable of accurate transient and high-frequency circuit simulation.

### The Imperative of Charge Conservation

The primary motivation for the development of charge-based compact models stems from a fundamental requirement of physics: the conservation of electric charge. For any isolated device, the net charge must remain constant. In a circuit context, this is expressed through Kirchhoff's Current Law (KCL), which mandates that the algebraic sum of currents entering any node—or a multi-terminal device as a whole—must be zero at all times.

In a compact model, the terminal currents $I_i$ are composed of conduction and displacement components. Under the **Quasi-Static Approximation (QSA)**, which assumes the internal charge distribution of the device adjusts instantaneously to changes in terminal voltages, the displacement currents are given by the time derivatives of the terminal charges, $Q_i(\mathbf{V})$, where $\mathbf{V}$ is the vector of terminal voltages. The total current at terminal $i$ is thus $I_i = I_i^{\text{cond}} + dQ_i/dt$.

The sum of all terminal currents is therefore:
$$
\sum_i I_i = \sum_i I_i^{\text{cond}} + \frac{d}{dt} \left( \sum_i Q_i \right)
$$
In most operating regimes, the sum of conduction currents is zero (e.g., for a MOSFET, $I_d^{\text{cond}} + I_s^{\text{cond}} = 0$ and other conduction currents are negligible). For KCL to hold universally for the device ($\sum_i I_i = 0$), it is necessary that the time derivative of the total modeled charge be zero. This implies that the total charge itself must be constant. By convention, we model a neutral device, so this constant is zero. This leads to the central tenet of charge-based modeling: the **global charge conservation** condition [@problem_id:3733687]:
$$
Q_g(\mathbf{V}) + Q_d(\mathbf{V}) + Q_s(\mathbf{V}) + Q_b(\mathbf{V}) = 0
$$
This equation must hold for all possible bias conditions $\mathbf{V}$. Models that violate this condition, often termed "non-charge-conservative," produce a spurious net current $d/dt (\sum_i Q_i) \neq 0$ during transient operation. In a circuit simulator, this unphysical current must be sunk by the global ground reference, leading to accumulated charge errors, incorrect simulation of charge-sensitive circuits (like switched-capacitor filters or charge pumps), and numerical instability [@problem_id:3733687] [@problem_id:3733649]. Earlier models, which focused primarily on fitting DC current-voltage ($I-V$) characteristics and appended capacitances as an afterthought, often suffered from this "charge non-conservation" pathology.

### Foundational Principles of Charge-Based Models

A physically consistent charge-based model is built upon a set of rigorous principles derived from fundamental laws of physics [@problem_id:3733649]. These principles ensure that the model behaves correctly not only in DC but also in AC and transient simulations.

1.  **Primacy of Charge**: The fundamental state variables of the model are the terminal charges, $\{Q_g, Q_d, Q_s, Q_b\}$, which are expressed as unique, continuous functions of the terminal voltages, $\mathbf{V} = \{V_g, V_d, V_s, V_b\}$. The entire behavior of the model, including currents and capacitances, is derived from these charge functions.

2.  **Global Charge Conservation**: As established above, the sum of all terminal charges must identically be zero for all biases to ensure the model satisfies KCL in transient simulations.

3.  **Gauge Invariance (Reference Invariance)**: The internal state of a device (i.e., its internal electric fields and charge distributions) depends only on potential *differences* between its terminals, not on the absolute potential of the device as a whole. Therefore, a valid model must be invariant to a uniform shift in the reference potential. If all terminal voltages are shifted by a constant $\alpha$, the charges must not change:
    $$
    \mathbf{Q}(\mathbf{V} + \alpha\mathbf{1}) = \mathbf{Q}(\mathbf{V})
    $$
    where $\mathbf{1}$ is the vector of all ones. This implies that the charges $Q_i$ are functions of only the three independent voltage differences (e.g., $V_{gs} = V_g - V_s$, $V_{ds} = V_d - V_s$, and $V_{bs} = V_b - V_s$) [@problem_id:3733649]. A model that violates this principle can generate spurious currents when the common-mode voltage of the device changes [@problem_id:3733687].

4.  **Quasi-Static Currents**: The link between the charge state functions and the terminal currents is provided by the QSA. The total current flowing into each terminal is the sum of a conduction component (e.g., drift-diffusion current) and a displacement component given by the total time derivative of the terminal charge:
    $$
    I_i(t) = I_i^{\text{cond}}(\mathbf{V}(t)) + \frac{d Q_i(\mathbf{V}(t))}{dt}
    $$
    The QSA is valid when the frequency of the electrical signals is low compared to the inverse of the carrier transit time, $\tau_{tr}$, across the device. Formally, for a signal with angular frequency $\omega$, the condition is $\omega \tau_{tr} \ll 1$ [@problem_id:3775935].

### The Surface-Potential-Based Approach

To construct the functions $Q_i(\mathbf{V})$, we must look inside the device. Surface-potential-based models provide a physically rigorous method for this. They use the electrostatic potential at the semiconductor-insulator interface, the **surface potential** $\psi_s$, as the primary internal state variable that connects the external terminal voltages to the internal charge distribution.

In a MOS structure, the gate voltage $V_G$ controls the bending of the energy bands in the semiconductor. The amount of band bending at the surface is precisely the surface potential $\psi_s$. As derived from a one-dimensional analysis of the MOS capacitor using Poisson's equation, the applied gate voltage is partitioned between the voltage drop across the oxide ($V_{ox}$) and the potential at the semiconductor surface ($\psi_s$), plus a constant offset due to work function differences and fixed charges, known as the flat-band voltage $V_{FB}$ [@problem_id:3775966]. This gives the fundamental relationship:
$$
V_G - V_{FB} = \psi_s + V_{ox}
$$
The voltage across the oxide is supported by the charge on the gate, which mirrors the total charge in the semiconductor, $Q_{sc}$. By Gauss's law, $V_{ox} = -Q_{sc}/C_{ox}$, where $C_{ox}$ is the oxide capacitance per unit area. This yields the core equation of surface-potential models:
$$
V_G - V_{FB} = \psi_s - \frac{Q_{sc}(\psi_s)}{C_{ox}}
$$
This implicit equation links the external voltage $V_G$ to the internal variable $\psi_s$, which in turn determines the total semiconductor charge $Q_{sc}$. The power of this approach is that $Q_{sc}$ can be calculated accurately from fundamental semiconductor physics.

### Calculating Semiconductor Charge

The total semiconductor space charge, $Q_{sc}$, is composed of contributions from ionized dopant atoms (depletion charge, $Q_{dep}$) and mobile carriers (inversion charge, $Q_{inv}$, and accumulation charge, $Q_{acc}$).

As a simple illustration, we can calculate the depletion charge in a p-type substrate under the **depletion approximation**, which neglects mobile carriers in the space-charge region. Solving Poisson's equation shows that the depletion charge per unit area, $Q_{dep}$, is directly related to the surface potential $\psi_s$ [@problem_id:3776025]:
$$
Q_{dep}(\psi_s) = -\sqrt{2qN_A\epsilon_s\psi_s}
$$
where $q$ is the elementary charge, $N_A$ is the acceptor doping concentration, and $\epsilon_s$ is the semiconductor permittivity.

A more complete model, valid from subthreshold to strong inversion, must include the mobile inversion charge. This is derived from the Poisson-Boltzmann equation, which accounts for both fixed dopant ions and mobile carrier densities described by Boltzmann statistics. This yields a more complex expression for the total charge $Q_{sc}$ as a function of $\psi_s$ and the channel quasi-Fermi potential $V_{ch}$ (which represents the effect of the drain-source bias). The inversion charge, $Q_{inv}$, which is critical for current conduction, can then be isolated by subtracting the bulk charge (depletion and accumulation) from the total charge [@problem_id:3776011].

Alternatively, for simpler models, one can use approximations valid in strong inversion. For example, the total charge in the channel, $Q_{ch}$, can be expressed directly in terms of terminal voltages. In the linear regime ($V_{DS} \ll V_{GS}-V_T$), the average charge is lower due to the potential gradient, while in saturation, the charge profile is fixed by the pinch-off condition [@problem_id:3733672]. These simplified expressions are:
$$
Q_{ch,lin} = -W L C_{ox} \left[ (V_{GS}-V_T) - \frac{V_{DS}}{2} \right]
$$
$$
Q_{ch,sat} = -\frac{2}{3} W L C_{ox} (V_{GS}-V_T)
$$
where $W$ and $L$ are the channel width and length, and $V_T$ is the threshold voltage.

### Charge Partitioning

Once the total mobile charge in the channel, $Q_{ch} = \int q_{inv}(x) dx$, is known, it must be partitioned between the source and drain terminals to define $Q_s$ and $Q_d$. A physically-based method is required to ensure the resulting model is reciprocal and accurate. This is achieved by defining terminal-specific **weighting functions**, $w_s(x)$ and $w_d(x)$, which represent the fraction of a charge element at position $x$ that should be attributed to the source and drain, respectively.
$$
Q_s = \int_0^L w_s(x) q_{inv}(x) dx, \qquad Q_d = \int_0^L w_d(x) q_{inv}(x) dx
$$
To conserve charge ($Q_s + Q_d = Q_{ch}$), these functions must sum to one: $w_s(x) + w_d(x) = 1$. The canonical example is the **Ward-Dutton linear partitioning scheme** [@problem_id:3733654]. It is derived by considering the potential distribution in a uniform resistive channel, which is linear. This leads to the intuitive weighting functions:
$$
w_s(x) = 1 - \frac{x}{L}, \qquad w_d(x) = \frac{x}{L}
$$
This scheme correctly attributes charge at the source-end ($x=0$) entirely to the source ($w_s(0)=1, w_d(0)=0$) and charge at the drain-end ($x=L$) entirely to the drain ($w_d(L)=1, w_s(L)=0$).

### The Transcapacitance Matrix and Reciprocity

The rigorous, self-consistent derivation of charges from a unified physical framework has profound and beneficial consequences for the model's capacitive behavior. The small-signal capacitances are defined as the partial derivatives of the terminal charges with respect to the terminal voltages. Adopting the convention used in circuit simulation, the **transcapacitance matrix** $\mathbf{C}$ has elements:
$$
C_{ij} = -\frac{\partial Q_i}{\partial V_j}
$$
The negative sign ensures that the diagonal self-capacitances ($C_{gg}, C_{dd}$, etc.) are positive. This matrix exhibits crucial properties that are guaranteed by the charge-based formulation [@problem_id:3733649] [@problem_id:3733687]:

1.  **Column-Sum-Zero**: Differentiating the global charge conservation condition $\sum_i Q_i = 0$ with respect to any voltage $V_j$ yields $\sum_i (\partial Q_i / \partial V_j) = 0$. This directly implies that each column of the capacitance matrix sums to zero: $\sum_i C_{ij} = 0$.

2.  **Row-Sum-Zero**: As a consequence of gauge invariance, each individual charge $Q_i$ depends only on voltage differences. This implies that the sum of its derivatives with respect to all terminal voltages is zero, $\sum_j (\partial Q_i / \partial V_j) = 0$. This means each row of the capacitance matrix sums to zero: $\sum_j C_{ij} = 0$.

3.  **Reciprocity**: Because all terminal charges are derived as derivatives of a single underlying physical state (described by a potential energy), Maxwell relations apply. This guarantees that the capacitance matrix is symmetric: $C_{ij} = C_{ji}$. That is, $-\partial Q_i / \partial V_j = -\partial Q_j / \partial V_i$. This property, also known as reciprocity, is critical for ensuring the model does not spuriously generate or dissipate energy in the reactive network.

As a concrete example, by applying the Ward-Dutton partitioning scheme to a simple strong-inversion charge model, we can derive the intrinsic gate capacitances. The total gate charge is found to be $Q_G = W L C_{ox} (V_G - V_{th} - (V_S+V_D)/2)$. Taking the derivatives gives [@problem_id:3775937]:
$$
\frac{\partial Q_G}{\partial V_G} = W L C_{ox}
$$
$$
\frac{\partial Q_G}{\partial V_S} = -\frac{1}{2} W L C_{ox}
$$
$$
\frac{\partial Q_G}{\partial V_D} = -\frac{1}{2} W L C_{ox}
$$
(Note: Using the $C_{ij} = -\partial Q_i / \partial V_j$ definition, these become $-WLC_{ox}$, $+\frac{1}{2}WLC_{ox}$, and $+\frac{1}{2}WLC_{ox}$ respectively). Independent calculation of $Q_S$ and $Q_D$ and their derivatives confirms that $C_{sg} = C_{gs}$ and $C_{dg} = C_{gd}$, explicitly demonstrating the inherent reciprocity of the formulation.

### Ensuring Numerical Robustness

A final, practical principle in modern compact modeling is the need for numerical robustness when the model is implemented in a circuit simulator. Simulators like SPICE use iterative numerical methods, such as the Newton-Raphson algorithm, to solve the nonlinear system of circuit equations. The convergence of this algorithm relies on the Jacobian matrix of the system being continuous.

The model's transcapacitances, $C_{ij}$, are direct contributions to this Jacobian matrix. If the charge functions $Q_i(\mathbf{V})$ have "kinks" or points where their first derivatives are discontinuous (i.e., the model is not $C^1$ continuous), the capacitances will exhibit jump discontinuities. This typically occurs at the boundaries between different operating regimes (e.g., the transition from linear to saturation). A discontinuous Jacobian can cause the Newton-Raphson iteration to oscillate or fail, leading to slow simulations or convergence failures [@problem_id:3733671].

To prevent this, it is essential to construct charge expressions that are smooth and at least $C^1$ continuous across all operating regions. This is achieved by using **smoothing** or **blending functions** to create a seamless transition between the mathematical expressions for different regimes. A common and effective approach is to use a weighting function $w(S)$ based on the hyperbolic tangent, which is infinitely differentiable ($C^\infty$), to blend between a model for regime (a), $\mathbf{Q}^{(a)}$, and regime (b), $\mathbf{Q}^{(b)}$:
$$
\mathbf{Q}(\mathbf{V}) = \mathbf{Q}^{(a)}(\mathbf{V}) + w(S(\mathbf{V})) \left[ \mathbf{Q}^{(b)}(\mathbf{V}) - \mathbf{Q}^{(a)}(\mathbf{V}) \right]
$$
with
$$
w(S) = \frac{1}{2}\left(1 + \tanh\left(\frac{S}{\delta}\right)\right)
$$
Here, $S(\mathbf{V})=0$ defines the transition boundary, and $\delta$ is a parameter that controls the sharpness of the transition. Crucially, the same blending function must be applied to all terminal charges to preserve the global charge conservation property throughout the transition region [@problem_id:3733671]. By embracing this principle, charge-based models can be both physically rigorous and numerically robust.