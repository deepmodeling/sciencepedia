## Introduction
The Bipolar Junction Transistor (BJT) is a cornerstone of modern electronics, essential for everything from high-frequency amplifiers to precision analog circuits. While its function can be described by simplified circuit models, a deep understanding of its capabilities and limitations requires a dive into the underlying semiconductor physics. This article addresses the need for a quantitative physical description of BJT operation by exploring how charge carriers move and interact within the device to produce its characteristic behavior.

This article will guide you through a comprehensive analysis, starting from first principles to build a robust model of current transport. The first chapter, **Principles and Mechanisms**, establishes the theoretical foundation, deriving the key current components from the drift-diffusion and continuity equations. We will explore the roles of quasi-Fermi potentials, recombination, and [minority carrier diffusion](@entry_id:188843). The second chapter, **Applications and Interdisciplinary Connections**, connects this physics to practical [device modeling](@entry_id:1123619) (like Ebers-Moll), characterization techniques (the Gummel plot), and advanced device engineering, showing how these principles influence fields from power electronics to reliability physics. Finally, the **Hands-On Practices** chapter allows you to apply these concepts to solve quantitative problems, solidifying your understanding of the link between device physics and performance.

## Principles and Mechanisms

This chapter delves into the fundamental principles governing carrier transport and current flow in the Bipolar Junction Transistor (BJT). We will develop a quantitative physical model, starting from first principles of [semiconductor physics](@entry_id:139594), to describe the relationships between the terminal currents and the applied voltages. This model will not only elucidate the BJT's amplification mechanism but also reveal design trade-offs and non-ideal behaviors inherent in practical devices.

### Fundamental Principles of Carrier Transport

At the heart of all semiconductor device operation are the dual processes of carrier drift and diffusion, governed by the continuity equations. In a BJT, these processes occur under non-equilibrium conditions, where carrier populations are modulated by applied biases. To formalize this, we employ the powerful concept of quasi-Fermi levels.

#### Quasi-Fermi Potentials as Driving Forces

While the Fermi level $E_F$ is uniform throughout a semiconductor in thermal equilibrium, this is no longer true when external biases or illumination create excess carriers. Under such non-equilibrium, steady-state conditions, we define separate **quasi-Fermi levels** for electrons ($F_n$) and holes ($F_p$). The carrier concentrations are then related to these levels by:

$n = n_i \exp\left( \frac{F_n - E_i}{k_B T} \right)$

$p = n_i \exp\left( \frac{E_i - F_p}{k_B T} \right)$

where $E_i$ is the intrinsic Fermi level, $n_i$ is the [intrinsic carrier concentration](@entry_id:144530), $k_B$ is the Boltzmann constant, and $T$ is the [absolute temperature](@entry_id:144687). The product $np = n_i^2 \exp\left( \frac{F_n - F_p}{k_B T} \right)$ reveals that the separation of the quasi-Fermi levels is a direct measure of the deviation from equilibrium.

The true significance of the quasi-Fermi level is that its spatial gradient represents the generalized thermodynamic driving force for [carrier transport](@entry_id:196072). The drift-diffusion current equations can be elegantly re-expressed in terms of the quasi-Fermi potentials, defined as $\phi_n = F_n/q$ and $\phi_p = F_p/q$, where $q$ is the [elementary charge](@entry_id:272261). Through a straightforward substitution of the [carrier concentration](@entry_id:144718) expressions into the standard drift-diffusion equations, it can be shown that the electron and hole current densities are given by:

$J_n(x) = q \mu_n n(x) \frac{d\phi_n(x)}{dx}$

$J_p(x) = q \mu_p p(x) \frac{d\phi_p(x)}{dx}$

These relations are profound: they state that a net current of a specific carrier type flows if and only if there is a gradient in its corresponding quasi-Fermi potential. The term $q\mu n$ is the conductivity, $\sigma_n$.

In the forward-active operation of an $n-p-n$ BJT, a large electron current flows across the $p$-type base. This necessitates a significant gradient in the electron quasi-Fermi potential, $\phi_n$, across the base. However, the base current, which is composed of hole-related currents, is much smaller. In the quasi-neutral base, holes are the majority carriers, so their concentration $p(x)$ is large. The hole conductivity $\sigma_p(x) = q\mu_p p(x)$ is therefore very high. Since $d\phi_p/dx = J_p(x)/\sigma_p(x)$, the combination of a small hole current $J_p$ and a large hole conductivity $\sigma_p$ means that the gradient of the hole quasi-Fermi potential is negligible.

