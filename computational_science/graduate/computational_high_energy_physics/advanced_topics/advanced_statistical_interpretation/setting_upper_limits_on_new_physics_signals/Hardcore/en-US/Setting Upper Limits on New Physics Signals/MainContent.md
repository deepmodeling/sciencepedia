## Introduction
The search for physics beyond the Standard Model is a cornerstone of modern particle physics. When a search for a new signal yields no definitive discovery, the critical task becomes quantifying what has been ruled out. This is achieved by setting an upper limit on the signal's strength, a process that presents a significant statistical challenge. How can scientists draw robust conclusions from complex, [high-dimensional data](@entry_id:138874), while rigorously accounting for numerous sources of experimental and theoretical uncertainty? This article provides a comprehensive guide to the statistical methods used to address this question. We will begin in "Principles and Mechanisms" by building the statistical framework from the ground up, introducing the [likelihood function](@entry_id:141927), [nuisance parameters](@entry_id:171802), the [profile likelihood ratio](@entry_id:753793), and the pivotal CLs method. Next, "Applications and Interdisciplinary Connections" will bridge theory and practice, exploring how these tools are applied in sophisticated, multi-channel physics analyses, including the crucial techniques of data combination and uncertainty correlation. Finally, "Hands-On Practices" will provide computational exercises to solidify your understanding. Our journey begins with the fundamental principles that underpin all modern limit-setting procedures.

## Principles and Mechanisms

This chapter delves into the fundamental principles and statistical mechanisms that form the bedrock of setting upper limits on new physics signals. We will construct the statistical framework piece by piece, starting from the simplest counting experiment and progressively incorporating the complexities of real-world measurements, such as [systematic uncertainties](@entry_id:755766). Our exploration will focus on the frequentist paradigm that is prevalent in high-energy physics, culminating in an examination of the [profile likelihood ratio](@entry_id:753793) and the CLs method, while also providing context by contrasting these with alternative approaches.

### The Likelihood Function for a Counting Experiment

The simplest form of a search for a new physical process involves a counting experiment. An experimentalist defines a specific "signal region"—a selection of events with particular properties where a new signal is predicted to appear—and simply counts the number of events, $n$, observed in that region after collecting a certain amount of data. The [statistical modeling](@entry_id:272466) of this count is the first crucial step.

Particle interactions are discrete, quantum-mechanical events that occur independently of one another. For a rare process, the number of events observed in a fixed interval (of time, or more relevantly, integrated luminosity) is excellently described by the **Poisson distribution**. Our model for the experiment must account for two sources of events: the hypothetical new signal, and the known Standard Model processes that can mimic the signal, collectively known as **background**.

Let us denote the expected number of background events as $b$. For the signal, we introduce a **parameter of interest**, the **signal strength** $\mu$. This is a dimensionless, non-negative parameter ($\mu \ge 0$) that scales a nominal signal prediction. We define $\mu = 1$ as the benchmark [signal hypothesis](@entry_id:137388) (e.g., the rate predicted by a specific new physics theory), $\mu = 0$ as the background-only hypothesis, and other values of $\mu$ as corresponding to a stronger or weaker signal. If the nominal expected signal yield for $\mu=1$ is $s$ (a value that absorbs factors like selection efficiency and integrated luminosity), then the expected signal yield for a given strength $\mu$ is $\mu s$.

Assuming that signal and background events are independent processes, the total expected number of events in the signal region is the sum of their individual expectations: $\lambda = \mu s + b$. Since the number of signal events and background events are each described by independent Poisson distributions, a fundamental property of the Poisson distribution dictates that their sum is also a Poisson-distributed random variable. Therefore, the total number of observed events, $n$, follows a Poisson distribution with mean $\mu s + b$.

From this, we can write the **likelihood function**, $L(\mu)$. The likelihood is the probability of observing the specific data, $n$, as a function of the model parameters. For our simple counting experiment, this is given by the Poisson probability [mass function](@entry_id:158970):

