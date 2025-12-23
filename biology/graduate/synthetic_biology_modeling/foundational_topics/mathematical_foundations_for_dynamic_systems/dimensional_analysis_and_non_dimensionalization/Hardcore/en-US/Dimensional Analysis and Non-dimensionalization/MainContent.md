## Introduction
In the quantitative sciences, particularly in fields like synthetic biology and engineering, mathematical models are essential tools for understanding complex systems. However, these models often come with a bewildering array of parameters, each with its own physical units, making analysis, simulation, and interpretation a formidable task. This complexity obscures the fundamental principles governing a system's behavior and hinders the development of universal design rules. The central challenge addressed in this article is how to systematically simplify these models to reveal their essential dynamics.

This article introduces [dimensional analysis](@entry_id:140259) and non-dimensionalization as a powerful methodology to overcome this challenge. By mastering these techniques, you will learn to transform complex, parameter-rich equations into elegant, dimensionless forms that are easier to analyze and offer deeper physical insight. Across the following sections, we will embark on a comprehensive journey. First, in **"Principles and Mechanisms,"** we will establish the foundational concepts, from [dimensional homogeneity](@entry_id:143574) to the systematic Buckingham π theorem. Next, **"Applications and Interdisciplinary Connections"** will showcase how these principles are applied to simplify models, identify critical thresholds, and quantify competing processes in fields ranging from epidemiology to [transport phenomena](@entry_id:147655). Finally, **"Hands-On Practices"** will provide you with the opportunity to apply these techniques to solve practical modeling problems, solidifying your understanding and building your analytical skills.

## Principles and Mechanisms

### Foundational Concepts: Dimensions, Units, and Dimensional Homogeneity

At the core of all quantitative science is the measurement of physical quantities. Understanding the distinction between the fundamental nature of a quantity and the conventional scale used to measure it is the first step toward mastering dimensional analysis.

#### Physical Dimensions versus Units

A **physical dimension** is a fundamental property of a physical quantity that describes how it relates to a set of chosen base quantities, such as mass ($M$), length ($L$), time ($T$), temperature ($\Theta$), and [amount of substance](@entry_id:145418) ($N$). For example, velocity is defined as the rate of change of position with time, so its dimension is length divided by time, denoted as $L T^{-1}$. This dimensional representation is universal and independent of any measurement system.

In contrast, a **unit** is a specific, conventional standard used to assign a numerical value to a physical quantity. For a quantity with the dimension of length, units such as the meter ($\mathrm{m}$), kilometer ($\mathrm{km}$), or foot ($\mathrm{ft}$) can be used. Two quantities can share the same dimension while being expressed in different units. For instance, in hydrological modeling, a precipitation rate is often given in units of millimeters per day ($\mathrm{mm\,day^{-1}}$). This is a measure of depth (a length) per unit time. Its fundamental dimension is $L T^{-1}$. This remains true even if the rate is converted to different units, such as meters per second ($\mathrm{m\,s^{-1}}$). The conversion from $\mathrm{mm\,day^{-1}}$ to $\mathrm{m\,s^{-1}}$ involves multiplying by a constant conversion factor (specifically, $\frac{10^{-3}}{86400}$), which changes the numerical value but leaves the intrinsic physical dimension of the quantity unaltered .

It is critical to distinguish this process of [unit conversion](@entry_id:136593) from **[non-dimensionalization](@entry_id:274879)**. Converting all variables in an equation to a consistent unit system, such as the International System of Units (SI), is a prudent step for calculation, but it does not render the equation dimensionless. The variables and terms within the equation still carry their physical dimensions. Non-dimensionalization is a separate, more profound process of rescaling variables by characteristic quantities of the system itself, which we will explore in detail.

Another common point of confusion arises when different physical quantities are related by a dimensional constant. For example, a precipitation mass flux, with units $\mathrm{kg\,m^{-2}\,s^{-1}}$, has dimensions of $M L^{-2} T^{-1}$. This is fundamentally different from a precipitation depth rate, which has dimensions $L T^{-1}$. The two are related by the density of water, $\rho$ (dimensions $M L^{-3}$), through the equation $J_m = \rho P$. Although the density of water is often approximated as a constant value (e.g., $1000 \, \mathrm{kg\,m^{-3}}$), it is not a dimensionless number. Its presence is the dimensional link between mass flux and depth rate; the two quantities are not dimensionally equivalent .

#### The Principle of Dimensional Homogeneity

