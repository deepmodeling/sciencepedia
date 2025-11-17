## Introduction
The ability of a neuron to process information is fundamentally tied to its electrical response to incoming signals. Central to this response are two key properties: membrane resistance and [input resistance](@entry_id:178645), which dictate how a neuron converts synaptic or injected currents into voltage changes. This article addresses the challenge of quantifying these properties, which are shaped by a complex interplay between a neuron's physical structure, its size, and the biophysical characteristics of its ion channels. Over the next three chapters, you will gain a comprehensive understanding of this topic. The "Principles and Mechanisms" chapter will establish the biophysical foundations, modeling the neuron from a simple RC circuit to a complex, non-linear cable. The "Applications and Interdisciplinary Connections" chapter will explore how these principles govern everything from [synaptic integration](@entry_id:149097) to the organization of entire motor systems. Finally, the "Hands-On Practices" section will provide practical problems to solidify your computational and theoretical skills. We begin by dissecting the core principles that govern how a neuron resists the flow of current.

## Principles and Mechanisms

In [cellular neuroscience](@entry_id:176725), understanding how a neuron responds to electrical input is fundamental. The concepts of [membrane resistance](@entry_id:174729) and [input resistance](@entry_id:178645) are central to this understanding, providing a framework to quantify and predict the voltage changes that arise from current flow across the [neuronal membrane](@entry_id:182072). This chapter elucidates the principles governing these resistive properties, starting from the intrinsic characteristics of the lipid bilayer and its embedded channels, and progressing to the integrated behavior of geometrically complex and biophysically non-linear neurons.

### The Membrane as a Resistor-Capacitor Circuit

At its most basic level, the [neuronal membrane](@entry_id:182072) is a physical structure separating two conductive [aqueous solutions](@entry_id:145101): the intracellular cytoplasm and the extracellular fluid. This structure gives rise to two fundamental passive electrical properties: capacitance and resistance.

The [lipid bilayer](@entry_id:136413) itself is a very thin insulating sheet. Like any physical capacitor, it can store charge. An accumulation of positive ions on one side of the membrane and negative ions on the other creates an electric field within the dielectric core of the bilayer. The ability to store charge is quantified by the **[specific membrane capacitance](@entry_id:177788)**, $C_m$, typically measured in microfarads per square centimeter ($\mu\mathrm{F}/\mathrm{cm}^2$). A changing transmembrane voltage, $V_m$, results in a flow of **[capacitive current](@entry_id:272835)**, also known as [displacement current](@entry_id:190231), given by $I_C = C_m (\mathrm{d}V_m/\mathrm{d}t)$. This current does not involve charge carriers crossing the membrane but rather reflects the charging or discharging of the membrane capacitor.

Embedded within this insulating bilayer are [ion channels](@entry_id:144262), which are proteinaceous pores that permit the passage of specific ions. These channels constitute a conductive pathway across the membrane. The flow of ions through these channels is a **[conduction current](@entry_id:265343)**, often called [ionic current](@entry_id:175879). At steady state, or for small perturbations around the resting potential, this flow can be approximated by Ohm's law. The property of the membrane that opposes this [ionic current](@entry_id:175879) is the **[specific membrane resistance](@entry_id:166665)**, denoted $R_m$ and measured in units of ohm-centimeters squared ($\Omega\cdot\mathrm{cm}^2$). It is an [intrinsic property](@entry_id:273674) of the membrane, reflecting the density and [single-channel conductance](@entry_id:197913) of the ion channels that are open at rest, collectively known as **[leak channels](@entry_id:200192)**.

From first principles, the total current crossing a patch of membrane is the sum of the conduction current and the [displacement current](@entry_id:190231). Because both phenomena—the charging of the dielectric and the flow of ions through pores—occur across the same two electrical points (the intracellular and extracellular compartments), they are modeled as being in parallel. Therefore, a small patch of [neuronal membrane](@entry_id:182072) is fundamentally represented by a resistor in parallel with a capacitor (an RC circuit). [@problem_id:2724487] The total current density, $J_{total}$, across the membrane is:

$$ J_{total} = \frac{V_m}{R_m} + C_m \frac{\mathrm{d}V_m}{\mathrm{d}t} $$

