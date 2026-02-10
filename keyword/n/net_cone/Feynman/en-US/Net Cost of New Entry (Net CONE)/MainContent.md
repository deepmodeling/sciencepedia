## Introduction
The constant reliability of our electric grid is a modern marvel, yet it depends on power plants that may operate for only a few hours a year. This creates a fundamental economic challenge known as the "missing money" problem: how can these essential but seldom-used plants remain financially viable when their energy sales are minimal? This article addresses this critical question by providing a comprehensive exploration of the Net Cost of New Entry (Net CONE), an elegant economic concept that forms the cornerstone of modern [electricity market design](@entry_id:1124242) and ensures sufficient resources are available to keep the lights on.

This exploration is structured to build a complete understanding of this vital topic. In the "Principles and Mechanisms" chapter, we will deconstruct the Net CONE formula, starting with the costs of building a new power plant and then subtracting the revenues it can expect to earn from the energy market. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate how this powerful number is used in practice—from architecting reliable markets and ensuring fair competition to guiding multi-billion-dollar investment decisions across different market structures. By the end, you will understand how this single economic principle underpins the stability and long-term health of our power grid.

## Principles and Mechanisms

### The Quiet Hum of Reliability and the Economics of Being Ready

Think, for a moment, about the electric grid. It’s one of civilization's most astonishing achievements, a silent, sprawling machine that works so flawlessly we only notice it when it fails. This constant, unwavering reliability isn't magic. It is the result of careful engineering and, just as importantly, meticulous economic design. The grid must be ready for the hottest summer afternoon, the coldest winter night, and every moment in between. This readiness requires having enough power plants on standby, prepared to generate electricity at a moment's notice, even if some of them are only called upon to run for a few dozen hours in an entire year.

This raises a wonderfully simple but profound economic puzzle: How do you convince someone to build and maintain a billion-dollar power plant that might rarely sell any electricity? The owner has to pay for the land, the construction, the staff, and the insurance, year after year. If their only income comes from selling kilowatt-hours, and they sell very few, they will quickly go bankrupt. This conundrum is famously known in the energy world as the **“missing money” problem** . The revenue from selling energy alone is often insufficient to cover the total costs of keeping enough power plants on the system to ensure reliability.

To solve this puzzle, grid operators created a special kind of marketplace: the **capacity market**. In this market, power plant owners are not paid for the energy they produce, but for the *promise* of being available to produce it when called upon. It's a payment for readiness. But this leads to the next question, the one at the heart of our story: How much should we pay? What is the fair, economically sound price for this promise of availability? To answer this, we must build a power plant on paper.

### Building a Power Plant on Paper: The Cost of New Entry (CONE)

Let's put ourselves in the shoes of a risk-neutral investor considering whether to build a new power plant—say, a natural gas "peaker" plant designed to fire up quickly during periods of high demand . What are our costs?

The most obvious cost is the giant, one-time price tag to build the facility, known as the **overnight capital cost** ($K$). This includes everything from engineering and procurement to construction . But a power plant is an asset that will operate for decades, perhaps 20 or 25 years. We cannot simply compare a single, massive cost today with a stream of small revenues stretching far into the future. We need a way to put them on equal footing.

The solution is a beautiful financial principle you might already be familiar with from mortgages or car loans. Just as a bank converts the large price of a house into a series of manageable monthly payments, we can convert the large, upfront capital cost $K$ into an equivalent stream of annual payments. This conversion is done using a formula called the **Capital Recovery Factor** ($CRF$), or annualization factor ($\alpha$). This factor takes the [economic life](@entry_id:1124123) of the plant ($T$) and the cost of capital ($r$)—essentially the interest rate our investors demand—and calculates the levelized annual payment required to pay back the initial investment over its lifetime  . The annualized capital cost is simply $\alpha K$.

Of course, the costs don't stop once the plant is built. Every year, we have to pay for salaries, security, insurance, property taxes, and routine maintenance. These are the **fixed operations and maintenance (O&M) costs** ($F$), which we must pay regardless of whether the plant produces a single watt of electricity .

