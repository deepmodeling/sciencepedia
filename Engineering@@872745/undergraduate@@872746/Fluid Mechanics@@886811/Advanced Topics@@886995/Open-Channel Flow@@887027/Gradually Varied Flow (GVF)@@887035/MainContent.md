## Introduction
In the world of fluid mechanics, the flow of water in open channels like rivers, canals, and spillways rarely maintains a constant depth. More often, the water surface gently rises or falls over long distances in response to changes in channel geometry, roughness, or slope. This phenomenon, known as Gradually Varied Flow (GVF), is fundamental to [hydraulic engineering](@entry_id:184767) and environmental science. The central challenge for engineers and scientists is to predict the shape of this [water surface profile](@entry_id:270649) to design effective water conveyance systems, assess flood risks, and manage river ecosystems. This article provides a foundational understanding of GVF, bridging theory with practical application. The first chapter, "Principles and Mechanisms," will derive the core governing equation from first principles and introduce a systematic framework for classifying flow profiles. Following this, "Applications and Interdisciplinary Connections" will explore how these principles are used to solve real-world problems, from designing canals to modeling complex environmental dynamics. Finally, "Hands-On Practices" offers exercises to reinforce these concepts and develop practical analytical skills.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of Gradually Varied Flow (GVF) as a prevalent condition in natural and engineered open channels where the flow depth changes slowly along the direction of flow. This chapter delves into the fundamental principles that govern this phenomenon. We will derive the master differential equation that describes the [water surface profile](@entry_id:270649), explore the key hydraulic parameters that control its behavior, and establish a systematic framework for classifying and analyzing these profiles.

### The Governing Equation of Gradually Varied Flow

The foundation for analyzing gradually varied flow is the principle of [conservation of energy](@entry_id:140514). For an open channel, the total energy head $H$ at any cross-section, measured relative to a fixed horizontal datum, is the sum of the elevation head of the channel bed ($z_b$), the flow depth ($y$), and the velocity head ($V^2/(2g)$).

$$ H = z_b + y + \frac{V^2}{2g} $$

where $V$ is the average flow velocity and $g$ is the acceleration due to gravity. As water flows downstream, it loses energy due to friction between the fluid and the channel boundaries. The slope of the total energy line, known as the **[friction slope](@entry_id:265665)** or **energy slope** ($S_f$), represents this head loss per unit length of the channel. By definition, $S_f = -dH/dx$, where $x$ is the longitudinal distance along the channel.

Differentiating the total head equation with respect to $x$ gives:

$$ \frac{dH}{dx} = \frac{dz_b}{dx} + \frac{dy}{dx} + \frac{d}{dx}\left(\frac{V^2}{2g}\right) $$

The term $dz_b/dx$ represents the slope of the channel bed. It is conventional to define the bed slope $S_0$ as positive for a downward-sloping channel, so $S_0 = -dz_b/dx$. Substituting this and the definition of $S_f$ yields:

$$ -S_f = -S_0 + \frac{dy}{dx} + \frac{d}{dx}\left(\frac{V^2}{2g}\right) $$

Rearranging this equation provides a profound insight into the [energy balance](@entry_id:150831). The term $y + V^2/(2g)$ is defined as the **specific energy**, $E$, which represents the energy per unit weight of fluid relative to the channel bed.

$$ E = y + \frac{V^2}{2g} $$

The change in [specific energy](@entry_id:271007) along the channel is therefore:

$$ \frac{dE}{dx} = \frac{dy}{dx} + \frac{d}{dx}\left(\frac{V^2}{2g}\right) = S_0 - S_f $$

This crucial relationship reveals that the specific energy of the flow changes based on the balance between the energy supplied by the bed slope ($S_0$) and the energy dissipated by friction ($S_f$). If the bed slope is steeper than the [friction slope](@entry_id:265665) ($S_0 > S_f$), the [specific energy](@entry_id:271007) increases in the direction of flow; if the bed slope is milder ($S_0 < S_f$), the specific energy decreases [@problem_id:1760969].

To obtain an equation for the water surface slope, $dy/dx$, we must express $dE/dx$ in terms of $dy/dx$. Using the chain rule, we have $\frac{dE}{dx} = \frac{dE}{dy} \frac{dy}{dx}$. The term $dE/dy$ represents the rate of change of specific energy with respect to flow depth. For a channel of arbitrary shape carrying a constant discharge $Q$, we have $V = Q/A$, where the cross-sectional area $A$ is a function of $y$. Differentiating the [specific energy](@entry_id:271007) equation gives:

$$ \frac{dE}{dy} = \frac{d}{dy}\left(y + \frac{Q^2}{2gA^2}\right) = 1 - \frac{Q^2}{gA^3}\frac{dA}{dy} $$

Recognizing that the top width of the channel is $T = dA/dy$, and the Froude number is defined by $Fr^2 = Q^2T/(gA^3)$, we arrive at a remarkably compact result:

$$ \frac{dE}{dy} = 1 - Fr^2 $$

This shows that the term $1 - Fr^2$ is not merely a mathematical factor but has a distinct physical meaning: it is the dimensionless rate of change of specific energy with respect to flow depth [@problem_id:1760948].

By equating the two expressions for $dE/dx$, we get $(1 - Fr^2) \frac{dy}{dx} = S_0 - S_f$. Solving for $dy/dx$ gives the general differential equation for gradually varied flow:

$$ \frac{dy}{dx} = \frac{S_0 - S_f}{1 - Fr^2} $$

This is the central equation of GVF analysis. It describes how the water depth $y$ changes with longitudinal distance $x$. To use this equation, we need expressions for the [friction slope](@entry_id:265665) $S_f$ and the Froude number $Fr$. The Froude number depends only on the channel geometry and discharge, but the [friction slope](@entry_id:265665) must be estimated using an empirical resistance formula, such as the Manning or Chezy equations. For instance, using the Chezy equation $V = C \sqrt{R S_f}$ (where $C$ is the Chezy coefficient and $R$ is the [hydraulic radius](@entry_id:265684)), the [friction slope](@entry_id:265665) can be written as $S_f = V^2 / (C^2 R)$. For a wide rectangular channel where $R \approx y$ and $V = q/y$ (with $q$ being discharge per unit width), the GVF equation becomes [@problem_id:1798130]:

$$ \frac{dy}{dx} = \frac{S_{0} - \frac{q^{2}}{C^{2} y^{3}}}{1 - \frac{q^{2}}{g y^{3}}} $$

Regardless of the specific resistance formula used, the structure of the GVF equation remains the same, governed by the balance in the numerator and the flow regime in the denominator.

### Characterizing the Flow: Normal and Critical Depths

The behavior of the GVF equation is entirely determined by the numerator ($S_0 - S_f$) and the denominator ($1 - Fr^2$). These two terms are controlled by two fundamental flow depths: the **[normal depth](@entry_id:265980)** and the **[critical depth](@entry_id:275576)**.

