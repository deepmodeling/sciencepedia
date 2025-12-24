## Introduction
Feed-in Tariffs (FITs) and Feed-in Premiums (FIPs) are cornerstone policies in the global transition to renewable energy. Designing these support schemes involves a critical trade-off: providing sufficient revenue certainty to attract investment while maintaining economic efficiency and integrating generators into the market. This article provides a comprehensive guide to modeling and analyzing these complex instruments. First, in **Principles and Mechanisms**, we will dissect the fundamental structures of FIT and FIP schemes, quantifying their distinct impacts on revenue, risk, financing costs, and [market efficiency](@entry_id:143751). Next, **Applications and Interdisciplinary Connections** will explore how these models are applied in real-world scenarios, examining strategic decisions for producers, system-level market impacts like price cannibalization, and the design of policy auctions. Finally, **Hands-On Practices** will offer guided exercises to build practical skills in modeling key aspects such as curtailment risk and basis risk. We begin by establishing the foundational principles that distinguish these essential policy tools.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanisms governing Feed-in Tariff (FIT) and Feed-in Premium (FIP) support schemes. We will dissect their structural differences, analyze their implications for generator revenue and risk, evaluate their impact on economic efficiency, and explore the advanced financial and modeling considerations they entail.

### Foundational Revenue Structures: FIT versus FIP

At the most fundamental level, Feed-in Tariffs and Feed-in Premiums represent two distinct philosophies for supporting electricity generation, particularly from renewable energy sources. Their primary distinction lies in how they interact with the wholesale [electricity market](@entry_id:1124240) price.

A **Feed-in Tariff (FIT)** is a remuneration mechanism that largely decouples a generator's revenue from the volatile wholesale market price. In its archetypal form, a FIT operates as a regulated power purchase agreement where a designated off-taker (often a utility or a state agency) purchases all of the generator's output at a pre-determined, administratively set price, denoted as $\tau_t$ (in units of currency per MWh) for each settlement interval $t$. The generator's revenue per unit of energy is therefore simply $r_t^{\text{FIT}} = \tau_t$. Consequently, under a standard FIT, the generator's revenue is independent of the wholesale market price, $p_t$. This structure provides revenue certainty, insulating the producer from market price risk.

However, this independence is conditional. Many real-world FIT designs include clauses that re-introduce a dependency on $p_t$. A common example is the suspension of payments during periods of negative market prices. In such a case, the revenue function becomes piecewise, for example, $r_t^{\text{FIT}} = \tau_t$ if $p_t \ge 0$ and $r_t^{\text{FIT}} = 0$ if $p_t \lt 0$. Other designs may feature caps or floors that are linked to $p_t$. Therefore, while the core principle of a FIT is to provide price certainty, the specific rules of the contract are paramount in determining the true extent of market price exposure .

In contrast, a **Feed-in Premium (FIP)** is a mechanism designed to supplement a generator's market-based revenue. Under a FIP, the generator sells its output directly into the wholesale market, receiving the market price $p_t$. On top of this market revenue, it receives an additional payment, the premium, denoted as $\pi_t$. The total revenue per unit of energy is thus $r_t^{\text{FIP}} = p_t + \pi_t$.

The nature of the generator's exposure to market prices under a FIP depends entirely on the structure of the premium $\pi_t$. In its simplest form, known as a **fixed-adder** or **constant FIP**, the premium is a constant value ($\pi_t = s$). In this case, the revenue is $r_t^{\text{FIP}} = p_t + s$, which remains directly and linearly dependent on the market price $p_t$. While the premium enhances the average revenue level, it does not mitigate price risk; the generator remains fully exposed to the volatility of $p_t$ .

### A Taxonomy of Premium-Based Mechanisms

The general FIP framework, $r_t = p_t + \pi_t$, accommodates a variety of sophisticated designs that modulate the generator's exposure to market prices. These are typically defined by a **strike price**, $S$, and a **market reference price**, $P_t^{\text{ref}}$. For these mechanisms to be transparent, enforceable, and to maintain proper market incentives, the reference price $P_t^{\text{ref}}$ must be an observable, audited, ex-post market price that is aligned with the generator's physical transactions in terms of location, product, and time . We can distinguish three principal archetypes:

1.  **Fixed Premium**: As discussed, this is the simplest case where the premium is a constant adder, $s$, that does not depend on any market price. The total per-unit revenue is $p_t + s$. This mechanism does not require a reference price for its settlement.

