## Introduction
Understanding the causes of health and disease is the cornerstone of epidemiology. While we can easily observe associations between an exposure and an outcome, determining whether that association is truly causal is a complex challenge fraught with potential biases. Simply observing that people who take a certain drug have worse outcomes does not mean the drug is harmful; the underlying illness might be the true cause of both the prescription and the outcome. This article provides a formal framework for navigating these complexities and moving from mere association to robust causal inference.

This guide is structured to build your understanding from the ground up. In the first chapter, **Principles and Mechanisms**, we will introduce the foundational concepts of the [potential outcomes framework](@entry_id:636884), define the average causal effect, and explore the core assumptions—consistency, exchangeability, and positivity—that make causal inference possible. We will also introduce Directed Acyclic Graphs (DAGs) as a powerful tool for visualizing causal structures and identifying key biases like confounding and selection bias.

Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action. We will examine how they are used to address real-world epidemiological questions, from establishing the causal link between smoking and cancer to tackling modern challenges like confounding by indication in pharmacoepidemiology and using genetic data in Mendelian randomization.

Finally, the **Hands-On Practices** section offers an opportunity to apply what you've learned by working through guided problems on key analytical methods, such as standardization and inverse probability weighting. By the end of this journey, you will be equipped with the conceptual tools needed to critically evaluate and conduct causal research in epidemiology and related health sciences.

## Principles and Mechanisms

### The Causal Question: Potential Outcomes and the Average Causal Effect

The central goal of epidemiology is to understand the causes of health and disease. While we may casually speak of causes and effects, a scientifically rigorous definition requires a more precise language. At the heart of modern causal inference lies the concept of a **potential outcome**, which formalizes the intuitive notion of "what would have happened."

Imagine a simple study of a binary exposure, $A$, such as receiving a vaccine ($A=1$) versus not receiving it ($A=0$), and a health outcome, $Y$. For any single individual, we can conceptualize two potential outcomes:
-   $Y^{1}$: The outcome this individual *would have* if they were exposed ($A=1$).
-   $Y^{0}$: The outcome this individual *would have* if they were not exposed ($A=0$).

These outcomes are "potential" because, for any given individual, at least one of them will be counterfactual—that is, contrary to what actually happened. The causal effect of the exposure for that specific individual is the difference between their two potential outcomes, $Y^{1} - Y^{0}$. However, we can never observe both $Y^{1}$ and $Y^{0}$ for the same person at the same time. If an individual receives the vaccine, we observe $Y^{1}$, but their un-vaccinated outcome, $Y^{0}$, remains unobserved. Conversely, if they do not receive the vaccine, we observe $Y^{0}$, and $Y^{1}$ remains unobserved. This is known as the **Fundamental Problem of Causal Inference**: causal inference is a missing data problem, as we are systematically missing the counterfactual outcome for every individual in our study [@problem_id:4575725].

Because we cannot calculate individual-level causal effects, we shift our focus to the population average. The **Average Causal Effect (ACE)**, often called the **Average Treatment Effect (ATE)**, is defined as the difference in the expected (or average) potential outcomes over the entire population of interest:

$$
\text{ATE} = E[Y^{1}] - E[Y^{0}]
$$

By the [linearity of expectation](@entry_id:273513), this is equivalent to the average of the individual-level causal effects, $E[Y^{1} - Y^{0}]$. The ATE tells us, on average, how much the outcome would change if we could somehow move the entire population from being unexposed to being exposed. This is the primary target of most causal inquiries in epidemiology.

### From Association to Causation: The Core Identification Assumptions

It is crucial to distinguish the causal ATE from a simple associational measure. In observational data, we can easily calculate the difference in the average outcome between the group that was actually exposed and the group that was unexposed: $E[Y \mid A=1] - E[Y \mid A=0]$. This associational contrast compares outcomes between two potentially very different groups of people. For instance, in an observational study of a new drug, those who chose to take it ($A=1$) might be sicker on average than those who did not ($A=0$). In contrast, the ATE compares the average outcome in the *same* population under two different hypothetical exposure scenarios [@problem_id:4575725].

For the observed association to equal the causal ATE, we must be willing to make three core assumptions, often called the **identification assumptions**. These assumptions form the logical bridge that allows us to use observable data to learn about unobservable causal effects.

#### 1. Consistency

The **consistency** assumption links the potential outcomes, which are theoretical constructs, to the observed data. It states that an individual's observed outcome is their potential outcome corresponding to the exposure they actually received. Formally, if an individual's observed exposure is $A$, their observed outcome $Y$ is equal to $Y^{A}$.

$$
Y = Y^{A}
$$

While seemingly trivial, consistency is a powerful and necessary assumption that demands our exposure variable, $A$, represent a well-defined intervention. If the "exposure" is ambiguous, consistency can fail. Consider two scenarios [@problem_id:4575755]:

-   **Vague Treatment Definitions**: Suppose a study protocol for physical therapy ($A=1$) allows for both high-intensity and low-intensity versions. If both are recorded simply as $A=1$, but the effect differs ($Y^{1, \text{high}} \neq Y^{1, \text{low}}$), then there is no single, well-defined potential outcome $Y^{1}$. The quantity $E[Y \mid A=1]$ becomes an uninterpretable average of the effects of two different treatments, and it cannot identify a single causal effect.

-   **Exposure Measurement Error**: Imagine the true exposure is $A$, but we observe a misclassified version, $A^{*}$. If we naively try to apply consistency to the observed data, we would write $Y=Y^{A^{*}}$. However, for an individual whose true exposure is $A=0$ but is misclassified as $A^{*}=1$, their observed outcome is $Y = Y^{0}$. The consistency statement would falsely equate this to $Y^{1}$. Because of this disconnect, the observed associational contrast $E[Y \mid A^{*}=1] - E[Y \mid A^{*}=0]$ will be a biased estimate of the ATE.

#### 2. Exchangeability (No Confounding)

**Exchangeability** is the crucial "no confounding" assumption. It posits that the potential outcomes are independent of the exposure that was actually received. Formally:

$$
(Y^{0}, Y^{1}) \perp A
$$

Intuitively, this means that the group that received the treatment and the group that did not were, on average, comparable with respect to their prognosis or risk of the outcome *before* the exposure was assigned. If exchangeability holds, then the risk of the outcome in the treated group *would have been* the same as the risk in the untreated group, had they instead been left untreated. An ideal **Randomized Controlled Trial (RCT)**, with perfect adherence, achieves exchangeability by design. The random assignment of exposure ensures that, on average, the exposure groups are balanced on all pre-exposure characteristics, both measured and unmeasured. Therefore, in an ideal RCT, the association is the causation: $E[Y \mid A=1] - E[Y \mid A=0] = E[Y^{1}] - E[Y^{0}] = \text{ATE}$ [@problem_id:4575725].

In observational studies, exchangeability is rarely plausible. We must instead rely on a weaker, conditional form, which we will discuss below.

#### 3. Positivity

The **positivity** assumption, sometimes called the experimental treatment assignment assumption, requires that every individual in the population has a non-zero probability of receiving every level of the exposure. For a binary exposure:

$$
P(A=a) > 0 \text{ for } a \in \{0, 1\}
$$

If, for example, no one in the study population ever receives the treatment ($P(A=1)=0$), it is self-evidently impossible to estimate its effect. As with exchangeability, this assumption becomes more nuanced when we consider other covariates.

### Visualizing Causal Structures: Directed Acyclic Graphs (DAGs)

To navigate the complexities of causal inference in non-ideal, observational settings, it is invaluable to have a visual language for our assumptions. **Directed Acyclic Graphs (DAGs)** provide this language [@problem_id:4575749]. In a causal DAG:

-   **Nodes** represent random variables (e.g., exposure, outcome, covariates).
-   **Directed arrows** ($ \rightarrow $) represent hypothesized direct causal effects. For example, an arrow from $A$ to $Y$ ($A \to Y$) means we assume $A$ is a direct cause of $Y$.
-   The graph is **acyclic**, meaning there are no directed paths that start and end at the same node. This reflects the natural asymmetry of time and causation.

The power of a DAG is that it encodes conditional independence relationships via a graphical rule called **[d-separation](@entry_id:748152)**. If a set of nodes $X$ is d-separated from a set of nodes $Y$ by a third set of nodes $Z$, then our DAG implies that the variables $X$ and $Y$ must be conditionally independent given the variables in $Z$. These implied conditional independencies are testable predictions that allow us to check if our assumed causal structure is compatible with the observed data [@problem_id:4575749].

Paths in a DAG can be of several types. A **causal path** is a directed path from exposure to outcome (e.g., $A \to M \to Y$). A **non-causal path** connects exposure and outcome through other routes. Understanding these non-causal paths is the key to identifying and controlling for bias.

### Bias in Causal Inference: Confounding and Selection Bias

Two major types of bias that can distort causal estimates are confounding and selection bias. DAGs provide a clear way to understand and distinguish them.

#### Confounding Bias

Confounding arises when the exposure and outcome share a common cause. On a DAG, this is represented by a **backdoor path**: a non-causal path from exposure $A$ to outcome $Y$ that begins with an arrow pointing into $A$.

For example, in a study of smoking ($S$) and lung cancer ($C$), a genetic predisposition ($G$) might be a common cause of both. This is represented by the path $S \leftarrow G \to C$. This path is a backdoor path because it starts with an arrow into the exposure, $S$. This open backdoor path creates a non-causal association between smoking and cancer, which gets mixed in with any real causal effect. This is confounding [@problem_id:4575749].

