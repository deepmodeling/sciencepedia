## Introduction
The representation of technological change is a cornerstone of modern energy [systems analysis](@entry_id:275423), with profound implications for policy design and investment strategy. As the world navigates the transition to a low-carbon future, how we model the evolution of technology costs and performance can either illuminate or obscure the most effective pathways. A critical decision for any modeler is whether to treat technological progress as an external, predetermined force (exogenous) or as a dynamic process that responds to investments and market conditions (endogenous). This choice addresses a fundamental knowledge gap: it determines whether a model can capture the crucial feedback loops where policies not only leverage existing technologies but actively contribute to making future technologies cheaper.

This article provides a comprehensive exploration of these two modeling paradigms. In the first chapter, **Principles and Mechanisms**, we will dissect the fundamental distinction between exogenous and endogenous assumptions, detailing the key mechanisms like learning-by-doing and learning-by-researching that drive endogenous change. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the real-world consequences of this modeling choice for energy and climate policy, and reveal its relevance in fields ranging from economic history to genomics. Finally, the **Hands-On Practices** chapter will offer concrete exercises to build practical skills in simulating and analyzing these dynamic technological processes, cementing the theoretical concepts discussed.

## Principles and Mechanisms

In the modeling of energy systems, the representation of technological change is a critical choice that profoundly influences a model's structure, behavior, and policy implications. The evolution of technology cost and performance can be treated as either an external input to the model or an internal process that responds to the model's own dynamics. This chapter delineates the principles and mechanisms governing these two approaches—exogenous and [endogenous technological change](@entry_id:1124428)—and explores the significant consequences of this modeling decision.

### The Fundamental Distinction: Exogenous versus Endogenous Assumptions

At the most fundamental level, the distinction between exogenous and endogenous technology assumptions lies in whether the parameters governing a technology's cost and performance are independent of the model's decisions.

An **[exogenous technology](@entry_id:1124729) assumption** posits that parameters such as capital cost $p_{i,t}$, operating cost $o_{i,t}$, or efficiency $\eta_{i,t}$ for a given technology $i$ at time $t$ are determined outside the model. These parameters are treated as fixed inputs, often specified as pre-determined trajectories over time or across different scenarios. They do not react to the model's decisions, such as investment in new capacity, the level of generation, or spending on research and development. Formally, if $z$ represents any decision or state variable within the model (e.g., cumulative deployment $Q_{i,t}$ or knowledge stock $S_{i,t}$), an exogenous parameter $\theta_{i,t}$ satisfies the condition $\frac{\partial \theta_{i,t}}{\partial z} = 0$. The technology's progress is an external narrative imposed upon the system . For instance, an exogenous cost trajectory might be specified as a [simple function](@entry_id:161332) of time and a scenario index $s$, such as $c_t = \hat{c}(t,s)$, with no dependence on model-driven deployment .

Conversely, an **endogenous technology assumption** allows these same parameters to evolve as a function of the model's state variables, creating an internal feedback loop. Decisions made within the model, such as deploying a technology, directly influence its future cost and performance. This means that the partial derivative of a technology parameter with respect to at least one state or decision variable is non-zero, e.g., $\frac{\partial p_{i,t}}{\partial Q_{i,t}} \neq 0$. The path of technological progress is thus determined, at least in part, by the model's own solution. This approach transforms technological advancement from a mere assumption into a dynamic outcome of the modeled energy system .

### Mechanisms of Endogenous Technological Change

Several distinct mechanisms have been proposed and are widely used to formalize the process of [endogenous technological change](@entry_id:1124428). These mechanisms provide structured ways to link economic activity to technological progress.

#### Learning-by-Doing: The Experience Curve

The most widely recognized mechanism for endogenous cost reduction is **learning-by-doing** (LBD), which posits that the cost of a technology decreases as the cumulative experience in manufacturing and deploying it grows. This cumulative experience is typically proxied by cumulative installed capacity or cumulative production.

The [canonical representation](@entry_id:146693) of this phenomenon is the experience curve, often referred to as **Wright's Law**. It is mathematically derived from the premise of a constant elasticity of cost with respect to cumulative deployment. If $c_t$ is the unit cost and $Q_t$ is the cumulative deployment, this relationship is defined by the differential equation:
$$
\frac{\partial \ln c_t}{\partial \ln Q_t} = -\lambda
$$
where $\lambda > 0$ is a constant known as the **learning elasticity**. Integrating this equation yields the familiar power-law function:
$$
c_t = c_0 \left(\frac{Q_t}{Q_0}\right)^{-\lambda}
$$
Here, $c_0$ is a reference cost at a reference cumulative deployment $Q_0$ . The cost at any time $t$ is thus an explicit function of the state variable $Q_t$, which itself is the result of past deployment decisions. This functional form is common for representing cost evolution driven by deployment within a model, e.g., $c_t = \phi(Q_{t-1})$ or $c_t = \phi(Q_t)$ where $\phi'  0$ .

