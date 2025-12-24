## Introduction
The ability to predict and control the time-dependent behavior of a nuclear reactor is paramount for its safe and efficient operation. At the heart of [reactor dynamics](@entry_id:1130674) lies a fundamental connection: the relationship between an induced change in the neutron chain reaction, known as **reactivity**, and the rate at which the reactor power evolves, characterized by the **reactor period**. Understanding this relationship quantitatively is not merely an academic exercise; it is essential for designing control systems, analyzing accident scenarios, and performing critical core measurements. This article bridges the gap between the cause ([reactivity insertion](@entry_id:1130664)) and effect (power change), providing a detailed exploration of the [period-reactivity relationship](@entry_id:1129520).

To build a comprehensive understanding, we will first delve into the **Principles and Mechanisms** that govern this dynamic behavior, starting from fundamental definitions and deriving the cornerstone inhour equation from the [point kinetics model](@entry_id:1129861). Subsequently, the section on **Applications and Interdisciplinary Connections** will demonstrate how these theoretical principles are put into practice for [reactor diagnostics](@entry_id:1130673), safety analysis, and control rod calibration, highlighting connections to thermal-hydraulics and [spatial dynamics](@entry_id:899296). Finally, **Hands-On Practices** will offer the opportunity to solidify these concepts through guided computational problems, moving from theory to practical application.

## Principles and Mechanisms

The temporal behavior of a nuclear reactor following a departure from its critical state is of paramount importance for both operational control and safety analysis. This behavior is fundamentally dictated by the relationship between the magnitude of the perturbation, quantified by **reactivity**, and the rate at which the neutron population changes, characterized by the **reactor period**. This chapter elucidates the principles and mechanisms that govern this critical relationship, beginning with fundamental definitions and culminating in an analysis of the spatial effects that modulate reactor response.

### Fundamental Concepts: Reactivity and Period

The state of a reactor's neutron chain reaction is described by the **effective multiplication factor**, $k_{\text{eff}}$, defined as the ratio of the number of neutrons produced in one generation to the number of neutrons lost (through absorption and leakage) in the preceding generation. A reactor is exactly critical when $k_{\text{eff}} = 1$, supercritical when $k_{\text{eff}} > 1$, and subcritical when $k_{\text{eff}}  1$.

While $k_{\text{eff}}$ describes the state, the quantitative cause of any change in the neutron population is the **reactivity**, denoted by the symbol $\rho$. Reactivity is formally defined as the fractional change in neutron population per generation, normalized by the total number of neutrons in the new generation. This definition leads to the exact relationship between reactivity and the multiplication factor :

$$
\rho = \frac{k_{\text{eff}} - 1}{k_{\text{eff}}}
$$

For states very close to critical, where $k_{\text{eff}} \approx 1$, it is common to use the approximation $\rho \approx k_{\text{eff}} - 1$. However, it is crucial to recognize that the relationship is fundamentally nonlinear. The reactivity "worth" of a given change in the multiplication factor, $\Delta k_{\text{eff}}$, depends on the state of the reactor. The change in reactivity, $\Delta\rho$, for a small change $\Delta k_{\text{eff}}$ is given by $\Delta\rho \approx \frac{\Delta k_{\text{eff}}}{k_{\text{eff}}^2}$. For instance, a change of $\Delta k_{\text{eff}} = +0.001$ from a [critical state](@entry_id:160700) ($k_{\text{eff}}=1$) results in a reactivity change of $\Delta\rho \approx +0.001$. However, if the same change of $\Delta k_{\text{eff}} = +0.001$ is introduced into a reactor already in a supercritical state of $k_{\text{eff}}=1.05$, the resulting reactivity change is smaller, approximately $\Delta\rho \approx \frac{0.001}{(1.05)^2} \approx +0.000907$ .

Reactivity is a dimensionless quantity, but it is often expressed in more convenient units. The **per cent mille (pcm)** is a common unit, where $1 \text{ pcm} = 10^{-5}$ in reactivity. Another physically significant unit is the **dollar ($)**, which is the reactivity normalized to the **effective delayed neutron fraction**, $\beta_{\text{eff}}$. That is, $\rho_{\$} = \rho / \beta_{\text{eff}}$. A reactivity of one dollar ($\rho = \beta_{\text{eff}}$) is a critical threshold in reactor dynamics, known as **[prompt critical](@entry_id:159881)**, which we will explore later in this chapter.