From the potential outcomes perspective, the existence of an open backdoor path is equivalent to a violation of marginal exchangeability ($Y^a \not\perp A$). The solution to confounding is to "block" all open backdoor paths. We achieve this by **conditioning** on the confounding variable(s). By stratifying our analysis by the confounder $L$ (or adjusting for it in a [regression model](@entry_id:163386)), we render the backdoor path inactive. This allows us to achieve **conditional exchangeability**, $Y^a \perp A \mid L$, which is the assumption that within levels of the confounder $L$, exposure is effectively random with respect to the potential outcomes [@problem_id:4575764].

To use this adjustment strategy, the **positivity** assumption must also hold within strata of the confounders. We must require that $P(A=a \mid L=l) > 0$ for all treatment levels $a$ and all covariate strata $l$ that exist in our population ($P(L=l)>0$). If this condition fails, identification is impossible without further untestable assumptions. For instance, if in a study of a new surgery, all patients with a severe comorbidity ($L=1$) receive the standard of care ($A=0$), then $P(A=1 \mid L=1) = 0$. We have no data on what would happen to these severely ill patients if they received the new surgery. Therefore, we cannot estimate the stratum-specific effect in the $L=1$ group, and the overall ATE becomes non-identifiable [@problem_id:4575700].

#### Selection Bias

Selection bias is a different form of bias that is often more insidious. It does not arise from pre-existing common causes but is instead induced by the researcher's actions—specifically, by conditioning on a common effect. A variable that is a common effect of two other variables is called a **[collider](@entry_id:192770)**. On a DAG, a collider on a path is a node with two arrows pointing into it (e.g., $A \to S \leftarrow Y$).

The rules of [d-separation](@entry_id:748152) state that a path containing a collider is naturally blocked. However, if we condition on the collider (or a descendant of the collider), the path becomes *open*, creating a spurious association between its parents. This is often called **[collider](@entry_id:192770)-stratification bias** [@problem_id:4575749].

A classic example occurs in studies where selection into the study sample ($S$) is affected by both the exposure ($A$) and the outcome ($Y$). In this case, $S$ is a [collider](@entry_id:192770) on the path $A \to S \leftarrow Y$. By restricting the analysis to the selected sample ($S=1$), we are conditioning on a collider. This can induce an association between $A$ and $Y$ even if none existed in the source population [@problem_id:4575764].

Consider a hypothetical scenario where a new medication ($A$) has no causal effect on recovery ($Y$), so $A \perp Y$. However, both the medication and the illness symptoms affect the decision to be hospitalized ($S$). If we conduct our study only on hospitalized patients (conditioning on $S=1$), we can create a spurious association between $A$ and $Y$ among the hospitalized. For instance, among patients hospitalized with severe symptoms, those taking the medication might appear to have worse outcomes, not because the medication is harmful, but because the medication use is a marker for a condition that was severe enough to warrant hospitalization in the first place [@problem_id:4575768].

The distinction is critical: confounding is a bias due to a *common cause* that we must actively block by conditioning. Selection bias is a bias due to conditioning on a *common effect* (a collider), which we must avoid.

### Refining the Causal Question: Effect Modification and Mediation

Beyond simply asking "What is the average causal effect?", we can ask more nuanced questions about how the effect works and for whom.

#### Effect Measure Modification (EMM)

The magnitude of a causal effect may not be uniform across the entire population. When the effect of an exposure on an outcome differs across strata of a third variable, $L$, we say there is **Effect Measure Modification (EMM)** by $L$. The variable $L$ is also known as an effect modifier or an [interaction term](@entry_id:166280).

Crucially, the presence or absence of EMM depends on the mathematical **scale** used to measure the effect. The two most common scales in epidemiology for binary outcomes are the additive scale (Risk Difference) and the multiplicative scale (Risk Ratio). An effect can be uniform on one scale but vary on the other.

Consider a treatment that halves the risk of an outcome in all subjects (constant Risk Ratio of 0.5). In a low-risk group ($L=0$) with a baseline risk of $0.10$, the treatment reduces the risk to $0.05$, for a Risk Difference of $-0.05$. In a high-risk group ($L=1$) with a baseline risk of $0.40$, the treatment reduces the risk to $0.20$, for a Risk Difference of $-0.20$. Here, the Risk Ratio is constant ($0.5$), indicating no EMM on the multiplicative scale. However, the Risk Difference varies ($-0.05 \neq -0.20$), indicating the presence of EMM on the additive scale [@problem_id:4575733].

EMM is not a bias. It is a real feature of the causal relationship, reflecting biological or social interaction. Identifying EMM is often a primary goal of a study, as it can inform which subgroups of the population will benefit most (or be harmed most) by an intervention. It is fundamentally different from confounding, which is a bias we seek to eliminate [@problem_id:4575733].

