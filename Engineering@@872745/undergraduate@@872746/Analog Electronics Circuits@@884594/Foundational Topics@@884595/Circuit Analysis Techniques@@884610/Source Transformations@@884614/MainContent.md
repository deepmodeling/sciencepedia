## Introduction
In the realm of [circuit analysis](@entry_id:261116), engineers are constantly seeking methods to simplify [complex networks](@entry_id:261695) into more manageable forms. Source transformation stands out as a fundamental and powerful technique that achieves precisely this. It provides a systematic procedure for converting a practical voltage source model into an equivalent practical [current source](@entry_id:275668) model, and vice versa, without altering the behavior of the external circuit. This equivalence, rooted in the duality of Thévenin's and Norton's theorems, is a cornerstone for simplifying analysis, reducing the number of equations to be solved, and gaining deeper insight into circuit behavior. This article will guide you through the theory and practice of this indispensable tool.

The first chapter, "Principles and Mechanisms," will lay the theoretical foundation, explaining the core equivalence and extending it from simple DC resistors to AC impedances and s-domain representations, including circuits with [dependent sources](@entry_id:267114). Next, "Applications and Interdisciplinary Connections" will demonstrate the technique's practical utility in modeling real-world devices, from sensors to amplifiers, and reveal its conceptual parallels in other scientific fields like control theory and signal processing. Finally, the "Hands-On Practices" section will solidify your understanding through a series of guided problems, allowing you to apply [source transformation](@entry_id:264552) to concrete circuit challenges.

## Principles and Mechanisms

In the analysis of linear electronic circuits, one of the most versatile and powerful tools at our disposal is the principle of **[source transformation](@entry_id:264552)**. This technique allows us to replace a voltage source in series with an impedance with an equivalent [current source](@entry_id:275668) in parallel with the same impedance, and vice versa, without altering the behavior of the rest of the circuit. This chapter will elucidate the fundamental principles of [source transformation](@entry_id:264552), extend its application from simple DC circuits to complex AC and transient scenarios, and explore its utility in simplifying [circuit analysis](@entry_id:261116), including those with dependent and non-linear elements.

### The Fundamental Equivalence

The foundation of [source transformation](@entry_id:264552) lies in the **Thévenin and Norton [equivalent circuits](@entry_id:274110)**. Thévenin's theorem states that any linear, two-terminal electrical network can be replaced by an equivalent circuit consisting of an [ideal voltage source](@entry_id:276609) $V_{Th}$ in series with an equivalent impedance $Z_{Th}$. Dually, Norton's theorem states that the same network can be replaced by an [ideal current source](@entry_id:272249) $I_N$ in parallel with an equivalent impedance $Z_N$.

For these two [equivalent circuits](@entry_id:274110) to be indistinguishable from the outside, they must exhibit the exact same voltage-current ($V-I$) relationship at their terminals for any load connected to them. We can establish the relationship between the Thévenin and Norton parameters by examining two specific conditions: the [open-circuit voltage](@entry_id:270130) ($V_{oc}$, where the terminal current is zero) and the short-circuit current ($I_{sc}$, where the terminal voltage is zero).

For a Thévenin circuit, the [open-circuit voltage](@entry_id:270130) is simply $V_{oc} = V_{Th}$, and the short-circuit current is $I_{sc} = V_{Th} / Z_{Th}$.
For a Norton circuit, the [open-circuit voltage](@entry_id:270130) is $V_{oc} = I_N Z_N$, and the short-circuit current is $I_{sc} = I_N$.

By equating these corresponding values, we derive the rules for [source transformation](@entry_id:264552):
1.  The equivalent impedances are identical: $Z_{Th} = Z_N$.
2.  The source values are related by Ohm's Law: $V_{Th} = I_N Z_N$ and $I_N = V_{Th} / Z_{Th}$.

