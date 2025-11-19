## Introduction
Surge waves and hydraulic jumps are among the most dynamic and visually striking phenomena in [open-channel flow](@entry_id:267863). Characterized by abrupt changes in water depth and velocity, they are critical features in both natural river systems and engineered hydraulic structures. Their analysis, however, presents a significant challenge: the intense turbulence and [energy dissipation](@entry_id:147406) involved render the principle of energy conservation intractable for predicting the flow transition. This article confronts this challenge by building a robust analytical framework grounded in the conservation of momentum.

This article provides a graduate-level exploration of these complex flows, structured to build understanding from first principles to advanced applications. In **Principles and Mechanisms**, you will master the foundational theory, starting with the concept of [specific force](@entry_id:266188), deriving the classic Bélanger equation for hydraulic jumps, analyzing moving surges, and quantifying the associated energy loss. Following this, **Applications and Interdisciplinary Connections** will reveal the astonishing breadth of these concepts, showcasing their role in civil engineering design, geophysical processes, and as powerful analogies for [shock waves](@entry_id:142404) in astrophysics and quantum mechanics. Finally, the **Hands-On Practices** section offers a chance to apply this knowledge to solve complex problems, solidifying your understanding of how these powerful fluid dynamic events are modeled and predicted.

## Principles and Mechanisms

Following the general introduction to [open-channel flow](@entry_id:267863), this chapter delves into the fundamental principles and mechanisms governing two of its most dynamic phenomena: the [surge wave](@entry_id:185243) and the [hydraulic jump](@entry_id:266212). These are forms of [rapidly varied flow](@entry_id:274873) where significant changes in flow depth and velocity occur over a very short distance. Our analysis will pivot from the idealized case to more complex and realistic scenarios, building a comprehensive theoretical framework. We will begin by establishing the primary analytical tool for these phenomena: the [momentum principle](@entry_id:261235), articulated through the concept of [specific force](@entry_id:266188).

### The Momentum Principle and Specific Force

In the study of [gradually varied flow](@entry_id:264271), the conservation of energy is the guiding principle. However, for rapidly varied flows like a hydraulic jump, the intense turbulence and [energy dissipation](@entry_id:147406) render the energy equation intractable for determining the relationship between the upstream and downstream flow depths. Instead, we turn to the conservation of momentum.

For a one-dimensional, [steady flow](@entry_id:264570) in a prismatic channel, the [integral momentum equation](@entry_id:272259) applied to a [control volume](@entry_id:143882) encompassing a short reach of the channel yields a powerful relationship. Neglecting boundary friction and the component of gravity for a horizontal channel, the sum of the pressure force and the [momentum flux](@entry_id:199796) remains constant. This conserved quantity, when normalized by the [specific weight](@entry_id:275111) of the fluid ($\rho g$), is termed the **[specific force](@entry_id:266188)**, denoted by $M$. It is defined as:

$M = \frac{Q^2}{gA} + \mathcal{P}$

Here, $Q$ is the [volumetric flow rate](@entry_id:265771), $g$ is the [acceleration due to gravity](@entry_id:173411), and $A$ is the cross-sectional area of flow. The first term, $\frac{Q^2}{gA}$, represents the momentum flux per unit weight passing through the cross-section. The second term, $\mathcal{P}$, represents the [hydrostatic pressure](@entry_id:141627) force acting on the cross-section, also per unit weight. This pressure term is equivalent to the first moment of the wetted area $A$ about the free surface. For a channel whose width is described by a function $b(z)$ at a vertical distance $z$ from the bed, $\mathcal{P}$ can be calculated by the integral:

$\mathcal{P}(y) = \int_0^y (y-z) b(z) dz$

where $y$ is the flow depth. For the simple case of a wide rectangular channel, this integral yields $\mathcal{P}(y) = \frac{y^2}{2}$ per unit width.

The utility of this integral formulation becomes apparent when dealing with complex channel geometries, such as a compound channel composed of a main channel and adjacent floodplains. For instance, consider a channel with a rectangular main section of width $b_m$ and floodplains elevated by a height $h_f$, with a total width $B$ when the water level $y$ exceeds $h_f$. To find the pressure force term, the integral is split according to the piecewise-constant width function. This yields an expression for $\mathcal{P}(y)$ that correctly accounts for the geometry [@problem_id:614199]:

$\mathcal{P}(y) = b_m \left(yh_f - \frac{h_f^2}{2}\right) + \frac{B (y-h_f)^2}{2} \quad \text{for } y > h_f$

