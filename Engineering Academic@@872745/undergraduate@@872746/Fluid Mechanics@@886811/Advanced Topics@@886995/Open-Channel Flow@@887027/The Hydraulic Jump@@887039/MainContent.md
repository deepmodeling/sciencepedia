## Introduction
Visible in a kitchen sink or at the base of a massive dam, the hydraulic jump is a striking and fundamental phenomenon in fluid mechanics. It marks an abrupt transition where a fast, shallow stream of water suddenly slows and deepens, creating a turbulent, [standing wave](@entry_id:261209). While seemingly chaotic, this transition is governed by precise physical laws. Understanding these laws is essential for engineers who must control high-velocity flows and for scientists seeking to explain natural events.

This article provides a comprehensive exploration of the hydraulic jump. In the **Principles and Mechanisms** chapter, we will delve into the core physics, applying conservation laws of mass, momentum, and energy to derive the governing equations that predict the jump's characteristics. Next, the **Applications and Interdisciplinary Connections** chapter will reveal the jump's vital role in [hydraulic engineering](@entry_id:184767), [water treatment](@entry_id:156740), and natural systems like tidal bores, even highlighting its analogy to shock waves in gas dynamics. Finally, you can test your knowledge with a series of **Hands-On Practices** designed to reinforce these key concepts.

## Principles and Mechanisms

A hydraulic jump is a striking phenomenon of [open-channel flow](@entry_id:267863), representing a rapid and turbulent transition from a high-velocity, shallow (supercritical) flow to a low-velocity, deep (subcritical) flow. This chapter delves into the fundamental physical principles that govern the formation and characteristics of a hydraulic jump. By applying the integral forms of the conservation laws for mass, momentum, and energy to a control volume encompassing the jump, we can derive the quantitative relationships that are essential for engineering analysis and design.

### The Governing Principles: A Control Volume Approach

To analyze the hydraulic jump, we consider a short, horizontal, rectangular channel of constant width. We define a control volume that envelops the jump, with inlet plane 1 located just upstream of the jump (where the flow is supercritical and uniform) and outlet plane 2 located just downstream (where the flow has returned to a subcritical, uniform state).

#### Conservation of Mass

The principle of mass conservation, expressed through the [continuity equation](@entry_id:145242) for steady, incompressible flow, provides the most elementary relationship across the jump. The [volumetric flow rate](@entry_id:265771), $Q$, must be constant. For a channel of width $w$ and depth $y$, with average velocity $v$, the flow rate is $Q = vwy$. Thus, we have:

$Q = v_1 w_1 y_1 = v_2 w_2 y_2$

If we consider a channel of constant width ($w_1 = w_2$), the equation simplifies to conservation of discharge per unit width, $q$:

$q = v_1 y_1 = v_2 y_2$

This simple relationship immediately reveals a key feature of the jump: as velocity decreases from $v_1$ to $v_2$, the depth must correspondingly increase from $y_1$ to $y_2$. More generally, for a channel where both width and velocity may change, the ratio of downstream to upstream depth is inversely proportional to the product of the velocity and width ratios. If we define $\alpha = v_2/v_1$ and $\beta = w_2/w_1$, the [continuity equation](@entry_id:145242) yields the depth ratio as $\frac{y_2}{y_1} = \frac{1}{\alpha \beta}$ [@problem_id:1800311]. While fundamental, the [continuity equation](@entry_id:145242) alone is insufficient to determine the final state of the flow, as it contains two unknowns, $v_2$ and $y_2$.

#### Conservation of Momentum and the Specific Force

The key to solving the hydraulic jump lies in the [momentum equation](@entry_id:197225). The jump occurs over a very short distance, allowing us to neglect the effects of bed friction and air resistance on the [control volume](@entry_id:143882). For a horizontal channel, the net force acting on the fluid within the [control volume](@entry_id:143882) is the difference between the hydrostatic pressure forces at the inlet and outlet. This [net force](@entry_id:163825) must equal the rate of change of momentum flux across the [control volume](@entry_id:143882).