A cornerstone of physics and engineering is the **Principle of Dimensional Homogeneity**. This principle states that for any physically meaningful equation, all additive terms must have the same physical dimensions. You cannot, for example, add a mass to a length. This principle provides a powerful tool for checking the validity of equations and for deriving relationships between physical quantities.

Consider the one-dimensional [momentum balance](@entry_id:1128118) equation for a shallow geophysical flow, which describes how the velocity of a fluid element changes due to pressure gradients and viscous forces :
$$
\rho\,\partial_{t} u \;=\; -\partial_{x} p \;+\; \mu\,\partial_{xx} u
$$
Here, $\rho$ is the mass density, $u$ is velocity, $p$ is pressure, and $\mu$ is the [dynamic viscosity](@entry_id:268228). To verify that this equation is dimensionally consistent, we must determine the dimensions of each term. We begin by expressing the dimensions of the variables in terms of the [base dimensions](@entry_id:265281) $M$, $L$, and $T$:

- **Density ($\rho$)**: Mass per unit volume. $[\rho] = M L^{-3}$.
- **Velocity ($u$)**: Length per unit time. $[u] = L T^{-1}$.
- **Pressure ($p$)**: Force per unit area. Force is mass times acceleration ($[F] = M \cdot L T^{-2} = M L T^{-2}$), and area is $[A] = L^2$. Thus, $[p] = \frac{M L T^{-2}}{L^2} = M L^{-1} T^{-2}$.
- **Dynamic Viscosity ($\mu$)**: Ratio of shear stress (force per area) to strain rate ([velocity gradient](@entry_id:261686)). $[\mu] = \frac{[\text{Stress}]}{[\text{Strain Rate}]} = \frac{M L^{-1} T^{-2}}{[u]/[L]} = \frac{M L^{-1} T^{-2}}{T^{-1}} = M L^{-1} T^{-1}$.

The derivative operators also contribute to the dimensions: $[\partial_t] = T^{-1}$ and $[\partial_x] = L^{-1}$. We can now analyze each term in the equation:

- **Inertial Term**: $[\rho\,\partial_{t} u] = [\rho] [\partial_t] [u] = (M L^{-3})(T^{-1})(L T^{-1}) = M L^{-2} T^{-2}$.
- **Pressure Gradient Term**: $[-\partial_{x} p] = [\partial_x] [p] = (L^{-1})(M L^{-1} T^{-2}) = M L^{-2} T^{-2}$.
- **Viscous Term**: $[\mu\,\partial_{xx} u] = [\mu] [\partial_{xx}] [u] = (M L^{-1} T^{-1})(L^{-2})(L T^{-1}) = M L^{-2} T^{-2}$.

All three terms possess the identical dimension of $M L^{-2} T^{-2}$, which corresponds to force per unit volume (force density). The equation is therefore dimensionally homogeneous, satisfying a fundamental requirement for physical validity.

### The Process of Non-dimensionalization

While [dimensional homogeneity](@entry_id:143574) is a check for consistency, **non-dimensionalization** is a constructive procedure that transforms a dimensional equation into an equivalent dimensionless one. This is achieved by rescaling all variables using [characteristic scales](@entry_id:144643) inherent to the problem. The resulting dimensionless equation often provides deeper insight into the system's behavior.

#### Scaling Variables and Identifying Characteristic Scales

The core of the method is to define new, dimensionless variables (often denoted with an asterisk or hat) by dividing the original dimensional variables by constants that have the same dimensions. These constants are the **[characteristic scales](@entry_id:144643)** of the system. For a problem involving time $t$, length $x$, and concentration $m$, we would introduce:
$$
\hat{t} = \frac{t}{\tau}, \quad \hat{x} = \frac{x}{L_{c}}, \quad \hat{m} = \frac{m}{m_{ref}}
$$
Here, $\tau$, $L_c$, and $m_{ref}$ are the characteristic time, length, and concentration scales, respectively. The choice of these scales is a critical part of the art of modeling. They should be chosen based on the physics of the problem to represent natural scales of variation.

#### A Simple Example: First-Order Dynamics

Let us illustrate this with a simple model from synthetic biology describing the concentration of an mRNA species, $m(t)$ :
$$
\frac{dm}{dt} = \alpha - \gamma m
$$
Here, $m$ is concentration ($N L^{-3}$), $\alpha$ is a constant production rate (concentration per time, $N L^{-3} T^{-1}$), and $\gamma$ is a first-order degradation rate constant ($T^{-1}$).

