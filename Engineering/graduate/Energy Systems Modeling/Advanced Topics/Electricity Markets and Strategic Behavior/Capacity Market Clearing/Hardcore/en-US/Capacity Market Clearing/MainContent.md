## Introduction
Ensuring a reliable supply of electricity, especially as power grids evolve, is a paramount challenge. While energy markets manage the real-time balance of supply and demand, they often fail to provide sufficient long-term investment signals, creating the "missing money" problem for generators needed for [resource adequacy](@entry_id:1130949). Capacity markets are the primary mechanism designed to solve this, ensuring that enough generation resources are available to meet peak demand years into the future. But how do these markets translate an abstract goal like "reliability" into a concrete price signal that drives billions of dollars in investment? This article demystifies the complex world of capacity market clearing.

We will embark on a structured journey through this critical topic. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, defining the capacity product, explaining how demand is constructed from reliability targets like LOLE, and detailing the auction mechanics that determine the market outcome. The second chapter, **Applications and Interdisciplinary Connections**, bridges theory and practice, exploring how these principles are applied to real-world power systems, accounting for physical grid constraints, accrediting new technologies like renewables and storage, and integrating complex policy rules. Finally, the **Hands-On Practices** section provides opportunities to apply these concepts to solve concrete modeling problems, reinforcing the key lessons learned. By the end, you will have a comprehensive understanding of how capacity markets function as the cornerstone of long-term grid reliability.

## Principles and Mechanisms

### The Capacity Product: From Installed Capacity to Performance Obligation

In a capacity market, the product being transacted is not electricity itself, but rather the accredited capability to produce electricity when the system needs it most. Understanding the principles of capacity market clearing begins with a precise definition of this product. The transition from a generator's physical nameplate rating to its market-qualified capacity involves a probabilistic de-rating to account for potential unavailability.

A generator's maximum sustained output under ideal conditions is its **Installed Capacity (ICAP)**. However, since no generator is perfectly reliable, the market must account for the statistical likelihood of forced outages. The product that is bought and sold is typically **Unforced Capacity (UCAP)**, which represents the expected deliverable capacity, accounting for the probability of such outages.

The relationship between these two measures is derived from first principles of probability. Let us consider a single generating unit with a deterministic $ICAP$. At any moment it is called upon to perform, its availability can be modeled as a Bernoulli random variable, $Z$, where $Z=1$ if the unit is available and $Z=0$ if it is on a forced outage. The available capacity is thus the random variable $ICAP \cdot Z$. The UCAP is defined as the expected value of this available capacity. 

$$UCAP = \mathbb{E}[ICAP \cdot Z]$$

Since $ICAP$ is a constant, we can write:

$$UCAP = ICAP \cdot \mathbb{E}[Z]$$

The expectation of the Bernoulli variable $Z$ is simply the probability that it equals $1$, i.e., the probability that the unit is available when called upon. This probability is directly related to the **Equivalent Forced Outage Rate on Demand (EFORd)**, an industry-standard metric that measures the probability that a unit is unavailable due to a forced outage when it is needed by the system. By definition, $EFORd = \mathbb{P}(Z=0)$. Therefore, the probability of being available is $\mathbb{P}(Z=1) = 1 - EFORd$. Substituting this into our equation yields the fundamental de-rating formula:

$$UCAP = ICAP \cdot (1 - EFORd)$$

This de-rating is crucial because it transforms the physical asset into a standardized, probabilistic product. A $100$ MW unit with an $EFORd$ of $0.1$ provides $90$ MW of UCAP, making it comparable to a $90$ MW unit with perfect reliability. This approach implicitly assumes that the outage probability is a stationary parameter, representative of the unit's future performance during periods of system need.

Beyond this statistical de-rating, the capacity product embodies a strict **performance obligation**. A resource that has cleared the market and receives a capacity payment is not merely being paid to exist; it is obligated to perform during declared scarcity events. Failure to do so results in significant financial penalties. This feature ensures that capacity suppliers have strong incentives to maintain their equipment and be available when [system reliability](@entry_id:274890) is at stake.

