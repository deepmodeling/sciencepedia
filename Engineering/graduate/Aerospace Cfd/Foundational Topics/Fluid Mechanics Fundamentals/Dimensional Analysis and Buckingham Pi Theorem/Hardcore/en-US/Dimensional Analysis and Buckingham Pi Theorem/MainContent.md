## Introduction
Dimensional analysis is a cornerstone of engineering and the physical sciences, providing a powerful framework for simplifying complexity and revealing the underlying physics of a system. For practitioners in fields like computational fluid dynamics (CFD), who grapple with intricate systems of partial differential equations, this tool is indispensable. The central challenge it addresses is the overwhelming number of variables that can influence a phenomenon, making it difficult to design experiments, interpret data, or generalize results. This article offers a comprehensive guide to mastering dimensional analysis, transforming it from an abstract concept into a practical tool for problem-solving.

Across the following chapters, you will embark on a structured journey through this essential topic. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, starting with the [principle of dimensional homogeneity](@entry_id:273094) and building up to the systematic procedure of the Buckingham Pi theorem. You will learn how to derive [dimensionless groups](@entry_id:156314) and understand their mathematical foundations. The second chapter, "Applications and Interdisciplinary Connections," demonstrates the theorem's vast utility, showcasing how [dimensionless parameters](@entry_id:180651) govern phenomena from [aerodynamic drag](@entry_id:275447) and boundary layers to heat transfer, chemical reactions, and even multi-physics problems like [aeroelasticity](@entry_id:141311). Finally, the "Hands-On Practices" section provides an opportunity to apply these concepts to solve concrete problems, solidifying your understanding and building practical skills.

## Principles and Mechanisms

The formulation of physical laws must be independent of the arbitrary choice of units used to measure quantities. This foundational concept, known as the principle of [dimensional consistency](@entry_id:271193), is the bedrock of [dimensional analysis](@entry_id:140259). In the context of computational fluid dynamics (CFD), where complex systems of partial differential equations are solved numerically, [dimensional analysis](@entry_id:140259) provides an indispensable framework for simplifying problems, guiding experimentation, interpreting results, and ensuring the generality of conclusions. This chapter systematically develops the principles of [dimensional analysis](@entry_id:140259), from the basic requirement of homogeneity to the powerful predictive capabilities and inherent limitations of the Buckingham Pi theorem.

### The Principle of Dimensional Homogeneity

A physical equation is said to be **dimensionally homogeneous** if every additive term within it possesses the same fundamental dimensions. This is a necessary condition for any physically meaningful law. An equation comparing, for instance, a mass to a length is nonsensical. Verifying [dimensional homogeneity](@entry_id:143574) is the first step in analyzing any physical system and serves as a crucial check on the validity of derived equations.

To perform this verification, we express all physical quantities in terms of a chosen set of **[base dimensions](@entry_id:265281)**. In mechanics and fluid dynamics, the most common choice is the Mass-Length-Time system, denoted $\{M, L, T\}$. For problems involving heat transfer, a fourth dimension, Temperature, denoted by $\Theta$, is included.

Let us illustrate this with a cornerstone of fluid dynamics: the inviscid momentum equation, or Euler equation. In [index notation](@entry_id:191923), it is written as:
$$
\rho\left(\frac{\partial u_{i}}{\partial t}+u_{j}\frac{\partial u_{i}}{\partial x_{j}}\right)=-\frac{\partial p}{\partial x_{i}}
$$
To verify its [dimensional homogeneity](@entry_id:143574), we must first establish the dimensions of each variable from its fundamental definition . We use the notation $[X]$ to denote the dimensions of a quantity $X$.

1.  **Density ($\rho$)**: Mass per unit volume. $[Volume] = L^3$.
    $$[\rho] = \frac{[Mass]}{[Volume]} = \frac{M}{L^3} = ML^{-3}$$
2.  **Velocity ($u_i$)**: Rate of change of position ($x_i$, dimension $L$) with respect to time ($t$, dimension $T$).
    $$[u_i] = \frac{[x_i]}{[t]} = \frac{L}{T} = LT^{-1}$$
3.  **Pressure ($p$)**: Force per unit area. Force is defined by Newton's second law, $F=ma$. The dimensions of acceleration ($a$) are $[a] = [u_i]/[t] = (LT^{-1})/T = LT^{-2}$.
    $$[Force] = [Mass] \times [Acceleration] = M(LT^{-2}) = MLT^{-2}$$
    With $[Area] = L^2$, the dimensions of pressure are:
    $$[p] = \frac{[Force]}{[Area]} = \frac{MLT^{-2}}{L^2} = ML^{-1}T^{-2}$$

