## Introduction
Switched-mode power converters are the cornerstone of modern power electronics, yet their inherent nonlinear and time-varying nature presents a significant challenge for analysis and control design. To achieve stable, high-performance regulation, engineers must understand how a converter responds to both control commands and external disturbances like input voltage variations. This article addresses this challenge by providing a comprehensive guide to the [small-signal modeling](@entry_id:1131775) of DC-DC converters, focusing on two fundamental models: the control-to-output and input-to-output [transfer functions](@entry_id:756102). By mastering these concepts, you will gain the ability to predict dynamic behavior, design robust feedback and feedforward controllers, and understand the fundamental performance limits of any given topology. The first chapter, "Principles and Mechanisms," will guide you through the [state-space averaging](@entry_id:1132297) technique to derive these [transfer functions](@entry_id:756102) for common converters. Following this, "Applications and Interdisciplinary Connections" will demonstrate their practical use in analyzing audio susceptibility, designing controllers, and understanding system-level interactions. Finally, "Hands-On Practices" will offer exercises to solidify your understanding of these essential engineering tools.

## Principles and Mechanisms

In the analysis and design of [feedback control](@entry_id:272052) for switched-mode power converters, it is essential to understand the dynamic response of the power stage to changes in its control inputs and external disturbances. As these converters are inherently nonlinear and [time-varying systems](@entry_id:175653), direct analysis is intractable. We therefore employ a powerful technique known as **[state-space averaging](@entry_id:1132297)** to create a continuous-time, time-invariant model that accurately captures the converter's low-frequency dynamics. This model is then linearized around a specific DC operating point to yield a [small-signal model](@entry_id:270703), which is amenable to linear control theory. This chapter delineates the principles behind this modeling approach and the mechanisms that govern the dynamic behavior of common converter topologies.

### Small-Signal Modeling and Fundamental Transfer Functions

The first step in our analysis is to establish a clear framework for modeling. The state of a converter is typically described by the energy stored in its inductors and capacitors, represented by the inductor currents and capacitor voltages. The [state-space averaging](@entry_id:1132297) technique yields a set of [nonlinear differential equations](@entry_id:164697) that describe the evolution of the cycle-averaged values of these [state variables](@entry_id:138790).

To analyze the system's response to small changes, we linearize this averaged model around a quiescent DC operating point. This operating point is defined by the steady-state, period-averaged values of the state variables, such as the inductor current $I_L$ and the capacitor voltage $V_C$, for a given set of constant inputs (input voltage $V_g$ and duty ratio $D$) and a load $R$. Any time-varying quantity is then expressed as the sum of its DC operating point value and a small, zero-mean AC perturbation. For instance, the output voltage $v_o(t)$, inductor current $i_L(t)$, input voltage $v_g(t)$, and duty ratio $d(t)$ are decomposed as follows :

$v_o(t) = V_O + \hat{v}_o(t)$
$i_L(t) = I_L + \hat{i}_L(t)$
$v_g(t) = V_g + \hat{v}_g(t)$
$d(t) = D + \hat{d}(t)$

Here, the uppercase letters denote the constant DC values at the operating point, and the hatted variables represent the small-signal perturbations. It is crucial to recognize that these perturbations model the low-frequency dynamics of the averaged quantities, not the high-frequency switching ripple, which is removed by the averaging process itself. The output voltage, $v_o(t)$, is the regulated voltage delivered to the load. In a non-isolated converter, it is measured across the output capacitor with respect to the common ground. In an isolated converter, it is measured across the secondary-side output capacitor with respect to the secondary-side ground .

This linearization process results in a Linear Time-Invariant (LTI) model that describes how the perturbations evolve. For a typical converter with two primary inputs—the control input ([duty ratio](@entry_id:199172)) and the line voltage—we can define two critical transfer functions that characterize the system's dynamics. These are derived by applying the principle of superposition, which is valid for LTI systems. Each transfer function is found by considering the effect of one input perturbation while setting the other independent input perturbation to zero .

The **control-to-output transfer function**, denoted $G_{vd}(s)$, describes how perturbations in the [duty ratio](@entry_id:199172) affect the output voltage. It is defined in the Laplace domain as:

$G_{vd}(s) = \frac{\hat{v}_o(s)}{\hat{d}(s)} \bigg|_{\hat{v}_g(t)=0}$

This transfer function quantifies the sensitivity of the output voltage to the control input. It is the fundamental "plant" model used in designing the feedback compensator. Since the [duty ratio](@entry_id:199172) $\hat{d}(t)$ is a dimensionless quantity and the output $\hat{v}_o(t)$ is a voltage, the units of $G_{vd}(s)$ are **volts**.

