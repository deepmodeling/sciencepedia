## Introduction
Computable General Equilibrium (CGE) models are powerful laboratories for economists and policymakers, allowing them to simulate the economy-wide impacts of policies like tax changes or trade deals. However, beneath their complex equations lies a fundamental challenge: these models are mathematically underdetermined, with more variables than rigid accounting laws to define them. This creates a critical knowledge gap for anyone trying to interpret their results, as the modeler must make crucial assumptions to make the system solvable.

This article addresses that gap by focusing on the "closure rules"—the set of theoretical assumptions that complete the model and, in doing so, dictate its behavior. These rules are not mere technicalities; they are the model's soul, representing distinct worldviews on how economies function. By understanding them, you can move from being a passive consumer of economic reports to an active, critical interrogator of the stories they tell. The following chapters will demystify this essential concept. First, under "Principles and Mechanisms," we will explore what closure rules are and demonstrate how different choices lead to dramatically different outcomes. Then, in "Applications and Interdisciplinary Connections," we will see how these rules are applied to analyze real-world issues in development, [environmental policy](@article_id:200291), and labor markets.

## Principles and Mechanisms

Imagine you want to build a perfect scale model of a city's water system. You'd map every pipe, every pump, every reservoir, and every faucet. You’d write down equations for flow rates and pressures. Now, what happens if the city decides to open a new fire hydrant? To predict the effect on the water pressure in your friend's apartment across town, your model needs to be complete. It needs to know which pumps will ramp up, which reservoirs will drain, and which valves will close. If you leave any of these decisions out, your model is just a collection of pipes with no rules of operation; it's an unsolvable puzzle.

An economy is much like this. And a **Computable General Equilibrium (CGE)** model is our attempt to map its intricate plumbing—the flow of money, goods, and labor between households, firms, and the government. But just like the water system, the economic map is not enough. We face a fundamental problem: there are always more variables (like the level of employment, the government's budget deficit, or the nation's investment rate) than there are rigid accounting laws (like "spending must equal income") to pin them all down. The system is mathematically *underdetermined*. We need to add rules. These extra, assumption-based equations are what we call **closure rules**. They are the modeler's way of deciding which valves turn and which pumps activate when a shock, like a policy change, hits the system.

This act of choosing is the art and soul of CGE modeling. Most CGE models aren't "estimated" from decades of data, which might reveal statistical patterns of adjustment. Instead, they are often **calibrated**: the modeler picks a set of parameters so that the model perfectly replicates the economy of a single year, a snapshot in time. This means the model's predictions for the future depend profoundly on the closure rules—the *theories of adjustment*—that the modeler chooses to impose . These choices aren't just technical tweaks; they represent fundamentally different worldviews about how an economy functions.

### A Tale of Two Economies: One Shock, Wildly Different Fates

Let's see this in action with a simple, yet powerful, thought experiment. Imagine a developing country receives a sudden windfall of foreign aid. Is this universally a good thing? How does the economy absorb it? The answer, as we'll see, depends entirely on the "world" we assume our model economy lives in .

**The Neoclassical World: The Well-Oiled Machine**

First, let's imagine a **Neoclassical** world. This is the economist's ideal: a perfectly efficient, flexible machine. Every person who wants a job has one, and every factory is running at full tilt. The economy is already producing at its maximum capacity, which we can call its **full-employment output ($y^{FE}$)**. In this world, the main constraint is a physical one: there simply aren't any more workers or machines to put to use.

What happens when foreign aid ($FA$) flows in? The country's total output $y^{FE}$ cannot increase, because it's already maxed out. So, how is the aid used? The aid allows the country to consume and invest more than it produces. The economic identity tells us that total domestic spending (or **absorption**, $D$) must equal output plus net imports. Since the foreign aid allows for more imports, we have $D = y + FA$. Since output $y$ is fixed at $y^{FE}$, the extra spending from the aid must be accommodated. In the Neoclassical closure, we assume that some component of domestic demand, let's call it autonomous absorption $a_0$, adjusts to make it all work. It rises to absorb the new resources, ensuring the books balance: $a_0^{NC} = (1 - a_1) \cdot y^{FE} + FA$ . The aid doesn't make the economic pie bigger; it simply provides an extra slice from abroad, which is then eaten.

