## Introduction
Modern embedded and cyber-physical systems are increasingly consolidating functions of varying importance onto shared hardware platforms to save cost, weight, and power. This trend creates a fundamental conflict: safety-critical functions demand verifiable, [deterministic timing](@entry_id:174241) guarantees, which often leads to significant resource over-provisioning, while less critical functions could benefit from using the otherwise idle resources. Traditional [real-time scheduling](@entry_id:754136), which relies on a single, highly pessimistic Worst-Case Execution Time (WCET) for every task, fails to navigate this trade-off efficiently. Mixed-Criticality Scheduling (MCS) emerges as a structured theoretical framework designed to resolve this very problem, enabling the creation of systems that are both certifiably safe and highly resource-efficient.

This article provides a comprehensive exploration of Mixed-Criticality Real-time Scheduling, bridging theory and practice. You will learn how MCS provides a formal basis for building dependable systems that can adapt their behavior based on runtime conditions. The following chapters will guide you through the foundational concepts, real-world applications, and practical analysis techniques. The first chapter, **Principles and Mechanisms**, will introduce the formal mixed-criticality task model, explain the rationale behind multiple WCET estimates, and detail the critical mode-switching mechanism that underpins the entire framework. Subsequently, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these principles are applied to design complex Cyber-Physical Systems, distributed architectures, and integrate with technologies like real-time networking and [power management](@entry_id:753652). Finally, the **Hands-On Practices** chapter will provide a set of guided problems, allowing you to apply [schedulability analysis](@entry_id:754563) and design algorithms for mixed-criticality systems.

## Principles and Mechanisms

The design of certifiably dependable [real-time systems](@entry_id:754137) that integrate functionalities of varying importance onto a shared hardware platform presents a fundamental conflict between [safety assurance](@entry_id:1131169) and resource efficiency. Traditional [real-time scheduling](@entry_id:754136) theory often relies on a single, highly conservative Worst-Case Execution Time (WCET) for each task to provide deterministic guarantees. While this approach ensures safety, it can lead to systems that are significantly over-provisioned and underutilized, as the absolute worst-case scenario is typically rare. Mixed-Criticality Scheduling (MCS) offers a structured and verifiable framework to resolve this conflict by formally incorporating different levels of assurance into the system's design and runtime behavior. This chapter elucidates the core principles of the mixed-criticality model and the mechanisms that enable its implementation.

### The Formal Model of Mixed-Criticality Systems

The departure from traditional [real-time scheduling](@entry_id:754136) begins with a more nuanced task model that explicitly acknowledges the role of certification and evidence in defining timing properties.

#### The Challenge of Certification and Efficiency

Safety-critical functions, such as flight control in an aerial vehicle or motor control in a robotic arm, must undergo rigorous certification by regulatory authorities (e.g., DO-178C in avionics, ISO 26262 in automotive). Certification demands high-confidence evidence that timing deadlines will always be met. This evidence often compels engineers to use extremely pessimistic WCET estimates derived from conservative [static analysis](@entry_id:755368) tools. In contrast, less critical functions, like telemetry or diagnostic logging, may be verified using lower-confidence evidence, such as measurements from extensive testing, which yield smaller and more typical WCET estimates.

A system that provisions resources based on the pessimistic, high-assurance WCET for all its functions would be certifiably safe but potentially wasteful. The central innovation of mixed-criticality theory is to create a system that is sized for the more typical, optimistic case, while retaining a certified contingency plan for the rare, pessimistic case.

#### The Mixed-Criticality Task Model

The Vestal model, a foundational framework for MCS, extends the classic real-time task model. A mixed-criticality system is composed of a set of sporadic tasks, $\{\tau_i\}$. Each task is defined by a tuple that includes its timing properties and its criticality level . For a dual-criticality system, the most common type, this is represented as:

$\tau_i : (L_i, T_i, D_i, \{C_i(\mathrm{LO}), C_i(\mathrm{HI})\})$

