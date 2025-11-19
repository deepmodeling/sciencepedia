## Introduction
Computable General Equilibrium (CGE) models are powerful computational laboratories for analyzing the economy-wide impacts of policies and [economic shocks](@entry_id:140842). Their significance lies in their ability to move beyond the limitations of partial equilibrium analysis, which examines a single market in isolation. By contrast, CGE models capture the intricate web of connections between all markets, allowing analysts to trace the ripple effects of a change—such as a new tax or a trade agreement—through the entire economic system. This article addresses the challenge of understanding these complex, indirect consequences, which are often overlooked but can be critical for sound policy-making. It provides a structured guide to the theory and practice of CGE modeling.

Across three chapters, you will gain a deep understanding of this essential tool. The "Principles and Mechanisms" chapter lays the theoretical groundwork, explaining the core building blocks of production and consumption, the mechanisms for achieving equilibrium, and advanced extensions that incorporate dynamics and market imperfections. Next, the "Applications and Interdisciplinary Connections" chapter showcases the remarkable versatility of CGE models, exploring their use in public finance, [environmental policy](@entry_id:200785), international trade, and even epidemiology. Finally, the "Hands-On Practices" section offers concrete problems to help solidify your understanding of how to interpret and critically evaluate CGE-based analyses. This journey from foundational theory to real-world application will equip you with the knowledge to appreciate and engage with modern economic policy analysis.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that form the engine of a Computable General Equilibrium (CGE) model. We move from the foundational building blocks that represent economic activity—production technologies and consumer preferences—to the overarching rules that ensure a coherent and complete representation of the macroeconomy. We then explore how this core framework can be extended to incorporate more complex and realistic features, such as dynamic adjustments, imperfect competition, and market frictions. Finally, we address the practical aspects of [model parameterization](@entry_id:752079) and its application to nuanced policy analysis.

### Core Building Blocks: Production, Consumption, and Trade

At its core, a CGE model is a numerical representation of an economy's network of production, consumption, and trade activities. The behavior of firms and households is typically described by micro-founded optimization problems, subject to technological and budgetary constraints.

#### Production Technology and Nesting Structures

The productive capacity of an economy is represented by **production functions**, which describe how firms transform inputs (like capital and labor) into outputs. While a [simple function](@entry_id:161332) like the **Cobb-Douglas** production function, $Y = A K^{\alpha} L^{1-\alpha}$, is a common starting point, its assumption of a unitary elasticity of substitution between inputs is often too restrictive.

To allow for greater flexibility, CGE models widely employ the **Constant Elasticity of Substitution (CES)** function. The CES function allows the modeler to specify the degree of substitutability between inputs through an elasticity parameter, $\sigma$. This is crucial for realistic policy analysis, as the ease with which firms can substitute away from an input whose price has risen (e.g., due to a tax) determines the ultimate economic impact.

Real-world production processes are complex, often involving many stages and types of inputs. CGE models capture this complexity through **nested production structures**. In a nested structure, composites of inputs are first formed at lower levels, and these composites then serve as inputs at higher levels. Each nest is typically represented by a CES function, potentially with a different substitution elasticity.

A common and powerful example is a three-level nested structure [@problem_id:2380395]. Imagine a firm producing gross output.
1.  **Top Nest**: At the highest level, the firm combines a value-added composite (e.g., capital and labor) with an intermediate input composite (e.g., energy and raw materials) to produce gross output. The elasticity of substitution here, $\sigma_T$, determines how easily the firm can switch between its own value-added and purchasing intermediates from other sectors.
2.  **Value-Added Nest**: The value-added composite is itself produced by combining primary factors, typically capital ($K$) and a labor composite ($L$). The elasticity $\sigma_V$ in this nest governs the capital-labor substitution, a critical parameter for analyzing long-run adjustments to changes in factor prices.
3.  **Labor Nest**: The labor composite can be further disaggregated, for instance, into skilled labor ($L_S$) and unskilled labor ($L_U$). The elasticity $\sigma_L$ in this nest captures the degree to which firms can substitute between different types of workers in response to changes in their relative wages, a key mechanism when analyzing policies like skill-specific wage subsidies.

A key concept in working with these structures is **duality**. Corresponding to a CES quantity aggregator for inputs, there is a CES unit-cost aggregator for prices. For two inputs with prices $p_1$ and $p_2$, share parameter $\alpha$, and elasticity $\sigma \neq 1$, the unit cost of the composite is given by:
$$
P(\alpha, \sigma; p_1, p_2) = \left[ \alpha p_1^{1-\sigma} + (1-\alpha) p_2^{1-\sigma} \right]^{\frac{1}{1-\sigma}}
$$
This dual approach is computationally convenient, allowing us to calculate the aggregate price index for a composite good directly from the prices of its components. By working from the bottom nest upwards, we can determine the final price of gross output based on the prices of all primary factors and intermediate inputs [@problem_id:2380395].