Now, we analyze each term in the Euler equation. The equation essentially states that the mass of a fluid element times its acceleration is equal to the pressure force acting on it. The left-hand side represents the rate of change of momentum per unit volume, while the right-hand side represents the pressure [gradient force](@entry_id:166847) per unit volume.

The term in parentheses, $\frac{\partial u_{i}}{\partial t}+u_{j}\frac{\partial u_{i}}{\partial x_{j}}$, is the total or **[material acceleration](@entry_id:270992)**. It consists of the **[local acceleration](@entry_id:272847)** ($\partial u_i / \partial t$) and the **convective acceleration** ($u_j \partial u_i / \partial x_j$). For the equation to be homogeneous, these two terms must first share the same dimensions.
-   Local acceleration: $\left[\frac{\partial u_{i}}{\partial t}\right] = \frac{[u_i]}{[t]} = \frac{LT^{-1}}{T} = LT^{-2}$.
-   Convective acceleration: $\left[u_{j}\frac{\partial u_{i}}{\partial x_{j}}\right] = [u_j]\frac{[u_i]}{[x_j]} = (LT^{-1})\frac{LT^{-1}}{L} = LT^{-2}$.

Both terms indeed have the dimensions of acceleration. The entire left-hand side (LHS) of the equation thus has dimensions:
$$[\text{LHS}] = [\rho] \times [\text{Acceleration}] = (ML^{-3})(LT^{-2}) = ML^{-2}T^{-2}$$
The right-hand side (RHS) is the negative of the pressure gradient:
$$[\text{RHS}] = \left[\frac{\partial p}{\partial x_{i}}\right] = \frac{[p]}{[x_i]} = \frac{ML^{-1}T^{-2}}{L} = ML^{-2}T^{-2}$$
Since $[LHS] = [RHS]$, the Euler equation is dimensionally homogeneous. The common dimension, $ML^{-2}T^{-2}$, is that of force per unit volume.

A more formal way to represent dimensions is through a **dimension vector**, where each component corresponds to the exponent of a base dimension in the ordered basis $\{M, L, T, \Theta\}$ . For instance, the dimension vector for pressure ($p$) with dimensions $M^1 L^{-1} T^{-2} \Theta^0$ is $\begin{pmatrix} 1 & -1 & -2 & 0 \end{pmatrix}$. This formalism is particularly useful when implementing dimensional analysis algorithmically. For example, the dimension of **dynamic viscosity ($\mu$)** can be derived from Newton's law of viscosity, which states that shear stress ($\tau$) is proportional to the [velocity gradient](@entry_id:261686) ($du/dy$).
$$ [\mu] = \frac{[\tau]}{[du/dy]} $$
Shear stress, being a force per area, has the same dimensions as pressure, $[\tau] = ML^{-1}T^{-2}$. The velocity gradient has dimensions $[du/dy] = [u]/[y] = (LT^{-1})/L = T^{-1}$. Therefore,
$$[\mu] = \frac{ML^{-1}T^{-2}}{T^{-1}} = ML^{-1}T^{-1}$$
The corresponding dimension vector for $\mu$ in the $\{M, L, T, \Theta\}$ basis is $\begin{pmatrix} 1 & -1 & -1 & 0 \end{pmatrix}$.

### The Buckingham Pi Theorem: A Systematic Framework

While [dimensional homogeneity](@entry_id:143574) provides a consistency check, its true power is harnessed through the **Buckingham Pi ($\Pi$) theorem**. This theorem provides a systematic method for reorganizing a physical relationship into a more compact and universal form.

The theorem states: If a physical process is described by a dimensionally [homogeneous equation](@entry_id:171435) involving $n$ physical variables, and these variables can be described using $r$ independent fundamental dimensions, then the process can be equivalently described by an equation involving $p = n - r$ independent **[dimensionless groups](@entry_id:156314)**, also known as **Pi ($\Pi$) groups**.

The primary utility of the theorem is complexity reduction. A problem involving, say, 8 variables and 3 fundamental dimensions can be reduced to a relationship between just $8-3=5$ dimensionless parameters. This makes it vastly more efficient to study the system experimentally or computationally.

