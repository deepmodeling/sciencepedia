## Introduction
In the realm of public health and preventive medicine, resources are finite, while the potential interventions are vast. This reality creates a critical need for rigorous, quantitative methods to determine which health strategies offer the best value for money. How do we decide whether to implement a new screening program, fund a vaccination campaign, or approve a novel preventive medication? This article addresses this fundamental challenge by introducing the core analytical tools of health economic evaluation: decision trees and Markov models. These models provide a structured framework for synthesizing clinical evidence, costs, and patient outcomes to make rational, evidence-based decisions about resource allocation.

This article will guide you through the theory and practice of health [economic modeling](@entry_id:144051) in three parts. First, the "Principles and Mechanisms" chapter will deconstruct decision trees and Markov models, explaining their core components, mathematical foundations, and the assumptions that underpin them. You will learn how to structure a decision problem and simulate disease progression over time. Next, in "Applications and Interdisciplinary Connections," we will explore how these theoretical models are applied to solve real-world problems in preventive medicine, from evaluating screening programs to incorporating complex patient behaviors and connecting with fields like epidemiology and ethics. Finally, the "Hands-On Practices" section will provide opportunities to apply your knowledge, reinforcing the key concepts and building practical skills in model calculation and interpretation.

## Principles and Mechanisms

This chapter delineates the foundational principles and operational mechanisms of the primary analytical tools used in health economic evaluation: decision trees and Markov models. We will explore the theoretical underpinnings of each method, their structural components, and the mathematical formalisms required for their correct application in assessing the value of preventive health interventions.

### The Anatomy of a Decision: Decision Trees

A decision tree is a powerful tool for modeling problems that involve a sequence of choices and uncertain events unfolding over a relatively short and finite time horizon. This framework is most appropriate when the clinical pathway is straightforward, events are not recurrent, and all significant outcomes are resolved within the modeled period. Consider, for example, the evaluation of a single-dose vaccine against an acute infectious disease where reinfection is negligible; the sequence of events (vaccination, potential adverse event, potential infection, recovery) is linear and does not loop back on itself [@problem_id:4530865].

#### Core Components of a Decision Tree

A decision tree is composed of a specific set of building blocks that visually and mathematically structure the decision problem.

*   **Decision Nodes:** A decision tree begins with a **decision node**, typically represented by a square. This node signifies a point where the decision-maker must choose between two or more mutually exclusive strategies. For instance, in evaluating a preventive screening program, the primary decision node would represent the choice between 'Offer Screening' and 'No Screening' [@problem_id:4530928].

*   **Chance Nodes:** Emanating from each branch of a decision node are sequences of **chance nodes**, typically represented by circles. Each chance node represents a point of uncertainty where an event occurs according to a set of probabilistic outcomes. The branches extending from a chance node must be **mutually exclusive** and **[collectively exhaustive](@entry_id:262286)**, meaning that they represent all possible outcomes and their associated probabilities must sum to one [@problem_id:4530938]. For example, after the choice to 'Offer Screening', a chance node might represent the patient's underlying disease status (e.g., 'Disease Present' with probability $p$ or 'Disease Absent' with probability $1-p$). Subsequent chance nodes could represent test results (positive or negative, conditional on disease status), the occurrence of complications from follow-up procedures, or the development of symptoms.

*   **Terminal Nodes and Payoff Vectors:** The final endpoints of any path through the tree are called **terminal nodes**. Each terminal node represents a unique, complete sequence of events and decisions. In health [economic modeling](@entry_id:144051), it is crucial that each terminal node is assigned a **payoff vector**, not a single value. This vector typically has at least two components: total accrued **cost** ($C$) and total accrued **health outcome**, measured in **Quality-Adjusted Life Years (QALYs)**, $(C, Q)$ [@problem_id:4530938].

This vector-based approach is fundamental to **cost-effectiveness analysis (CEA)**. By tracking costs and QALYs separately, we can calculate the expected values for each dimension independently. This allows for the computation of trade-off metrics, such as the Incremental Cost-Effectiveness Ratio (ICER), which is the cornerstone of CEA. If costs and QALYs were collapsed into a single utility measure, this explicit trade-off would be lost. Furthermore, a vector payoff is necessary to distinguish between paths that may result in the same health state but incur different costs. For instance, in a vaccination model, the outcome 'No Infection' costs $0 if unvaccinated but incurs the cost of the vaccine if vaccinated; a single outcome label would obscure this vital economic difference [@problem_id:4530938].