Let us consider a practical, non-ideal DC current source, which is commonly modeled as an [ideal current source](@entry_id:272249) $I_s$ in parallel with a finite [internal resistance](@entry_id:268117) $R_s$ [@problem_id:1334093]. This is, by definition, a Norton equivalent circuit where $I_N = I_s$ and $R_N = R_s$. To convert this to its equivalent series voltage source model (a Thévenin equivalent), we apply the transformation rules. The [equivalent resistance](@entry_id:264704) is unchanged: $R_{eq} = R_s$. The equivalent voltage is found using the relationship $V_{eq} = I_N R_N$, which gives $V_{eq} = I_s R_s$. Thus, a current source $I_s$ in parallel with $R_s$ is externally indistinguishable from a voltage source of value $I_s R_s$ in series with the same resistance $R_s$. This fundamental transformation is the cornerstone of the technique.

### Generalization to AC and s-Domain Circuits

The power of [source transformation](@entry_id:264552) is that its principles are not confined to DC circuits with simple resistors. The method seamlessly extends to alternating current (AC) circuits analyzed in the [phasor](@entry_id:273795) domain and to general linear circuits analyzed in the Laplace or s-domain. In these domains, resistance $R$ is replaced by the more general concept of **impedance** $Z(j\omega)$ or $Z(s)$, and DC source values are replaced by [phasors](@entry_id:270266) or [s-domain](@entry_id:260604) functions.

Consider a signal generator modeled as an ideal sinusoidal voltage source $v_s(t) = V_m \cos(\omega t)$ in series with an inductor $L$ [@problem_id:1334063]. In the phasor domain, this is a Thévenin equivalent circuit with a voltage [phasor](@entry_id:273795) $\mathbf{V}_{Th} = V_m$ and a series impedance $Z_{Th} = j\omega L$. To find the Norton equivalent, we apply the same rules. The Norton impedance is identical to the Thévenin impedance:
$$ Z_N = Z_{Th} = j\omega L $$
The Norton current phasor $\mathbf{I}_N$ is found by dividing the Thévenin voltage phasor by the Thévenin impedance:
$$ \mathbf{I}_N = \frac{\mathbf{V}_{Th}}{Z_{Th}} = \frac{V_m}{j\omega L} = -j\frac{V_m}{\omega L} $$
Thus, the original series combination is equivalent to a [current source](@entry_id:275668) with [phasor](@entry_id:273795) $\mathbf{I}_N = -jV_m/(\omega L)$ in parallel with an impedance $Z_N = j\omega L$.

This principle is equally valid in the [s-domain](@entry_id:260604), which is used for analyzing transient behavior. For a source described by a time-dependent voltage $v(t) = V_0 \exp(-\alpha t) \cos(\omega t)$ in series with a capacitor $C$ [@problem_id:1334092], we first find the [s-domain](@entry_id:260604) representations. The Thévenin impedance is the impedance of the capacitor, $Z_{th}(s) = 1/(sC)$. The Thévenin voltage is the Laplace transform of $v(t)$:
$$ V_{th}(s) = \mathcal{L}\{V_0 \exp(-\alpha t) \cos(\omega t)\} = V_0 \frac{s+\alpha}{(s+\alpha)^2 + \omega^2} $$
The Norton equivalent impedance is simply $Z_N(s) = Z_{th}(s) = 1/(sC)$. The Norton current source is:
$$ I_N(s) = \frac{V_{th}(s)}{Z_{th}(s)} = \frac{V_0 \frac{s+\alpha}{(s+\alpha)^2 + \omega^2}}{1/(sC)} = \frac{V_0 C s (s+\alpha)}{(s+\alpha)^2 + \omega^2} $$
This demonstrates the universal applicability of the transformation rules, provided the circuit is represented in a consistent domain (time, [phasor](@entry_id:273795), or Laplace).

### Transformations with Dependent Sources

Source transformations are also valid for circuits containing **[dependent sources](@entry_id:267114)**. These sources, whose output is controlled by a voltage or current elsewhere in the circuit, are fundamental to the modeling of active devices like transistors and operational amplifiers. When performing a transformation, the controlling variable is treated as a given parameter.

