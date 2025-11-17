## Introduction
In any empirical field, from medicine to economics, the data we collect is often imperfect. While we strive for complete and accurate observations, real-world constraints frequently lead to incomplete datasets. Two of the most structured and common forms of this incompleteness are [censoring](@entry_id:164473) and truncation. Failing to account for these phenomena can lead to severely biased estimates and invalid scientific conclusions. This article tackles this fundamental challenge in statistical analysis by providing a clear and comprehensive guide to understanding and handling censored and [truncated data](@entry_id:163004).

First, in **Principles and Mechanisms**, we will establish the crucial distinction between [censoring](@entry_id:164473) and truncation, explore their various forms, and introduce the foundational statistical tools used for their analysis, including Maximum Likelihood Estimation and the Kaplan-Meier method. Then, in **Applications and Interdisciplinary Connections**, we will demonstrate the far-reaching impact of these techniques by exploring their use in diverse fields such as biomedical research, [engineering reliability](@entry_id:192742), and astrophysics. Finally, **Hands-On Practices** will offer an opportunity to solidify your understanding by applying these methods to practical problems. Through this structured journey, you will gain the skills necessary to perform robust and valid inference in the face of incomplete data.

## Principles and Mechanisms

In an idealized statistical setting, we often assume that we can fully observe the variable of interest for every subject in our sample. However, in nearly every field of empirical research—from engineering and medicine to sociology and economics—the data we collect are subject to various forms of incompleteness. Understanding the nature of this incompleteness is not merely a technicality; it is fundamental to the validity of statistical inference. This chapter delineates the principles and mechanisms of two primary sources of data incompleteness: **[censoring](@entry_id:164473)** and **truncation**. We will explore their formal definitions, the contexts in which they arise, and the statistical methods required to handle them correctly.

### The Fundamental Distinction: Censoring versus Truncation

At first glance, [censoring](@entry_id:164473) and truncation may seem similar, as both result in data that do not fully represent the underlying distribution of interest. However, they are fundamentally different processes with distinct implications for analysis.

**Censoring** occurs when we have partial information about an observation. A [censored data](@entry_id:173222) point corresponds to a subject who is known to be in the sample, but for whom the event of interest has only been partially observed. We know the event occurred within a certain range (e.g., after a specific time), but we do not know the exact value. For example, in a study tracking patient survival, a patient who is still alive at the end of the study provides a censored observation; we know their survival time is *at least* the duration of the study, but we do not know the exact time of death. The key is that we have information about the individual and a lower (or upper, or interval) bound for their event time.

**Truncation**, by contrast, is a condition on the sample selection itself. Truncation excludes certain subjects from the sample altogether, based on the value of the outcome variable. If a subject's value falls into the truncated region, they are not observed and are not included in the dataset in any form. We are often not even aware of their existence. For instance, if a study on income is conducted by surveying only individuals with incomes above the poverty line, the resulting sample is left-truncated. We have no information whatsoever about individuals with incomes below that line because they were never included in the sample. This is a form of [selection bias](@entry_id:172119) that must be accounted for by adjusting the statistical model itself.

### Mechanisms of Censoring

Censoring can manifest in several ways, depending on the structure of the study. The appropriate analytical approach depends on correctly identifying the [censoring](@entry_id:164473) mechanism.

#### Right-Censoring

**Right-[censoring](@entry_id:164473)** is the most common form of [censoring](@entry_id:164473), occurring when the true event time is known only to be greater than a certain value. This happens when the study or observation period for a subject ends before the event of interest has occurred.

There are several sub-types of [right-censoring](@entry_id:164686):
*   **Type I Censoring**: The study is designed to end at a predetermined time $T$. All subjects who have not experienced the event by time $T$ are right-censored at $T$. For example, in a reliability test for [semiconductor lasers](@entry_id:269261), $N=50$ components might be tested for a fixed duration of $T = 1000$ hours. Any laser that fails before 1000 hours provides an exact failure time, while the 40 lasers still functioning at the 1000-hour mark are right-censored. We know their lifetimes are greater than 1000 hours, but not by how much [@problem_id:1902726]. A similar structure applies to a geological study of geyser eruptions monitored for a maximum of $C = 8.0$ hours per cycle; cycles without an eruption in this window are right-censored at 8.0 hours [@problem_id:1902748].

