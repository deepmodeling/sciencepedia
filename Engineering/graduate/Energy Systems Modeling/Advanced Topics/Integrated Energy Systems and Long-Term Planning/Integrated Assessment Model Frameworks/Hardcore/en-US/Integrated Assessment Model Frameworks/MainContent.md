## Introduction
Integrated Assessment Models (IAMs) represent one of the most crucial tools for understanding and addressing the long-term challenge of climate change. By quantitatively linking the complex dynamics of human socioeconomic systems—such as the global economy and energy sector—with the physical processes of the Earth's climate system, IAMs provide a structured framework for exploring the consequences of our collective choices. However, their complexity can often make them appear as "black boxes," obscuring the critical assumptions and mechanisms that drive their results. This article aims to demystify these models, providing a graduate-level overview of their internal architecture, practical applications, and the economic principles that guide them.

The following chapters will systematically unpack the IAM framework. First, **"Principles and Mechanisms"** will dissect the core architecture of IAMs, tracing the causal chain from economic activity to climate impacts and exploring the normative foundations of [policy optimization](@entry_id:635350). Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these models are used in practice to develop global scenarios, evaluate policy instruments, and analyze key sectors like energy. Finally, **"Hands-On Practices"** will offer a chance to engage directly with the core concepts through targeted problems, solidifying the theoretical knowledge gained. By the end of this exploration, you will have a robust conceptual understanding of how IAMs function as indispensable laboratories for [climate policy analysis](@entry_id:1122478).

## Principles and Mechanisms

Integrated Assessment Models (IAMs) are complex analytical tools that link human systems (such as the economy and energy sector) with Earth systems (such as the carbon cycle and climate). As established in the introduction, their purpose is to explore the long-term, large-scale consequences of different socioeconomic and technological trajectories, and to inform policy decisions concerning climate change. This chapter delves into the core principles and mechanisms that constitute the internal architecture of these models. We will dissect the fundamental building blocks of IAMs, explore the causal chain linking human activity to climate impacts and back, examine the normative foundations of [policy optimization](@entry_id:635350), and discuss the practical challenges of model construction, computation, and uncertainty.

### Core Architecture of Integrated Assessment Models

At their core, IAMs are formal representations of coupled, dynamic systems. They can be abstractly described using a [state-space](@entry_id:177074) formulation, where the state of the entire world system at time $t$ is captured by a state vector $s_t$. This vector includes physical [state variables](@entry_id:138790) (e.g., atmospheric carbon concentration, global temperature) and economic [state variables](@entry_id:138790) (e.g., capital stock). The evolution of the system is driven by a control vector $u_t$, which represents choices made within the system, such as investment or emissions abatement levels. The system transitions from one state to the next according to a set of equations, $s_{t+1} = F(s_t, u_t)$, which represent physical laws, economic production, and behavioral relationships.

Within this general framework, two primary archetypes of IAMs can be distinguished based on their fundamental objectives and solution concepts: optimization-based models and simulation-based models .

**Optimization-based IAMs**, such as the Dynamic Integrated Climate-Economy (DICE) model, are primarily **normative** in nature. They are formulated as optimal control problems where a hypothetical benevolent social planner chooses the [control path](@entry_id:747840) $\{u_t\}$ over a long time horizon to maximize a [social welfare function](@entry_id:636846). This function is typically a sum of discounted utilities of consumption, for example, $W = \sum_{t=0}^{\infty} \beta^t U(C_t)$. In this structure, the planner makes decisions fully aware of the coupled dynamics of the entire system. Feedbacks, such as the economic damages caused by climate change, are endogenously incorporated into the optimization. The solution to this problem is an optimal, dynamically consistent policy path that satisfies a set of necessary conditions (e.g., Euler-Kuhn-Tucker conditions). This approach seeks to identify the "best" course of action, given the model's assumptions and the specified welfare objective.

