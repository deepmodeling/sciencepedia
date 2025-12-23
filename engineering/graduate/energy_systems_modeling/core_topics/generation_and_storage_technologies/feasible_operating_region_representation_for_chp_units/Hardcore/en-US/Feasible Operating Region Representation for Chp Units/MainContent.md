## Introduction
Combined Heat and Power (CHP) units are cornerstones of energy efficiency, simultaneously producing electricity and useful heat from a single fuel source. Their ability to flexibly trade-off between these two energy vectors makes them valuable assets in modern energy systems. However, to unlock their full potential in system-wide optimization and planning, we must first capture their complex physical capabilities in a mathematically tractable format. The core challenge lies in accurately representing the "[feasible operating region](@entry_id:1124878)"—the complete set of all achievable heat and power output combinations—without creating a model that is too computationally intensive for large-scale problems.

This article provides a comprehensive guide to constructing and applying these crucial models. It bridges the gap between the underlying thermodynamics of CHP units and their practical application in energy [system analysis](@entry_id:263805). Across three chapters, you will learn to build these representations from the ground up and wield them to solve real-world operational challenges.

The journey begins in **"Principles and Mechanisms,"** where we will derive the [feasible operating region](@entry_id:1124878) from the First Law of Thermodynamics. You will learn to translate physical constraints—such as energy conservation, fuel limits, and turbine characteristics—into the linear inequalities that form the boundaries of a convex [polyhedral model](@entry_id:753566), and explore advanced techniques for handling non-convexities. Next, **"Applications and Interdisciplinary Connections"** will demonstrate how this mathematical model becomes a powerful tool for economic dispatch, unit commitment, and [reliability analysis](@entry_id:192790), situating the CHP unit within the broader context of power grids, heat networks, and [environmental policy](@entry_id:200785). Finally, **"Hands-On Practices"** will allow you to apply these concepts through targeted exercises, solidifying your ability to model everything from piecewise-linear approximations to the discrete operational choices inherent in complex CHP plants.

## Principles and Mechanisms

This chapter delves into the fundamental principles and thermodynamic mechanisms that govern the operation of Combined Heat and Power (CHP) units. Our objective is to translate these physical principles into robust mathematical representations suitable for [energy systems optimization](@entry_id:1124494). We will construct the [feasible operating region](@entry_id:1124878)—the set of all achievable steady-state combinations of electrical power and useful heat—from the ground up, starting with the First Law of Thermodynamics and progressively incorporating technology-specific constraints.

### The First Law of Thermodynamics and Efficiency

The foundational principle governing any [energy conversion](@entry_id:138574) device is the First Law of Thermodynamics, which dictates the conservation of energy. For a CHP unit operating in a steady state, the rate of energy entering the system must equal the rate of energy leaving it.

Let us define our primary variables:
- $F$: The rate of chemical energy input from the fuel, typically measured in megawatts based on the fuel's Lower Heating Value (LHV) and denoted as MW$_{\text{fuel}}$.
- $P$: The net electrical power output, measured in megawatts electric (MW$_{\text{e}}$).
- $H$: The useful thermal energy (heat) output rate, measured in megawatts thermal (MW$_{\text{th}}$).

The energy balance for a steady-state CHP unit can be written as:

$F = P + H + L_{\text{loss}}$

where $L_{\text{loss}}$ represents the rate of all unrecovered energy losses, such as heat in exhaust gases, radiation and convection from equipment surfaces, and mechanical friction. For any physically realistic device, these losses are unavoidable, meaning $L_{\text{loss}} > 0$ during operation. At the absolute theoretical limit, $L_{\text{loss}}$ could be zero. Therefore, for any feasible operating point, we have the fundamental inequality:

$P + H \le F$

This inequality establishes that the total useful energy output can never exceed the energy input from the fuel. It represents the primary trade-off between electrical and thermal [power generation](@entry_id:146388): for a given fuel input rate $F$, an increase in $P$ must be accompanied by a decrease in $H$ (or vice-versa), assuming the unit is operating near its energy conversion limit.

From this energy balance, we can define several key performance metrics. The **electric efficiency**, $\eta_e$, and **thermal efficiency**, $\eta_h$, are defined as the ratios of the respective useful outputs to the fuel input. Because the conversion characteristics of a CHP unit depend on its operating point, these efficiencies are functions of $(P,H)$:

$\eta_e(P,H) = \frac{P}{F}$

$\eta_h(P,H) = \frac{H}{F}$