*   **Random Censoring**: The [censoring](@entry_id:164473) time for each subject is a random variable, independent of the event time. This is common in [clinical trials](@entry_id:174912) where patients may withdraw from the study for personal reasons, move away, or be lost to follow-up at various times. Another source of random [censoring](@entry_id:164473) is the occurrence of a "competing risk"—an event that precludes the observation of the primary event of interest. For example, in a cancer trial where the primary endpoint is tumor response, a patient might die from a heart attack before a response is observed. Their time to tumor response is then right-censored at their time of death [@problem_id:1902739]. The key feature is that [censoring](@entry_id:164473) can happen at different times for different subjects [@problem_id:1902747].

#### Left-Censoring

**Left-[censoring](@entry_id:164473)** occurs when the event is known to have happened *before* a certain observation time, but the exact time is unknown. This is symmetric to [right-censoring](@entry_id:164686). A classic example arises in environmental or pharmacological studies when an instrument has a lower [limit of detection](@entry_id:182454) (LOD). If a test is performed to measure the concentration of a chemical in a sample and the reading is below the LOD, say $\tau$, the true concentration is unknown but is known to be in the interval $[0, \tau)$. The observation is therefore left-censored at $\tau$ [@problem_id:1902762, thumbnail].

#### Interval-Censoring

**Interval-[censoring](@entry_id:164473)** occurs when an event is known to have occurred within a specific interval of time, $(t_L, t_R]$. This typically arises when subjects are not monitored continuously but are instead assessed at discrete follow-up times. For instance, consider a study on the time to viral activation where patients are tested only at annual checkups. If a patient tests negative at their 2-year checkup but positive at their 3-year checkup, their true time of viral activation, $T$, is not known precisely. We only know that it falls within the interval $(2, 3]$ years [@problem_id:1902716].

### Parametric Inference with Incomplete Data

When we can specify a parametric probability distribution for the event time (e.g., Exponential, Weibull, Pareto), the method of **Maximum Likelihood Estimation (MLE)** is a powerful and flexible tool for estimating the model parameters from [censored data](@entry_id:173222).

#### Constructing the Likelihood Function

The core principle of constructing a likelihood function with incomplete data is to represent the probability of observing the information we have for each subject. The total likelihood is the product of these individual contributions, assuming independence between subjects. Let $T$ be the random variable for the event time, with probability density function (PDF) $f(t; \theta)$ and [survival function](@entry_id:267383) $S(t; \theta) = P(T > t)$, where $\theta$ represents the model parameters.

The contribution of a single subject to the [likelihood function](@entry_id:141927) is:
*   For an **exact observation** at time $t_i$: The probability density of the event occurring at that exact moment is $f(t_i; \theta)$.
*   For a **right-censored observation** at time $t_i$: The event has not occurred by $t_i$. The probability of this is the probability of surviving past $t_i$, which is $S(t_i; \theta)$.
*   For a **left-censored observation** at time $t_i$: The event occurred before $t_i$. The probability of this is $P(T \le t_i) = 1 - S(t_i; \theta)$, also known as the [cumulative distribution function](@entry_id:143135) (CDF), $F(t_i; \theta)$.
*   For an **interval-censored observation** in $(t_{L,i}, t_{R,i}]$: The event occurred after $t_{L,i}$ but no later than $t_{R,i}$. The probability of this is $P(t_{L,i}  T \le t_{R,i}) = S(t_{L,i}; \theta) - S(t_{R,i}; \theta)$.

The full likelihood $L(\theta)$ is the product of these terms over all $n$ individuals in the sample. The [log-likelihood](@entry_id:273783) $\ell(\theta) = \ln L(\theta)$ is typically maximized to find the MLE $\hat{\theta}$.

