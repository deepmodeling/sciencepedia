## Introduction
Neurons perform complex computations by integrating thousands of synaptic inputs across their elaborate dendritic arbors. The fundamental process underlying this integration is the transient spread of voltage: how electrical signals generated at synapses travel, decay, and summate as they propagate towards the soma. To understand neuronal function, we must move beyond a qualitative picture and develop a quantitative framework that links a neuron's intricate morphology to its electrical behavior. This article provides that foundation by exploring the passive cable model, a cornerstone of computational neuroscience.

This article is structured to build a comprehensive understanding from the ground up. In the first chapter, **Principles and Mechanisms**, we will derive the governing [passive cable equation](@entry_id:1129411) from first principles, uncovering the key physical scales of time and space that dictate [signal propagation](@entry_id:165148). In the second chapter, **Applications and Interdisciplinary Connections**, we will use this framework to explore the computational roles of dendrites, their involvement in [synaptic plasticity](@entry_id:137631), and the crucial dialogue between theory and experimental [neurophysiology](@entry_id:140555). Finally, the **Hands-On Practices** section offers practical exercises to simulate and analyze cable properties. Together, these sections will illuminate how the biophysical properties of dendrites give rise to the very first steps of computation in the brain.

## Principles and Mechanisms

The transient spread of voltage in dendrites is governed by the interplay between the cable-like properties of the dendritic structure and the electrical characteristics of the [neuronal membrane](@entry_id:182072). Understanding this process is fundamental to deciphering how synaptic inputs are integrated to shape neuronal output. This chapter deconstructs the passive cable model, deriving its governing equation from first principles and exploring its solutions to reveal the core mechanisms of subthreshold [signal propagation](@entry_id:165148).

### The Foundational Model: The Passive Cable Equation

We begin by modeling a segment of a dendrite as a uniform cylinder. The electrical behavior of this structure can be described by considering the flow of current both along its axis (axially) and across its membrane (transmembranally). The derivation of the governing equation, known as the **[passive cable equation](@entry_id:1129411)**, rests on three pillars: Ohm's law, the constitutive relation for a capacitor, and the principle of [conservation of charge](@entry_id:264158).

Let us define the essential parameters. We consider a cylinder of radius $a$. The cytoplasm has a specific intracellular resistivity $r_i$. The membrane itself has a [specific membrane capacitance](@entry_id:177788) per unit area $c_m$ and a specific membrane leak conductance per unit area $g_m$. From these, we derive parameters per unit length of the cable:
- **Axial resistance per unit length ($r_a$)**: The resistance to current flowing along the cytoplasm. It is given by $r_a = r_i / (\pi a^2)$. Note that a thicker dendrite (larger $a$) has a lower axial resistance.
- **Membrane conductance per unit length ($g_m^\ell$)**: The conductance for current leaking out across the membrane. It is given by $g_m^\ell = g_m \cdot (2\pi a)$.
- **Membrane capacitance per unit length ($c_m^\ell$)**: The capacitance of the membrane. It is given by $c_m^\ell = c_m \cdot (2\pi a)$.

Now, consider the currents. Let $V(x, t)$ be the intracellular potential at position $x$ and time $t$, relative to the extracellular space, which is assumed to be at a ground potential of zero. The axial current, $i_a(x, t)$, is driven by the spatial gradient of this potential, as described by Ohm's law:
$i_a(x, t) = -\frac{1}{r_a} \frac{\partial V}{\partial x}$

The transmembrane current per unit length, $i_m(x, t)$, has two components in a passive model: a leak current through ionic channels, $i_\ell$, and a [capacitive current](@entry_id:272835), $i_c$, which charges or discharges the membrane.
- The **leak current** is assumed to be ohmic, proportional to the driving force $(V - E_L)$, where $E_L$ is the leak [reversal potential](@entry_id:177450). Per unit length, this is $i_\ell = g_m^\ell (V - E_L)$.
- The **[capacitive current](@entry_id:272835)** is proportional to the rate of change of the voltage, $i_c = c_m^\ell \frac{\partial V}{\partial t}$.

The total outward transmembrane current is the sum of these two: $i_m = i_c + i_\ell$. The principle of [conservation of charge](@entry_id:264158) requires that any change in axial current along an infinitesimal segment must be balanced by the current leaving through the membrane. This gives the continuity relation: $-\frac{\partial i_a}{\partial x} = i_m$.

