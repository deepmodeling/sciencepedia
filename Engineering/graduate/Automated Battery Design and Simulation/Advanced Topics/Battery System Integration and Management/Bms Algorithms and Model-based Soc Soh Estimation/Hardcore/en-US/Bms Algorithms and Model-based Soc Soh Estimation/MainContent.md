## Introduction
Accurate estimation of a battery's State of Charge (SOC) and State of Health (SOH) is fundamental to the safety, performance, and longevity of systems from electric vehicles to [grid-scale energy storage](@entry_id:276991). While simple methods like Coulomb counting exist, they are insufficient to capture the complex, dynamic, and degrading nature of [electrochemical cells](@entry_id:200358). This creates a critical need for robust, [model-based estimation](@entry_id:1128001) algorithms that can provide reliable insights into the battery's internal state in real-time. This article provides a comprehensive exploration of these advanced methods. The journey begins in the "Principles and Mechanisms" chapter, where we establish rigorous definitions for SOC and SOH, construct the Equivalent Circuit Models (ECMs) that form the bedrock of these algorithms, and delve into the filtering techniques used for online estimation. We will then bridge theory and practice in the "Applications and Interdisciplinary Connections" chapter, demonstrating how these core estimates enable everything from power prediction and [safety assurance](@entry_id:1131169) to [distributed control](@entry_id:167172) in large battery packs and fleet-wide data analytics. Finally, the "Hands-On Practices" chapter offers an opportunity to solidify this knowledge by tackling practical implementation challenges.

## Principles and Mechanisms

This chapter delves into the foundational principles and mechanisms that underpin modern model-based algorithms for estimating a battery's State of Charge (SOC) and State of Health (SOH). We will begin by establishing rigorous definitions for these crucial states. Subsequently, we will explore the construction and physical interpretation of the Equivalent Circuit Models (ECMs) that form the core of these algorithms. Finally, we will examine the methods of [system identification](@entry_id:201290) and online filtering used to extract parameter information and track the battery's state in real time, paying close attention to the practical challenges of identifiability, [observability](@entry_id:152062), and sensor imperfections.

### Fundamental State Definitions: SOC and SOH

At the heart of any Battery Management System (BMS) are the concepts of State of Charge and State of Health. While intuitively understood as "how full" and "how old" the battery is, their precise, quantitative definitions are critical for the design of [robust estimation](@entry_id:261282) algorithms.

#### State of Charge (SOC)

The most common and fundamental definition of SOC is based on the accounting of electrical charge. The **charge-based SOC**, denoted as $z(t)$, is defined as the ratio of the remaining extractable charge to the battery's nominal capacity:

$$
z(t) = \frac{Q(t)}{Q_{\mathrm{nom}}}
$$

Here, $Q(t)$ is the available charge at time $t$, and $Q_{\mathrm{nom}}$ is the nominal capacity, typically determined under specific reference conditions (e.g., low-rate discharge at a set temperature). The dynamics of SOC are governed by **Coulomb counting**, which integrates the current over time. Assuming unity coulombic efficiency and negligible self-discharge, the rate of change of charge is directly proportional to the current $I(t)$ (with the convention that $I(t) > 0$ for discharge):

$$
\frac{dQ}{dt} = -I(t)
$$

This leads to the familiar differential equation for SOC: $\dot{z}(t) = -I(t)/Q_{\mathrm{nom}}$.

An alternative perspective is to consider the battery's energy content. An **energy-based SOC**, let's call it $z_E(t)$, can be defined as the ratio of the remaining reversible electrochemical energy $E(t)$ to the nominal energy capacity $E_{\mathrm{nom}}$:

$$
z_E(t) = \frac{E(t)}{E_{\mathrm{nom}}}
$$

Under ideal, reversible conditions, the change in energy is related to charge $q$ and the Open-Circuit Voltage (OCV), $V_{\mathrm{OC}}(q)$, by $dE = V_{\mathrm{OC}}(q) dq$. This allows us to express the energy as an integral of the OCV. A critical question then arises: are these two definitions of SOC equivalent? 

To explore this, we can write the condition for their equivalence, $z(t) = z_E(t)$, as:

$$
\frac{Q(t)}{Q_{\mathrm{nom}}} = \frac{\int_{0}^{Q(t)} V_{\mathrm{OC}}(q)\\,dq}{\int_{0}^{Q_{\mathrm{nom}}} V_{\mathrm{OC}}(q)\\,dq}
$$