*   $L_i \in \{\mathrm{LO}, \mathrm{HI}\}$ is the **criticality level** of the task. A high-criticality (HI) task, such as a flight stabilization loop, is one whose failure could have catastrophic consequences. A low-criticality (LO) task is one whose failure is tolerable. This level maps directly to the assurance requirements of certification standards .

*   $T_i$ is the **minimum inter-arrival time**, also known as the period for sporadic tasks. It specifies the minimum duration between the release of consecutive jobs of task $\tau_i$.

*   $D_i$ is the **relative deadline**. Each job released by $\tau_i$ must complete its execution within $D_i$ time units of its release. A key distinction exists based on this parameter :
    *   **Implicit-deadline tasks**: These have $D_i = T_i$. This is common in control systems where the output of one job is needed before the start of the next.
    *   **Constrained-deadline tasks**: These have $D_i \le T_i$. Such tasks require completion well before the next job arrives. As we will see, constrained deadlines can create a higher "density" of computational demand over short intervals, making [schedulability analysis](@entry_id:754563) more complex than for implicit-deadline systems.

*   $\{C_i(\mathrm{LO}), C_i(\mathrm{HI})\}$ is a set of **Worst-Case Execution Time (WCET) estimates**.
    *   $C_i(\mathrm{LO})$ is the low-assurance WCET, representing the execution time bound under normal, less pessimistic assumptions. For LO-criticality tasks, this is the only WCET specified.
    *   $C_i(\mathrm{HI})$ is the high-assurance WCET for HI-criticality tasks, representing a more conservative bound credible under stricter certification evidence.

#### The Epistemology of Worst-Case Execution Time

The existence of multiple WCET values for a single task is not an arbitrary modeling choice; it is a direct consequence of the relationship between evidence, confidence, and assurance in safety-critical systems .

The value of a WCET is an **epistemic claim**—a claim about what can be known and justified with evidence—rather than an absolute physical property of the task. A lower-assurance WCET, $C_i(\mathrm{LO})$, might be derived from measurement-based evidence, such as observing the maximum execution time over millions of test runs. A higher-assurance WCET, $C_i(\mathrm{HI})$, must be supported by stronger evidence, such as formal static analysis that accounts for rare hardware states, pipeline conflicts, and other timing anomalies that may not be observed in testing.

This leads to the fundamental **[monotonicity](@entry_id:143760) principle**: for any high-criticality task $\tau_i$, it must be that $C_i(\mathrm{HI}) \ge C_i(\mathrm{LO})$. The justification for this is mathematical . Let $\mathcal{X}_i^{\mathrm{LO}}$ be the set of execution circumstances (hardware states, input values, etc.) considered in the low-assurance analysis, and $\mathcal{X}_i^{\mathrm{HI}}$ be the set for the high-assurance analysis. Higher assurance requires greater conservatism, meaning the analysis must consider a superset of possible behaviors: $\mathcal{X}_i^{\mathrm{LO}} \subseteq \mathcal{X}_i^{\mathrm{HI}}$. The WCET is the [supremum](@entry_id:140512) ([least upper bound](@entry_id:142911)) of the execution time functional $T_i(x)$ over these sets. By the property of the [supremum](@entry_id:140512), it follows that:
$$ C_i(\mathrm{LO}) = \sup_{x \in \mathcal{X}_i^{\mathrm{LO}}} T_i(x) \le \sup_{x \in \mathcal{X}_i^{\mathrm{HI}}} T_i(x) = C_i(\mathrm{HI}) $$

