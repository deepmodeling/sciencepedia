## Introduction
Estimating the causal effect of treatments or exposures from observational data is a fundamental challenge in bioinformatics and medical research. Unlike in randomized controlled trials, non-random treatment assignment often leads to confounding, where systematic differences between treatment and control groups can severely bias effect estimates. Propensity score methods offer a powerful and widely-used framework to address this challenge, allowing researchers to adjust for a large number of [confounding variables](@entry_id:199777) and emulate the conditions of a randomized experiment. However, applying these methods correctly requires a deep understanding of their underlying causal theory, practical implementation details, and inherent limitations.

This article provides a structured guide to mastering propensity score methods. The first chapter, **"Principles and Mechanisms"**, lays the theoretical groundwork, starting from the fundamental problem of causal inference and the key assumptions required to identify causal effects. The second chapter, **"Applications and Interdisciplinary Connections"**, demonstrates how these principles are translated into practice through methods like matching, weighting, and stratification, and explores advanced extensions for complex data structures found in genomics and longitudinal studies. Finally, the **"Hands-On Practices"** chapter offers practical exercises to build intuition and solidify your understanding of key concepts. We begin by delving into the core principles that motivate and govern the use of propensity scores in causal analysis.

## Principles and Mechanisms

The estimation of causal effects from observational data is a central challenge in biomedical research and data analytics. Unlike in randomized controlled trials, treatment assignment in observational studies is not controlled by the investigator and is often influenced by patient characteristics. This non-random assignment can lead to systematic differences between treated and control groups, a phenomenon known as confounding, which can severely bias naive estimates of a treatment's effect. Propensity score methods provide a powerful and flexible framework for addressing this challenge by allowing researchers to adjust for a large number of covariates to reduce or eliminate [confounding bias](@entry_id:635723). This chapter delineates the foundational principles of causal inference that motivate [propensity score](@entry_id:635864) methods and explains the mechanisms through which these methods operate.

### The Fundamental Problem of Causal Inference

The modern framework for causal inference is built upon the concept of **potential outcomes**. For a binary treatment $T$, where $T=1$ indicates receiving the treatment and $T=0$ indicates receiving the control, we posit that each individual $i$ has two potential outcomes: $Y_i(1)$, the outcome that would have been observed had the individual received the treatment, and $Y_i(0)$, the outcome that would have been observed had the individual received the control. The individual-level causal effect is the difference between these two potential outcomes, $Y_i(1) - Y_i(0)$.

However, we can never observe both potential outcomes for the same individual at the same time. We only observe the outcome corresponding to the treatment that was actually received. This is often expressed as $Y_i = T_i Y_i(1) + (1-T_i)Y_i(0)$. The unobserved outcome is called the **counterfactual**. This "[missing data](@entry_id:271026)" problem is the **fundamental problem of causal inference** [@problem_id:4599527]. Because we cannot directly measure individual-level causal effects, we shift our focus to population-level average causal effects, such as the **Average Treatment Effect (ATE)**, defined as $\text{ATE} = \mathbb{E}[Y(1) - Y(0)]$.

A naive comparison of mean outcomes between the treated and control groups in an observational study, $\mathbb{E}[Y | T=1] - \mathbb{E}[Y | T=0]$, generally does not estimate the ATE. The reason is **selection bias**. For example, $\mathbb{E}[Y | T=1] = \mathbb{E}[Y(1) | T=1]$, which is the average outcome under treatment for those who actually chose the treatment. This is not necessarily equal to $\mathbb{E}[Y(1)]$, the average outcome if the *entire population* had been treated. The groups receiving $T=1$ and $T=0$ may differ systematically in ways that are related to the outcome, and it is this difference that biases the naive comparison.

### Conditions for Identification of Causal Effects

To overcome the fundamental problem of causal inference and connect the unobservable potential outcomes to the observed data, we must rely on a set of critical, untestable assumptions. These assumptions, when met, allow for the **identification** of causal effects from observational data.

#### The Stable Unit Treatment Value Assumption (SUTVA)