**The Keynesian World: The Sleeping Giant**

Now, let's imagine a different world, a **Keynesian** one. This world is not a perfectly tuned machine; it's more like a sleeping giant. There are unemployed workers waiting for jobs and factories sitting idle. The primary constraint here isn't a lack of resources, but a lack of **aggregate demand**. There simply isn't enough spending in the economy to wake the giant up.

In this world, the influx of foreign aid is like a jolt of caffeine. It represents new spending. This new demand for goods and services signals to firms that they should hire more of those idle workers and fire up those silent factories. Output isn't fixed at all! It's determined by demand. An increase in foreign aid directly boosts demand, leading to a higher equilibrium output, $y^{KY} = \frac{a_0 + FA}{1 - a_1}$, where $a_0$ is the baseline level of autonomous spending . Notice the term $1-a_1$ in the denominator; this is the marginal propensity to save, and its presence creates a **multiplier effect**. The initial boost from the aid gets re-spent, creating more income, which is spent again, and so on. The total increase in economic activity can be much larger than the aid itself!

The contrast is stunning. In the Neoclassical world, the aid is simply absorbed. In the Keynesian world, it kicks off a virtuous cycle of growth. The *same policy*, in the *same model*, produces entirely opposite conclusions about its effect on national output, all because of one change in a closure rule—one change in our assumption about how the world works.

### Economic Detective Work: Reading the Closures in the Wild

This might seem abstract, but it has profound real-world implications. When you read a report from a major international institution about the predicted effects of a tax cut, a carbon price, or a trade deal, you are not reading a statement of fact. You are reading a story, and the plot of that story was written by the closure rules the authors chose. With a little detective work, you can often figure out what those choices were.

Let's put on our detective hats and examine the evidence from a hypothetical CGE study that analyzes an import tariff change . The report gives us a table of results—percentage changes in key variables.

**Clue #1: The Labor Market**

Look at the lines for wages and employment.

*   If the report says that after the policy shock, the real wage stayed exactly the same ($\Delta w = 0$), but aggregate employment went up ($\Delta N > 0$), you can be almost certain the modelers used a **Keynesian labor market closure**. They assumed that wages are "sticky" and that a pool of unemployed workers is available to be hired if demand increases. This is the "sleeping giant" assumption.
*   Conversely, if the report says aggregate employment was unchanged ($\Delta N = 0$), but the real wage fell ($\Delta w  0$), you're looking at a **Neoclassical labor market closure**. They assumed the economy is always at "full employment," so the labor market must adjust through price (wages), not quantity (the number of jobs). This is the "well-oiled machine" assumption.

**Clue #2: The Government's Budget**

Next, look at the line for government savings (the budget surplus or deficit).

*   Suppose the tariff change reduces government revenue. If the report shows that government savings is unchanged ($\Delta S_G = 0$), the modelers have used a **fixed government savings closure**. This is a powerful assumption. It means they've built into the model that some *other* tax, like an income tax, or some government spending program automatically adjusts to fill the revenue hole and keep the budget balanced.
*   If, on the other hand, the report shows that government savings fell ($\Delta S_G  0$) and the deficit widened, they've likely used a **fixed tax rates closure**. They assumed that tax policy is fixed and the government's budget simply absorbs the shock.

Why does this detective work matter? Because recognizing the closure rule is like discovering the philosophical lens through which the authors view the world. An analysis that assumes a Keynesian labor market and flexible government deficits will almost inevitably conclude that policies creating demand are beneficial for growth. An analysis assuming a Neoclassical world with a fixed government budget will tell a story about efficiency, resource reallocation, and the constraints of a balanced budget.

The closure rule is not a footnote; it is often the main event. It is the choice that dictates whether a policy is a game-changing stimulus or a drop in the bucket. Understanding this single concept gives you a powerful tool to look beyond the headlines and spreadsheets, to question the story being told, and to appreciate the beautiful, complex, and deeply human art of modeling an economy.