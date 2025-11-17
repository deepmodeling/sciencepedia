## Introduction
Mixing problems provide a classic and powerful application of [first-order ordinary differential equations](@entry_id:264241), allowing us to model the dynamic change of a substance's concentration in a system over time. From tracking a pollutant in a lake to predicting the level of a drug in a patient's bloodstream, the ability to mathematically describe these processes is crucial across many scientific and engineering disciplines. A common challenge, however, is translating the physical setup of inflow, outflow, and internal reactions into a coherent mathematical framework. This article bridges that gap by systematically developing the theory and application of mixing models.

In the following chapters, you will build a comprehensive understanding of this topic. The first chapter, **Principles and Mechanisms**, establishes the foundational [mass balance equation](@entry_id:178786) and walks through the construction of differential equations for single-compartment, multi-compartment, and more complex variable-parameter systems. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the remarkable versatility of these models by exploring their use in fields ranging from medicine and [chemical engineering](@entry_id:143883) to environmental safety and finance. Finally, in **Hands-On Practices**, you will have the opportunity to solidify your knowledge by applying these principles to solve a series of guided problems.

## Principles and Mechanisms

Mixing problems represent a fundamental application of [first-order ordinary differential equations](@entry_id:264241), modeling the dynamic change of a substance's quantity within a well-defined volume. These problems are ubiquitous in engineering, chemistry, [environmental science](@entry_id:187998), and biology, describing scenarios from pollutant dispersal in a lake to drug concentration in the bloodstream. The core of solving any mixing problem lies in a single, powerful principle: the **[mass balance equation](@entry_id:178786)**.

### The Fundamental Principle: The Mass Balance Equation

The [mass balance equation](@entry_id:178786) is a statement of conservation. For a given substance (solute) dissolved or suspended in a medium (solvent) within a container or "compartment," the rate at which the mass of the substance accumulates is equal to the rate at which it enters, minus the rate at which it leaves. We can express this fundamental relationship as:

$$
\frac{dA}{dt} = (\text{Rate of mass in}) - (\text{Rate of mass out})
$$

Here, $A(t)$ represents the total mass of the substance in the compartment at time $t$. To translate this principle into a solvable differential equation, we must define the rate terms more precisely. Typically, fluid flows into and out of the compartment at certain volumetric rates. Let $r_{in}$ and $r_{out}$ be the volumetric flow rates (e.g., in liters/minute) of the solution entering and leaving the compartment, respectively.

The rate at which mass enters is the product of the incoming solution's concentration, $c_{in}$, and its flow rate:

$$
\text{Rate of mass in} = c_{in} r_{in}
$$

A crucial assumption in these models is that the substance within the compartment is **perfectly and instantaneously mixed**. This implies that the concentration of the substance is uniform throughout the entire volume at any given moment. Therefore, the concentration of the substance in the outgoing solution is the same as the overall concentration within the compartment. If $V(t)$ is the volume of the solution in the compartment at time $t$, the internal concentration is $C(t) = \frac{A(t)}{V(t)}$. The rate at which mass leaves is thus:

$$
\text{Rate of mass out} = C(t) \cdot r_{out} = \frac{A(t)}{V(t)} \cdot r_{out}
$$

Combining these elements gives the general form of the differential equation for mixing problems:

$$
\frac{dA}{dt} = c_{in} r_{in} - \frac{A(t)}{V(t)} r_{out}
$$

The volume itself may change if the inflow and outflow rates are not equal, following its own simple differential equation: $\frac{dV}{dt} = r_{in} - r_{out}$. Solving this gives $V(t) = V_0 + (r_{in} - r_{out})t$, where $V_0$ is the initial volume.

### Single-Compartment Models with Constant Volume

The most straightforward mixing problems occur when the volume of the solution in the compartment remains constant. This happens when the total volumetric inflow rate equals the total volumetric outflow rate ($r_{in} = r_{out} = r$), making $V(t)$ a constant, $V$.

#### Flushing a Contaminant

Consider the scenario of clearing a contaminant from a fixed-volume system by flushing it with a pure solvent. In this case, the incoming solution is clean, so its contaminant concentration is zero ($c_{in} = 0$). The [mass balance equation](@entry_id:178786) simplifies significantly.

For instance, imagine a sealed laboratory of volume $V = 60 \text{ m}^3$ accidentally filled with an opaque gas. A ventilation system pumps fresh, clear air ($c_{in} = 0$) into the room at a rate $r = 1.5 \text{ m}^3/\text{min}$ while the mixed air is forced out at the same rate [@problem_id:2186776]. If we let $A(t)$ be the amount of opaque gas in the room, the governing equation is:

$$
\frac{dA}{dt} = (0 \cdot r) - \frac{A(t)}{V} r = -\frac{r}{V} A(t)
$$

This is a separable, first-order linear [homogeneous differential equation](@entry_id:176396). The solution, obtained by [separation of variables](@entry_id:148716) or by inspection, is a classic [exponential decay model](@entry_id:634765):

