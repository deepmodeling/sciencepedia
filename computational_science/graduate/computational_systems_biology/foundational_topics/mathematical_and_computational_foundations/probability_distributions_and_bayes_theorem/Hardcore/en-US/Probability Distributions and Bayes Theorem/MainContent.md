## Introduction
The quantitative modeling of biological systems is fundamentally a challenge of reasoning under uncertainty. From the stochastic nature of gene expression to the noise inherent in high-throughput measurements, a coherent framework is required to build models, learn from data, and make robust scientific conclusions. Probability distributions and Bayes' theorem provide precisely this framework, offering a complete and principled language for statistical inference. This article serves as a comprehensive guide for graduate students in [computational systems biology](@entry_id:747636), bridging the gap between abstract theory and practical application.

The journey is structured across three key chapters. First, in **Principles and Mechanisms**, we will establish the rigorous mathematical foundation of probability, introduce essential distributions for modeling biological data, and develop the complete workflow of Bayesian inference. Next, **Applications and Interdisciplinary Connections** will demonstrate how these principles are applied to solve real-world biological problems, from classifying cell types and inferring dynamic processes to designing optimal experiments. Finally, **Hands-On Practices** will solidify this knowledge through a series of guided exercises that tackle realistic research scenarios. We begin by exploring the core principles and mechanisms that form the bedrock of [probabilistic modeling](@entry_id:168598).

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanisms that underpin [probabilistic modeling](@entry_id:168598) and Bayesian inference in [computational systems biology](@entry_id:747636). We will begin by establishing the rigorous mathematical foundation of probability theory, then introduce key probability distributions for modeling biological data, and finally develop the complete framework of Bayesian inference, from [parameter estimation](@entry_id:139349) to [model comparison](@entry_id:266577) and predictive assessment.

### The Mathematical Foundation of Probability

While intuitive notions of probability are sufficient for simple scenarios, a rigorous and systematic approach is essential for developing complex stochastic models of biological systems. This rigor is provided by the measure-theoretic framework of probability, first axiomatized by Andrey Kolmogorov.

At the core of this framework is the **probability space**, a mathematical construct defined by the triple $(\Omega, \mathcal{F}, \mathbb{P})$.

1.  **The Sample Space, $\Omega$**: This is the set of all possible elementary and indivisible outcomes of a stochastic experiment or process. In the context of a [stochastic gene expression](@entry_id:161689) model, an outcome $\omega \in \Omega$ might represent a complete time-series trajectory of mRNA and protein numbers in a single cell.

2.  **The Event Space, $\mathcal{F}$**: This is a collection of subsets of $\Omega$, which we call **events**. For this collection to be mathematically versatile, it cannot be just any collection of subsets. It must be a **$\sigma$-algebra** (or $\sigma$-field), meaning it satisfies three properties:
    *   The entire sample space is an event: $\Omega \in \mathcal{F}$.
    *   If a set $A$ is an event, its complement $A^c = \{\omega \in \Omega \mid \omega \notin A\}$ is also an event.
    *   For any countable sequence of events $A_1, A_2, \dots$, their union $\bigcup_{i=1}^\infty A_i$ is also an event.
    These properties ensure that we can perform standard logical operations on events (like 'and', 'or', 'not') and consider limiting cases, which is crucial for advanced applications.

3.  **The Probability Measure, $\mathbb{P}$**: This is a function that assigns a probability, a real number in $[0,1]$, to every event in $\mathcal{F}$. It must satisfy the **Kolmogorov axioms**:
    *   **Non-negativity**: $\mathbb{P}(A) \ge 0$ for all $A \in \mathcal{F}$.
    *   **Normalization**: $\mathbb{P}(\Omega) = 1$.
    *   **Countable Additivity**: For any countable collection of pairwise [disjoint events](@entry_id:269279) $A_1, A_2, \dots$ (i.e., $A_i \cap A_j = \emptyset$ for $i \neq j$), the probability of their union is the sum of their probabilities: $\mathbb{P}(\bigcup_{i=1}^\infty A_i) = \sum_{i=1}^\infty \mathbb{P}(A_i)$.

While these axioms seem abstract, they provide the foundation for assigning probabilities to scientifically meaningful observations. For instance, in an experiment measuring mRNA [burst size](@entry_id:275620) in a cell, we are not directly observing the underlying microscopic state $\omega$, but rather a numerical quantity derived from it. This numerical quantity is a **random variable**. Formally, a real-valued random variable $X$ is a function that maps outcomes from the [sample space](@entry_id:270284) to the real numbers, $X: \Omega \to \mathbb{R}$.

