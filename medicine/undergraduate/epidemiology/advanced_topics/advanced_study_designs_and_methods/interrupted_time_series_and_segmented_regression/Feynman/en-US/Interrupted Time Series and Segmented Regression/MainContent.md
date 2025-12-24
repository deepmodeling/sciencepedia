## Introduction
How can we know if a new public policy, a city-wide health campaign, or a change in clinical protocol actually worked? In many real-world scenarios, we cannot run a perfect [randomized controlled trial](@entry_id:909406) with a separate control group. This presents a fundamental challenge for scientists and policymakers seeking to make evidence-based decisions. We are often left asking, "What would have happened if we had done nothing?" This article introduces a powerful [quasi-experimental design](@entry_id:895528) created to answer that very question: the Interrupted Time Series (ITS) analysis.

This article provides a comprehensive overview of the theory and application of ITS and its statistical engine, [segmented regression](@entry_id:903371). It bridges the gap between the intuitive idea of comparing "before" and "after" and the rigorous scientific method required to infer causality. By reading through the following chapters, you will gain a robust understanding of this essential evaluative tool.

First, in **Principles and Mechanisms**, we will deconstruct the core logic of ITS, exploring the concept of the counterfactual and detailing how [segmented regression](@entry_id:903371) models precisely quantify an intervention's impact as an immediate level change and a long-term slope change. Next, in **Applications and Interdisciplinary Connections**, we will see the method in action across diverse fields—from [public health](@entry_id:273864) to economics—and learn how to address real-world complexities like seasonality and [confounding variables](@entry_id:199777). Finally, the **Hands-On Practices** section provides exercises to reinforce the foundational mathematical concepts that power this elegant and versatile method.

## Principles and Mechanisms

### The Ghost of the Unseen: Chasing the Counterfactual

In science, as in life, one of the most tantalizing questions we can ask is, "What if?" What if a new vaccine had never been developed? What if a nationwide seatbelt law had not been passed? To truly understand the effect of any action, any intervention, we must compare the world as it *is* with the world as it *would have been* without that action. This "what if" world, this ghostly parallel reality, is what scientists call the **counterfactual**.

In a pristine laboratory setting, creating a counterfactual is straightforward. We can take a colony of cells, divide it in two, and treat one half while leaving the other as a pristine "control group." The control group gives us a physical manifestation of the counterfactual. But how do you do this for an entire city? When a new clean-air policy is enacted across a whole country, we cannot keep a spare, identical "control country" in our back pocket to see what would have happened without the policy.

This is the great challenge of [public health](@entry_id:273864) and social science. We are often forced to evaluate interventions that are, by their nature, broad and singular. We cannot simply run a perfect, randomized experiment. So, what can we do? Do we give up on knowing? Absolutely not. We simply have to be more clever.

### Time as its Own Control

Here we arrive at the beautifully simple idea at the heart of the **Interrupted Time Series (ITS)** design. If we can't create a control group in space, perhaps we can find one in time. The "control" for the period *after* an intervention is the period *before* it—or, more precisely, the *projection* of the trend from before.

Imagine you are tracking monthly [asthma](@entry_id:911363)-related hospital admissions in a city. You have data for several years. You notice a trend; perhaps, due to a growing population and industrial activity, admissions are slowly creeping up month after month. You can plot this data and see a clear upward-sloping line.

Now, at a specific, known point in time—let's say January 1st, 2020—the city implements a strict new policy to reduce industrial [air pollution](@entry_id:905495). Starting from that date, you continue to track the hospital admissions. You notice that the number of admissions not only stops climbing but begins to fall. How can you attribute this change to the new policy?

The ITS method invites us to perform a thought experiment. We take the trend we established from the years of data *before* the policy was enacted. Then, we use it as a kind of crystal ball. We extrapolate that line forward, into the post-policy era. This extended line represents our best guess at the counterfactual—it's our picture of what would have likely happened to [asthma](@entry_id:911363) admissions if the city had done nothing at all. The difference between this projected line and what *actually* happened is our estimate of the policy's effect. The pre-intervention period has served as its own control.

### Drawing the Lines: The Machinery of Segmented Regression

This is a wonderful intuitive picture, but to do science, we need to make it rigorous. We can't just eyeball it. The mathematical engine we use to power the ITS design is called **[segmented regression](@entry_id:903371)**. It's a method for fitting distinct lines (or "segments") to the data before and after the interruption.

Let’s build the model from the ground up. Suppose $Y_t$ is our outcome—say, the number of [asthma](@entry_id:911363) admissions—at time $t$.

First, we describe the world before the policy. There's a baseline level of admissions and a pre-existing trend. We can represent this with a simple linear equation:

$$
E[Y_t] \approx \beta_0 + \beta_1 t
$$

Here, $\beta_1$ is the slope of the line before the interruption—the rate at which admissions were changing per month. $\beta_0$ is the intercept, which simply anchors the line at the beginning ($t=0$).