The insufficiency of purely measurement-based evidence for high assurance can be demonstrated statistically . Suppose certification requires that the probability of a job's execution time exceeding $C_i(\mathrm{HI})$ be no more than $\varepsilon = 10^{-6}$ with $99\%$ confidence. A development team runs $n=1,000$ tests and observes zero exceedances of a measured maximum time $\hat{B}$. Proposing to set $C_i(\mathrm{HI}) = \hat{B}$ is not justifiable. Statistical analysis shows that observing zero exceedances in $1,000$ trials only provides $99\%$ confidence that the true probability of exceedance is less than or equal to approximately $4.6 \times 10^{-3}$, which is orders of magnitude higher than the required $10^{-6}$. This highlights the "epistemic uncertainty" from finite evidence and explains why $C_i(\mathrm{HI})$ must often come from conservative analytical methods, resulting in a larger value than $C_i(\mathrm{LO})$.

### The Operational Cycle: Mode Switching

The mixed-criticality task model enables a dynamic runtime strategy centered on **mode switching**. This mechanism allows the system to adapt its behavior and guarantees based on observed execution times.

#### The Two-Mode Operational Contract

The system operates under a two-part contract, corresponding to two system-wide modes :

1.  **Low-Criticality (LO) Mode**: This is the nominal, optimistic mode of operation. The system starts in this mode. The scheduler's contract is to guarantee that **all tasks** (both LO and HI) meet their deadlines, under the assumption that every task $\tau_i$ completes its execution within its low-assurance budget, $C_i(\mathrm{LO})$. Offline, a schedulability test must prove this is possible.

2.  **High-Criticality (HI) Mode**: This is the contingency, pessimistic mode. If any HI-criticality task, say $\tau_k$, has a job whose execution time exceeds its $C_k(\mathrm{LO})$ budget, the system's optimistic assumption is violated. A mode switch is triggered. In HI mode, the scheduler's contract changes dramatically: it is now only required to guarantee the deadlines of **HI-criticality tasks**, assuming they may execute up to their high-assurance budget, $C_i(\mathrm{HI})$. To secure the resources needed for this guarantee, all LO-criticality tasks may be degraded or dropped entirely.

This modal behavior allows the system to achieve high resource utilization in the common case (LO mode) while having a certified, safe fallback plan for the rare worst case (HI mode).

#### The Trigger: Execution Time Monitoring

A mode switch is not a random event; it is triggered by a precise monitoring mechanism . A safe and correct implementation requires careful accounting of processor time. The monitor must track the cumulative **execution time** of each job, which is the actual processor time consumed, excluding any time the job is preempted or blocked. It must not use wall-clock time since the job's release.

The ideal mechanism is an event-driven, per-job budget monitor. When a HI-criticality job is dispatched, the scheduler arms a high-resolution timer (e.g., a hardware performance counter) for a budget of $C_i(\mathrm{LO})$. If the job completes or is preempted before the timer expires, the timer is disarmed or adjusted. If the timer expires while the job is still running, it means the execution time has reached $C_i(\mathrm{LO})$. This event generates a synchronous exception or interrupt that immediately passes control to the scheduler. The scheduler then initiates the mode switch *before* any further instructions of the overrunning job are executed. This immediacy is critical for safety, as it prevents the system from operating in an uncertified state.

#### The Consequence: Guarantee Preservation and Load Shedding

The policy of suspending or degrading LO tasks upon a mode switch is not arbitrary; it is a necessary measure to uphold the certified guarantees of the HI-criticality tasks . This can be illustrated with a simple example. Consider a uniprocessor system with implicit deadlines scheduled by Earliest Deadline First (EDF), where schedulability requires total utilization $U \le 1$. Let the task set be:
*   HI task $\tau_1$: $T_1 = 20$, $C_1^{\mathrm{LO}} = 5$, $C_1^{\mathrm{HI}} = 9$.
*   HI task $\tau_2$: $T_2 = 25$, $C_2^{\mathrm{LO}} = 6$, $C_2^{\mathrm{HI}} = 10$.
*   LO task $\tau_3$: $T_3 = 10$, $C_3^{\mathrm{LO}} = 2$.
*   LO task $\tau_4$: $T_4 = 20$, $C_4^{\mathrm{LO}} = 3$.