**Simulation-based IAMs**, such as the Global Change Analysis Model (GCAM), are primarily **descriptive** or **projective**. They do not solve for a single, intertemporally optimal path by maximizing a global welfare function. Instead, they simulate the evolution of the system under a set of exogenously specified scenarios or policies. These models often feature a high degree of sectoral and technological detail, representing the decisions of multiple, decentralized agents (e.g., firms, households) who may be optimizing their own objectives myopically (e.g., minimizing costs in the current period). The model advances period by period, solving for a market-clearing equilibrium at each step. The modules within the model are often coupled sequentially or through an iterative process until a consistent state is reached for a given time period. The solution is a recursive path that describes a plausible future conditional on the scenario assumptions, rather than a globally optimal one.

### The IAM Causal Chain: From Economy to Climate and Back

To understand the mechanics of any IAM, it is useful to trace the primary causal chain that links economic activity to climate change, and then feeds back to affect the economy. This loop is the fundamental feedback mechanism that IAMs are designed to capture .

#### Emissions Accounting: Linking Economic Activity to Emissions

The first link in the chain is the quantification of greenhouse gas (GHG) emissions arising from economic activities. The fundamental principle is an **emissions accounting identity**, where total emissions $E_t$ in a period $t$ are the sum of emissions from all sectors $s$ within the model's boundary. For each sector, emissions are calculated as the product of an **activity level** ($A_{s,t}$) and a corresponding **emission factor** ($F_{s,t}$) :

$E_t = \sum_{s \in \mathcal{S}} F_{s,t} A_{s,t}$

The activity level $A_{s,t}$ is a [physical measure](@entry_id:264060) of the process driving emissions, such as the amount of fuel combusted (in joules or tonnes), tonnes of cement produced, or hectares of forest cleared. The emission factor $F_{s,t}$ represents the mass of GHG emitted per unit of activity (e.g., kg $\text{CO}_2$ per GJ of natural gas). Emission factors can change over time due to technological progress (e.g., improved efficiency, deployment of carbon capture).

A critical element in this accounting is the definition of the **system boundary**. Most IAMs, in line with IPCC guidelines for national inventories, use a **territorial, production-based** accounting framework. This means the inventory includes all emissions produced within a given geographical boundary (e.g., a country), attributed to the producer of those emissions. In this framework:
- Emissions from industrial processes, such as the [calcination](@entry_id:158338) of limestone in cement production ($CaCO_3 \rightarrow CaO + CO_2$), are accounted for based on physical output (tonnes of [clinker](@entry_id:153294)), separate from the energy used in the process.
- Emissions from electricity generation are attributed to the power supply sector, not the sectors that consume the electricity.
- Emissions embodied in imported goods are excluded, while those in exported goods are included.

Special care must be taken with biogenic carbon from the **Land-Use, Land-Use Change, and Forestry (LULUCF)** sector. To avoid double-counting, the net flux of carbon between the biosphere and atmosphere is accounted for in the LULUCF sector. This includes emissions from deforestation and soil degradation, as well as removals from [afforestation](@entry_id:1120871) and forest growth. Consequently, when biomass is combusted for energy, the resulting $\text{CO}_2$ emissions are reported as zero in the energy sector, as the carbon has already been accounted for as a stock change in the LULUCF sector .

#### The Climate System: From Emissions to Temperature

Once emissions are accounted for, IAMs employ simplified climate modules to translate these emissions into changes in global temperature. This part of the causal chain involves three key steps.

First, emissions are translated into atmospheric GHG concentrations. This is governed by the **carbon cycle**. While complex Earth System Models simulate this in great detail, IAMs often use [reduced-form models](@entry_id:137045), such as **impulse-response functions (IRFs)**. An IRF describes the fraction of a pulse of emitted $\text{CO}_2$ that remains in the atmosphere over time. The total concentration change is the sum (or convolution) of the effects of all past emissions, accounting for the partial uptake of $\text{CO}_2$ by land and ocean sinks .

Second, the increased GHG concentration is translated into a change in the Earth's energy balance, known as **radiative forcing**. For $\text{CO}_2$, this relationship is well-established to be logarithmic, a consequence of absorption band saturation. The standard formula used in many IAMs is :

