## Introduction
Distinguishing true causation from mere correlation is one of the most fundamental challenges in science and policy. While the Randomized Controlled Trial (RCT) is the gold standard for establishing cause and effect, it is often impractical, unethical, or impossible to implement. This leaves a critical gap: how can we confidently answer "what if" questions using the observational data the world naturally provides? We need methods that can find a sliver of experimental evidence hidden within the messy reality of non-randomized data.

This article introduces Regression Discontinuity (RD), an elegant and powerful design within the causal inference toolkit that finds its power in the sharp breaks created by rules and policies. Across the following chapters, you will gain a deep understanding of this method. The first chapter, "Principles and Mechanisms," will demystify the logic behind both Sharp and Fuzzy RD, explain the core assumptions that make it work, and detail the critical tests used to build trust in its findings. Following that, "Applications and Interdisciplinary Connections" will showcase the incredible versatility of RD, exploring real-world examples from public health, economics, urban planning, and even neuroscience, revealing how arbitrary lines on a map or ticks of a clock can become windows into causality.

## Principles and Mechanisms

### The Beauty of the Break: Isolating Cause from Correlation

In our quest to understand the world, we are surrounded by a sea of correlations. We observe that neighborhoods with more libraries tend to have higher graduation rates, or that people who drink coffee tend to live longer. It is tempting, but treacherous, to leap from these observations to a conclusion of cause and effect. Do libraries *cause* students to succeed, or do affluent communities that value education simply have both? Does coffee *cause* longevity, or do coffee drinkers happen to have other healthy habits?

The gold standard for untangling this knot is the **Randomized Controlled Trial (RCT)**, where we randomly assign a treatment to one group and a placebo to another. Randomization works its magic by ensuring that, on average, the two groups are identical in every conceivable way—both seen and unseen—except for the treatment itself. Any difference in outcomes can then be confidently attributed to the treatment. But what can we do when an RCT is impossible, unethical, or impractical? We cannot randomly assign poverty to some children to study its effects, nor can we force a new financial regulation on a random half of the stock market.

Here, we must become detectives, searching for clues in the world as it is. We need to find situations where nature, policy, or administrative rules have inadvertently created a setup that *approximates* an RCT. This brings us to a profound distinction between two goals of data analysis: prediction and causal inference. Prediction is about finding patterns to make the best possible forecast. A time-series model like ARIMA, for instance, might be excellent at predicting tomorrow's stock price based on the patterns of the past. It is a powerful tool for forecasting, but it is mute on the question of "what if?" It cannot, by itself, tell you the causal impact of a new tax on that stock price. For that, we need a different kind of tool—one designed not to predict the future, but to understand the causal levers that shape it [@problem_id:2438832].

The **Regression Discontinuity (RD)** design is one of the most elegant and powerful tools in the causal inference toolkit. It finds its power not in complex correlations across all data, but in the simple, stark beauty of a sharp break.

### The Sharp Discontinuity: A Local Laboratory

Imagine a school district implements an intensive tutoring program for students who are struggling. To be objective, they create a rule: any student who scores below 80 on a pre-test is enrolled in the program. Everyone with a score of 80 or above is not [@problem_id:4570258]. This setup gives us the three key ingredients of an RD design: a continuous **running variable** (the test score), a precise **cutoff** (a score of 80), and a **treatment** (the tutoring program).

The "discontinuity" is the jump in treatment status right at the cutoff. A student with a score of 79.9 gets the treatment; a student with a score of 80.0 does not. Now for the beautiful insight: think about these two students. Is there any meaningful difference between them in terms of their motivation, their family background, their innate intelligence, or their study habits? It's highly unlikely. For this pair of students, separated by a trivial sliver of a point, their assignment to the tutoring program was essentially random. Near the cutoff, the administrative rule has created a natural "local laboratory" that mimics an RCT [@problem_id:5036278] [@problem_id:4776678].