This principle of nesting can be applied to any input. For example, the aggregate capital stock is often disaggregated into different types, as they have different economic characteristics and are affected differently by policy. A model might disaggregate capital services ($K$) into equipment ($K_E$), structures ($K_S$), and intellectual property ($K_P$) [@problem_id:2380416]. Each type has a distinct depreciation rate ($\delta_i$) and may be targeted by different tax policies, like an investment tax credit ($\tau_i$). The **user cost of capital** for each type—the effective rental price a firm pays to use one unit of capital for a period—is determined by the world interest rate ($r$), its depreciation rate, and any relevant taxes or subsidies. For a capital type $i$, this is given by:
$$
R_i = \frac{r + \delta_i}{1 - \tau_i}
$$
These different capital types are then aggregated, often using a CES function, to form the total capital services that enter the top-level production function. This detailed approach is essential for accurately analyzing the impact of investment-related policies.

#### Consumption, Preferences, and the Armington Assumption

On the demand side, household behavior is governed by **utility functions**, which represent preferences over different goods and leisure. Just as with production, these are often specified using nested CES structures to allow for varying degrees of substitutability.

A particularly important application of this idea in CGE modeling is the **Armington assumption**, which addresses international trade [@problem_id:2407868]. Instead of assuming that imported goods and domestically produced goods are [perfect substitutes](@entry_id:138581) (the "law of one price"), the Armington model treats them as distinct varieties of the same good. For instance, consumers might perceive American-made cars and Japanese-made cars as similar but not identical. A household's total consumption of "cars" is therefore a CES composite of domestically produced cars and imported cars. The **Armington elasticity**, $\sigma$, captures the consumer's willingness to substitute between them based on their relative prices.

This assumption is critical for explaining two key empirical facts: (1) countries simultaneously import and export similar goods (intra-industry trade), and (2) domestic prices can differ from the world price of similar goods. When a government imposes a tariff ($\tau$) on an imported good, its price rises for domestic consumers. According to the Armington model, consumers will substitute away from the more expensive imported variety towards the cheaper domestic one. The magnitude of this shift, and thus the tariff's impact on trade volumes and domestic production, is governed by the Armington elasticity.

### Achieving Equilibrium: Market Clearing and Model Closure

A CGE model brings together the optimizing behavior of all firms and households into a single system. The "general equilibrium" is a set of prices (for goods, labor, and capital) at which all markets clear—supply equals demand for every good and factor—and all agents are simultaneously optimizing.

A fundamental constraint on any economy is that aggregate expenditures must equal aggregate income. This is represented by the macroeconomic identity:
$$
(S - I) + (T - G) = (X - M)
$$
where $S$ is private savings, $I$ is investment, $T$ is tax revenue, $G$ is government spending, $X$ is exports, and $M$ is imports. This can be rearranged as *Private Balance + Government Balance = External Balance*. Walras's Law ensures that if all but one market are in equilibrium and all agents' budget constraints are met, the final market must also be in equilibrium. In a CGE model, this macro identity serves as a crucial consistency check.

However, this identity also presents a challenge. The individual components ($S, I, G, T, X, M$) are determined by the behavior of various agents. The model must include a mechanism that guarantees this identity holds. This mechanism is known as the **macroeconomic closure** of the model. The choice of closure is a fundamental assumption that defines the "rules of the game" for the macroeconomy and strongly influences the model's response to shocks [@problem_id:2380471]. Three common closures are:

1.  **Neoclassical Closure**: This closure assumes that factor markets clear, meaning the economy is always at **full employment**. Output is therefore determined by the supply side (factor endowments and technology). To ensure the macro identity holds, one component must adjust. A common assumption is that investment is determined by the available savings. In an open economy, the external balance (trade deficit/surplus) might adjust via changes in the real exchange rate. In the simplified model of [@problem_id:2380471], where prices are fixed, an influx of foreign aid is absorbed by an endogenous increase in domestic absorption (investment or consumption), representing the economy's adjustment to the newfound resources while remaining at its productive frontier.

2.  **Keynesian Closure**: This closure reflects a world with sticky prices and wages, leading to the possibility of **involuntary unemployment**. Output is not determined by supply constraints but by the level of aggregate demand. Investment is often assumed to be exogenous or fixed, and firms produce whatever is demanded at the going price. In this world, an influx of foreign aid that increases demand will lead to a multiplier effect, increasing total output and employment. Here, the labor market does not clear, and the economy operates inside its production possibility frontier.

