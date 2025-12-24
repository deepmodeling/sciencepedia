## Introduction
Modeling the transmission of signals between neurons is a cornerstone of computational neuroscience. The synapse, as the [fundamental unit](@entry_id:180485) of communication, dictates how information is integrated and processed. Understanding its function requires abstracting its complex biology into a mathematically tractable form. However, this abstraction can be approached in several ways, leading to models with profoundly different computational properties. The most significant divergence in these approaches lies in the choice between current-based and conductance-based synaptic models. This choice is not merely a technical detail; it defines the elementary computations a model neuron can perform and shapes the dynamics of entire neural networks.

This article addresses the critical distinction between these two modeling frameworks. It clarifies why the seemingly simple decision to make [synaptic current](@entry_id:198069) dependent on postsynaptic voltage has far-reaching consequences. Across the following chapters, you will gain a comprehensive understanding of this topic. The "Principles and Mechanisms" chapter will lay out the mathematical and biophysical foundations of each model. "Applications and Interdisciplinary Connections" will explore how these differences manifest in single-neuron integration, [network dynamics](@entry_id:268320), and complex phenomena like [shunting inhibition](@entry_id:148905). Finally, "Hands-On Practices" will offer practical exercises to solidify your grasp of these core concepts. By navigating this comparison, you will be equipped to make informed decisions in your own modeling work and critically evaluate the literature.

## Principles and Mechanisms

### Foundational Models of Synaptic Integration

The interaction between synaptic inputs and the intrinsic properties of a neuron determines its computational function. To model this process, we begin with the [fundamental representation](@entry_id:157678) of a [neuronal membrane](@entry_id:182072) as a parallel resistor-capacitor (RC) circuit. In this framework, the membrane potential, $V(t)$, evolves according to the principle of [charge conservation](@entry_id:151839). The capacitive current, $C \frac{dV}{dt}$, must balance the sum of all [ionic currents](@entry_id:170309) flowing across the membrane. At its simplest, this includes a leak current, $I_L$, that accounts for the passive permeability of the membrane to various ions.

According to Ohm's law, this leak current is proportional to a constant **leak conductance**, $g_L$, and the difference between the membrane potential and the **leak [reversal potential](@entry_id:177450)**, $E_L$. The [reversal potential](@entry_id:177450) is the voltage at which there is no net flow of a particular ion, determined by its Nernst potential. The leak [reversal potential](@entry_id:177450) is thus a weighted average of the Nernst potentials for the ions that passively permeate the membrane, and it typically corresponds to the neuron's resting potential. The membrane equation for a passive neuron is therefore:

$$
C \frac{dV}{dt} = -g_L(V(t) - E_L) + I_{ext}(t)
$$

where $I_{ext}(t)$ represents any externally applied current, such as from an experimenter's electrode. Synaptic inputs are incorporated as an additional current, $I_{syn}(t)$, leading to the general form:

$$
C \frac{dV}{dt} = -g_L(V(t) - E_L) + I_{syn}(t)
$$

The critical distinction in synaptic modeling arises from how $I_{syn}(t)$ is defined. Two primary formulations exist: the current-based model and the [conductance-based model](@entry_id:1122855).

The **current-based synaptic model** treats synaptic input as an ideal current source. The [synaptic current](@entry_id:198069), $I_{syn}(t)$, is specified as a waveform that is independent of the postsynaptic membrane potential $V(t)$. If a neuron receives input from multiple presynaptic sources, their contributions are summed linearly:

$$
I_{syn}(t) = \sum_{j} w_j s_j(t)
$$

Here, $s_j(t)$ is a dimensionless variable representing the time course of the $j$-th synaptic event (e.g., a brief pulse or an alpha function), and $w_j$ is a constant weight with units of current. The defining feature of this model is its simplicity: the synaptic input is purely additive and does not interact with the state of the postsynaptic neuron. The complete membrane equation is:

$$
C \frac{dV}{dt} = -g_L(V(t) - E_L) + \sum_{j} w_j s_j(t)
$$

In contrast, the **conductance-based synaptic model** provides a more biophysically detailed description. It represents the opening of synaptic channels as the addition of a new, time-varying conductance to the membrane circuit. The current flowing through this [synaptic conductance](@entry_id:193384), $g_{syn}(t)$, also obeys Ohm's law. It is proportional to the **driving force**, which is the difference between the instantaneous membrane potential $V(t)$ and the specific **[synaptic reversal potential](@entry_id:911810)**, $E_{syn}$ . For a single synapse, the current is:

$$
I_{syn}(t) = g_{syn}(t) (E_{syn} - V(t))
$$

Note the convention: a positive current depolarizes the cell. The total current is the sum over all active synapses, each with its own conductance $g_j(t)$ and [reversal potential](@entry_id:177450) $E_j$. The full membrane equation becomes:

$$
C \frac{dV}{dt} = -g_L(V(t) - E_L) + \sum_{j} g_j(t)(E_j - V(t))
$$

This seemingly small change—making the synaptic current dependent on the postsynaptic voltage $V(t)$—has profound consequences for [neuronal dynamics](@entry_id:1128649) and computation.

### The Biophysical Consequences of Voltage Dependence

The voltage dependence inherent in the [conductance-based model](@entry_id:1122855) allows it to capture several key biophysical phenomena that the current-based model cannot. These include the modulation of intrinsic membrane properties, a divisive form of inhibition known as shunting, and the natural saturation of synaptic potentials.

#### Modulation of Intrinsic Membrane Properties

In a current-based model, the synaptic input is an external [forcing term](@entry_id:165986). The intrinsic properties of the neuron, governed by $C$ and $g_L$, remain unchanged. The membrane time constant, $\tau_m = C/g_L$, which dictates the speed of voltage integration, is static  .

In the [conductance-based model](@entry_id:1122855), the synaptic conductance $g_{syn}(t)$ adds in parallel to the leak conductance $g_L$. We can rewrite the membrane equation to make this explicit :

$$
C \frac{dV}{dt} = -(g_L + \sum_{j} g_j(t))V(t) + (g_L E_L + \sum_{j} g_j(t)E_j)
$$

The total instantaneous membrane conductance is $g_{tot}(t) = g_L + \sum_{j} g_j(t)$. Consequently, the **effective membrane time constant** becomes a dynamic quantity that decreases during periods of synaptic activity:

$$
\tau_{eff}(t) = \frac{C}{g_{tot}(t)} = \frac{C}{g_L + \sum_{j} g_j(t)}
$$

When synaptic conductances are active, the neuron becomes "leakier," and its voltage responds more quickly to inputs. This dynamic modulation of the integration time window is a fundamental computational feature of real neurons, particularly in high-activity states.

#### Shunting Inhibition: A Divisive Mechanism

The most dramatic consequence of dynamic conductance changes is **[shunting inhibition](@entry_id:148905)**. Consider an inhibitory synapse, such as one mediated by $\text{GABA}_{\text{A}}$ receptors, whose reversal potential $E_I$ is very close to the neuron's resting potential $E_L$ (e.g., $E_I \approx -75$ mV, $E_L \approx -70$ mV)  . When the neuron's membrane potential $V(t)$ is near rest, the driving force for this synapse, $(E_I - V(t))$, is very small. Consequently, opening these inhibitory channels generates very little hyperpolarizing current.

The primary effect of activating this synapse is not to pull the voltage down, but to drastically increase the total membrane conductance $g_{tot}$. This increase in conductance reduces the membrane's [input resistance](@entry_id:178645), $R_{in} = 1/g_{tot}$. According to Ohm's law, the voltage change, $\Delta V$, in response to any other coincident excitatory input current $I_{exc}$ is approximately $\Delta V = I_{exc} R_{in}$. By reducing $R_{in}$, the inhibitory synapse effectively "shunts" the excitatory current, divisively reducing its impact on the membrane potential.

For example, consider a neuron with a leak conductance $g_L = 10 \text{ nS}$. Its [input resistance](@entry_id:178645) is $R_{in} = 1/(10 \text{ nS}) = 100 \text{ M}\Omega$. If a shunting inhibitory synapse with a conductance of $g_I = 40 \text{ nS}$ is activated, the new total conductance becomes $g_{tot} = 10 + 40 = 50 \text{ nS}$. The input resistance drops to $R_{in} = 1/(50 \text{ nS}) = 20 \text{ M}\Omega$. The neuron's response to any other input current is now attenuated by a factor of 5 . This powerful, divisive gain control mechanism is entirely absent in current-based models, which can only implement [subtractive inhibition](@entry_id:1132623).

#### Driving Force Saturation and Current Reversal

The driving force term, $(E_{syn} - V(t))$, also ensures that the membrane potential has a natural ceiling. In the [conductance-based model](@entry_id:1122855), the steady-state potential $V_{\infty}$ for a constant synaptic conductance $g_s$ is a weighted average of the reversal potentials:

$$
V_{\infty} = \frac{g_L E_L + g_s E_s}{g_L + g_s}
$$

As the excitatory [synaptic conductance](@entry_id:193384) $g_s$ becomes very large ($g_s \gg g_L$), the voltage $V_{\infty}$ approaches the [synaptic reversal potential](@entry_id:911810) $E_s$. For a typical excitatory (AMPA) synapse, $E_{AMPA} \approx 0 \text{ mV}$ . No matter how strong the excitatory input, it cannot drive the membrane potential above its own [reversal potential](@entry_id:177450). This voltage-dependent saturation is a critical form of nonlinear summation. In contrast, the steady-state potential in a current-based model, $V_{\infty} = E_L + I_s/g_L$, is an unbounded linear function of the input current $I_s$, which is biophysically unrealistic .

Furthermore, the sign of the driving force determines the direction of the current. For an AMPA synapse with $E_{AMPA} = 0 \text{ mV}$ and a resting potential $V_{rest} = -65 \text{ mV}$, the driving force is large and positive ($0 - (-65) = +65 \text{ mV}$), producing a strong inward (depolarizing) current. For a GABA synapse with $E_{GABA} = -75 \text{ mV}$, the driving force is small and negative ($-75 - (-65) = -10 \text{ mV}$), producing a weak outward (hyperpolarizing) current . If the membrane potential were to be driven by other inputs to a value below $-75 \text{ mV}$, this same GABAergic synapse would become depolarizing. This state-dependent reversal of synaptic effect is a hallmark of conductance-based dynamics that is absent in the fixed-weight current-based model .

### Linearity, Superposition, and Implications for Neural Coding

The voltage dependence of conductance-based synapses also fundamentally alters the mathematical structure of the system, with important consequences for how inputs are integrated.

A **linear system** is one that obeys the principle of **superposition**: the response to a sum of inputs is equal to the sum of the responses to each input applied individually. The current-based model describes a linear system . The membrane equation, $C \frac{dV}{dt} + g_L V = g_L E_L + I_{syn}(t)$, is a linear [ordinary differential equation](@entry_id:168621). This means that the effects of multiple synaptic currents sum linearly, and the powerful toolkit of [linear systems analysis](@entry_id:166972) (e.g., calculating the response to any input via convolution with a single [impulse response function](@entry_id:137098)) can be applied.

The [conductance-based model](@entry_id:1122855), however, is **nonlinear**. The membrane equation contains terms of the form $g_j(t)V(t)$, which are products of the input ($g_j(t)$) and the state variable ($V(t)$). This structure is known as **bilinear**. Due to this nonlinearity, superposition is broken. The voltage response to the simultaneous activation of two synapses is not simply the sum of the responses to each synapse activated alone. For instance, the shunting effect described earlier is a clear example of this: the effect of an excitatory synapse is diminished in the presence of an inhibitory one, an interaction that goes beyond simple subtraction. This nonlinear integration is thought to be a critical element of neural computation, allowing neurons to perform operations like multiplication or gain control.

This nonlinearity has direct implications for experimental neuroscience. Techniques for linear [system identification](@entry_id:201290), which are used to measure a neuron's "transfer function," are only strictly valid if the system is linear. However, under experimental **[voltage clamp](@entry_id:264099)**, where the membrane potential $V(t)$ is held constant at a value $V_{hold}$, the synaptic current becomes $I_{syn}(t) = g_{syn}(t)(E_{syn} - V_{hold})$. Since $(E_{syn} - V_{hold})$ is now a constant, the measured current is directly proportional to the [synaptic conductance](@entry_id:193384). This experimental manipulation linearizes the system, allowing for the direct measurement of synaptic conductances .

### The Current-Based Model as a Formal Approximation

While the [conductance-based model](@entry_id:1122855) is more biophysically realistic, the current-based model is computationally simpler and often serves as a useful approximation. It is crucial to understand the formal conditions under which this approximation is valid.

The current-based model can be derived from the [conductance-based model](@entry_id:1122855) by linearizing the synaptic current term, $g_s(t)(E_s - V(t))$, around a fixed operating voltage, $V_0$ (e.g., the average membrane potential). If voltage fluctuations $v(t) = V(t) - V_0$ are small, we can approximate $V(t) \approx V_0$:

$$
I_{syn}(t) = g_s(t)(E_s - V(t)) \approx g_s(t)(E_s - V_0)
$$

This gives an effective current source proportional to the conductance, which is the form of a current-based model. This approximation is accurate under two key conditions :

1.  **Small Voltage Fluctuations**: The voltage deviation from the operating point must be small compared to the magnitude of the driving force at that point. That is, $|V(t) - V_0| \ll |E_s - V_0|$.
2.  **Small Synaptic Conductance**: The total [synaptic conductance](@entry_id:193384) must be much smaller than the leak conductance, $\sum g_s(t) \ll g_L$. This ensures that the effective membrane time constant is not significantly altered by synaptic activity.

We can quantify the error of this approximation. The instantaneous relative error, $\varepsilon(t)$, between the true conductance-based current and its current-based approximation is given by:

$$
\varepsilon(t) = \frac{|I_s^{\mathrm{GB}}(t) - I_s^{\mathrm{CB}}(t)|}{|I_s^{\mathrm{CB}}(t)|} = \frac{|g_s(t)(E_s - V(t)) - g_s(t)(E_s - V_0)|}{|g_s(t)(E_s - V_0)|} = \frac{|V_0 - V(t)|}{|E_s - V_0|}
$$

If the voltage deviation is bounded by $|V(t) - V_0| \le \Delta V$, then the error is bounded by:

$$
\varepsilon(t) \le \frac{\Delta V}{|E_s - V_0|}
$$

This simple expression formalizes the regime of validity. For an excitatory synapse with $E_s = 0$ mV and a neuron operating at $V_0 = -65$ mV, the driving force is large ($65$ mV). Even for a voltage fluctuation of $\Delta V = 2$ mV, the maximum [relative error](@entry_id:147538) is small: $\varepsilon_{max} = 2/65 \approx 0.031$, or about 3.1% . In this case, the current-based approximation is quite accurate. However, for a shunting inhibitory synapse with $E_s = -75$ mV, the driving force is very small ($10$ mV). The same $2$ mV fluctuation would lead to a much larger error of $2/10 = 0.2$, or 20%. This confirms that current-based models are particularly poor at capturing the dynamics of shunting inhibition.

### Practical Guidelines for Model Selection in Large-Scale Simulations

The choice between a current-based and a [conductance-based model](@entry_id:1122855) in computational neuroscience is a practical one, balancing the need for biophysical realism against computational cost, especially in large-scale network simulations. The principles discussed above provide clear criteria for making this decision .

**Use a current-based model when:**
*   **The system operates in a low-conductance state:** The total background [synaptic conductance](@entry_id:193384) is small compared to the leak conductance ($\bar{g}_{syn} \ll g_L$), and voltage fluctuations are expected to be small.
*   **Computational efficiency is paramount:** Current-based models are simpler and can sometimes permit larger integration time steps, reducing total simulation time.
*   **The scientific question does not hinge on gain modulation:** If the core phenomena being studied are not shunting inhibition, divisive gain control, or saturation near reversal potentials, the simpler model may suffice.

**Use a [conductance-based model](@entry_id:1122855) when:**
*   **The system operates in a [high-conductance state](@entry_id:1126053):** This regime is characteristic of the awake cortex, where background synaptic activity is high ($\bar{g}_{syn} \ge g_L$). Here, the modulation of membrane properties is a dominant effect.
*   **The scientific question demands biophysical realism:** To study phenomena like [divisive inhibition](@entry_id:172759), the nonlinear integration of inputs, or the detailed dynamics of [voltage-clamp](@entry_id:169621) experiments, a [conductance-based model](@entry_id:1122855) is indispensable.
*   **The computational budget is sufficient:** Conductance-based models can make the [system of differential equations](@entry_id:262944) "stiffer" by introducing a faster [effective time constant](@entry_id:201466) ($\tau_{eff} = C/g_{tot}$). Numerical stability for explicit integration methods often requires the time step $h$ to be smaller than $\tau_{eff}$, potentially increasing the overall computational load. For example, a four-fold increase in total conductance can reduce $\tau_{eff}$ from $20$ ms to $5$ ms, demanding a correspondingly smaller time step for a stable and accurate simulation .

Ultimately, the choice of synaptic model is not merely a technical detail but a core theoretical commitment. It defines the elementary computations available to the model neuron and shapes the dynamics of the entire network. A careful consideration of these principles is therefore essential for the design of any meaningful computational model of neural circuits.