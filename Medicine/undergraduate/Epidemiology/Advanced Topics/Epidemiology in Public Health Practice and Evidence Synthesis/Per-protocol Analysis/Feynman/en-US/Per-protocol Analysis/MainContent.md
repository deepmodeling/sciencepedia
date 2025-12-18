## Introduction
When a clinical trial is complete, how do we determine if a new treatment was successful? The answer is more complex than it seems, hinging on what question we are truly asking. Do we want to know the real-world effect of *recommending* a drug, accounting for imperfect [patient adherence](@entry_id:900416)? Or do we want to understand the pure biological effect of the drug when taken *exactly as prescribed*? The first question is answered by Intention-to-Treat (ITT) analysis, while the second requires a Per-Protocol (PP) analysis—an approach riddled with profound statistical challenges. This article navigates the landscape of per-protocol analysis, providing the tools to discern a treatment's true efficacy.

Across the following chapters, you will delve into this critical area of [epidemiology](@entry_id:141409). "Principles and Mechanisms" unpacks the core theory behind per-protocol effects, exposing dangerous biases like [collider bias](@entry_id:163186) and [immortal time bias](@entry_id:914926), and introducing the powerful corrective technique of Inverse Probability Weighting. "Applications and Interdisciplinary Connections" demonstrates how the dialogue between ITT and PP analyses informs crucial decisions in [drug regulation](@entry_id:921775), clinical practice, and even biological discovery. Finally, "Hands-On Practices" offers the opportunity to apply these concepts, solidifying your understanding of how to estimate and evaluate per-protocol effects in practice.

## Principles and Mechanisms

Imagine we've just completed a massive, expensive clinical trial for a new heart disease medication. The data is in, and the moment of truth has arrived. But what is the "truth" we are looking for? It turns out, there isn't just one. In the world of [clinical trials](@entry_id:174912), there are at least two fundamental questions we might ask, each leading us down a different path of discovery, with its own unique insights and perils.

### The Two Questions: "Should I Prescribe?" vs. "Does It Work?"

The first question is a pragmatic one, asked by doctors and [public health](@entry_id:273864) officials: "Given all the complexities of the real world—where patients might forget doses, stop taking the drug due to side effects, or feel better and quit—what is the overall benefit of having this new drug as a treatment *option*?" This is the question of **Intention-to-Treat (ITT)**. The principle is simple and beautiful in its robustness: analyze them as you randomized them. If a patient was assigned to the new drug group, they stay in that group for the analysis, even if they never took a single pill.

The magic of randomization ensures that, at the start of the race, the two groups (treatment and placebo) are, on average, perfectly balanced in every conceivable way—both measured and unmeasured. The ITT analysis preserves this pristine balance. It gives an unbiased estimate of the effect of *assigning* the treatment strategy . The downside? If many people in the treatment group don't adhere, the observed effect will be a "diluted" or watered-down version of the drug's true potential. It's like estimating the power of a new engine by including cars that never left the starting line .

This leads us to the second, more mechanistic question, often asked by scientists and pharmacologists: "If a patient takes the drug exactly as prescribed, how does it *actually* affect their biology?" This is the **per-protocol** question. It seeks to understand the pure, undiluted effect of the treatment itself. Answering this question, however, is fantastically more difficult. In stepping away from the simple elegance of ITT, we wander into a landscape riddled with statistical traps and illusions.

### Defining the Ideal: A Glimpse into Parallel Universes