In response to a positive [reactivity insertion](@entry_id:1130664), the neutron population, and thus the reactor power, will begin to grow. After initial transients have subsided, the power level enters a phase of stable exponential growth, described by $n(t) \propto \exp(t/T)$, where $n(t)$ is the neutron population. The time constant $T$ in this expression is the **asymptotic reactor period**, defined as the e-folding time of the neutron population after all higher-order transient modes have decayed .

### The Role of Delayed Neutrons and the Point Kinetics Model

The time scale of reactor response is not governed by [prompt neutrons](@entry_id:161367) alone. A small fraction of neutrons are emitted following the [radioactive decay](@entry_id:142155) of fission products, known as **delayed neutrons**. While their fraction is small (typically less than 1%), their much longer time scales (seconds to minutes) compared to [prompt neutrons](@entry_id:161367) (microseconds to milliseconds) are what make reactor control feasible.

To model this behavior, we use the **[point kinetics](@entry_id:1129859) equations (PKE)**, which describe the time evolution of the spatially averaged neutron population, $n(t)$, and the concentrations of the various delayed neutron precursor groups, $C_i(t)$. The key parameters in this model are :
- The **prompt [neutron generation time](@entry_id:1128698)**, $\Lambda$, which is the average time between the birth of a prompt neutron and the fission it induces.
- The **delayed neutron fraction** for group $i$, $\beta_i$, which is the fraction of all fission neutrons born as delayed neutrons belonging to group $i$.
- The total delayed neutron fraction, $\beta = \sum_i \beta_i$.
- The **precursor decay constant** for group $i$, $\lambda_i$, where $1/\lambda_i$ is the [mean lifetime](@entry_id:273413) of that precursor.

For a constant reactivity $\rho$, the PKE form a system of coupled, linear, time-invariant (LTI) ordinary differential equations :
$$
\frac{dn(t)}{dt} = \frac{\rho - \beta}{\Lambda} n(t) + \sum_{i=1}^{M} \lambda_i C_i(t)
$$
$$
\frac{dC_i(t)}{dt} = \frac{\beta_i}{\Lambda} n(t) - \lambda_i C_i(t), \quad \text{for } i = 1, \dots, M
$$
The solution to such an LTI system is a [linear combination](@entry_id:155091) of exponential terms, $e^{\alpha_k t}$, where the $\alpha_k$ are the eigenvalues of the system's characteristic matrix. For a positive [reactivity insertion](@entry_id:1130664), one of these eigenvalues, $\alpha_0$, will be positive, while all others will be negative. As time progresses, the modes corresponding to the negative eigenvalues decay, and the long-term behavior of the system is dominated by the single growing exponential mode: $n(t) \propto e^{\alpha_0 t}$. This is the mathematical origin of the asymptotic [exponential response](@entry_id:269644), and the [asymptotic period](@entry_id:1121162) is simply $T = 1/\alpha_0$ .

### The Inhour Equation: Linking Reactivity and Period

By substituting the asymptotic solution form, $n(t) \propto e^{\alpha t}$ and $C_i(t) \propto e^{\alpha t}$, into the point kinetics equations, we can eliminate the precursor concentrations and derive a single characteristic equation that relates the reactivity $\rho$ to the inverse period $\alpha = 1/T$. This relationship is known as the **inhour equation**:

$$
\rho(\alpha) = \Lambda \alpha + \sum_{i=1}^{M} \frac{\alpha \beta_i}{\alpha + \lambda_i}
$$

This equation is the cornerstone of [reactor kinetics](@entry_id:160157). It can also be expressed in terms of the period $T$:

$$
\rho(T) = \frac{\Lambda}{T} + \sum_{i=1}^{M} \frac{\beta_i}{1 + \lambda_i T}
$$