#### The Algorithmic Procedure

The application of the Buckingham $\Pi$ theorem follows a clear, step-by-step process.

1.  **List Variables**: Identify and list all $n$ physical variables and parameters believed to influence the phenomenon. This is the most critical step, as omitting a relevant variable will lead to an incomplete set of $\Pi$ groups.
2.  **Determine Dimensions**: Express the dimensions of each of the $n$ variables in terms of a set of fundamental [base dimensions](@entry_id:265281), e.g., $\{M, L, T, \Theta\}$.
3.  **Find the Rank**: Determine $r$, the number of independent fundamental dimensions required. This is the rank of the *dimensional matrix*, a matrix whose columns correspond to the variables and whose rows correspond to the exponents of the [base dimensions](@entry_id:265281). In most fluid dynamics problems, $r$ is equal to the number of [base dimensions](@entry_id:265281) used (e.g., $r=3$ for $\{M, L, T\}$).
4.  **Calculate Number of $\Pi$ Groups**: The number of independent [dimensionless groups](@entry_id:156314) is $p = n - r$.
5.  **Select Repeating Variables**: Choose $r$ variables from the original list to serve as **repeating variables**. These variables will be used to form the [dimensionless groups](@entry_id:156314). The selection of these variables is constrained by several crucial criteria.
6.  **Construct $\Pi$ Groups**: Each of the $p = n-r$ remaining variables (the non-repeating ones) is combined with the $r$ repeating variables to form one $\Pi$ group. The exponents of the repeating variables are chosen such that the resulting product is dimensionless. This results in a [system of linear equations](@entry_id:140416) for the exponents for each $\Pi$ group.

#### Criteria for Selecting Repeating Variables

The choice of repeating variables is not arbitrary and must adhere to strict rules to ensure a valid and solvable system .

*   **Rule 1: Number**: The number of repeating variables must be equal to the rank, $r$.
*   **Rule 2: Dimensional Independence**: The set of repeating variables must be **dimensionally independent**. This means that the dimensions of any one repeating variable cannot be formed by a product of powers of the others. Mathematically, the dimensional matrix of the repeating variables must have a rank of $r$. For a square matrix ($r$ variables, $r$ dimensions), this is equivalent to its determinant being non-zero. For example, in an aerospace context with variables $\{U, L, \rho, \mu, a\}$ and base $\{M,L,T\}$, the set $\{U, L, \rho\}$ is a valid choice because its dimensional matrix has a non-zero determinant. Conversely, a set like $\{U, a, L\}$ is invalid because $[U]$ and $[a]$ have the same dimensions ($LT^{-1}$), making them dimensionally dependent.
*   **Rule 3: Span the Dimensions**: The set of repeating variables must collectively include all the fundamental dimensions. This is automatically satisfied if Rule 2 holds for a set of $r$ variables and $r$ dimensions. A set like $\{U, a, L\}$ is invalid also because it lacks the [mass dimension](@entry_id:160525) $M$, making it impossible to non-dimensionalize mass-bearing quantities like density $\rho$ or drag force $D$.
*   **Rule 4: Exclude the Dependent Variable**: The primary variable of interest (the "dependent" variable, such as drag force) should not be chosen as a repeating variable. This ensures that it appears in only one $\Pi$ group, allowing for an explicit functional relationship of the form $\Pi_1 = f(\Pi_2, \Pi_3, ...)$.

As a matter of good practice, repeating variables are often chosen to be fundamental quantities representing the primary scales of the problem, such as a characteristic length, velocity, and density.

#### A Comprehensive Example: Aerodynamic Drag

Let's apply this procedure to a canonical aerospace problem: determining the [dimensionless parameters](@entry_id:180651) governing the drag force $D$ on an [aerofoil](@entry_id:195951) . The relevant physical variables are identified as:
-   Drag force, $D$ ($MLT^{-2}$)
-   Freestream velocity, $U$ ($LT^{-1}$)
-   Characteristic chord length, $L$ ($L$)
-   Fluid density, $\rho$ ($ML^{-3}$)
-   Dynamic viscosity, $\mu$ ($ML^{-1}T^{-1}$)
-   Speed of sound, $a$ ($LT^{-1}$)
-   Surface roughness height, $k_s$ ($L$)
-   Angle of attack, $\alpha$ (dimensionless, i.e., $1$)