3.  **Johansen Closure**: This is a specific type of neoclassical closure typically used in applied modeling. It assumes full employment and that investment is determined by savings. To balance the external account, the real exchange rate is allowed to vary. A fixed domestic price level (the numeraire) is chosen, and the nominal exchange rate adjusts to equilibrate the balance of payments. In the one-good model of [@problem_id:2380471], the mechanism is trivialized, but in a multi-good model, a change in the exchange rate alters the relative prices of tradable and non-tradable goods, inducing the resource reallocations necessary for external balance.

The choice of closure is not a matter of right or wrong but depends on the economic context and the time horizon of the analysis. A neoclassical closure is often more suitable for long-run analyses where prices are expected to be flexible, while a Keynesian closure may be more appropriate for short-run analyses of business cycles in economies with rigidities.

### Extending the Framework: Dynamics, Behavior, and Market Structure

The basic static CGE model can be extended in numerous ways to capture more realistic economic features. These extensions demonstrate the framework's remarkable flexibility.

#### Dynamic Models and Expectations

While static models are useful for comparing two [equilibrium states](@entry_id:168134) ("before" and "after" a shock), **dynamic CGE models** trace the entire adjustment path over time. This requires specifying how capital accumulates and how agents form expectations about the future [@problem_id:2380393].

*   **Recursive-Dynamic Models**: In this approach, agents are modeled as myopic or having adaptive expectations. Decisions in each period are based only on current and past information. A common specification is that aggregate investment is a fixed fraction of current income ($I_t = s Y_t$). When a permanent, positive productivity shock occurs, output and investment jump up in the initial period. As the higher investment leads to capital accumulation, output and investment continue to rise gradually over time toward a new, higher steady-state. This approach is computationally straightforward but lacks theoretical rigor in its treatment of expectations.

*   **Forward-Looking Models**: This more sophisticated approach assumes agents have **[rational expectations](@entry_id:140553)** and optimize over an infinite horizon. Investment decisions are not based on a simple savings rule but on a forward-looking calculation of the value of new capital, encapsulated in **Tobin's q** (the ratio of the market value of capital to its replacement cost). When an unanticipated, permanent productivity increase occurs, agents immediately understand that the future returns to capital will be higher. This causes Tobin's q to jump on impact, leading to a large, **front-loaded surge in investment** that may overshoot the new steady-state level. As the capital stock builds up, the marginal product of capital falls, and investment gradually declines to its new long-run level. These models are theoretically consistent but computationally much more demanding.

#### Imperfect Competition and Market Power

The standard CGE model assumes perfect competition, where firms are price-takers. However, many key sectors (e.g., energy, telecommunications, steel) are characterized by a small number of large firms with market power. CGE models can be adapted to handle such **imperfect competition** [@problem_id:2380444].

For example, a perfectly competitive steel industry can be re-specified as a **Cournot oligopoly**, where a fixed number of firms ($N$) compete by choosing output quantities. In contrast to the competitive outcome where price equals marginal cost ($P = c$), Cournot firms recognize that their output affects the market price. The resulting equilibrium price is a markup over marginal cost, $P > c$, and the total quantity produced is lower than the competitive level. The markup and the extent of the output restriction depend on the number of firms; as $N \to \infty$, the Cournot equilibrium converges to the perfectly competitive one. Incorporating this structure is crucial for analyzing policies in sectors where firms have significant market power, as the welfare implications of taxes or regulations will differ substantially.

#### Frictions and Equilibrium Unemployment

Another important extension is the incorporation of real-world frictions. The classical assumption of a frictionless labor market that instantly clears is empirically false. Modern CGE models can incorporate **search-and-matching frictions** to generate **equilibrium unemployment**, following the framework of Diamond, Mortensen, and Pissarides [@problem_id:2380479].

In this framework, unemployed workers must search for jobs and firms must post costly vacancies to find workers. The meeting process is described by a **matching function**. The equilibrium is characterized by a steady-state **unemployment rate** ($u$) and a level of **labor market tightness** ($\theta$, the ratio of vacancies to unemployed workers). Key equilibrium conditions include:
1.  A **Beveridge curve** relationship, where flows into and out of unemployment are balanced ($u = s / (s + f(\theta))$ where $s$ is the job separation rate and $f(\theta)$ is the job-finding rate).
2.  A **job creation condition**, where free entry of firms drives the value of posting a vacancy to zero. This links the cost of posting a vacancy to the expected profit from a filled job.
3.  A **wage determination equation**, often derived from Nash bargaining, where the wage splits the surplus of a match between the worker and the firm.

