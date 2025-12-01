## Introduction
Survival analysis provides essential tools for studying time-to-event data, a common challenge in fields from biostatistics to engineering. While [non-parametric methods](@entry_id:138925) offer a first look, [parametric models](@entry_id:170911) provide a more powerful framework for understanding the underlying processes governing event times. These models assume that survival times follow a specific probability distribution, which allows for the smooth estimation of survival curves, [extrapolation](@entry_id:175955) beyond observed data, and a deeper interpretation of how covariates influence outcomes. However, choosing and correctly applying these models requires a solid grasp of their theoretical foundations.

This article serves as a comprehensive guide to two of the most fundamental [parametric models](@entry_id:170911): the Exponential and Weibull distributions. In the first chapter, **Principles and Mechanisms**, we will delve into the mathematical underpinnings of these models, exploring hazard functions, [parameter estimation](@entry_id:139349) with [censored data](@entry_id:173222), and the crucial frameworks of Proportional Hazards (PH) and Accelerated Failure Time (AFT) models. Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the real-world utility of these models across diverse fields like clinical research, epidemiology, and health economics. Finally, the **Hands-On Practices** chapter will solidify your understanding through guided problems that bridge the gap between theory and practical implementation.

## Principles and Mechanisms

In this chapter, we transition from the general concepts of survival analysis to the specification and application of [parametric models](@entry_id:170911). Parametric models assume that the survival time follows a specific probability distribution, which can be fully described by a small set of parameters. This approach offers several advantages, including efficiency in estimation (if the model is correctly specified), the ability to smoothly estimate the survival and hazard functions, and the capacity to extrapolate beyond the observed data range. We will focus on two of the most fundamental and widely used [parametric models](@entry_id:170911) in biostatistics: the Exponential and Weibull distributions.

### Fundamental Quantities of Survival Distributions

Before examining specific models, let us briefly recall the four key functions that characterize any time-to-event distribution. Let $T$ be a non-negative continuous random variable representing the time to an event.

The **survival function**, $S(t)$, gives the probability that the event has not occurred by time $t$:
$$ S(t) = \Pr(T > t) $$
By definition, $S(0) = 1$ and $\lim_{t \to \infty} S(t) = 0$.

The **probability density function (PDF)**, $f(t)$, describes the instantaneous probability of the event occurring at time $t$. It is related to the [survival function](@entry_id:267383) by:
$$ f(t) = -\frac{d}{dt} S(t) $$

The **[hazard function](@entry_id:177479)**, $h(t)$, also known as the [hazard rate](@entry_id:266388) or [instantaneous failure rate](@entry_id:171877), is the [conditional probability](@entry_id:151013) of the event occurring in an infinitesimally small interval after time $t$, given that the subject has survived up to time $t$. It is defined as:
$$ h(t) = \lim_{\Delta t \to 0} \frac{\Pr(t \le T  t + \Delta t \mid T \ge t)}{\Delta t} = \frac{f(t)}{S(t)} $$
The hazard function describes the instantaneous risk and its evolution over time, making it a central quantity in survival modeling.

The **[cumulative hazard function](@entry_id:169734)**, $H(t)$, represents the total accumulated risk up to time $t$. It is the integral of the hazard function:
$$ H(t) = \int_0^t h(u) \, du $$
From the relationship $h(t) = f(t)/S(t) = -S'(t)/S(t)$, we can see that $h(t) = -\frac{d}{dt} \ln S(t)$. Integrating this yields the fundamental link between the cumulative hazard and survival functions [@problem_id:4936588]:
$$ S(t) = \exp(-H(t)) $$
These relationships form the mathematical foundation upon which all parametric survival models are built.

### The Exponential Model: A Constant Hazard Assumption

The simplest parametric survival model is the **exponential model**, which is defined by the assumption of a **constant hazard function**.
$$ h(t) = \lambda $$
Here, $\lambda > 0$ is a constant [rate parameter](@entry_id:265473). This assumption implies that the instantaneous risk of the event is the same at all times, regardless of how long a subject has been at risk. This is known as the **memoryless property** [@problem_id:4936588].