For instance, in a typical silicon base with acceptor density $N_A = 10^{17}\,\mathrm{cm}^{-3}$ and [hole mobility](@entry_id:1126148) $\mu_p = 100\,\mathrm{cm}^2/(\mathrm{V} \cdot \mathrm{s})$, the hole conductivity is approximately $1.6\,\mathrm{A/(V \cdot cm)}$. Even for a substantial base-current component of $J_p = 0.5\,\mathrm{A/cm^2}$ crossing a base width of $W_B = 0.2\,\mu\mathrm{m}$, the total drop in $\phi_p$ would be less than $10^{-5}\,\mathrm{V}$. Consequently, it is an excellent approximation to consider the **majority carrier quasi-Fermi potential as constant** throughout a quasi-neutral region.

#### The Continuity Equation and Recombination

Carrier transport is also subject to the law of [charge conservation](@entry_id:151839), encapsulated in the continuity equation. For electrons in one dimension under steady-state conditions, this is:

$\frac{1}{q} \frac{dJ_n}{dx} - U_n = 0$

where $U_n = R_n - G_n$ is the net [recombination rate](@entry_id:203271) (recombination minus generation). This equation states that any spatial variation in the electron current density must be balanced by the net local removal or addition of electrons via recombination or generation.

In the quasi-neutral base of a forward-active BJT, a large concentration of minority electrons is injected from the emitter. This excess concentration, $\Delta n(x) = n_p(x) - n_{p0}$, drives net recombination. Under [low-level injection](@entry_id:1127474), this process is well-described by the Shockley-Read-Hall (SRH) model, which simplifies to $U_n \approx \Delta n(x) / \tau_n$, where $\tau_n$ is the minority electron lifetime. The continuity equation thus becomes:

$\frac{dJ_n}{dx} = q \frac{\Delta n(x)}{\tau_n}$

This equation provides a crucial physical insight. In an $n-p-n$ BJT, electrons flow from the emitter ($x=0$) to the collector ($x=W_B$), so the conventional electron current $J_n$ is negative. As electrons traverse the base, some are lost to recombination, causing the magnitude of the current to decrease. A decreasing magnitude for a negative number means its value increases (becomes less negative). Thus, the slope $dJ_n/dx$ must be positive, which is consistent with the equation, as $q$, $\Delta n$, and $\tau_n$ are all positive. The right-hand side represents the rate of charge removal per unit volume due to recombination.

Recombination is a loss mechanism. A key goal in BJT design is to minimize this loss. The recombination term can be neglected if the time an electron takes to cross the base (the **base transit time**, $t_{tr}$) is much shorter than the average time before it recombines (the **[minority carrier lifetime](@entry_id:267047)**, $\tau_n$). The characteristic transit time for diffusion across a width $W_B$ is $t_{tr} \sim W_B^2/(2D_n)$. The condition for negligible recombination is therefore $t_{tr} \ll \tau_n$, which is equivalent to $W_B \ll \sqrt{2D_n\tau_n}$. By defining the **[minority carrier diffusion](@entry_id:188843) length** $L_n = \sqrt{D_n \tau_n}$ as the average distance an electron diffuses before recombining, this condition is succinctly expressed as $W_B \ll L_n$. This is known as the **narrow-base** or **short-base** condition. When it is met, $dJ_n/dx \approx 0$, and the electron current is nearly constant across the base.

### Minority Carrier Transport in the Quasi-Neutral Regions

The operation of a BJT is dominated by the behavior of minority carriers injected across the forward-biased emitter-base junction. To determine the device currents, we must first solve for the [spatial distribution](@entry_id:188271) of these minority carriers.

#### The Diffusion Equation and Boundary Conditions

We model the BJT as a one-dimensional structure. In the quasi-neutral regions (emitter and base), we assume that any built-in or induced electric fields are negligible, a valid assumption under [low-level injection](@entry_id:1127474). Carrier transport is therefore dominated by diffusion. Combining the diffusion current equation ($J_n = qD_n \frac{dn_p}{dx}$) with the steady-state continuity equation gives the fundamental **[minority carrier diffusion](@entry_id:188843) equation** for excess electrons $\Delta n(x)$ in the $p$-base:

$D_n \frac{d^2 \Delta n(x)}{dx^2} - \frac{\Delta n(x)}{\tau_n} = 0 \quad \implies \quad \frac{d^2 \Delta n(x)}{dx^2} - \frac{\Delta n(x)}{L_n^2} = 0$

An analogous equation holds for excess holes $\Delta p(x)$ in the $n$-emitter, with corresponding parameters $D_p$, $\tau_p$, and $L_p$. To solve this [second-order differential equation](@entry_id:176728), we need two boundary conditions for each region.

1.  **The Law of the Junction**: At the edge of the emitter-base depletion region, the forward bias $V_{BE}$ dramatically increases the minority carrier concentrations. Under [low-level injection](@entry_id:1127474), the relationship is given by the Shockley boundary conditions, which state that the [minority carrier](@entry_id:1127944) concentrations at the edges of the depletion region are exponentially dependent on the junction voltage. For the $n-p-n$ BJT at the depletion edges ($x=0$):
    *   Base side: $n_p(0) = n_{p0} \exp\left(\frac{V_{BE}}{V_T}\right)$, where $V_T = k_B T/q$ is the thermal voltage. The excess concentration is $\Delta n(0) = n_{p0} \left( \exp\left(\frac{V_{BE}}{V_T}\right) - 1 \right)$.
    *   Emitter side: $p_n(0) = p_{n0} \exp\left(\frac{V_{BE}}{V_T}\right)$. The excess concentration is $\Delta p(0) = p_{n0} \left( \exp\left(\frac{V_{BE}}{V_T}\right) - 1 \right)$.

2.  **Far-End Conditions**:
    *   At the collector end of the base ($x=W_B$), the reverse-biased collector-base junction acts as a sink for minority electrons, sweeping them into the collector. This enforces the boundary condition $\Delta n(W_B) \approx 0$. Note that a more precise condition is $n_p(W_B) = n_{p0} \exp(-V_{CB}/V_T) \approx 0$ for large reverse bias $V_{CB}$, which for low injection makes $\Delta n(W_B) \approx -n_{p0}$. However, since $\Delta n(0)$ is typically much larger than $n_{p0}$, setting $\Delta n(W_B)=0$ is an excellent approximation that simplifies the mathematics.
    *   At the far end of the emitter region, an ohmic contact ensures [local thermal equilibrium](@entry_id:147993), forcing the excess minority [carrier concentration](@entry_id:144718) to zero: $\Delta p(W_E) = 0$.

#### The Minority Carrier Concentration Profile

The general solution to the diffusion equation can be written as a sum of exponential or [hyperbolic functions](@entry_id:165175). With the boundary conditions $\Delta n(0)$ and $\Delta n(W_B)=0$, the excess electron profile in the base is found to be:

$\Delta n(x) = \Delta n(0) \frac{\sinh\left(\frac{W_B-x}{L_n}\right)}{\sinh\left(\frac{W_B}{L_n}\right)}$

Similarly, the excess hole profile in the emitter is:

$\Delta p(x') = \Delta p(0) \frac{\sinh\left(\frac{W_E-x'}{L_p}\right)}{\sinh\left(\frac{W_E}{L_p}\right)}$

where $x'$ is the coordinate into the emitter. These profiles describe how the injected [minority carrier](@entry_id:1127944) populations decay due to diffusion towards a sink and recombination along the way.

### Analysis of Current Components

With the [minority carrier](@entry_id:1127944) profiles established, we can calculate the various current components by evaluating the [diffusion current](@entry_id:262070) density ($J = qD \nabla n$) at the junction boundaries. The performance of a BJT is characterized by how efficiently it moves charge from the emitter to the collector. This is quantified by two key figures of merit: the [emitter injection efficiency](@entry_id:269307) and the base transport factor.

#### Emitter Injection Efficiency, $\gamma$

The total current crossing the emitter-base junction, $J_E$, is the sum of two components: the desired electron current injected from the emitter into the base ($J_{n,E}$) and the parasitic hole current injected from the base back into the emitter ($J_{p,E}$). The **[emitter injection efficiency](@entry_id:269307)**, $\gamma$, is defined as the fraction of the total emitter current that is carried by the desired minority carriers:

$\gamma = \frac{J_{n,E}}{J_E} = \frac{J_{n,E}}{J_{n,E} + J_{p,E}} = \left( 1 + \frac{J_{p,E}}{J_{n,E}} \right)^{-1}$

The current densities are found by differentiating the carrier profiles at the junction ($x=0$). The results are:

$J_{n,E} = \left| q D_n \frac{d\Delta n}{dx} \right|_{x=0} = \frac{q D_n \Delta n(0)}{L_n} \coth\left(\frac{W_B}{L_n}\right)$

$J_{p,E} = \left| -q D_p \frac{d\Delta p}{dx'} \right|_{x'=0} = \frac{q D_p \Delta p(0)}{L_p} \coth\left(\frac{W_E}{L_p}\right)$

Substituting the "Law of the Junction" expressions for $\Delta n(0)$ and $\Delta p(0)$, the term $(\exp(V_{BE}/V_T) - 1)$ cancels in the ratio $J_{p,E}/J_{n,E}$. This shows that, under [low-level injection](@entry_id:1127474), $\gamma$ is independent of the bias voltage. The final expression is:

$\gamma = \left[ 1 + \frac{\frac{D_p p_{n0}}{L_p} \coth\left(\frac{W_E}{L_p}\right)}{\frac{D_n n_{p0}}{L_n} \coth\left(\frac{W_B}{L_n}\right)} \right]^{-1}$

Recalling that $p_{n0} = n_i^2/N_{D,E}$ and $n_{p0} = n_i^2/N_{A,B}$, the ratio $p_{n0}/n_{p0} = N_{A,B}/N_{D,E}$. To achieve a high injection efficiency ($\gamma \approx 1$), the ratio $J_{p,E}/J_{n,E}$ must be minimized. This is achieved by making the emitter doping much higher than the base doping ($N_{D,E} \gg N_{A,B}$), which makes $p_{n0}$ very small and suppresses the back-injection of holes. For a typical BJT with $N_{D,E} = 10^{19}\,\mathrm{cm}^{-3}$ and $N_{A,B} = 10^{17}\,\mathrm{cm}^{-3}$, a calculation yields $\gamma \approx 0.9987$, confirming the effectiveness of this strategy.

#### Base Transport Factor, $\alpha_T$

Not all electrons injected into the base reach the collector; some are lost to recombination. The **base transport factor**, $\alpha_T$, quantifies the efficiency of transport across the base:

$\alpha_T = \frac{\text{Electron current reaching collector}}{\text{Electron current injected into base}} = \frac{|J_n(W_B)|}{|J_n(0)|}$

Using the expressions for [diffusion current](@entry_id:262070) derived from the minority carrier profile, we find:

$|J_n(W_B)| = \frac{q D_n \Delta n(0)}{L_n \sinh(W_B/L_n)}$

$|J_n(0)| = \frac{q D_n \Delta n(0)}{L_n \tanh(W_B/L_n)}$

Taking their ratio gives the elegant result:

$\alpha_T = \frac{1}{\cosh\left(\frac{W_B}{L_n}\right)}$

To maximize $\alpha_T$ and ensure most electrons reach the collector, the argument of the hyperbolic cosine must be small, which requires $W_B \ll L_n$. This is the same "narrow-base" condition we identified for neglecting recombination. For $W_B \ll L_n$, we can use the Taylor expansion $\cosh(u) \approx 1 + u^2/2$, which gives $\alpha_T \approx 1 - \frac{1}{2}\left(\frac{W_B}{L_n}\right)^2$. This shows that the fraction of current lost to recombination is proportional to the square of the ratio of base width to diffusion length.

#### The Collector Current and Common-Base Current Gain

The total collector current $I_C$ is the electron current that successfully crosses the base. It is related to the total emitter current $I_E$ by these two efficiency factors:

$I_C = \gamma \alpha_T I_E$

The ratio $\alpha = I_C/I_E = \gamma \alpha_T$ is the **[common-base current gain](@entry_id:268840)**. For a well-designed transistor, both $\gamma$ and $\alpha_T$ are very close to unity, making $\alpha$ slightly less than 1 (e.g., 0.99). The small difference, $I_E - I_C = I_B$, constitutes the base current, which is the sum of the hole back-injection current and the electron recombination current.

### The Short-Base Approximation and the Charge-Control Model