SUTVA is a foundational assumption that posits a well-behaved relationship between treatments and outcomes. It has two components [@problem_id:5221120]:
1.  **Consistency**: The observed outcome for an individual is their potential outcome corresponding to the treatment they actually received. This is the link $Y_i = Y_i(T_i)$ we used earlier. It also implicitly assumes there are no hidden or different versions of the treatment; for example, "immunotherapy" is administered in a consistent manner for everyone assigned $T=1$.
2.  **No Interference**: The potential outcomes for any individual do not depend on the treatment assignments of other individuals. This allows us to write an individual's potential outcome as $Y_i(t)$, depending only on their own treatment $t$, rather than on the entire vector of treatments assigned to the population.

#### Unconfoundedness

Also known as **conditional exchangeability** or **ignorability**, unconfoundedness is the central assumption for controlling confounding. It states that, conditional on a set of pre-treatment covariates $X$, the mechanism for assigning treatment is independent of the potential outcomes. Formally, this is written as:

$$
(Y(1), Y(0)) \perp T \mid X
$$

Conceptually, this means that within any stratum defined by the covariates $X=x$, the treatment assignment is "as-if randomized" [@problem_id:4599459]. It implies that the set of measured covariates $X$ is sufficiently rich to include all **confounders**—variables that are common causes of both treatment assignment and the outcome. If unconfoundedness holds, the treated and control groups are considered exchangeable within levels of $X$. For example, for patients with the same clinical profile $X=x$, their potential outcomes are, on average, the same regardless of whether they happened to receive the treatment or the control. Crucially, unconfoundedness is an assumption that cannot be verified from the data, as it involves the unobserved counterfactual outcomes [@problem_id:4599459].

A powerful way to reason about confounding and the sufficiency of a covariate set $X$ is through **Directed Acyclic Graphs (DAGs)**. In this framework, unconfoundedness is achieved if the set $X$ is sufficient to block all non-causal "backdoor" paths between the treatment $A$ and the outcome $Y$. A backdoor path is a path starting with an arrow into $A$. For instance, in a simple DAG where a measured covariate $L$ causes both treatment and outcome ($A \leftarrow L \rightarrow Y$), adjusting for $L$ blocks this backdoor path and removes the confounding. In a more complex scenario, such as $A \leftarrow U \to X \to Y$ where $U$ is unmeasured, adjusting for the measured variable $X$ is sufficient to block this path and control for confounding by $U$ [@problem_id:4943138].

#### Positivity

The **positivity** assumption, also called **overlap**, requires that for every set of covariate values $x$ present in the population, there is a non-zero probability of receiving either treatment level. Formally:

$$
0  \mathbb{P}(T=1 \mid X=x)  1 \quad \text{for all } x \text{ with } \mathbb{P}(X=x) > 0
$$

This assumption ensures that for any type of subject, a comparison group exists. If for a certain subgroup of patients (e.g., those with a severe contraindication), the probability of receiving treatment is zero, we have no empirical information about what their outcome would have been under treatment.

The necessity of positivity for identification can be rigorously shown from two perspectives [@problem_id:4830839]. First, under unconfoundedness, the ATE is identified via the **g-formula**: $\text{ATE} = \mathbb{E}_X[\mathbb{E}[Y \mid T=1, X]] - \mathbb{E}_X[\mathbb{E}[Y \mid T=0, X]]$. If positivity is violated, for example $\mathbb{P}(T=1 \mid X=x) = 0$ for some $x$, then the conditional expectation $\mathbb{E}[Y \mid T=1, X=x]$ is undefined because there are no observations in that stratum. The integrand is thus unidentified, and the ATE cannot be computed. Second, from an inverse probability weighting perspective, the identity $E[Y(a)] = \mathbb{E}\left[\frac{\mathbb{I}\{T=a\}Y}{\mathbb{P}(T=a \mid X)}\right]$ involves dividing by the probability of treatment. If this probability is zero for some subjects, the weight is infinite and the identity breaks down.

### The Propensity Score: A Unidimensional Summary for Confounding Control

When the covariate vector $X$ is high-dimensional, as is common in medical genomics with thousands of features [@problem_id:4599527], directly conditioning on $X$ through methods like stratification or matching becomes infeasible (the "[curse of dimensionality](@entry_id:143920)"). The **[propensity score](@entry_id:635864)**, defined as the conditional probability of receiving treatment given the pre-treatment covariates, provides an elegant solution to this problem.

$$
e(X) = \mathbb{P}(T=1 \mid X)
$$