$F_t = \kappa \ln\left(\frac{C^{\text{atm}}_t}{C^{\text{atm}}_{\text{pre}}}\right)$

Here, $C^{\text{atm}}_t$ is the atmospheric concentration at time $t$, $C^{\text{atm}}_{\text{pre}}$ is the pre-industrial reference concentration, and $\kappa$ is a calibration constant. The physical reason for the logarithmic form is that the main absorption bands for $\text{CO}_2$ (notably around the $15\,\mu\text{m}$ wavelength) are already largely saturated. Additional $\text{CO}_2$ molecules therefore have their greatest effect by broadening the absorption lines and capturing radiation in the "wings" of the absorption bands, an effect that yields a diminishing marginal forcing for each additional unit of concentration. Given the empirically estimated forcing for a doubling of $\text{CO}_2$, $F_{2\times} \approx 3.71 \, \text{W m}^{-2}$, the constant can be calculated as $\kappa = F_{2\times} / \ln(2) \approx 5.35 \, \text{W m}^{-2}$.

Third, radiative forcing is translated into a change in global mean surface temperature. IAMs typically use simple **energy balance models (EBMs)** to capture this dynamic. The simplest is the one-box EBM, which represents the atmosphere and [ocean mixed layer](@entry_id:1129065) as a single [heat reservoir](@entry_id:155168) :

$C \frac{dT_s(t)}{dt} = F(t) - \lambda T_s(t)$

In this equation, $T_s(t)$ is the global mean surface temperature anomaly. The left-hand side represents the rate of energy storage in the system, where $C$ is the **effective areal heat capacity** of the system (in $\text{J m}^{-2} \text{K}^{-1}$), capturing its thermal inertia. The right-hand side is the net energy flux. $F(t)$ is the incoming radiative forcing. The term $-\lambda T_s(t)$ represents the primary stabilizing feedback: as the Earth warms, it radiates more energy back to space. The **[climate feedback parameter](@entry_id:1122450)**, $\lambda$ (in $\text{W m}^{-2} \text{K}^{-1}$), quantifies this response. The equilibrium temperature change for a constant forcing $F_0$ is simply $T_s^* = F_0 / \lambda$. More complex two-box models add a deep-ocean reservoir to better capture the transient dynamics of ocean heat uptake .

#### Climate Impacts: From Temperature to Economic Damages

The final link in the causal chain closes the loop, mapping the change in temperature back to an impact on the socioeconomic system. This is accomplished through a **damage function**, which quantifies the economic losses associated with climate change. These losses can arise from a wide range of impacts, including reduced agricultural productivity, [sea-level rise](@entry_id:185213), increased frequency of extreme weather events, and impacts on human health.

Two common functional forms are used for damages in IAMs: additive and multiplicative .
- **Additive damages** subtract an absolute amount of output that depends on temperature: $Y_t^{\text{net}} = Y_t^{\text{gross}} - \Delta(T_t)$.
- **Multiplicative damages** reduce gross output by a fraction that depends on temperature: $Y_t^{\text{net}} = Y_t^{\text{gross}}(1 - \Lambda(T_t))$.

The choice between these forms has significant implications for how damages scale with economic growth. Under the multiplicative specification, the absolute marginal damage of an extra degree of warming (in dollars) is proportional to gross output ($-\partial Y_t^{\text{net}}/\partial T_t = -Y_t^{\text{gross}} \Lambda'(T_t)$). This means that a richer world will experience larger absolute losses from the same amount of warming. Under the additive specification, the absolute marginal damage is independent of the level of gross output ($-\partial Y_t^{\text{net}}/\partial T_t = -\Delta'(T_t)$). This implies that as the world gets richer, the economic cost of climate change becomes smaller in relative terms. This distinction significantly affects the calculation of the Social Cost of Carbon (SCC), as the multiplicative form tends to produce a higher SCC in a growing economy compared to the additive form .

### The Normative Core: Welfare Economics in Optimization IAMs