Now, the policy is enacted at time $T_0$. Suddenly, two things could happen.

1.  **An Immediate Shock**: The policy might have an immediate impact. The day it starts, the air quality might improve enough to cause a sudden, sharp drop in admissions. This is a **level change**. To capture this, we introduce a "switch" variable, often called $A_t$. This variable is simply $0$ for all times before $T_0$ and flips to $1$ for all times from $T_0$ onwards. The model becomes:

    $$
    E[Y_t] \approx \beta_0 + \beta_1 t + \beta_2 A_t
    $$

    The new parameter, $\beta_2$, directly measures the size of that immediate jump (or drop, if it's negative). It's the difference, right at time $T_0$, between where the old trend was heading and where the new trend begins.

2.  **A New Path**: The policy might also alter the long-term trajectory. Perhaps the gradual improvements in air quality cause the number of admissions to decrease steadily over the following months. This is a **slope change**. To model this, we need another variable that "activates" only after the policy. A clever way to do this is to define a variable, let's call it $P_t$, that measures the time elapsed since the intervention. So, $P_t = 0$ before $T_0$, and $P_t = t - T_0$ after. Our model now expands to its full, elegant form:

    $$
    E[Y_t] = \beta_0 + \beta_1 t + \beta_2 A_t + \beta_3 P_t
    $$

    This is the classic [segmented regression](@entry_id:903371) model . Let's look at what it tells us. Before the policy, $A_t=0$ and $P_t=0$, so the slope is just $\beta_1$. After the policy, the equation for the trend line rearranges to $(\beta_0 + \beta_2 - \beta_3 T_0) + (\beta_1 + \beta_3)t$. The new slope is $(\beta_1 + \beta_3)$. Therefore, the parameter $\beta_3$ represents the **change in the slope**—the difference between the pre-policy trend and the post-policy trend.

With this single equation, we have captured the entire story: the original trend ($\beta_1$), the immediate impact of the policy ($\beta_2$), and the change in the trend over time due to the policy ($\beta_3$).

### The Scientist's Burden: The Rules of Causal Inference

We have our model and our parameters. We've calculated that the policy led to an immediate drop of $\beta_2 = -50$ admissions and changed the slope by $\beta_3 = -5$ admissions per month. It's tempting to declare victory and publish a press release. But this is where the true discipline of science begins. Our model is an abstraction, and it is only as good as its underlying assumptions. To claim that $\beta_2$ and $\beta_3$ represent a *causal* effect, we must be able to defend our "crystal ball"—the assumption that the pre-intervention trend is a valid counterfactual. This requires us to play by a strict set of rules .

-   **No Other Shocks (No Co-interventions)**: Was the clean-air policy the *only* major thing that happened at that time? What if, in the same month, a major employer in the city shut down, drastically reducing traffic, or a new allergy clinic opened, offering better [asthma](@entry_id:911363) management? Any other event that could affect our outcome and occurs at the same time as the policy is a **co-intervention**. If we are not careful, our model will mistakenly attribute effects from these other events to the policy we are studying.

-   **No Peeking at the Future (No Anticipatory Effects)**: Humans are not passive subjects. If it was publicly known for months that the stringent pollution policy was coming, factories might have started upgrading their equipment and reducing emissions *before* the law's official start date. This would cause the pre-intervention trend to bend downwards before the interruption, making our projection of the "do-nothing" scenario too optimistic. Consequently, our estimate of the policy's effect would be smaller than it truly is.

-   **Stable Rules of Measurement**: The way we measure our outcome must remain consistent throughout the entire study period. If, by coincidence, the hospital system changed its definition of an "[asthma](@entry_id:911363)-related admission" at the same time the policy was enacted, it would create an artificial jump or drop in our data that has nothing to do with air quality. The same goes for the population itself; a sudden change in demographics could alter the underlying trend.

-   **Drawing the Right Picture (Correct Model Specification)**: We assumed the trends were straight lines. What if they are not? What if [asthma](@entry_id:911363) admissions always spike in the winter and fall in the summer? Our simple linear model would be misspecified. A robust ITS analysis must account for such **seasonality** and other patterns. Furthermore, data points in a time series are often not independent; this month's value can be influenced by last month's value, a phenomenon known as **[autocorrelation](@entry_id:138991)**. This must be statistically addressed to ensure our estimates and our confidence in them are correct.

Making a causal claim from an [observational study](@entry_id:174507) is an exercise in diligence and intellectual honesty. It requires us to become detectives, hunting for co-interventions and other threats to validity. We can never achieve the absolute certainty of a randomized trial, but by carefully constructing our model and rigorously challenging our own assumptions, we can build a powerful and convincing case. The Interrupted Time Series design, in its elegance, doesn't just give us answers; it teaches us the right questions to ask.