$$
A(t) = A_0 \exp\left(-\frac{r}{V} t\right)
$$

where $A_0$ is the initial amount of the gas. To find the time required to reduce the gas concentration to $5.0\%$ of its initial value, we set $\frac{A(t)}{A_0} = 0.05$.

$$
0.05 = \exp\left(-\frac{1.5}{60} t\right)
$$

Solving for $t$ yields $t = -\frac{60}{1.5} \ln(0.05) = 40 \ln(20) \approx 1.20 \times 10^{2}$ minutes. The term $\frac{V}{r}$ is often called the **[time constant](@entry_id:267377)** or **residence time** of the system, representing the average time a particle of the substance spends in the compartment.

#### Internal Sources and Sinks

The [mass balance equation](@entry_id:178786) can be extended to include internal generation or consumption of the substance. These processes, often chemical or biological in nature, add another rate term to our equation:

$$
\frac{dA}{dt} = (\text{Rate in}) - (\text{Rate out}) + (\text{Rate of generation}) - (\text{Rate of consumption})
$$

Consider a [bioreactor](@entry_id:178780) of fixed volume $V$ where a compound is synthesized at a constant rate $R$ (mass per time). Clean solvent flows in and out at a rate $F$ [@problem_id:2186786]. If $A(t)$ is the mass of the compound, the [mass balance](@entry_id:181721) is:

$$
\frac{dA}{dt} = (0 \cdot F) - \frac{A(t)}{V} F + R \quad \Rightarrow \quad \frac{dA}{dt} + \frac{F}{V}A = R
$$

This is a linear first-order non-homogeneous ODE. Its solution, assuming an initial amount $A(0)=0$, is:

$$
A(t) = \frac{RV}{F}\left(1 - \exp\left(-\frac{F}{V}t\right)\right)
$$

As $t \to \infty$, the exponential term vanishes, and the amount of the compound approaches a **steady-state** or **equilibrium** value, $A_{ss} = \frac{RV}{F}$. This equilibrium occurs when the rate of removal ($F \cdot A_{ss}/V$) exactly balances the rate of generation ($R$).

Conversely, a substance might be consumed internally. In a bioreactor, microorganisms might consume a nutrient at a rate proportional to the total mass of nutrient present, a first-order consumption process with rate $k A(t)$ [@problem_id:2186783]. If nutrient is also added at a constant mass rate $r$ and the volume is constant with no outflow, the equation becomes:

$$
\frac{dA}{dt} = r - kA(t)
$$

This is again a linear ODE, which solves to $A(t) = \frac{r}{k} + \left(A_0 - \frac{r}{k}\right)\exp(-kt)$. The system again approaches a steady state, this time where generation balances consumption.

These effects can be combined. A coolant tank in a nuclear facility might experience a leak of a radioactive isotope, while being simultaneously flushed with pure coolant and experiencing radioactive decay [@problem_id:2186781]. Let's say the isotope leaks in at a rate $R_{in}$ (mass/time), is flushed out at a rate $\frac{r_{out}}{V}A(t)$, and decays radioactively at a rate $\lambda A(t)$, where $\lambda$ is the decay constant. The mass balance is:

$$
\frac{dA}{dt} = R_{in} - \frac{r_{out}}{V}A(t) - \lambda A(t) = R_{in} - \left(\frac{r_{out}}{V} + \lambda\right)A(t)
$$

This demonstrates a crucial concept: for first-order removal processes, the total rate of removal is the sum of the rates of the individual processes. The effective removal rate constant is $k_{eff} = \frac{r_{out}}{V} + \lambda$. The maximum amount of the isotope in the tank occurs at steady state ($dA/dt = 0$), which is $A_{max} = \frac{R_{in}}{k_{eff}} = \frac{R_{in}}{r_{out}/V + \lambda}$.

### Advanced Single-Compartment Models

The complexity of mixing problems increases when parameters such as volume or inflow concentration are no longer constant.

#### Variable Volume

When the inflow and outflow rates differ ($r_{in} \neq r_{out}$), the volume of the solution changes linearly with time: $V(t) = V_0 + (r_{in} - r_{out})t$. The [mass balance equation](@entry_id:178786) becomes:

$$
\frac{dA}{dt} = c_{in}r_{in} - \frac{r_{out}}{V_0 + (r_{in} - r_{out})t}A(t)
$$

This is a linear first-order ODE, but the coefficient of $A(t)$ is now a function of time, so the equation is not separable. We must solve it using an **[integrating factor](@entry_id:273154)**, $\mu(t)$. For an equation of the form $\frac{dA}{dt} + P(t)A = Q(t)$, the [integrating factor](@entry_id:273154) is $\mu(t) = \exp\left(\int P(t) dt\right)$.