A related and more intuitive metric is the **learning rate** ($LR$), defined as the fractional reduction in cost for every doubling of cumulative deployment. The [learning rate](@entry_id:140210) is directly related to the learning elasticity by the formula:
$$
LR = 1 - 2^{-\lambda}
$$
For example, a [learning rate](@entry_id:140210) of $0.20$ implies that costs decrease by 20% each time cumulative deployment doubles. An important property of Wright's Law is that while the *percentage* cost reduction for a doubling of capacity is constant, the *absolute* marginal cost reduction from an additional unit of deployment, given by $\frac{\partial c_t}{\partial Q_t} = -\lambda \frac{c_t}{Q_t}$, diminishes as cumulative deployment $Q_t$ increases. This reflects inherent [diminishing returns](@entry_id:175447) to learning .

#### Learning-by-Researching: The Role of RD

An alternative, complementary driver of technological progress is dedicated Research and Development (RD). This mechanism, termed **learning-by-researching** (LBR), proposes that costs fall as a result of knowledge accumulated through targeted RD efforts.

In this framework, the key state variable is not cumulative deployment but a **knowledge stock**, denoted $K_t$. This stock represents the accumulated body of scientific and engineering knowledge relevant to a technology. It evolves according to its own law of motion, which typically includes accumulation from new RD investments ($R_t$) and depreciation ($\delta$) of old, obsolete knowledge:
$$
K_{t+1} = (1-\delta)K_t + \eta R_t
$$
where $\eta$ is a parameter that translates RD expenditure into new knowledge. The technology's cost is then modeled as a decreasing function of this knowledge stock, for example, using a power-law form analogous to the experience curve: $c_t = \tilde{c}_0 K_t^{-\beta}$, where $\beta > 0$ is the RD learning elasticity .

#### Combining Mechanisms and Inducing Innovation

In reality, technological progress is often driven by both deployment experience and dedicated research. More sophisticated models capture this by incorporating multiple factors. A **[two-factor learning curve](@entry_id:1133539)** combines LBD and LBR into a single cost function:
$$
c_t = c_0 \left(\frac{Q_t}{Q_0}\right)^{-\lambda} \left(\frac{K_t}{K_0}\right)^{-\mu}
$$
Here, the cost reductions from cumulative deployment (with elasticity $\lambda$) and knowledge stock (with elasticity $\mu$) are multiplicatively separable .

A more general framework for understanding how policy influences innovation is **price-induced technological change**. This theory, rooted in microeconomic principles, posits that the direction of innovation is influenced by the relative prices of inputs. For instance, a policy such as a carbon price raises the effective price of carbon-intensive energy. This, in turn, can increase the incentive for firms to invest in RD aimed at improving energy efficiency or developing low-carbon substitutes.

In a [dynamic optimization](@entry_id:145322) context, this mechanism operates through the shadow value of the knowledge stock. A higher energy price increases the cost savings that can be achieved from an improved technology. This higher return to innovation makes RD more attractive. Formally, this "energy-saving bias" of technological change is captured by the cross-partial derivative of the cost function $c(\mathbf{p}, K)$ with respect to the energy price vector $\mathbf{p}$ and the knowledge stock $K$. For price-induced innovation to occur, this derivative must be negative, $\frac{\partial^2 c}{\partial \mathbf{p} \partial K} \prec \mathbf{0}$, meaning that a higher energy price increases the marginal value of the knowledge stock .

### Modeling Implications and Practical Considerations

The choice between exogenous and endogenous assumptions has profound implications for a model's mathematical structure, [computational tractability](@entry_id:1122814), and its suitability for policy analysis.

#### Structural Impact on Optimization Models

A primary consequence of endogenizing technology is the introduction of **nonconvexity**. In an optimization model, the total cost of an activity is often the product of its unit cost and its activity level (e.g., investment cost = $p_t \cdot I_t$). When the unit cost $p_t$ is itself a function of past investments (via cumulative deployment), the objective function contains terms like $p_t(\sum_{\tau't} I_\tau) \cdot I_t$. Because the cost function is decreasing, this creates a situation of [increasing returns](@entry_id:1126450) to scale, where the per-unit cost falls as the scale of activity rises. This violates the convexity assumptions required for many standard, efficient optimization algorithms (such as linear or convex [quadratic programming](@entry_id:144125)), potentially making the model computationally intractable or requiring specialized [global optimization](@entry_id:634460) solvers . Modelers often resort to approximations, such as discretizing the learning curve into a piecewise linear convex function, to maintain computational feasibility .

#### The Lucas Critique and Policy Analysis

A second, more profound implication relates to the validity of using a model for [policy evaluation](@entry_id:136637). The **Lucas Critique** argues that it is naive to try to predict the effects of a change in economic policy entirely on the basis of relationships observed in historical data. The rationale is that the structure of economic models, including the behavioral parameters of agents, depends on the policy regime. When the policy changes, the agents' behavior changes, and thus the model's parameters will change.

This critique is directly applicable to the choice of technology assumption. A model with [exogenous technology](@entry_id:1124729) assumes that the rate of cost reduction is a fixed structural parameter, independent of policy. However, if a new, aggressive climate policy is introduced, it will stimulate deployment and investment in clean technologies, which in turn will accelerate their cost reduction via learning-by-doing. A model with endogenous technology can capture this feedback loop, allowing the rate of technological progress to respond to the policy shift. An exogenous model, by contrast, would fail to capture this acceleration, systematically overestimating the cost of the policy because it ignores the policy's power to "endogenously" make the solution cheaper. For this reason, models with endogenous technology are considered more "structurally robust" for policy analysis, as they internalize a key behavioral response that would otherwise be a source of error .