The full hyperbolic expressions, while exact, can be cumbersome. In modern transistors, the narrow-base condition ($W_B \ll L_n$) is almost always satisfied. This allows for a powerful simplification that leads to a more intuitive model of transistor action.

#### The Linear Carrier Profile

When $W_B/L_n \ll 1$, we can approximate $\sinh(u) \approx u$ in the minority carrier profile expression:

$\Delta n(x) = \Delta n(0) \frac{\sinh\left(\frac{W_B-x}{L_n}\right)}{\sinh\left(\frac{W_B}{L_n}\right)} \approx \Delta n(0) \frac{(W_B-x)/L_n}{W_B/L_n} = \Delta n(0) \left(1 - \frac{x}{W_B}\right)$

This shows that for a narrow base, the minority [carrier concentration](@entry_id:144718) profile is approximately a straight line, decreasing linearly from its maximum value at the emitter edge to zero at the collector edge. This simplification is equivalent to neglecting recombination within the base altogether, which is why the profile is linear (constant diffusion gradient implies constant current).

#### The Collector Current in the Short-Base Limit

Using this linear profile, the calculation of the collector current becomes trivial. The gradient is constant throughout the base: $d\Delta n/dx = -\Delta n(0)/W_B$. The collector current density is thus:

$J_C = |q D_n \frac{d\Delta n}{dx}| = \frac{q D_n \Delta n(0)}{W_B}$

Substituting $\Delta n(0) = n_{p0}(\exp(V_{BE}/V_T) - 1)$ and $n_{p0} = n_i^2/N_{A,B}$, and multiplying by the device area $A$, we obtain the classic expression for collector current in the [forward-active region](@entry_id:261687):

$I_C = \frac{A q D_n n_i^2}{W_B N_{A,B}} \left( \exp\left(\frac{V_{BE}}{V_T}\right) - 1 \right)$

This equation is a cornerstone of BJT modeling. It shows that the collector current is controlled exponentially by the base-emitter voltage $V_{BE}$ and is inversely proportional to the base width $W_B$ and base doping $N_{A,B}$. The collection of terms $I_S = \frac{A q D_n n_i^2}{W_B N_{A,B}}$ is called the saturation current.

#### The Charge-Control Concept and Base Transit Time

An alternative and powerful perspective is the **[charge-control model](@entry_id:1122284)**. This model relates the terminal currents to the total amount of excess minority charge stored in the device. The total excess electron charge stored in the base is $Q_B = qA \int_0^{W_B} \Delta n(x) dx$. The collector current can be seen as the result of this stored charge being "replaced" at a certain rate. This rate is characterized by the **base transit time**, $\tau_T$, defined by the relation:

$I_C = \frac{Q_B}{\tau_T}$

We can derive an expression for $\tau_T$ by calculating both $Q_B$ and $I_C$ from our exact solution for $\Delta n(x)$ and taking their ratio. This calculation yields:

$\tau_T = \frac{L_n^2}{D_n} \left( \cosh\left(\frac{W_B}{L_n}\right) - 1 \right)$

Since $L_n^2 = D_n \tau_n$, we can write $\tau_T = \tau_n (\cosh(W_B/L_n) - 1)$. For a short base where $W_B \ll L_n$, using the Taylor expansion $\cosh(u) \approx 1 + u^2/2$, we find a remarkably simple result:

$\tau_T \approx \frac{L_n^2}{D_n} \left( 1 + \frac{W_B^2}{2L_n^2} - 1 \right) = \frac{W_B^2}{2D_n}$

This is the characteristic time for diffusion across the base. The [charge-control model](@entry_id:1122284) provides a crucial link between the static (DC) behavior of the transistor and its dynamic (AC and transient) performance, as $\tau_T$ is a primary factor determining the device's cutoff frequency.

### Non-Ideal Effects and Second-Order Models

The ideal model provides a solid foundation, but real transistors exhibit behaviors that require more detailed analysis. We now consider two important non-ideal effects.

#### Base-Width Modulation: The Early Effect and Output Resistance

Our ideal model predicts that $I_C$ depends on $V_{BE}$ but not on the collector-emitter voltage, $V_{CE}$. This would imply an infinite small-signal output resistance $r_o = (\partial I_C / \partial V_{CE})^{-1}$. In reality, $r_o$ is finite. This is due to **base-width modulation**, also known as the **Early effect**.