In a bakery scenario [@problem_id:2186767], a vat initially with $1000$ L of dough receives a high-spice paste at $20.0$ L/min ($r_{in}$) while dough is extracted at $15.0$ L/min ($r_{out}$). The volume increases over time: $V(t) = 1000 + 5t$. The ODE for the mass of spice, $y(t)$, is:

$$
\frac{dy}{dt} = (0.025 \text{ kg/L}) \cdot (20.0 \text{ L/min}) - \frac{15.0}{1000+5t}y(t) \quad \Rightarrow \quad \frac{dy}{dt} + \frac{15}{1000+5t}y = 0.5
$$

The [integrating factor](@entry_id:273154) is $\mu(t) = \exp\left(\int \frac{15}{1000+5t} dt\right) = \exp(3\ln(1000+5t)) = (1000+5t)^3$. Multiplying the ODE by $\mu(t)$ makes the left side the derivative of a product, $\frac{d}{dt}[\mu(t)y(t)]$, allowing for direct integration to find the solution. The same principle applies to scenarios like a polluted lake with differing river inflow and outflow rates [@problem_id:2186806].

#### Time-Dependent Parameters

The model's versatility allows for other parameters to be functions of time. Consider a [bioreactor](@entry_id:178780) where the incoming nutrient solution has a concentration that increases linearly with time, $c_{in}(t) = kt$ [@problem_id:2186811]. The forcing function of the ODE, $Q(t) = r_{in}c_{in}(t) = r_{in}kt$, is now time-dependent. The solution process remains the same—use an integrating factor—but the final integration step will involve integrating the term $\mu(t)Q(t)$.

A more complex scenario involves a variable outflow rate determined by physical laws. For a cylindrical tank draining through an orifice at its base, **Torricelli's Law** states that the outflow velocity is proportional to the square root of the liquid height, $h$. Thus, the volumetric outflow rate is $r_{out} = \alpha \sqrt{h}$ for some constant $\alpha$ [@problem_id:2186784]. This couples the [mass balance equation](@entry_id:178786) for the solute, $S(t)$, with the volume balance equation for the liquid:

$$
\frac{dS}{dt} = r_{in}c_{in} - \frac{\alpha \sqrt{h}}{A_{tank}h}S \quad \text{and} \quad A_{tank}\frac{dh}{dt} = r_{in} - \alpha\sqrt{h}
$$

While this system can be solved numerically, if the goal is to find the mass of solute as a function of height, $S(h)$, we can use the [chain rule](@entry_id:147422) to change the [independent variable](@entry_id:146806) from $t$ to $h$:

$$
\frac{dS}{dh} = \frac{dS/dt}{dh/dt}
$$

Substituting the expressions for the derivatives gives a single first-order ODE for $S$ as a function of $h$. This powerful technique eliminates time from the problem, directly relating the two state variables of interest.

### Multi-Compartment Systems

Many real-world systems consist of interconnected compartments. For example, drugs distribute between blood plasma and body tissues, and pollutants move between connected lakes. These scenarios are modeled by a **system of [ordinary differential equations](@entry_id:147024)**, where the outflow of one compartment becomes the inflow for another.

Consider a swimming pool (A) and a connected spa (B), exchanging water while the pool also has a [filtration](@entry_id:162013) system removing a dye [@problem_id:2186762]. Let $Q_A(t)$ and $Q_B(t)$ be the mass of dye in each. The rate of change for each is affected by the other:

$$
\frac{dQ_A}{dt} = (\text{in from B}) - (\text{out to B}) - (\text{removed by filter}) = k_B Q_B - (k_A + k_f) Q_A
$$
$$
\frac{dQ_B}{dt} = (\text{in from A}) - (\text{out to A}) = k_A Q_A - k_B Q_B
$$

This is a system of two linear, homogeneous, first-order ODEs with constant coefficients. Such systems can be solved using linear algebra by finding the [eigenvalues and eigenvectors](@entry_id:138808) of the [coefficient matrix](@entry_id:151473), or by the method of elimination.

The **method of elimination** is particularly instructive. In a system of two tanks where salt solution is exchanged and fresh water flows in [@problem_id:2186813], we have a system for the salt masses $x(t)$ and $y(t)$:
$$
\frac{dx}{dt} = ay - bx
$$
$$
\frac{dy}{dt} = cx - dy
$$
We can differentiate the first equation with respect to $t$ and substitute the expression for $dy/dt$ from the second equation. Then, we can use the first equation again to eliminate $y$ entirely, resulting in a single **second-order homogeneous linear ODE** for $x(t)$:
$$
x'' + (b+d)x' + (bd-ac)x = 0
$$
This equation can be solved using its characteristic equation, a familiar technique. Once $x(t)$ is found, $y(t)$ can be determined from the first ODE. This process reveals the deep connection between systems of first-order equations and single higher-order equations. Finding quantities like the maximum amount of salt that ever enters the first tank requires finding the solution $x(t)$ and then using calculus to find its maximum value by setting $x'(t)=0$.