Combining these relationships, we first find an expression for the transmembrane current from the axial current:
$i_m = -\frac{\partial}{\partial x} \left(-\frac{1}{r_a} \frac{\partial V}{\partial x}\right) = \frac{1}{r_a} \frac{\partial^2 V}{\partial x^2}$

This provides a profound physical interpretation of the voltage's second spatial derivative, or **curvature**: a [positive curvature](@entry_id:269220) ($\partial^2 V/\partial x^2 > 0$) at a point means the voltage profile is concave up (like a local minimum), which implies a [net convergence](@entry_id:150788) of axial current into that location, forcing current to flow outward across the membrane ($i_m > 0$). Conversely, a negative curvature ($\partial^2 V/\partial x^2  0$, a [local maximum](@entry_id:137813)) implies a divergence of axial current, which must be supplied by an inward transmembrane current ($i_m  0$) .

Equating our two expressions for $i_m$ and including an optional external injected current per unit length, $i_{inj}(x,t)$ (positive inward), we arrive at the [passive cable equation](@entry_id:1129411):
$\frac{1}{r_a} \frac{\partial^2 V}{\partial x^2} = c_m^\ell \frac{\partial V}{\partial t} + g_m^\ell (V - E_L) - i_{inj}(x,t)$

Rearranging for the time derivative, we get the [canonical form](@entry_id:140237):
$c_m^\ell \frac{\partial V}{\partial t} = \frac{1}{r_a} \frac{\partial^2 V}{\partial x^2} - g_m^\ell (V - E_L) + i_{inj}(x,t)$

The term $-g_m^\ell (V - E_L)$ represents a restorative force, always acting to pull the voltage back towards the leak [reversal potential](@entry_id:177450) $E_L$. This term is inherently dissipative; the power lost to heat per unit length through the leak resistance is proportional to $(V-E_L)^2$ .

A critical property of this equation is its **linearity**. Because the axial, capacitive, and leak currents are all described by linear relationships with respect to voltage and its derivatives, the governing PDE is linear. However, the presence of the constant $E_L$ term makes the equation for $V$ technically *affine*. This is easily handled by defining a new variable, $u(x,t) = V(x,t) - E_L$, which represents the deviation from the resting potential. The equation for $u$ becomes a true homogeneous linear PDE (in the absence of injection), allowing the powerful **[principle of superposition](@entry_id:148082)** to be applied. This means that the response to multiple synaptic inputs is simply the sum of the responses to each input individually, provided the underlying membrane and axial properties do not depend on voltage. This linearity holds even if the properties vary in time or space, as long as they are not functions of the voltage itself .

### Characteristic Scales: Time Constant and Space Constant

The parameters of the cable equation can be combined into two characteristic scales that dictate the [spatiotemporal dynamics](@entry_id:201628) of voltage: the [membrane time constant](@entry_id:168069), $\tau$, and the [electrotonic length constant](@entry_id:196410), $\lambda$.

#### The Membrane Time Constant, $\tau$

To understand the intrinsic temporal properties of the membrane, we can consider a spatially uniform patch where $\partial^2 V / \partial x^2 = 0$. This is equivalent to an isopotential RC circuit. If we inject a step of current density $i_0$ starting at $t=0$, the [cable equation](@entry_id:263701) simplifies to an [ordinary differential equation](@entry_id:168621):
$c_m^\ell \frac{du}{dt} = -g_m^\ell u + i_{inj}$

Dividing by $g_m^\ell$ and defining the **membrane time constant** $\tau = c_m^\ell / g_m^\ell$, we get:
$\tau \frac{du}{dt} + u = \frac{i_{inj}}{g_m^\ell}$

For a step current injection and an initial condition $u(0)=0$, the solution is an exponential rise to a steady-state value :
$u(t) = \frac{i_{inj}}{g_m^\ell} \left(1 - \exp\left(-\frac{t}{\tau}\right)\right)$

The time constant $\tau$ sets the [characteristic timescale](@entry_id:276738) for the local membrane to charge and discharge. It determines the temporal window over which synaptic inputs can be integrated. Importantly, if we expand the definitions of the per-unit-length parameters, we find $\tau = (c_m \cdot 2\pi a) / (g_m \cdot 2\pi a) = c_m/g_m$. This shows that $\tau$ is an intrinsic property of the membrane itself, independent of the dendrite's geometry, such as its radius .