The [propensity score](@entry_id:635864) is a **balancing score**, a property with two profound consequences for causal inference.

#### Propensity Score Estimation

In practice, the true propensity score is unknown and must be estimated from the data. This is typically done by fitting a [probabilistic classification](@entry_id:637254) model to predict the treatment assignment $T$ from the covariates $X$. The most common choice is a **[logistic regression model](@entry_id:637047)**, where the [log-odds](@entry_id:141427) of receiving treatment is modeled as a linear function of the covariates:

$$
\ln\left(\frac{e(X)}{1 - e(X)}\right) = X^{\top}\beta
$$

Given a dataset of $n$ individuals with observed treatments $T_i$ and covariates $X_i$, the parameter vector $\beta$ is estimated by maximizing the likelihood of the observed treatment assignments. Assuming [conditional independence](@entry_id:262650) of assignments, the likelihood function for $\beta$ is the product of individual Bernoulli probabilities [@problem_id:4830874]:

$$
L(\beta) = \prod_{i=1}^{n} [e(X_i)]^{T_i} [1 - e(X_i)]^{1 - T_i} = \prod_{i=1}^{n} \frac{\exp(T_{i} X_{i}^{\top}\beta)}{1 + \exp(X_{i}^{\top}\beta)}
$$

Once $\hat{\beta}$ is obtained, the estimated propensity score for each individual, $\hat{e}(X_i)$, can be calculated.

#### Core Properties of the Propensity Score

The utility of the propensity score stems from two key theorems proven by Rosenbaum and Rubin (1983).

1.  **The Balancing Property**: The propensity score is a balancing score, meaning that conditional on the propensity score, the treatment assignment $T$ is independent of the covariates $X$. Formally, $T \perp X \mid e(X)$. This implies that within strata of individuals who have the same [propensity score](@entry_id:635864), the distribution of the full, high-dimensional covariate vector $X$ will be the same between the treated and control groups. Geometrically, the [level sets](@entry_id:151155) of the propensity score function, $L_c = \{x : e(x) = c\}$, are surfaces in the covariate space. The balancing property guarantees that if we sample treated and control subjects from any such surface $L_c$, their covariate distributions will be identical [@problem_id:4599517].

2.  **Unconfoundedness via the Propensity Score**: If treatment assignment is unconfounded given the full set of covariates $X$, then it is also unconfounded given the scalar [propensity score](@entry_id:635864) $e(X)$. That is, if $(Y(1), Y(0)) \perp T \mid X$, then it follows that $(Y(1), Y(0)) \perp T \mid e(X)$ [@problem_id:4599459].

Together, these properties are transformative. They justify replacing conditioning on the high-dimensional vector $X$ with conditioning on the one-dimensional propensity score $e(X)$ to remove [confounding bias](@entry_id:635723), without loss of information for identification. This makes adjustment feasible through methods like matching, stratification, or weighting based on the estimated [propensity score](@entry_id:635864).

### Practical Guidance on Covariate Selection

The validity of a propensity score analysis hinges critically on the choice of covariates $X$ used to build the model. The goal is to select a set of covariates that, as closely as possible, satisfies the unconfoundedness assumption without inducing further bias. Causal DAGs are an invaluable tool for guiding this selection [@problem_id:4599512] [@problem_id:4943073].

#### Variables to Include

1.  **Confounders**: The set $X$ must include all measured pre-treatment variables that are common causes of both treatment and outcome. These are the classic confounders. Omitting a confounder from the propensity score model will leave a backdoor path open, resulting in residual confounding and a biased effect estimate.

2.  **Prognostic Variables**: It is highly advisable to include pre-treatment variables that are strong predictors of the outcome, even if they are not associated with treatment assignment [@problem_id:4599512]. While these variables are not confounders, including them in the [propensity score](@entry_id:635864) model can significantly increase the precision (reduce the variance) of the estimated treatment effect. By explaining variation in the outcome, they reduce the residual error in the final effect estimate.

#### Variables to Exclude