2.  **Sliding Premium**: This is a one-sided mechanism designed to provide a floor on revenue. The premium "slides" inversely with the market price, paying the difference between a strike price $S$ and the reference price $P_t^{\text{ref}}$, but only when this difference is positive. The premium payment is thus $\pi_t = \max(0, S - P_t^{\text{ref}})$. The generator's total revenue per MWh becomes $p_t + \max(0, S - P_t^{\text{ref}})$. This structure provides downside protection against low prices while allowing the generator to profit from prices above the strike price.

3.  **Two-sided Contract for Differences (CfD)**: This mechanism creates a symmetric settlement around the strike price. The premium is calculated as $\pi_t = S - P_t^{\text{ref}}$. The generator's total revenue per MWh is $p_t + (S - P_t^{\text{ref}})$. A crucial feature of the CfD is that the settlement term $(S - P_t^{\text{ref}})$ can be negative. If the reference price exceeds the strike price ($P_t^{\text{ref}} > S$), the generator must pay back the difference. If the reference price perfectly matches the price the generator actually receives for its energy ($P_t^{\text{ref}} = p_t$), the total revenue simplifies to $p_t + (S - p_t) = S$. In this ideal case, the CfD perfectly hedges the generator from market price volatility, locking in a fixed revenue of $S$ per MWh, similar to a FIT  .

### Quantifying Risk and Revenue

The structural differences between these schemes have profound and quantifiable implications for a generator's revenue profile. We can analyze this using a mean-variance framework, considering a producer whose output $Q$ and the market price $P$ are both stochastic random variables. An empirically observed feature of markets with high penetration of [variable renewable energy](@entry_id:1133712) (VRE) is a negative correlation between VRE output and market prices ($\rho_{P,Q}  0$), often called the **price cannibalization effect**, as high supply from renewables depresses prices .

Let's model the hourly revenue $R$ under three regimes: a pure merchant regime ($R_{\text{MER}} = P \cdot Q$), a fixed-premium FIP ($R_{\text{FIP}} = (P+s)Q$), and a FIT ($R_{\text{FIT}} = T \cdot Q$).

The expected revenue for the product of two [correlated random variables](@entry_id:200386) $P$ and $Q$ with means $\mu_P, \mu_Q$, standard deviations $\sigma_P, \sigma_Q$, and correlation $\rho$ is given by:
$$ \mathbb{E}[PQ] = \mu_P \mu_Q + \text{Cov}(P,Q) = \mu_P \mu_Q + \rho \sigma_P \sigma_Q $$

Applying this, the expected revenues for each regime are:
-   **Merchant**: $\mathbb{E}[R_{\text{MER}}] = \mathbb{E}[PQ] = \mu_P \mu_Q + \rho \sigma_P \sigma_Q$
-   **FIP**: $\mathbb{E}[R_{\text{FIP}}] = \mathbb{E}[(P+s)Q] = \mathbb{E}[PQ] + s\mathbb{E}[Q] = (\mu_P \mu_Q + \rho \sigma_P \sigma_Q) + s\mu_Q$
-   **FIT**: $\mathbb{E}[R_{\text{FIT}}] = \mathbb{E}[TQ] = T\mathbb{E}[Q] = T\mu_Q$

The variance of revenue reveals the risk profile. For a FIT, revenue only depends on the stochastic quantity $Q$, so price risk is eliminated:
$$ \text{Var}(R_{\text{FIT}}) = \text{Var}(TQ) = T^2 \sigma_Q^2 $$

For merchant and FIP revenues, which involve the product of two random variables, the variance is substantially more complex. For [jointly normal variables](@entry_id:167741), the variance of the product is:
$$ \text{Var}(PQ) = \mu_P^2 \sigma_Q^2 + \mu_Q^2 \sigma_P^2 + 2\rho\mu_P\mu_Q\sigma_P\sigma_Q + (1+\rho^2)\sigma_P^2\sigma_Q^2 $$

The producer under a FIP or merchant scheme is exposed to both **price risk** (terms with $\sigma_P^2$) and **volume risk** (terms with $\sigma_Q^2$), as well as the risk from their interaction (the covariance term). A FIT, by contrast, exposes the producer only to volume risk. This stark difference in risk exposure is a central theme in the analysis of these policies .

### Economic Efficiency and Dispatch Incentives