The [inhour equation](@entry_id:1126513) provides a rich geometric interpretation of the [period-reactivity relationship](@entry_id:1129520) when we plot $\rho$ as a function of the inverse period $\alpha$ . The function $\rho(\alpha)$ is strictly increasing ($\frac{d\rho}{d\alpha} > 0$) and strictly concave downward ($\frac{d^2\rho}{d\alpha^2}  0$) for $\alpha > 0$. This means that for any positive reactivity, there is a unique, positive reactor period, and there are no [inflection points](@entry_id:144929) in the curve.
- In the limit of very long periods ($\alpha \to 0^+$), the curve is approximately linear, with a slope given by $\frac{d\rho}{d\alpha}|_{\alpha=0} = \Lambda + \sum_i \beta_i/\lambda_i$. This slope is often called the effective [neutron lifetime](@entry_id:159692).
- In the limit of very short periods ($\alpha \to \infty$), the contribution from the delayed neutron terms approaches a constant, $\sum_i \beta_i = \beta$. The curve becomes asymptotic to the straight line $\rho \approx \beta + \Lambda \alpha$, which describes the behavior of a system driven only by [prompt neutrons](@entry_id:161367).
- The presence of multiple delayed neutron groups, each with a different decay constant $\lambda_i$, causes the curve to exhibit several "knees." Each group's contribution to the reactivity transitions from being proportional to $\alpha$ (for $\alpha \ll \lambda_i$) to being constant (for $\alpha \gg \lambda_i$), and these transitions at different scales give the inhour curve its characteristic shape.

### Reactor Dynamics in Different Reactivity Regimes

The inhour equation reveals that reactor dynamics are qualitatively different depending on the magnitude of the inserted reactivity relative to the delayed neutron fraction.

#### Delayed Supercritical Regime ($0  \rho  \beta$)
In this regime, reactivity insertions are small. The resulting reactor period is relatively long (seconds to minutes), making the inverse period $\alpha$ small. Consequently, the prompt neutron term in the [inhour equation](@entry_id:1126513), $\Lambda \alpha$, is typically negligible compared to the delayed neutron terms. The relationship is well approximated by :

$$
\rho \approx \sum_{i=1}^{M} \frac{\alpha \beta_i}{\alpha + \lambda_i}
$$

The reactor's response is paced by the time constants of the delayed neutron precursors. For example, for a reactor with $\beta_{\text{eff}}=0.0065$, $\Lambda=1.0 \times 10^{-5} \text{ s}$, and a single effective delayed group with $\lambda_d=0.08 \text{ s}^{-1}$, a [reactivity insertion](@entry_id:1130664) corresponding to $k_{\text{eff}}=1.0025$ (where $\rho \approx 0.0025$) yields a stable [asymptotic period](@entry_id:1121162) of about $20$ seconds .

#### Prompt Critical Regime ($\rho = \beta$)
This is the critical threshold where the reactor can sustain a chain reaction on prompt neutrons alone. At this point, the [inhour equation](@entry_id:1126513) still yields a single, finite, positive root for $\alpha$. Contrary to some misconceptions, there is no mathematical singularity or root [multiplicity](@entry_id:136466) at $\rho=\beta$; it is simply the point where the [asymptotic behavior](@entry_id:160836) transitions dramatically . The [principal root](@entry_id:164411) $\alpha_0$ at prompt critical is approximately $\alpha_0 \approx \sqrt{(\sum \beta_i \lambda_i) / \Lambda}$.

#### Prompt Supercritical Regime ($\rho > \beta$)
When reactivity exceeds the total [delayed neutron fraction](@entry_id:158691), the reactor is **prompt supercritical**. The chain reaction grows so rapidly that the delayed neutron precursors do not have time to respond and contribute significantly to the rate of power change. In this regime, the period becomes extremely short, and the inverse period $\alpha$ becomes very large ($\alpha \gg \max_i(\lambda_i)$). The inhour equation simplifies significantly :

$$
\rho \approx \Lambda \alpha + \sum_{i=1}^{M} \frac{\alpha \beta_i}{\alpha + \lambda_i} \approx \Lambda \alpha + \beta
$$

This leads to the famous **[prompt jump approximation](@entry_id:1130232)** for the inverse period:

$$
\alpha \approx \frac{\rho - \beta}{\Lambda}
$$

The reactor period, $T = 1/\alpha$, is now directly proportional to the prompt [neutron generation time](@entry_id:1128698) $\Lambda$ and inversely proportional to the [reactivity insertion](@entry_id:1130664) above prompt critical. Because $\Lambda$ is extremely small, periods in this regime are in the sub-second range, leading to dangerously rapid power excursions.

### Sensitivity Analysis and Practical Measurement

The [inhour equation](@entry_id:1126513) forms the basis for measuring reactivity in an operating reactor. By observing the stable reactor period $T$ following a control rod movement, one can infer the reactivity change that was introduced. The sensitivity of this measurement is related to the derivative $d\rho/dT$ . Differentiating the inhour equation gives:

$$
\frac{d\rho}{dT} = -\frac{\Lambda}{T^2} - \sum_{i=1}^{M} \frac{\lambda_i \beta_i}{(1 + \lambda_i T)^2}
$$

Since all parameters are positive, $d\rho/dT$ is always negative, confirming that a positive [reactivity insertion](@entry_id:1130664) leads to a shorter (more positive) period. The sensitivity of the period to a change in reactivity is given by the inverse, $\frac{dT}{d\rho}$. The magnitude of this sensitivity varies strongly with the period itself.
- For **very short periods** (e.g., $T=0.05$ s), $|d\rho/dT|$ is large. This means a significant change in reactivity is required to produce a noticeable change in the period.
- For **very long periods** (e.g., $T=20$ s), $|d\rho/dT|$ is much smaller. The reactor is highly sensitive, and a very small [reactivity insertion](@entry_id:1130664) of $+50$ pcm can shorten the period by several seconds . This high sensitivity makes period meters effective instruments for monitoring reactivity near critical.

### Beyond the Point Kinetics Model: Spatial Effects

The [point kinetics model](@entry_id:1129861), while powerful, assumes the neutron flux shape is constant in time. In reality, the flux distribution $\phi(\mathbf{r},t)$ evolves. A full space-time description of [reactor kinetics](@entry_id:160157) reveals that the system's response is a superposition of **spatial-temporal eigenmodes**, often called $\alpha$-modes . Each mode has a characteristic spatial shape (a **spatial harmonic**) and a corresponding eigenvalue $\alpha_n$ that determines its [exponential time](@entry_id:142418) constant.

Higher spatial harmonics possess greater curvature, which leads to increased neutron leakage. This loss of neutrons makes these modes inherently less reactive, resulting in algebraically smaller eigenvalues ($\text{Re}(\alpha_n)  \text{Re}(\alpha_0)$ for $n>0$). Consequently, following a perturbation, these higher modes decay more rapidly, and the long-term, [asymptotic behavior](@entry_id:160836) is always dominated by the [fundamental mode](@entry_id:165201) ($n=0$). This fundamental dominance is why the concept of a single asymptotic reactor period is valid and why the [point kinetics model](@entry_id:1129861) is often a good approximation, especially for whole-core measurements  .

However, during the initial phase of a transient, especially one induced by a localized perturbation, these higher modes can be significantly excited. The measured power trace is a superposition of all active modes, and an "instantaneous effective period" $T_{\text{eff}}(t) = (\frac{d}{dt}\ln P(t))^{-1}$ will vary with time before settling to the asymptotic value $T$ .

Furthermore, in a reactor with a spatially varying composition, changes in the flux shape can alter the effective kinetic parameters themselves. The [effective delayed neutron fraction](@entry_id:1124177), $\beta_{\text{eff}}$, must be defined by weighting the local delayed fraction $\beta(\mathbf{r})$ with the fission rate and the **adjoint flux** (or neutron importance) $\psi^\dagger(\mathbf{r})$ .

$$
\beta_{\text{eff}} = \frac{\int \psi^\dagger(\mathbf{r}) \beta(\mathbf{r}) \nu\Sigma_f(\mathbf{r}) \phi(\mathbf{r}) \, dV}{\int \psi^\dagger(\mathbf{r}) \nu\Sigma_f(\mathbf{r}) \phi(\mathbf{r}) \, dV}
$$

Consider a reactor with a ${}^{235}\text{U}$-rich region (higher $\beta$) and a plutonium-rich region (lower $\beta$). If a control action causes the flux to shift or "tilt" towards the plutonium region, the importance-weighted average gives more weight to the smaller local $\beta$. The result is a decrease in the overall effective delayed fraction, $\beta_{\text{eff}}$. For the same physical [reactivity insertion](@entry_id:1130664), this smaller $\beta_{\text{eff}}$ means the reactivity in dollars is now higher, placing the reactor closer to prompt critical. The reactor will respond more quickly, exhibiting a shorter period than would be predicted by a [point kinetics model](@entry_id:1129861) that assumes a constant $\beta_{\text{eff}}$ . This illustrates a crucial limitation of simple models and highlights the complex interplay between spatial and temporal dynamics in reactor physics.