This enriched structure allows the model to analyze how policies—such as labor taxes, unemployment benefits, or hiring subsidies—affect not only wages and output but also the unemployment rate, vacancy rate, and labor market dynamics.

#### Behavioral Economics

The CGE framework can also accommodate non-standard behavioral assumptions from psychology and economics. For instance, instead of standard neoclassical preferences, a model can feature a household with **reference-dependent preferences**, as described by [prospect theory](@entry_id:147824) [@problem_id:2380420]. Here, utility depends not just on the absolute level of consumption ($c$), but on consumption relative to a fixed **reference point** ($r$). Furthermore, the household may exhibit **loss aversion**, meaning a loss in consumption below the reference point is felt more keenly than an equivalent gain above it ($U = v(c-r) + \dots$, where the slope of $v(\cdot)$ is steeper for negative arguments). This leads to a kink in the household's [utility function](@entry_id:137807) and can result in a kinked labor supply curve, where the response of labor supply to a wage change depends critically on whether the change pushes consumption across the reference point. This demonstrates the model's capacity to explore the implications of more psychologically realistic assumptions.

### Parameterization and Policy Analysis

A CGE model's structure is only half the story; its quantitative results depend entirely on the values of its parameters, especially substitution elasticities.

#### Calibration vs. Estimation

There are two primary methods for parameterizing a CGE model [@problem_id:2380454].

*   **Calibration**: This is the most common approach. The modeler first constructs a **Social Accounting Matrix (SAM)**, a comprehensive snapshot of all economic flows in a specific **base year**. Then, key behavioral parameters—namely substitution elasticities—are chosen based on surveys of the econometric literature. Finally, the remaining parameters (such as share and scale parameters in production and utility functions) are calculated precisely so that the model's equilibrium solution, given the base-year policies, exactly replicates the SAM. Calibration is computationally convenient and ensures the model is grounded in a real-world dataset. However, it is an a-statistical method; it produces a single, deterministic set of results with no inherent [measure of uncertainty](@entry_id:152963).

*   **Econometric Estimation**: This approach treats the CGE model as a system of [structural equations](@entry_id:274644) and statistically estimates its parameters using [time-series data](@entry_id:262935) for the economy. This is more data-intensive and computationally complex. Its primary advantage is that it provides statistical measures of uncertainty for the estimated parameters (e.g., a covariance matrix $\hat{\Sigma}$). This [parameter uncertainty](@entry_id:753163) can then be propagated through the model (e.g., via Monte Carlo simulations) to generate [confidence intervals](@entry_id:142297) for the policy simulation results (such as the welfare impact). This provides a valuable measure of the robustness of the model's conclusions. A key difference is that an estimated model, optimized to fit many years of data, will generally not replicate the base-year SAM perfectly without a separate reconciliation step.

#### Policy Analysis and the Theory of the Second Best

CGE models are indispensable tools for policy analysis precisely because they capture the general equilibrium interactions that partial equilibrium analysis misses. A classic application is in illustrating the **[theory of the second best](@entry_id:138240)** [@problem_id:2380449]. This theory states that in the presence of an existing, unavoidable market distortion, introducing a policy to correct a second distortion does not guarantee an improvement in overall welfare.

A salient example is the interaction between [environmental policy](@entry_id:200785) and the tax system. Consider an economy with a pre-existing, distortionary labor tax. Now, suppose a "corrective" carbon tax is introduced, set equal to the marginal environmental damage of emissions (a Pigouvian tax). In a first-best world with no other distortions, this tax would unambiguously improve welfare. However, in the presence of the labor tax, the carbon tax has two effects: (1) the beneficial **environmental effect** of reducing the negative [externality](@entry_id:189875), and (2) a **tax-interaction effect**. The carbon tax raises energy prices, which slightly reduces the real return to labor, thereby exacerbating the distortion from the pre-existing labor tax. If this negative interaction effect is strong enough, it can outweigh the environmental benefit, leading to an overall **reduction in welfare**. CGE models are uniquely suited to quantify these competing effects and determine the net impact of the policy.

Finally, for analyzing small policy changes, it is not always necessary to solve the full nonlinear CGE model. By **linearizing** the system of [equilibrium equations](@entry_id:172166) around the initial equilibrium, one can obtain a tractable linear system that approximates the impact of the shock [@problem_id:2407868]. This approach, which forms the basis of Johansen-style CGE solution software, can yield powerful and intuitive analytical results. For instance, such an analysis can show how the proportional change in imports from a small tariff is determined by the Armington elasticity and the induced change in relative prices. This transparently links policy impacts to the model's key behavioral parameters.