We introduce dimensionless time $\hat{t} = t/\tau$ and concentration $\hat{m} = m/m_{ref}$. From these, $t = \tau \hat{t}$ and $m = m_{ref} \hat{m}$. Using the [chain rule](@entry_id:147422), the time derivative becomes $\frac{dm}{dt} = \frac{m_{ref}}{\tau} \frac{d\hat{m}}{d\hat{t}}$. Substituting these into the original equation yields:
$$
\frac{m_{ref}}{\tau}\frac{d\hat{m}}{d\hat{t}} = \alpha - \gamma (m_{ref}\hat{m})
$$
To simplify this equation, we rearrange it to isolate the derivative term:
$$
\frac{d\hat{m}}{d\hat{t}} = \frac{\alpha \tau}{m_{ref}} - (\gamma \tau)\hat{m}
$$
The goal of non-dimensionalization is to make the coefficients of the resulting equation of order one. A standard approach is to choose the [characteristic scales](@entry_id:144643) $\tau$ and $m_{ref}$ such that the coefficients become unity. This leads to the conditions:
$$
\gamma \tau = 1 \quad \text{and} \quad \frac{\alpha \tau}{m_{ref}} = 1
$$
From the first condition, we find the characteristic timescale of the system is $\tau = 1/\gamma$. This is the e-folding time of mRNA degradation, a natural time unit for this system. Substituting this into the second condition gives $m_{ref} = \alpha \tau = \alpha/\gamma$. This is the steady-state concentration ($dm/dt=0$), a natural concentration scale.

With these choices, our complex-looking equation becomes elegantly simple:
$$
\frac{d\hat{m}}{d\hat{t}} = 1 - \hat{m}
$$
This single, universal equation describes the dynamics of any system governed by first-order production and degradation, illustrating one of the profound benefits of non-dimensionalization.

#### Benefits of Non-dimensionalization

The effort of non-dimensionalizing a model is rewarded with several key advantages:

1.  **Parameter Reduction**: The original model had two parameters, $\alpha$ and $\gamma$. The dimensionless model has zero parameters. All systems with this underlying structure behave identically when viewed in their own characteristic units. This drastically simplifies the parameter space that needs to be explored.
2.  **Identification of Governing Dimensionless Groups**: In more complex problems, the dimensionless equation will retain some parameters. These are not just arbitrary coefficients; they are fundamental **[dimensionless groups](@entry_id:156314)** (like the Reynolds or Péclet numbers) that represent ratios of competing physical effects and govern the system's qualitative behavior.
3.  **Universality and Scalability**: A single dimensionless solution can be scaled to describe an entire family of different physical systems at different sizes and with different parameter values, so long as they share the same [dimensionless groups](@entry_id:156314).
4.  **Revealing Scales and Balances**: The process forces the modeler to identify the natural scales of the problem, leading to a deeper physical understanding. It highlights the balances between different terms, which is the basis for more advanced techniques like perturbation theory.

### Systematic Dimensional Analysis: The Buckingham $\pi$ Theorem

For simple problems, characteristic scales can often be found by inspection. For complex systems with many variables, a more systematic approach is needed. This is provided by the **Buckingham $\pi$ theorem**.

#### Statement of the Theorem

The Buckingham $\pi$ theorem provides a formal method for determining the number of independent [dimensionless groups](@entry_id:156314) in a physical system. A precise statement is as follows :

If a physically meaningful relationship involves $n$ dimensional variables, and the dimensions of these variables can be expressed using $r$ independent [base dimensions](@entry_id:265281) (where $r$ is the rank of the dimension matrix), then the relationship can be rewritten as an equation involving $k$ independent dimensionless groups (denoted $\pi_1, \pi_2, \dots, \pi_k$), where:
$$
k = n - r
$$
The new relationship takes the form $f(\pi_1, \pi_2, \dots, \pi_k) = 0$ for some unknown function $f$.

#### The Role of Linear Algebra: Dimension Matrix and Rank

