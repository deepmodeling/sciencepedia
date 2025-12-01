## Introduction
Accelerated Failure Time (AFT) models represent a powerful and distinct class of statistical tools for survival analysis. While many practitioners are familiar with Proportional Hazards (PH) models, which focus on how covariates affect the instantaneous risk of an event, AFT models offer an alternative and often more intuitive framework by directly modeling the effect of covariates on the event time itself. This distinction addresses a fundamental gap in modeling: how to quantify whether a factor speeds up or slows down the timeline to a specific outcome, rather than just altering momentary risk. Choosing between these frameworks is a critical decision driven by both empirical evidence and mechanistic understanding.

This article provides a comprehensive guide to understanding and applying AFT models. We will begin in the **Principles and Mechanisms** chapter by dissecting the core mathematical structure of AFT models, introducing the key concept of the "acceleration factor," and contrasting its assumptions with those of PH models. Next, the **Applications and Interdisciplinary Connections** chapter will illustrate how these models are used to gain mechanistic insights and solve complex problems in fields like medicine and engineering, including handling advanced [data structures](@entry_id:262134). Finally, the **Hands-On Practices** section will offer opportunities to solidify your understanding through practical exercises. This structured journey will equip you with the theoretical knowledge and practical skills to effectively leverage AFT models in your own research.

## Principles and Mechanisms

This chapter delves into the theoretical underpinnings of Accelerated Failure Time (AFT) models. We will dissect the core mathematical structure, explore the intuitive interpretation of its parameters, and contrast its foundational assumptions and outputs with those of the more widely known Proportional Hazards (PH) models. We will also detail the construction of the likelihood function, which is the basis for [parameter estimation](@entry_id:139349), and scrutinize the critical assumptions that support this inferential framework.

### The Log-Linear AFT Model and the Acceleration Factor

The Accelerated Failure Time model offers a direct and intuitive framework for understanding how covariates influence the time to an event. Its foundation lies in a linear model for the logarithm of the event time, $T$. For a subject with a vector of covariates $\mathbf{x}$, the AFT model is specified as:

$$ \log T = \mu + \mathbf{x}^{\top}\gamma + \sigma W $$

Here, $\mu$ is an intercept term, $\gamma$ is a vector of regression coefficients corresponding to the covariates, $\sigma$ is a positive [scale parameter](@entry_id:268705), and $W$ is a [random error](@entry_id:146670) variable with a specified distribution that is independent of the covariates $\mathbf{x}$. Often, the intercept $\mu$ is absorbed into the definition of the error term, or the model is written with an intercept included in the $\mathbf{x}^{\top}\beta$ term. A common and equivalent formulation is:

$$ \log T = \mathbf{x}^{\top}\beta + \sigma \varepsilon $$

where $\beta$ now includes the intercept (if an intercept is modeled) and $\varepsilon$ is a standardized error term with a pre-specified baseline distribution (e.g., standard normal, standard logistic, or standard extreme value).

This log-linear structure leads to a powerful and direct interpretation. By exponentiating both sides of the equation, we can express the event time $T$ directly:

$$ T = \exp(\mathbf{x}^{\top}\beta + \sigma \varepsilon) = \exp(\mathbf{x}^{\top}\beta) \exp(\sigma \varepsilon) $$

Let us define a **baseline event time**, $T_0$, as the event time for a subject with a covariate vector of all zeros ($\mathbf{x}=\mathbf{0}$). In this case, $T_0 = \exp(\sigma \varepsilon)$. This allows us to rewrite the relationship as:

$$ T(\mathbf{x}) = \exp(\mathbf{x}^{\top}\beta) T_0 $$

This equation is the conceptual heart of the AFT model. It states that the effect of the covariates $\mathbf{x}$ is to act multiplicatively on the baseline time scale $T_0$. The term $\psi(\mathbf{x}) = \exp(\mathbf{x}^{\top}\beta)$ is known as the **acceleration factor**. If $\psi(\mathbf{x}) > 1$, the event time is "accelerated" or stretched, meaning the subject is expected to experience the event later than a baseline subject. Conversely, if $\psi(\mathbf{x})  1$, the event time is "decelerated" or compressed, and the event is expected to occur sooner.