To formalize this intuition, we turn to the **[potential outcomes framework](@entry_id:636884)**. Every student, let's call her Jane, has two potential outcomes: her final exam score if she gets tutoring, $Y_{\text{Jane}}(1)$, and her final exam score if she doesn't, $Y_{\text{Jane}}(0)$. The causal effect of the tutoring for Jane is the difference, $Y_{\text{Jane}}(1) - Y_{\text{Jane}}(0)$. Of course, we can never observe both potential outcomes for the same person; we only see the one that corresponds to the treatment she actually received.

The entire RD design hinges on one crucial, plausible assumption: the **continuity of potential outcomes**. This assumption states that if the tutoring program didn't exist, the relationship between a student's pre-test score and their average potential final exam score would be a smooth, continuous function. There is no reason to think that students' potential to succeed would mysteriously jump right at the 80-point mark. Any smooth trend—perhaps students with higher pre-test scores tend to do better anyway—is perfectly fine, as long as it's *smooth* [@problem_id:4570258] [@problem_id:3110485].

If we accept this assumption, the logic becomes beautifully simple. When we plot the *observed* final exam scores against the pre-test scores, any smooth trend we see is just the natural relationship between aptitude and performance. But if we see a sudden, discontinuous *jump* in the scores right at the cutoff of 80, what could have caused it? Only one thing changed discontinuously at that point: the treatment. That jump, therefore, must be the causal effect of the tutoring program for students right at the threshold. The quantity we estimate is precisely this jump:

$$
\tau_{\text{SRD}} = \lim_{x \to c^+} E[Y | X=x] - \lim_{x \to c^-} E[Y | X=x]
$$

where $Y$ is the observed outcome, $X$ is the running variable, and $c$ is the cutoff. This gives us the **Local Average Treatment Effect (LATE)**—the effect of the treatment for the specific population of individuals right at the cutoff [@problem_id:4570258].

### The Fuzzy Discontinuity: When Rules Are Bent

The world is often messier than a deterministic rule. Imagine a clinical guideline that recommends doctors prescribe a high-intensity statin for patients whose LDL cholesterol (the running variable) is above 130 mg/dL (the cutoff). In practice, doctors use their discretion. Some patients with LDL of 132 might not get the high-intensity statin, and some with LDL of 128 might get it for other reasons [@problem_id:5036278].

This is a **Fuzzy Regression Discontinuity (FRD)**. Crossing the cutoff doesn't guarantee treatment; it just makes it *more likely*. If we were to plot the probability of receiving the statin against the LDL score, we would no longer see a jump from 0 to 1. Instead, we might see the probability jump from, say, 0.20 to 0.70 [@problem_id:4626106].

Does this "fuzziness" ruin our design? Not at all. It just requires one more clever step. The observed jump in the health outcome (e.g., a reduction in hospitalizations) is now a "diluted" effect. It's the true effect of the statin, but averaged over a population where only a fraction of people actually changed their treatment status because of the guideline. To recover the true effect for those who were influenced, we need to account for this dilution.

The solution is to frame the problem as one of **Instrumental Variables (IV)** [@problem_id:4626151]. Think of the eligibility rule itself (having an LDL score $\ge 130$) as an "instrument." This instrument encourages people to take the treatment, but it doesn't force them. Under a few key assumptions—most importantly, that the eligibility rule only affects health outcomes *through* its effect on taking the statin, and that the rule doesn't convince anyone to *stop* taking a statin they otherwise would have (an assumption called **[monotonicity](@entry_id:143760)**)—we can identify the causal effect.

The method is stunningly elegant: we calculate the jump in the outcome at the cutoff and divide it by the jump in the probability of treatment at the cutoff [@problem_id:4626151].

$$
\tau_{\text{FRD}} = \frac{\lim_{x \to c^+} E[Y|X=x] - \lim_{x \to c^-} E[Y|X=x]}{\lim_{x \to c^+} E[D|X=x] - \lim_{x \to c^-} E[D|X=x]}
$$

The denominator measures how much the rule actually changed behavior at the margin, and the full ratio "re-inflates" the diluted outcome jump to give us the causal effect. This effect, however, is even more local. It is the **Local Average Treatment Effect for Compliers**: the average effect of the treatment on the specific group of people at the cutoff who took the treatment *only because* the rule change made them eligible [@problem_id:4626106] [@problem_id:4776678].

