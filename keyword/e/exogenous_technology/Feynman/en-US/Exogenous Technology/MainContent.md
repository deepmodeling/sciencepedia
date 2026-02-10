## Introduction
When we attempt to understand and predict the behavior of complex systems, from global economies to local ecosystems, we must first make a crucial distinction: what forces are generated from within the system, and what forces are imposed upon it from the outside? This separation between internal (endogenous) and external (exogenous) drivers is a cornerstone of scientific modeling. Technological progress, in particular, presents a fascinating challenge: is it an inevitable, clockwork-like force that arrives on a predetermined schedule, or is it something that grows and accelerates in response to our own actions and investments?

This article addresses this fundamental question by exploring the concept of exogenous technology. It provides a framework for understanding how progress can be treated as a given input, a gift from the outside that systematically changes the rules of the game. Across the following chapters, you will learn the core principles of modeling exogenous change and how this idea contrasts with the feedback-driven world of endogenous progress. We will begin by examining the underlying principles and mechanisms, exploring how abstract concepts like "progress" are translated into mathematical models. Following that, we will journey across a vast landscape of applications to see how this powerful lens helps connect and explain phenomena in economics, public health, ecology, and even the most profound ethical debates of our time.

## Principles and Mechanisms

### The Clockwork from Outside

Imagine you are building a magnificent, intricate model of a city. You are the master planner. You decide where to place the residential buildings, the commercial zones, and the parks. You control the flow of traffic by designing the road network. These are the internal, or **endogenous**, parts of your model—variables whose values are determined by the rules and interactions *within* the system you've created.

But your city does not exist in a vacuum. It is part of a larger world. The sun rises and sets on a schedule you cannot change. The price of steel for your skyscrapers is set by a global market far beyond your city's control. A major river flows along its border, providing water but also posing a flood risk. These external forces are given; they are inputs that your city must react to, but cannot influence. In the language of modeling, these are **exogenous** drivers. Their trajectories are determined "outside the model boundary" and are fed into your system as fundamental assumptions .

This distinction is one of the most fundamental concepts in understanding our world through the lens of science and mathematics. When we model complex systems—be it an economy, an ecosystem, or the global climate—we must draw a line between the parts of the world we are trying to explain (the endogenous) and the parts of the world we take as given (the exogenous).

Technological progress is often treated this way. Sometimes, it feels like a force of nature, a relentless tide of innovation that arrives on a schedule of its own. We can model it as an external clockwork, a gift from the outside that steadily makes our tools better, our processes cleaner, and our lives easier. This is the core idea of **exogenous technological change**.

### Charting the Future: Scenarios as Storylines

If we are to treat things like [population growth](@entry_id:139111), economic development, or technological progress as exogenous drivers, we face a critical question: what values should we feed into our model? We can't just invent numbers. The future path of global GDP isn't arbitrary; it's linked to assumptions about population, education, and political stability.

This is where the art of scenario building comes in. Scientists and modelers develop comprehensive, self-consistent narratives about how the future might unfold. A prominent example is the **Shared Socioeconomic Pathways (SSPs)**, which are used extensively in climate and energy research . The SSPs are not predictions; they are a set of plausible, internally consistent stories. For instance, "SSP1: Sustainability" tells a story of a world shifting toward a more sustainable path, with lower population growth, high education, and collaborative international relations. In contrast, "SSP3: Regional Rivalry" paints a picture of a fragmented world with resurgent nationalism, slower economic growth, and high population growth.

The power of this approach is in its consistency. By taking population ($P_t$) and GDP ($Y_t$) trajectories from the same SSP, a modeler ensures their core assumptions don't contradict each other . These coherent storylines provide the time-series data for the exogenous drivers that force the model forward. They act as **boundary conditions** for the system's evolution, defining the external world in which the model's internal dynamics—like the clearing of a market or the allocation of land—play out . Whether we are modeling the demand for crops in a region or the need for electricity in a country, these exogenous scenarios set the stage upon which our model's story unfolds.

### The Mathematics of Progress: A Simple, Powerful Idea

Let's make this tangible. How does "exogenous technological change" actually look inside a model? Imagine we are trying to project future carbon emissions. A very simple but powerful relationship, known as the Kaya identity, states that emissions are the product of economic activity and the emissions intensity of that activity:

$F(t) = \epsilon_t Y_t$

Here, $F(t)$ is the flow of emissions at time $t$, $Y_t$ is the economic activity (like GDP), and $\epsilon_t$ is the emissions intensity (e.g., tonnes of CO2 per dollar of GDP). We can take the GDP trajectory, $Y_t = Y_0 \exp(gt)$, from an SSP scenario. What about the intensity, $\epsilon_t$? This is where technology enters. Exogenous technological change can be modeled as a steady, autonomous improvement in efficiency, causing intensity to decline exponentially:

$\epsilon_t = \epsilon_0 \exp(-\lambda t)$

The parameter $\lambda$ is the "rate of learning" or the speed of autonomous technological progress. If $\lambda = 0.03$, it means our economy is getting 3% cleaner every year, automatically, like clockwork.

This simple formula is incredibly powerful. By plugging these equations into the definition of cumulative emissions, we can calculate precisely how much this steady progress helps us. For instance, one might calculate that a 3% annual improvement rate in emissions intensity could reduce total cumulative emissions over 30 years by about 37% compared to a world with no technological progress at all . This turns a vague concept—"things get better"—into a number that can inform monumental policy decisions about climate change.

### The Ghost in the Machine: When Technology Fights Back

The exogenous view of technology is elegant, useful, and often a very good approximation. But is it the whole story? What happens when technology isn't just an external gift, but something that grows and changes based on our own choices? What if the machine has a ghost in it?

This brings us to the crucial counterpoint: **[endogenous technological change](@entry_id:1124428)**. The most famous example is **learning-by-doing**. The idea is simple: the more you make of something, the better you get at making it. The cost to produce the 100th wind turbine is lower than the cost of the first, because you've learned, streamlined, and perfected the process.

This creates a **positive feedback loop**. Imagine two competing technologies, A and B. If A gets a small, early lead in adoption, its cumulative capacity ($K_A$) grows. Through learning-by-doing, its cost ($c_A$) falls. Because it's now cheaper, investors favor it, so its share of new investment ($s_A$) increases. This, in turn, accelerates the growth of its capacity, $K_A$, further lowering its cost. The loop is $K_A \uparrow \implies c_A \downarrow \implies s_A \uparrow \implies \frac{dK_A}{dt} \uparrow$, which reinforces the initial advantage .

This dynamic changes everything. The world is no longer predictable and pre-ordained. Instead, it becomes characterized by three new, fascinating properties:

1.  **Path Dependence**: The final outcome depends on the initial starting conditions. A small, random event that gives one technology a slight early edge can be amplified over time, determining the winner. The "best" technology doesn't always win; the "first" or "luckiest" one might. History matters deeply.

2.  **Multiple Equilibria**: The future is not a single, inevitable destination. The system has multiple possible stable states, like a ball that could settle into one of several valleys. The system could "lock in" to a future dominated by Technology A or a future dominated by Technology B .

3.  **Policy Leverage**: In a world of path dependence, temporary policies can have permanent effects. A short-term subsidy for a new technology might be just enough to help it accumulate enough experience to become cost-competitive on its own. It can push the system "over the hill" into a new valley, and even after the subsidy is removed, the system will not roll back. It's now on a new, self-reinforcing path .

This stands in stark contrast to an exogenous world. If technology costs are just externally defined schedules, there is one optimal path. The system is destined to follow it. But when technology learns from our choices, the future becomes a landscape of possibilities that we, through our actions, help create.

### Choosing the Right Lens: Wright vs. Moore

So, which is it? Is technological progress a clockwork from the outside (exogenous) or a creature that learns from within (endogenous)? The beautiful answer is: it depends on the technology. The modeler's challenge is to choose the right lens for the right situation.

This choice is perfectly captured by the debate between two famous models of technological progress :

- **Moore's Law**: Originally describing the doubling of transistors on a chip every couple of years, this has become a general term for progress that happens as a function of **calendar time**. Cost falls exponentially with time, $c(t) = c_0 \exp(-\alpha t)$. This is the archetypal model for **exogenous** change. It's the right lens for technologies whose improvement is driven by fundamental science, R&D in adjacent fields, or breakthroughs that are not strongly coupled to the production volume of that specific product. For example, advances in materials science might improve [solar cells](@entry_id:138078), regardless of how many panels were installed last year.

- **Wright's Law**: This law, also known as the [experience curve](@entry_id:1124759), states that cost is a function of **cumulative production**. Cost falls as a power law of total volume produced, $c(Q) = c_0 Q^{-b}$. This is the archetypal model for **endogenous** change—for learning-by-doing. It's the right lens for technologies where the main path to improvement is through perfecting manufacturing, streamlining supply chains, and gaining experience on the factory floor.

A wise modeler knows that correlation is not causation. For a growing technology, cumulative production ($Q$) and time ($t$) are often highly correlated. But they represent fundamentally different causal stories. Mistaking one for the other can lead to deeply flawed forecasts . The key is to ask: what is the true *driver* of progress? Is it the quiet ticking of the clock of science, or is it the loud hum of the factory floor?

The distinction between exogenous and endogenous technology, therefore, is not a mere technicality. It is a profound statement about the nature of progress. It forces us to confront whether we see the future as something that unfolds *before* us, or as something that is shaped *by* us, with all the feedback, uncertainty, and opportunity that this entails.