The application of the $\pi$ theorem is fundamentally an exercise in linear algebra. For a set of variables, we can construct a **dimension matrix** where the rows correspond to the [base dimensions](@entry_id:265281) ($M, L, T, \dots$) and the columns correspond to the variables. Each entry in the matrix is the exponent of the corresponding base dimension for that variable. A dimensionless product of variables, $\pi = q_1^{a_1} q_2^{a_2} \cdots q_n^{a_n}$, corresponds to a vector of exponents $\mathbf{a} = (a_1, a_2, \dots, a_n)^T$ that is in the null space of the dimension matrix. The number of independent [dimensionless groups](@entry_id:156314), $k$, is therefore the dimension of this null space (the [nullity](@entry_id:156285)). The [rank-nullity theorem](@entry_id:154441) states that for a matrix with $n$ columns, `rank + [nullity](@entry_id:156285) = n`, which directly yields the Buckingham $\pi$ theorem's formula, $k = n - r$.

As an example, consider a coastal [plume model](@entry_id:1129836) with $n=6$ variables: velocity $U$, length $L$, density $\rho$, density deficit $\Delta\rho$, [kinematic viscosity](@entry_id:261275) $\nu$, and gravity $g$. The [base dimensions](@entry_id:265281) are $M, L, T$. The dimension matrix, with rows for $M, L, T$ and columns for $U, L, \rho, \Delta\rho, \nu, g$, is as follows :
$$
A = \begin{pmatrix}
 0  0  1  1  0  0 \\
 1  1  -3  -3  2  1 \\
 -1  0  0  0  -1  -2
\end{pmatrix}
$$
To find the number of independent [dimensionless groups](@entry_id:156314), we need the rank $r$ of this matrix. Through Gaussian elimination ([row reduction](@entry_id:153590)), this matrix can be reduced to a [row-echelon form](@entry_id:199986) with 3 non-zero rows. Thus, the rank is $r=3$. The number of independent $\pi$ groups is:
$$
k = n - r = 6 - 3 = 3
$$
This tells us that the complex dynamics governed by six parameters can be fully described by a relationship between just three dimensionless numbers (which turn out to be the Reynolds number, the Froude number, and the density ratio).

#### The Method of Repeating Variables

A practical procedure for constructing the $\pi$ groups is the **method of repeating variables**:

1.  List all $n$ physical variables involved.
2.  Identify the number of fundamental [base dimensions](@entry_id:265281) and determine the rank $r$ of the dimension matrix.
3.  Choose $r$ of the variables to be **repeating variables**. This set must be dimensionally independent; that is, the dimension matrix of the repeating variables alone must have rank $r$. This ensures they form a basis for the dimensional space. Good choices typically include variables representing geometry ($L$), kinematics ($U$), and dynamics ($\rho$).
4.  For each of the $n-r$ remaining (non-repeating) variables, form a $\pi$ group by creating a product of that variable with the repeating variables raised to unknown exponents. Solve for the exponents to make the product dimensionless.

#### A Common Pitfall: Choosing Repeating Variables

The choice of repeating variables is not arbitrary and must satisfy the condition of dimensional independence. A failure to do so renders the method invalid. Consider a fluid dynamics problem with variables $\{\rho, U, L, \mu\}$. The rank of the system is $r=3$ (spanning $M, L, T$). Therefore, we must choose 3 repeating variables.

Suppose one incorrectly chooses only two repeating variables, for instance, $\{U, \mu\}$ . The dimension matrix for this pair (with columns for $U, \mu$ and rows for $M, L, T$) is $\begin{pmatrix} 0  1 \\ 1  -1 \\ -1  -1 \end{pmatrix}$. This matrix has a rank of 2, which is less than the system rank of 3. These two variables do not span the full dimensional space. The consequence is immediate: it becomes impossible to non-dimensionalize the remaining variables. For example, if we try to form a $\pi$ group for density, $\Pi_\rho = \rho^1 U^a \mu^b$, we seek exponents $a, b$ that cancel the dimensions:
$$
[\Pi_\rho] = (M^1 L^{-3} T^0) (L T^{-1})^a (M L^{-1} T^{-1})^b = M^{1+b} L^{-3+a-b} T^{-a-b}
$$
For this to be dimensionless ($M^0 L^0 T^0$), we need to solve the system:
1.  $M: 1+b = 0 \implies b = -1$
2.  $T: -a-b = 0 \implies a = -b = 1$
3.  $L: -3+a-b = 0$
Substituting our solutions for $a$ and $b$ into the third equation gives $-3 + 1 - (-1) = -1 \neq 0$. The system is overdetermined and has no solution. This failure confirms that the chosen repeating variables do not form a proper dimensional basis.

### Advanced Applications and Interpretations

Non-dimensionalization is not merely a formal exercise; it is a gateway to deeper analysis, enabling model reduction, stability analysis, and physical interpretation.