In LO mode, the total utilization is:
$U^{\mathrm{LO}} = (\frac{5}{20} + \frac{6}{25}) + (\frac{2}{10} + \frac{3}{20}) = (0.25 + 0.24) + (0.20 + 0.15) = 0.49 + 0.35 = 0.84$.
Since $0.84 \le 1$, the system is schedulable in LO mode.

Now, suppose $\tau_1$ overruns its $C_1^{\mathrm{LO}}$ budget, triggering a switch to HI mode. The system must now provision for the HI-criticality WCETs. If we did not drop the LO tasks, the total utilization would become:
$U^{\mathrm{HI}} = (\frac{9}{20} + \frac{10}{25}) + (\frac{2}{10} + \frac{3}{20}) = (0.45 + 0.40) + 0.35 = 0.85 + 0.35 = 1.20$.
Since $1.20 > 1$, the system is overloaded. Deadline misses are inevitable. To ensure the HI tasks meet their deadlines, their combined utilization must be $\le 1$. The only way to achieve this is to shed the load from the LO tasks. By dropping $\tau_3$ and $\tau_4$, the utilization becomes $0.85$, which is schedulable. This shows that suspending LO tasks is a direct mathematical necessity for preserving HI-criticality guarantees.

#### Recovery: Returning to Low-Criticality Mode

A system cannot remain in the degraded HI mode indefinitely. A **recovery protocol** is needed to safely transition back to the fully functional LO mode . A simple but unsafe approach, like returning to LO mode as soon as the triggering job completes, is incorrect because other HI jobs may have been delayed and could also require their $C_i(\mathrm{HI})$ budgets.

A safe recovery protocol must wait until the system's state is no longer affected by the temporal overload caused by the mode switch. This occurs at the first time instant when the processor becomes idle with respect to the HI-criticality workload—a **HI-idle instant**. At this point, there are no pending HI-criticality jobs, so the past execution history is irrelevant.

Even at a HI-idle instant, it may not be safe to immediately revert to LO-mode assumptions. The reason for the original overrun might be persistent. A robust protocol may therefore re-admit LO tasks under a pessimistic schedulability condition, for instance, by checking that the system remains schedulable even if HI tasks continue to demand $C_i(\mathrm{HI})$. Only after a "probation period," during which all HI jobs are observed to complete within their $C_i(\mathrm{LO})$ budgets, would the system fully revert to nominal LO-mode operation.

### Scheduling Mechanisms for Mixed-Criticality

The principles of the MC model must be implemented by concrete [scheduling algorithms](@entry_id:262670). While many exist, a common and instructive approach involves adapting traditional schedulers like EDF.

#### The Virtual Deadline Approach (EDF-VD)

One significant challenge in a mode switch is handling the sudden increase in a HI-task's execution demand ($C_i(\mathrm{HI}) - C_i(\mathrm{LO})$) without missing its deadline. The **EDF with Virtual Deadlines (EDF-VD)** algorithm proactively prepares for this contingency .

The core idea is to modify the scheduling priorities of HI-criticality tasks during LO mode. Under EDF, priority is determined by the absolute deadline. EDF-VD assigns each HI-criticality task $\tau_i$ a **virtual deadline**, $D_i^{virt}$, that is shorter than its actual deadline, $D_i$. For example, one might set $D_i^{virt} = x \cdot D_i$ for some scaling factor $x  1$.

In LO mode, the scheduler uses the virtual deadlines for HI tasks and the actual deadlines for LO tasks. Since HI tasks have artificially shorter deadlines, they are granted higher priority and tend to execute earlier than they otherwise would. This early execution builds up a temporal safety margin. If a mode switch occurs, the scheduler abandons the virtual deadlines and reverts to using the actual, longer deadlines for the HI tasks. The temporal margin created by the early execution in LO mode now provides extra time to accommodate the increased execution demand ($C_i(\mathrm{HI})$) while still meeting the original deadline, $D_i$. This strategy effectively reserves processor capacity in LO mode to be used in HI mode, significantly improving the chances of a seamless and safe transition.