For this identity to hold for all possible values of $Q(t)$ in the range $[0, Q_{\mathrm{nom}}]$, a rigorous [mathematical analysis](@entry_id:139664) reveals that the Open-Circuit Voltage, $V_{\mathrm{OC}}(q)$, must be a constant value, independent of the amount of charge $q$. Real-world batteries, however, exhibit a characteristic OCV curve that varies significantly with SOC. For example, lithium-ion chemistries like NMC (Nickel Manganese Cobalt) have a sloped profile, while LFP (Lithium Iron Phosphate) has a very flat profile over a wide SOC range, but neither is perfectly constant. Consequently, charge-based SOC and energy-based SOC are not interchangeable. While energy content is often the ultimate quantity of interest for an application, the charge-based SOC, governed by the simple and direct principle of Coulomb counting, serves as the fundamental and more practical state variable for estimation algorithms.

#### State of Health (SOH)

Unlike SOC, State of Health is not a single, universally defined state. It is a multidimensional concept that quantifies the extent of battery degradation relative to its fresh, beginning-of-life (BOL) condition. This degradation manifests as a collection of physical changes, most notably **capacity fade** (a reduction in the total charge the battery can store) and **internal resistance growth** (an increase in the opposition to current flow).

For [model-based estimation](@entry_id:1128001), it is therefore most natural to represent SOH not as a single scalar, but as a vector of physically meaningful parameters that are tracked over the battery's lifetime. A common and effective choice for this **SOH vector**, $\theta_{\mathrm{SOH}}$, is:

$$
\theta_{\mathrm{SOH}} = \begin{pmatrix} Q_{\mathrm{max}} \\ R_{\mathrm{int}} \end{pmatrix}
$$

Here, $Q_{\mathrm{max}}$ represents the current maximum usable capacity, which decreases from its nominal value $Q_{\mathrm{nom}}$ as the battery ages. $R_{\mathrm{int}}$ is the internal resistance, which increases from its initial value $R_{\mathrm{int},0}$. These two parameters directly impact performance: a lower $Q_{\mathrm{max}}$ reduces runtime, and a higher $R_{\mathrm{int}}$ reduces power capability and efficiency due to increased voltage drop and heat generation ($I^2R_{\mathrm{int}}$ losses).

While this vector representation is ideal for internal tracking within the BMS, a single, scalar indicator is often required for reporting and for making an End-of-Life (EOL) decision. Industry practice often defines EOL when either capacity fades below a certain threshold (e.g., $80\%$ of nominal) or resistance increases above a threshold (e.g., by $30\%$ from BOL). A crucial requirement for a scalar EOL indicator is that it must reflect this "weakest link" behavior; a battery is considered at EOL if *either* criterion is met, and good performance in one metric should not compensate for failure in another.

Consider the challenge of creating a unitless scalar indicator $s(\theta_{\mathrm{SOH}})$ that captures this logic, with an EOL rule like "declare EOL if $s \ge 1$". A simple summation of normalized degradation, such as summing the percentage of capacity fade and resistance growth, is flawed because it allows for compensation. A mathematically sound and robust mapping that prevents compensation uses the `max` function . For instance, given a $20\%$ [capacity fade](@entry_id:1122046) limit and a $30\%$ resistance growth limit, the indicator can be defined as:

$$
s(\theta_{\mathrm{SOH}}) = \max \left\{ \frac{Q_{\mathrm{nom}} - Q_{\mathrm{max}}}{0.20 \cdot Q_{\mathrm{nom}}}, \frac{R_{\mathrm{int}} - R_{\mathrm{int},0}}{0.30 \cdot R_{\mathrm{int},0}} \right\}
$$

With this definition, the EOL condition $s \ge 1$ is triggered if the normalized [capacity fade](@entry_id:1122046) term exceeds $1$ *or* if the normalized resistance growth term exceeds $1$. This `max` operator correctly implements the logical "OR" condition required for a non-compensating EOL criterion, providing a direct and interpretable link between the physically estimated SOH parameters and the high-level health status of the battery.

### Model-Based Estimation: The Equivalent Circuit Model (ECM)

Model-based estimation relies on a mathematical representation of the battery's electrical behavior. The most widely used models in commercial BMS are Equivalent Circuit Models (ECMs), which use a combination of ideal circuit elements to emulate the battery's voltage response to a current input.

#### The Structure of ECMs