The **input-to-output transfer function**, denoted $G_{vg}(s)$, describes how perturbations in the input voltage propagate to the output voltage. It is defined as:

$G_{vg}(s) = \frac{\hat{v}_o(s)}{\hat{v}_g(s)} \bigg|_{\hat{d}(t)=0}$

This transfer function measures the converter's rejection of line voltage variations. For this reason, it is also commonly referred to as **line-to-output transfer function** or **audio susceptibility**. The term "audio susceptibility" arises because a common source of input voltage ripple is an upstream AC-DC rectifier, which often produces ripple at twice the line frequency (e.g., $100$ Hz or $120$ Hz). These frequencies fall within the audio spectrum. A large magnitude of $G_{vg}(s)$ at these frequencies indicates poor line rejection, meaning the converter is "susceptible" to this "audio" frequency ripple, which can manifest as audible noise from components like ceramic capacitors or magnetics . Since both the numerator and denominator of $G_{vg}(s)$ are voltages, this transfer function is **dimensionless** (Volts/Volt).

### Derivation via State-Space Averaging: The Buck Converter

The systematic derivation of these [transfer functions](@entry_id:756102) is best illustrated with an example. Let us consider an ideal [synchronous buck converter](@entry_id:1132781) operating in Continuous Conduction Mode (CCM). The power stage has an inductor $L$, a capacitor $C$, and a load resistance $R$.

The derivation follows a structured, four-part process:

1.  **Averaged Model Formulation:** The first step is to derive the averaged [state equations](@entry_id:274378). The natural state variables are the inductor current $i_L(t)$ and the capacitor voltage $v_C(t)$. For an ideal buck converter, the averaged equations are:
    $L \frac{di_L(t)}{dt} = d(t)v_g(t) - v_C(t)$
    $C \frac{dv_C(t)}{dt} = i_L(t) - \frac{v_C(t)}{R}$
    Note that the first equation contains a product of two time-varying quantities, $d(t)v_g(t)$, which makes the model nonlinear.

2.  **Equilibrium (DC) Operating Point:** We find the [steady-state solution](@entry_id:276115) by setting the time derivatives to zero and assuming constant inputs, yielding the DC relations $V_C = D V_g$ and $I_L = V_C / R$.

3.  **Linearization and Small-Signal State-Space Model:** We substitute the perturbed variables (e.g., $i_L = I_L + \hat{i}_L$) into the averaged model, subtract the DC steady-[state equations](@entry_id:274378), and neglect all products of small-signal terms. This yields a set of [linear differential equations](@entry_id:150365) for the perturbations. For the buck converter, these are :
    $L \frac{d\hat{i}_L(t)}{dt} = V_g \hat{d}(t) + D \hat{v}_g(t) - \hat{v}_C(t)$
    $C \frac{d\hat{v}_C(t)}{dt} = \hat{i}_L(t) - \frac{\hat{v}_C(t)}{R}$

    These can be written in the [standard state](@entry_id:145000)-[space form](@entry_id:203017) $\dot{\hat{x}}(t) = A\hat{x}(t) + B_d \hat{d}(t) + B_g \hat{v}_g(t)$ with the state vector $\hat{x}(t) = \begin{pmatrix} \hat{i}_L(t) & \hat{v}_C(t) \end{pmatrix}^T$. The output is $\hat{v}_o(t) = \hat{v}_C(t)$, so the output equation is $\hat{y}(t) = C_{out}\hat{x}(t)$ with $C_{out} = \begin{pmatrix} 0 & 1 \end{pmatrix}$. The resulting matrices are:
    $A = \begin{pmatrix} 0 & -\frac{1}{L} \\ \frac{1}{C} & -\frac{1}{RC} \end{pmatrix}$, $B_d = \begin{pmatrix} \frac{V_g}{L} \\ 0 \end{pmatrix}$, $B_g = \begin{pmatrix} \frac{D}{L} \\ 0 \end{pmatrix}$

4.  **Transfer Function Calculation:** The transfer function from an input $u$ with input matrix $B$ to the output is given by the general formula $G(s) = C_{out} (sI - A)^{-1} B$. Applying this formula gives the transfer functions for the buck converter:
    $G_{vd}(s) = \frac{V_g}{LCs^2 + \frac{L}{R}s + 1}$
    $G_{vg}(s) = \frac{D}{LCs^2 + \frac{L}{R}s + 1}$

