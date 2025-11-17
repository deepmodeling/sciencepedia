## Introduction
Flows with a free surface, from natural rivers to engineered canals, are ubiquitous in our environment and essential to civil infrastructure. Unlike contained [pipe flow](@entry_id:189531), these open-channel flows are governed by a complex interplay of gravity, inertia, and friction, requiring a distinct analytical framework. This article addresses the fundamental need for this framework by systematically explaining the principles that dictate the behavior of water in open channels. It aims to bridge the gap between basic [fluid mechanics](@entry_id:152498) and the specialized field of [open-channel hydraulics](@entry_id:273093).

This article is structured to build your expertise progressively. In the first chapter, **Principles and Mechanisms**, you will master the core concepts of [specific energy](@entry_id:271007), [critical flow](@entry_id:275258), and the [momentum principle](@entry_id:261235). Next, **Applications and Interdisciplinary Connections** will demonstrate how these theories are applied to design hydraulic structures and understand river systems. Finally, **Hands-On Practices** will allow you to solidify your knowledge by tackling practical problems. By the end, you will have a robust understanding of how to analyze and predict the behavior of open-channel flows.

## Principles and Mechanisms

Open-channel flow, characterized by a free surface exposed to [atmospheric pressure](@entry_id:147632), encompasses the vast majority of water movement on the Earth's surface, from small rivulets to mighty rivers. Unlike pressurized [pipe flow](@entry_id:189531), where the fluid is confined by solid boundaries on all sides, the free surface of an [open-channel flow](@entry_id:267863) allows for complex interactions between gravitational, inertial, and frictional forces. This chapter delves into the fundamental principles of energy and momentum that govern these flows, establishing a rigorous framework for their analysis.

### Geometrical Properties of Open Channels

The analysis of [open-channel flow](@entry_id:267863) begins with a precise characterization of the channel's geometry. For a given flow, the primary parameters are the **flow depth** ($y$), the **cross-sectional area** of the flow ($A$), and the **[wetted perimeter](@entry_id:268581)** ($P$), which is the length of the channel boundary in contact with the fluid. These three parameters are not independent and their relationship is dictated by the channel's shape.

From these fundamental properties, we derive a crucial parameter known as the **[hydraulic radius](@entry_id:265684)**, $R_h$, defined as the ratio of the flow area to the [wetted perimeter](@entry_id:268581):

$$R_h = \frac{A}{P}$$

The [hydraulic radius](@entry_id:265684) serves as the characteristic length scale for flow resistance. It quantifies the efficiency of a channel in conveying flow; for a given cross-sectional area, a larger [hydraulic radius](@entry_id:265684) implies a smaller [wetted perimeter](@entry_id:268581) and consequently, less frictional resistance from the channel walls and bed.

To illustrate this concept, consider a simple, yet common, geometry: a circular culvert of diameter $D$ flowing exactly half-full [@problem_id:1765931]. The flow area $A$ is that of a semicircle, $A = \frac{1}{2} \left( \frac{\pi D^2}{4} \right) = \frac{\pi D^2}{8}$. The [wetted perimeter](@entry_id:268581) $P$ is the length of the semicircular arc, $P = \frac{1}{2}(\pi D) = \frac{\pi D}{2}$. The [hydraulic radius](@entry_id:265684) is therefore:

$$R_h = \frac{A}{P} = \frac{\pi D^2 / 8}{\pi D / 2} = \frac{D}{4}$$

Interestingly, this is the same [hydraulic radius](@entry_id:265684) as a circular pipe flowing full ($A = \pi D^2 / 4$, $P = \pi D$, so $R_h = D/4$). However, this equivalence does not hold for other filling depths.

The significance of the [hydraulic radius](@entry_id:265684) is highlighted when comparing the energy losses in [open-channel flow](@entry_id:267863) to those in [pipe flow](@entry_id:189531). The energy loss due to friction over a length of channel is quantified by the **[friction slope](@entry_id:265665)** or **energy gradient**, $S_f$. Based on a force balance between pressure, gravity, and shear stress, the [friction slope](@entry_id:265665) can be expressed using the Darcy-Weisbach formulation as:

$$S_f = \frac{f}{8g} \frac{V^2}{R_h}$$

where $f$ is the Darcy friction factor, $V$ is the mean flow velocity, and $g$ is the acceleration due to gravity. This equation shows that for a given velocity and friction factor, the energy slope is inversely proportional to the [hydraulic radius](@entry_id:265684). A channel with a smaller [hydraulic radius](@entry_id:265684) will experience a steeper energy gradient, signifying greater energy loss per unit length. A hypothetical comparison between a wide, rectangular open channel and a full-flowing circular pipe, designed to carry the same flow rate with the same cross-sectional area, material roughness, and friction factor, would demonstrate that the ratio of their energy slopes is simply the inverse ratio of their hydraulic radii ($S_{f,c}/S_{f,p} = R_{h,p}/R_{h,c}$) [@problem_id:1765945].

### The Principle of Specific Energy

A cornerstone of [open-channel flow](@entry_id:267863) analysis is the concept of **[specific energy](@entry_id:271007)**, denoted by $E$. It is defined as the energy head per unit weight of fluid, measured relative to the channel bottom as the datum. For a channel with a small bed slope, the specific energy is the sum of two components: the potential energy associated with the depth of flow, and the kinetic energy of the moving fluid.

$$E = y + \frac{V^2}{2g}$$

Here, $y$ is the flow depth, and the term $\frac{V^2}{2g}$ is the **velocity head**. This simple equation is a powerful tool for understanding flow behavior. For instance, if sensors in a triangular irrigation channel measure a specific energy of $E = 1.15$ m and a depth of $y = 0.80$ m, we can directly calculate the velocity head as $E - y = 0.35$ m. This allows us to find the velocity $V = \sqrt{2g(E-y)}$ and, if the channel geometry is known, the total discharge $Q = A \cdot V$ [@problem_id:1765904].

The relationship between [specific energy](@entry_id:271007) and depth for a fixed discharge $Q$ reveals fundamental characteristics of [open-channel flow](@entry_id:267863). By substituting $V = Q/A$ into the [specific energy](@entry_id:271007) equation, where the area $A$ is a function of depth $y$, we get:

$$E = y + \frac{Q^2}{2gA(y)^2}$$

A plot of $E$ versus $y$ for a constant $Q$ yields a characteristic **[specific energy curve](@entry_id:263440)**. This curve shows that for any given [specific energy](@entry_id:271007) value greater than a certain minimum, there are two possible depths at which the flow can occur. These two depths are known as **[alternate depths](@entry_id:193161)**.

*   The greater depth, $y_{sub}$, corresponds to a low velocity. This flow regime is termed **[subcritical flow](@entry_id:276823)**.
*   The smaller depth, $y_{super}$, corresponds to a high velocity. This flow regime is termed **supercritical flow**.

For example, for a rectangular channel with a width of $2.00$ m carrying a discharge of $18.79$ m³/s, a [specific energy](@entry_id:271007) of $3.50$ m corresponds to two [alternate depths](@entry_id:193161): a subcritical depth of $3.00$ m and a supercritical depth of $1.50$ m [@problem_id:1765884]. To find these depths, one must solve the cubic equation $y^3 - E y^2 + Q^2/(2gb^2) = 0$ for $y$.

### Critical Flow: The Nexus of Energy and Discharge

The [specific energy curve](@entry_id:263440) reveals a point of special significance: the point of minimum specific energy, $E_{min}$. The depth at which this minimum occurs is called the **[critical depth](@entry_id:275576)**, $y_c$, and the corresponding flow state is **[critical flow](@entry_id:275258)**. At this point, the two [alternate depths](@entry_id:193161) merge into one.

The condition for [critical depth](@entry_id:275576) can be found by differentiating the [specific energy](@entry_id:271007) equation with respect to $y$ (for a constant $Q$) and setting the derivative to zero:

$$\frac{dE}{dy} = \frac{d}{dy} \left( y + \frac{Q^2}{2gA^2} \right) = 1 - \frac{Q^2}{gA^3} \frac{dA}{dy} = 0$$