A typical ECM consists of three main parts connected in series:
1.  A **voltage source** representing the Open-Circuit Voltage, $\mathrm{OCV}(z(t))$, which captures the battery's equilibrium potential as a function of SOC.
2.  An **ohmic resistor**, $R_0$, which models the instantaneous voltage drop due to the bulk resistance of electrodes, electrolyte, and current collectors.
3.  One or more parallel **Resistor-Capacitor (RC) pairs**. Each RC pair is intended to model a different transient process, such as [charge transfer kinetics](@entry_id:1122307) at the [electrode-electrolyte interface](@entry_id:267344) or [mass transport](@entry_id:151908) (diffusion) of lithium ions.

The terminal voltage $V(t)$ of an ECM with $m$ RC branches is given by:

$$
V(t) = \mathrm{OCV}(z(t)) - R_0 I(t) - \sum_{k=1}^{m} V_k(t)
$$

where $V_k(t)$ is the voltage across the $k$-th RC pair. The dynamics of each polarization voltage $V_k(t)$ are described by a first-order [linear differential equation](@entry_id:169062):

$$
\frac{dV_k(t)}{dt} = -\frac{1}{R_k C_k} V_k(t) + \frac{1}{C_k} I(t)
$$

The product $\tau_k = R_k C_k$ is the **time constant** of the $k$-th branch, which characterizes the speed of the relaxation process it represents.

#### Physical Interpretation and Model Order Selection

The choice of the number of RC pairs, known as the model order, is a critical design decision. A model with too few pairs may fail to capture the complex dynamics of the battery, leading to inaccurate SOC and SOH estimates. A model with too many pairs can be computationally expensive and may overfit the data, leading to poor generalization.

The choice of model order can often be guided by the underlying physics. In lithium-ion batteries, there are typically at least two dominant, separable transient processes: a fast process related to [charge transfer](@entry_id:150374) and double-layer capacitance at the electrode surfaces, and a much slower process related to solid-state diffusion of lithium within the active material particles.

Consider an experiment where a battery's voltage relaxation is measured after a current pulse . Suppose the relaxation is well-described by two decaying exponentials with time constants $\hat{\tau}_f \approx 0.4\,\mathrm{s}$ and $\hat{\tau}_s \approx 80\,\mathrm{s}$. We can compare these observed time scales to theoretical estimates derived from the battery's physical properties. The characteristic time for diffusion in the electrolyte across the separator (thickness $L_e$, diffusivity $D_e$) is approximately $\tau_e \sim L_e^2/(\pi^2 D_e)$, while the time for [solid-state diffusion](@entry_id:161559) in active material particles (radius $r_s$, diffusivity $D_s$) is approximately $\tau_s \sim r_s^2/(\pi^2 D_s)$. Using typical physical values ($L_e \approx 20\,\mu\mathrm{m}$, $D_e \approx 10^{-10}\,\mathrm{m^2/s}$, $r_s \approx 3\,\mu\mathrm{m}$, $D_s \approx 10^{-14}\,\mathrm{m^2/s}$), these formulas yield theoretical estimates of $\tau_e \approx 0.4\,\mathrm{s}$ and $\tau_s \approx 90\,\mathrm{s}$. The excellent agreement between the observed and theoretical time constants suggests that a **2RC model** is physically justified and necessary to capture these distinct processes. A 1RC model, having only one time constant, would be structurally inadequate and would conflate these two phenomena into a single, non-physical [effective time constant](@entry_id:201466).

While physical insight is invaluable, a more formal and data-driven approach to [model selection](@entry_id:155601) involves statistical information criteria. The **Akaike Information Criterion (AIC)** is a powerful tool for this purpose, as it provides a principled way to trade off goodness-of-fit with model complexity . Starting from the principle of maximum likelihood estimation under the assumption of Gaussian measurement noise, the AIC is defined as:

$$
\mathrm{AIC} = -2\ln(\hat{L}) + 2k
$$

where $\hat{L}$ is the maximized value of the [likelihood function](@entry_id:141927) for the model, and $k$ is the total number of parameters estimated from the data. For a least-squares fit with $n$ data points, this can be expressed in terms of the [residual sum of squares](@entry_id:637159) (RSS):

$$
\mathrm{AIC} \approx n \ln(\mathrm{RSS}) + 2k
$$

The first term, $n \ln(\mathrm{RSS})$, rewards [goodness-of-fit](@entry_id:176037) (a lower RSS leads to a lower AIC). The second term, $2k$, is a penalty for complexity. The model with the lowest AIC is preferred. It is crucial to correctly count all parameters estimated from the data. For an ECM, this includes not only the physical parameters ($R_0, R_k, C_k$) but also any unknown initial conditions (e.g., initial capacitor voltages $V_k(0)$) and the variance of the measurement noise, $\sigma^2$. Each of these adds a degree of freedom that could contribute to overfitting, and the AIC penalty term correctly accounts for them.