$L(\mu) = P(n | \mu, s, b) = \frac{(\mu s + b)^{n} e^{-(\mu s + b)}}{n!}$

This type of likelihood, where the total number of events is itself a Poisson variate, is often called an **extended likelihood**. This function is the statistical foundation upon which all subsequent inference is built. It quantifies how well different hypotheses for the signal strength $\mu$ accord with the observed data $n$ .

### Incorporating Systematic Uncertainties via Nuisance Parameters

In a real experiment, parameters such as the background yield $b$ or the signal efficiency encapsulated in $s$ are not known perfectly. They are estimates that carry their own uncertainties, often called **[systematic uncertainties](@entry_id:755766)**. To create a more realistic model, we must incorporate these uncertainties. This is achieved by promoting such parameters from fixed numbers to **[nuisance parameters](@entry_id:171802)**, typically denoted by a set of parameters $\theta$.

For instance, if the background normalization is uncertain, we might model the expected background as $\theta_b b_{0}$, where $b_{0}$ is a nominal estimate and $\theta_b$ is a [nuisance parameter](@entry_id:752755) whose value is expected to be close to $1$. The expected number of events becomes $\lambda(\mu, \theta_b) = \mu s + \theta_b b_0$.

To constrain the possible values of a [nuisance parameter](@entry_id:752755), we use information from other measurements. These **auxiliary measurements**, often made in "control regions" where the signal is expected to be negligible, provide data that helps determine the value of $\theta$. A common and powerful way to model the result of an auxiliary measurement is to treat it as providing a Gaussian constraint on the [nuisance parameter](@entry_id:752755).

Let's consider a [nuisance parameter](@entry_id:752755) $\theta$ with a nominal value of $\theta_0$ and an uncertainty of $\sigma$, derived from an auxiliary measurement. The information from this measurement can be encoded as a Gaussian term in the total likelihood function. Because the main measurement (in the signal region) and the auxiliary measurement are independent, the **joint [likelihood function](@entry_id:141927)** is the product of the individual likelihoods:

$L(\mu, \theta) = L_{\text{main}}(n | \mu, \theta) \times L_{\text{aux}}(\theta_0 | \theta)$

For our example, this would be:

$L(\mu, \theta) = \underbrace{\text{Poisson}(n | \mu s + \theta b_0)}_{\text{Main Measurement}} \times \underbrace{\mathcal{N}(\theta_0 | \theta, \sigma^2)}_{\text{Auxiliary Constraint}}$

where $\mathcal{N}(\theta_0 | \theta, \sigma^2)$ is the probability density for observing the auxiliary data (summarized by $\theta_0$) given the parameter $\theta$. Often, it is more convenient to work with the natural logarithm of the likelihood, the **log-likelihood**, $l(\mu, \theta) = \ln L(\mu, \theta)$. In this form, the joint log-likelihood is a sum:

$l(\mu, \theta) = \left[ n \ln(\mu s + \theta b_0) - (\mu s + \theta b_0) \right] - \frac{(\theta_0 - \theta)^2}{2\sigma^2} + \text{constants}$

The Gaussian constraint from the auxiliary measurement manifests as a quadratic **penalty term** in the log-likelihood. This term penalizes choices of $\theta$ that stray far from the value $\theta_0$ measured in the control region, with the strength of the penalty governed by the uncertainty $\sigma$ .

### Handling Nuisance Parameters: Profiling and the Variance-Bias Trade-off

With a multi-parameter likelihood $L(\mu, \theta)$, our goal remains to make an inference on the parameter of interest, $\mu$. In the frequentist framework, the standard method for eliminating the dependence on [nuisance parameters](@entry_id:171802) is **profiling**.