The standard definition of [specific force](@entry_id:266188) assumes a uniform [velocity profile](@entry_id:266404) across the channel section. In reality, velocity varies, being zero at the boundaries and typically maximum near the free surface. To account for this, the [momentum flux](@entry_id:199796) term is corrected by the **Boussinesq coefficient**, $\beta$, also known as the momentum correction coefficient. The corrected [specific force](@entry_id:266188) is $M = \beta \frac{Q^2}{gA} + \mathcal{P}$. The coefficient $\beta$ is defined as:

$\beta = \frac{1}{A V^2} \int_A v^2 dA$

where $v$ is the local velocity and $V$ is the [average velocity](@entry_id:267649) ($Q/A$). For a uniform profile, $\beta=1$. For any non-uniform profile, $\beta > 1$. As a detailed example, consider a power-law velocity profile $v(z) = v_{max} (z/y)^{1/n}$ in a wide channel. By performing the integration, one can show that $\beta = \frac{(n+1)^2}{n(n+2)}$. A similar coefficient, the [energy correction](@entry_id:198270) coefficient $\alpha$, corrects the kinetic energy term in the energy equation. The relationship between these correction factors provides insight into the nature of the [velocity profile](@entry_id:266404). For the same power-law profile, a characteristic parameter $K = (\alpha-1)/(\beta-1)$ can be derived, resulting in $K = \frac{(n+2)(3n+1)}{n(n+3)}$ [@problem_id:614304]. These coefficients are crucial for high-accuracy analyses but are often assumed to be unity in introductory treatments.

### The Ideal Hydraulic Jump: Conservation of Specific Force

A **hydraulic jump** is a stationary, abrupt transition from a high-velocity, low-depth (supercritical) flow to a low-velocity, high-depth (subcritical) flow. This phenomenon is commonly engineered in stilling basins downstream of dam spillways to safely dissipate energy.

For an idealized jump in a horizontal, frictionless, prismatic channel, the [specific force](@entry_id:266188) is conserved between the upstream section (subscript 1) and the downstream section (subscript 2):

$M_1 = M_2$

This equation implies that for a given discharge $Q$, there are two possible depths, known as **conjugate depths**, that share the same value of [specific force](@entry_id:266188). One depth, $y_1$, corresponds to supercritical flow, and the other, $y_2$, corresponds to [subcritical flow](@entry_id:276823).

For a wide rectangular channel, the conservation of [specific force](@entry_id:266188) per unit width is written as:

$\frac{q^2}{gy_1} + \frac{y_1^2}{2} = \frac{q^2}{gy_2} + \frac{y_2^2}{2}$

where $q$ is the discharge per unit width. This equation can be rearranged to relate the two conjugate depths. By introducing the upstream Froude number, $Fr_1 = q / \sqrt{gy_1^3}$, we arrive at the celebrated **Bélanger equation**:

$\frac{y_2}{y_1} = \frac{1}{2} \left( \sqrt{1 + 8Fr_1^2} - 1 \right)$

This equation is a cornerstone of hydraulic jump analysis, explicitly linking the geometry of the jump ($y_2/y_1$) to the dynamics of the incoming flow ($Fr_1$).

The principle of [specific force](@entry_id:266188) conservation is general and applies to any prismatic channel shape. For a non-rectangular channel, the algebra becomes more involved. For example, in a symmetric [trapezoidal channel](@entry_id:269134) with bottom width $b$ and side slopes $z:1$, applying $M_1=M_2$ leads to a more complex, implicit relationship for the conjugate depths. The required discharge $Q$ to produce a jump between depths $y_1$ and $y_2$ can be explicitly found [@problem_id:614229]:

$\frac{Q^2}{g} = \frac{y_1(b+z y_1) y_2(b+z y_2) \bigl[3b(y_1+y_2)+2z(y_1^2+y_1y_2+y_2^2)\bigr]}{6\bigl[b+z(y_1+y_2)\bigr]}$

For arbitrary channel shapes, the conjugate depth relationship must typically be solved numerically using the fundamental principle $M_1=M_2$.

### Surge Waves: The Moving Hydraulic Jump

When a hydraulic jump is not stationary but propagates through the fluid, it is known as a **[surge wave](@entry_id:185243)** or a **bore**. Examples include tidal bores advancing up [estuaries](@entry_id:192643) and waves generated by the sudden opening or closing of a [sluice gate](@entry_id:267992). Analyzing this unsteady phenomenon directly is complex. However, a powerful simplification is achieved by shifting into a **[moving frame](@entry_id:274518) of reference** that translates with the constant **celerity** (propagation speed), $c$, of the surge.