For much of our analysis of resistance, we focus on the **steady-state** response to a direct current (DC) injection. At steady state, the voltage is no longer changing, so $\mathrm{d}V_m/\mathrm{d}t = 0$. Consequently, the [capacitive current](@entry_id:272835) vanishes, and all injected current must flow through the resistive pathways. [@problem_id:2724487] [@problem_id:2724502] This simplifies the analysis to purely resistive circuits.

In many contexts, it is more convenient to work with conductance, the reciprocal of resistance. The **specific [membrane conductance](@entry_id:166663)**, $g_m$, is defined as $g_m = 1/R_m$ and has units of Siemens per square centimeter ($\mathrm{S}/\mathrm{cm}^2$). Since different populations of [leak channels](@entry_id:200192) provide independent parallel pathways for ion flow, their conductances add. If a membrane contains two distinct populations of [leak channels](@entry_id:200192) with uniform conductance densities $g_{L1}$ and $g_{L2}$, the total specific [membrane conductance](@entry_id:166663) is simply their sum: $g_m = g_{L1} + g_{L2}$. [@problem_id:2724467] This principle of additive parallel conductances is foundational to understanding how changes in channel expression or function alter a neuron's electrical properties. [@problem_id:2724511]

### Input Resistance of the Isopotential Neuron

While $R_m$ is an [intrinsic property](@entry_id:273674) of a unit area of membrane, neurophysiologists typically measure a whole-cell property called the **input resistance**, $R_{in}$. This is an operational quantity defined as the ratio of the steady-state voltage change ($\Delta V$) at a point to the steady DC current ($I$) injected at that same point:

$$ R_{in} = \frac{\Delta V}{I} $$

$R_{in}$ is measured in Ohms ($\Omega$) and represents the total opposition of the neuron to a current injection as seen from the recording site. It is a lumped parameter that depends on both the intrinsic [specific membrane resistance](@entry_id:166665) and the neuron's overall size and shape. [@problem_id:2724515]

To understand the relationship between $R_m$ and $R_{in}$, we begin with the simplest possible model: an idealized, small, spherical neuron that is **isopotential**. The isopotential assumption means that at any instant, the voltage is uniform across the entire surface of the membrane. This is a reasonable approximation for a compact cell soma without extensive processes.

In an isopotential cell, every small patch of the membrane is electrically in parallel with every other patch. For electrical components in parallel, their conductances sum to give the total conductance. The total conductance of the entire cell, known as the **input conductance** ($G_{in} = 1/R_{in}$), is the integral of the specific [membrane conductance](@entry_id:166663) $g_m$ over the total surface area $A$. Assuming $g_m$ is uniform across the surface:

$$ G_{in} = \int_A g_m \, dA = g_m \int_A dA = g_m A $$

Since $g_m = 1/R_m$, we can express the input resistance as:

$$ R_{in} = \frac{1}{G_{in}} = \frac{1}{g_m A} = \frac{R_m}{A} $$

This crucial equation states that for a simple isopotential cell, the [input resistance](@entry_id:178645) is inversely proportional to its total surface area. A larger cell, having more membrane area and thus more [leak channels](@entry_id:200192) in parallel, presents more pathways for current to escape, resulting in a lower overall input resistance. [@problem_id:2724470]

For example, consider a spherical neuron with a radius $a=10\,\mu\mathrm{m}$ and a typical [specific membrane resistance](@entry_id:166665) $R_m = 20\,\mathrm{k}\Omega\cdot\mathrm{cm}^2$. The surface area is $A = 4\pi a^2 = 4\pi (10^{-3}\,\mathrm{cm})^2 \approx 1.26 \times 10^{-5}\,\mathrm{cm}^2$. The input resistance would be:

$$ R_{in} = \frac{20 \times 10^3\,\Omega\cdot\mathrm{cm}^2}{1.26 \times 10^{-5}\,\mathrm{cm}^2} \approx 1.59 \times 10^9\,\Omega = 1.59\,\mathrm{G}\Omega $$