#### The Open-Circuit Voltage (OCV) and Hysteresis

The OCV term, $\mathrm{OCV}(z)$, is the largest and most significant component of the voltage model. Its accurate characterization is paramount for accurate SOC estimation. The OCV-SOC relationship is typically determined by performing a quasi-static experiment, where the battery is charged or discharged at a very low rate, with long rest periods to allow the voltage to settle to its equilibrium value.

However, a significant challenge arises because the internal states of the battery, such as concentration gradients, may take a very long time to fully relax. Measuring the voltage after a finite rest period can lead to a biased estimate of the true OCV, as the measured voltage still contains a residual polarization component . A naive approach of simply taking the voltage at the end of each rest period can result in an inaccurate OCV curve.

A more rigorous, model-based approach is to treat the OCV estimation as a [system identification](@entry_id:201290) problem. This involves using the full dynamic model, including the polarization dynamics. By fitting the model to the entire dataset (both current pulses and rest periods), a state estimator (such as a Kalman smoother) can be used to estimate the time-varying polarization voltage $V_{pol}(t) = \sum V_k(t)$. The OCV can then be isolated by subtracting all other modeled voltage components from the measurement:

$$
\mathrm{OCV}(z(t))_{\text{est}} = V(t) - I(t)R_0 - V_{pol}(t)
$$

This "de-polarized" voltage, paired with the estimated SOC, yields an unbiased set of points from which a smooth and accurate OCV curve can be constructed.

A further complication, particularly prominent in chemistries like LFP, is **OCV hysteresis**: the OCV curve during charging is slightly higher than the curve during discharging. This is a rate-independent phenomenon related to the thermodynamics of [phase transformations](@entry_id:200819) within the active materials. Two main approaches exist to model this behavior :

1.  **Dynamic State Approach (Plett Model):** This approach adds a hysteresis state variable, $h$, to the model, which evolves dynamically based on the current. The OCV is then modeled as $V_{OCV}(z) + h$. The dynamic nature of $h$ means this model captures rate-dependent hysteresis effects observed in experiments. Its smooth, [differential form](@entry_id:174025) makes it easy to integrate into state estimators like the Extended Kalman Filter (EKF).

2.  **Preisach-Inspired Models:** These models represent hysteresis as a weighted sum of many simple, rate-independent "hysteron" elements (like ideal relays). This approach excels at capturing complex memory effects observed in quasi-static tests, such as the closure of minor loops and the "wiping-out" property. However, the identification of the model's density function is an [ill-posed inverse problem](@entry_id:901223) requiring regularization, and the non-differentiable nature of the ideal hysteron operators makes them challenging to use with standard EKFs, often requiring alternative filters like the Unscented Kalman Filter (UKF).

The choice between these models depends on the specific application, the battery chemistry, and the available characterization data. The dynamic model is often favored for its simplicity and ease of implementation in online applications, while Preisach models are powerful tools for high-fidelity offline analysis and simulation.

### Parameter and State Estimation: System Identification and Filtering

Once a model structure is chosen, its parameters must be determined, and it must be implemented in a filter to track the states online.

#### Parameter Identification (Offline)

The process of determining the values of the ECM parameters ($R_0, R_k, C_k$) from experimental data is a [system identification](@entry_id:201290) problem. This is typically formulated as an optimization problem where the goal is to find the parameter values that minimize the error between the model's predicted voltage and the measured voltage.

A powerful technique for this is **separable nonlinear least-squares** . The problem is nonlinear because the voltage response depends nonlinearly on the time constants $\tau_k = R_k C_k$. However, for a *given* set of time constants, the problem becomes linear in the resistances $R_k$. This structure can be exploited by nesting a linear least-squares fit for the resistances inside a nonlinear search for the time constants.

For a unique set of parameters to be identifiable from the data, two conditions are essential:
1.  **Structural Identifiability:** The model structure itself must not be ambiguous. For an ECM, this means that the time constants $\tau_k$ must all be distinct. If two time constants are identical, $\tau_i = \tau_j$, their corresponding RC branches respond to the current in the same way. It becomes impossible to distinguish the individual resistances $R_i$ and $R_j$; only their sum, $R_i + R_j$, can be identified . In the language of linear systems, this corresponds to having distinct poles in the system's transfer function .
2.  **Persistent Excitation:** The input current signal used for identification must be "sufficiently rich" to excite all the dynamic modes of the system. A constant current, for example, is not persistently exciting. After an initial transient, the system settles to a steady state, and no further information about the dynamic parameters (the RC pairs) can be extracted. The input must vary over time, containing a spectrum of frequencies that is rich enough to ensure that the [information matrix](@entry_id:750640) of the estimation problem is well-conditioned and invertible.