However, not just any function will do. For the framework to be coherent, we must be able to ask questions like, "What is the probability that the mRNA count $X$ is less than or equal to some value $x$?" This corresponds to the event $\{\omega \in \Omega \mid X(\omega) \le x\}$, which is the pre-image of the interval $(-\infty, x]$ under the function $X$, denoted $X^{-1}((-\infty, x])$. For the probability of this event to be defined, the set itself must be in our [event space](@entry_id:275301) $\mathcal{F}$. This leads to the crucial requirement of **measurability** . A function $X: \Omega \to \mathbb{R}$ is a random variable only if it is a [measurable function](@entry_id:141135). This means that for any "reasonable" subset $B$ of the real line, its pre-image $X^{-1}(B)$ is an event in $\mathcal{F}$. The standard collection of such reasonable subsets of $\mathbb{R}$ is the **Borel $\sigma$-algebra**, denoted $\mathcal{B}(\mathbb{R})$, which is the smallest $\sigma$-algebra containing all [open intervals](@entry_id:157577).

In summary, a real-valued random variable is a [measurable function](@entry_id:141135) $X: (\Omega, \mathcal{F}) \to (\mathbb{R}, \mathcal{B}(\mathbb{R}))$. This ensures that events like $\{X \le x\}$ are always in $\mathcal{F}$, making the expression $\mathbb{P}(X \le x)$ well-defined. This allows us to define the **Cumulative Distribution Function (CDF)** of $X$ as $F_X(x) = \mathbb{P}(X \le x)$, the fundamental object from which all other descriptions of the variable's distribution are derived.

### Modeling Biological Data with Probability Distributions

With the formal definition of a random variable, we can now turn to specific families of probability distributions that are indispensable for modeling data in [computational systems biology](@entry_id:747636), particularly the [count data](@entry_id:270889) prevalent in sequencing experiments.

The choice of distribution is a modeling decision that encodes our assumptions about the data-generating process. We can analyze the appropriateness of these assumptions by examining properties of the distributions, such as the relationship between their mean and variance.

-   **The Bernoulli and Binomial Distributions:** The simplest case involves a [binary outcome](@entry_id:191030). For example, in a single-cell RNA sequencing (scRNA-seq) experiment, a gene may be considered either detected (1) or not detected (0). Such an outcome is modeled by a **Bernoulli random variable**, which takes value 1 with probability $p$ and 0 with probability $1-p$. Its mean is $p$ and its variance is $p(1-p)$. The [variance-to-mean ratio](@entry_id:262869) is $(1-p)$, which is always less than 1 for $p \in (0,1)$. This property is known as **[underdispersion](@entry_id:183174)**.

    If we consider a fixed number of trials, such as a fixed total number of [unique molecular identifiers](@entry_id:192673) (UMIs) captured in a cell, say $L$, the count of UMIs belonging to a specific gene $g$ can be modeled as a **Binomial random variable**. If each of the $L$ UMIs has a probability $\pi_g$ of being from gene $g$, independently of the others, then the count for that gene follows a $\text{Binomial}(L, \pi_g)$ distribution. Its mean is $L\pi_g$ and its variance is $L\pi_g(1-\pi_g)$. The [variance-to-mean ratio](@entry_id:262869) is $(1-\pi_g)$, which is again less than 1 (underdispersed) .

-   **The Poisson Distribution:** Many processes in molecular biology, such as the synthesis of a new transcript or the binding of a transcription factor to DNA, can be modeled as memoryless events occurring at a constant average rate. The number of such events occurring in a fixed interval of time or space follows a **Poisson distribution**. A random variable $Y \sim \text{Poisson}(\lambda)$ has mean $\mathbb{E}[Y] = \lambda$ and variance $\text{Var}(Y) = \lambda$. The defining characteristic of the Poisson distribution is that its **[variance-to-mean ratio](@entry_id:262869) is exactly 1**. This provides a simple diagnostic: if we observe [count data](@entry_id:270889) across many cells and the sample variance is substantially different from the [sample mean](@entry_id:169249), a simple Poisson model is likely inadequate .

