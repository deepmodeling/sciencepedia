## Introduction
Corrosion, the gradual destruction of materials by chemical reaction with their environment, is a pervasive and costly electrochemical problem. While thermodynamics can predict if a metal is susceptible to corrosion, it cannot tell us how fast this degradation will occur. This knowledge gap is critical, as the rate of corrosion determines the functional lifetime of everything from pipelines and bridges to microelectronic components. The key to bridging this gap lies in understanding [corrosion kinetics](@entry_id:192636), and the most powerful tool for visualizing these kinetics is the Evans diagram.

This article provides a foundational understanding of Evans diagrams and their application in predicting and controlling corrosion. It demystifies the complex interplay between the different electrochemical reactions that drive the corrosion process. Across three chapters, you will gain a comprehensive perspective on this essential topic.

The first chapter, **"Principles and Mechanisms,"** lays the groundwork by introducing the [mixed potential theory](@entry_id:153089), explaining how the Tafel equation describes [reaction kinetics](@entry_id:150220), and showing how these elements combine to construct an Evans diagram. You will learn to identify the [corrosion potential](@entry_id:265069) and [current density](@entry_id:190690) and understand why kinetics, not just thermodynamics, govern corrosion rates. The second chapter, **"Applications and Interdisciplinary Connections,"** moves from theory to practice, demonstrating how Evans diagrams are used to analyze real-world phenomena like galvanic corrosion, [cathodic protection](@entry_id:137081), passivation, and the action of inhibitors, with connections to fields from materials science to battery technology. Finally, the **"Hands-On Practices"** chapter will allow you to apply these concepts to solve quantitative and conceptual problems, solidifying your ability to use Evans diagrams as an analytical tool.

## Principles and Mechanisms

### The Foundation: Mixed Potential Theory

The electrochemical nature of corrosion dictates that at least two distinct reactions must occur simultaneously on a metal's surface: an **anodic reaction** (oxidation), where the metal dissolves into its ions, and a **cathodic reaction** (reduction), which consumes the electrons released by the anodic process. For a metal corroding uniformly, the entire surface is equipotential. This leads to the central tenet of [corrosion kinetics](@entry_id:192636): the **[mixed potential theory](@entry_id:153089)**. This theory posits that a corroding conductor, isolated from any external electrical circuit, will establish a single, steady-state electrode potential known as the **[corrosion potential](@entry_id:265069)**, denoted as $E_{corr}$. At this potential, the total rate of all anodic reactions is precisely equal to the total rate of all cathodic reactions. This rate, when expressed as an electrical [current density](@entry_id:190690), is termed the **[corrosion current density](@entry_id:272787)**, $i_{corr}$.

It is crucial to understand that $E_{corr}$ is a non-equilibrium, or mixed, potential. It does not represent the thermodynamic equilibrium for either the anodic or the cathodic reaction alone. Instead, it is a kinetic steady state where, while the *net* external current is zero, there are equal and opposing currents flowing due to the simultaneous oxidation and reduction processes on the surface. The magnitude of this current, $i_{corr}$, is directly proportional to the rate at which the metal is being destroyed.

### Visualizing Corrosion Kinetics: The Evans Diagram

To visualize the principles of [mixed potential theory](@entry_id:153089), we employ a powerful graphical tool known as the **Evans diagram**. An Evans diagram is a plot of [electrode potential](@entry_id:158928) ($E$) versus the logarithm of the current density ($\log|i|$). By plotting the polarization curves for the individual anodic and cathodic reactions on the same set of axes, we can predict the corrosion behavior of the system. The intersection of the total anodic curve and the total cathodic curve reveals the [corrosion potential](@entry_id:265069) ($E_{corr}$) on the vertical axis and the [corrosion current density](@entry_id:272787) ($i_{corr}$) on the horizontal axis.

Let us consider a simple case of a pure metal, such as iron, corroding in a deaerated acidic solution [@problem_id:1560291]. The two reactions are:

Anodic (Iron Dissolution): $Fe \rightarrow Fe^{2+} + 2e^-$
Cathodic (Hydrogen Evolution): $2H^{+} + 2e^{-} \rightarrow H_{2}$

In many cases, when the reactions are driven far from their [equilibrium states](@entry_id:168134), the relationship between potential and [current density](@entry_id:190690) can be described by the **Tafel equation**.

For the anodic reaction, the potential $E$ required to drive the reaction at a current density $i_a$ is:
$E = E_{eq, a} + \beta_a \log_{10}\left(\frac{i_a}{i_{0,a}}\right)$