In this co-[moving frame](@entry_id:274518), the unsteady surge becomes a stationary hydraulic jump. The flow appears to approach the jump from upstream with velocity $u_1$ and exit downstream with velocity $u_2$. If the surge advances into quiescent water of depth $y_1$, the upstream velocity in the [moving frame](@entry_id:274518) is simply $u_1 = c$. The downstream fluid, which moves at velocity $v_2$ in the [laboratory frame](@entry_id:166991), will have a velocity of $u_2 = v_2 - c$ in the [moving frame](@entry_id:274518).

By applying the steady-state continuity and momentum equations across this stationary jump, we can derive the characteristics of the surge. This analysis can be performed using either a control volume fixed to the moving surge or by applying the impulse-[momentum principle](@entry_id:261235) to a fluid system in the stationary frame; both methods yield identical results [@problem_id:1796666]. The resulting expression for the surge celerity squared is:

$c^2 = \frac{g y_2}{2 y_1} (y_1 + y_2)$

This fundamental equation relates the propagation speed of the surge to the depths upstream and downstream of it. It notably shows that in the limit of an infinitesimally small wave ($y_2 \to y_1$), the celerity approaches $c \to \sqrt{gy_1}$, which is the speed of shallow water [gravity waves](@entry_id:185196).

Within this moving reference frame, we can analyze the flow properties just as we would for a stationary jump. For instance, we can determine the Froude number of the flow immediately downstream of the surge front, $Fr_2 = u_2 / \sqrt{gy_2}$. By combining the continuity and momentum relations, this can be expressed solely in terms of the surge strength, defined by the depth ratio $\eta = y_2 / y_1$ [@problem_id:549672]:

$Fr_2 = \sqrt{\frac{\eta+1}{2\eta^2}}$

This result demonstrates that for any surge of finite strength ($\eta > 1$), the downstream flow in the co-[moving frame](@entry_id:274518) is always subcritical ($Fr_2  1$), consistent with the properties of a [hydraulic jump](@entry_id:266212).

### Energy Dissipation in Hydraulic Jumps

A key feature of a [hydraulic jump](@entry_id:266212) is the significant loss of [mechanical energy](@entry_id:162989). While the [specific force](@entry_id:266188) is conserved (in the ideal case), the specific energy, $E = y + V^2/(2g)$, is not. The flow entering the jump has a high [specific energy](@entry_id:271007) ($E_1$), and the flow leaving has a lower specific energy ($E_2$). The difference, $\Delta E = E_1 - E_2$, is the **[head loss](@entry_id:153362)**, which is dissipated primarily through turbulence into thermal energy.

For a hydraulic jump in a rectangular channel, the [head loss](@entry_id:153362) can be derived using the continuity equation and the Bélanger equation. The result is a classic formula:

$\Delta E = \frac{(y_2 - y_1)^3}{4 y_1 y_2}$

This equation reveals that the [head loss](@entry_id:153362) is strongly dependent on the jump's strength, scaling with the cube of the depth difference.

To appreciate the magnitude of this dissipated energy, we can perform a thought experiment. Assuming all dissipated [mechanical energy](@entry_id:162989) is converted into internal thermal energy, we can calculate the resulting temperature rise, $\Delta T$. By equating the energy loss per unit mass, $g \Delta E$, to the change in thermal energy, $c_p \Delta T$, where $c_p$ is the [specific heat capacity](@entry_id:142129), we can express the temperature increase solely as a function of the upstream flow conditions [@problem_id:614242]:

$\Delta T = \frac{g y_1 \bigl(\sqrt{1+8 Fr_1^2}-3\bigr)^3}{16 c_p \bigl(\sqrt{1+8 Fr_1^2}-1\bigr)}$

While typically small for water under normal conditions, this demonstrates a direct physical consequence of the [energy dissipation](@entry_id:147406).

From a practical engineering perspective, the **rate of energy dissipation** (power dissipated), $\dot{E}_{diss} = \rho g q \Delta E$, is often the quantity of interest. Maximizing this rate is the primary goal of stilling basins. For a fixed upstream specific energy $E_1$, there exists an upstream Froude number $Fr_1$ that maximizes this [dissipation rate](@entry_id:748577). Through optimization, this value can be found to be $Fr_1 = \sqrt{\frac{11+5\sqrt{5}}{2}} \approx 3.33$ [@problem_id:614276].