#### Analysis of Complex Systems: The Genetic Toggle Switch

The power of this technique is fully realized in [nonlinear dynamical systems](@entry_id:267921). Consider a synthetic [genetic toggle switch](@entry_id:183549), where two proteins, $X$ and $Y$, mutually repress each other's synthesis . The dimensional equations are:
$$
\frac{dx}{dt} = \frac{\alpha}{1 + (y/K)^{n}} - \delta x, \qquad \frac{dy}{dt} = \frac{\alpha}{1 + (x/K)^{n}} - \delta y
$$
Here, $K$ is a concentration scale and $\delta$ is a degradation rate. Choosing the characteristic concentration as $K$ and time as $1/\delta$, we define dimensionless variables $u = x/K$, $v = y/K$, and $\tau = \delta t$. The system transforms into a much cleaner form:
$$
\frac{du}{d\tau} = \frac{\beta}{1 + v^n} - u, \qquad \frac{dv}{d\tau} = \frac{\beta}{1 + u^n} - v
$$
The entire system's behavior is now controlled by just two [dimensionless parameters](@entry_id:180651): the Hill coefficient $n$ and a single dimensionless group $\beta = \frac{\alpha}{K\delta}$, which represents the normalized maximal production strength.

This simplified form is ideal for analysis. For instance, to find the condition for bistability (the hallmark of a switch), we can analyze the stability of the symmetric steady state ($u=v$). Linear stability analysis on the dimensionless system reveals that this state becomes unstable when $\beta$ exceeds a critical value. For the common case of dimeric repression ($n=2$), this bifurcation occurs precisely at $\beta_c=2$. This elegant result, obtained from the dimensionless model, provides a universal design principle for building a functional [genetic switch](@entry_id:270285).

#### Characteristic Timescales and Process Dominance

Dimensionless groups can often be interpreted as ratios of [characteristic timescales](@entry_id:1122280) of competing physical processes. This interpretation provides immediate physical insight. Consider the transport of a reactive solute in a river, governed by the [advection-diffusion-reaction equation](@entry_id:156456) :
$$
\frac{\partial C}{\partial t} + U \frac{\partial C}{\partial x} \;=\; D \frac{\partial^{2} C}{\partial x^{2}} \;-\; k C
$$
We can identify a characteristic timescale for each process over a river reach of length $L$:

-   **Advection timescale ($T_A$)**: The time to travel the length $L$ at speed $U$. $T_A = L/U$.
-   **Diffusion timescale ($T_D$)**: The time for diffusion to act over the length $L$. By balancing $\partial C/\partial t \sim C/T_D$ and $D \partial^2 C/\partial x^2 \sim D C/L^2$, we find $T_D = L^2/D$.
-   **Reaction timescale ($T_R$)**: The e-folding time for the first-order decay. $T_R = 1/k$.

The ratio of these timescales forms key dimensionless groups. The **Péclet number**, $Pe = T_D/T_A = UL/D$, compares the efficiency of advective transport to [diffusive transport](@entry_id:150792). The **Damköhler number**, $Da = T_A/T_R = kL/U$, compares the rate of reaction to the rate of advection.

By computing these timescales for a specific scenario (e.g., $L=20\,\mathrm{km}, U=0.3\,\mathrm{m\,s^{-1}}, D=40\,\mathrm{m^2\,s^{-1}}, k=2 \times 10^{-6}\,\mathrm{s^{-1}}$), we might find $T_A \approx 6.7 \times 10^4\,\mathrm{s}$, $T_D = 1.0 \times 10^7\,\mathrm{s}$, and $T_R = 5.0 \times 10^5\,\mathrm{s}$ . The hierarchy of timescales ($T_A \ll T_R \ll T_D$) tells us instantly that advection is the fastest (most dominant) process, while diffusion is the slowest. This suggests that over this reach, a simple model neglecting diffusion might be a reasonable first approximation.

#### Asymptotic Analysis and Model Reduction: The QSSA