### The Art of the Skeptic: How We Build Trust in RDD

A good scientist is a good skeptic, especially of their own work. The "as-if random" assumption at the heart of RDD is powerful, but is it true? How can we be sure we are not fooling ourselves? The beauty of the RD design is that it comes with a built-in toolkit for self-critique.

The biggest threat is **manipulation** of the running variable. If the stakes are high, people will try to get on the "right" side of the cutoff. Imagine a test for entry into a prestigious school. Parents might hire tutors specifically to get their child's score from 79 to 80. Or a clinician, wanting a patient to receive a beneficial intervention, might subjectively nudge their risk score from just below to just above the eligibility threshold [@problem_id:5175036]. If this happens, the people at 79.9 and 80.1 are no longer comparable. The ones who successfully manipulated their score might be wealthier, more motivated, or sicker to begin with. The "local laboratory" is contaminated [@problem_id:3110485].

So, we must test for this.

**1. The Density Test:** The most direct way to look for manipulation is to examine the distribution of the running variable itself. In the absence of manipulation, we would expect the number of people to be smoothly distributed around the cutoff. If we see a suspicious "bunching" of individuals just above the cutoff and a corresponding "dip" just below it, it's a huge red flag. This can be formally checked with a **McCrary test**, which tests for a discontinuity in the density of the running variable [@problem_id:4776678] [@problem_id:5175036].

**2. Covariate Balance Tests:** We can also check other variables that should *not* be affected by the treatment rule. These are called **pre-treatment covariates**, such as age, gender, or baseline health indicators. Just as the potential outcomes should be continuous across the cutoff, so should the average values of these covariates. If we plot average age against the running variable and see a sudden jump at the cutoff, it tells us that the groups on either side are fundamentally different, and our core assumption is violated [@problem_id:4570228].

Imagine a study where we find trouble. The initial tests show a significant jump in the density of the running variable and a suspicious jump in the smoking status of participants right at the cutoff. This looks bad. But a good researcher digs deeper. They might perform a **"donut-hole" sensitivity analysis**, re-running the study while excluding a very narrow band of data right around the cutoff. If all the suspicious jumps suddenly vanish, it suggests the manipulation was highly localized—perhaps due to people rounding their scores to the nearest whole number. This tells us the problem might be manageable, and a "donut RDD" could be a valid way forward. This process of testing, finding problems, and investigating their nature is the heart of rigorous science [@problem_id:4570228] [@problem_id:5175036].

### From Principles to Practice: The Challenge of Estimation

The principle of RDD is to measure a jump at a single point. But in the real world, data is finite and noisy. We cannot simply look at the people *exactly* at the cutoff; there may be few or none. Instead, we must estimate the jump.

The standard approach is to use **local [polynomial regression](@entry_id:176102)**. We fit a curve (like a straight line or a quadratic) to the data on the left of the cutoff and a separate curve to the data on the right. The estimated jump is the difference in the heights of these two curves right where they meet the cutoff.

This practical step introduces crucial research choices. How wide a window of data around the cutoff should we use? This is the **bandwidth**. A very narrow bandwidth is true to the "local" spirit of RDD but uses little data, making the estimate noisy and sensitive to outliers (high variance). A very wide bandwidth uses lots of data, giving a stable estimate (low variance), but risks being biased if the true relationship between the running variable and the outcome is curvy [@problem_id:3157188]. How flexible should our curve be—a simple line or a complex spline with many "knots"? A more flexible model can capture complex relationships but can also overfit the noise in the data.

These choices require care and judgment. There is no single "right" answer, and researchers must show their results are robust to different reasonable choices. Regression Discontinuity is not a black box that spits out truth. It is a brilliant and logical design, a way of thinking that, when applied with skepticism and care, allows us to find a precious sliver of experimental evidence hidden within the messy world of observational data. Its beauty lies not in its complexity, but in its profound, disarming simplicity.