From this simple assumption, all other functions of the exponential distribution can be derived. The cumulative hazard is:
$$ H(t) = \int_0^t \lambda \, du = \lambda t $$
The survival function is:
$$ S(t) = \exp(-\lambda t) $$
And the probability density function is:
$$ f(t) = h(t)S(t) = \lambda \exp(-\lambda t) $$

The constant hazard assumption, while mathematically convenient, is a strong one. Its plausibility depends critically on the underlying mechanism of the event. For example, in a hospital ward, the risk of accidental removal of an intravenous catheter might be driven by random patient movements or routine staff interactions. If these occur at a roughly constant rate over a short time frame (e.g., 72 hours), a constant hazard model may be a reasonable approximation [@problem_id:4977944].

However, in many biological and medical contexts, risk is not constant. Consider the risk of [acute rejection](@entry_id:150112) after an organ transplant. The risk is typically highest immediately following surgery and then decreases as the patient's body adapts and immunosuppressive therapy takes effect. A constant hazard model would be a poor fit, underestimating the initial risk and overestimating the later risk. Similarly, for mechanical components like orthopedic implants, the risk of failure often increases over time due to wear and tear or accumulated micro-damage—a phenomenon known as aging or wear-out. An exponential model cannot capture such increasing-risk dynamics [@problem_id:4977944]. To address these limitations, we need more flexible models.

### The Weibull Model: A Flexible Generalization

The **Weibull distribution** is a direct and powerful generalization of the exponential distribution that allows for non-constant hazard functions. It is one of the most widely used models in survival analysis due to its flexibility. While it can be defined in several ways, a particularly insightful approach is to define it via its [cumulative hazard function](@entry_id:169734) as a [power function](@entry_id:166538) of time [@problem_id:4936588]:
$$ H(t) = \left(\frac{t}{\lambda}\right)^k $$
where $k > 0$ is the **[shape parameter](@entry_id:141062)** and $\lambda > 0$ is the **[scale parameter](@entry_id:268705)**.

From this definition, we can derive the other key functions:
The **[hazard function](@entry_id:177479)** is the derivative of $H(t)$:
$$ h(t) = \frac{d}{dt} H(t) = \frac{k t^{k-1}}{\lambda^k} = \frac{k}{\lambda} \left(\frac{t}{\lambda}\right)^{k-1} $$
The **survival function** is:
$$ S(t) = \exp(-H(t)) = \exp\left(-\left(\frac{t}{\lambda}\right)^k\right) $$

The great utility of the Weibull model lies in its shape parameter, $k$, which determines the character of the [hazard function](@entry_id:177479) over time [@problem_id:4936588]:
-   **If $k=1$**: The hazard function becomes $h(t) = 1/\lambda$, a constant. The Weibull model reduces to the exponential model with rate $1/\lambda$.
-   **If $k > 1$**: The [hazard function](@entry_id:177479) $h(t)$ is a strictly increasing function of time ($t^{k-1}$ with $k-1 > 0$). This represents an increasing risk of failure over time, characteristic of aging or wear-out processes, such as the failure of an orthopedic implant.
-   **If $0  k  1$**: The hazard function $h(t)$ is a strictly decreasing function of time ($t^{k-1}$ with $k-1  0$). This represents a decreasing risk, where events are more likely to happen early on. This is suitable for modeling phenomena like post-surgical recovery, where the risk of complications is highest initially and then declines.

The [scale parameter](@entry_id:268705) $\lambda$ stretches or compresses the time axis. We can also derive important properties of the distribution. For instance, the **[median survival time](@entry_id:634182)**, $t_{0.5}$, is found by solving $S(t_{0.5}) = 0.5$:
$$ \exp\left(-\left(\frac{t_{0.5}}{\lambda}\right)^k\right) = 0.5 \implies t_{0.5} = \lambda (\ln 2)^{1/k} $$
The **mean survival time** can be shown to be [@problem_id:4936588]:
$$ \mathbb{E}[T] = \lambda \Gamma\left(1 + \frac{1}{k}\right) $$
where $\Gamma(\cdot)$ is the Euler Gamma function.

### The Shape of Survival: Interpreting Hazard Functions