-   **The Negative Binomial Distribution:** It is an empirical fact that [count data](@entry_id:270889) from scRNA-seq experiments are almost always **overdispersed**, meaning the variance is greater than the mean. This cannot be captured by a Binomial or Poisson model. This [overdispersion](@entry_id:263748) arises from both technical noise and, more importantly, genuine biological heterogeneity. For instance, gene expression is often "bursty," and cells in a population, even if genetically identical, will be in different states (e.g., cell cycle phase), leading to different underlying transcription rates.

    A powerful way to model such heterogeneity is with a hierarchical model. We can assume that the count in each cell $i$, $Y_i$, follows a Poisson distribution with its own rate, $\lambda_i$, but that the rates $\lambda_i$ themselves vary across the population according to a probability distribution. A mathematically convenient and biophysically plausible choice for the distribution of rates is the **Gamma distribution**. This leads to the **Poisson-Gamma mixture model**:
    $$ Y_i \mid \lambda_i \sim \text{Poisson}(\lambda_i) $$
    $$ \lambda_i \sim \text{Gamma}(\alpha, \beta) $$
    When we average over the distribution of the latent rates $\lambda_i$, the resulting [marginal distribution](@entry_id:264862) for the counts $Y_i$ is a **Negative Binomial (NB) distribution**. The mean of this NB distribution is $\mathbb{E}[Y_i] = \mathbb{E}[\lambda_i]$, and its variance is $\text{Var}(Y_i) = \mathbb{E}[\lambda_i] + \text{Var}(\lambda_i)$. Since the variance of the Gamma distribution is always positive, the variance of the resulting NB distribution is strictly greater than its mean. The NB distribution is therefore a natural choice for modeling overdispersed [count data](@entry_id:270889), directly accounting for [cell-to-cell variability](@entry_id:261841) .

### The Core of Bayesian Inference

The central aim of [statistical inference](@entry_id:172747) is to learn about unknown quantities, or **parameters**, of a system from observed data. Bayesian inference provides a complete and coherent framework for this task, built upon a single, elegant rule: **Bayes' theorem**.

For a set of parameters $\theta$ and observed data $y$, Bayes' theorem states:
$$ p(\theta \mid y) = \frac{p(y \mid \theta) p(\theta)}{p(y)} $$
Each term in this equation has a distinct and crucial role:

-   **Prior Distribution, $p(\theta)$**: This distribution represents our knowledge or belief about the parameters $\theta$ *before* observing the data. It is where we can incorporate information from previous experiments, physical constraints, or established biological knowledge.

-   **Likelihood, $p(y \mid \theta)$**: This is the probability (or probability density) of the observed data $y$ for a *given* value of the parameters $\theta$. It is the function that connects the unobserved parameters to the observed data through the chosen statistical model (e.g., a Poisson distribution). When viewed as a function of $\theta$ for fixed data $y$, it is called the **likelihood function**.

-   **Posterior Distribution, $p(\theta \mid y)$**: This is the result of the inference. It represents our updated knowledge or belief about the parameters $\theta$ *after* having observed the data $y$. It is a synthesis of the [prior information](@entry_id:753750) and the information contained in the data.

-   **Marginal Likelihood (or Evidence), $p(y)$**: This term is the probability of the data integrated over all possible parameter values: $p(y) = \int p(y \mid \theta) p(\theta) d\theta$. It acts as the [normalization constant](@entry_id:190182), ensuring that the posterior distribution integrates to 1. While it can be difficult to compute, it plays a vital role in [model comparison](@entry_id:266577), as we will see later.

Because the [marginal likelihood](@entry_id:191889) $p(y)$ does not depend on $\theta$, we often work with the proportional form of Bayes' theorem:
$$ p(\theta \mid y) \propto p(y \mid \theta) p(\theta) $$
This states that the posterior is proportional to the likelihood times the prior.

#### Parameter Identifiability

A critical prerequisite for successful inference is **[parameter identifiability](@entry_id:197485)**. A parameter is identifiable if it is, in principle, possible to learn its value from an infinite amount of data. Formally, in a model $\{p(y \mid \theta) : \theta \in \Theta \}$, the parameter $\theta$ is identifiable if the mapping from the parameter to the probability distribution is injective. That is, if $\theta_1 \neq \theta_2$, then there must be some data $y$ for which $p(y \mid \theta_1) \neq p(y \mid \theta_2)$. If this condition is not met, the parameter is **non-identifiable**, and no amount of data from the experiment can distinguish between the different parameter values that produce the same likelihood.

