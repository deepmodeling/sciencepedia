## Introduction
Ensuring the lights stay on in our modern world is a deceptively complex challenge. It relies on a constant stream of new investment in [power generation](@entry_id:146388), yet these multi-billion dollar projects face immense financial uncertainty. In traditional markets, the promise of future revenue might be enough to spur construction, but electricity markets are unique. Regulatory interventions, designed to protect consumers, can unintentionally create a critical revenue shortfall, famously known as the "missing money" problem. This gap between the cost of new generation and the expected market revenue threatens grid reliability, as investors become unwilling to build the power plants we need. How, then, can we systematically bridge this financial divide and create a market that guarantees a reliable power supply at a fair price?

This article delves into the Net Cost of New Entry (Net CONE), an elegant economic concept designed to solve this very problem. We will first explore the foundational "Principles and Mechanisms," deconstructing how Net CONE is calculated and how it pinpoints the exact size of the "missing money" gap. Following this, the "Applications and Interdisciplinary Connections" chapter will reveal how this single figure becomes a cornerstone of modern energy systems, shaping everything from [electricity market design](@entry_id:1124242) and financial strategy to public policy and the transition to clean energy.

## Principles and Mechanisms

Imagine you want to open a small business—let's say a power plant. Like any business, you have costs. First, there's the enormous upfront investment to build the thing, a **capital cost** ($K$). Then, every year, you have **fixed costs** ($F$) for things like salaries, maintenance, and insurance, which you have to pay whether you produce a single spark of electricity or not. Finally, you have **variable costs**, like fuel, that depend on how much you operate. To be a successful entrepreneur in the power business, your annual revenues must, over the long run, cover all these costs.

This simple balancing act is the heart of ensuring our lights stay on. If power plants aren't profitable, no one will build them, and the grid will eventually fail to meet our needs. But how do you balance a massive, one-time capital cost against a stream of annual revenues? This is where our journey into the economics of electricity begins.

### The Great Balancing Act: Costs vs. Revenues

Let's first tackle the cost side of the equation. We can’t just compare the entire multi-million-dollar construction cost $K$ to a single year's revenue. That would be like trying to pay off your house mortgage with your first month's salary. Instead, we need to spread that huge initial cost over the economic lifetime of the power plant, say 20 or 25 years.

Economists have a wonderful tool for this called **annualization**. It’s the same principle used to calculate a mortgage payment. Given the initial investment ($K$), the lifetime of the asset ($T$), and the cost of capital ($r$)—which is essentially the interest rate investors demand for tying up their money—we can calculate an equivalent annual cost. This is done using a formula called the **Capital Recovery Factor**, which we can call $\alpha$. Multiplying the initial capital cost by this factor gives us the annualized capital cost, $\alpha K$. 

Now we can state the total annual cost of our power plant in a clear way. It’s the annualized capital cost plus the annual fixed operating costs. Economists call this the **Cost of New Entry (CONE)**, or sometimes Gross CONE.

$$ \text{CONE} = \alpha K + F $$

This number is incredibly important. It represents the total annual revenue a new power plant must earn, year after year, just to break even. It’s the revenue target, the financial finish line it must cross to be a viable investment. 

### The Curious Case of the Missing Money

So, our power plant needs to earn an amount equal to CONE each year. Where does this revenue come from? The obvious source is the **energy market**, where electricity is bought and sold every hour of every day. When our plant runs, it sells its electricity at the market price and earns a margin—the price minus its variable fuel cost. Let's call the total expected annual margin from the energy market $M$.

In a normal market, you might think that competition would ensure that, on average, the price is high enough for a new entrant to recover its CONE. That is, you'd expect $M$ to be roughly equal to $\text{CONE}$. But [electricity markets](@entry_id:1124241) are anything but normal.

For most of the year, there is usually more than enough generating capacity to meet demand. Competition is fierce, and the market price for electricity is often driven down to the variable cost of the most expensive generator currently running. In these conditions, many plants make just enough to cover their fuel costs, with very little left over to pay for their massive fixed and capital costs.

The real money, the revenue needed to cover those fixed costs, is supposed to be made during a few dozen critical hours a year. These are the moments of **scarcity**: a sweltering summer afternoon when every air conditioner is running, or a calm winter evening when there's no wind for the turbines and the sun has long set. During these brief periods, the demand for electricity pushes right up against the grid's maximum supply.