1.  **Colliders**: It is imperative to **exclude** any variable that is a **[collider](@entry_id:192770)** on a path between treatment and outcome. A collider is a variable that is a common *effect* of two other variables. Consider a path structure like $T \to K \leftarrow U \to Y$, where $U$ is an unmeasured cause of the outcome $Y$. The variable $K$ is a collider. Without conditioning on $K$, this path is blocked, and no association flows from $T$ to $Y$ along it. However, if we condition on the [collider](@entry_id:192770) $K$ (e.g., by including it in the [propensity score](@entry_id:635864) model), we open this path, inducing a spurious association between $T$ and the unmeasured factor $U$. This, in turn, creates a non-causal association between $T$ and $Y$, violating unconfoundedness and introducing **collider-stratification bias** [@problem_id:4599512] [@problem_id:4943073]. This is a pernicious form of bias because it is actively created by the analytical choice to adjust for the wrong variable. A common mistake is to adjust for post-treatment variables that may be affected by both the treatment and other causes of the outcome.

2.  **Instrumental Variables (with caution)**: An [instrumental variable](@entry_id:137851) is a variable that is a strong cause of treatment but has no causal pathway to the outcome except through the treatment. Including a strong instrument in the [propensity score](@entry_id:635864) model does not, in theory, introduce bias. However, it can have severe practical consequences. By strongly predicting treatment, it can push estimated propensity scores toward 0 and 1, creating a practical violation of the positivity assumption. In inverse probability weighting, this leads to extremely large weights and a highly unstable, high-variance effect estimate [@problem_id:4599512]. While they do not introduce bias, their inclusion can be detrimental to the performance of some estimators.

### Propensity Score Methods and Their Target Estimands

Once propensity scores are estimated, several methods can be used to estimate a causal effect. It is crucial to recognize that different methods may target different causal estimands [@problem_id:4830861].

#### Causal Estimands: ATE, ATT, and ATC

-   **Average Treatment Effect (ATE)**: $\mathbb{E}[Y(1) - Y(0)]$. This is the average effect of the treatment on the entire population of interest. It answers the question: "What would be the effect, on average, if everyone in the population were treated versus if everyone were not treated?"

-   **Average Treatment Effect on the Treated (ATT)**: $\mathbb{E}[Y(1) - Y(0) \mid T=1]$. This is the average effect of the treatment specifically for those individuals who, in reality, received the treatment. It answers the question: "What was the effect of the treatment for the patients who actually received it?"

-   **Average Treatment Effect on the Controls (ATC)**: $\mathbb{E}[Y(1) - Y(0) \mid T=0]$. This is the average effect of the treatment specifically for those who did not receive it. It answers the question: "What would have been the effect of the treatment had it been given to the patients who, in reality, did not receive it?"

The choice of estimand depends on the research question. For policy decisions about a population-wide intervention, the ATE is often most relevant. For evaluating the benefit of a therapy for the types of patients who are currently receiving it, the ATT may be more appropriate.

#### Matching Methods to Estimands

-   **Inverse Probability of Treatment Weighting (IPTW) for ATE**: The standard IPTW method assigns weights of $w_i = 1/\hat{e}(X_i)$ to treated subjects and $w_i = 1/(1-\hat{e}(X_i))$ to control subjects. This weighting scheme creates a pseudo-population in which the covariate distributions are balanced and mimic the distribution of the original full population. Therefore, this method targets the **ATE**.

-   **Propensity Score Matching for ATT**: A common matching procedure involves taking each treated subject and finding one or more control subjects with the closest propensity scores. Unmatched control subjects are often discarded. This process effectively re-samples the control group to make its covariate distribution match that of the treated group. The resulting comparison therefore estimates the treatment effect within the treated population, targeting the **ATT**.

-   **Weighting for ATT and ATC**: Specific weighting schemes can be devised to target ATT or ATC. To estimate **ATT**, one can assign a weight of $1$ to treated units and a weight of $\hat{e}(X_i)/(1-\hat{e}(X_i))$ to control units. This up-weights controls who look like the treated, making the control group comparable to the treated group. To estimate **ATC**, one can assign a weight of $1$ to controls and a weight of $(1-\hat{e}(X_i))/\hat{e}(X_i)$ to treated units, which reweights the treated group to resemble the control group [@problem_id:4830861].

Understanding these principles and mechanisms is essential for the rigorous application of propensity score methods, ensuring that the chosen analytical strategy aligns with the underlying assumptions and the specific causal question being investigated.