For optimization-based IAMs, the "planner's problem" requires specifying a social objective. This is grounded in the principles of welfare economics, particularly regarding the aggregation of well-being across time and individuals.

#### The Social Welfare Function: Aggregating Utility

The standard approach in IAMs is to use a time-separable, discounted utilitarian [social welfare function](@entry_id:636846) :

$W = \sum_{t=0}^{\infty} \beta^{t} U(C_t)$

Here, $U(C_t)$ is the utility derived from per-capita consumption $C_t$ at time $t$, and $\beta$ is a discount factor reflecting pure time preference. The shape of the [utility function](@entry_id:137807) $U(C)$ is critically important, as it encodes the planner's aversion to both risk and inequality.

**Risk aversion** relates to uncertainty in consumption at a single point in time. **Inequality aversion** relates to the distribution of consumption across different individuals at a single point in time. Both concepts are governed by the curvature of the utility function, a property known as **[diminishing marginal utility](@entry_id:138128) of consumption**. A strictly concave [utility function](@entry_id:137807) ($U''(C)  0$) implies that an additional dollar of consumption provides more utility to a poor person (or in a low-consumption state of the world) than to a rich person (or in a high-consumption state).

By Jensen's inequality, a concave $U(C)$ means that [expected utility](@entry_id:147484) is less than the utility of expected consumption ($\mathbb{E}[U(C)]  U(\mathbb{E}[C])$), which defines [risk aversion](@entry_id:137406). Similarly, it means that the total utility from an unequal distribution of consumption is less than the utility from an equal distribution with the same total consumption ($\sum U(C_i)  N \cdot U(\bar{C})$), which defines inequality aversion.

A more curved (more concave) [utility function](@entry_id:137807) implies a more rapid decline in marginal utility, and thus a stronger aversion to both risk and inequality. The canonical utility function used in most IAMs is the **Constant Relative Risk Aversion (CRRA)** function :

$U(C) = \frac{C^{1-\eta}}{1-\eta} \quad (\text{for } \eta \neq 1), \quad U(C) = \ln(C) \quad (\text{for } \eta = 1)$

In this formulation, the parameter $\eta$ is the (constant) elasticity of the marginal utility of consumption, and it serves as the single parameter governing both the coefficient of [relative risk](@entry_id:906536) aversion and the degree of inequality aversion.

#### Discounting: Valuing the Future

One of the most consequential components of an optimization IAM is how it values future costs and benefits relative to present ones. This is determined by the **[social discount rate](@entry_id:142335)**. This is not a single, fixed number but an emergent property of the optimal growth path. The instantaneous [social discount rate](@entry_id:142335) for consumption, $r_t$, can be derived through the **Ramsey rule** :

$r_t = \rho + \eta g_t$

This fundamental equation states that the rate at which we should discount future consumption benefits has two components:
1.  $\rho$: The **pure rate of time preference**. This parameter captures reasons we might value utility today more than utility tomorrow, even if consumption levels were the same. It can reflect pure impatience, or it can be interpreted as a proxy for existential risks (e.g., the probability of an asteroid strike that ends civilization).
2.  $\eta g_t$: The **wealth effect**. This component arises from the combination of economic growth and [diminishing marginal utility](@entry_id:138128). If the economy is growing ($g_t = \dot{c}/c > 0$), future generations will be richer. Due to [diminishing marginal utility](@entry_id:138128) (quantified by $\eta$), an extra dollar of consumption will be worth less to them than it is to us today. Therefore, we discount future consumption benefits more heavily when growth is high and when our aversion to inequality (across time) is strong.

The choice of $\rho$ and $\eta$ is a subject of intense ethical debate, as these parameters have a profound impact on the optimal level of climate mitigation recommended by an IAM.

### Model Formulation and Implementation

Bringing these conceptual pieces together into a functioning model requires careful formalization and computational strategies.

#### Constructing a Well-Posed Model

