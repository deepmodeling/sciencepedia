## Introduction
In an interconnected global economy, policies aimed at addressing challenges like climate change or trade imbalances rarely have simple, isolated effects. A tax on carbon, for instance, doesn't just impact power plants; it ripples through supply chains, alters consumer prices, affects household incomes, and influences international competitiveness. To understand these complex, system-wide consequences, policymakers and analysts rely on powerful quantitative tools. Computable General Equilibrium (CGE) and Input-Output (IO) models stand as the primary frameworks for this kind of holistic analysis, moving beyond the limitations of single-market studies to capture the full web of economic interactions. This article provides a comprehensive introduction to these essential modeling techniques. The first chapter, **Principles and Mechanisms**, demystifies the theoretical foundations, from Walrasian equilibrium to the accounting rules of a Social Accounting Matrix (SAM) and the behavioral equations that drive the models. The second chapter, **Applications and Interdisciplinary Connections**, showcases how these models are used to evaluate environmental policies, analyze distributional impacts, and integrate with engineering-based approaches. Finally, the **Hands-On Practices** section provides a bridge from theory to application, with guided problems that build a working understanding of the models' mechanics. By navigating these sections, you will gain a robust conceptual and practical foundation in CGE and I-O policy modeling, starting with their foundational principles.

## Principles and Mechanisms

This chapter delineates the foundational principles and core mechanisms that underpin Computable General Equilibrium (CGE) and Input-Output (IO) models. Building upon the introductory concepts, we will now formalize the theoretical architecture of these models, starting from the bedrock of [general equilibrium theory](@entry_id:143523) and progressing to the specific accounting frameworks, behavioral assumptions, and mathematical formulations used in applied policy analysis.

### The Theoretical Foundation: Walrasian General Equilibrium

At its core, a CGE model is a numerical representation of the Walrasian [general equilibrium theory](@entry_id:143523). This theory provides a comprehensive framework for understanding how a market-based economy operates, accounting for the complex web of interactions among all economic agents and markets.

A **Walrasian general equilibrium** is defined by a state of the economy consisting of a vector of prices for all goods and factors, and an allocation of these goods and factors among all households and firms, such that three fundamental conditions are simultaneously met :

1.  **Household Optimization**: Given the equilibrium price vector, every household chooses a consumption plan (a bundle of goods and leisure) that maximizes its utility, subject to its [budget constraint](@entry_id:146950). A household's income is derived from its endowments of primary factors (like labor and capital) and any profits distributed from firms it owns.

2.  **Firm Optimization**: Given the same price vector, every firm chooses a production plan (a set of inputs and outputs) that maximizes its profit, subject to the technological constraints it faces.

3.  **Market Clearing**: For every good and every factor in the economy, the total quantity demanded by all agents equals the total quantity supplied. The aggregate supply consists of the economy's initial endowments plus the net output from all firms.

This holistic approach stands in stark contrast to **[partial equilibrium analysis](@entry_id:1129369)**, which examines a single market in isolation under the *[ceteris paribus](@entry_id:637315)* ("all else equal") assumption. While useful for focused inquiries, partial equilibrium ignores the crucial feedback effects that ripple across the economy. For instance, a carbon tax on electricity not only raises the price of power but also affects the production costs of all industries using electricity, alters the real income of households, changes the demand for other goods and services, and ultimately impacts wages and returns to capital. General equilibrium analysis is designed explicitly to capture these system-wide interdependencies, making it indispensable for evaluating policies with broad economic impacts .

The theoretical integrity of the CGE framework is anchored by the **Arrow-Debreu [existence theorems](@entry_id:261096)**. These landmark results in mathematical economics prove that a Walrasian general equilibrium is guaranteed to exist under a set of standard regularity conditions. These conditions include :
*   Complete, continuous, and **convex preferences** for all households.
*   **Local non-satiation**, meaning households always prefer slightly more of at least one good.
*   Closed and **convex production sets** for all firms, which implies non-[increasing returns](@entry_id:1126450) to scale.
*   **Free disposal**, meaning surplus goods can be eliminated without cost.