#### The Electrotonic Length Constant, $\lambda$

To isolate the spatial properties, we consider the steady-state condition where $\partial V/\partial t = 0$. In this case, the [capacitive current](@entry_id:272835) vanishes, and the cable equation balances the change in axial current with the steady leak current. For a source-free region of the cable, this simplifies to:
$\frac{1}{r_a} \frac{d^2 u}{dx^2} - g_m^\ell u = 0$

We can rewrite this as:
$\frac{d^2 u}{dx^2} = (r_a g_m^\ell) u$

This equation describes exponential decay. We define the **[electrotonic length constant](@entry_id:196410)** (or [space constant](@entry_id:193491)), $\lambda$, such that the equation takes the [canonical form](@entry_id:140237) $d^2u/dx^2 = u/\lambda^2$. By comparison, we find:
$\lambda = \sqrt{\frac{1}{r_a g_m^\ell}}$

This constant $\lambda$ represents the distance over which a steady-state voltage perturbation decays to $1/e$ (approximately 37%) of its original value . Unlike $\tau$, the [space constant](@entry_id:193491) $\lambda$ explicitly depends on the dendrite's geometry. Substituting the definitions of $r_a$ and $g_m^\ell$:
$\lambda = \sqrt{\frac{1}{(r_i / \pi a^2)(g_m \cdot 2\pi a)}} = \sqrt{\frac{a}{2 r_i g_m}}$

This reveals that $\lambda$ is proportional to the square root of the radius, $\lambda \propto \sqrt{a}$ . A thicker dendrite provides a wider path for axial current (lower $r_a$), allowing voltage to propagate farther before leaking out.

### The Universal Cable: Normalization and Similarity

The existence of these natural scales, $\tau$ and $\lambda$, suggests a powerful simplification. By measuring distance in units of $\lambda$ and time in units of $\tau$, we can remove all physical parameters from the [cable equation](@entry_id:263701). Let us define dimensionless position $X = x/\lambda$ and dimensionless time $T = t/\tau$. Using the chain rule to transform the derivatives, the [passive cable equation](@entry_id:1129411) for the deviation voltage $u$ becomes :
$\frac{\partial u}{\partial T} = \frac{\partial^2 u}{\partial X^2} - u$

This normalized equation is universal; it has no free parameters. This means that the behavior of any passive dendritic cable, regardless of its specific radius or membrane properties, is fundamentally the same. The voltage response of one dendrite is simply a spatially and temporally scaled version of the response of another. This concept of **similarity** is profound, as it allows us to study one canonical problem to understand the behavior of all passive cables. The parameters $\lambda$ and $\tau$ act as the natural rulers for space and time for any specific cable.

### Transient Voltage Spread: The Green's Function

We now turn to the full transient problem: how does voltage evolve in both space and time following a brief, localized input? The answer is encapsulated in the **Green's function**, which is the solution to the [cable equation](@entry_id:263701) for an instantaneous point injection of charge (a Dirac delta function in space and time). This function represents the fundamental building block of the response; by the [principle of superposition](@entry_id:148082), the response to any arbitrary input can be found by convolving that input with the Green's function.

To find this solution, we rewrite the [cable equation](@entry_id:263701) by dividing by $\tau$:
$\frac{\partial u}{\partial t} = \frac{\lambda^2}{\tau} \frac{\partial^2 u}{\partial x^2} - \frac{1}{\tau} u$

Here, we can identify a new crucial parameter, the **effective diffusion constant**, $D = \lambda^2/\tau$ . This gives the equation the form of a reaction-diffusion equation:
$\frac{\partial u}{\partial t} = D \frac{\partial^2 u}{\partial x^2} - \frac{1}{\tau} u$

The solution to this equation for an initial condition $u(x,0) = Q_0 \delta(x)$ (representing a total charge $Q_0$ injected at $x=0, t=0$) can be found using Fourier transform methods . The result is the Green's function, $G(x,t)$:
$G(x,t) = \frac{Q_0}{\sqrt{4\pi D t}} \exp\left(-\frac{x^2}{4Dt}\right) \exp\left(-\frac{t}{\tau}\right)$