A classic example in systems biology is the simple model of gene expression as a linear [birth-death process](@entry_id:168595), with synthesis rate $k_{syn}$ and degradation rate $k_{deg}$. If our only data are snapshot measurements of mRNA counts at steady state, the data follow a Poisson distribution with mean $\mu = k_{syn} / k_{deg}$. The likelihood function depends only on this ratio. Any combination of $(k_{syn}, k_{deg})$ with the same ratio (e.g., $(k_{syn}, k_{deg})$ and $(2k_{syn}, 2k_{deg})$) will produce the exact same likelihood for any observed data. Thus, the individual parameters $k_{syn}$ and $k_{deg}$ are structurally non-identifiable from this experiment alone .

This non-identifiability can sometimes be resolved by incorporating data from a different type of experiment. For example, if we augment the snapshot data with data from a pulse-chase experiment that directly measures the mRNA [half-life](@entry_id:144843) $T_{1/2} = (\ln 2) / k_{deg}$, we can independently identify $k_{deg}$. With $k_{deg}$ known, we can then use the identified ratio $\mu = k_{syn} / k_{deg}$ to solve for $k_{syn}$. In a Bayesian context, non-identifiability often manifests as an **improper posterior** (one that cannot be normalized to integrate to 1) if an improper prior is used, or a posterior that remains highly diffuse along the non-identifiable combinations of parameters .

### Mechanisms of Bayesian Computation

The application of Bayes' theorem involves calculating the posterior distribution $p(\theta \mid y)$. In some fortunate cases, this can be done analytically. In most realistic scenarios, however, it requires [numerical approximation methods](@entry_id:169303).

#### Conjugate Priors

The simplest case for Bayesian inference occurs when the prior and likelihood are "compatible" in a way that leads to a posterior distribution in the same family as the prior. This property is called **conjugacy**. A prior distribution $p(\theta)$ is said to be conjugate to a likelihood $p(y \mid \theta)$ if the resulting posterior $p(\theta \mid y)$ is in the same distributional family as $p(\theta)$, albeit with updated parameters. This provides a closed-form, analytical solution for the posterior, avoiding the need for numerical integration.

Several conjugate pairs are fundamental in [computational systems biology](@entry_id:747636) :

-   **Beta-Binomial**: For a Binomial likelihood (modeling successes in $n$ trials), the [conjugate prior](@entry_id:176312) for the success probability $\theta$ is the Beta distribution. If the prior is $\text{Beta}(\alpha, \beta)$ and we observe $k$ successes, the posterior is $\text{Beta}(\alpha+k, \beta+n-k)$.
-   **Gamma-Poisson**: For a Poisson likelihood (modeling counts), the [conjugate prior](@entry_id:176312) for the [rate parameter](@entry_id:265473) $\lambda$ is the Gamma distribution. If the prior is $\text{Gamma}(\alpha, \beta)$ and we observe data with sum $\sum y_i$ from $n$ samples, the posterior is $\text{Gamma}(\alpha + \sum y_i, \beta + n)$ .
-   **Dirichlet-Multinomial**: For a Multinomial likelihood (modeling counts in $K$ categories), the [conjugate prior](@entry_id:176312) for the probability vector $\boldsymbol{\pi}$ is the Dirichlet distribution.
-   **Normal-Normal**: For a Normal likelihood with unknown mean $\mu$ and known variance $\sigma^2$, the [conjugate prior](@entry_id:176312) for $\mu$ is also a Normal distribution.

The underlying reason for these convenient pairings is that the likelihoods belong to the **[exponential family](@entry_id:173146)** of distributions, and their [conjugate priors](@entry_id:262304) have a corresponding mathematical form . This structure ensures that when the likelihood and prior are multiplied, the resulting functional form for the posterior matches that of the prior.

#### Markov Chain Monte Carlo (MCMC)

In many complex [systems biology](@entry_id:148549) models, the [likelihood function](@entry_id:141927) is intricate, and no [conjugate prior](@entry_id:176312) exists. In these cases, we cannot compute the posterior analytically. The dominant approach for navigating this challenge is **Markov Chain Monte Carlo (MCMC)**. MCMC methods are a class of algorithms that generate samples from a probability distribution by constructing a Markov chain whose [equilibrium distribution](@entry_id:263943) is the desired [target distribution](@entry_id:634522)—in our case, the posterior $p(\theta \mid y)$.