The proof of existence typically involves normalizing prices to a compact and [convex set](@entry_id:268368) (the price [simplex](@entry_id:270623)) and applying a **[fixed-point theorem](@entry_id:143811)**—such as Kakutani's theorem for set-valued functions—to an aggregate [excess demand](@entry_id:136831) correspondence. The standard building blocks of CGE models, including the functional forms and market structures discussed in this chapter, are chosen specifically to satisfy these conditions, ensuring that the models are theoretically coherent and have a well-defined solution.

### From Theory to Practice: Accounting and Core Equations

To operationalize [general equilibrium theory](@entry_id:143523), CGE models are constructed upon a rigorous and consistent accounting framework known as a **Social Accounting Matrix (SAM)**. A SAM is a snapshot of all economic transactions within a period, organized as a square matrix where each row and column corresponds to an account (e.g., production activities, commodities, institutions). The fundamental rule of a SAM is that for every account, total inflows (receipts) must equal total outflows (expenditures). This double-entry bookkeeping ensures complete consistency.

The equilibrium of a CGE model is characterized by a set of equations that enforce these accounting principles alongside the optimizing behavior of agents. The two primary sets of balancing equations are for commodity and factor markets.

#### Market Clearing Conditions

For an equilibrium to hold, every market must clear.

First, for every **commodity** $c$ in the economy, the total supply must equal the total uses (or demand). In an open economy, this is expressed as :

$X_c + M_c = \sum_{a}\text{INT}_{c,a} + C_c + G_c + I_c + \Delta \text{ST}_c + E_c$

Where:
*   $X_c$ is the domestic production of commodity $c$.
*   $M_c$ is the volume of imports of commodity $c$.
*   The left-hand side, $X_c + M_c$, represents the **total supply** available to the economy.
*   $\text{INT}_{c,a}$ is the intermediate demand for commodity $c$ by production activity $a$.
*   $C_c$ is final consumption demand by households.
*   $G_c$ is final consumption demand by the government.
*   $I_c$ is investment demand (gross fixed capital formation).
*   $\Delta \text{ST}_c$ is the change in inventories (a positive value represents an addition to stocks, which is a use of current supply).
*   $E_c$ is export demand from the rest of the world.
*   The right-hand side represents the **total uses** of the commodity.

Second, for every **primary factor** of production (e.g., labor $L$, capital $K$), the total demand from all production activities must equal the economy's total endowment of that factor, which is typically assumed to be fixed in a static model :

$\sum_{a} l_a = \bar{L}$

$\sum_{a} k_a = \bar{K}$

Where $l_a$ and $k_a$ are the labor and capital demanded by activity $a$, and $\bar{L}$ and $\bar{K}$ are the fixed total endowments of labor and capital.

#### The Circular Flow of Income

The SAM framework also tracks the circular flow of income among the economy's institutions: typically **households**, **enterprises** (firms), the **government**, and the **rest of the world**. Factor payments from production activities become income for institutions, which is then spent or saved, creating the demands that production must satisfy. In equilibrium, each institution's budget must balance .

*   **Households** receive income from labor, distributed profits (dividends) from enterprises, and transfers from the government and the rest of the world. They use this income for consumption, paying taxes, making transfers, and saving.
*   **Enterprises** receive income from their operating surplus (capital income). They use this to pay corporate taxes and distribute dividends to their owners (households), with the remainder being enterprise savings (retained earnings).
*   **Government** receives income from various taxes (e.g., direct taxes on households and firms, indirect taxes on production, and import tariffs). It uses this revenue for government consumption and transfers, with the remainder being government savings (the budget surplus or deficit).
*   The **Rest of the World** account tracks all transactions with the domestic economy. Its balancing item is **foreign savings**, which is the negative of the domestic economy's current account balance. A positive value for foreign savings signifies a current account deficit for the domestic economy, financed by a capital inflow from abroad.

The concept of **disposable income** represents the income available to an institution after mandatory payments like direct taxes. For example, household disposable income is what remains for consumption and saving. The balancing item that ensures inflows equal outflows for each domestic institution is its **savings**.

#### A Complete Equilibrium Specification