To be solvable, a minimal dynamic IAM must be a well-posed system of equations. This requires a complete specification of its core components :
- **State Variables**: These define the state of the system at any time $t$. A minimal set includes economic capital ($K_t$), atmospheric carbon stock ($C^{\text{atm}}_t$), and global temperature ($T_t$).
- **Control Variables**: These are the choice variables. A minimal set includes investment ($I_t$) and the emissions abatement rate ($\mu_t$). These must have feasible bounds (e.g., $I_t \ge 0$ and $0 \le \mu_t \le 1$).
- **Laws of Motion**: A set of difference or differential equations describing how the [state variables](@entry_id:138790) evolve over time based on their current values and the chosen controls. This includes the capital accumulation equation, the [carbon cycle model](@entry_id:1122069), and the [energy balance model](@entry_id:195903).
- **Constraints**: A set of algebraic equations that must hold at each point in time. These include resource constraints (e.g., total output must be allocated among consumption, investment, and abatement costs), physical feasibility constraints (e.g., capital stock cannot be negative), and accounting identities.
- **Initial and Terminal Conditions**: The values of all [state variables](@entry_id:138790) must be specified at the beginning of the time horizon, and boundary conditions may be required at the end.

A complete and scientifically consistent specification of these elements ensures that the model is mathematically coherent and can, in principle, be solved.

#### Computational Coupling Strategies

IAMs are by definition modular, coupling distinct models of the economy, energy system, and climate. The strategy used to link these modules computationally involves significant trade-offs .

- **Hard Coupling**: This approach combines all equations and constraints from all modules into a single, large-scale system. This monolithic system is then solved simultaneously for all variables. If a solution is found, it is guaranteed to be internally consistent by construction. However, this method can be computationally prohibitive due to the size and complexity of the joint problem.

- **Soft Coupling**: This is the simplest but least rigorous approach. It involves a single, feed-[forward pass](@entry_id:193086) through the modules. For example, an economic model generates an emissions path, which is fed into a climate model to get a temperature path. There is no feedback. This method has the lowest computational cost but is inherently inconsistent, as the inputs and outputs of the modules are not mutually aligned.

- **Iterative Coupling**: This is a common intermediate approach. Modules are run sequentially in a loop, with the outputs of one module becoming the inputs for the next in the subsequent iteration. This process continues until the shared variables exchanged between modules converge to a stable fixed point. If the iteration converges, the resulting solution is internally consistent. However, convergence is not guaranteed and depends on the mathematical properties of the inter-module mapping. The computational cost depends on the number of iterations required.

#### Navigating Uncertainty

Finally, it is crucial to recognize that IAMs are characterized by deep uncertainty. Understanding the different sources of uncertainty and how they propagate to model outputs is essential for a credible interpretation of the results . We distinguish three main types:

- **Parametric Uncertainty**: This refers to uncertainty in the values of specific parameters within a fixed model structure, such as the equilibrium climate sensitivity, the damage function curvature, or the rate of time preference ($\rho$). This uncertainty propagates through the model's equations, and its impact on outputs like the SCC and temperature can be highly non-linear, often creating skewed or fat-tailed output distributions.

- **Structural Uncertainty**: This is uncertainty about the fundamental structure of the model itself—the choice of equations, functional forms, and included mechanisms. For example, different IAMs may use different types of damage functions or different representations of the carbon cycle. This "between-model" uncertainty often accounts for a large part of the total variance in policy-relevant outputs and cannot be reduced simply by collecting more data to constrain the parameters of a single, potentially misspecified, model.

- **Scenario Uncertainty**: This refers to uncertainty about the future trajectory of exogenous drivers, such as population growth, technological change, and socioeconomic policies. Different baseline scenarios create different contexts for climate policy. For example, the SCC is a marginal concept evaluated along a specific baseline; a scenario of rapid economic growth will typically yield a different SCC than a scenario of stagnation, because the wealth and background emissions levels are different. This type of uncertainty reflects our fundamental inability to predict the long-term evolution of human society.

A comprehensive analysis using IAMs must therefore move beyond single, deterministic "best-guess" projections and instead employ techniques like sensitivity analysis and scenario ensembles to explore the full space of possibilities defined by these interacting uncertainties.