1.  **Variables**: $n=8$. The list is $\{D, U, L, \rho, \mu, a, k_s, \alpha\}$.
2.  **Dimensions**: The [base dimensions](@entry_id:265281) are $\{M, L, T\}$.
3.  **Rank**: The rank is $r=3$.
4.  **$\Pi$ Groups**: The number of groups is $p = n - r = 8 - 3 = 5$.
5.  **Repeating Variables**: We select the standard set $\{U, L, \rho\}$. They are $r=3$ in number, are dimensionally independent, and do not include the [dependent variable](@entry_id:143677) $D$.
6.  **Construct Groups**: We form five $\Pi$ groups, one for each remaining variable $\{D, \mu, a, k_s, \alpha\}$, of the form $\Pi = (\text{non-repeating variable}) \times U^x L^y \rho^z$.

*   **$\Pi_D$ (for Drag $D$)**: $\Pi_D = D U^x L^y \rho^z$.
    $$[M^1 L^1 T^{-2}] (LT^{-1})^x (L)^y (ML^{-3})^z = M^0 L^0 T^0$$
    Solving the [system of linear equations](@entry_id:140416) for the exponents yields $x=-2, y=-2, z=-1$.
    $$\Pi_D = \frac{D}{\rho U^2 L^2}$$
    This is the definition of the **drag coefficient**, $C_D$, with $L^2$ representing a characteristic area.

*   **$\Pi_{\mu}$ (for Viscosity $\mu$)**: $\Pi_{\mu} = \mu U^x L^y \rho^z$.
    $$[M^1 L^{-1} T^{-1}] (LT^{-1})^x (L)^y (ML^{-3})^z = M^0 L^0 T^0$$
    Solving gives $x=-1, y=-1, z=-1$.
    $$\Pi_{\mu} = \frac{\mu}{\rho U L}$$
    This is the inverse of the **Reynolds number**, $Re = \frac{\rho U L}{\mu}$.

*   **$\Pi_a$ (for Speed of Sound $a$)**: $\Pi_a = a U^x L^y \rho^z$.
    $$[L^1 T^{-1}] (LT^{-1})^x (L)^y (ML^{-3})^z = M^0 L^0 T^0$$
    Solving gives $x=-1, y=0, z=0$.
    $$\Pi_a = \frac{a}{U}$$
    This is the inverse of the **Mach number**, $Ma = \frac{U}{a}$.

*   **$\Pi_{k_s}$ (for Roughness $k_s$)**: $\Pi_{k_s} = k_s U^x L^y \rho^z$. By inspection, since $k_s$ and $L$ both have dimensions of length, their ratio must be dimensionless.
    $$\Pi_{k_s} = \frac{k_s}{L}$$
    This is the **[relative roughness](@entry_id:264325)**.

*   **$\Pi_{\alpha}$ (for Angle of Attack $\alpha$)**: Since $\alpha$ is already dimensionless, it is a $\Pi$ group by itself.
    $$\Pi_{\alpha} = \alpha$$

The final result of the dimensional analysis is that the complex relationship among 8 variables is reduced to the much simpler and universal form:
$$ C_D = f\left(Re, Ma, \frac{k_s}{L}, \alpha\right) $$

#### A Common Pitfall: Redundant Variables

The selection of the initial list of variables is paramount. If physically [dependent variables](@entry_id:267817) are included, the procedure will still work but will produce a trivial $\Pi$ group that is identically equal to a constant, revealing the redundancy . Consider a problem where one naively includes density $\rho$, dynamic viscosity $\mu$, and kinematic viscosity $\nu$ in the variable list. Since these are related by the definition $\nu = \mu/\rho$, they are not independent. A [dimensional analysis](@entry_id:140259) on the set $\{\rho, \mu, \nu\}$ would produce the dimensionless group $\Pi = \frac{\mu}{\rho\nu}$. Substituting the definition of $\nu$, we find $\Pi = 1$. The appearance of a constant $\Pi$ group is a signal that the initial variable list was redundant. The correct approach is to recognize the dependency beforehand and remove one of the variables (e.g., $\nu$) from the list, reducing $n$ by one and leading to the correct number of physically meaningful $\Pi$ groups.

### Mathematical Foundation and Physical Interpretation

While the algorithmic approach is effective, a deeper understanding comes from its mathematical underpinnings and the physical meaning of the resulting [dimensionless groups](@entry_id:156314).

#### The Null Space Formulation