Since for any prismatic channel, a small change in area $dA$ is related to a small change in depth $dy$ by $dA = T dy$, where $T$ is the top width of the water surface, we have $\frac{dA}{dy} = T$. Substituting this into the equation gives the general condition for [critical flow](@entry_id:275258):

$$\frac{Q^2 T_c}{g A_c^3} = 1$$

where the subscript 'c' denotes values at the critical condition. This single equation is a universal criterion for [critical flow](@entry_id:275258) in any open channel of arbitrary shape [@problem_id:467782].

Critical flow is not only the state of minimum specific energy for a given discharge, but it is also the state of **maximum discharge** for a given specific energy. By rearranging the specific energy equation to solve for $Q$ and finding the depth $y$ that maximizes $Q$ for a fixed $E$, one arrives at the same [critical flow](@entry_id:275258) condition. Under this condition of maximum discharge, it can be shown that the velocity head is directly related to the channel's geometry [@problem_id:1765906]:

$$\left(\frac{V^2}{2g}\right)_c = \frac{A_c}{2T_c}$$

This duality underscores the central role of [critical flow](@entry_id:275258) as a control point in [open-channel hydraulics](@entry_id:273093), often occurring at weirs, sluice gates, and channel outfalls.

### The Froude Number and the Celerity of Surface Waves

The [critical flow](@entry_id:275258) condition can be expressed more elegantly using a dimensionless parameter, the **Froude number**, $Fr$. The Froude number is defined as the ratio of the mean flow velocity $V$ to the celerity (speed) of a small-amplitude surface wave, $c$.

$$Fr = \frac{V}{c}$$

For a channel of arbitrary shape, the wave celerity is given by $c = \sqrt{gD}$, where $D = A/T$ is the **hydraulic depth**. Therefore, the Froude number is:

$$Fr = \frac{V}{\sqrt{gD}} = \frac{Q/A}{\sqrt{gA/T}} = \sqrt{\frac{Q^2 T}{g A^3}}$$

Comparing this with the [critical flow](@entry_id:275258) criterion, we see that [critical flow](@entry_id:275258) is simply the condition where the Froude number is unity:

$$Fr = 1 \quad \text{(Critical Flow)}$$

The physical meaning of the Froude number is profound. It represents the ratio of inertial forces to gravitational forces.
*   When $Fr  1$ (**[subcritical flow](@entry_id:276823)**), the flow velocity is less than the wave celerity. Disturbances can propagate both upstream and downstream. This corresponds to the deep, tranquil flow on the upper limb of the [specific energy curve](@entry_id:263440).
*   When $Fr > 1$ (**supercritical flow**), the flow velocity is greater than the wave celerity. Disturbances cannot travel upstream; they are swept downstream. This corresponds to the shallow, rapid flow on the lower limb of the [specific energy curve](@entry_id:263440).

A simple thought experiment illustrates this principle. If a pebble is dropped into a stream, it creates ripples that expand outwards at the wave celerity $c$ relative to the water. If the stream's velocity $V$ is greater than $c$ (supercritical flow, $Fr>1$), even the part of the ripple attempting to move upstream will be washed downstream relative to a stationary observer on the bank [@problem_id:1765903].

### Momentum Principle and the Hydraulic Jump

While the [energy principle](@entry_id:748989) is invaluable for analyzing gradual changes in flow, it is insufficient for situations involving rapid changes and significant energy loss. A prime example is the **hydraulic jump**, an abrupt transition from a supercritical flow to a [subcritical flow](@entry_id:276823), characterized by intense turbulence and [energy dissipation](@entry_id:147406).

Across a hydraulic jump, mechanical energy is not conserved. Instead, the analysis relies on the conservation of momentum. Applying Newton's second law to a [control volume](@entry_id:143882) encompassing the jump leads to the **momentum function**, $M$, which is conserved across the jump (assuming a horizontal channel and negligible friction):

$$M = A\bar{z} + \frac{Q^2}{gA}$$

where $\bar{z}$ is the distance from the free surface to the [centroid](@entry_id:265015) of the flow area $A$. For a given discharge $Q$, the depths upstream ($y_1$) and downstream ($y_2$) of a hydraulic jump must satisfy $M(y_1) = M(y_2)$. These two depths are known as **conjugate depths** or **sequent depths**.