The shape of the hazard function imparts a distinct signature on the survival curve and its logarithm. This relationship is not only mathematically elegant but also provides a basis for visual diagnostics.

Consider the logarithm of the survival function, $\log S(t) = -H(t)$. Its derivatives reveal the connection to the [hazard function](@entry_id:177479) $\lambda(t)$ (using $\lambda(t)$ here as a general notation for the [hazard function](@entry_id:177479), equivalent to $h(t)$):
$$ \frac{d}{dt} \log S(t) = -H'(t) = -\lambda(t) $$
$$ \frac{d^2}{dt^2} \log S(t) = -\lambda'(t) $$
The sign of this second derivative determines the [concavity](@entry_id:139843) of the $\log S(t)$ plot [@problem_id:4977990].
-   If hazard is **increasing** ($\lambda'(t) > 0$), then $\frac{d^2}{dt^2} \log S(t)  0$, so $\log S(t)$ is **strictly concave**.
-   If hazard is **constant** ($\lambda'(t) = 0$), then $\frac{d^2}{dt^2} \log S(t) = 0$, so $\log S(t)$ is **linear**.
-   If hazard is **decreasing** ($\lambda'(t)  0$), then $\frac{d^2}{dt^2} \log S(t) > 0$, so $\log S(t)$ is **strictly convex**.

A plot of $\log S(t)$ versus $t$ (or $\log t$ for certain models) can therefore serve as a powerful graphical tool to assess whether a constant, increasing, or decreasing hazard model might be appropriate for a dataset.

The shape of the [survival function](@entry_id:267383) $S(t)$ itself is also informative. Its second derivative is given by:
$$ S''(t) = S(t) \left( [\lambda(t)]^2 - \lambda'(t) \right) $$
Under a constant hazard ($\lambda'(t)=0$), $S''(t) = S(t)\lambda^2 > 0$, so $S(t)$ is strictly convex. Interestingly, if the hazard is decreasing ($\lambda'(t)  0$), the term $-\lambda'(t)$ is positive, which also ensures that $S''(t) > 0$. Therefore, for both constant and decreasing hazard functions, the survival curve $S(t)$ is strictly convex [@problem_id:4977990].

### Parameter Estimation from Observed Data

The parameters of a survival model are typically estimated using the method of **maximum likelihood**. The construction of the [likelihood function](@entry_id:141927) must account for the nature of survival data, particularly the presence of censoring and truncation.

#### Right-Censored Data

In most clinical studies, some subjects may not experience the event by the end of the study period, or may be lost to follow-up. These observations are **right-censored**. For a subject $i$, we observe a time $t_i$ and an event indicator $\delta_i$, where $\delta_i=1$ if the event occurred at $t_i$ and $\delta_i=0$ if the observation was censored at $t_i$.

The likelihood contribution for subject $i$ is the probability density of the event if it occurred, $f(t_i)$, or the probability of surviving beyond the censoring time, $S(t_i)$, if it did not. This can be written compactly as:
$$ L_i = [f(t_i)]^{\delta_i} [S(t_i)]^{1-\delta_i} $$
For a sample of $n$ independent subjects, the total likelihood is $L = \prod_{i=1}^n L_i$.

Let's apply this to the exponential model where $f(t) = \lambda \exp(-\lambda t)$ and $S(t) = \exp(-\lambda t)$. The likelihood contribution for subject $i$ is:
$$ L_i(\lambda) = [\lambda \exp(-\lambda t_i)]^{\delta_i} [\exp(-\lambda t_i)]^{1-\delta_i} = \lambda^{\delta_i} \exp(-\lambda t_i) $$
The full [log-likelihood](@entry_id:273783) for the sample is [@problem_id:4977940]:
$$ \ell(\lambda) = \ln \left( \prod_{i=1}^n \lambda^{\delta_i} \exp(-\lambda t_i) \right) = \left(\sum_{i=1}^n \delta_i\right) \ln \lambda - \lambda \left(\sum_{i=1}^n t_i\right) $$
To find the maximum likelihood estimate (MLE), we differentiate with respect to $\lambda$ and set the result to zero:
$$ \frac{d\ell}{d\lambda} = \frac{\sum \delta_i}{\lambda} - \sum t_i = 0 $$
Solving for $\lambda$ yields the MLE, $\hat{\lambda}$:
$$ \hat{\lambda} = \frac{\sum_{i=1}^n \delta_i}{\sum_{i=1}^n t_i} $$
This result has a highly intuitive interpretation: the estimated event rate is the total number of observed events divided by the total observed time-at-risk for all subjects [@problem_id:4936602].

#### Left-Truncated and Right-Censored Data

In some studies, subjects are not observed from time zero but only enter the study at a later time $L_i > 0$. This is known as **left truncation** or delayed entry. A subject is only included in the sample if their true event time $T$ is greater than their entry time $L_i$. The likelihood must be conditioned on this fact.

The correct likelihood contribution for a subject $i$ with entry time $L_i$, observed time $T_i$, and event indicator $\delta_i$ is the [conditional probability](@entry_id:151013) of the observation given inclusion in the study ($T > L_i$) [@problem_id:4936604]:
$$ L_i = \frac{f(T_i)^{\delta_i} S(T_i)^{1-\delta_i}}{S(L_i)} $$
For an exponential model, this becomes:
$$ L_i(\lambda) = \frac{[\lambda \exp(-\lambda T_i)]^{\delta_i} [\exp(-\lambda T_i)]^{1-\delta_i}}{\exp(-\lambda L_i)} = \lambda^{\delta_i} \exp(-\lambda(T_i - L_i)) $$
The [log-likelihood](@entry_id:273783) for the sample is then:
$$ \ell(\lambda) = \left(\sum \delta_i\right) \ln \lambda - \lambda \sum (T_i - L_i) $$
Maximizing this yields the MLE:
$$ \hat{\lambda} = \frac{\sum \delta_i}{\sum (T_i - L_i)} $$
Again, the interpretation is clear: the event rate is the total number of events divided by the total *net* time-at-risk, which is the time from entry to event or censoring for each subject [@problem_id:4936604].

It is important to recognize that our ability to estimate these parameters depends on the quality of our data. If events are only observed at discrete clinic visits (**interval censoring**), or if there is substantial **[unobserved heterogeneity](@entry_id:142880)** (frailty) in the population, where subgroups have different underlying risks, the assumptions of a simple parametric model may be violated, leading to biased estimates [@problem_id:4977944].

### Incorporating Covariates: PH and AFT Models

A primary goal of survival analysis is to understand how covariates, such as treatment assignment or patient characteristics, affect event times. There are two dominant frameworks for incorporating covariates into survival models.

#### The Proportional Hazards (PH) Framework

The **Proportional Hazards (PH) model** assumes that covariates act multiplicatively on the [hazard function](@entry_id:177479). For a subject with a vector of covariates $x$, the [hazard function](@entry_id:177479) is modeled as:
$$ h(t \mid x) = h_0(t) \exp(x^\top \beta) $$
Here, $h_0(t)$ is the **baseline [hazard function](@entry_id:177479)** for a subject with covariates $x=0$, and $\beta$ is a vector of [regression coefficients](@entry_id:634860). The key implication is that the ratio of hazards for two subjects with different covariates is constant over time. The term $\exp(\beta_j)$ is the **hazard ratio (HR)** associated with a one-unit increase in the covariate $x_j$.

For a parametric PH model, we specify a distribution for $h_0(t)$. For example, an exponential PH model assumes $h_0(t) = \lambda_0$, a constant baseline rate. The full hazard function is $h(t \mid x) = \lambda_0 \exp(x^\top \beta)$, which is still constant in time for any given subject, but differs between subjects based on their covariates [@problem_id:4936605].

#### The Accelerated Failure Time (AFT) Framework

The **Accelerated Failure Time (AFT) model** offers an alternative perspective. It assumes that covariates act multiplicatively on the time scale itself. If $T_0$ is a baseline event time, the event time $T$ for a subject with covariates $x$ is modeled as:
$$ T = T_0 \exp(x^\top \gamma) $$
This means the covariates accelerate or decelerate the time to event. The term $\exp(\gamma_j)$ is interpreted as a **time ratio (TR)**. If $TR > 1$, survival times are prolonged; if $TR  1$, they are shortened. A key feature of the AFT model is that this time ratio applies to all quantiles of the survival distribution. For example, if the time ratio for a treatment is $1.3$, it means the median, 25th percentile, and 75th percentile of survival time are all 30% longer in the treated group compared to the control group [@problem_id:4978005].

#### The Duality of the Weibull Model

The Weibull distribution holds a unique and powerful position in survival analysis because it is the only common distribution that satisfies both the PH and AFT model structures simultaneously. This duality provides a rich framework for interpretation.

Let's start with a Weibull AFT model, where the baseline survival is $S_0(t) = \exp(-\lambda t^k)$. The [survival function](@entry_id:267383) for a subject with covariates $x$ is [@problem_id:4977989]:
$$ S(t \mid x) = S_0(t \exp(-x^\top \gamma)) = \exp(-\lambda [t \exp(-x^\top \gamma)]^k) = \exp(-\lambda t^k \exp(-k x^\top \gamma)) $$
Now, let's derive the hazard function for this model:
$$ H(t \mid x) = \lambda t^k \exp(-k x^\top \gamma) $$
$$ h(t \mid x) = \frac{d}{dt} H(t \mid x) = (\lambda k t^{k-1}) \exp(-k x^\top \gamma) $$
If we define the baseline hazard as $h_0(t) = \lambda k t^{k-1}$, we see that $h(t \mid x) = h_0(t) \exp(-k x^\top \gamma)$. This is a PH model with a [regression coefficient](@entry_id:635881) vector $\beta = -k \gamma$.

This leads to a direct and elegant relationship between the hazard ratio and the time ratio for the Weibull family [@problem_id:4978005]:
$$ HR = \exp(\beta_j) = \exp(-k \gamma_j) = (\exp(\gamma_j))^{-k} = (TR)^{-k} $$
This equation is profoundly useful. For the exponential case ($k=1$), it simplifies to $HR = 1/TR$. For a Weibull model with an increasing hazard ($k>1$), a treatment effect that doubles survival time ($TR=2$) would correspond to a hazard ratio of $HR = 2^{-k}$, which is less than $0.5$. The effect on the hazard is magnified. This duality allows an analyst to interpret a single fitted Weibull model from both the hazard ratio and time ratio perspectives.

### Consequences of Model Misspecification

The efficiency and interpretability of [parametric models](@entry_id:170911) come at a price: they are vulnerable to **[model misspecification](@entry_id:170325)**. What happens if we fit an exponential model when the true data-generating process is Weibull with a shape parameter $k \ne 1$?

1.  **Inconsistent Parameter Estimates**: The maximum likelihood estimators for the model parameters (e.g., the log-hazard ratio $\beta$) will be **inconsistent**. That is, even with an infinitely large dataset, the estimator will not converge to the true value. Instead, it converges to a "pseudo-true" value that minimizes the Kullback-Leibler divergence between the misspecified model family and the true data-generating distribution [@problem_id:4936607].

2.  **Biased Survival Function**: The estimated baseline survival function will have the wrong shape (e.g., exponential instead of Weibull) and will therefore be a biased estimate of the true survival curve.

3.  **Invalid Standard Errors**: Standard methods for calculating confidence intervals, which rely on the Fisher information matrix, are no longer valid under misspecification. The true variance of the estimator must be calculated using a robust "sandwich" estimator that accounts for the discrepancy between the model and reality [@problem_id:4936607].

This sensitivity to misspecification highlights a critical trade-off. While [parametric models](@entry_id:170911) are powerful when correct, their assumptions must be carefully checked. In contrast, a [semi-parametric model](@entry_id:634042) like the **Cox [proportional hazards model](@entry_id:171806)** offers a more robust alternative for estimating hazard ratios. By leaving the baseline [hazard function](@entry_id:177479) $h_0(t)$ completely unspecified, the Cox model avoids making assumptions about the shape of the hazard over time. If the true data-generating process follows a PH structure (as the Weibull model does), the Cox model will provide a consistent estimate of the hazard ratio, even without knowing the underlying distributional family [@problem_id:4936607]. This robustness is a key reason for the Cox model's immense popularity in biostatistics.