The **total efficiency**, $\eta_{\text{tot}}$, is the ratio of the total useful energy output to the fuel input:

$\eta_{\text{tot}}(P,H) = \frac{P+H}{F} = \eta_e(P,H) + \eta_h(P,H)$

From the energy conservation inequality, it follows directly that $\eta_{\text{tot}}(P,H) \le 1$. In practice, every real-world technology has a maximum achievable total efficiency, $\eta_{\text{max}}$, which is strictly less than 1. This parameter encapsulates the best performance the unit can achieve under optimal conditions .

For modeling purposes, a CHP unit is also constrained by a maximum fuel input rate, $\bar{F}$, due to the physical limits of its fuel handling system and combustor. Combining the fuel limit $F \le \bar{F}$ with the definition of efficiency, we can derive a crucial constraint on the [feasible operating region](@entry_id:1124878). If we consider a simplified model where the total efficiency is approximately constant, $\eta_{\text{tot}}$, over the operating range, the required fuel input is $F = (P+H)/\eta_{\text{tot}}$. The fuel cap then imposes:

$\frac{P+H}{\eta_{\text{tot}}} \le \bar{F} \quad \implies \quad P+H \le \eta_{\text{tot}}\bar{F}$

This [linear inequality](@entry_id:174297) defines a primary boundary of the [feasible operating region](@entry_id:1124878) in the $(P,H)$ plane. It describes a closed half-space. The boundary line, $H = -P + \eta_{\text{tot}}\bar{F}$, has a slope of $-1$. The oriented angle of this boundary line with respect to the positive $P$-axis is $\arctan(-1) = -\frac{\pi}{4}$ [radians](@entry_id:171693), or -45 degrees . This downward-sloping line represents the fundamental trade-off imposed by energy conservation.

### Distinguishing Technology Constraints from System Constraints

When building large-scale energy system models, it is crucial to maintain a modular and clear structure. This involves a strict separation between constraints that are intrinsic to a component and those that arise from its integration into the wider system .