A complete specification of a competitive equilibrium integrates these elements—agent optimization, market clearing, and institutional balances. As a formal example, consider an economy with production, taxes, and government transfers. An equilibrium is a set of prices and allocations such that :
1.  The **representative household** maximizes its utility subject to a [budget constraint](@entry_id:146950) where expenditures on goods (at tax-inclusive consumer prices) cannot exceed income from labor, firm profits ($\Pi$), and government transfers ($T$).
2.  Each **firm** maximizes its profit—revenue minus costs for inputs like labor and intermediates. Any taxes on production or inputs (like a carbon tax) are treated as a cost to the firm.
3.  The **government** balances its budget, such that total tax revenues (e.g., from consumption and carbon taxes) are equal to its total outlays (e.g., the lump-sum transfer $T$).
4.  All **markets** for goods and factors clear, as described by the equations above.

This system of [simultaneous equations](@entry_id:193238) and optimization problems defines the CGE model, which can then be solved numerically to find the equilibrium prices and quantities.

### Key Mechanisms and Functional Forms

While the equilibrium framework provides the model's skeleton, its behavior is determined by the "flesh"—the specific mathematical functions used to model production, consumption, and trade. The choice of these **functional forms** dictates the degree of substitutability and responsiveness in the economy.

#### The Leontief Input-Output Structure

The simplest technological specification is the **Leontief production function**, which forms the basis of traditional Input-Output (IO) analysis. This model assumes a fixed, zero-substitution relationship between inputs and outputs. The technology is characterized by a **technical coefficients matrix**, $A$, where each element $a_{ij}$ represents the quantity of input from sector $i$ required to produce one unit of output in sector $j$ .

The fundamental equation of the demand-driven Leontief model is $x = Ax + y$, where $x$ is the vector of gross outputs and $y$ is the vector of final demands. For a given final demand $y$, the required gross output is found using the **Leontief inverse**:

$x = (I - A)^{-1}y$

The term $(I - A)^{-1}$ is a matrix of multipliers that shows the total output required from each sector, both directly and indirectly, to deliver one unit of a good to final demand. The primary limitation of this framework is its rigidity: it cannot account for substitution away from an input whose price has increased. It is a pure quantity model that is well-suited for impact analysis under the strong assumption of fixed technology.

An alternative, the supply-driven **Ghosh model**, assumes fixed output allocation shares rather than fixed input shares. However, this model is considered behaviorally implausible for market economies, as firms sell to the highest bidder, not in fixed proportions, making it unsuitable for analyzing supply constraints .

#### The Constant Elasticity of Substitution (CES) Function

To overcome the rigidity of the Leontief model, CGE models primarily employ the **Constant Elasticity of Substitution (CES)** function. This flexible functional form allows for a continuous range of substitution possibilities between inputs. For a set of inputs $X_i$, the CES aggregator for output $Q$ is:

$Q = \left( \sum_{i} \alpha_i X_i^{\rho} \right)^{1/\rho}$

The key feature of the CES function is governed by the parameter $\rho$, which is directly related to the **elasticity of substitution**, $\sigma$, via the formula :

$\sigma = \frac{1}{1 - \rho}$

The elasticity of substitution $\sigma$ measures the percentage change in the ratio of two inputs in response to a one percent change in their relative prices. The "constant" in CES means this elasticity is the same at all levels of input usage. The value of $\sigma$ (and thus $\rho$) determines the technology:
*   **Leontief (Fixed Proportions)**: As $\rho \to -\infty$, $\sigma \to 0$. There is no substitution between inputs.
*   **Cobb-Douglas**: As $\rho \to 0$, $\sigma \to 1$. Inputs have a unitary elasticity of substitution.
*   **Linear (Perfect Substitutes)**: As $\rho \to 1$, $\sigma \to \infty$. Inputs are perfectly interchangeable.

By choosing different values for $\sigma$, modelers can represent a wide array of production and consumption structures. For instance, in analyzing a carbon tax, a higher $\sigma$ between coal and natural gas in electricity generation would lead to a stronger shift away from coal as its relative price increases .

#### The Armington Assumption and International Trade