The **Metropolis-Hastings algorithm** is a general and powerful MCMC algorithm . It works as follows. Starting from an initial parameter value $\theta^{(t)}$:

1.  **Propose:** A new candidate value $\theta'$ is drawn from a **[proposal distribution](@entry_id:144814)** $q(\theta' \mid \theta^{(t)})$. This distribution can be chosen in many ways; a common choice is a symmetric distribution centered on the current value, such as a Normal distribution (a "random walk" proposal).

2.  **Accept/Reject:** The candidate $\theta'$ is accepted or rejected based on an **acceptance probability**, $\alpha(\theta^{(t)}, \theta')$. This probability is ingeniously constructed to ensure the chain eventually converges to the correct [posterior distribution](@entry_id:145605). A uniform random number $u \in [0,1]$ is drawn, and the move is accepted if $u \le \alpha(\theta^{(t)}, \theta')$. If accepted, the next state is $\theta^{(t+1)} = \theta'$; otherwise, the chain stays put, $\theta^{(t+1)} = \theta^{(t)}$.

The acceptance probability is derived from the requirement of **detailed balance**, which is a [sufficient condition](@entry_id:276242) for ensuring the chain's stationary distribution is the target posterior $\pi(\theta) \propto p(\theta \mid y)$. The detailed balance condition is $\pi(\theta) K(\theta' \mid \theta) = \pi(\theta') K(\theta \mid \theta')$, where $K$ is the chain's transition kernel. This leads to the Metropolis-Hastings [acceptance probability](@entry_id:138494):
$$ \alpha(\theta, \theta') = \min \left\{ 1, \frac{p(y \mid \theta') p(\theta') q(\theta \mid \theta')}{p(y \mid \theta) p(\theta) q(\theta' \mid \theta)} \right\} $$
Crucially, this ratio only depends on the likelihood and the prior. The intractable marginal likelihood $p(y)$ cancels out, making this a widely applicable method. The ratio of proposal densities, $q(\theta \mid \theta')/q(\theta' \mid \theta)$, serves as a correction factor for any asymmetry in the proposal mechanism. If the proposal is symmetric (i.e., $q(\theta' \mid \theta) = q(\theta \mid \theta')$), this ratio is 1, simplifying the algorithm to the original Metropolis algorithm.

### Using the Posterior Distribution

After obtaining the [posterior distribution](@entry_id:145605) $p(\theta \mid y)$, either analytically via conjugacy or as a set of samples from MCMC, we can use it to answer a wide range of scientific questions.

#### Point Estimation and Bayesian Decision Theory

Often, we need to report a single value as our "best guess" for a parameter. **Bayesian decision theory** provides a formal framework for choosing such a **[point estimate](@entry_id:176325)**. We define a **[loss function](@entry_id:136784)**, $L(\theta, a)$, which quantifies the penalty incurred if we choose estimate $a$ when the true parameter value is $\theta$. The optimal estimate is the one that minimizes the expected loss under the posterior distribution.

The choice of [loss function](@entry_id:136784) determines the [optimal estimator](@entry_id:176428) :

-   **Squared Error Loss**: $L(\theta, a) = (\theta - a)^2$. This heavily penalizes large errors. The estimator that minimizes the posterior expected squared error is the **[posterior mean](@entry_id:173826)**, $\mathbb{E}[\theta \mid y] = \int \theta p(\theta \mid y) d\theta$.

-   **Absolute Error Loss**: $L(\theta, a) = |\theta - a|$. This penalizes all errors in proportion to their magnitude. The [optimal estimator](@entry_id:176428) is the **[posterior median](@entry_id:174652)**, the value $a$ such that $\mathbb{P}(\theta \le a \mid y) = 0.5$.

-   **Zero-One Loss**: $L(\theta, a) = \mathbb{1}\{\theta \neq a\}$ (for discrete $\theta$) or its continuous analogue, $L_{\epsilon}(\theta, a) = \mathbb{1}\{|\theta - a| > \epsilon\}$. This loss simply asks if our estimate is correct or not. The estimator that minimizes this loss is the **Maximum a Posteriori (MAP)** estimate, $\hat{\theta}_{\text{MAP}} = \arg\max_{\theta} p(\theta \mid y)$. The MAP estimate represents the mode, or the most probable value, of the parameter under the [posterior distribution](@entry_id:145605).

#### Prediction and Model Checking

Beyond estimating parameters, a key strength of the Bayesian framework is its ability to make predictions and to assess its own adequacy. This is accomplished through the **[posterior predictive distribution](@entry_id:167931)**. For a new, unobserved data point $y^*$, its distribution, given the observed data $y$, is:
$$ p(y^* \mid y) = \int p(y^* \mid \theta) p(\theta \mid y) d\theta $$
This distribution represents our prediction for a new observation. It is obtained by averaging the predictions made by the likelihood ($p(y^* \mid \theta)$) over all possible values of the parameters, weighted by their posterior probabilities ($p(\theta \mid y)$). This process naturally accounts for our uncertainty in the parameter values. The variance of this predictive distribution, for example, is the sum of the expected sampling variance and the variance due to [parameter uncertainty](@entry_id:753163): $\text{Var}(Y^* \mid y) = \mathbb{E}[\text{Var}(Y^* \mid \theta)] + \text{Var}[\mathbb{E}(Y^* \mid \theta)]$ .

The [posterior predictive distribution](@entry_id:167931) is the cornerstone of **posterior predictive checking**, a method for assessing **model fit**. The logic is simple: if our model is a good representation of the data-generating process, then new data generated from the model should look similar to the data we have actually observed. We can formalize this by simulating replicate datasets $y^{\text{rep}}$ from the [posterior predictive distribution](@entry_id:167931) and comparing them to the observed data $y$, often via a test statistic or discrepancy measure $T(\cdot)$ that captures a scientifically relevant feature of the data. A large discrepancy between $T(y)$ and the distribution of $T(y^{\text{rep}})$ suggests that the model is failing to capture that particular aspect of the data, signaling a potential model misfit .

#### Model Comparison

Often, we have competing scientific hypotheses that can be formulated as different statistical models. For instance, is a particular signaling pathway active or inactive? We can represent these as two models, $\mathcal{M}_1$ and $\mathcal{M}_0$. Bayesian inference provides a direct and principled way to compare them using the **Bayes Factor**.

The Bayes Factor for comparing $\mathcal{M}_1$ to $\mathcal{M}_0$ is the ratio of their marginal likelihoods:
$$ \text{BF}_{10} = \frac{p(y \mid \mathcal{M}_1)}{p(y \mid \mathcal{M}_0)} $$
Recall that the marginal likelihood, $p(y \mid \mathcal{M}) = \int p(y \mid \theta, \mathcal{M}) p(\theta \mid \mathcal{M}) d\theta$, is the probability of the observed data under model $\mathcal{M}$, averaged over the prior for its parameters. The Bayes factor thus quantifies how much the data have shifted our relative belief between the two models. A $\text{BF}_{10} > 1$ indicates that the data are more probable under $\mathcal{M}_1$ than $\mathcal{M}_0$, lending support to $\mathcal{M}_1$.

A remarkable property of the Bayes factor is that it automatically implements a form of **Ockham's razor**, penalizing overly complex models. A model with many parameters (high flexibility) can fit a wide range of potential datasets. However, by spreading its prior predictions so broadly, it assigns a relatively low probability to any *specific* dataset, including the one we observed. A simpler model that makes more focused predictions will be rewarded with a higher [marginal likelihood](@entry_id:191889) if those predictions turn out to be correct .

#### Hierarchical Models and Information Pooling

Finally, the principles of Bayesian inference can be extended to **[hierarchical models](@entry_id:274952)**, which are particularly powerful for analyzing structured data, such as data from multiple subpopulations, patients, or experimental conditions. In a hierarchical model, parameters for individual units are themselves drawn from a shared, higher-level distribution.

This structure allows for "information pooling." For example, consider a mixed cell culture with multiple subpopulations, where we want to estimate the S-phase fraction in each. We can build a separate model for each subpopulation (e.g., a Beta-Binomial model for S-phase counts), and then combine the results using the **Law of Total Probability**. If $A$ is the event that a randomly selected cell is in S-phase, and $\{B_i\}$ is the partition of cells into subpopulations, then:
$$ \mathbb{P}(A) = \sum_i \mathbb{P}(A \mid B_i) \mathbb{P}(B_i) $$
Here, $\mathbb{P}(B_i)$ is the proportion of the $i$-th subpopulation, and $\mathbb{P}(A \mid B_i)$ is the posterior predictive probability of being in S-phase for a cell drawn from that subpopulation. This provides a principled way to marginalize over the population structure to obtain an overall estimate, elegantly combining inference performed at multiple levels of a biological system .