#### Maximum Likelihood Estimation for Right-Censored Data

Let's formalize the likelihood for right-[censored data](@entry_id:173222), which is the most common scenario. For each subject $i$, we observe a time $t_i$ and an event indicator $\delta_i$, where $\delta_i = 1$ if the event occurred at $t_i$ and $\delta_i = 0$ if the observation was censored at $t_i$. The likelihood contribution for subject $i$ can be written compactly as:
$$ L_i(\theta) = [f(t_i; \theta)]^{\delta_i} [S(t_i; \theta)]^{1-\delta_i} $$
The full likelihood for a sample of $n$ subjects is $L(\theta) = \prod_{i=1}^{n} L_i(\theta)$.

Let's apply this to a clinical trial where the time-to-event follows an exponential distribution with rate parameter $\lambda$. The PDF is $f(t; \lambda) = \lambda \exp(-\lambda t)$ and the survival function is $S(t; \lambda) = \exp(-\lambda t)$. The likelihood is:
$$ L(\lambda) = \prod_{i=1}^{n} [\lambda \exp(-\lambda t_i)]^{\delta_i} [\exp(-\lambda t_i)]^{1-\delta_i} $$
This simplifies beautifully [@problem_id:1902747]:
$$ L(\lambda) = \left( \prod_{i=1}^{n} \lambda^{\delta_i} \right) \left( \prod_{i=1}^{n} \exp(-\lambda t_i) \right) = \lambda^{\sum \delta_i} \exp\left(-\lambda \sum t_i\right) $$
Let $D = \sum_{i=1}^{n} \delta_i$ be the total number of observed events, and $T_{total} = \sum_{i=1}^{n} t_i$ be the total observed time for all patients. The likelihood function is $L(\lambda) = \lambda^{D} \exp(-\lambda T_{total})$.

Taking the logarithm, differentiating with respect to $\lambda$, and setting to zero gives the MLE for $\lambda$:
$$ \frac{d\ell}{d\lambda} = \frac{D}{\lambda} - T_{total} = 0 \implies \hat{\lambda} = \frac{D}{T_{total}} $$
The MLE for the mean time to event, $\theta = 1/\lambda$, is, by the invariance property of MLEs:
$$ \hat{\theta} = \frac{1}{\hat{\lambda}} = \frac{T_{total}}{D} $$
This result is remarkably intuitive: the estimated mean lifetime is the total time all subjects were under observation (the "total time on test") divided by the number of events (failures) observed. This holds for both Type I and random [censoring](@entry_id:164473). In the laser reliability study [@problem_id:1902726], with $k=10$ failures, a sum of failure times of 4500 hours, and 40 units censored at 1000 hours, the total time on test is $T_{total} = 4500 + 40 \times 1000 = 44500$ hours. The MLE for the Mean Time To Failure (MTTF) is $\widehat{\text{MTTF}} = 44500 / 10 = 4450$ hours.

The same principle extends to other distributions. For a Pareto distribution with PDF $f(t; \alpha) = \frac{\alpha t_m^{\alpha}}{t^{\alpha+1}}$ and [survival function](@entry_id:267383) $S(t; \alpha) = (t_m/t)^{\alpha}$, the MLE for the shape parameter $\alpha$ under Type I [censoring](@entry_id:164473) at time $\tau$ can be derived by constructing the corresponding likelihood and maximizing it.

### Non-Parametric Estimation: The Kaplan-Meier Method

Often, assuming a specific [parametric form](@entry_id:176887) for the survival distribution is too restrictive. **Non-parametric methods** allow us to estimate the [survival function](@entry_id:267383) directly from the data without such assumptions. The most widely used method for right-[censored data](@entry_id:173222) is the **Kaplan-Meier estimator** (also known as the [product-limit estimator](@entry_id:171437)).

The intuition behind the Kaplan-Meier estimator is to model survival as a series of conditional steps. The probability of surviving past time $t$ is the probability of surviving past the first event time, times the conditional probability of surviving past the second event time given survival past the first, and so on.