For the cathodic reaction, the potential required for a [current density](@entry_id:190690) $i_c$ is:
$E = E_{eq, c} - \beta_c \log_{10}\left(\frac{i_c}{i_{0,c}}\right)$

Here, $E_{eq, a}$ and $E_{eq, c}$ are the equilibrium potentials for the anodic and cathodic [half-reactions](@entry_id:266806), respectively. The **[exchange current density](@entry_id:159311)**, $i_0$, represents the [rate of reaction](@entry_id:185114) at equilibrium (i.e., the rate of forward and reverse reactions are equal and non-zero). The **Tafel slope**, $\beta$, is a measure of the reaction's polarizability; a larger Tafel slope indicates that a greater change in potential is required to produce a one-decade change in [current density](@entry_id:190690).

According to [mixed potential theory](@entry_id:153089), at the [corrosion potential](@entry_id:265069) $E_{corr}$, the anodic current density equals the cathodic current density, $i_a = i_c = i_{corr}$. Therefore, we can find the corrosion parameters by setting the two Tafel expressions equal:

$E_{eq, a} + \beta_a \log_{10}\left(\frac{i_{corr}}{i_{0,a}}\right) = E_{eq, c} - \beta_c \log_{10}\left(\frac{i_{corr}}{i_{0,c}}\right)$

By rearranging this equation, one can solve for $i_{corr}$ and subsequently $E_{corr}$. For example, if we consider iron in an acid with $E_{eq, a} = -0.440 \text{ V}$, $E_{eq, c} = 0.000 \text{ V}$, $\beta_a = 0.060 \text{ V/decade}$, and $\beta_c = 0.120 \text{ V/decade}$, and assuming for simplicity a common reference current, we can algebraically solve for the intersection. This calculation would yield a [corrosion current density](@entry_id:272787) $i_{corr} \approx 2.8 \times 10^{-4} \text{ A/cm}^2$ [@problem_id:1560291]. In many practical scenarios, such as the corrosion of zinc in an acid, one must first calculate the specific equilibrium potentials $E_{eq, a}$ and $E_{eq, c}$ under non-standard conditions using the Nernst equation before applying the Tafel analysis [@problem_id:1560348].

### The Primacy of Kinetics over Thermodynamics

A common misconception is that the thermodynamic tendency of a metal to corrode, as indicated by its [standard electrode potential](@entry_id:170610) ($E^\circ$), is a direct predictor of its [corrosion rate](@entry_id:274545). A more negative $E^\circ$ signifies a greater thermodynamic driving force for oxidation, but it says nothing about the *rate* at which this oxidation will occur. Corrosion is a kinetic phenomenon.

Consider two different metals, Metal A ($E^\circ_{A^{2+}/A} = -0.250 \text{ V}$) and Metal B ($E^\circ_{B^{2+}/B} = -0.500 \text{ V}$), both corroding in the same acidic solution where hydrogen evolution is the cathodic reaction [@problem_id:2935326]. Based on thermodynamics alone, one might predict that Metal B, with its much more negative standard potential, would corrode far more rapidly. However, the actual [corrosion rate](@entry_id:274545) depends on the kinetics of both the metal dissolution and the [hydrogen evolution reaction](@entry_id:184471) occurring on the metal's surface.

Let's assume Metal B is a much better catalyst for the [hydrogen evolution reaction](@entry_id:184471) than Metal A, reflected by a significantly higher [exchange current density](@entry_id:159311) for hydrogen evolution ($i_{0,H_2}^{(B)} \gg i_{0,H_2}^{(A)}$). For instance, if $i_{0,H_2}^{(B)} = 10^{-4} \text{ A/cm}^2$ while $i_{0,H_2}^{(A)} = 10^{-8} \text{ A/cm}^2$, the cathodic [polarization curve](@entry_id:271394) for Metal B will be positioned far to the right of the curve for Metal A on an Evans diagram. The intersection of this highly efficient cathodic process with Metal B's anodic curve can result in a [corrosion current density](@entry_id:272787) ($i_{corr}^{(B)}$) that is orders of magnitude higher than that for Metal A ($i_{corr}^{(A)}$), despite Metal A's nobler standard potential. In such a case, calculations may show $i_{corr}^{(B)} \approx 6.0 \times 10^{-3} \text{ A/cm}^2$ while $i_{corr}^{(A)} \approx 1.1 \times 10^{-6} \text{ A/cm}^2$. This demonstrates unequivocally that [corrosion rate](@entry_id:274545) is governed by the kinetic parameters ($i_0$, $\beta$) of the coupled system, not just the [thermodynamic potentials](@entry_id:140516).