The total force exerted by the fluid on a cross-section, per unit weight of the fluid, is composed of the pressure force and the [momentum flux](@entry_id:199796). This combined quantity is known as the **[specific force](@entry_id:266188)**, $F_s$, and for a rectangular channel, it is expressed per unit width as:

$F_s = \frac{q^2}{gy} + \frac{y^2}{2}$

Here, the term $\frac{y^2}{2}$ represents the hydrostatic pressure force per unit width divided by $\rho g$, and the term $\frac{q^2}{gy}$ represents the [momentum flux](@entry_id:199796) per unit width divided by $\rho g$. The application of the [momentum principle](@entry_id:261235) to the control volume reveals that the [specific force](@entry_id:266188) is conserved across the jump:

$F_{s1} = F_{s2}$

$\frac{q^2}{gy_1} + \frac{y_1^2}{2} = \frac{q^2}{gy_2} + \frac{y_2^2}{2}$

This momentum balance is the central governing equation for the hydraulic jump. It demonstrates that while the individual components of pressure and [momentum flux](@entry_id:199796) change dramatically, their sum remains constant [@problem_id:1800341]. Any two depths, $y_1$ and $y_2$, that satisfy this equation for a given flow rate $q$ are known as **conjugate depths** or sequent depths.

#### The Energy Principle and Dissipation

In stark contrast to momentum, [mechanical energy](@entry_id:162989) is *not* conserved across a hydraulic jump. The intense, chaotic turbulence, characterized by eddies and vortices within the roller of the jump, is a highly effective mechanism for converting mean-flow kinetic energy into thermal energy (heat). This process is irreversible and results in a significant reduction in the [total mechanical energy](@entry_id:167353) of the flow.

The **specific energy**, $E$, is the total mechanical energy head per unit weight of the fluid, relative to the channel bed. For a rectangular channel, it is given by:

$E = y + \frac{V^2}{2g} = y + \frac{q^2}{2gy^2}$

Due to the [turbulent dissipation](@entry_id:261970), the [specific energy](@entry_id:271007) downstream of the jump, $E_2$, is always less than the [specific energy](@entry_id:271007) upstream, $E_1$. The difference, $\Delta E = E_1 - E_2$, is the **head loss** due to the jump. A hydraulic jump is fundamentally an energy-dissipating phenomenon [@problem_id:1800342]. This property is not a drawback; it is, in fact, the primary reason hydraulic jumps are engineered in hydraulic structures like spillways and sluice gates, where they serve to safely dissipate the potentially erosive energy of high-velocity flows.

### The Bélanger Equation: Relating Conjugate Depths

The momentum conservation equation provides the means to derive a direct relationship between the conjugate depths ($y_1$, $y_2$) and the initial flow conditions. We begin with the [specific force](@entry_id:266188) balance:

$\frac{y_1^2}{2} - \frac{y_2^2}{2} = \frac{q^2}{g} \left( \frac{1}{y_2} - \frac{1}{y_1} \right)$

Factoring both sides gives:

$\frac{(y_1 - y_2)(y_1 + y_2)}{2} = \frac{q^2}{g} \frac{(y_1 - y_2)}{y_1 y_2}$

For a jump to occur, $y_1 \neq y_2$, so we can cancel the $(y_1 - y_2)$ term:

$\frac{y_1 + y_2}{2} = \frac{q^2}{g y_1 y_2}$

Recalling that $q = V_1 y_1$, we can substitute $q^2 = V_1^2 y_1^2$. The equation becomes:

$y_2(y_1 + y_2) = \frac{2 V_1^2 y_1}{g}$

To express this in a dimensionless form, we introduce the **Froude number**, $Fr$, which is the ratio of the flow velocity to the celerity (speed) of a small surface wave ($c = \sqrt{gy}$):

$Fr = \frac{V}{\sqrt{gy}}$

The upstream Froude number is $Fr_1 = \frac{V_1}{\sqrt{gy_1}}$, so $V_1^2 = Fr_1^2 g y_1$. Substituting this into the momentum balance yields:

$y_2(y_1 + y_2) = \frac{2 (Fr_1^2 g y_1) y_1}{g} = 2 Fr_1^2 y_1^2$

Dividing by $y_1^2$ and letting $r = y_2/y_1$ gives a quadratic equation for the depth ratio $r$:

$r(1+r) = 2Fr_1^2 \implies r^2 + r - 2Fr_1^2 = 0$

Solving this for the positive root $r$ gives the celebrated **Bélanger equation**:

$\frac{y_2}{y_1} = \frac{1}{2} \left( \sqrt{1 + 8 Fr_1^2} - 1 \right)$

This equation is the cornerstone of [hydraulic jump](@entry_id:266212) analysis in rectangular channels [@problem_id:1800314]. It explicitly connects the ratio of the conjugate depths to a single dimensionless parameter, the upstream Froude number.

A physical jump requires an increase in depth, meaning $y_2 > y_1$, or $\frac{y_2}{y_1} > 1$. Applying this condition to the Bélanger equation:

$\frac{1}{2} \left( \sqrt{1 + 8 Fr_1^2} - 1 \right) > 1 \implies \sqrt{1 + 8 Fr_1^2} > 3 \implies 1 + 8 Fr_1^2 > 9 \implies Fr_1^2 > 1$

Since the Froude number is non-negative, this proves a fundamental requirement: **a [hydraulic jump](@entry_id:266212) can only form if the upstream flow is supercritical ($Fr_1 > 1$)** [@problem_id:1800335]. The jump represents a transition from this supercritical state to a subcritical state ($Fr_2  1$).

### Energy Dissipation in the Hydraulic Jump

With the Bélanger equation, we can now quantify the energy lost in the jump. The [head loss](@entry_id:153362), $\Delta E = E_1 - E_2$, can be derived through algebraic manipulation involving the [specific energy](@entry_id:271007) and momentum equations. The result is a remarkably compact and useful formula:

$\Delta E = \frac{(y_2 - y_1)^3}{4 y_1 y_2}$

Since a jump requires $y_2 > y_1$, this equation mathematically confirms that the [head loss](@entry_id:153362) $\Delta E$ is always positive [@problem_id:1752962]. The energy at the downstream section is always less than the energy at the upstream section.

To assess the efficiency of the jump as an energy dissipator, it is often useful to calculate the fraction of initial [specific energy](@entry_id:271007) that is lost. For instance, consider an upstream flow with a Froude number of $Fr_1 = 3.0$ [@problem_id:1800334] [@problem_id:1752962]. First, we find the depth ratio:

$\frac{y_2}{y_1} = \frac{1}{2} \left( \sqrt{1 + 8 (3.0)^2} - 1 \right) = \frac{1}{2} \left( \sqrt{73} - 1 \right) \approx 3.77$

The initial specific energy is $E_1 = y_1 + \frac{V_1^2}{2g} = y_1 \left( 1 + \frac{Fr_1^2}{2} \right) = y_1 \left( 1 + \frac{3.0^2}{2} \right) = 5.5 y_1$. The head loss is $\Delta E = \frac{(y_2 - y_1)^3}{4 y_1 y_2} = \frac{(3.77y_1 - y_1)^3}{4 y_1 (3.77y_1)} = \frac{(2.77)^3}{4 \times 3.77} y_1 \approx 1.41 y_1$.

The fraction of energy dissipated is then:

$\frac{\Delta E}{E_1} \approx \frac{1.41 y_1}{5.5 y_1} \approx 0.257$

This means that for an upstream Froude number of 3.0, nearly 26% of the incoming [specific energy](@entry_id:271007) is converted to heat through turbulence. For higher Froude numbers, this fraction increases dramatically. For example, for an upstream Froude number of $Fr_1 = 5.0$, the dissipated fraction is approximately 49% [@problem_id:1800342].

In engineering practice, the quantity of interest is often the **rate of energy dissipation** (power). This is calculated by multiplying the [head loss](@entry_id:153362) by the weight flow rate of the fluid. The power dissipated per unit width of the channel, $\dot{E}'$, is:

$\dot{E}' = \rho g q \Delta E$

For a flow with $y_1 = 0.450 \, \text{m}$ and $v_1 = 8.00 \, \text{m/s}$, the upstream Froude number is $Fr_1 \approx 3.81$. The flow rate per unit width is $q = v_1 y_1 = 3.60 \, \text{m}^2/\text{s}$. The conjugate depth is $y_2 \approx 2.21 \, \text{m}$, and the head loss is $\Delta E \approx 1.37 \, \text{m}$. The resulting power dissipation is:

$\dot{E}' = (1000 \, \text{kg/m}^3)(9.81 \, \text{m/s}^2)(3.60 \, \text{m}^2/\text{s})(1.37 \, \text{m}) \approx 48,300 \, \text{W/m} = 48.3 \, \text{kW/m}$ [@problem_id:1752969].

This calculation shows that even in a moderately sized channel, a [hydraulic jump](@entry_id:266212) can dissipate megawatts of power over a full-width spillway, protecting the downstream riverbed from catastrophic erosion.

### Classification of Hydraulic Jumps

The physical appearance and characteristics of a [hydraulic jump](@entry_id:266212) are strongly dependent on the upstream Froude number, $Fr_1$. Based on this parameter, jumps are typically classified as follows:

- **Undular Jump ($1  Fr_1 \le 1.7$)**: The water surface shows smooth, undulating waves. Energy dissipation is minimal.
- **Weak Jump ($1.7  Fr_1 \le 2.5$)**: A small roller begins to form on the surface. The downstream water surface is still relatively smooth.
- **Oscillating Jump ($2.5  Fr_1 \le 4.5$)**: An unstable, oscillating jet enters the jump, creating irregular waves that can propagate far downstream. This can be problematic for channel banks. A jump with $Fr_1 = 3.0$ falls into this category [@problem_id:1800334].
- **Steady Jump ($4.5  Fr_1 \le 9.0$)**: The jump is well-balanced and stable. The position is well-defined, and the [energy dissipation](@entry_id:147406) is substantial (45-70%). This is the ideal range for design purposes.
- **Strong Jump ($Fr_1 > 9.0$)**: The downstream water surface is rough and choppy. The jump action is effective but can be accompanied by spray and entrained air. Energy dissipation can exceed 85%.

### The Submerged Hydraulic Jump

The classical analysis assumes the jump forms freely, with the downstream depth $y_2$ being determined solely by the upstream conditions. However, if the downstream **tailwater depth**, $y_t$, is greater than the required conjugate depth ($y_t > y_2$), the jump cannot form freely. Instead, it is forced upstream and becomes a **submerged** or **drowned jump**.

In a submerged jump, the transition is less abrupt, and the jump is "drowned" by the high tailwater. The simple [specific force](@entry_id:266188) balance and the Bélanger equation no longer apply between the initial depth $y_1$ and the final tailwater depth $y_t$. However, the principles of energy and momentum still hold. Energy is still dissipated, though typically less than in a free jump under the same upstream conditions. If the amount of energy dissipated, $\Delta E$, is known or specified, one can determine the corresponding tailwater depth. The downstream specific energy is $E_t = E_1 - \Delta E$. The tailwater depth $y_t$ must then satisfy the cubic specific energy equation:

$y_t + \frac{q^2}{2 g y_t^2} = E_t$

For a given $q$ and a calculated $E_t$, this equation must be solved for $y_t$. For example, if a flow with $q = 5.00 \, \text{m}^2/\text{s}$ and $y_1=0.500 \, \text{m}$ forms a submerged jump that dissipates 35% of the initial specific energy, the final tailwater depth can be calculated by first finding $E_1$, then $E_t$, and finally solving the cubic equation for the corresponding subcritical depth, which yields $y_t \approx 3.54 \, \text{m}$ [@problem_id:1800325]. This type of analysis is crucial for designing stilling basins that must operate under a variety of tailwater conditions.