This [multiplicative scaling](@entry_id:197417) of time provides a clear interpretation for individual coefficients. For a single covariate $x_j$, holding all other covariates constant, a one-unit increase in $x_j$ changes the event time by a factor of $\exp(\beta_j)$. This factor is a **time ratio**, which makes AFT model results particularly easy to communicate in many clinical contexts [@problem_id:4772649]. For instance, if $\exp(\beta_j) = 1.3$, a one-unit increase in $x_j$ is associated with a $30\%$ increase in the expected time to the event.

### Implications for Survival, Quantiles, and Hazards

The [time-scaling property](@entry_id:263340) of the AFT model has direct consequences for the primary functions used in survival analysis: the survival function, [quantile function](@entry_id:271351), and hazard function.

**Survival Function**

The conditional [survival function](@entry_id:267383), $S(t | \mathbf{x}) = \mathbb{P}(T > t | \mathbf{x})$, can be expressed in terms of the baseline [survival function](@entry_id:267383), $S_0(t) = \mathbb{P}(T_0 > t)$. Using the relationship $T(\mathbf{x}) = \psi(\mathbf{x}) T_0$, we have:

$$ S(t | \mathbf{x}) = \mathbb{P}(\psi(\mathbf{x}) T_0 > t) = \mathbb{P}\left(T_0 > \frac{t}{\psi(\mathbf{x})}\right) = S_0\left(\frac{t}{\psi(\mathbf{x})}\right) $$

where $\psi(\mathbf{x}) = \exp(\mathbf{x}^{\top}\beta)$. This equation shows that the survival curve for a subject with covariates $\mathbf{x}$ is simply the baseline survival curve rescaled horizontally. The curve is stretched out if $\psi(\mathbf{x}) > 1$ and compressed if $\psi(\mathbf{x})  1$. This contrasts with the Proportional Hazards model, where covariates act to scale the survival curve vertically [@problem_id:5228296].

**Quantile Function**

The interpretation of AFT coefficients as time ratios is most clearly seen in their effect on [quantiles](@entry_id:178417) of the event time distribution. Let $Q_{\mathbf{x}}(p)$ be the $p$-th quantile of the event time distribution for a subject with covariates $\mathbf{x}$, defined by $\mathbb{P}(T \le Q_{\mathbf{x}}(p)) = p$. Let $Q_0(p)$ be the corresponding baseline quantile. Using the AFT relationship:

$$ \mathbb{P}(T \le Q_{\mathbf{x}}(p)) = \mathbb{P}(\psi(\mathbf{x}) T_0 \le Q_{\mathbf{x}}(p)) = \mathbb{P}\left(T_0 \le \frac{Q_{\mathbf{x}}(p)}{\psi(\mathbf{x})}\right) = p $$

By the definition of the baseline quantile, the argument of the probability must be $Q_0(p)$. Therefore:

$$ \frac{Q_{\mathbf{x}}(p)}{\psi(\mathbf{x})} = Q_0(p) \quad \implies \quad Q_{\mathbf{x}}(p) = \psi(\mathbf{x}) Q_0(p) $$

This shows that every quantile of the survival time distribution (including the median, [quartiles](@entry_id:167370), etc.) is multiplied by the same acceleration factor $\exp(\mathbf{x}^{\top}\beta)$. This uniform scaling of all time-to-event summaries is a powerful and intuitive feature of the AFT model [@problem_id:5228296] [@problem_id:4772649].

**Hazard Function**

The effect of covariates on the hazard function, $h(t | \mathbf{x}) = f(t | \mathbf{x}) / S(t | \mathbf{x})$, is more complex. To derive it, we first find the probability density function $f(t | \mathbf{x})$ by differentiating the survival function $S(t | \mathbf{x}) = S_0(t / \psi(\mathbf{x}))$ with respect to $t$:

$$ f(t | \mathbf{x}) = -\frac{d}{dt} S_0\left(\frac{t}{\psi(\mathbf{x})}\right) = -S'_0\left(\frac{t}{\psi(\mathbf{x})}\right) \cdot \frac{1}{\psi(\mathbf{x})} = f_0\left(\frac{t}{\psi(\mathbf{x})}\right) \frac{1}{\psi(\mathbf{x})} $$

where $f_0$ is the baseline density function. The [hazard function](@entry_id:177479) is then the ratio of the density to the [survival function](@entry_id:267383):