The **[normal depth](@entry_id:265980)**, denoted by $y_n$, is the hypothetical depth at which the flow would be uniform for a given discharge and channel configuration. Uniform flow is characterized by a constant depth, meaning $dy/dx=0$. From the GVF equation, this occurs when the numerator is zero, i.e., $S_f = S_0$. The [friction slope](@entry_id:265665) equals the bed slope, indicating a perfect balance between the gravitational force driving the flow and the frictional forces resisting it. For any given $Q$, $S_0$, and channel roughness (e.g., Manning's $n$), there is a unique [normal depth](@entry_id:265980) $y_n$ that can be found by solving the Manning equation for $y$:

$$ Q = \frac{1}{n} A(y_n) R(y_n)^{2/3} S_0^{1/2} $$

The **[critical depth](@entry_id:275576)**, denoted by $y_c$, is the depth at which the Froude number is exactly 1. At this depth, the denominator of the GVF equation becomes zero. The condition $Fr = 1$ is equivalent to $dE/dy = 0$, meaning the specific energy is at a minimum for a given discharge. The equation defining $y_c$ is purely a function of geometry and discharge:

$$ \frac{Q^2 T(y_c)}{g A(y_c)^3} = 1 $$

The [critical depth](@entry_id:275576) is a crucial benchmark that separates two distinct [flow regimes](@entry_id:152820):
- **Subcritical flow**: $y > y_c$, which means $Fr < 1$. The denominator $1 - Fr^2$ is positive. Flow is tranquil and relatively deep.
- **Supercritical flow**: $y < y_c$, which means $Fr > 1$. The denominator $1 - Fr^2$ is negative. Flow is rapid and relatively shallow.

A critical point of analysis is the behavior of the GVF equation when the flow depth approaches the [critical depth](@entry_id:275576) ($y \to y_c$). As the denominator $1 - Fr^2$ approaches zero, the water surface slope $dy/dx$ will approach infinity, unless the numerator $S_0 - S_f$ simultaneously approaches zero. In the general case where flow passes through [critical depth](@entry_id:275576) at a location where flow is not uniform (i.e., $S_f \neq S_0$), the GVF equation predicts a vertical water surface. This is a physical impossibility and signals a breakdown of the underlying assumption of "gradual" variation. In reality, the flow becomes rapidly varied in the vicinity of the [critical depth](@entry_id:275576), with strong [streamline](@entry_id:272773) curvature and a non-hydrostatic pressure distribution, phenomena not captured by the GVF model [@problem_id:1760971].

### Classification of Slopes and Water Surface Profiles

The hydraulic character of a channel is determined by the relationship between its [normal depth](@entry_id:265980) ($y_n$) and [critical depth](@entry_id:275576) ($y_c$). This relationship dictates the type of uniform flow the channel can sustain and forms the basis for a comprehensive classification system for GVF profiles.

A channel slope is classified as follows:
- **Mild (M) Slope**: A slope where $y_n > y_c$. In its natural state of [uniform flow](@entry_id:272775), the channel supports [subcritical flow](@entry_id:276823). This is the most common type of slope in rivers and large canals.
- **Steep (S) Slope**: A slope where $y_n < y_c$. The uniform flow in such a channel is supercritical. These are found in mountain rivers, spillways, and specially designed high-speed channels.
- **Critical (C) Slope**: A special case where $y_n = y_c$. Uniform flow occurs at exactly the [critical depth](@entry_id:275576).
- **Horizontal (H) Slope**: A slope where $S_0 = 0$. For such a slope, uniform flow is impossible (unless the fluid is frictionless), so $y_n$ is infinite.
- **Adverse (A) Slope**: A slope where $S_0 < 0$ (i.e., the channel bed slopes uphill). Uniform flow is impossible, and $y_n$ is not defined.

The transition between a mild and a steep slope occurs at the **critical slope**, $S_c$, which is the bed slope that results in $y_n = y_c$. We can derive an expression for $S_c$ by setting the depth in the Manning equation to the [critical depth](@entry_id:275576) $y_c$. For a wide rectangular channel, for instance, where $y_c = (q^2/g)^{1/3}$ and the [hydraulic radius](@entry_id:265684) $R \approx y$, the critical slope is found to be $S_c = n^2 g^{10/9} q^{-2/9}$ [@problem_id:1760963]. An engineer can thus determine if a proposed [channel design](@entry_id:272187) is hydraulically steep or mild by comparing its bed slope $S_0$ to the calculated critical slope $S_c$. If $S_0 > S_c$, the slope is steep; if $S_0 < S_c$, the slope is mild. This classification is vital for predicting flow behavior, as demonstrated in the design of various channel shapes, from rectangular flumes to V-shaped ditches [@problem_id:1760970].

Once the slope is classified, the [water surface profile](@entry_id:270649) itself is categorized based on the actual flow depth $y$ relative to $y_n$ and $y_c$. A number from 1 to 3 is appended to the slope letter (M, S, etc.):
- **Zone 1**: $y > y_n$ and $y > y_c$. The flow depth is above both normal and critical depths.
- **Zone 2**: $y$ is between $y_n$ and $y_c$.
- **Zone 3**: $y < y_n$ and $y < y_c$. The flow depth is below both normal and critical depths.

This system gives rise to various profile types, such as M1, M2, M3, S1, S2, S3, etc., each with a unique shape and character.

### Qualitative Analysis of Water Surface Profiles

The GVF equation is a powerful tool for predicting the qualitative shape of the water surface. By simply examining the signs of the numerator ($S_0 - S_f$) and the denominator ($1 - Fr^2$), we can determine whether the water depth increases or decreases with distance.

The sign analysis proceeds as follows:
- **Numerator ($S_0 - S_f$):** Since [friction slope](@entry_id:265665) $S_f$ is a decreasing function of depth $y$ (for a given $Q$), we have:
    - If $y > y_n$, then $S_f < S_0 \implies S_0 - S_f > 0$.
    - If $y < y_n$, then $S_f > S_0 \implies S_0 - S_f < 0$.
- **Denominator ($1 - Fr^2$):** Since the Froude number $Fr$ is a decreasing function of depth $y$, we have:
    - If $y > y_c$ (subcritical), then $Fr < 1 \implies 1 - Fr^2 > 0$.
    - If $y < y_c$ (supercritical), then $Fr > 1 \implies 1 - Fr^2 < 0$.

Let us apply this to understand a specific profile, the **M3 profile**. This occurs on a mild slope ($y_n > y_c$) when the flow depth is in Zone 3, meaning $y < y_c$. A common example is the flow emerging from under a [sluice gate](@entry_id:267992) into a mild channel. For this profile, the conditions are $y < y_c < y_n$.
- Numerator: Since $y < y_n$, we have $S_f > S_0$, so $S_0 - S_f < 0$.
- Denominator: Since $y < y_c$, the flow is supercritical, so $1 - Fr^2 < 0$.

Therefore, the water surface slope is:
$$ \frac{dy}{dx} = \frac{S_0 - S_f}{1 - Fr^2} = \frac{(\text{negative})}{(\text{negative})} > 0 $$

The depth increases in the downstream direction. The flow, initially supercritical, attempts to approach the subcritical state dictated by the mild slope. As $y$ increases towards $y_c$, the denominator approaches zero, causing $dy/dx$ to approach $+\infty$. This means the M3 profile terminates abruptly at the [critical depth](@entry_id:275576), typically in a hydraulic jump that provides a rapid transition to [subcritical flow](@entry_id:276823). Further analysis shows the profile is concave up, as the water surface becomes progressively steeper as it approaches the [critical depth](@entry_id:275576) line [@problem_id:1760959]. Similar analysis can be performed for all other profile types to build a complete picture of GVF behavior.

### Control Sections and Information Propagation

To compute a specific GVF profile, one must start the calculation from a point where the flow depth is known. Such a location is called a **control section**. The nature of controls is fundamentally tied to the Froude number and the direction in which information (in the form of small disturbances) can propagate.

In **[subcritical flow](@entry_id:276823) ($Fr < 1$)**, the wave celerity is greater than the flow velocity. This allows small disturbances to travel both upstream and downstream. Consequently, [subcritical flow](@entry_id:276823) is controlled by downstream conditions. A dam, a weir, or the elevation of a lake into which a river flows acts as a downstream control. The [water surface profile](@entry_id:270649) is determined by integrating the GVF equation *upstream* from this known downstream depth.

In **supercritical flow ($Fr > 1$)**, the flow velocity is greater than the wave celerity. Small disturbances are swept away and can only travel downstream. This means that supercritical flow is insensitive to downstream conditions and is governed by upstream controls. An upstream control is typically a location where flow passes through [critical depth](@entry_id:275576), such as the entrance to a steep channel from a reservoir or flow emerging from under a [sluice gate](@entry_id:267992). The GVF profile is determined by integrating the GVF equation *downstream* from this known upstream depth.

This principle has profound practical implications. For example, consider a long, uniform channel with supercritical flow. If a smooth, low-profile bump is placed on the channel bed, this downstream obstruction will not affect the flow depth upstream of it, provided the bump is not large enough to "choke" the flow and force a [hydraulic jump](@entry_id:266212) to form upstream. The flow passes over the bump, adjusting its depth locally, but the upstream conditions remain governed by the upstream control section, completely unaware of the downstream feature. The water depth just upstream of the bump will be the same whether the bump is present or not [@problem_id:1760965]. This is in stark contrast to [subcritical flow](@entry_id:276823), where the same bump would cause the water level to rise for a considerable distance upstream, a phenomenon known as backwater.

### Extensions and Limitations of the One-Dimensional Model

The classical GVF equation assumes a prismatic channel with constant discharge. However, the framework can be extended to more complex scenarios.

A significant extension is to **Spatially Varied Flow (SVF)**, where the discharge $Q$ changes along the length of the channel, $x$. This occurs in side-channel spillways (inflow) or in irrigation canals with constant water withdrawal or infiltration into the bed (outflow). The change in discharge introduces an additional term related to the momentum flux of the water being added or removed. The governing equation becomes:

$$ \frac{dy}{dx} = \frac{S_0 - S_f - \frac{V}{gA}\frac{dQ}{dx}}{1 - Fr^2} $$

The new term in the numerator, $-\frac{V}{gA}\frac{dQ}{dx}$, accounts for the momentum change. For an infiltrating channel where water is lost, $dQ/dx$ is negative, making this term positive and thus contributing to a milder water surface slope (or a greater rate of depth increase) than would otherwise be expected [@problem_id:1760944].

Despite its power and versatility, it is crucial to recognize the limitations of the one-dimensional GVF model. The model is built on the assumption that streamlines are nearly parallel and the pressure distribution is hydrostatic. This assumption is violated in regions of high streamline curvature. A prominent example is the flow in a channel bend. Centrifugal forces acting on the fluid create a transverse pressure gradient, causing the water surface to be higher at the outer wall and lower at the inner wall—a phenomenon known as **superelevation**. This is an inherently two-dimensional effect. While one can estimate the magnitude of this transverse slope, its presence means the water surface is not truly one-dimensional, complicating the direct application of the GVF equation and highlighting the boundaries of the model's validity [@problem_id:1760945]. In such cases, or in situations involving very rapid changes in geometry, more complex two- or three-dimensional models may be required for an accurate analysis.