When [non-dimensionalization](@entry_id:274879) reveals a parameter that is very small (or very large), it opens the door to **asymptotic analysis** and [model reduction](@entry_id:171175). A prominent example in synthetic biology is the **[quasi-steady-state approximation](@entry_id:163315) (QSSA)**. Consider a simple gene expression model where mRNA ($m$) is transcribed and then translated into protein ($p$) :
$$
\frac{dm}{dt} = \alpha \phi(S) - \delta_m m, \qquad \frac{dp}{dt} = k_t m - \delta_p p
$$
In many biological systems, mRNA is much less stable than protein, meaning its degradation rate is much higher, $\delta_m \gg \delta_p$. If we non-dimensionalize time using the slower [protein dynamics](@entry_id:179001), $\tau = \delta_p t$, the dimensionless system becomes:
$$
\epsilon \frac{dx}{d\tau} = f(s) - x, \qquad \frac{dy}{d\tau} = x - y
$$
where $x$ and $y$ are dimensionless mRNA and protein concentrations, and a small parameter $\epsilon = \delta_p / \delta_m \ll 1$ has emerged. This parameter represents the ratio of the slow timescale ([protein lifetime](@entry_id:1130250)) to the fast timescale (mRNA lifetime).

Because $\epsilon$ is small, the term $\epsilon \frac{dx}{d\tau}$ is negligible unless $x$ is changing extremely rapidly. This implies that the mRNA concentration $x$ adjusts almost instantaneously to a "quasi-steady state" where its production balances its degradation: $x(\tau) \approx f(s(\tau))$. This approximation allows us to eliminate the first differential equation entirely, reducing the system to a single, simpler ODE for the protein: $\frac{dy}{d\tau} = f(s) - y$. This powerful reduction, justified rigorously by the small dimensionless parameter, is a cornerstone of modeling complex [biochemical networks](@entry_id:746811).

#### Extending Non-dimensionalization to PDEs

The principles of [non-dimensionalization](@entry_id:274879) apply equally to partial differential equations (PDEs) describing spatially [distributed systems](@entry_id:268208). For a model of phytoplankton biomass $B(x,t)$ subject to diffusion and [logistic growth](@entry_id:140768) in a channel of length $L$ :
$$
\frac{\partial B}{\partial t} = D \frac{\partial^2 B}{\partial x^2} + r B \left(1 - \frac{B}{K}\right)
$$
We can choose characteristic scales for length ($\ell=L$), time ($T=1/r$), and biomass ($B_{ref}$, which could be the [carrying capacity](@entry_id:138018) $K$ or, as in some cases, the average initial biomass). The rescaling transforms the PDE into a dimensionless form:
$$
\frac{\partial u}{\partial \tau} = \delta \frac{\partial^2 u}{\partial \xi^2} + u\left(1-\frac{u}{\kappa}\right)
$$
where $\xi=x/L, \tau=t/r, u=B/B_{ref}$. The system's behavior is now governed by two [dimensionless groups](@entry_id:156314): $\delta = D/(rL^2)$, the ratio of the reaction timescale to the diffusion timescale, and $\kappa = K/B_{ref}$, the dimensionless [carrying capacity](@entry_id:138018). The six original parameters ($L, D, r, K$, and those defining $B_{ref}$) have been collapsed into just two governing groups, dramatically simplifying the problem.

#### Special Cases: Handling Dimensionless Variables

A final point of clarification regards the treatment of variables that are already dimensionless, or are defined nonlinearly. A common example from environmental chemistry is $pH$, defined as $pH = -\log_{10} a_{\mathrm{H}^+}$, where $a_{\mathrm{H}^+}$ is the dimensionless activity of the hydrogen ion .

The Buckingham $\pi$ theorem is a method for constructing [dimensionless groups](@entry_id:156314) from a set of *dimensional* primitives. If a variable in your initial list is already dimensionless (such as an [activity coefficient](@entry_id:143301) $\gamma$, or the activity $a_{\mathrm{H}^+}$ itself), it is, by definition, already a $\pi$ group. It should be set aside and included as one of the final arguments in the dimensionless function $f(\pi_1, \pi_2, \dots)$. One does not—and cannot—multiply it by dimensional variables to "create" a $\pi$ group.

Furthermore, any monotonic, invertible transformation of a $\pi$ group is also a valid dimensionless parameter. Since $pH$ is such a transformation of the $\pi$ group $a_{\mathrm{H}^+}$, it is perfectly valid to use $pH$ as an argument in the final dimensionless relationship. The choice between using $a_{\mathrm{H}^+}$ or $pH$ is one of convention and convenience, not of fundamental principle. The count of independent [dimensionless groups](@entry_id:156314), $k = n-r$, remains unchanged. One must not make the mistake of treating $pH$ as a new fundamental dimension, as it is explicitly defined in terms of other physical quantities.