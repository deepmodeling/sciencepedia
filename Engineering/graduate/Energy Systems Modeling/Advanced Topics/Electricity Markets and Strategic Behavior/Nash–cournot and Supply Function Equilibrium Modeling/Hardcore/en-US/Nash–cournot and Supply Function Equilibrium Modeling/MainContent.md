## Introduction
In industries dominated by a small number of firms, such as wholesale energy, understanding [strategic interaction](@entry_id:141147) is paramount. Oligopoly models provide the essential framework for analyzing how these firms compete, exercise [market power](@entry_id:1127631), and respond to regulatory changes. This article delves into two of the most powerful and widely used frameworks in energy [systems analysis](@entry_id:275423): the Nash–Cournot model of quantity competition and the more complex Supply Function Equilibrium (SFE) model. It aims to bridge the gap between abstract economic theory and concrete application by providing a comprehensive guide to their mechanics and utility.

To achieve this, the article is structured to build your understanding progressively. The first chapter, **"Principles and Mechanisms,"** lays the theoretical groundwork, detailing the core assumptions, optimization problems, and equilibrium concepts for both the Nash–Cournot and SFE models. Next, **"Applications and Interdisciplinary Connections"** demonstrates the versatility of these models by extending them to analyze realistic market structures, policy interventions, and the spatiotemporal complexities of energy networks. Finally, **"Hands-On Practices"** provides opportunities to apply these concepts through guided exercises, solidifying your ability to solve for and interpret equilibrium outcomes in various market scenarios.

## Principles and Mechanisms

This chapter delineates the foundational principles and operational mechanisms of two canonical oligopoly models widely applied in energy systems: the Nash–Cournot model of quantity competition and the Supply Function Equilibrium (SFE) model. We will begin with the Cournot framework, exploring its core assumptions, equilibrium conditions, and implications for [market power](@entry_id:1127631). Subsequently, we will transition to the more complex Supply Function Equilibrium model, highlighting its distinct strategic environment and its particular relevance to wholesale electricity markets.

### The Nash–Cournot Model of Quantity Competition

The Cournot model, first proposed by Augustin Cournot in 1838, provides a foundational framework for analyzing oligopolistic markets where a small number of firms compete by choosing their output levels. The central premise is that firms simultaneously and non-cooperatively decide *how much* to produce, and the market price adjusts to clear the total quantity supplied.

#### The Firm's Optimization Problem and the Nature of Marginal Revenue

To understand the behavior of firms in a Cournot setting, we must first characterize their decision-making process. Each firm aims to maximize its profit, which is the difference between its revenue and its production costs. The critical element that distinguishes this model from perfect competition lies in how a firm perceives its revenue.

Consider a market with $n$ firms, where the market price $P$ is determined by a downward-sloping inverse demand function $P(Q)$, with $Q = \sum_{i=1}^n q_i$ being the aggregate quantity supplied. An inverse demand function is appropriate here because the [independent variable](@entry_id:146806), chosen by the firms, is the total quantity $Q$, and the [dependent variable](@entry_id:143677), determined by the market, is the price $P$. For instance, a common and tractable representation is the linear inverse demand function $P(Q) = a - bQ$, where $a > 0$ is the **choke price** (the price at which demand falls to zero) and $b > 0$ represents the slope .

A firm $i$ with cost function $C_i(q_i)$ seeks to maximize its profit $\pi_i$:
$$
\pi_i(q_1, \dots, q_n) = P(Q)q_i - C_i(q_i) = P\left(q_i + \sum_{j \neq i} q_j\right)q_i - C_i(q_i)
$$
The core assumption of the Cournot model is that each firm $i$ chooses its quantity $q_i$ while treating the quantities of its rivals, $Q_{-i} = \sum_{j \neq i} q_j$, as fixed. How does this affect the firm's calculation of marginal revenue?