The economic decision faced by a capacity supplier during a shortage event can be modeled to reveal the true marginal cost of providing this reliability service . Consider a supplier with a capacity commitment of $1$ MW during a shortage event of duration $H$ hours. Let the variable cost of generation be $c$, the scarcity energy price be $s$, and the non-performance penalty rate be $p$ (all in $\$/\text{MWh}$). The supplier faces a choice:
1.  **Perform:** Generate $H$ MWh of energy. The net cost of this action is the generation cost minus the energy revenue: $H \cdot (c - s)$.
2.  **Do not perform:** Incur the penalty for the shortfall of $H$ MWh. The cost is $H \cdot p$.

A rational, cost-minimizing supplier will choose the less expensive option. Therefore, the cost it will actually incur during the shortage is $H \cdot \min\{c-s, p\}$. If the probability of a shortage event occurring during the commitment period is $\pi$, the expected net cost of holding the $1$ MW capacity obligation is $\pi H \min\{c-s, p\}$. In a competitive market, the capacity price, $P^{\text{cap}}$, must compensate the marginal supplier for this expected cost. Thus, the indifference price for the supplier is:

$$P^{\text{cap}} = \pi H \min\{c-s, p\}$$

This demonstrates that the capacity price is fundamentally linked to the costs and risks of the performance obligation itself, including energy market opportunity costs and penalty rates.

### The Demand for Capacity: Quantifying and Procuring Reliability

While the supply side offers a product defined by expected availability and performance, the demand side is determined by the system's need for reliability. Unlike conventional markets, the "demand" in a capacity market is not typically derived from the aggregation of individual consumer preferences. Instead, it is an administrative construct designed to achieve a specific, system-wide reliability target at a reasonable cost.

The most common reliability metric is the **Loss of Load Expectation (LOLE)**, defined as the expected number of time units (e.g., days or hours) per year in which system demand exceeds the available generating capacity. Calculating LOLE is a fundamentally probabilistic exercise that must account for uncertainty in both generation availability and system load. It is not a deterministic measure and cannot be accurately assessed by simply comparing expected load to expected capacity.

To illustrate, consider a system with a portfolio of generators, each with a known probability of being on a forced outage, and a load that varies stochastically. The LOLE is the sum of the **Loss of Load Probabilities (LOLP)** for each period in the year . For any given period $t$, the LOLP is the probability that the load $L_t$ will exceed the available capacity $C_t$. This is calculated using the law of total probability, by summing over all possible available capacity states:

$$\text{LOLP}_t = \mathbb{P}(L_t > C_t) = \sum_{k} \mathbb{P}(L_t > C_t | \text{state } k) \mathbb{P}(\text{state } k)$$

where each state $k$ corresponds to a specific combination of online and offline generators. For example, with $N$ identical generators each having an independent availability of $(1-q)$, the number of available units follows a binomial distribution, providing the probabilities for each capacity state. By convolving these capacity state probabilities with the load distribution, one can precisely calculate the LOLP for each period and sum them to find the system's LOLE. This rigorous probabilistic approach correctly captures the risk of extreme events in the tails of the distributions, which simplified deterministic methods would miss.

The system operator's goal is to procure enough capacity to meet a target LOLE, such as $0.1$ days per year. A critical step in market design is to translate this abstract reliability standard into a concrete procurement target in megawatts ($Q^*$). This can be accomplished by modeling the distributions of both available supply and peak demand .

For a system with a large number of independent generators, the **Central Limit Theorem** can be invoked to approximate the distribution of total available capacity, $A$, as a Normal distribution. The mean of this distribution, $\mathbb{E}[A]$, is precisely the system's total Unforced Capacity (UCAP), $U$. The variance, $\text{Var}(A)$, can also be derived from the parameters of the individual generators. If the daily peak load, $L$, is also modeled as a Normal random variable, then the margin, $M = A - L$, is also Normally distributed. A loss-of-load event occurs when $M  0$. The probability of this event (the LOLP) can then be expressed using the standard Normal CDF, $\Phi(z)$. The LOLE target equation becomes:

$$\text{Target LOLE} = (\text{Number of Days}) \times \mathbb{P}(L > A) = 365 \times \Phi\left(\frac{-(U - \mu_L)}{\sqrt{\sigma_A^2 + \sigma_L^2}}\right)$$

where $\mu_L$ and $\sigma_L^2$ are the mean and variance of load, and $\sigma_A^2$ depends on $U$. This equation can be solved for the minimum UCAP level, $U$, required to meet the target. This derived quantity, $Q^*$, forms the primary quantity anchor for the capacity market's demand curve.

### The Market Framework: Supply and Demand Curves

The capacity market clears by balancing supply offers against this administratively determined demand. The aggregate **supply curve** is constructed by stacking the UCAP offers from all participating resources in "merit order," from the lowest offer price to the highest. This creates a non-decreasing step-function, where each step represents the quantity offered at a specific price.

The **demand curve** in a modern capacity market is an administrative tool designed to reflect the social value of reliability while promoting market stability. Instead of a simple vertical line at the procurement target $Q^*$, most markets employ a downward-sloping demand curve. This design has two key anchoring points: a price anchor and a quantity anchor.

The **quantity anchor** is the reliability target $Q^*$ derived from the LOLE analysis described previously. This is the amount of capacity deemed necessary to achieve the desired level of system reliability.

The **price anchor** is the **Net Cost of New Entry (Net CONE)**. Net CONE represents the annualized revenue, per megawatt, that a hypothetical new "reference" generator would need to earn from the capacity market to be economically viable, after accounting for all other expected revenue streams . It is calculated as:

$$\text{Net CONE} = (\text{Annualized Capital Cost} + \text{Fixed O Cost}) - \text{Expected Net Energy  AS Revenue}$$

The annualized capital cost is determined by applying a **Capital Recovery Factor (CRF)** to the initial overnight capital cost of the reference plant. The CRF correctly amortizes the investment over the plant's economic life at a given cost of capital. The subtraction of expected revenues from the energy and ancillary services (AS) markets reflects the "missing money" principle: the capacity market's role is to provide the residual revenue required to incentivize sufficient investment to meet reliability needs. An increase in expected energy market revenues, for example due to higher scarcity prices, would lower Net CONE, thus reducing the price required from the capacity market.

The sloped demand curve is then constructed around the point $(Q^*, \text{Net CONE})$. The logic is that if the system has exactly the right amount of capacity, $Q^*$, the market price should be equal to Net CONE, providing the correct signal for a new entrant to build if needed. If capacity is scarce ($Q  Q^*$), the price should rise above Net CONE to incentivize more supply. If capacity is abundant ($Q > Q^*$), the price should fall below Net CONE to discourage new entry.

The slope of the demand curve itself can be derived from economic principles, reflecting the marginal social value of capacity. This value is the reduction in social cost achieved by adding one more megawatt of capacity. This cost is primarily the **Value of Lost Load (VOLL)**, a monetary estimate of the damage caused by an outage, multiplied by the reduction in **Expected Unserved Energy (EUE)**. As shown in , the slope $b$ of the demand curve at $Q^*$ can be set to equal the rate of change of this marginal value:

$$b = - \frac{d}{dQ} \left( \text{VOLL} \times \left(-\frac{d}{dQ}\text{EUE}(Q)\right) \right) \bigg|_{Q=Q^*} = \text{VOLL} \cdot K \cdot f_X(Q^*)$$

where $K$ is the number of critical hours and $f_X(Q^*)$ is the probability density of the net load distribution evaluated at the capacity level $Q^*$. This sophisticated approach embeds the economic value of reliability directly into the market clearing mechanism.

### Market Clearing and Auction Mechanics

With the supply and demand curves established, the market clearing process is straightforward. The **market clearing price** ($P$) and **cleared quantity** ($Q$) are determined by the intersection of the aggregate supply curve and the administrative demand curve. In a **uniform-price auction**, all suppliers whose offers were accepted (i.e., whose offer prices were at or below the clearing price) are paid the same uniform clearing price, $P$, for each megawatt of their cleared capacity.

