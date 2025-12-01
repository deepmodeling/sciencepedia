## Introduction
In medical and public health research, a critical challenge lies in moving beyond mere [statistical association](@entry_id:172897) to establish true causal relationships. Simply observing that two variables are correlated is insufficient to conclude that one causes the other, as this association may be driven by confounding or other biases. This article addresses this fundamental problem by providing a rigorous framework for causal inference, equipping researchers with the tools to ask and answer causal questions with greater precision.

Over the next three chapters, you will embark on a structured journey into modern causal thinking. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, introducing the potential outcomes framework to formally define causal effects and using Directed Acyclic Graphs (DAGs) to visualize and manage confounding. The second chapter, "Applications and Interdisciplinary Connections," explores how these foundational principles are operationalized through various statistical methods and applied across diverse fields, from genetics to artificial intelligence. Finally, "Hands-On Practices" provides an opportunity to apply these concepts to solve concrete problems in causal analysis. We begin by establishing the core principles and mechanisms that form the bedrock of all causal inquiry.

## Principles and Mechanisms

In the preceding chapter, we introduced the fundamental challenge of distinguishing causation from mere association. This chapter provides the formal scientific apparatus for this task. We will develop a systematic framework based on potential outcomes and causal graphs to define, identify, and estimate causal effects, particularly in the context of medical and public health research.

### The Potential Outcomes Framework

The cornerstone of modern causal inference is the **potential outcomes** framework, often called the Rubin Causal Model. To define a causal effect, we must be able to conceive of counterfactuals. For an individual unit $i$ (e.g., a patient) and a binary treatment or exposure $X \in \{0,1\}$, we define two potential outcomes:

*   $Y_i(1)$: The outcome that would be observed if unit $i$ were to receive the treatment ($X=1$).
*   $Y_i(0)$: The outcome that would be observed if unit $i$ were to receive the control ($X=0$).

The **individual causal effect** for unit $i$ is the difference between these two potential outcomes: $Y_i(1) - Y_i(0)$. This definition immediately reveals the **fundamental problem of causal inference**: for any given individual, we can only ever observe one of the potential outcomes. We can observe $Y_i(1)$ if the patient receives the treatment or $Y_i(0)$ if the patient receives the control, but never both. We observe the factual, but the counterfactual remains unseen.

Because individual causal effects are not observable, the goal of causal inference shifts to estimating **average causal effects** across a population, such as the **Average Treatment Effect (ATE)**, defined as $\text{ATE} = \mathbb{E}[Y(1) - Y(0)] = \mathbb{E}[Y(1)] - \mathbb{E}[Y(0)]$. The task then becomes one of estimating the average potential outcomes, $\mathbb{E}[Y(1)]$ and $\mathbb{E}[Y(0)]$, from observed data.

### Well-Posed Causal Questions: The Stable Unit Treatment Value Assumption (SUTVA)

Before we can estimate causal effects, we must ensure the causal question itself is well-posed. The notation $Y(x)$ contains powerful, but often hidden, assumptions about the nature of the treatment and the units. These are formalized by the **Stable Unit Treatment Value Assumption (SUTVA)**, which comprises two distinct components.

#### Treatment Version Equivalence and Consistency