$$ h(t | \mathbf{x}) = \frac{f(t | \mathbf{x})}{S(t | \mathbf{x})} = \frac{f_0(t / \psi(\mathbf{x})) \cdot (1 / \psi(\mathbf{x}))}{S_0(t / \psi(\mathbf{x}))} = \frac{1}{\psi(\mathbf{x})} h_0\left(\frac{t}{\psi(\mathbf{x})}\right) $$

This relationship demonstrates that covariates rescale the [hazard function](@entry_id:177479) in two ways: the time axis is scaled by $1/\psi(\mathbf{x})$, and the hazard value itself is also scaled by $1/\psi(\mathbf{x})$. This is fundamentally different from the simple [multiplicative scaling](@entry_id:197417), $h(t|\mathbf{x}) = \theta(\mathbf{x}) h_0(t)$, assumed by the PH model [@problem_id:4949786].

### Distinguishing AFT from Proportional Hazards (PH) Models

The AFT and PH model families represent two different paradigms for modeling time-to-event data. Understanding their differences is crucial for correct application and interpretation.

**Interpretive Divergence: Time Ratio vs. Hazard Ratio**

The core difference lies in what their coefficients represent. As established, the AFT model parameter $\exp(\beta_j)$ is a **time ratio**. It answers the question: "By what factor does the event time change for a unit increase in $x_j$?" This applies to the median, mean, and all quantiles of the survival distribution.

In contrast, the PH model parameter $\exp(\beta_j)$ is a **hazard ratio**. It answers the question: "By what factor does the instantaneous risk of the event change at any given moment in time for a unit increase in $x_j$?"

Consider a clinical trial comparing a new therapy ($Z=1$) to a control ($Z=0$). If an AFT model yields $\exp(\beta_{\text{AFT}}) = 1.30$, the interpretation is that the new therapy prolongs the median (and any other quantile) time to the event by a factor of 1.30, or 30%. If a PH model yields $\exp(\beta_{\text{PH}}) = 0.75$, the interpretation is that the new therapy reduces the instantaneous risk of the event by 25% at any point in time, compared to control. The AFT model speaks to *how much longer* patients survive, while the PH model speaks to *how much lower* their risk is at any moment. These are distinct clinical questions, and the two models provide direct answers to them, respectively [@problem_id:4949797].

**Non-Equivalent Assumptions**

The AFT and PH assumptions are generally not compatible. That is, if one model holds, the other typically does not.

To see this, consider an example where the AFT model holds exactly, with a baseline Gompertz survival distribution. The baseline hazard is $h_0(t) = \lambda \exp(\gamma t)$. Using the AFT hazard transformation, the hazard ratio between a group with covariate $x=1$ and a baseline group with $x=0$ is:

$$ \mathrm{HR}(t) = \frac{h(t | x=1)}{h(t | x=0)} = \exp(-\beta) \exp\left(\gamma t [\exp(-\beta) - 1]\right) $$

This hazard ratio is clearly a function of time $t$, violating the PH assumption. For certain parameter values ($\beta>0, \gamma0$), the hazards for the two groups will even cross at a specific time point $t_c$, a phenomenon that PH models cannot represent [@problem_id:4949732].

Conversely, we can construct a model where PH holds but AFT fails. Suppose the baseline cumulative hazard is $H_0(t) = t + t^2$ and the hazard for a treatment group is proportional, $h_1(t) = c \cdot h_0(t)$. This satisfies the PH assumption by construction. If we then compute the ratio of the survival quantiles for the two groups, $R(p) = t_1(p) / t_0(p)$, we find that this time ratio is a function of the quantile level $p$:

$$ R(p) = \frac{-1 + \sqrt{1 - 4\ln(p)/c}}{-1 + \sqrt{1 - 4\ln(p)}} $$

Since the time ratio is not constant, the AFT assumption is violated. A plot of the quantile ratio $R(p)$ against $p$ can serve as a graphical diagnostic for the AFT assumption [@problem_id:4949764].

**The Weibull Model: A Special Case of Overlap**

There is one important distribution for which the AFT and PH models are equivalent: the Weibull distribution. If the error term $W$ in the AFT model follows a standard [extreme value distribution](@entry_id:174061), the resulting event time $T$ follows a Weibull distribution. The baseline hazard is $h_0(t) = k \lambda^k t^{k-1}$. Applying the AFT hazard transformation gives:

$$ h(t | \mathbf{x}) = \frac{1}{\psi(\mathbf{x})} h_0\left(\frac{t}{\psi(\mathbf{x})}\right) = \frac{1}{\psi(\mathbf{x})} k \lambda^k \left(\frac{t}{\psi(\mathbf{x})}\right)^{k-1} = \left( k \lambda^k t^{k-1} \right) \psi(\mathbf{x})^{-k} = h_0(t) \cdot \exp(-k \mathbf{x}^{\top}\beta) $$

This shows that the [hazard function](@entry_id:177479) is proportional to the baseline hazard, with a constant hazard ratio of $\exp(-k \mathbf{x}^{\top}\beta)$. Thus, a Weibull AFT model is also a PH model. The exponential model is a further special case where the Weibull [shape parameter](@entry_id:141062) is 1 [@problem_id:5228296].

### Common Parametric AFT Models

The choice of distribution for the error term $\varepsilon$ in the log-linear model $\log T = \mathbf{x}^{\top}\beta + \sigma \varepsilon$ determines the specific parametric family for the event time $T$. Three common choices lead to the log-normal, Weibull, and log-logistic models [@problem_id:4949771].

*   **Log-Normal AFT Model:** If $\varepsilon$ follows a [standard normal distribution](@entry_id:184509), $\varepsilon \sim N(0, 1)$, then $\log T$ is normally distributed with mean $\mu(\mathbf{x}) = \mathbf{x}^{\top}\beta$ and standard deviation $\sigma$. By definition, $T$ follows a **[log-normal distribution](@entry_id:139089)**.
    *   PDF: $f(t | \mathbf{x}) = \frac{1}{t\sigma\sqrt{2\pi}} \exp\left\{-\frac{(\ln t - \mu(\mathbf{x}))^{2}}{2\sigma^{2}}\right\}$
    *   Survival Function: $S(t | \mathbf{x}) = 1 - \Phi\left(\frac{\ln t - \mu(\mathbf{x})}{\sigma}\right)$, where $\Phi$ is the standard normal CDF.

*   **Weibull AFT Model:** If $\varepsilon$ follows a standard minimum extreme value (Gumbel) distribution, then $T$ follows a **Weibull distribution**. The AFT parameters $(\beta, \sigma)$ map to the conventional Weibull shape parameter $p$ and [scale parameter](@entry_id:268705) $\lambda(\mathbf{x})$ as follows:
    *   Shape: $p = 1/\sigma$ (constant across covariates)
    *   Scale: $\lambda(\mathbf{x}) = \exp(\mathbf{x}^{\top}\beta)$ (dependent on covariates)
    *   Survival Function: $S(t | \mathbf{x}) = \exp\left\{ - \left(\frac{t}{\lambda(\mathbf{x})}\right)^p \right\}$
    *   Hazard Function: $h(t | \mathbf{x}) = \frac{p}{\lambda(\mathbf{x})} \left(\frac{t}{\lambda(\mathbf{x})}\right)^{p-1}$

*   **Log-Logistic AFT Model:** If $\varepsilon$ follows a standard logistic distribution, then $T$ follows a **log-logistic distribution**. The parameters map similarly to the Weibull case:
    *   Shape: $p = 1/\sigma$ (constant across covariates)
    *   Scale: $\lambda(\mathbf{x}) = \exp(\mathbf{x}^{\top}\beta)$ (dependent on covariates)
    *   Survival Function: $S(t | \mathbf{x}) = \left[1 + \left(\frac{t}{\lambda(\mathbf{x})}\right)^p\right]^{-1}$
    *   Hazard Function: $h(t | \mathbf{x}) = \frac{p/\lambda(\mathbf{x}) (t/\lambda(\mathbf{x}))^{p-1}}{1 + (t/\lambda(\mathbf{x}))^p}$. This model features a non-monotonic (hump-shaped) hazard when $p  1$. The log-logistic AFT model, unlike the Weibull, does not satisfy the [proportional hazards assumption](@entry_id:163597). For instance, the hazard ratio for two covariate levels will depend on time, often exhibiting crossing hazards [@problem_id:4949786].

### Estimation and Core Assumptions

Parameter estimation in AFT models is typically performed via maximum likelihood. This requires constructing a [likelihood function](@entry_id:141927) that accounts for the incomplete nature of survival data.

**Likelihood for Censored and Truncated Data**