Consider a simple example : A set of generators submit offers, which are stacked to form a supply curve. An administrative demand curve, say $P_D(Q) = 150 - 0.10Q$, is also defined. The equilibrium is found where the supply and demand curves cross. If the demand curve crosses a vertical segment of the supply stack (e.g., at a cumulative quantity of $550$ MW), then that quantity becomes the cleared quantity $Q$. The clearing price $P$ is then read off the demand curve at that quantity, for instance $P = P_D(550) = 95$. At this price of $95$, all generators who offered below $95$ will be cleared. If the market also includes constraints, such as a procurement limit ($Q \le 600$ MW) or a price floor ($P \ge 60$), these constraints must also be respected, potentially overriding the initial intersection point.

Capacity is typically procured through a competitive auction. Common formats include the **sealed-bid uniform-price auction**, where suppliers submit their offers privately, and the **descending clock auction**, where an auctioneer announces successively lower prices and suppliers indicate the quantity they are willing to offer at each price. Under idealized assumptions (such as independent private costs and no strategic behavior), these two formats are strategically equivalent and produce the same efficient allocation and clearing price .

### Ensuring a Stable and Competitive Marketplace

Real-world capacity markets incorporate several additional design features to ensure they function effectively over the long term and are resilient to strategic manipulation.

#### The Rationale for Forward Procurement

Most capacity markets are **forward markets**, meaning that capacity is procured several years in advance of the delivery year (e.g., three years forward). This forward-looking structure is essential for ensuring that new resources have sufficient time to be financed, permitted, and constructed to meet future reliability needs. If procurement were done on a short-term basis, there would not be enough time to build new capacity in response to a projected shortfall, leading to a significant risk of failing to meet the reliability standard.

This risk reduction can be quantified . The completion of a new project can be modeled as a probabilistic process. A longer lead time between procurement and delivery significantly increases the probability of successful project completion. For example, a project procured three years in advance might have an $88\%$ chance of being completed on time, whereas the same project procured only six months in advance might have less than a $30\%$ chance. This higher completion probability under forward procurement translates directly into a lower expected LOLE and, critically, a much lower probability of the system actually experiencing a reliability failure in the delivery year.

#### Mitigating Market Power

Because ensuring reliability is paramount, capacity markets can be susceptible to the exercise of market power. Market design includes rules to detect and mitigate such behavior from both sellers and buyers.

**Seller-side market power** arises when a supplier is structurally indispensable for meeting the reliability requirement. Such a supplier is termed **pivotal**. A formal **pivotal supplier test** can be conducted by calculating the **Residual Supply Index (RSI)** for each supplier . The RSI for a given supplier is the ratio of the total capacity available from all *other* sources (rivals and imports) to the total capacity requirement.

$$RSI_i = \frac{\text{UCAP from rivals of } i + \text{Imports}}{D_{\text{UCAP}}}$$

If $RSI_i  1$, it means the system cannot meet its reliability requirement without supplier $i$. This supplier is pivotal and has structural market power. To prevent them from exploiting this position by submitting uncompetitively high offers, pivotal suppliers are often subject to offer mitigation, such as a price cap based on their estimated costs.

**Buyer-side market power** is a more subtle but equally important issue. A large load-serving entity (LSE) that pays for a significant share of the total capacity cost may have an incentive to artificially suppress the market clearing price. It can do this by subsidizing a new or existing resource to submit an offer far below its actual costs . This subsidized, low-priced offer shifts the aggregate supply curve to the right, lowering the clearing price for everyone. The LSE's savings from the lower price on its large procurement volume can outweigh the cost of the subsidy, making this a profitable, albeit inefficient, strategy.

To combat this, markets implement a **Minimum Offer Price Rule (MOPR)**. The MOPR establishes a price floor for offers from certain resources, typically new ones or those receiving out-of-market state support. This floor is set at a level reflecting the resource's expected net cost of entry (related to Net CONE), effectively neutralizing the price-suppressive impact of the subsidy. The MOPR is thus a critical tool for preventing the distortion of investment signals and preserving a level playing field for all resources competing to provide capacity.