#### Calculating Expected Values

The central operation in solving a decision tree is the calculation of expected values. For any chance node, the expected value of a given payoff (e.g., cost or QALYs) is the probability-weighted average of the payoffs of its subsequent branches. If a branch leads to a terminal node with payoff $v_i$ with probability $p_i$, the expected value is given by $E[V] = \sum_i p_i v_i$.

The process, often called "folding back" or "rolling back" the tree, starts from the terminal nodes and works backward. The expected value of each chance node is calculated. When a decision node is reached, the strategy with the most favorable expected value (e.g., highest expected QALYs or lowest expected cost, depending on the objective) is chosen, and the other branches are "pruned."

To illustrate, consider the evaluation of a one-time screening test for colorectal neoplasia [@problem_id:4530928]. For the 'No Screening' strategy, the tree branches by disease status. If the prevalence of disease is $0.06$ and the probability of a symptomatic event in the untreated is $0.2$, the path 'Disease' followed by 'Symptomatic Event' has a probability of $0.06 \times 0.2 = 0.012$. If this event costs \$10,000 and causes a QALY loss of 0.1, this path contributes $0.012 \times 10,000 = 120$ to the expected cost and $0.012 \times 0.1 = 0.0012$ to the expected QALY loss for the 'No Screening' arm. Summing over all paths gives the total expected values for that strategy. A similar, more complex calculation is performed for the 'Screening' arm, which includes additional branches for test results, follow-up procedures, and complications. By comparing the final expected cost and expected QALYs of the two main strategies, the analyst can determine which provides better value.

### Modeling Chronic and Recurrent Events: The Markov Model

While decision trees excel at modeling single, acute events, they are ill-suited for chronic diseases or situations involving recurrent events over long periods. Attempting to model a decade of potential annual cardiovascular events with a decision tree would lead to an unmanageably large "bushy" tree. For such problems, the **Markov model** is the appropriate and essential tool [@problem_id:4530865]. These models are designed to simulate the progression of a cohort of individuals through a set of health states over time, with the possibility of remaining in a state or transitioning to others at each time step.

#### Core Components of a Discrete-Time Markov Model

The structure of a Markov model is defined by a few key concepts, which together provide a powerful engine for simulating long-term health and economic outcomes [@problem_id:4530988].

*   **Markov States:** The model defines a set of **health states** that must be **mutually exclusive** (an individual can only be in one state at a time) and **[collectively exhaustive](@entry_id:262286)** (the states cover all possible conditions relevant to the model). Examples include 'Healthy', 'Preclinical Disease', 'Clinical Disease', and 'Dead'.

*   **The Memoryless Property:** The defining characteristic of a Markov process is the **memoryless property**. This principle states that the probability of transitioning to a future state depends *only* on the current state, not on the sequence of states that preceded it. Formally, for a process with states $X_t$ at time $t$:
    $$ \Pr(X_{t+1} = j \mid X_t = i, X_{t-1} = i_{t-1}, \ldots) = \Pr(X_{t+1} = j \mid X_t = i) $$
    This means the current state must capture all information from the past that is relevant for predicting the future. For example, if the risk of a future event depends on how long a person has had a disease, a simple 'Diseased' state would violate the [memoryless property](@entry_id:267849). To handle this, more complex states might be defined, such as 'Disease Year 1', 'Disease Year 2+', etc.

*   **Transition Probabilities and the Transition Matrix:** The movement of individuals between states is governed by a set of **one-step [transition probabilities](@entry_id:158294)**, denoted $p_{ij}$, which is the probability of moving from state $i$ to state $j$ in a single time cycle. These probabilities are organized into a square **[transition probability matrix](@entry_id:262281)**, $P$. Each entry in this matrix must be non-negative ($p_{ij} \ge 0$), and because an individual must be in *some* state in the next cycle, each row of the matrix must sum to $1$. Such a matrix is known as a **row-stochastic** matrix.

*   **Absorbing States:** A state is called **absorbing** if, once entered, it cannot be left. This is formally defined by the condition that for an [absorbing state](@entry_id:274533) $i$, the transition probability of remaining is $p_{ii} = 1$, and the probabilities of moving to any other state are $p_{ij} = 0$ for all $j \ne i$ [@problem_id:4530862]. In health economic models, 'Death' is the canonical [absorbing state](@entry_id:274533). Modeling it as such is not merely a convention but a logical necessity. It reflects the clinical irreversibility of death and ensures that once an individual enters the 'Dead' state, they cease to accumulate further costs or health utility in all subsequent model cycles [@problem_id:4530862]. This is fully consistent with the requirement for a valid transition matrix, as a row for the 'Death' state with a $1$ on the diagonal and $0$s elsewhere sums to $1$.