A price-taking firm in a perfectly competitive market assumes its own output has no effect on the market price. Its marginal revenue is simply the market price $P$. In contrast, a Cournot firm recognizes that its own production decision affects the total quantity $Q$, and therefore influences the market price. To find the optimal quantity, the firm differentiates its profit function with respect to its own output $q_i$. Applying the product and chain rules to the revenue term yields the [first-order condition](@entry_id:140702) for an interior solution ($q_i > 0$):
$$
\frac{\partial \pi_i}{\partial q_i} = \underbrace{P(Q) + q_i \frac{dP}{dQ} \frac{\partial Q}{\partial q_i}}_{\text{Marginal Revenue (MR}_i\text{)}} - \underbrace{\frac{dC_i}{dq_i}}_{\text{Marginal Cost (MC}_i\text{)}} = 0
$$
Since $Q = q_i + Q_{-i}$ and firm $i$ treats $Q_{-i}$ as constant, the derivative $\frac{\partial Q}{\partial q_i} = 1$. The condition thus becomes:
$$
MR_i = P(Q) + P'(Q)q_i = C_i'(q_i)
$$
This equation reveals the crucial insight of the Cournot model . The marginal revenue for a Cournot firm has two components:
1.  $P(Q)$: The revenue gained from selling one additional unit at the prevailing price.
2.  $P'(Q)q_i$: The change in revenue on all of the firm's *inframarginal* units. Since inverse demand is downward sloping ($P'(Q)  0$), this term is negative. It represents the revenue lost because the additional unit of output depresses the market price for all $q_i$ units the firm sells. This is the **price impact term** that a firm with [market power](@entry_id:1127631) must internalize.

#### Defining the Nash–Cournot Equilibrium

A **Nash–Cournot equilibrium** is a set of quantities $(q_1^*, q_2^*, \dots, q_n^*)$ where each firm's chosen quantity is a [best response](@entry_id:272739) to the quantities chosen by its rivals. Formally, for every firm $i$, $q_i^*$ must solve the profit maximization problem given the equilibrium quantities of the other firms, $Q_{-i}^* = \sum_{j \neq i} q_j^*$ :
$$
q_i^* \in \arg\max_{q_i \ge 0} \left\{ P(q_i + Q_{-i}^*)q_i - C_i(q_i) \right\}
$$
This leads to a system of [optimality conditions](@entry_id:634091) for all $n$ firms. For any firm $i$ producing a positive quantity in equilibrium ($q_i^* > 0$), its marginal revenue must equal its marginal cost:
$$
P(Q^*) + P'(Q^*)q_i^* - C_i'(q_i^*) = 0
$$
where $Q^* = \sum_j q_j^*$. If a firm produces zero ($q_i^* = 0$), it must be that its marginal profit from the first infinitesimal unit is non-positive. This means that at the price prevailing with its absence, $P(Q_{-i}^*)$, this price is not sufficient to cover its marginal cost of starting production, $C_i'(0)$. The condition is $P(Q_{-i}^*) - C_i'(0) \le 0$.

The set of optimal quantities for firm $i$ given any possible rival output $Q_{-i}$ defines its **best [response function](@entry_id:138845)**, $q_i = R_i(Q_{-i})$. The Nash–Cournot equilibrium is the fixed point of this system of best response functions, where $q_i^* = R_i(Q_{-i}^*)$ for all $i$. In a duopoly ($n=2$), this corresponds to the intersection of the two firms' [best response](@entry_id:272739) curves.

### Solving the Cournot Model: Analytical Examples

To make these concepts concrete, we now solve for the equilibrium in two common settings: one with constant marginal costs and another with increasing marginal costs.

#### Symmetric Firms with Linear Costs

Let's analyze a market with $n$ identical firms, a linear inverse demand $P(Q) = a - bQ$, and a linear cost function $C_i(q_i) = c q_i$ for all firms, where $a > c > 0$ and $b > 0$. The marginal cost is constant at $c$, and the slope of the inverse demand is $P'(Q) = -b$.

The [first-order condition](@entry_id:140702) for firm $i$, $P(Q) + P'(Q)q_i = C_i'(q_i)$, becomes:
$$
(a - bQ) + (-b)q_i = c
$$
We seek a symmetric equilibrium where all firms produce the same quantity, $q_i = q^*$ for all $i$. In this case, the total quantity is $Q = nq^*$. Substituting this into the [first-order condition](@entry_id:140702) for a representative firm:
$$
(a - b(nq^*)) - bq^* = c
$$
Solving for the symmetric equilibrium quantity per firm, $q^*$ :
$$
a - c = bnq^* + bq^* = b(n+1)q^*
$$
$$
q^* = \frac{a - c}{b(n+1)}
$$
The aggregate equilibrium quantity is $Q^* = nq^* = \frac{n(a - c)}{b(n+1)}$, and the equilibrium price is $P^* = a - bQ^* = \frac{a + nc}{n+1}$.

These results are instructive. As the number of firms $n$ increases, the per-firm output $q^*$ decreases, but the total output $Q^*$ increases and approaches the competitive level $\frac{a-c}{b}$. Correspondingly, the equilibrium price $P^*$ decreases and approaches the competitive price, $c$. In the limit as $n \to \infty$, the Cournot model converges to the perfectly competitive outcome. For $n=1$, the model yields the standard monopoly outcome.

#### The Effect of Increasing Marginal Costs

In many real-world settings, such as electricity generation, marginal costs are not constant but increase with output. We can model this with a convex cost function, for example, a quadratic function $C_i(q_i) = \alpha_i q_i + \frac{1}{2}\beta_i q_i^2$, which implies a linearly increasing marginal cost $MC_i(q_i) = \alpha_i + \beta_i q_i$, with $\beta_i > 0$ .

Let the inverse demand again be $P(Q) = A - BQ$. The [first-order condition](@entry_id:140702) for firm $i$, equating marginal revenue to marginal cost, is:
$$
(A - B(q_i + s)) - Bq_i = \alpha_i + \beta_i q_i
$$
where $s = \sum_{j \neq i} q_j$ is the total output of rivals. Solving for $q_i$ yields the best response function for firm $i$:
$$
q_i = R_i(s) = \max\left\{0, \frac{A - \alpha_i - Bs}{2B + \beta_i}\right\}
$$
This function shows how firm $i$'s optimal output decreases as its rivals' output $s$ increases. The slope of this reaction function, $\frac{-B}{2B + \beta_i}$, depends on the cost parameter $\beta_i$. A higher $\beta_i$ (steeper marginal cost curve) makes the firm's output less responsive to its rivals' actions, as the slope becomes less negative.

In a symmetric case where $\alpha_i = \alpha$ and $\beta_i = \beta$ for all $n$ firms, we can find the equilibrium quantity $q^*$ by setting $q_i = q^*$ and $s = (n-1)q^*$:
$$
q^* = \frac{A - \alpha - B(n-1)q^*}{2B + \beta}
$$
Solving for $q^*$ gives:
$$
q^* = \frac{A - \alpha}{\beta + B(n+1)}
$$
As expected, a higher marginal cost (either through a higher intercept $\alpha$ or a steeper slope $\beta$) leads to a lower equilibrium output for each firm.

### Market Power in the Cournot Model

The Cournot model provides a clear way to quantify [market power](@entry_id:1127631) and link it to market structure.

#### The Lerner Index and Demand Elasticity

A widely used measure of market power is the **Lerner Index**, which measures the percentage markup of price over marginal cost: $L_i = \frac{P - MC_i}{P}$. Starting again from firm $i$'s [first-order condition](@entry_id:140702), $P + P'(Q)q_i = MC_i$, we can rearrange it as $P - MC_i = -P'(Q)q_i$. Dividing by $P$ gives:
$$
L_i = \frac{-P'(Q)q_i}{P} = \frac{-P'(Q)Q}{P} \cdot \frac{q_i}{Q}
$$
The term $\frac{-P'(Q)Q}{P}$ is the inverse of the [price elasticity of demand](@entry_id:903053), $\epsilon = \frac{P}{Q} \frac{dQ}{dP} = \frac{P}{Q} \frac{1}{P'(Q)}$. Note that we consider elasticity in magnitude, so $\epsilon = |\frac{dQ}{dP} \frac{P}{Q}|$. The term $\frac{q_i}{Q}$ is simply firm $i$'s market share, $s_i$. This yields a fundamental relationship:
$$
L_i = \frac{s_i}{\epsilon}
$$
This equation shows that a firm's [market power](@entry_id:1127631) is directly proportional to its market share and inversely proportional to the market demand elasticity. In a symmetric Cournot equilibrium with $n$ firms, each has a market share of $s_i = 1/n$, so the Lerner Index for each firm is :
$$
L = \frac{1}{n\epsilon}
$$
For the linear model ($P(Q) = a - bQ$, $MC=c$), we can derive a [closed-form expression](@entry_id:267458) for the Lerner Index at equilibrium. Using our previous results $P^* = \frac{a+nc}{n+1}$ and $MC=c$:
$$
L = \frac{P^* - c}{P^*} = \frac{\frac{a+nc}{n+1} - c}{\frac{a+nc}{n+1}} = \frac{a-c}{a+nc}
$$
This confirms our intuition: [market power](@entry_id:1127631) (the markup) decreases as the number of firms $n$ increases, and it disappears ($L \to 0$ as $n \to \infty$).

### The Supply Function Equilibrium (SFE) Model

While the Cournot model provides powerful insights, its assumption that firms compete on a single quantity can be restrictive. In many modern markets, particularly wholesale [electricity markets](@entry_id:1124241), firms do not submit a single quantity but rather a schedule of quantities they are willing to supply at different prices. The **Supply Function Equilibrium (SFE)** model, developed by Grossman (1981) and Klemperer and Meyer (1989), captures this richer strategic environment.

#### From Quantities to Functions: A Richer Strategy Space

The most fundamental distinction between the Cournot and SFE models lies in the strategic variable.
- In Cournot, the strategy of firm $i$ is a scalar quantity, $q_i \in \mathbb{R}_+$.
- In SFE, the strategy of firm $i$ is a function, $S_i(p)$, which maps every possible market price $p$ to a quantity the firm offers to produce, $q_i = S_i(p)$ .

This seemingly technical difference has profound implications. By submitting a function, a firm commits to a contingent plan of action that covers all possible price outcomes. This allows for more complex strategic interactions than the simple choice of a single output level.

#### Market Clearing in an SFE Framework

In an SFE context, the market is typically operated by an Independent System Operator (ISO). For a given set of submitted supply functions $\{S_i(p)\}_{i=1}^n$ and a realized demand function $D(p, \theta)$ (where $\theta$ can be a random shock), the ISO's role is to determine the market-clearing uniform price, $p^*$. This price is found by enforcing power balance: total offered supply must equal total demand . Mathematically, $p^*$ is the solution to:
$$
\sum_{i=1}^n S_i(p^*) = D(p^*, \theta)
$$
Under standard regularity conditions—namely, that the aggregate supply function $\sum S_i(p)$ is continuous and non-decreasing, and the demand function $D(p, \theta)$ is continuous and strictly decreasing—a unique market-clearing price is guaranteed to exist.

#### Formal Definition of Supply Function Equilibrium

With this clearing mechanism in mind, we can formally define an SFE. In a market with uncertainty (e.g., about the demand parameter $\theta$), firms choose their supply functions *before* the uncertainty is resolved. Therefore, firms must maximize their *expected* profit.

A **Supply Function Equilibrium** is a set of supply functions $\{S_i^*(p)\}_{i=1}^n$ such that for each firm $i$, the function $S_i^*(p)$ is a best response to the functions submitted by its rivals, $\{S_j^*(p)\}_{j \neq i}$. This means that no firm $i$ can unilaterally choose a different supply function $\tilde{S}_i(p)$ and achieve a strictly higher expected profit, given the clearing rule and its rivals' strategies. This is a form of **Bayes–Nash equilibrium** where the strategies themselves are functions .

### Analytical Characterization of SFE

Solving for an SFE is considerably more complex than solving for a Cournot equilibrium. The equilibrium condition is not a system of algebraic equations but rather a [system of differential equations](@entry_id:262944).

#### The Equilibrium Condition as a Differential Equation

To find its optimal supply function, a firm must ensure that for every price $p$ that could potentially be the market-clearing price, the quantity it offers, $q_i = S_i(p)$, is the profit-maximizing response. This means that at the point $(p, q_i)$ on its supply curve, the firm's isoprofit curve must be tangent to its *residual demand curve* (the market demand minus the supply of all other firms). This [tangency condition](@entry_id:173083), which equates marginal revenue to marginal cost along the residual demand curve, must hold for all points on the supply function. This requirement translates into a differential equation.

For a market with inverse demand $P(Q, \theta) = \alpha(\theta) - \beta Q$ and firms with constant marginal cost $c$, the [first-order condition](@entry_id:140702) for a symmetric equilibrium where all firms submit the same differentiable supply function $S(p)$ can be derived using the [calculus of variations](@entry_id:142234) . The resulting ordinary differential equation (ODE) that characterizes the equilibrium supply function $S(p)$ is:
$$
S'(p) = \frac{S(p)}{(n - 1)(p - c)} - \frac{1}{\beta(n - 1)}
$$

#### Multiplicity of Equilibria

This differential equation highlights a key feature of the SFE model. To find a unique solution for $S(p)$, this first-order ODE requires a boundary condition—for example, specifying a quantity at a particular price, $S(p_0) = q_0$. However, in a model with linear costs and no capacity constraints, there is no natural economic condition to pin down this boundary.

As a result, there is not one single SFE, but a **continuum of equilibria** . Each possible boundary condition gives rise to a different, valid equilibrium supply function. This indeterminacy is a hallmark of the SFE model in simple linear environments. Outcomes ranging from the perfectly competitive result to the Cournot result can all be supported as supply function equilibria. This contrasts sharply with the unique equilibrium typically found in the corresponding Cournot model. The strategic richness of choosing a function, rather than a scalar, opens the door to a much wider set of possible self-enforcing outcomes. In practical applications, this [multiplicity](@entry_id:136466) is often resolved by introducing more realistic features, such as capacity constraints, start-up costs, or multi-period linkages, which can impose the necessary boundary conditions to select a unique or small set of equilibria.