If we add these two pieces together—the annualized capital cost and the annual fixed O&M costs—we get the total annual bill our power plant must cover just to break even. This grand total is a crucial benchmark known as the **Gross Cost of New Entry**, or more simply, **CONE**.

$$ \text{CONE} = \alpha K + F $$

This figure represents the total annual revenue a new, efficient power plant would need to earn to be economically viable. It's the price of entry into the electricity generation business.

### From Gross to Net: Accounting for Real-World Revenues

Our hypothetical power plant, however, doesn't just sit there waiting for a capacity payment. It's also an active participant in the day-to-day energy market. When demand for electricity is very high and the system's supply cushion gets thin, the price of energy can, and should, rise dramatically. This phenomenon, known as **[scarcity pricing](@entry_id:1131280)**, is not a market flaw but a vital economic signal that reflects the high value of keeping the lights on when the system is under stress .

During these relatively few hours of scarcity, a power plant can earn significant profits over and above its fuel costs. These profits are often called **scarcity rents**. These rents, along with any other income from providing grid-stabilizing services (known as ancillary services), form a stream of revenue for the plant owner. Let's call the total expected annual income from these sources the **energy and [ancillary services](@entry_id:1121004) (E&AS) margin**, denoted by $M$ .

This means the "missing money" we need to cover isn't the *entire* Gross CONE. It's the Gross CONE *minus* the revenues we reasonably expect the plant to earn on its own in the energy markets. This simple but powerful subtraction brings us to the central concept of this chapter: the **Net Cost of New Entry (Net CONE)**.

$$ \text{Net CONE} = \text{Gross CONE} - \text{Expected Energy and Ancillary Services Revenues} $$

Or, using our familiar variables:

$$ \text{Net CONE} = (\alpha K + F) - M $$

This single number is beautiful in its elegance and utility. It represents the precise annual payment, per unit of capacity, that a new, efficient power plant needs from the capacity market to achieve zero economic profit—the break-even point for a competitive investor . It is the definitive answer to the "missing money" problem . If the capacity market offers a price equal to Net CONE, it makes it rational for our investor to build the plant. If the price is lower, they will walk away.

### Net CONE in Action: The North Star of the Capacity Market

Now that we have derived this fundamental number, what do grid operators do with it? Net CONE becomes a foundational tool, a "North Star" that guides the entire capacity market in two critical ways.

First, Net CONE serves as a **competitive benchmark** for ensuring long-term reliability. Grid operators know they need a certain amount of total capacity to keep the system reliable. They construct a demand curve for this capacity. The most important point on this curve is the price they are willing to pay to secure the target amount of resources. By setting this price equal to Net CONE, they send a clear and powerful signal to the market: "If the system needs more capacity to stay reliable, we are prepared to pay a price that makes it economically viable for a new, efficient power plant to be built" . This anchors the entire market to the real-world cost of ensuring a dependable electricity supply.

Second, and just as importantly, Net CONE is used to ensure fairness and prevent market manipulation. In any market with a small number of large players, there is a risk that one of them could try to exercise **[market power](@entry_id:1127631)**—for instance, by withholding their capacity from the market to artificially create a shortage and drive up the price for everyone .

To combat this, regulators often implement an **offer cap**. No market participant is allowed to submit a bid higher than this cap. The perfect, economically-justified value for this cap is Net CONE . Why? Because Net CONE represents the legitimate cost for a competitive new entrant. A bid *above* Net CONE is an implicit admission that the bidder is asking for more than a competitive price—a strong sign of an attempt to extract supra-competitive profits.

By capping offers at Net CONE, regulators create a system that is both fair and efficient. It allows prices to rise to reflect genuine scarcity, but it places a hard ceiling that prevents a single firm from holding the market hostage. Even if a firm withholds some of its supply to push prices up, the clearing price can never exceed this reasonable, cost-based benchmark  . This allows individual power plants to offer based on their unique costs while using a technology-neutral backstop to protect consumers from non-competitive behavior.

In the end, Net CONE is far more than an abstract calculation. It is a concept of remarkable unity, elegantly weaving together the principles of engineering, finance, and microeconomics. It acts as a fundamental constant that provides stability and rationality to the multi-billion-dollar decisions required to keep our modern world humming with quiet, reliable power.