#### Mediation: Natural Direct and Indirect Effects

Another way to refine our causal question is to investigate the mechanisms or pathways through which an effect operates. **Mediation analysis** aims to decompose the total causal effect of an exposure $A$ on an outcome $Y$ into a **direct effect** and an **indirect effect** that is transmitted through an intermediate variable, or **mediator**, $M$. The canonical causal structure is $A \to Y$ (direct path) and $A \to M \to Y$ (indirect path).

To define these effects, we must introduce a more complex type of potential outcome. Let $Y^{a, M^{a'}}$ denote the nested potential outcome representing the outcome if we were to set the exposure to level $a$, but set the mediator to the value it *would have naturally taken* if the exposure had been $a'$. Using this notation, we can define [@problem_id:4575718]:
-   **Natural Direct Effect (NDE)**: The effect of changing the exposure from $a'$ to $a$ while keeping the mediator at the level it would have taken under the reference exposure $a'$.
    $$ \text{NDE} = E[Y^{a, M^{a'}}] - E[Y^{a', M^{a'}}] $$
-   **Natural Indirect Effect (NIE)**: The effect on the outcome of changing the mediator from its natural value under $a'$ to its natural value under $a$, while holding the direct effect of exposure constant at level $a$.
    $$ \text{NIE} = E[Y^{a, M^{a}}] - E[Y^{a, M^{a'}}] $$

The sum of the NDE and NIE gives the total average causal effect. Identifying these effects is challenging because they involve "cross-world" counterfactuals like $Y^{a, M^{a'}}$, which depend on potential outcomes under two different exposure worlds simultaneously. In addition to standard assumptions like consistency and no unmeasured confounding, their identification requires a strong and untestable assumption of **cross-world independence**, such as $Y^{a,m} \perp M^{a'} \mid L$. This assumes that, after accounting for baseline covariates $L$, the value a person's mediator would take under exposure $a'$ is independent of the outcome they would have if their exposure were set to $a$ and their mediator were set to some value $m$ [@problem_id:4575718].

### Advanced Topics: Complex Causal Dependencies

The foundational principles described above form the basis for tackling more complex causal scenarios.

#### Interference and SUTVA

Our simplified potential outcome notation $Y^a$ implicitly bundles two major assumptions, which together are known as the **Stable Unit Treatment Value Assumption (SUTVA)** [@problem_id:4575765]. SUTVA comprises:
1.  **Consistency**: As defined previously, the exposure level must be well-defined.
2.  **No Interference**: The potential outcome of one individual does not depend on the exposure status of any other individual in the population.

The no-interference assumption allows us to write an individual's potential outcome as $Y_i^a$, depending only on their own exposure $a$. A more general notation would be $Y_i^{a, \mathbf{a}_{-i}}$, where $\mathbf{a}_{-i}$ is the vector of exposures for everyone else. No interference states that $Y_i^{a, \mathbf{a}_{-i}} = Y_i^{a, \mathbf{a}'_{-i}}$ for any two different exposure vectors $\mathbf{a}_{-i}$ and $\mathbf{a}'_{-i}$ for the rest of the population. This assumption is often violated in studies of infectious diseases (where one person's vaccination status affects another's risk of infection) or in social or educational settings. In such cases, we may need to relax the assumption to, for example, "no interference between clusters," allowing for effects within a household or school but not between them [@problem_id:4575765].

#### Time-Varying Confounding

A particularly challenging problem in longitudinal studies is **time-varying confounding**. This occurs when a variable $L_t$ at time $t$ is both:
1.  A **confounder** for a future exposure-outcome relationship (e.g., $L_t$ is a common cause of $A_{t+1}$ and $Y$).
2.  An **intermediate** on the causal pathway from a past exposure (e.g., $A_{t-1}$ is a cause of $L_t$).

Consider a treatment for a chronic disease, where physicians adjust the dose ($A_t$) at each visit based on the patient's current clinical status ($L_t$), and the past dose ($A_{t-1}$) affects that clinical status. Here, $L_t$ is a time-varying confounder affected by prior treatment.

Standard adjustment methods fail in this scenario. If we adjust for $L_t$ in a regression model to control for its confounding of the $A_{t+1} \to Y$ relationship, we inadvertently block the portion of the causal effect of $A_{t-1}$ that acts through $L_t$ (the path $A_{t-1} \to L_t \to Y$). This biases the estimate of the total effect of the treatment history. Correctly identifying causal effects in the presence of time-varying confounding requires advanced methods such as the **g-formula** or **Inverse Probability of Treatment Weighting (IPTW)** for Marginal Structural Models, which properly account for the temporal sequence of events [@problem_id:4575744].