To even ask the per-protocol question in a way that isn't nonsense, we must first enter the strange and wonderful world of **[potential outcomes](@entry_id:753644)**. Imagine for every single person in our trial, there exists a set of parallel universes. In one universe, the person adheres perfectly to the new drug protocol, and we observe their outcome—let's call it $Y^{\bar a}$, their potential outcome under the active drug regimen $\bar a$. In another universe, that *exact same person* adheres perfectly to the placebo protocol, and we observe their outcome $Y^{\bar a'}$.

The true per-protocol causal effect is the difference between the average outcome across all individuals in the first universe and the average outcome in the second: $E[Y^{\bar a}] - E[Y^{\bar a'}]$. This is the ideal we seek—a comparison of two perfectly defined, counterfactual worlds. The problem, of course, is that we only get to live in one universe. We only ever observe one outcome for each person. The per-protocol analysis is therefore an attempt to use the data from our world to intelligently guess what's happening in these parallel ones.

And what exactly is a "protocol"? It's not always as simple as "take one pill a day." A real-world protocol is a set of rules over time. It might specify taking a dose within a certain time window, allowing for a "grace period" of, say, a few hours or even a day . Adherence becomes a dynamic process, a path a patient walks through time, and a deviation is a step off that path.

### The Peril of Simple Comparisons: Why Naive Analysis Fails

So, why not just compare the people who, in our real-world trial, happened to take the drug (the adherers) to those who didn't? This seems like the most obvious approach. It is also, as it turns out, almost always wrong. The moment we abandon the original [randomization](@entry_id:198186) groups and start regrouping people based on their behavior *after* the trial starts, we lose the guarantee of a fair comparison.

#### The Illusion of a Fair Race: Collider Bias

Let's think about who chooses to adhere to a difficult medication regimen. Adherence is not a random event. It's often the result of two things: the patient's underlying motivation or health status, and their ability to tolerate the treatment.

Imagine a simple causal diagram. Randomization ($Z$) influences who is asked to take the drug. Let's say an unmeasured factor, like "Health-Consciousness" ($U$), also influences adherence. Furthermore, the assigned treatment itself ($Z$) can affect adherence ($D$), perhaps due to side effects. So we have two arrows pointing to adherence: $Z \rightarrow D$ and $U \rightarrow D$. In the language of causal graphs, this makes adherence ($D$) a **[collider](@entry_id:192770)**.

Now, suppose "Health-Consciousness" ($U$) also leads to better health outcomes ($Y$), so $U \rightarrow Y$. At the start of the trial, [randomization](@entry_id:198186) ensures that "Health-Consciousness" is, on average, balanced between the treatment and placebo groups ($Z \perp U$).

But what happens when we decide to only look at the adherers (i.e., we condition on $D=1$)? We have inadvertently selected a very special group of people. In the treatment arm, someone who experiences nasty side effects will only adhere if they have very high "Health-Consciousness" to power through. In the placebo arm, adherence is easy, so you'll find people with both high and low "Health-Consciousness." The result? Among the adherers, the treatment group is now artificially enriched with highly health-conscious people compared to the placebo group. The original balance is destroyed. We are no longer comparing apples to apples . This phenomenon, known as **[collider-stratification bias](@entry_id:904466)** or [selection bias](@entry_id:172119), is one of the most subtle and dangerous pitfalls in [epidemiology](@entry_id:141409). By selecting on a common *effect* of two independent causes, we create a [spurious association](@entry_id:910909) between them .

#### A Story of Immortality

Another trap awaits in how we define our groups, especially when dealing with time. Suppose we are studying a drug to prevent hospitalization, and we define an "adherer" as someone who successfully takes their medication for the first four weeks. We then compare the hospitalization rate of this "adherer" group to the "non-adherer" group from the very beginning of the trial ($t=0$).

Do you see the paradox? To be included in the "adherer" group, a person *must have survived without being hospitalized for at least four weeks*. Their first four weeks of follow-up time are, by definition, "immortal." They cannot experience the event. This guarantees a period of zero risk for the adherer group, artificially deflating their overall event rate and making the treatment look far more effective than it is. This is known as **[immortal time bias](@entry_id:914926)**.

The correct approach is to treat adherence as a status that changes over time. A person contributes [person-time](@entry_id:907645) to the "non-adherent" group right up until they take their first dose. Their [person-time](@entry_id:907645) is then classified as "adherent" only for as long as they continue to take the drug. This time-dependent classification ensures that we are not using future knowledge to predict the past, preserving the natural flow of time and risk .

### The Tangled Web of Time

In any real study, adherence isn't a one-time decision. It's a continuous process, unfolding over weeks, months, or years. This introduces an even more complex form of [confounding](@entry_id:260626).

Consider our antihypertensive trial. A patient's treatment yesterday ($A_{t-1}$) affects their blood pressure today ($L_t$). Today's [blood pressure](@entry_id:177896), in turn, affects their decision to take their pill today ($A_t$)—perhaps high blood pressure motivates them, or side effects from low blood pressure discourage them. And, of course, today's [blood pressure](@entry_id:177896) ($L_t$) also directly predicts their long-term risk of a heart attack ($Y$).

This creates a feedback loop where treatment history influences a factor that is both a cause of future treatment and a predictor of the final outcome. This variable, $L_t$, is a **time-varying confounder affected by prior treatment**. We have a chain of events: $A_{t-1} \rightarrow L_t \rightarrow A_t$, with $L_t$ also pointing to $Y$.

We cannot simply "adjust" for $L_t$ in a standard [regression model](@entry_id:163386), because it is also part of the causal pathway from past treatment to the outcome. Doing so would block some of the very effect we want to measure. To untangle this web, we need a stronger assumption: **[sequential exchangeability](@entry_id:920017)**. This is the idea that at every single point in time, the choice to adhere is essentially random, conditional on the entire observed past history of covariates and treatments . It is a bold assumption, claiming that we have measured all the time-varying factors that form these feedback loops. It's like assuming we are running a new, perfectly balanced mini-trial every single day. The challenges grow as the causal chains get longer and more interconnected, creating new opportunities for selection biases to creep in .

### Recreating the Ideal World: The Power of Weighting

Given these daunting challenges, how can we ever hope to estimate the per-protocol effect? We cannot rewind time and force people down different paths. But we can use a remarkable statistical tool to build a "pseudo-population" in which the biases we've discussed are corrected. This tool is **Inverse Probability Weighting (IPW)**.

The intuition is this: in our [real-world data](@entry_id:902212), the decision to adhere is confounded. For example, sicker patients might be less likely to adhere. As a result, the group of adherers is unrepresentatively healthy. To fix this, we can perform a statistical re-balancing act. We identify an individual who followed a "surprising" path—for instance, a very sick patient who nonetheless managed to adhere—and we give them a larger weight in our analysis. This single individual's outcome now stands in for all the other sick patients who *would have* adhered if their adherence decisions hadn't been tied to their health status.

Technically, the weight for each person is calculated as the inverse of the probability of them following the treatment and adherence path they actually took, conditional on their past history. When we analyze this new, weighted population, the [confounding](@entry_id:260626) is broken. In the pseudo-population, a patient's health status no longer predicts their adherence, just as in a perfectly randomized trial .

In a longitudinal study, this weight is a product over time. For a person $i$ who remains uncensored (adherent) up to time $t$, their **stabilized weight** might look like this:

$$
w_i = \prod_{k=0}^{t} \frac{P(C_i(k)=0 \mid \bar L_i(k-1))}{P(C_i(k)=0 \mid \bar L_i(k-1), \bar A_i(k-1))}
$$

Here, $C_i(k)=0$ means the person remains uncensored (adherent) at time $k$. The denominator is the probability of adherence given the full history of covariates ($\bar L$) and past treatments ($\bar A$). Its inverse does the heavy lifting of up-weighting surprising choices. The numerator is a "stabilization" factor; it's the probability of adherence given a more restricted set of covariates. This term doesn't change the average result but helps to reduce the wild variability these weights can sometimes have .

### The Fine Print: No Free Lunch

This powerful technique is the closest we can get to estimating the true per-protocol effect, but it is not magic. It relies on three critical, untestable assumptions—there is no free lunch in [causal inference](@entry_id:146069).

1.  **No Unmeasured Confounding (Sequential Exchangeability):** We must have measured and correctly modeled all the factors that influence both adherence and the outcome at every point in time. If there is a crucial unmeasured factor, like the "Health-Consciousness" ($U$) from our [collider](@entry_id:192770) example, the bias will remain. Our pseudo-population will not be properly balanced. 

2.  **Positivity:** For any given patient history, there must have been a non-zero probability of both adhering and not adhering. If, in our data, every single patient with very high blood pressure stops taking the drug, we have a positivity violation. There is simply no information—no data—to tell us what would happen if a person with very high blood pressure *did* continue the drug. We cannot create a counterfactual out of thin air. In practice, when these probabilities get very close to zero, the [inverse probability](@entry_id:196307) weights become enormous, leading to wildly unstable estimates that are sensitive to the slightest change in our models .

3.  **Correct Models:** The weights are calculated from statistical models that estimate the probability of adherence at each time point. If our models are wrong—if we assume a linear relationship when it's quadratic, or miss an important interaction—the weights will be wrong, and our final estimate will still be biased .

Answering the "simple" question of what happens when people take a drug as prescribed forces us to confront the deepest challenges in [causal inference](@entry_id:146069). It requires us to imagine parallel worlds, to be wary of statistical illusions like colliders and immortal time, and to wield powerful but demanding tools like [inverse probability](@entry_id:196307) weighting. It is a journey that reveals the profound difficulty, and the profound beauty, of trying to discern cause and effect from the messy fabric of reality.