Imagine a circuit segment containing a dependent voltage source $V_{dep} = \beta i_c$ in series with a resistor $R_S$ [@problem_id:1334059]. Here, $i_c$ is a control current from another part of the circuit, and $\beta$ is a transresistance gain. This is a Thévenin form with $V_{th} = \beta i_c$ and $R_{th} = R_S$. The equivalent Norton circuit will have a parallel resistance $R_{eq} = R_S$ and a [current source](@entry_id:275668) $I_{eq}$. The value of this [current source](@entry_id:275668) is:
$$ I_{eq} = \frac{V_{th}}{R_{th}} = \frac{\beta i_c}{R_S} = \left(\frac{\beta}{R_S}\right) i_c $$
Notice that the resulting equivalent source is also a dependent source, but it is now a [current source](@entry_id:275668) controlled by the same current $i_c$. The new gain factor is a dimensionless current gain $\gamma = \beta / R_S$.

Conversely, we can transform a Norton-style dependent source into a Thévenin equivalent. If a circuit's output stage is modeled as a [current-controlled current source](@entry_id:263443) (CCCS) of value $\beta i_x$ in parallel with a resistor $R_p$ [@problem_id:1334075], this is a Norton model. Its Thévenin equivalent will have the same resistance, $R_{th} = R_p$, and a Thévenin voltage given by:
$$ V_{th} = I_N R_N = (\beta i_x) R_p $$
The resulting Thévenin source is a current-controlled voltage source (CCVS). This ability to switch between series and parallel representations of [dependent sources](@entry_id:267114) is invaluable in device modeling and analysis.

### Applications in Circuit Simplification

The primary motivation for using source transformations is to simplify [circuit analysis](@entry_id:261116). By strategically applying these transformations, we can often reduce the number of nodes or meshes, combine sources, or simplify complex networks into forms that are easier to solve.

One powerful application is in [nodal analysis](@entry_id:274889). Consider a circuit with an [ideal voltage source](@entry_id:276609) $V_S$ connected between ground and Node 1, followed by a resistor $R_1$ between Node 1 and Node 2 [@problem_id:1334049]. In standard [nodal analysis](@entry_id:274889), the voltage at Node 1 is fixed at $V_1 = V_S$, but Node 1 still exists in the equations. We can simplify the topology by transforming the series combination of the voltage source $V_S$ and resistor $R_1$ into an equivalent [current source](@entry_id:275668). The new [current source](@entry_id:275668) would have a value of $I_{eq} = V_S / R_1$ and would be placed in parallel with resistor $R_1$. In the transformed circuit, the current source and the resistor would be connected between Node 2 and ground. This transformation effectively eliminates Node 1 from the analysis, reducing the number of unknown node voltages and simplifying the resulting system of KCL equations.

For more extensive circuits, such as ladder networks, source transformations can be applied iteratively to "roll up" the circuit from the source end to the load end. For instance, in a circuit where a voltage source and series resistor feed a node that has both a shunt resistor and a series resistor leading to the next stage [@problem_id:1334080], we can proceed as follows:
1.  Transform the initial voltage source and its series resistor into a parallel [current source](@entry_id:275668) and resistor.
2.  Combine the parallel resistor from the transformation with the original shunt resistor at that node.
3.  The result is a new, simpler Norton equivalent circuit feeding the next stage. Now, transform this back into a Thévenin equivalent.
4.  This new Thévenin equivalent's series resistance can be combined with the next series resistor in the ladder.
By repeating this process of transformation and combination, a complex ladder can be reduced to a single Thévenin or Norton equivalent circuit as seen by the final load, making the calculation of load current or voltage trivial.

### Important Caveats and Nuances

While [source transformation](@entry_id:264552) is a robust tool, it is essential to understand its scope and limitations.

#### Equivalence is External Only

A crucial point is that the Thévenin and Norton circuits are equivalent only with respect to their **external terminals**. The internal physics of the two models are different. A common misconception is to assume that internal characteristics, like the power dissipated in the [internal resistance](@entry_id:268117), are conserved across the transformation. They are not.