Let $t_{(1)}  t_{(2)}  \dots  t_{(k)}$ be the distinct event times observed in the sample. Let $d_j$ be the number of events at time $t_{(j)}$ and $n_j$ be the number of individuals "at risk" (i.e., alive and not yet censored) just before time $t_{(j)}$. The estimated conditional probability of surviving past time $t_{(j)}$, given survival up to that point, is $(n_j - d_j) / n_j = 1 - d_j/n_j$. The Kaplan-Meier estimate of the survival function $S(t)$ is the product of these conditional probabilities for all event times up to $t$:
$$ \widehat{S}(t) = \prod_{j: t_{(j)} \le t} \left(1 - \frac{d_j}{n_j}\right) $$
Crucially, censored observations do not change the survival estimate at the time they are censored; they simply reduce the number of individuals at risk for the next event time.

Consider a clinical trial where the goal is to estimate the probability that a patient has not achieved tumor response by the end of week 25 [@problem_id:1902739]. The observed events occurred at weeks 6, 12, 15, 24, 30, and 40.
*   Just before week 6, $n_1=10$ patients are at risk. One event occurs, so the survival probability is estimated as $1 - 1/10 = 0.9$.
*   Between week 6 and 12, one patient is censored at week 10. So, just before week 12, $n_2=8$ patients are at risk. One event occurs, so the conditional [survival probability](@entry_id:137919) is $1 - 1/8 = 7/8$.
*   Continuing this process, we calculate the [survival function](@entry_id:267383) at time $t=25$. The event times up to 25 are 6, 12, 15, and 24.
$$ \widehat{S}(25) = \left(1 - \frac{1}{10}\right) \times \left(1 - \frac{1}{8}\right) \times \left(1 - \frac{1}{7}\right) \times \left(1 - \frac{1}{5}\right) = \frac{9}{10} \times \frac{7}{8} \times \frac{6}{7} \times \frac{4}{5} = \frac{27}{50} = 0.54 $$
The estimated probability that a patient has not responded by week 25 is $0.540$.

### Understanding Truncation

Truncation requires a more fundamental adjustment to our analysis than [censoring](@entry_id:164473). Because truncated subjects are systematically excluded from the sample, the distribution of the observed data is not the same as the underlying population distribution. We must derive the correct [conditional distribution](@entry_id:138367) for the observed data.

#### Inference for Truncated Data

Let $f(x)$ be the PDF of the population distribution.
*   If the data are **left-truncated** at $t_0$, meaning we only observe subjects for whom $X \ge t_0$, the PDF of the observed data is the conditional PDF:
    $$ g(x) = \frac{f(x)}{P(X \ge t_0)} = \frac{f(x)}{S(t_0)} \quad \text{for } x \ge t_0 $$
*   If the data are **right-truncated** at $T$, meaning we only observe subjects for whom $X \le T$, the PDF of the observed data is:
    $$ g(x) = \frac{f(x)}{P(X \le T)} = \frac{f(x)}{F(T)} \quad \text{for } x \le T $$

Consider a historical study of marriage ages, which are modeled as exponential with rate $\lambda$. Due to records only starting in 1850, the sample of individuals born in 1830 is left-truncated at age $t_0=20$ [@problem_id:1902743]. For an exponential distribution, $f(x) = \lambda \exp(-\lambda x)$ and $S(t_0) = \exp(-\lambda t_0)$. The truncated PDF is:
$$ g(x; \lambda) = \frac{\lambda \exp(-\lambda x)}{\exp(-\lambda t_0)} = \lambda \exp(-\lambda(x - t_0)) \quad \text{for } x \ge t_0 $$
This is the PDF of an [exponential distribution](@entry_id:273894) shifted by $t_0$. Using this PDF to construct the likelihood function for a sample $x_1, \dots, x_n$ and maximizing it yields the MLE:
$$ \hat{\lambda} = \frac{n}{\sum_{i=1}^n (x_i - t_0)} = \frac{1}{\bar{x} - t_0} $$
This result makes intuitive sense due to the [memoryless property](@entry_id:267849) of the exponential distribution: the distribution of the remaining lifetime, given survival past $t_0$, is the same as the original distribution. This model would apply equally to a marine biology survey using a net that cannot catch fish shorter than $l_{min}$ [@problem_id:1902763].