The denominator is a second-order polynomial, reflecting the two energy storage elements, the inductor and the capacitor. The **minimal state dimension** required to capture the dynamics of a converter is equal to the number of independent energy storage elements in the circuit, which for a standard buck, boost, or [buck-boost converter](@entry_id:270314) in CCM is **2** .

To illustrate with a concrete example, consider a buck converter with $L = 1.2 \times 10^{-7} \text{ H}$, $C = 4.7 \times 10^{-8} \text{ F}$, $R = 0.8 \Omega$, $V_g = 1.8 \text{ V}$, and $D = 0.55$. The denominator coefficients are $LC = 5.64 \times 10^{-15}$ and $L/R = 1.5 \times 10^{-7}$. The transfer functions become :
$G_{vd}(s) = \frac{1.8}{5.64 \times 10^{-15} s^2 + 1.5 \times 10^{-7} s + 1}$
$G_{vg}(s) = \frac{0.55}{5.64 \times 10^{-15} s^2 + 1.5 \times 10^{-7} s + 1}$

### Key Dynamic Features: The Right-Half-Plane Zero

While the buck converter exhibits a simple second-order low-pass response, other topologies like the boost and flyback converters have a more complex and challenging dynamic characteristic: a **Right-Half-Plane Zero (RHPZ)** in their control-to-output transfer function. This feature has profound implications for [control loop design](@entry_id:1123004).

Let's derive the transfer function for an ideal CCM boost converter. Following the same [state-space averaging](@entry_id:1132297) and linearization procedure, we find its control-to-output transfer function is :

$G_{vd}(s) = V_o \frac{(1-D) - s \frac{LI_L}{V_o}}{s^2LC + s\frac{L}{R} + (1-D)^2}$

Substituting the steady-state DC relations $I_L = V_o / ((1-D)R)$, the numerator term simplifies, and the RHPZ location $s_z$ is found by setting the numerator to zero:
$(1-D)V_o - s_z L I_L = 0 \implies s_z = \frac{(1-D)V_o}{LI_L} = \frac{R(1-D)^2}{L}$

Since $R$, $L$, and $(1-D)^2$ are all positive, $s_z$ is a positive real number. A zero in the right half of the [s-plane](@entry_id:271584) introduces phase lag that increases with frequency, similar to a pole, but its magnitude response increases with frequency, like a left-half-plane zero. This conflicting behavior severely limits the achievable closed-loop bandwidth.

The physical origin of the RHPZ is an **[inverse response](@entry_id:274510)** in the time domain. Consider a step increase in the duty cycle $D$ of a boost converter.
1.  **Initial Response:** The switch is held on for a longer duration. During the switch ON-time, the inductor is disconnected from the output, and the output capacitor must supply the load current alone. A longer ON-time means the output is "starved" of current from the source for a longer fraction of the switching cycle. This causes the output voltage $v_o$ to *initially dip*.
2.  **Final Response:** The longer ON-time allows the inductor to store more energy. This increased energy is delivered to the output during the OFF-time, eventually causing the output voltage to rise to its new, higher steady-state value.

This behavior—an initial response in the opposite direction of the final [steady-state response](@entry_id:173787)—is the hallmark of a [non-minimum-phase system](@entry_id:270162) and is caused by the RHPZ . The same mechanism applies to the [flyback converter](@entry_id:1125159), which is topologically a derivative of the [buck-boost converter](@entry_id:270314) and also exhibits an RHPZ. It's noteworthy that this RHPZ is eliminated when these converters operate in Discontinuous Conduction Mode (DCM), as the inductor energy is fully delivered to the output each cycle, removing the conflicting energy transfer dynamic.

Interestingly, the RHPZ is a feature of the [control path](@entry_id:747840), not the line input path. The input-to-output transfer function $G_{vg}(s)$ for the boost converter is :

$G_{vg}(s) = \frac{1-D}{s^2LC + s\frac{L}{R} + (1-D)^2}$

This transfer function has no finite zeros. A perturbation in input voltage $\hat{v}_g$ directly increases the rate of energy storage in the inductor, which subsequently raises the output voltage, a straightforward low-pass response without the conflicting pathways that cause the RHPZ in $G_{vd}(s)$.

### The Impact of Practical Non-Idealities

The ideal models provide foundational understanding, but practical design requires accounting for component non-idealities.

#### Capacitor ESR and the LHP Zero