The width of the reverse-biased collector-base depletion region depends on the voltage across it, $V_{CB}$. As $V_{CE}$ increases (for fixed $V_{BE}$), $V_{CB}$ increases, causing the depletion region to widen. Since the junction is typically one-sided ($N_C \gg N_B$), this widening occurs primarily by extending into the more lightly doped base. This encroachment reduces the effective width of the quasi-neutral base, $W_B$.

From the short-base model, we know $I_C \propto 1/W_B$. Therefore, as $V_{CE}$ increases, $W_B$ decreases, and $I_C$ increases. This gives the $I_C$-$V_{CE}$ curves a finite, positive slope. The output conductance is $g_o = \partial I_C / \partial V_{CE}$. Using the [chain rule](@entry_id:147422):

$g_o = \frac{dI_C}{dW_B} \frac{\partial W_B}{\partial V_{CE}} = \left(-\frac{I_C}{W_B}\right) \frac{\partial W_B}{\partial V_{CE}}$

The **Early voltage**, $V_A$, is formally defined from this physical mechanism:

$V_A \equiv -W_B \left( \frac{\partial W_B}{\partial V_{CE}} \right)^{-1}$

Geometrically, $V_A$ is the voltage on the $-V_{CE}$ axis where the extrapolated $I_C$-$V_{CE}$ curves for a given $V_{BE}$ would intersect. From this definition, we immediately recover the well-known circuit model relationship for the output resistance:

$r_o = \frac{1}{g_o} = \frac{V_A}{I_C}$

This shows that the finite output resistance of a BJT is a direct consequence of the physics of [diffusion current](@entry_id:262070) and the voltage-dependent nature of depletion regions.

#### Recombination in the Emitter-Base Space-Charge Region

The ideal model accounts for recombination in the quasi-neutral base (via $\alpha_T$) and hole injection into the emitter (via $\gamma$), both of which contribute to the base current. However, there is a third, often significant, component: recombination of electrons and holes within the forward-biased emitter-base [space-charge region](@entry_id:136997) (SCR).

The net recombination rate is given by the **Shockley-Read-Hall (SRH)** theory. For a single trap level at energy $E_t$, the rate is:

$U_{SRH} = \frac{np - n_i^2}{\tau_p(n+n_1) + \tau_n(p+p_1)}$

where $\tau_n$ and $\tau_p$ are the minority carrier lifetimes, and $n_1$ and $p_1$ are carrier concentrations when the Fermi level aligns with the trap level. In the SCR under [forward bias](@entry_id:159825) $V_{BE}$, the product $np = n_i^2 \exp(V_{BE}/V_T)$ is constant, while $n$ and $p$ vary dramatically with position. The total recombination current is found by integrating this rate across the SCR width, $W_{EB}$:

$I_{B,rec} = qA \int_{SCR} U_{SRH}(x) dx$

Evaluating this integral is complex, but we can determine its voltage dependence. The [recombination rate](@entry_id:203271) $U_{SRH}$ is maximized at the point in the SCR where the denominator is smallest. For the common case of traps near mid-gap ($E_t \approx E_i$) and roughly equal lifetimes ($\tau_n \approx \tau_p = \tau$), the denominator is minimized where $n \approx p$. This occurs where $n(x) \approx p(x) \approx n_i \exp(V_{BE}/(2V_T))$. At this point, the [recombination rate](@entry_id:203271) is strongly peaked and has a voltage dependence of approximately $\exp(V_{BE}/(2V_T))$. Since the integral is dominated by the contribution from this peak, the total SCR recombination current exhibits a characteristic voltage dependence:

$I_{B,rec} \propto \exp\left(\frac{qV_{BE}}{2k_B T}\right)$

This is in contrast to the ideal diffusion currents ($I_C$, and the other components of $I_B$) which are proportional to $\exp(V_{BE}/V_T)$. The general current-voltage relationship is often written as $I \propto \exp(qV/\eta k_B T)$, where $\eta$ is the **ideality factor**. We see that the SCR recombination current has an ideality factor of $\eta = 2$.

The total base current is the sum of these components, so its ideality factor is generally between 1 and 2. At low forward biases, the $\eta=2$ recombination current often dominates, while at higher biases, the $\eta=1$ diffusion currents take over. This is a key non-ideal characteristic observed in the Gummel plot of a practical BJT.