### Factors Influencing Corrosion

The [corrosion potential](@entry_id:265069) and [current density](@entry_id:190690) are sensitive to any factor that alters the position or shape of the anodic or cathodic polarization curves.

#### Effect of Kinetic Parameters

The intrinsic kinetic properties of the reactions, namely the [exchange current density](@entry_id:159311) ($i_0$) and the Tafel slope ($\beta$), are paramount.

-   **Exchange Current Density ($i_0$)**: A higher [exchange current density](@entry_id:159311) means a reaction is kinetically faster or less polarizable. On an Evans diagram, a higher $i_0$ shifts the entire Tafel line horizontally towards higher currents. For instance, an engineer might develop an alloy that reduces the [exchange current density](@entry_id:159311) for metal dissolution ($i_{0,a}$) from $10^{-7} \text{ A/cm}^2$ to $10^{-9} \text{ A/cm}^2$ [@problem_id:1560322]. This modification shifts the anodic curve to the left (towards lower current for a given potential), causing its intersection with the fixed cathodic curve to occur at a lower [current density](@entry_id:190690). This directly reduces the [corrosion rate](@entry_id:274545).

-   **Tafel Slope ($\beta$)**: The Tafel slope reflects how strongly a reaction's rate changes with potential. A larger slope means the reaction is more easily polarized. Graphically, increasing a Tafel slope makes the line steeper on an Evans diagram. If the anodic Tafel slope ($\beta_a$) is increased, the anodic line becomes steeper. For a fixed cathodic curve, this steeper anodic line will intersect it at a lower [current density](@entry_id:190690), thus decreasing $i_{corr}$ [@problem_id:1560336]. Therefore, modifications that increase the polarizability of either the anodic or cathodic reaction can serve as a strategy for [corrosion inhibition](@entry_id:152717).

#### Effect of Reactant Concentration

The concentration of reacting species can significantly alter the corrosion behavior, primarily by affecting the cathodic reaction. A classic example is the effect of pH on corrosion in acids, where hydrogen evolution is the cathodic step [@problem_id:1560330]. According to the Nernst equation for the hydrogen reaction ($2H^{+} + 2e^{-} \rightarrow H_{2}$), the [equilibrium potential](@entry_id:166921) $E_{eq,c}$ becomes more positive as the concentration (activity) of $H^+$ increases (i.e., as pH decreases).

$E_{eq,H_2} = E^\circ_{H_2} - \frac{2.303 RT}{2F} \log_{10}\left(\frac{P_{H_2}}{[H^+]^2}\right)$

This upward shift of the [equilibrium potential](@entry_id:166921) translates to an upward shift of the entire cathodic [polarization curve](@entry_id:271394) on the Evans diagram. The shifted cathodic curve now intersects the fixed anodic curve at a higher potential and a higher current density. Consequently, increasing the [acidity](@entry_id:137608) of a solution generally increases both the [corrosion potential](@entry_id:265069) ($E_{corr}$) and the [corrosion rate](@entry_id:274545) ($i_{corr}$).

### Complex Corrosion Scenarios

Real-world corrosion systems often involve additional complexities beyond simple activation control. Evans diagrams are indispensable for analyzing these scenarios as well.

#### Mass Transport Limitation

For many corrosion processes, especially those involving [dissolved oxygen](@entry_id:184689) in [aqueous solutions](@entry_id:145101), the rate of the cathodic reaction can be limited by the speed at which the reactant (e.g., $O_2$) is transported from the bulk solution to the metal surface. When this occurs, the cathodic [current density](@entry_id:190690) reaches a maximum value, the **[diffusion-limited current](@entry_id:267130) density**, $i_L$. On an Evans diagram, the cathodic curve, after an initial activation-controlled region, becomes a vertical line at $i_c = i_L$, independent of potential.

The corrosion process is then said to be under **[mass transport control](@entry_id:266547)** if the hypothetical intersection of the activation-controlled anodic and cathodic curves would have occurred at a current greater than $i_L$. In this case, the [corrosion current density](@entry_id:272787) is simply clamped at this limit: $i_{corr} = i_L$. The [corrosion potential](@entry_id:265069), $E_{corr}$, is then the potential on the *anodic* curve corresponding to this current density [@problem_id:2931539].