#### The Engine: Cohort Simulation and Accruing Outcomes

A Markov model simulates the evolution of a cohort over time. If we represent the proportion of the cohort in each state at the start of cycle $t$ with a row vector $\mathbf{x}_t$, the distribution at the start of the next cycle, $\mathbf{x}_{t+1}$, is found by simple matrix multiplication: $\mathbf{x}_{t+1} = \mathbf{x}_t \mathbf{P}$.

To perform a cost-effectiveness analysis, we must associate costs and health utilities with being in these states and discount them appropriately over time.

*   **State Rewards:** Each state $i$ is assigned a **reward vector** $(c_i, u_i)$, where $c_i$ is the cost rate and $u_i$ is the health utility rate associated with spending one full time unit in that state [@problem_id:4530859]. For example, $c_i$ might be the annual cost of maintenance medication for a chronic condition, and $u_i$ would be the quality-of-life weight for that health state.

*   **Discounting:** Future costs and health outcomes are valued less than present ones. This is due to **time preference** (people prefer benefits sooner) and **opportunity cost** (resources invested today can generate returns). Therefore, we apply a **[discount rate](@entry_id:145874)**, $r$, to convert future values to their **[present value](@entry_id:141163)**. For a cost or benefit $x_t$ occurring at the end of year $t$, its present value is $PV = \frac{x_t}{(1+r)^t}$ [@problem_id:4531024]. Health outcomes (QALYs) are discounted by the same principle to reflect time preference for health.

*   **Per-Cycle Accrual and Half-Cycle Correction:** In a discrete-time model, costs and QALYs are often assumed to accrue continuously throughout a cycle. A simple approach would be to assign them at the start or end of the cycle, but this introduces a known bias. A more accurate and standard method is to apply a **half-cycle correction**. This method approximates the continuous accrual by assuming that the average cohort distribution during the cycle is the average of the start- and end-of-cycle distributions. This reward is then discounted from the midpoint of the cycle. For a cycle $t$ (from time $t$ to $t+1$) of length $\Delta t$, with discount factor $\delta = \frac{1}{1+r}$, the discounted cost ($C_t$) and QALYs ($Q_t$) are calculated as [@problem_id:4530859]:
    $$ C_t = \delta^{t+\frac{1}{2}} \left( \frac{\mathbf{x}_t + \mathbf{x}_{t+1}}{2} \right) \mathbf{c} \, \Delta t $$
    $$ Q_t = \delta^{t+\frac{1}{2}} \left( \frac{\mathbf{x}_t + \mathbf{x}_{t+1}}{2} \right) \mathbf{u} \, \Delta t $$
    Here, $\mathbf{c}$ and $\mathbf{u}$ are column vectors of the state costs and utilities. Total expected discounted costs and QALYs are found by summing these values over all cycles in the model's time horizon.

### Key Outcomes and Model-Building Considerations

Constructing a valid and credible model requires careful consideration of the metrics used for outcomes and the structural assumptions about time.

#### Defining Health Outcomes: QALYs vs. DALYs

While this text focuses on QALYs, another common health outcome metric is the **Disability-Adjusted Life Year (DALY)**. Understanding their differences is crucial for interpreting study results [@problem_id:4530881].

*   A **Quality-Adjusted Life Year (QALY)** is a measure of health *gained*. It is calculated by weighting time spent in a health state by a preference-based utility value, where $1.0$ represents perfect health and $0.0$ represents death.
*   A **Disability-Adjusted Life Year (DALY)** is a measure of health *lost*. It is the sum of Years of Life Lost (YLL) due to premature mortality and Years Lived with Disability (YLD), where YLD is calculated by weighting time spent in a state of illness by a disability weight ($dw$), where $0.0$ represents no disability and $1.0$ represents a state equivalent to death.

QALY gains and DALYs averted will only be equivalent under very specific conditions: negligible impact on mortality (so YLL is zero) and utility weights that are the direct complement of disability weights (i.e., $u = 1 - dw$) for all health states. In most realistic scenarios, especially those involving mortality, the two metrics will yield different quantitative results due to their different conceptual frameworks [@problem_id:4530881].