The **Feasible Operating Region (FOR)** of a CHP unit, which we denote as $\mathcal{R}$, is the set of all operating points $(P,H)$ that the unit can physically sustain based on its internal design, thermodynamics, and material limits. These are its **technology-dependent constraints**. Examples include:
- The energy conservation boundary derived above.
- Minimum and maximum power and heat outputs ($P^{\text{min}}, P^{\text{max}}, H^{\text{min}}, H^{\text{max}}$).
- Specific trade-offs between $P$ and $H$ dictated by the prime mover technology (e.g., a turbine's back-pressure characteristics).
- Dynamic limits such as $dP/dt, dH/dt$ and minimum up/down times.

In contrast, **system-level constraints** are not properties of the unit itself but rather requirements imposed by the system in which it operates. These constraints are used by an optimization model to select a specific operating point $(P,H)$ from within the unit's feasible region $\mathcal{R}$. Examples include:
- The [nodal power balance](@entry_id:1128739) (i.e., total generation must meet total demand and losses).
- Reserve requirements for grid stability.
- Fleet-wide emissions caps or other environmental regulations.

Conflating these two types of constraints makes models monolithic, difficult to debug, and conceptually unsound. The feasible region $\mathcal{R}$ describes what a unit *can* do; system constraints dictate what it *must* do in concert with other components.

### Modeling CHP Technologies with Polyhedral Regions

The true [feasible operating region](@entry_id:1124878) of a CHP unit is a complex shape determined by non-linear thermodynamic and mechanical properties. For use in tractable optimization models, particularly linear and mixed-integer linear programs, this true region is typically approximated by a **[convex polygon](@entry_id:165008)** (or more generally, a polyhedron). This polygon is defined by the intersection of a set of linear inequalities.

#### The Back-Pressure Unit: A Fixed Heat-to-Power Ratio

The simplest type of CHP unit is the [back-pressure turbine](@entry_id:1121306). In an idealized model, steam expands to a fixed exhaust pressure, which is determined by the temperature required for the thermal process. The entire exhaust steam flow is then used for heating.

Applying the [steady-flow energy equation](@entry_id:146612) to the turbine-generator and the heat exchanger, we find that both the power output $P$ and the heat output $H$ are proportional to the mass flow rate of the steam, $\dot{m}$. This leads to a direct proportionality between heat and power :

$H = \rho P$

Here, $\rho$ is the **heat-to-power ratio**, a constant determined by the thermodynamic properties of the steam cycle. The [feasible region](@entry_id:136622) for this idealized unit is simply a line segment in the $(P,H)$ plane, bounded by the minimum and maximum power outputs, $P^{\text{min}}$ and $P^{\text{max}}$.

In reality, efficiencies vary with load, causing $\rho$ to fluctuate slightly. To create a more realistic and robust model for optimization, we can introduce a small tolerance band around this ideal line. By allowing for a fractional tolerance $\alpha$, the feasible region becomes a narrow convex quadrilateral defined by two inequalities:

$H \le (1+\alpha)\rho P$

$H \ge (1-\alpha)\rho P$

For example, for a unit with $P = 35\,\text{MW}_\text{e}$, $\rho = 2.4\,\text{MW}_\text{th}/\text{MW}_\text{e}$, and a tolerance of $\alpha = 0.06$, the maximum feasible heat output would be $H_{\text{max}} = (1+0.06) \times 2.4 \times 35 = 89.04\,\text{MW}_\text{th}$ . This polyhedral approximation captures operational flexibility while retaining the linearity required for efficient optimization.

#### The Extraction-Condensing Unit: A Flexible Trade-off

A more flexible and common configuration is the extraction-condensing steam turbine. In this design, a portion of the steam can be extracted from the turbine at an intermediate pressure for heating purposes, while the remaining steam continues to expand through the low-pressure stages to a [condenser](@entry_id:182997) to maximize [power generation](@entry_id:146388). This allows for variable heat-to-power ratios.

The key feature is the trade-off: extracting a marginal amount of steam, $d\dot{m}_{\text{ex}}$, for heating increases the thermal output $H$, but prevents that steam from producing work in the low-pressure turbine stages, thereby decreasing the electrical output $P$. This marginal relationship can be quantified by a **[coupling coefficient](@entry_id:273384)**, $\gamma$, defined as the ratio of power lost to heat gained :

$\gamma = -\frac{dP}{dH}$

This coefficient can be derived from first principles. The marginal power loss $dP$ is the specific work $w_{\text{LP,s}}$ that the extracted steam would have produced in the low-pressure turbine, multiplied by the [mass flow](@entry_id:143424) $d\dot{m}_{\text{ex}}$ and the generator efficiency $\eta_{\text{me}}$. The marginal heat gain $dH$ is the specific enthalpy drop of the extracted steam in the heat exchanger, $(h_{\text{ex}} - h_{\text{ret}})$, multiplied by $d\dot{m}_{\text{ex}}$. The coefficient is thus:

$\gamma = \frac{\eta_{\text{me}} w_{\text{LP,s}}}{h_{\text{ex}} - h_{\text{ret}}}$

This derivation demonstrates how a key parameter in a linearized model is grounded in the physical thermodynamics of the cycle. For example, with a specific electrical energy loss of $\eta_{\text{me}} w_{\text{LP,s}} = 252.2\,\text{kJ/kg}$ and a specific heat delivery of $h_{\text{ex}} - h_{\text{ret}} = 2105\,\text{kJ/kg}$, the coupling coefficient is $\gamma \approx 0.1198$. This means that for every 1 MW of heat extracted, approximately 0.12 MW of electricity generation is sacrificed . This relationship is modeled as a [linear inequality](@entry_id:174297) bounding the upper edge of the [feasible region](@entry_id:136622), often of the form:

$P \le P^{\text{max}} - \gamma H$

### The Complete Convex Polygonal Model

The full [feasible operating region](@entry_id:1124878) for a CHP unit is constructed by taking the intersection of all relevant [linear constraints](@entry_id:636966). This synthesis results in a [convex polygon](@entry_id:165008) in the $(P,H)$ plane, which is the standard representation used in large-scale planning models .

A comprehensive model for an extraction-condensing unit typically includes the following inequalities :

1.  **Maximum Fuel/Energy Limit**: $aP + bH \le c$. This represents the overall energy conversion limit, with coefficients $a$ and $b$ related to the marginal fuel consumption for power and heat.
2.  **Condensing/Extraction Limit**: $P \le P^{\text{max}} - \rho H$. This captures the trade-off where increased heat extraction reduces maximum power output.
3.  **Back-Pressure Limit**: $P \ge \alpha H + \beta$. This lower bound can represent a minimum required power generation that is coupled to heat output, especially in certain operating modes.
4.  **Box Constraints**: $P \ge P^{\text{min}}$, $P \le P^{\text{max}}$, $H \ge H^{\text{min}}$, $H \le H^{\text{max}}$. These are the absolute minimum and maximum outputs determined by equipment ratings.

The values $P^{\text{min}}$ and $H^{\text{min}}$ are not merely small numbers but are dictated by significant physical phenomena. For a unit to operate stably, it must maintain a minimum combustion rate and temperature to avoid [flame extinction](@entry_id:1125060) (a phenomenon related to the **Damköhler number**, which compares flow timescale to chemical reaction timescale). This sets a minimum fuel flow, which translates to a minimum power output $P^{\text{min}}$. Similarly, in heat recovery systems that rely on natural (buoyancy-driven) circulation, a minimum heat flux is required to create a sufficient density difference to overcome frictional losses and sustain flow, thereby establishing $H^{\text{min}}$ . To model the on/off nature of the unit, these constraints are coupled with a binary variable $u \in \{0,1\}$:

$P \ge P^{\text{min}}u \quad \text{and} \quad H \ge H^{\text{min}}u$

Another important constraint arises from metallurgical limits on steam turbine blades. To prevent erosion from wet steam droplets in the final low-pressure stages, manufacturers often mandate that the [mass flow](@entry_id:143424) through these stages must be at least some fraction $\beta$ of the total inlet [mass flow](@entry_id:143424). This imposes an upper limit on the fraction of steam that can be extracted for heating, which can be translated into a linear constraint of the form $H \le \chi P$ .

The intersection of all such inequalities defines the feasible polygon. For instance, consider a region defined by the intersection of $P \le 100 - 0.2H$, $P \ge \max(10, 0.05H+3)$, $H \ge 20$, and $H \le 200$. By finding the vertices where these lines cross, we can precisely map the operating envelope. The area of this polygon—found by integrating the vertical distance between the upper and lower boundaries—quantifies the total operational flexibility of the unit .

### Advanced Topic: Non-Convex Feasible Regions

While convex polygonal models are computationally convenient, the true [feasible operating region](@entry_id:1124878) of a CHP unit is often **non-convex**. Recognizing and modeling these non-convexities is essential for accurate operational planning.

The convex polygonal model, being an intersection of half-spaces, is mathematically guaranteed to be convex. Non-[convexity](@entry_id:138568) in the true [physical region](@entry_id:160106) arises from several sources :

1.  **Discrete Operating Modes**: A complex CHP plant may have multiple distinct modes, such as operating with or without supplementary firing in the heat recovery boiler. Each mode has its own convex [feasible region](@entry_id:136622). The total feasible region of the plant is the **union** of these individual regions. The union of [convex sets](@entry_id:155617) is, in general, not convex.

2.  **Valve-Point Loading**: Large steam turbines admit steam through a series of valves that open sequentially to increase power output. As a valve just begins to open, the steam is throttled, causing a temporary drop in efficiency. This results in a non-concave fuel-power curve and can create "indentations" or forbidden zones in the $(P,H)$ operating map.

These non-convexities cannot be captured by a simple set of linear inequalities. Instead, they require more advanced techniques involving integer variables. A common approach is to use a **disjunctive formulation**.

Consider a scenario where a CHP unit has a "forbidden operating wedge" due to instabilities in a certain range of heat-to-power ratios. This can be modeled by stating that the operating point $(p,h)$ must lie either *below* one line or *above* another line :

$(h \le a_{\text{low}} p + b_{\text{low}}) \quad \lor \quad (h \ge a_{\text{high}} p + b_{\text{high}})$

This logical "OR" creates a non-convex feasible set. To embed this into a Mixed-Integer Linear Program (MILP), we introduce a binary variable $b \in \{0,1\}$ and a sufficiently large positive constant $M$ (the "big-M" method). The disjunction is reformulated as a pair of coupled linear inequalities:

$h \le a_{\text{low}} p + b_{\text{low}} + M b$

$h \ge a_{\text{high}} p + b_{\text{high}} - M(1-b)$

If $b=0$, the first inequality becomes active ($h \le a_{\text{low}}p + b_{\text{low}}$), while the large negative term $-M$ in the second inequality effectively deactivates it. Conversely, if $b=1$, the second inequality becomes active ($h \ge a_{\text{high}}p + b_{\text{high}}$), and the large positive term $+M$ in the first deactivates it. This powerful technique allows for the accurate modeling of complex, non-convex operational envelopes, forming the bridge between detailed physical understanding and practical, large-scale [energy system optimization](@entry_id:1124497).