This has important practical implications. Any factor that enhances [mass transport](@entry_id:151908) will increase the [corrosion rate](@entry_id:274545). For example, stirring the water around a copper pipe decreases the thickness of the stagnant [diffusion layer](@entry_id:276329) ($\delta$) at the metal surface. Since $i_L$ is inversely proportional to $\delta$, stirring increases $i_L$. This shifts the vertical portion of the cathodic curve to the right, leading to a new intersection at a higher $i_{corr}$ and a more positive $E_{corr}$ [@problem_id:1571970]. Conversely, a cathodic inhibitor that hinders [oxygen transport](@entry_id:138803) (e.g., by forming a surface film) will decrease $i_L$, reduce the [corrosion rate](@entry_id:274545), and typically shift $E_{corr}$ to a more negative (active) potential [@problem_id:2931539].

#### Passivation

Many technologically crucial metals, such as titanium, aluminum, and stainless steels, owe their excellent [corrosion resistance](@entry_id:183133) to **passivation**. Passivation is the spontaneous formation of a very thin, ultra-stable, and non-reactive surface film (typically an oxide) that kinetically isolates the metal from its environment.

The [anodic polarization curve](@entry_id:276237) for a passivating metal is distinct. At low potentials, the metal corrodes actively, following a Tafel-like behavior. However, upon reaching a specific potential known as the **primary passivation potential** ($E_{pp}$), the current density drastically drops to a very low, nearly constant value called the **passive [current density](@entry_id:190690)**, $i_p$ [@problem_id:1979837]. The metal remains in this passive state over a wide range of potentials.

When such a metal is placed in an oxidizing environment (e.g., aerated seawater, where the cathodic oxygen reduction curve is high on the potential scale), the intersection point on the Evans diagram falls within this passive region. The [corrosion potential](@entry_id:265069) $E_{corr}$ becomes very noble, and more importantly, the [corrosion current density](@entry_id:272787) is limited to the extremely small passive [current density](@entry_id:190690), $i_{corr} = i_p$. For a titanium alloy in seawater, the hypothetical [corrosion rate](@entry_id:274545) if it did not passivate could be millions of times higher than the actual rate observed in its passive state. The Evans diagram graphically illustrates how this remarkable kinetic barrier, not the metal's inherent thermodynamic reactivity (titanium has a very negative $E^\circ$), provides its exceptional durability.

#### Systems with Multiple Cathodic Reactions

In environments like aerated acidic water, a metal surface can support more than one cathodic reaction simultaneously, for example, both hydrogen evolution and oxygen reduction. In such cases, the total rate of reduction at any given potential is the sum of the rates of all individual cathodic reactions.

On an Evans diagram, the total cathodic [polarization curve](@entry_id:271394) is constructed by adding the currents of the individual cathodic curves at each potential:
$i_{c,total}(E) = i_{c,1}(E) + i_{c,2}(E) + \dots$

The [corrosion potential](@entry_id:265069) and total [corrosion current density](@entry_id:272787) are then determined by the intersection of the anodic curve with this composite cathodic curve [@problem_id:1560313]. Often, one cathodic reaction will be dominant in the potential range of interest. For example, for zinc in slightly acidic aerated water, the oxygen reduction [limiting current](@entry_id:266039) might be much larger than the current from hydrogen evolution, making it the dominant cathodic process. However, the hydrogen evolution still contributes to the total cathodic current, and a precise calculation must account for its effect, however small.

#### Anodic, Cathodic, and Mixed Control

Finally, the concept of **control** helps describe which reaction is the primary bottleneck for the corrosion process.

-   **Cathodic Control**: Occurs when the anodic reaction is kinetically fast (low polarization) and the cathodic reaction is slow (high polarization). The [corrosion rate](@entry_id:274545) is limited almost entirely by the cathodic reaction's kinetics. $E_{corr}$ will be located close to the equilibrium potential of the anodic reaction, $E_{eq,a}$. This state can be induced by adding a cathodic inhibitor that slows down the reduction reaction [@problem_id:1560303].
-   **Anodic Control**: Occurs when the cathodic reaction is fast and the anodic reaction is slow. The [corrosion rate](@entry_id:274545) is determined by the anodic kinetics. This is characteristic of passivating metals, where the extremely slow anodic process in the passive state limits the overall rate. In this case, $E_{corr}$ will be close to the [equilibrium potential](@entry_id:166921) of the cathodic reaction, $E_{eq,c}$.
-   **Mixed Control**: Occurs when both the anodic and cathodic reactions exhibit significant polarization. The kinetics of both processes are important in determining the final [corrosion rate](@entry_id:274545) and potential. $E_{corr}$ lies somewhere between $E_{eq,a}$ and $E_{eq,c}$.

The Evans diagram provides a comprehensive and unified framework for understanding these diverse phenomena, enabling us to predict and interpret the complex kinetic interplay that governs the corrosion of metals.