Survival data often includes various forms of censoring and truncation. The likelihood contribution of each observation depends on what information it provides about the true event time $T$. Let $S(t|\mathbf{x})$, $F(t|\mathbf{x})$, and $f(t|\mathbf{x})$ be the survival, CDF, and density functions for a model with parameters $\boldsymbol{\theta}$.

*   **Exact Event:** An event is observed at time $t$. The likelihood contribution is the density $f(t|\mathbf{x}; \boldsymbol{\theta})$.
*   **Right Censoring:** The event is known to have occurred only after time $c$. The contribution is the probability of this, $S(c|\mathbf{x}; \boldsymbol{\theta})$.
*   **Left Censoring:** The event is known to have occurred before time $c$. The contribution is $F(c|\mathbf{x}; \boldsymbol{\theta})$.
*   **Interval Censoring:** The event occurred between times $\ell$ and $r$. The contribution is $\mathbb{P}(\ell  T \le r) = F(r|\mathbf{x}; \boldsymbol{\theta}) - F(\ell|\mathbf{x}; \boldsymbol{\theta})$.

For the most common case of a study with only exact events and right-censored observations, let $Y_i$ be the observed time for subject $i$ and $\Delta_i$ be an indicator that is 1 if an event was observed and 0 if censored. The likelihood for a single observation is $[f(Y_i|\mathbf{x}_i; \boldsymbol{\theta})]^{\Delta_i} [S(Y_i|\mathbf{x}_i; \boldsymbol{\theta})]^{1-\Delta_i}$. The total log-likelihood for $n$ independent subjects is the sum of the individual log-likelihoods [@problem_id:4949766]:

$$ \ell(\boldsymbol{\theta}) = \sum_{i=1}^{n} \left[ \Delta_{i} \ln(f(Y_{i} | \mathbf{x}_{i}; \boldsymbol{\theta})) + (1-\Delta_{i}) \ln(S(Y_{i} | \mathbf{x}_{i}; \boldsymbol{\theta})) \right] $$

**Truncation** adds another layer of complexity. Truncation is a conditioning event that reflects the study's inclusion criteria. For **left truncation** (delayed entry), where subjects are only included if they are event-free at time $a$, all likelihood contributions must be conditioned on $T>a$. This is achieved by dividing each contribution by $S(a|\mathbf{x}; \boldsymbol{\theta})$. For **right truncation**, where subjects are included only if their event occurs before time $b$, contributions are divided by $F(b|\mathbf{x}; \boldsymbol{\theta})$ [@problem_id:4949750].

**The Assumption of Independent, Non-Informative Censoring**

The validity of the likelihood function described above hinges on a crucial assumption: **independent, [non-informative censoring](@entry_id:170081)**. This assumption consists of two parts [@problem_id:4949809]:

1.  **Conditional Independence:** The true event time $T$ and the censoring time $C$ are statistically independent, conditional on the covariates $\mathbf{x}$. This is written as $T \perp C | \mathbf{x}$. It means that, for individuals with the same covariate values, knowing their censoring time provides no information about their likely event time, and vice versa.

2.  **Parameter Distinctness:** The parameters $\boldsymbol{\theta}$ governing the event time distribution and any parameters $\boldsymbol{\psi}$ governing the censoring time distribution are distinct and variation-independent.

This assumption is essential because it allows the [joint likelihood](@entry_id:750952) of the observed data to be factored into a part that depends only on the event time parameters $\boldsymbol{\theta}$ and a part that depends only on the censoring parameters $\boldsymbol{\psi}$. Consequently, we can maximize the part of the likelihood related to $\boldsymbol{\theta}$ to obtain consistent estimates without needing to model or know anything about the censoring process. If this assumption were violated (a situation known as **informative censoring**), the censoring process would provide information about the event time, and ignoring it would lead to biased estimates.

A critical point for practitioners is that the assumption of independent censoring is **not empirically testable** from the observed survival data $(Y, \Delta, \mathbf{x})$ alone. For any given subject, we observe either $T$ (if $\Delta=1$) or $C$ (if $\Delta=0$), but never the pair $(T,C)$. Without observing the joint realizations, it is impossible to empirically assess their [conditional independence](@entry_id:262650). Justification for this assumption must therefore come from an understanding of the study design and the mechanisms leading to censoring. For example, censoring due to the administrative end of a study is often considered non-informative, whereas censoring due to a patient dropping out of a trial because their health is rapidly declining would be a classic case of informative censoring.