This beautiful solution reveals that the [transient voltage spread](@entry_id:1133331) is a product of two distinct physical processes:
1.  **Diffusion**: The term $\frac{1}{\sqrt{4\pi D t}} \exp\left(-\frac{x^2}{4Dt}\right)$ is the solution to the pure diffusion equation. It describes how the charge, once injected, spreads out along the cable. The distribution is a Gaussian function of space whose variance, $\sigma^2 = 2Dt$, grows linearly with time. This spreading causes the amplitude of the voltage peak to decrease as $1/\sqrt{t}$.
2.  **Decay**: The term $\exp(-t/\tau)$ describes the uniform decay of voltage over the entire cable due to the leak conductance of the membrane. This process drains charge out of the cable, causing the total integrated voltage to decrease exponentially with the time constant $\tau$.

Together, these processes ensure that a localized synaptic potential will become smaller, slower to rise, and broader in space as it propagates along a dendrite.

### Practical Considerations: Boundary Conditions and Morphology

Real dendrites are finite structures with terminations and [branch points](@entry_id:166575). To model them accurately, we must impose **boundary conditions** at their ends. Two idealized cases are particularly important :
- **Sealed End**: This models an abrupt physical termination of a dendrite where no more cytoplasm exists. No axial current can flow past this point, so $i_a = 0$. Since $i_a \propto \partial V/\partial x$, this corresponds to a **Neumann boundary condition**: $\frac{\partial V}{\partial x} = 0$.
- **Killed End**: This models a termination that is electrically connected to a very large compartment, such as the soma, which can effectively clamp the voltage at the resting potential. This corresponds to a **Dirichlet boundary condition**: $V = E_L$ (or $u=0$).

The morphology of the dendrite has a profound impact on transient signaling. As we saw, a dendrite's radius $a$ strongly influences its electrical properties. While the membrane time constant $\tau$ is independent of radius, the space constant $\lambda$ scales with $\sqrt{a}$. Most critically for transient signals, the effective diffusion constant $D = \lambda^2/\tau$ depends linearly on the radius:
$D = \frac{\lambda^2}{\tau} = \frac{a/(2 r_i g_m)}{c_m/g_m} = \frac{a}{2 r_i c_m}$

This implies that voltage signals propagate not only farther but also significantly *faster* down thicker dendrites. Consider a voltage step applied at one end of two dendrites, one with radius $a$ and another with radius $4a$. At a fixed distance $x_0$, the signal in the thicker dendrite will arrive much earlier (the effective latency scales as $1/D \propto 1/a$), rise more rapidly, and reach a larger [steady-state amplitude](@entry_id:175458) . This makes thick dendritic trunks act as high-speed, high-fidelity information highways for transmitting synaptic information to the soma.

### The Limits of the Passive Model

The passive cable model, for all its power, relies on key simplifying assumptions. It is crucial to understand their justification and limitations. The model treats the [specific membrane capacitance](@entry_id:177788) $c_m$ and leak conductance $g_m$ as constants .
- The assumption of a constant $c_m \approx 1 \mu\text{F/cm}^2$ is physically well-grounded. The lipid bilayer acts as a dielectric whose thickness and permittivity are largely independent of the physiological voltage range.
- The assumption of a constant $g_m$ is an approximation. It models the net effect of various ion channels open at rest. While the current-voltage relationship of any single channel is nonlinear, for small deviations around the resting potential, a [linear approximation](@entry_id:146101) (Ohm's law) is valid.

The most significant simplification is the omission of **[voltage-gated ion channels](@entry_id:175526)**, which are ubiquitous in real dendrites. These channels endow the membrane with a conductance that changes dynamically with voltage, rendering the system nonlinear. While a full treatment of such [active dendrites](@entry_id:193434) is beyond the scope of this chapter, the framework we have developed provides the necessary foundation. For small voltage perturbations around a stable resting state, even an active membrane can be analyzed using a **linearized model**. This involves approximating the nonlinear [gating dynamics](@entry_id:1125526) with a linear system. An important consequence of this linearization is that the effective membrane admittance becomes frequency-dependent, introducing "memory" into the system that can give rise to complex phenomena like [subthreshold oscillations](@entry_id:198928) and resonance, properties that are absent in the purely passive model . Thus, the [passive cable equation](@entry_id:1129411) serves as the essential, foundational scaffold upon which more complex and biologically realistic models of [dendritic computation](@entry_id:154049) are built.