The choice between a FIT and a FIP also has significant consequences for overall [market efficiency](@entry_id:143751). In a simplified competitive market model, social welfare is maximized when generation occurs only up to the point where the marginal cost of production equals the marginal [willingness to pay](@entry_id:919482) (the market demand curve).

A FIP, by keeping the generator exposed to the market price $p_t$, preserves crucial economic signals. A generator with zero marginal cost operating under a fixed premium $s$ will find it profitable to produce as long as its total revenue, $p_t + s$, is non-negative, or $p_t \ge -s$. If market prices fall below this threshold (e.g., during times of very high renewable output and low demand), the generator has an incentive to curtail its output. This curtailment is economically efficient, as it avoids producing electricity for which society has a negative [willingness to pay](@entry_id:919482) .

A FIT, on the other hand, can create distorted incentives. Since the generator receives a fixed payment $T$ for every unit produced, irrespective of the market price, it has an incentive to produce at maximum capacity as long as $T$ is positive. This can lead to forced generation during periods of oversupply, driving market prices into negative territory. The production of units for which the market price is negative represents a **[deadweight loss](@entry_id:141093)**, as the cost of producing that energy (even if it is zero) exceeds its value to the market. Therefore, by maintaining a link to market prices, a FIP can promote more efficient dispatch and reduce [deadweight loss](@entry_id:141093) compared to a FIT, particularly in systems prone to oversupply .

### Investment, Valuation, and the Cost of Capital

The risk profiles inherent in FIT and FIP schemes directly influence how investors value projects and, consequently, the cost of financing them. A project's value, or **Net Present Value (NPV)**, is the discounted sum of its future net cash flows. For a risk-averse investor, the value of a risky future cash flow is not its simple expected value, but its **[certainty equivalent](@entry_id:143861)**—a lower, risk-adjusted value.

For an investor with Constant Absolute Risk Aversion (CARA) facing a normally distributed cash flow with mean $\mu_X$ and variance $\sigma_X^2$, the [certainty equivalent](@entry_id:143861) ($CE$) is given by:
$$ CE(X) = \mu_X - \frac{1}{2}\gamma\sigma_X^2 $$
where $\gamma$ is the coefficient of [absolute risk](@entry_id:897826) aversion. The term $\frac{1}{2}\gamma\sigma_X^2$ is the **risk penalty**, which increases with both the investor's [risk aversion](@entry_id:137406) and the cash flow's variance.

Applying this to our remuneration schemes, the net cash flow under a FIT is deterministic (assuming deterministic costs and output), so its variance is zero and there is no risk penalty. The net cash flow under a FIP, however, is exposed to price variance $v_t = \sigma_{P_t}^2$, resulting in a net cash flow variance of $Q_t^2 v_t$ (for deterministic quantity $Q_t$). The difference in NPV between a FIP and a FIT project can be expressed as the discounted sum of the differences in their certainty-equivalent cash flows over the project's life $T$:
$$ \Delta NPV \equiv NPV_{\text{FIP}} - NPV_{\text{FIT}} = \sum_{t=1}^{T} \frac{Q_t((\mu_t + \pi_t) - p_t^{\text{FIT}}) - \frac{1}{2}\gamma Q_t^2 v_t}{(1+r)^{t}} $$
This formula clearly illustrates the fundamental trade-off: the FIP might offer a higher expected price, but it comes at the cost of a significant risk penalty due to its price volatility .

This risk penalty is directly reflected in the project's cost of capital. A project's **Weighted Average Cost of Capital (WACC)**, the discount rate $r$ used in NPV calculations, is a function of its systematic, non-diversifiable risk. This risk is measured by the asset's **beta** ($\beta_A$), which reflects the covariance of its returns with the overall market portfolio.
-   A project with full **merchant exposure** has revenues that are correlated with the economy, giving it a significant positive asset beta and a high WACC.
-   A project under a long-term, creditworthy **FIT** has its market price risk almost entirely removed. Its cash flows become bond-like, with an asset beta close to zero. This dramatically lowers its WACC.
-   Furthermore, the stability of FIT cash flows allows the project to support a higher level of debt financing. In the presence of corporate taxes, this increased leverage enhances the value of the **tax shield** from interest deductions, further reducing the after-tax WACC.
-   A **FIP** represents an intermediate case. It reduces risk compared to a pure merchant project but retains more [systematic risk](@entry_id:141308) than a FIT. Consequently, its WACC will typically lie between the two extremes .