Let's analyze this by considering a practical voltage source ($V_S$ in series with $R_S$) connected to a load $R_L$ [@problem_id:1334073]. The current in this [series circuit](@entry_id:271365) is $I = V_S / (R_S + R_L)$, and the power dissipated in the internal resistance $R_S$ is $P_V = I^2 R_S = V_S^2 R_S / (R_S + R_L)^2$.

Now, we transform the source into its Norton equivalent ($I_N = V_S/R_S$ in parallel with $R_N = R_S$) and connect it to the same load $R_L$. The voltage across the parallel combination is found using the [current divider](@entry_id:271037) rule and Ohm's law, resulting in $V = I_N (R_N || R_L) = V_S R_L / (R_S + R_L)$. The power dissipated in the internal resistance $R_N$ is $P_I = V^2 / R_N = (V_S^2 R_L^2 / (R_S + R_L)^2) / R_S$.

Comparing the two dissipated powers, we find their ratio is:
$$ \frac{P_I}{P_V} = \frac{V_S^2 R_L^2 / (R_S(R_S+R_L)^2)}{V_S^2 R_S / (R_S+R_L)^2} = \frac{R_L^2}{R_S^2} = \left(\frac{R_L}{R_S}\right)^2 $$
Clearly, $P_I$ and $P_V$ are not equal unless $R_L = R_S$. This confirms that while the transformation provides an identical output to the load, it does not preserve the internal power distribution.

#### Limiting Cases: Ideal Sources

The transformation requires a finite, non-zero impedance in series (for a voltage source) or parallel (for a current source). This leads to interesting behavior when we consider ideal sources. An [ideal voltage source](@entry_id:276609) has zero internal resistance ($R_S=0$). If we attempt to find its Norton equivalent [@problem_id:1334081], the Norton resistance would be $R_N = R_S = 0$, and the Norton current would be $I_N = V_S / R_S \to \infty$. Therefore, an [ideal voltage source](@entry_id:276609) corresponds to a Norton equivalent with an infinite [current source](@entry_id:275668) in parallel with a zero-ohm resistor (a short circuit).

Conversely, an [ideal current source](@entry_id:272249) has infinite [internal resistance](@entry_id:268117) ($R_S \to \infty$). Attempting a transformation to a Thévenin equivalent yields a Thévenin resistance $R_{Th} = R_S \to \infty$ and a Thévenin voltage $V_{Th} = I_S R_S \to \infty$. These infinite values indicate that a direct [source transformation](@entry_id:264552) on an [ideal current source](@entry_id:272249) is not a physically meaningful or practical operation.

#### Application to Non-linear Circuits

Source transformations are a tool for linear circuits. However, they can still be exceptionally useful in the analysis of circuits containing non-linear elements, such as diodes or transistors, through [small-signal analysis](@entry_id:263462). The key is to apply the transformation only to the linear part of the circuit.

Consider a diode driven by a DC source with an AC signal superimposed ($V_{DC} + v_{ac}(t)$) through a series resistor $R_S$ [@problem_id:1334052]. The diode itself is a non-linear device. We cannot transform the diode. However, we can transform the linear source network ($V_{DC} + v_{ac}(t)$ and $R_S$) into its Norton equivalent *before* connecting it to the diode. This results in a composite current source in parallel with $R_S$. The DC part of this source sets the diode's DC [operating point](@entry_id:173374) (Q-point), around which we linearize the diode's behavior into a small-signal [dynamic resistance](@entry_id:268111), $r_d$. The AC part of the Norton current then drives a parallel combination of $R_S$ and $r_d$. As demonstrated by detailed analysis, the resulting AC current in the diode is identical to that calculated without the initial transformation. This powerful result shows that we can legitimately simplify the linear driving portion of a circuit using source transformations, even when the ultimate load is non-linear, greatly facilitating [small-signal analysis](@entry_id:263462).