The idea of profiling is to construct a function that depends only on $\mu$ by replacing $\theta$ with its most plausible value for each given $\mu$. For any fixed value of $\mu$, we find the value of $\theta$ that maximizes the [likelihood function](@entry_id:141927). This value is the **conditional maximum likelihood estimate (MLE)** of $\theta$, denoted $\hat{\hat{\theta}}(\mu)$.

$\hat{\hat{\theta}}(\mu) = \underset{\theta}{\operatorname{arg\,max}} \, L(\mu, \theta)$

By substituting this conditional MLE back into the likelihood, we obtain the **profile likelihood function**, $L_p(\mu)$:

$L_p(\mu) = L(\mu, \hat{\hat{\theta}}(\mu))$

This function of a single variable, $\mu$, inherits the information about $\theta$ through the profiling process and can be used to construct test statistics .

The process of profiling mediates a subtle but crucial **variance-bias trade-off**. This is best understood by considering the impact of the uncertainty $\sigma$ on our [nuisance parameter](@entry_id:752755) constraint . Suppose the true, unknown value of the [nuisance parameter](@entry_id:752755) is $\theta^{\star}$.

-   If the constraint is very tight ($\sigma \to 0$), the [nuisance parameter](@entry_id:752755) $\theta$ is effectively fixed to its measured value, $\theta_0$. This removes a source of uncertainty from the model, reducing the statistical variance of any estimate of $\mu$. However, if the auxiliary measurement was biased (i.e., $\theta_0 \ne \theta^{\star}$), we are forcing the model to adopt an incorrect background value. This introduces a systematic **bias** into our estimate of $\mu$.

-   If the constraint is very loose ($\sigma \to \infty$), the auxiliary measurement provides no information. The data from the signal region alone must constrain both $\mu$ and $\theta$. This often leads to a large degeneracy and a high **variance** for the estimate of $\mu$. However, since the model is flexible, the bias from a potentially incorrect auxiliary measurement is removed.

This illustrates a general principle: tightening constraints on [nuisance parameters](@entry_id:171802) reduces statistical variance but increases the risk of bias if the constraints are misspecified. This trade-off is a central challenge in experimental physics. It is also important to contrast profiling with the Bayesian approach of **[marginalization](@entry_id:264637)**, which involves integrating the likelihood over the [nuisance parameter](@entry_id:752755) $\theta$, weighted by a prior distribution. The two methods can yield different results, especially in low-statistics regimes or near physical boundaries where asymptotic approximations fail, but they often converge in the large-sample limit where the [likelihood function](@entry_id:141927) becomes approximately Gaussian .

### Hypothesis Testing with the Profile Likelihood Ratio

To decide whether a given [signal hypothesis](@entry_id:137388) $\mu$ is compatible with the data, we perform a [hypothesis test](@entry_id:635299). The [most powerful test](@entry_id:169322) statistic is generally formed from a **[likelihood ratio](@entry_id:170863)**, which compares the plausibility of the data under a specific null hypothesis against a chosen alternative.

For testing a specific signal strength $\mu$, we use the **[profile likelihood ratio](@entry_id:753793)**, $\lambda(\mu)$:

$\lambda(\mu) = \frac{L(\mu, \hat{\hat{\theta}}(\mu))}{L(\hat{\mu}, \hat{\theta})}$

The numerator is the [profile likelihood](@entry_id:269700) evaluated at $\mu$—the best possible fit to the data under the constraint that the signal strength is $\mu$. The denominator is the likelihood evaluated at its [global maximum](@entry_id:174153), $(\hat{\mu}, \hat{\theta})$, which represents the best possible fit to the data, period. By construction, $0 \le \lambda(\mu) \le 1$. A value of $\lambda(\mu)$ close to $1$ means the data are nearly as plausible under the hypothesized $\mu$ as they are under the best-fit scenario, while a value close to $0$ indicates a poor fit.