For **right-truncation**, such as analyzing warranty claims for products that failed before the warranty period $T$ ends [@problem_id:1902745], the analysis is similar. The truncated PDF for an exponential lifetime is $g(y; \lambda) = \frac{\lambda \exp(-\lambda y)}{1 - \exp(-\lambda T)}$ for $0 \le y \le T$. When we construct and maximize the [log-likelihood](@entry_id:273783), the resulting score equation does not yield a simple [closed-form solution](@entry_id:270799) for $\hat{\lambda}$. Instead, the MLE must be found by numerically solving the equation:
$$ \bar{y} = \frac{1}{\hat{\lambda}} - \frac{T}{\exp(\hat{\lambda} T) - 1} $$
This is a common outcome in more complex likelihood problems, highlighting the need for [computational statistics](@entry_id:144702).

### An Advanced Consideration: Dependent Censoring

A critical assumption underlying nearly all standard [survival analysis](@entry_id:264012) techniques, including the Kaplan-Meier estimator and the likelihood methods described above, is that of **independent [censoring](@entry_id:164473)**. This assumption states that the mechanisms leading to [censoring](@entry_id:164473) are unrelated to the mechanisms leading to the event of interest. For any subject, knowing their [censoring](@entry_id:164473) time provides no information about their event time, and vice versa.

In many real-world scenarios, this assumption may be violated. For example, in a clinical trial, patients who are sicker (and thus have a higher instantaneous risk, or **hazard**, of death) may also be more likely to drop out of the study (a higher hazard of [censoring](@entry_id:164473)). This is a case of **dependent [censoring](@entry_id:164473)**.

Modeling dependent [censoring](@entry_id:164473) requires more advanced techniques, often within the framework of **[competing risks](@entry_id:173277)**. A potential approach is to model the relationship between the cause-specific hazards directly. Suppose the hazard for the event is $\lambda_T(t)$ and the hazard for [censoring](@entry_id:164473) is $\lambda_C(t)$. If we can postulate a relationship, such as $\lambda_C(t) = \alpha \lambda_T(t)$ for some constant $\alpha$, we can incorporate this into the likelihood function [@problem_id:1902737].

In a scenario with an exponential event time $T \sim \text{Exponential}(\lambda)$, the event hazard is constant, $\lambda_T(t) = \lambda$. The [censoring](@entry_id:164473) hazard is thus $\lambda_C(t) = \alpha \lambda$, implying the [censoring](@entry_id:164473) time $C$ also follows an [exponential distribution](@entry_id:273894), $C \sim \text{Exponential}(\alpha \lambda)$. The likelihood contribution for an observed event at time $y$ is based on the joint probability of the event happening at $y$ *and* [censoring](@entry_id:164473) happening after $y$: $f_T(y) S_C(y)$. The contribution for a [censoring](@entry_id:164473) at $y$ is $f_C(y) S_T(y)$. By constructing the full likelihood using these principles and maximizing it with respect to both $\lambda$ and $\alpha$, one can derive the MLE for the dependency parameter $\alpha$:
$$ \hat{\alpha} = \frac{\sum_{i=1}^{n}(1-\delta_i)}{\sum_{i=1}^{n}\delta_i} $$
This result is remarkably intuitive: the estimated [dependency ratio](@entry_id:185721) is simply the total number of censored observations divided by the total number of events. This demonstrates how, with sufficient assumptions about the dependency structure, it is possible to perform valid inference even when the independent [censoring](@entry_id:164473) assumption is violated. This opens the door to a richer and more realistic class of models for survival data.