The process of finding the exponents for a $\Pi$ group can be formalized using linear algebra . For a set of variables $\{v_1, v_2, ..., v_n\}$, we seek a monomial $\Pi = v_1^{e_1} v_2^{e_2} \cdots v_n^{e_n}$ that is dimensionless. This is equivalent to solving the homogeneous linear system $A \mathbf{e} = \mathbf{0}$, where $\mathbf{e} = (e_1, e_2, ..., e_n)^T$ is the vector of exponents and $A$ is the dimensional matrix. The solutions to this equation form the **[null space](@entry_id:151476)** (or kernel) of the matrix $A$. The number of independent $\Pi$ groups, $p=n-r$, is precisely the dimension of this null space. Each vector in a basis for the [null space](@entry_id:151476) corresponds to the exponents of an independent $\Pi$ group.

For example, consider an inviscid, incompressible 2D flow where the sectional lift per unit span, $L'$, depends on speed $U$, density $\rho$, and chord $c$. The variables are $\{L', U, \rho, c\}$ with dimensions $[L'] = MT^{-2}$, $[U] = LT^{-1}$, $[\rho] = ML^{-3}$, and $[c]=L$. The dimensional matrix $A$ is:
$$ A = \begin{pmatrix} 1 & 0 & 1 & 0 \\ 0 & 1 & -3 & 1 \\ -2 & -1 & 0 & 0 \end{pmatrix} $$
Solving $A \mathbf{e} = \mathbf{0}$ for $\mathbf{e} = (\alpha, \beta, \gamma, \delta)^T$ gives a one-dimensional null space spanned by the vector $\begin{pmatrix} 1 & -2 & -1 & -1 \end{pmatrix}^T$. This corresponds to the exponents in the single $\Pi$ group:
$$ \Pi = (L')^1 U^{-2} \rho^{-1} c^{-1} = \frac{L'}{\rho U^2 c} $$
This group is a form of the sectional [lift coefficient](@entry_id:272114), $c_l$.

#### From Algebra to PDEs: Inspectional Analysis

For CFD, the most powerful application of these principles is **[inspectional analysis](@entry_id:1126530)**, the non-dimensionalization of the governing partial differential equations themselves . By scaling all variables in the Navier-Stokes equations with appropriate characteristic quantities (e.g., $x^* = x/L$, $u^*=u/U$, $p^* = p/(\rho U^2)$), the equations can be rewritten in a completely dimensionless form. In this process, the dimensionless groups emerge naturally as coefficients of the various terms.

For example, when the momentum equation is non-dimensionalized, the viscous term is found to be multiplied by the coefficient $1/Re$.
$$ \rho^* \left( \frac{\partial \mathbf{u}^*}{\partial t^*} + \mathbf{u}^* \cdot \nabla^* \mathbf{u}^* \right) = - \nabla^* p^* + \frac{1}{\mathrm{Re}} \nabla^* \cdot \boldsymbol{\tau}^* + \dots $$
This directly demonstrates that the Reynolds number, $Re$, governs the relative importance of the [viscous forces](@entry_id:263294) compared to the inertial forces. Similarly, non-dimensionalizing the energy equation reveals the Prandtl number, $Pr$, and Mach number, $Ma$, as coefficients controlling heat conduction and compressibility effects. This method provides a rigorous link between the abstract Pi theorem and the physical phenomena described by the governing equations.

#### The Physical Meaning of Pi Groups

Dimensionless groups are not arbitrary combinations; they represent ratios of competing physical effects. Understanding their physical meaning is essential for interpreting flow behavior.

*   **Reynolds Number ($Re = \rho U L / \mu$)**: As revealed by [inspectional analysis](@entry_id:1126530), the Reynolds number quantifies the ratio of inertial forces to viscous forces .
    -   The **inertial term** in the momentum equation, $\rho(\mathbf{u} \cdot \nabla)\mathbf{u}$, represents the [convective acceleration](@entry_id:263153) of fluid. Its magnitude scales as $\sim \rho U^2/L$.
    -   The **viscous term**, $\mu \nabla^2 \mathbf{u}$, represents the diffusion of momentum. Its magnitude scales as $\sim \mu U/L^2$.
    -   The ratio of these scales is:
        $$ \frac{\text{Inertial forces}}{\text{Viscous forces}} \sim \frac{\rho U^2 / L}{\mu U / L^2} = \frac{\rho U L}{\mu} = Re $$
    High-$Re$ flows (e.g., aircraft in flight) are dominated by inertia, leading to thin boundary layers and turbulence. Low-$Re$ flows (e.g., [microorganisms](@entry_id:164403) swimming) are dominated by viscosity, resulting in smooth, creeping motion.

*   **Mach Number ($Ma = U/a$)**: The Mach number quantifies the importance of compressibility effects . It represents the ratio of the fluid's bulk motion speed to the speed of sound, which is the speed at which infinitesimal disturbances propagate.
    -   It can also be interpreted as the ratio of the time it takes for a sound wave to cross a characteristic length ($t_{acoustic} \sim L/a$) to the time it takes for a fluid particle to be convected over that same length ($t_{convective} \sim L/U$). Thus, $Ma \sim t_{acoustic} / t_{convective}$.
    -   When $Ma \ll 1$, convective time is much longer than acoustic time. The flow has ample time to adjust to pressure changes, and density can be treated as nearly constant. The magnitude of [density fluctuations](@entry_id:143540) scales as $\Delta\rho/\rho \sim O(Ma^2)$, and the "[pressure work](@entry_id:265787)" term in the energy equation, which represents conversion of kinetic to internal energy, scales as $O((\gamma-1)Ma^2)$ relative to convective [heat transport](@entry_id:199637). For $Ma  0.3$, these effects are often negligible, and the flow can be modeled as incompressible. As $Ma$ approaches and exceeds 1, compressibility effects like shock waves become dominant.

### Applications and Limitations in CFD

Dimensional analysis is the theoretical foundation of **[dynamic similarity](@entry_id:162962)**. The principle states that two flows are dynamically similar if they have the same geometry and the same values for all relevant $\Pi$ groups. If this condition is met, the dimensionless solutions for all output quantities (e.g., [drag coefficient](@entry_id:276893)) will be identical. This allows results from a single CFD simulation (or wind tunnel test) to be applied to a vast family of flows with different fluids, sizes, and speeds, as long as they share the same dimensionless parameters.

Despite its power, dimensional analysis has profound limitations that are critical to appreciate, especially in the context of complex phenomena like turbulence .

1.  **Non-Uniqueness and Transition**: The governing equations of fluid dynamics are nonlinear and can admit multiple solutions for the same set of [dimensionless parameters](@entry_id:180651). A classic example is boundary layer flow, which can be either laminar or turbulent at the same Reynolds number. Dimensional analysis, applied to the standard set of variables, cannot predict which state will occur. The selection of the flow state is determined by the stability of the laminar solution to external disturbances. The amplitude and nature of these disturbances (e.g., freestream turbulence intensity) act as additional parameters. Without including them in the analysis, one cannot predict transition. The "quiet" and "noisy" wind tunnels described in  produce flows with identical $Re$ and $Ma$, but different transition locations, because the disturbance environment, an unstated parameter, is different.

2.  **The Turbulence Closure Problem**: Even when the flow is known to be turbulent, [dimensional analysis](@entry_id:140259) cannot predict the detailed structure of the flow. When the Navier-Stokes equations are averaged to derive equations for the mean flow (the RANS equations), new unknown terms appear, namely the **Reynolds stresses** (e.g., $\overline{\rho u_i' u_j'}$). These terms represent the transport of momentum by turbulent fluctuations. This gives rise to the **[turbulence closure problem](@entry_id:268973)**: there are more unknowns than equations. Dimensional analysis can guide the formulation of models for the Reynolds stresses—for instance, by showing how an "eddy viscosity" should depend on a turbulent velocity and length scale—but it cannot derive the functional form of these models or the values of the empirical constants within them. Resolving the turbulent structure requires a **closure hypothesis**, or [turbulence model](@entry_id:203176), which is fundamentally an empirical input that goes beyond pure dimensional reasoning.

In summary, [dimensional analysis](@entry_id:140259) is a powerful tool for reducing problem complexity and establishing scaling laws. It tells us *which* [dimensionless parameters](@entry_id:180651) govern a phenomenon. However, it cannot, by itself, determine the functional relationships between these parameters, nor can it resolve ambiguities arising from the [non-uniqueness of solutions](@entry_id:198694) to the governing equations. For the CFD practitioner, it is both a guide for setting up simulations and a crucial reminder of the need for physical insight and empirical modeling to tackle the full complexity of fluid flows.