The simple scaling relationship $R_{in} = R_m/A$ holds only under a strict set of assumptions [@problem_id:2724502]:
1.  **Isopotentiality:** The cell must be electrically compact, with no significant voltage gradients.
2.  **Passive and Uniform Membrane:** The [specific membrane resistance](@entry_id:166665) $R_m$ must be uniform across the entire surface and must not change with voltage (i.e., the membrane is linear or "Ohmic").
3.  **Steady-State DC Measurement:** The measurement must be made after all capacitive currents have decayed to zero.
4.  **No Series Resistance:** The access resistance of the recording electrode must be negligible.
5.  **No Parallel Shunts:** The cell must be electrically isolated, with no other current pathways such as [gap junctions](@entry_id:143226).

The shape of the cell (e.g., spherical vs. cubical) does not matter as long as the isopotential condition holds; only the total surface area is relevant.

### The Impact of Neuronal Morphology: Non-Isopotential Neurons

The assumption of isopotentiality breaks down for most real neurons, which possess extensive dendritic trees and long axons. Current injected into the soma must spread through the cytoplasm of these processes. The cytoplasm, while a conductor, has a finite resistance. This property is quantified by the **axial [resistivity](@entry_id:266481)**, $R_i$ (or $\rho_i$), an intrinsic material property of the cytoplasm with units of $\Omega\cdot\mathrm{m}$. [@problem_id:2724515]

Due to this [axial resistance](@entry_id:177656), voltage is not uniform throughout the neuron. As current flows from the soma down a dendrite, there is a voltage drop along the dendrite's length. This passive voltage decay with distance is known as **[electrotonic decay](@entry_id:183749)**. Consequently, a patch of membrane located far out on a dendrite will experience a smaller voltage change than a patch on the soma for the same somatic current injection.

This has a profound consequence: distant membrane patches contribute less to the overall input conductance of the neuron as measured at the soma. The [input resistance](@entry_id:178645) is no longer determined by the simple sum of all conductances over the total area. Instead, it reflects a weighted sum, where the contribution of each membrane patch is discounted by its electrotonic distance from the injection site. [@problem_id:2724504] As a result, for a non-isopotential neuron, the simple formula $R_{in} = R_m / A_{total}$ is incorrect; the true input resistance will always be greater than the value predicted by this naive formula. This also means that $R_{in}$ becomes a **point-dependent property**; its value changes depending on where on the neuron it is measured (e.g., soma vs. distal dendrite).

This principle can be rigorously demonstrated using **[cable theory](@entry_id:177609)**. Consider a model neuron consisting of a spherical soma attached to a single cylindrical dendrite of length $L$ and diameter $d$. The input conductance at the soma, $G_{in}$, is the sum of the soma's own [membrane conductance](@entry_id:166663), $G_{soma}$, and the input conductance of the attached dendrite, $G_{dend,in}$. From a detailed derivation based on the passive [cable equation](@entry_id:263701), the input conductance of a finite dendrite with a sealed end is found to be:

$$ G_{dend,in} = \frac{\pi d \lambda}{R_m} \tanh\left(\frac{L}{\lambda}\right) $$

Here, $\lambda = \sqrt{d R_m / (4 R_i)}$ is the **[space constant](@entry_id:193491)** of the dendrite, which represents the characteristic distance over which voltage decays. The total somatic input resistance is therefore: [@problem_id:2724498]

$$ R_{in} = \left( G_{soma} + G_{dend,in} \right)^{-1} = \left( \frac{A_{soma}}{R_m} + \frac{\pi d \lambda}{R_m} \tanh\left(\frac{L}{\lambda}\right) \right)^{-1} $$

This equation elegantly captures the breakdown of simple [geometric scaling](@entry_id:272350). The effective electrical "area" contributed by the dendrite is not its geometric area ($\pi d L$) but rather an electrotonically limited area, $\pi d \lambda \tanh(L/\lambda)$. For a very short dendrite ($L \ll \lambda$), $\tanh(L/\lambda) \approx L/\lambda$, and the dendritic contribution approaches the isopotential case, $(\pi d L)/R_m$. For a very long dendrite ($L \gg \lambda$), $\tanh(L/\lambda) \approx 1$, and the dendritic contribution becomes constant, $(\pi d \lambda)/R_m$, regardless of its further physical length.

### The Impact of Non-Linearity: Voltage-Dependent Resistance