### Advanced Modeling and Implementation Issues

#### Bankability and Project Finance

In practice, the ability to secure financing is critical. **Bankability** refers to a project's ability to attract non-recourse debt from lenders. Lenders are primarily concerned with the downside risk and the certainty of being repaid. They assess this using metrics like the **Debt Service Coverage Ratio (DSCR)**, defined as the ratio of net operating cash flow to the required debt service payment for a given period.
$$ \text{DSCR} = \frac{\text{Revenue} - \text{Operating Costs}}{\text{Debt Service}} $$
Lenders impose covenants requiring that both the expected DSCR and the probability of the DSCR falling below a critical threshold are acceptable. For instance, a covenant might require $\mathbb{E}[\text{DSCR}] \ge 1.30$ and $\mathbb{P}(\text{DSCR} \lt 1.20) \le 0.25$.

The high revenue volatility of a FIP translates directly into high DSCR volatility. Even if a FIP project has a healthy expected DSCR, its wide distribution may cause it to fail the tail-risk covenant (e.g., the probability of default or near-default is too high). A FIT, by contrast, generates stable revenues and a much narrower DSCR distribution, making it far easier to satisfy lender covenants. This is a key reason why FIT-supported projects can secure more debt at better terms, illustrating a practical manifestation of the lower cost of capital .

#### The Capture Rate

A crucial metric for modeling VRE revenue under market exposure is the **capture rate**. It is defined as the ratio of the generator's actual generation-weighted average price to the simple [time-weighted average](@entry_id:903461) market price:
$$ \text{CR} = \frac{\mathbb{E}[P_t \cdot \omega_t]}{\mathbb{E}[P_t] \cdot \mathbb{E}[\omega_t]} $$
where $\omega_t$ is the normalized output. The term $\frac{\mathbb{E}[P_t \cdot \omega_t]}{\mathbb{E}[\omega_t]}$ is the generator's effective "captured price".

A capture rate of less than one ($\text{CR} \lt 1$) indicates that the generator tends to produce more when prices are lower than average, and less when prices are higher than average. This is the typical situation for solar and wind power due to the price cannibalization effect. A capture rate greater than one implies the opposite.

Under a FIP with premium $s$, the expected revenue per unit of expected output is not simply $\mathbb{E}[P_t] + s$, but rather $\text{CR} \cdot \mathbb{E}[P_t] + s$. The capture rate thus directly scales the market-based component of FIP revenue. A low capture rate erodes the value a generator can realize from the market, making the fixed premium component of its revenue all the more important. In contrast, under a FIT paying a tariff $T$, the expected unit revenue is simply $T$, independent of the capture rate .

#### Basis Risk in Premium Schemes

The effectiveness of a FIP or CfD as a hedging instrument depends critically on the choice of the reference price, $P_t^{\text{ref}}$. **Basis risk** arises from any mismatch between the price a generator actually receives for its energy ($p_t$) and the reference price used to calculate its premium ($P_t^{\text{ref}}$). The unhedged portion of the generator's revenue is proportional to this difference, $\Delta_t = p_t - P_t^{\text{ref}}$. The volatility of this term is a direct measure of basis risk.

Several choices for the reference price exist, each with different implications for basis risk :
-   **Zonal Price Reference**: If the reference price is the day-ahead price in the generator's own bidding zone ($P_t^{\text{ref}} = P_{B,t}^{\text{DA}}$), and the generator sells its power at that same price ($p_t = P_{B,t}^{\text{DA}}$), then the basis difference $\Delta_t$ is zero. This choice eliminates basis risk.
-   **Hub Price Reference**: If the reference price is a system-wide hub price ($P_t^{\text{ref}} = P_{\text{hub},t}^{\text{DA}}$), but the generator is paid its local zonal price, it is exposed to **locational basis risk**. This is the risk that congestion in the transmission network causes the local price to deviate from the hub price.
-   **Averaged Reference**: Some contracts use a reference price that is an average over a longer period (e.g., monthly or an annual "capture-based" price). This introduces **temporal or shape basis risk**. The generator is exposed to the risk that its hourly generation profile does not match the hourly price profile over that period, even if there is no locational price difference. This type of basis risk is often the most significant, as it leaves the generator exposed to the full volatility of hourly prices relative to a fixed benchmark.

Understanding and quantifying these different forms of basis risk are essential for accurately modeling the financial performance and risk exposure of projects under advanced FIP and CfD contracts.