Real capacitors have an **Equivalent Series Resistance (ESR)**, denoted $r_c$. This resistance has a significant impact on the converter's dynamics. When we include $r_c$ in our buck converter model, the output voltage is no longer just the capacitor voltage $v_c$, but the sum of $v_c$ and the voltage across the ESR: $\hat{v}_o(s) = \hat{v}_c(s) + r_c \hat{i}_C(s)$. Incorporating this into the [state-space model](@entry_id:273798) reveals a crucial modification to the [transfer functions](@entry_id:756102) :

$G_{vd}(s) = V_g \frac{1+sr_cC}{Denominator(s)}$
$G_{vg}(s) = D \frac{1+sr_cC}{Denominator(s)}$

Both [transfer functions](@entry_id:756102) now possess a **Left-Half-Plane Zero (LHPZ)** located at $s_z = -1/(r_c C)$, introduced by the term $(1+sr_cC)$ in the numerator. Unlike an RHPZ, an LHPZ is beneficial for control. It contributes positive phase, or **[phase lead](@entry_id:269084)**, to the system's frequency response. At a given frequency $\omega$, the [phase lead](@entry_id:269084) contributed by this zero is $\arctan(\omega r_c C)$. For a feedback loop with a crossover frequency $\omega_c$, this [phase lead](@entry_id:269084) can increase the [phase margin](@entry_id:264609), improving [system stability](@entry_id:148296). In some designs, this ESR-induced phase boost is intentionally used to stabilize the converter.

#### Digital Control, Delay, and Quantization

When a converter is digitally controlled, new non-idealities are introduced by the nature of the Digital Pulse Width Modulation (DPWM) and the control loop timing. The process of sampling the output, performing a digital computation, and updating the DPWM register introduces a time delay. Typically, the duty cycle calculated in one period is applied during the *next* period. This creates a **[transport delay](@entry_id:274283)** of at least one switching period, $T_s$. In the Laplace domain, this delay is represented by the transfer function $e^{-sT_s}$ .

This delay term is crucial because it introduces phase lag, $\phi_{delay} = -\omega T_s$, which erodes phase margin and limits the achievable control bandwidth. For analysis at frequencies well below the switching frequency ($\omega T_s \ll 1$), we can use a Taylor [series approximation](@entry_id:160794) for the delay:

$e^{-sT_s} \approx 1 - sT_s + \frac{1}{2}(sT_s)^2$

This [polynomial approximation](@entry_id:137391) allows the delay to be incorporated into standard LTI analysis tools. Additionally, the finite resolution of the DPWM module is typically modeled as an effective modulator gain, $k_m$.

### Validity and Limitations of the Averaged Model

Finally, it is essential to understand the limits of the [state-space](@entry_id:177074) averaged model. The act of averaging is fundamentally a low-pass filtering operation. The model is valid only under the condition of **time-scale separation**: the dynamics of interest must be at frequencies much lower than the switching frequency, $f_s$ .

A more exact representation of the system is a **sampled-data model**, which accounts for the discrete-time nature of the PWM process. It can be shown that the state-space averaged model is a low-frequency approximation of this more exact model. The relationship between the exact sampled-data control-to-output transfer function, $G_{vd,exact}(j\omega)$, and the averaged one, $\bar{G}_{vd}(j\omega)$, can be approximated as :

$G_{vd,exact}(j\omega) \approx \bar{G}_{vd}(j\omega) \cdot H_{ZOH}(j\omega) = \bar{G}_{vd}(j\omega) \cdot e^{-j\omega T_s/2} \mathrm{sinc}\left(\frac{\omega T_s}{2}\right)$

where $H_{ZOH}(j\omega)$ is the frequency response of the [zero-order hold](@entry_id:264751) inherent in the PWM process. This correction term reveals two key errors in the simple averaged model:
1.  **Phase Error:** An additional phase lag of approximately $-\omega T_s/2$ [radians](@entry_id:171693) (a half-period delay).
2.  **Magnitude Error:** A magnitude reduction of approximately $(1/24)(\omega T_s)^2$.

For high-performance, high-bandwidth control design, accounting for this extra delay and the full computational delay is critical for an accurate prediction of [system stability](@entry_id:148296) and performance. Similarly, when analyzing the effect of input ripple in the presence of an EMI filter, the [small-signal model](@entry_id:270703) is only valid if the ripple amplitude is small ($|\hat{v}_g| \ll V_g$), its frequency is well below the switching frequency ($\omega_r \ll 2\pi f_s$), and the filter-converter system is stable, which is often assessed using the Middlebrook criterion for input [filter design](@entry_id:266363) .