The notation $Y(1)$ implicitly assumes that the treatment level "$1$" is a single, well-defined intervention. If "$X=1$" can mean different things, with different effects, then the potential outcome $Y(1)$ is ambiguous. For instance, in a study on the effect of statin therapy post-myocardial infarction, "statin therapy initiated" ($X=1$) might encompass various drugs and doses, from high-intensity atorvastatin to moderate-intensity simvastatin [@problem_id:4961040]. If these different versions, which we can index by $v$, have different effects, then the potential outcome should be written as $Y(1,v)$. The simplified notation $Y(1)$ is only valid under the assumption of **treatment version equivalence**, which states that $Y(1,v) = Y(1,v')$ for all feasible versions $v$ and $v'$. If different statin regimens plausibly have different effects on mortality, this assumption is violated, and the causal question must be refined to be about specific regimens (e.g., "the effect of high-intensity atorvastatin").

The second part of this is the **consistency assumption**, which links potential outcomes to observed outcomes. It states that the observed outcome $Y$ for a unit that received treatment $X=x$ is precisely its potential outcome under that treatment: $Y = Y(X)$. This seems trivial, but it relies on the treatment being well-defined, as discussed above.

#### No Interference

SUTVA also requires the assumption of **no interference**, which states that the potential outcomes for one unit are not affected by the treatment assignments of other units [@problem_id:4961013]. Formally, the potential outcome for unit $i$, $Y_i(x)$, does not depend on the treatment vector $\mathbf{X}_{-i}$ assigned to all other units. This assumption is often violated in infectious disease contexts. In a ward-based vaccination program, for example, an individual's risk of infection depends not only on their own vaccination status but also on the proportion of others in the ward who are vaccinated (the herd effect). In such cases, the simple potential outcome $Y_i(x)$ is ill-defined because its value depends on the actions of others. The problem can sometimes be resolved by defining more [complex potential](@entry_id:162103) outcomes that explicitly account for the interference, such as $Y_i(x, g)$, representing the outcome under individual treatment $x$ and neighborhood vaccine coverage $g$ [@problem_id:4961013].

### The Gold Standard: Randomized Controlled Trials and Exchangeability

The Randomized Controlled Trial (RCT) is considered the gold standard for causal inference precisely because its design guarantees that, on average, key assumptions are met. In an RCT, treatment $X$ is assigned to individuals by a random process (e.g., a coin flip) that is, by design, independent of all their other characteristics, both measured and unmeasured.

This randomization process achieves a crucial property known as **unconditional exchangeability** [@problem_id:4961098]. This means that the treatment assignment $X$ is statistically independent of the set of potential outcomes $\{Y(0), Y(1)\}$. Formally, $(Y(0), Y(1)) \perp X$. Intuitively, it means the group that was randomly assigned to treatment and the group assigned to control were, on average, identical in their prognoses before the treatment was administered. The only systematic difference between them is the treatment they receive.

Under exchangeability and consistency, we can identify the average potential outcomes directly from the observed data:
$$ \mathbb{E}[Y(x)] = \mathbb{E}[Y(x) \mid X=x] = \mathbb{E}[Y \mid X=x] $$
The first equality, $\mathbb{E}[Y(x)] = \mathbb{E}[Y(x) \mid X=x]$, holds due to exchangeability. The second equality, $\mathbb{E}[Y(x) \mid X=x] = \mathbb{E}[Y \mid X=x]$, holds due to consistency. This powerful result means that in an ideal RCT, the causal quantity $\mathbb{E}[Y(x)]$ is identified by the simple associational quantity $\mathbb{E}[Y \mid X=x]$—the average observed outcome in the group that received treatment $x$. For example, if a trial randomizes $749$ patients to a treatment and observes $163$ events, the best estimate for the population-level risk under treatment, $\mathbb{E}[Y(1)]$, is simply the observed risk in the treated group, $\frac{163}{749} \approx 0.2176$ [@problem_id:4961098].

### The Challenge of Observational Studies: Confounding

In observational studies, treatment is not assigned by the investigator; it is observed as it occurs in clinical practice. This means exchangeability is often violated. When a variable influences both the choice of treatment and the outcome, we have **confounding**.

Consider an observational study of an anticoagulant for stroke prevention, where physicians tend to prescribe the treatment to more severely ill patients [@problem_id:4961038]. Let $X$ be the treatment, $Y$ be the stroke outcome, and $S$ be baseline severity. Because severe patients ($S=1$) have a higher underlying risk of stroke and are also more likely to be treated, a naive comparison of treated and untreated patients may be misleading. In one such hypothetical scenario, the crude risk among the treated is $0.25$, while the risk among the untreated is $0.16$, suggesting the treatment is harmful. However, within the strata of mild patients ($S=0$), the risks are $0.05$ (treated) vs. $0.10$ (untreated), and within severe patients ($S=1$), the risks are $0.30$ (treated) vs. $0.40$ (untreated). In both strata, the treatment appears beneficial. This reversal is a classic example of **Simpson's Paradox**, induced by the [confounding variable](@entry_id:261683) $S$.

To formalize these relationships, we use **Directed Acyclic Graphs (DAGs)**. In a DAG, nodes represent variables and arrows represent direct causal effects. A **confounder** is represented as a common cause of treatment and outcome. In the anticoagulant example, the [causal structure](@entry_id:159914) is $X \leftarrow S \rightarrow Y$. The path $X \leftarrow S \rightarrow Y$ is a non-causal path, often called a **back-door path**, that creates a [statistical association](@entry_id:172897) between $X$ and $Y$ even if $X$ has no causal effect on $Y$. This is precisely the situation of **confounding by indication**, common in medical research, where patient prognosis influences the choice of therapy [@problem_id:4961095].

### Identification of Causal Effects in Observational Studies

To estimate causal effects from observational data, we must try to emulate an RCT by breaking the link between confounders and treatment choice. This is achieved through statistical adjustment, which rests on three key assumptions: conditional exchangeability, positivity, and consistency (as part of SUTVA).

#### Conditional Exchangeability

While unconditional exchangeability ($Y(x) \perp X$) rarely holds in observational studies, we might be able to argue for a weaker assumption: **conditional exchangeability**. If we have measured a sufficiently rich set of confounding variables $Z$, we may be able to assume that within levels of $Z$, treatment assignment is independent of potential outcomes:
$$ Y(x) \perp X \mid Z $$
This means that, for example, among patients with the same baseline severity, those who received treatment and those who did not are, on average, comparable. This assumption is also known as "no unmeasured confounding" or "ignorability". It is a strong, untestable assumption that is the foundation of most causal inference from observational data [@problem_id:4961095].

#### The Back-Door Criterion and Collider Bias

How do we choose a sufficient set of covariates $Z$ to adjust for? The **back-door criterion** provides a formal rule using a DAG [@problem_id:4961008]. A set of variables $Z$ satisfies the back-door criterion relative to $(X,Y)$ if:
1.  No variable in $Z$ is a descendant of $X$.
2.  $Z$ blocks every back-door path between $X$ and $Y$ (a path with an arrow into $X$).

The first rule prevents us from "adjusting away" part of the effect by conditioning on a **mediator**—a variable on the causal pathway from $X$ to $Y$ (e.g., $M$ in $X \rightarrow M \rightarrow Y$).

The second rule is the core of confounding control. However, it comes with a critical warning about a specific type of variable: a **[collider](@entry_id:192770)**. A [collider](@entry_id:192770) is a common effect of two other variables (e.g., $H$ in $X \rightarrow H \leftarrow Y$). Back-door paths containing a [collider](@entry_id:192770) are *already blocked* by the collider. Conditioning on a collider *opens* the path, inducing a non-causal association between its causes. This phenomenon is known as **[collider bias](@entry_id:163186)** or selection bias [@problem_id:4961077]. For example, if both pre-hospital antipyretic use ($X$) and underlying infection severity ($Y$) increase the chance of hospitalization ($H$), then among hospitalized patients, an artificial negative association may appear between $X$ and $Y$. This is because, given that a patient is hospitalized, the absence of one cause (e.g., low severity) makes the presence of the other cause (antipyretic use) more likely. Adjusting for colliders is a common and serious error in statistical analysis.

Applying the back-door criterion to a DAG with confounders $Z_1, Z_2$, a mediator $M$, and a [collider](@entry_id:192770) $C$, the correct minimal adjustment set to identify the total effect of $X$ on $Y$ would be $\{Z_1, Z_2\}$, as this set blocks the confounding paths without including descendants of $X$ or opening paths through colliders [@problem_id:4961008].

#### Positivity (Overlap)

The final crucial assumption for identification via adjustment is **positivity**, also known as overlap. This assumption requires that for every level of the covariates $Z$ present in the population, there is a non-zero probability of receiving each treatment level. Formally, for all $z$ with $P(Z=z) > 0$, we must have $P(X=x \mid Z=z) > 0$ for all $x$.

If this assumption is violated, there are certain subgroups of the population for whom we only ever observe one treatment condition. For example, if a clinical guideline mandates that all patients with profound hypotension ($Z=1$) receive vasopressor therapy ($X=1$), then $P(X=0 \mid Z=1) = 0$. We have no data on what would happen to profoundly hypotensive patients if they were *not* treated. It becomes impossible to estimate the stratum-specific outcome $\mathbb{E}[Y \mid X=0, Z=1]$ from the data, and thus we cannot compute the causal effect for the overall population without making untestable extrapolation assumptions [@problem_id:4961083].

#### The Standardization Formula

When the three assumptions of consistency, conditional exchangeability, and positivity hold, we can identify the average potential outcomes using the **standardization formula** (or g-formula). This formula calculates what the average outcome would be if everyone in the population had the covariate distribution $P(Z)$, but received the stratum-specific outcomes corresponding to treatment level $x$. Formally, the interventional distribution $P(Y \mid do(X=x))$ is given by:
$$ P(Y \mid do(X=x)) = \sum_{z} P(Y \mid X=x, Z=z) P(Z=z) $$
The corresponding expectation is $\mathbb{E}[Y(x)] = \sum_{z} \mathbb{E}[Y \mid X=x, Z=z] P(Z=z)$. This formula differs crucially from the associational quantity, which is $P(Y \mid X=x) = \sum_{z} P(Y \mid X=x, Z=z) P(Z=z \mid X=x)$ [@problem_id:4961084]. The causal formula uses the [marginal distribution](@entry_id:264862) of the confounder, $P(Z=z)$, effectively creating a pseudo-population where the confounder distribution is the same across treatment groups, thus mimicking an RCT. Applying this formula to the anticoagulant data from our earlier example reveals that the treatment provides a risk reduction of $0.075$, the opposite of the naive associational result [@problem_id:4961038].

### Defining the Causal Estimand: ATE, ATT, and ATC

Finally, the potential outcomes framework allows us to be precise about the causal question we are asking. While the ATE is a common target, other estimands may be more relevant for specific policy decisions, especially in observational studies where treatment effects might be heterogeneous [@problem_id:4961043].

*   **Average Treatment Effect (ATE)**: $\mathbb{E}[Y(1) - Y(0)]$. This is the average effect over the entire population. It is most relevant for deciding on a universal policy, such as whether to make an intervention standard practice for everyone.

*   **Average Treatment effect on the Treated (ATT)**: $\mathbb{E}[Y(1) - Y(0) \mid X=1]$. This is the average effect specifically among those who actually received the treatment in the observed data. It answers the question: "For the patients who are already receiving this intervention, how much benefit did they get?" This is relevant for evaluating existing programs or considering their de-implementation.

*   **Average Treatment effect on the Controls (ATC)** or Untreated (ATU): $\mathbb{E}[Y(1) - Y(0) \mid X=0]$. This is the average effect specifically among those who did not receive the treatment. It answers the question: "For the patients currently not receiving this intervention, what benefit would they get if we were to treat them?" This is the key estimand for decisions about expanding a program to new groups.

In an RCT, ATE, ATT, and ATC are typically all equal due to exchangeability. In an observational study, however, these quantities can differ substantially if the characteristics of the treated and untreated populations are different. Recognizing which estimand aligns with the clinical or policy question at hand is a critical step in a well-posed causal analysis.