#### Choosing the Right Time Scale: Cycle Length, Time Horizon, and Discretization Error

The temporal parameters of a model are critical structural choices that can significantly impact results [@problem_id:4531036].

*   **Time Horizon ($T$):** This is the total duration of the model. It should be long enough to capture all meaningful differences in costs and health outcomes between the strategies being compared. For preventive interventions, this often means a lifetime horizon. Truncating the horizon to a short budget cycle, for instance, would ignore long-term benefits and severely bias the analysis against prevention [@problem_id:4531036].

*   **Cycle Length ($t_c$):** This is the fixed time increment for transitions in a discrete-time model. The choice of $t_c$ introduces a **[discretization error](@entry_id:147889)**—a bias resulting from approximating a continuous-time disease process with discrete steps. This error worsens as the cycle length increases relative to the speed of clinical events. A fundamental assumption of a simple Markov model is that at most one event occurs per cycle. Therefore, the cycle length must be chosen to be shorter than the time scale of the most rapid, clinically relevant event. For example, in a model of [colorectal cancer](@entry_id:264919) screening, adverse events like perforation can occur within days, while disease progression occurs over years. Using an annual cycle length would grossly misrepresent the timing and consequences of these acute events [@problem_id:4531036].

*   **Hybrid Models:** To resolve the challenge of multiple time scales, analysts often employ **hybrid models**. A common approach is to use a short-term decision tree to model the immediate, fast-moving events (e.g., a surgical procedure and its peri-operative complications) and then use the terminal nodes of this tree as the starting states for a long-term Markov model with a longer, more efficient cycle length to simulate chronic disease progression [@problem_id:4531036].

### Addressing Uncertainty in Models

No model can perfectly represent reality, and a crucial part of the modeling process is to identify and quantify the impact of uncertainty on the conclusions.

#### Types of Uncertainty

There are two primary categories of uncertainty in health economic models.

*   **Parameter Uncertainty:** This refers to uncertainty in the numerical values of the model's inputs, such as probabilities, costs, and utility weights. These values are often estimated from clinical trials, observational studies, or expert opinion, and are subject to sampling variation and measurement error.

*   **Structural Uncertainty:** This more fundamental uncertainty arises from choices about the model's form and assumptions. This includes the choice of model type (e.g., decision tree vs. Markov), the definition of health states, the choice of cycle length and time horizon, and the inclusion or exclusion of certain clinical pathways [@problem_id:4531029].

#### Handling Parameter Uncertainty: Probabilistic Sensitivity Analysis (PSA)

The standard method for analyzing [parameter uncertainty](@entry_id:753163) is **Probabilistic Sensitivity Analysis (PSA)**. PSA is a Monte Carlo simulation technique where all uncertain parameters are simultaneously and repeatedly sampled from specified probability distributions. For each set of sampled parameters, the model is re-run to calculate the outcomes (e.g., incremental costs and QALYs). This process, repeated thousands of times, generates a distribution of outcomes that reflects the joint uncertainty across all parameters.

The choice of probability distribution for each parameter must be theoretically justified [@problem_id:4530894]:
*   **Probabilities and Utilities:** Parameters bounded between 0 and 1, such as probabilities and QALY utility weights, are best modeled using the **Beta distribution**. The Beta distribution is defined on the $(0,1)$ interval and is highly flexible in shape.
*   **Costs:** Healthcare costs are typically non-negative and often exhibit a right-[skewed distribution](@entry_id:175811) (a few patients incur very high costs). The **Gamma distribution** is an excellent choice as its domain is positive, it is naturally skewed, and its parameters can be easily derived from the mean and variance of observed data.

#### Illustrating Structural Uncertainty

Different structural assumptions can lead to vastly different conclusions, even when all input parameters are identical. Consider an analysis of a vaccine where one team uses a simple one-year decision tree that ignores minor adverse reactions, while another team uses a 10-year Markov model that explicitly includes a one-cycle **tunnel state** for adverse reactions in the first year [@problem_id:4531029]. A tunnel state is a temporary state that can be entered for a fixed duration (here, one cycle) before the individual must transition out. By including the costs and quality-of-life decrements associated with the adverse reaction, the second team's more complex structure might find the vaccine to be more costly and less effective than the first team's simpler model, potentially flipping the conclusion from cost-effective to not cost-effective. This demonstrates that structural uncertainty is not a technicality but a powerful driver of model results that must be carefully considered and justified.