In a theoretically perfect market, the price during these scarcity events would skyrocket. It would rise to reflect the immense value society places on not having a blackout, a figure known as the **Value of Lost Load (VOLL)**, which can be as high as $\$20,000$ per megawatt-hour or more. These brief, extreme price spikes create what are known as **scarcity rents**—the primary source of income that peaking power plants rely on to recover their large capital investments. 

But here's the rub. Regulators and politicians get very nervous about letting prices rise to such extreme levels, fearing public outcry. As a result, most electricity markets have a **price cap**, a regulatory ceiling that prevents the energy price from exceeding a certain level, perhaps $\$1,000$ or $\$3,000$ per megawatt-hour. 

This price cap, while well-intentioned, has a devastating side effect. It systematically cuts off the primary revenue stream that generators need to recover their fixed costs. The expected energy market revenue, $M$, ends up being significantly less than the total annual cost, CONE. This shortfall is famously known as the **"missing money" problem**. If investors foresee this gap, they won't build new power plants, even if the grid desperately needs them. The result is a slow march toward an unreliable system with frequent blackouts. A market with a low price cap might find itself with only a tiny fraction of the capacity needed for a reliable grid, leading to hundreds of hours of expected shortages per year instead of just a few. 

### Net CONE: A Number to Save the Grid

This is where the elegant concept of the **Net Cost of New Entry (Net CONE)** comes to the rescue. If Gross CONE is the total annual revenue a plant *needs*, and the energy market margin $M$ is the revenue it *expects to get*, then the missing money is simply the difference between the two.

$$ \text{Net CONE} = \text{CONE} - M = (\alpha K + F) - M $$

Net CONE precisely quantifies the annual revenue shortfall for a new, efficient power plant. It’s the answer to the question, "How much extra payment, on top of energy market revenues, is needed to make a new investment worthwhile?"   This single number transforms a vague problem ("investors aren't building enough plants") into a concrete, solvable equation.

Once you have this number, you can design a market to deliver it. This is the purpose of a **capacity market**. Instead of just paying for energy produced ($\$/\text{MWh}$), this market pays generators for being available to produce power when called upon ($\$/\text{kW-year}$). It's a payment for reliability itself.

In a well-designed system, the price paid in the capacity market, let's call it $p_C$, is intended to fill the "missing money" gap. For a new plant to be built, the long-run equilibrium condition must hold:

$$ \text{Energy Revenue} + \text{Capacity Revenue} = \text{Total Annual Cost} $$
$$ M + p_C = \text{CONE} $$
$$ p_C = \text{CONE} - M = \text{Net CONE} $$

The target price for the capacity market is Net CONE. System operators use it to build a **demand curve for reliability**. They determine the level of reliability they want to achieve (for example, allowing for only 3 hours of scarcity per year) and anchor the price on their demand curve at that point to Net CONE. If the system has too little capacity, the market price will rise toward Net CONE, sending a powerful signal to investors: "Build more plants, and we will make sure you are paid enough to cover your costs!" 

### A Benchmark and a Backstop

The beauty of Net CONE doesn't stop there. It also serves a crucial role as a regulatory tool to prevent market abuse. Electricity grids are often dominated by a few large companies. In a [capacity auction](@entry_id:1122039), a dominant firm might be tempted to exercise **[market power](@entry_id:1127631)**—for example, by strategically withholding some of its power plants from the auction to create an artificial shortage and drive up the price for its remaining plants. 

Regulators can guard against this by using Net CONE as a bright-line test. They can impose an **offer cap**, a rule stating that no generator can bid into the [capacity auction](@entry_id:1122039) at a price above Net CONE. The logic is simple and powerful: since Net CONE represents the full, legitimate cost for an efficient *new* power plant to enter the market, any offer significantly above this benchmark is likely not based on actual costs but is instead an attempt to extract excessive profits. 

This cap doesn't mean the price is always Net CONE. If there's plenty of existing capacity, the market will clear at a much lower price. But the cap ensures that even if a firm tries to manipulate the market by withholding supply, it cannot drive the price above this reasonable, cost-based ceiling. It acts as both a competitive benchmark and a protective backstop, ensuring the market delivers reliability at a fair price. 

From a simple accounting problem for a single power plant, we have arrived at a sophisticated mechanism that underpins the reliability of entire nations. The concept of Net CONE is a testament to the power of economic engineering—it identifies a fundamental problem, quantifies it with precision, and provides the foundation for a market-based solution that keeps our modern world powered. It bridges the gap between engineering reality and financial viability, ensuring that when you flip a switch, the lights turn on.