Our discussion so far has assumed a passive, linear membrane where $R_m$ is constant. However, real neurons are endowed with a rich variety of [voltage-gated ion channels](@entry_id:175526), which cause the membrane's current-voltage (I-V) relationship to be non-linear.

For a non-linear I-V curve, we must distinguish between two types of conductance [@problem_id:2724449]:
1.  **Chord Conductance ($g_{chord}$):** This is the ratio of the total current at a given voltage $V$ to the total driving force $(V - E_{rev})$, where $E_{rev}$ is the [reversal potential](@entry_id:177450) for that current.
    $$ g_{chord} = \frac{I(V)}{V - E_{rev}} $$
    Geometrically, this is the slope of the line (the "chord") connecting the reversal potential on the voltage axis to the point $(V, I(V))$ on the I-V curve.

2.  **Slope Conductance ($g_{slope}$):** This is the derivative of the I-V curve at a specific voltage $V$.
    $$ g_{slope} = \frac{\mathrm{d}I}{\mathrm{d}V} $$
    Geometrically, this is the slope of the tangent to the I-V curve at the point $(V, I(V))$.

The small-signal [input resistance](@entry_id:178645), $R_{in}$, which describes the neuron's response to very small current perturbations around a steady holding potential, is determined by the **slope conductance**. Specifically, the total [input resistance](@entry_id:178645) is the reciprocal of the sum of the slope conductances of all [ionic currents](@entry_id:170309) present in the membrane:

$$ R_{in}(V) = \frac{1}{\sum_j g_{slope, j}(V)} = \left( \sum_j \frac{\mathrm{d}I_j}{\mathrm{d}V} \right)^{-1} $$

A powerful physiological example of this principle is the effect of the **inward-rectifier potassium current** ($I_{K1}$) [@problem_id:2724500]. These channels are highly conductive at potentials near and negative to the potassium reversal potential ($E_K$), but their conductance decreases sharply upon [depolarization](@entry_id:156483). This "inward [rectification](@entry_id:197363)" is caused by [voltage-dependent block](@entry_id:177221) of the channel pore by intracellular polyamines and magnesium ions.

The slope conductance of $I_{K1}$ can be found by applying the [product rule](@entry_id:144424) to its definition, $I_{K1}(V) = g_{K1}(V)(V-E_K)$:

$$ \frac{\mathrm{d}I_{K1}}{\mathrm{d}V} = g_{K1}(V) + (V-E_K) \frac{\mathrm{d}g_{K1}}{\mathrm{d}V} $$

Because $g_{K1}(V)$ decreases as $V$ increases (i.e., $\mathrm{d}g_{K1}/\mathrm{d}V$ is negative), the second term is negative for voltages positive to $E_K$. Upon sufficient depolarization, this negative term can overwhelm the positive $g_{K1}(V)$ term, causing the slope conductance of $I_{K1}$ to become very small or even negative.

Consider a neuron with a passive leak ($g_L$) and an inward [rectifier](@entry_id:265678) ($I_{K1}$). Its total [input resistance](@entry_id:178645) is:

$$ R_{in}(V) = \left( g_L + \frac{\mathrm{d}I_{K1}}{\mathrm{d}V} \right)^{-1} $$

At hyperpolarized potentials near $E_K$, $\mathrm{d}I_{K1}/\mathrm{d}V$ is large and positive, making the total conductance high and $R_{in}$ low. This helps to clamp the resting membrane potential near $E_K$. As the cell is depolarized, $\mathrm{d}I_{K1}/\mathrm{d}V$ decreases dramatically. This reduction in total slope conductance causes a significant *increase* in the [input resistance](@entry_id:178645) $R_{in}$. For example, depolarizing a model cell from $-80\,\mathrm{mV}$ to $-60\,\mathrm{mV}$ can cause its input resistance to increase more than tenfold, from $\sim 46\,\mathrm{M\Omega}$ to $\sim 485\,\mathrm{M\Omega}$. This voltage-dependent amplification of resistance means that a small depolarizing current injected at a more depolarized potential can produce a much larger voltage response, a key mechanism that contributes to [neuronal excitability](@entry_id:153071) and the generation of action potentials.