It is critical to distinguish conjugate depths from [alternate depths](@entry_id:193161). Alternate depths ($y_1, y_a$) share the same specific energy ($E(y_1) = E(y_a)$). In contrast, conjugate depths ($y_1, y_2$) share the same momentum function ($M(y_1) = M(y_2)$). Due to the turbulent [energy dissipation](@entry_id:147406) within the jump, the specific energy of the downstream flow is always less than that of the upstream flow ($E_2  E_1$). Therefore, the downstream conjugate depth $y_2$ is not the same as the alternate depth $y_a$ corresponding to the initial depth $y_1$. Since $E_a = E_1$ by definition, it follows directly that $E_2  E_a$ [@problem_id:1734028]. The [hydraulic jump](@entry_id:266212) represents a transition between conjugate depths, not [alternate depths](@entry_id:193161), and is an irreversible process.

### Governing Equation for Gradually Varied Flow

Away from abrupt transitions like hydraulic jumps, flow depth often changes slowly and continuously along the length of a channel. This is known as **[gradually varied flow](@entry_id:264271) (GVF)**. The behavior of the [water surface profile](@entry_id:270649) in GVF is described by a fundamental differential equation.

We start with the total energy head $H$ relative to a fixed datum:

$$H = z_b + y + \frac{V^2}{2g}$$

where $z_b$ is the elevation of the channel bed. The change in total head with distance along the channel, $x$, is equal to the negative of the [friction slope](@entry_id:265665): $\frac{dH}{dx} = -S_f$. Differentiating the [energy equation](@entry_id:156281) with respect to $x$ gives:

$$\frac{dH}{dx} = \frac{dz_b}{dx} + \frac{dy}{dx} + \frac{d}{dx}\left(\frac{V^2}{2g}\right)$$

The term $\frac{dz_b}{dx}$ is the bed slope, which is defined as negative in the direction of falling elevation, so $\frac{dz_b}{dx} = -S_0$. Using the chain rule, the kinetic energy term becomes $\frac{d}{dx}\left(\frac{V^2}{2g}\right) = -Fr^2 \frac{dy}{dx}$. Substituting these into the differentiated energy equation:

$$-S_f = -S_0 + \frac{dy}{dx} - Fr^2 \frac{dy}{dx}$$

Rearranging to solve for the water surface slope, $\frac{dy}{dx}$, yields the governing equation for [gradually varied flow](@entry_id:264271) [@problem_id:549621] [@problem_id:1765886]:

$$\frac{dy}{dx} = \frac{S_0 - S_f}{1 - Fr^2}$$

This powerful equation reveals how the [water surface profile](@entry_id:270649) evolves. The numerator, $S_0 - S_f$, represents the net "[energy grade line](@entry_id:273452) slope" relative to the bed. If the bed slope $S_0$ is steeper than the [friction slope](@entry_id:265665) $S_f$, the flow has a surplus of energy and tends to accelerate (depth decreases). If $S_f > S_0$, the flow has an energy deficit and tends to decelerate (depth increases). The denominator, $1 - Fr^2$, acts as a control term. For [subcritical flow](@entry_id:276823) ($Fr  1$), the denominator is positive, and the water surface behavior follows the [energy balance](@entry_id:150831) in the numerator. For supercritical flow ($Fr > 1$), the denominator is negative, and the surface profile behavior is inverted.

Consider a [subcritical flow](@entry_id:276823) approaching a free overfall, or waterfall. The depth is observed to decrease, so $\frac{dy}{dx}  0$. Since the flow is subcritical, $1-Fr^2 > 0$. For the entire fraction to be negative, the numerator must be negative, meaning $S_0 - S_f  0$, or $S_f > S_0$. This indicates that as the water approaches the fall and accelerates, the frictional losses per unit length become greater than the energy supplied by the bed slope [@problem_id:1765886]. This single equation, combining geometric, energy, and resistance principles, is the key to predicting and analyzing the vast array of water surface profiles found in natural and engineered open channels.