A critical application of the CES function is in modeling international trade through the **Armington assumption** . Instead of treating goods of the same type (e.g., steel) as identical regardless of origin, this assumption posits that they are imperfect substitutes. A composite good $Q$ available to the economy is formed by aggregating a domestically produced variety $D$ and an imported variety $M$ using a CES function:

$Q = \left[ \delta D^{\theta} + (1-\delta) M^{\theta} \right]^{1/\theta}$

Here, the Armington elasticity $\sigma = 1/(1-\theta)$ determines how easily domestic users switch between domestic and imported sources in response to changes in their relative prices. This approach has two major advantages:
1.  It is empirically realistic, explaining the widespread phenomenon of **two-way trade** (a country both importing and exporting the same type of good) and **home bias** (a preference for domestically produced goods).
2.  It avoids the unrealistic "corner solutions" of perfect-substitutes models, where a small price difference would lead to a complete switch to the cheaper source. The Armington framework allows for smooth adjustment and is easily calibrated to observed trade shares in a base-year SAM .

### Advanced Topics: Closure and Solution Methods

Two final concepts are crucial for understanding how CGE models are specified and solved in practice: macroeconomic closure and the mathematical solution framework.

#### Macroeconomic Closure Rules

The savings-investment identity, $I = S_H + S_G + S_F$, must hold in any macroeconomic equilibrium. However, due to Walras's Law, this equation is not independent of the other market-clearing conditions. To obtain a determinate solution, the model must be "closed" by exogenously fixing one of the variables in this identity, which in turn defines how the macro-economy adjusts. This choice is known as the **macroeconomic closure rule** .

There are two standard [closures](@entry_id:747387):

1.  **Savings-Driven Investment (Classical) Closure**: In this regime, the behaviors determining savings are fixed (e.g., the household savings rate $s_H$ is constant, and government and foreign savings follow fixed rules). Total aggregate investment, $I$, becomes the endogenous variable that adjusts to equal the total available pool of savings. This closure represents a "savings-constrained" economy where investment is determined by the availability of loanable funds.

2.  **Investment-Driven Savings (Keynesian/Johansen) Closure**: Here, aggregate investment $I$ is fixed exogenously, often representing a policy target or an assumed investment path. To satisfy the identity, one of the savings components must adjust. Typically, the household savings rate $s_H$ is made endogenous, implying that household consumption is the residual that adjusts to "make room" for the planned investment. This represents an "investment-led" economy.

The choice of closure is a critical modeling assumption that reflects a belief about the underlying macroeconomic drivers and can significantly affect the simulated impacts of a policy, especially those related to growth and capital accumulation.

#### The Mixed Complementarity Problem (MCP) Formulation

Modern CGE models are often formulated and solved as a **Mixed Complementarity Problem (MCP)**. This powerful mathematical framework replaces the system of equilibrium equalities with a set of paired inequalities and complementarity conditions, which is more general and robust, especially for models with non-negativity constraints.

Two key equilibrium conditions are expressed as follows :

*   **Zero-Profit Condition**: For a competitive industry with constant returns to scale, profits cannot be positive. This implies that unit cost $c$ must be greater than or equal to the market price $p$. Production $x$ will only occur ($x > 0$) if profit is exactly zero ($p=c$). This is expressed as the complementarity pair:
    $c - p \ge 0 \quad \perp \quad x \ge 0$
    This notation means that $c - p \ge 0$, $x \ge 0$, and the product of these two terms, $(c-p)x$, must be zero.

*   **Market-Clearing Condition**: With free disposal, supply must be greater than or equal to demand. A good will only command a positive price ($p > 0$) if the market clears exactly (supply equals demand). If there is excess supply, the good is a free good and its price must be zero. This is expressed as:
    $x - d \ge 0 \quad \perp \quad p \ge 0$
    Where $d$ is demand. This means that $x - d \ge 0$, $p \ge 0$, and their product, $(x-d)p$, is zero.

This formulation elegantly captures the logic of [market equilibrium](@entry_id:138207) and is the basis for the powerful algorithms used to solve large-scale CGE models for policy analysis.