For statistical convenience, we work with the [test statistic](@entry_id:167372) $t_\mu = -2 \ln \lambda(\mu)$. Since $\lambda(\mu) \le 1$, we have $t_\mu \ge 0$. A larger value of $t_\mu$ signifies a greater disagreement between the data and the hypothesis $\mu$. A key result, **Wilks' theorem**, states that in the large-sample limit, the distribution of $t_\mu$ follows a chi-square ($\chi^2$) distribution with a number of degrees of freedom equal to the number of parameters of interest being fixed (in this case, one).

However, the specific question we are asking—discovery or exclusion—requires a refinement of this [test statistic](@entry_id:167372).

-   **For Discovery:** We test the background-only hypothesis, $\mu = 0$. We are only interested in an *excess* of events, corresponding to a best-fit signal strength $\hat{\mu} > 0$. A deficit of events ($\hat{\mu}  0$) is not evidence for a signal. Thus, we use a [one-sided test](@entry_id:170263) statistic, $q_0$, which is zero for downward fluctuations:
    $q_0 = \begin{cases} -2 \ln \lambda(0)  \text{if } \hat{\mu} \ge 0 \\ 0  \text{if } \hat{\mu}  0 \end{cases}$

-   **For Setting an Upper Limit:** We test a hypothesis of a signal with strength $\mu > 0$. We wish to exclude this hypothesis if the data are *less* signal-like than predicted, i.e., if the best-fit signal strength $\hat{\mu}$ is less than the tested value $\mu$. An upward fluctuation where $\hat{\mu} > \mu$ does not provide evidence against the hypothesis $\mu$. Therefore, we use a different [one-sided test](@entry_id:170263) statistic, conventionally denoted $\tilde{q}_\mu$ or $q_\mu$:
    $q_\mu = \begin{cases} -2 \ln \lambda(\mu)  \text{if } 0 \le \hat{\mu} \le \mu \\ 0  \text{if } \hat{\mu} > \mu \end{cases}$

These one-sided statistics are essential for asking the correct physical questions . The presence of a physical boundary ($\mu \ge 0$) modifies the [asymptotic distribution](@entry_id:272575). Instead of a simple $\chi^2_1$ distribution, the [sampling distribution](@entry_id:276447) of these one-sided statistics is a 50/50 mixture of a delta function at zero and a $\chi^2_1$ distribution, a result of Chernoff's theorem .

### From Test Statistics to Upper Limits: The CLs Method

With a test statistic $q_\mu$ and its distribution, we can calculate a **[p-value](@entry_id:136498)**. The p-value is the probability, assuming a hypothesis $\mu$ is true, of observing data at least as incompatible with that hypothesis as what was actually seen. For our limit-setting statistic $q_\mu$, where larger values mean greater incompatibility, the [p-value](@entry_id:136498) is a right-[tail probability](@entry_id:266795):

$p_\mu = P(q_\mu \ge q_{\mu, \text{obs}} | \text{hypothesis } \mu \text{ is true})$

This quantity is often denoted as $CL_{s+b}$ (Confidence Level for [signal-plus-background](@entry_id:754818)). A naive frequentist procedure would exclude the [signal hypothesis](@entry_id:137388) $\mu$ if $p_\mu$ falls below a predefined threshold, $\alpha$ (e.g., $\alpha = 0.05$ for a $95\%$ [confidence level](@entry_id:168001) exclusion).

However, this naive approach suffers from a critical flaw: **spurious exclusion**. In a low-sensitivity search, a downward fluctuation of the background can make the observed event count very low. This low count would be highly incompatible with a [signal-plus-background](@entry_id:754818) hypothesis, leading to a small $p_\mu$ and an exclusion, even if the experiment had no real power to detect that signal in the first place. Excluding a signal you cannot see is not a robust scientific conclusion.

To solve this, the high-energy physics community widely adopted the **CLs method**. This method modifies the exclusion criterion to protect against this issue. It introduces another quantity, $CL_b$, which is the p-value calculated under the background-only ($\mu=0$) hypothesis:

$CL_b = P(q_\mu \ge q_{\mu, \text{obs}} | \text{hypothesis } \mu=0 \text{ is true})$

$CL_b$ quantifies how likely it is for the background alone to produce an observation as or more extreme than what was seen. If $CL_b$ is also small, it signals that the observation lies in a region of low probability for *both* signal+background and background-only hypotheses (i.e., a background fluctuation).

The CLs method defines a new test criterion, $CL_s$, as the ratio of these two p-values :

$CL_s = \frac{CL_{s+b}}{CL_b}$

The exclusion rule is then to reject the hypothesis $\mu$ if $CL_s \le \alpha$.

Let's consider an example. Suppose we test a [signal hypothesis](@entry_id:137388) $s=2.0$ with an expected background $b=3.0$, and we observe $n_{\text{obs}}=1$. This observation is far below the signal+background expectation of $5.0$. The probability of observing 1 event or fewer, $CL_{s+b}$, might be very small, say $0.04$. Naively, since $0.04  0.05$, we would exclude the signal. However, the observation is also somewhat unlikely for the background-only expectation of $3.0$; let's say the probability for the background to fluctuate this low, $CL_b$, is $0.20$. The $CL_s$ value is then $0.04 / 0.20 = 0.20$. Since $0.20 > 0.05$, the signal is *not* excluded. The CLs method correctly identifies that the evidence against the signal is weak because the observation is also fairly unusual for the background itself .

By dividing by $CL_b$, the procedure becomes more conservative. Since $CL_b \le 1$, we always have $CL_s \ge CL_{s+b}$, making exclusion harder. In high-sensitivity regimes, where the data incompatible with signal are not unusual for the background, $CL_b \to 1$ and thus $CL_s \to CL_{s+b}$, restoring the full [statistical power](@entry_id:197129) of the test .

### Alternative and Foundational Approaches: A Broader Context

While the [profile likelihood](@entry_id:269700) and CLs method are the modern workhorses, it is instructive to understand their context.

One foundational frequentist technique is the **Neyman confidence belt construction**, famously refined in the **Feldman-Cousins (FC) unified approach**. This method builds an "acceptance region" for each possible true value of $\mu$ by including the observational outcomes that are "most likely" under that hypothesis. The ranking of outcomes is not based on their value, but on the [likelihood ratio](@entry_id:170863) $R(n; \mu) = L(n|\mu) / L(n|\hat{\mu}(n))$, where $\hat{\mu}(n) = \max(0, n-b)$ is the best-fit physical signal for observation $n$ . The confidence interval for an observed $n_{\text{obs}}$ is then the set of all $\mu$ values whose acceptance regions contain $n_{\text{obs}}$.

A key feature of the FC method is that the likelihood-ratio ordering guarantees the resulting [confidence interval](@entry_id:138194) always includes the best-fit physical parameter value, thus ensuring the interval is never empty. Furthermore, it naturally transitions from a two-sided interval for a significant signal discovery to a one-sided upper limit for an observation consistent with background, solving the "flip-flopping" problem of older methods .

Finally, it is crucial to recognize the philosophical distinction between frequentist profiling and Bayesian **[marginalization](@entry_id:264637)** for handling [nuisance parameters](@entry_id:171802). Profiling replaces a [nuisance parameter](@entry_id:752755) with its conditional best-fit value, while [marginalization](@entry_id:264637) averages over all possible values, weighted by a prior probability distribution. While both methods often yield numerically similar results in the large-sample, asymptotic limit where likelihoods become Gaussian, their results can differ substantially in the challenging real-world scenarios of low event counts and proximity to physical boundaries. In these regimes, the assumptions underlying asymptotic theorems fail, and the choice of statistical framework and priors can have a material impact on the final scientific conclusion . A deep understanding of these principles is therefore not just an academic exercise, but a prerequisite for the rigorous interpretation of experimental data at the frontiers of science.