#### State and Parameter Estimation (Online)

While parameters are often identified offline, there is also interest in tracking them online to adapt to changes due to aging and temperature. This leads to **joint [state-parameter estimation](@entry_id:755361)**, typically implemented using an **augmented Extended Kalman Filter (EKF)**. The idea is to augment the state vector with the parameters to be estimated (e.g., $z_{aug} = [z, V_1, \dots, R_0, R_1, \dots]^T$) and assume they are constant or slowly varying (i.e., $\dot{R}_k=0$).

However, this approach faces a critical challenge: **[observability](@entry_id:152062)**. A system is observable if its internal states can be uniquely determined from its external outputs. For an augmented battery model, this means we must be able to distinguish changes in the states (like SOC) from changes in the parameters (like resistance) based solely on the voltage and current measurements.

A fundamental problem arises under non-exciting input conditions. Consider the joint estimation of just SOC ($z$) and the series resistance $R_0$ under a constant current $i_0$ . An error in the SOC estimate, $\delta z$, produces an error in the OCV term of approximately $E'(z) \delta z$, where $E'(z)$ is the slope of the OCV curve. An error in the resistance estimate, $\delta R_0$, produces an error in the voltage drop of $i_0 \delta R_0$. If these two errors happen to cancel each other out, i.e., $E'(z) \delta z - i_0 \delta R_0 = 0$, their combined effect on the measured voltage is zero. The filter has no way of knowing whether it has an error in SOC, an error in resistance, or both. The system is unobservable.

This problem becomes even more severe when attempting to estimate all parameters of a 2RC model online . Under constant current, the polarization voltages reach a steady state, and the capacitors act as open circuits. The voltage response provides no information about the capacitances ($C_1, C_2$), which become completely unobservable.

The scientifically sound solution to this pervasive issue is a **two-stage estimation strategy**.
1.  **Parameter Estimation Stage:** Identify data segments where the current is sufficiently exciting (e.g., during acceleration or deceleration events). Use these information-rich segments to perform a robust [parameter identification](@entry_id:275485), perhaps using a batch method or an augmented EKF that is run only on this data.
2.  **State Estimation Stage:** During normal operation, especially under low-excitation conditions, freeze the parameter values at their most recently updated estimates. Run a simpler, more robust state-only EKF to track SOC. This avoids the [observability](@entry_id:152062) issues and instability associated with trying to update parameters with uninformative data. This two-stage approach combines the benefits of adaptability with the robustness required for a safety-critical system.

#### Practical Challenges: Sensor Bias

The theoretical models we have discussed assume perfect measurements. In reality, sensors have imperfections, such as noise and bias. A constant voltage sensor bias, $b_v$, can be particularly insidious for SOH estimation . If SOH is inferred from the estimated series resistance $R_0$, a voltage bias can be misinterpreted as a change in resistance, leading to an incorrect diagnosis of the battery's health.

The impact of this bias depends on the estimation method.
-   **Current-Step Method:** If $R_0$ is estimated by measuring the instantaneous voltage jump $\Delta V$ in response to a current step $\Delta I$, the estimate is $\hat{R}_0 = -\Delta V / \Delta I$. Since the constant bias $b_v$ is present both before and after the step, it cancels out in the difference $\Delta V$. This method is therefore inherently **robust** to constant sensor bias.
-   **Regression-Based Method:** If $R_0$ is estimated using a regression fit over a period of time, the bias must be handled explicitly. If a model like $y_k \approx -R_0 i_k$ is used (forcing a zero intercept), the bias $b_v$ will be absorbed into the estimate of $R_0$, leading to a biased and incorrect SOH assessment.

To overcome this, the bias $b_v$ must be treated as another unknown parameter to be estimated jointly with $R_0$. The model becomes a [linear regression](@entry_id:142318) with an intercept term: $y_k \approx b_v - R_0 i_k$. For both the intercept ($b_v$) and the slope ($-R_0$) to be uniquely identifiable, the regressor data (the current $i_k$) cannot be constant. This is the same **[persistent excitation](@entry_id:263834)** condition we encountered earlier: the current must take on at least two distinct values to allow for the unique determination of both parameters. This underscores a recurring theme: the quality and richness of the input signal are just as important as the sophistication of the model and the filter for achieving accurate and reliable [battery state estimation](@entry_id:1121447).