The macroscopic [head loss](@entry_id:153362) is a manifestation of microscopic turbulent processes. The intense velocity gradients within the jump's roller region generate turbulence, which cascades down to smaller scales and is ultimately dissipated by viscosity. This can be modeled using turbulence theories, such as Prandtl's mixing-length model. By postulating a local dissipation rate per unit volume, $\mathcal{P}_V = \rho l_m^2 |dU/dy|^3$, and integrating over an approximated jump volume, one can obtain a "local" estimate of the total dissipation, $P_{local}$. Comparing this to the "global" [dissipation rate](@entry_id:748577), $P_{global} = \rho g Q \Delta E$, provides a bridge between the fluid mechanics of turbulence and the macroscopic energy balance of the jump [@problem_id:614215].

### Critical Flow and its Relation to Specific Force

We have previously defined **[critical flow](@entry_id:275258)** as the state where, for a given discharge, the specific energy is at its minimum. An alternative but equivalent definition can be made using the [specific force](@entry_id:266188). For a given discharge $Q$ in a prismatic channel, [critical flow](@entry_id:275258) occurs at the depth that corresponds to the **minimum [specific force](@entry_id:266188)**.

This can be proven by differentiating the [specific force](@entry_id:266188) equation with respect to depth $y$ and setting the result to zero, $dM/dy = 0$. This condition yields the criterion for [critical flow](@entry_id:275258):

$\frac{Q^2 T}{g A^3} = 1$

where $T$ is the top width of the channel at the free surface. The left side of this equation is the square of the Froude number for a general channel shape, so [critical flow](@entry_id:275258) corresponds to $Fr=1$.

This property provides a deeper understanding of the [specific force](@entry_id:266188) curve (a plot of $M$ versus $y$). The curve has two branches, one for supercritical flow and one for [subcritical flow](@entry_id:276823), which meet at the minimum point corresponding to [critical flow](@entry_id:275258). At this critical condition, there is a unique relationship between the [momentum flux](@entry_id:199796) component and the pressure force component of the [specific force](@entry_id:266188). For a channel whose shape is described by a power-law for the top width, $T(z) = C z^{\alpha}$, the ratio of the momentum flux term to the pressure force term at [critical flow](@entry_id:275258) is found to be [@problem_id:614288]:

$\frac{Q^2/(gA)}{\mathcal{P}} = \frac{\alpha+2}{\alpha+1}$

This elegant result shows that the partitioning of [specific force](@entry_id:266188) at the critical state depends only on the exponent $\alpha$ that defines the channel's geometry. For a rectangular channel ($\alpha=0$), the ratio is 2; for a triangular channel ($\alpha=1$), the ratio is $3/2$.

### Refinements to the Ideal Jump Theory

The analysis thus far has assumed an idealized [hydraulic jump](@entry_id:266212) in a horizontal, frictionless channel, where [specific force](@entry_id:266188) is perfectly conserved. In reality, factors such as channel slope and bed friction can play a significant role, especially for jumps that occur over a long distance.

Consider a steady jump on a long, wide rectangular channel with a constant bed slope $S_0$. The momentum balance must now include the component of the fluid's weight acting along the slope and the opposing force of bed friction, $F_f$. The momentum equation becomes:

$M_2 - M_1 = \frac{1}{g} \int_{x_1}^{x_2} (W_x - F_f) dx$

This shows that the [specific force](@entry_id:266188) is no longer conserved ($M_2 \neq M_1$). It increases if the weight component dominates friction ($S_0 > S_f$) and decreases if friction dominates ($S_0  S_f$).

To obtain a tractable analytical result, we can employ engineering approximations for the forces. The weight component can be based on an average depth, and the [friction force](@entry_id:171772) can be modeled using an effective [friction slope](@entry_id:265665) $\bar{S}_f$ based on the Chezy formula. Applying these approximations allows for the derivation of the ratio of downstream to upstream [specific force](@entry_id:266188), which quantifies the deviation from the ideal case [@problem_id:614269]. A possible expression for this ratio is:

$\frac{M_2}{M_1} = 1 + \frac{\lambda (1+\eta)}{2 Fr_1^2 + 1} \left( S_0 - \frac{k g Fr_1^2}{2 C^2} \frac{\eta^3+1}{\eta^3} \right)$

where $\lambda$ is a dimensionless jump length, $\eta$ is the depth ratio, $C$ is the Chezy coefficient, and $k$ is an empirical factor. This equation highlights how the bed slope $S_0$ acts to increase $M_2$, while friction (the term with $1/C^2$) acts to decrease it. This refined model provides a more accurate picture of hydraulic jumps in natural and engineered channels, demonstrating that the [specific force](@entry_id:266188) concept is a powerful tool within a more general momentum balance framework.