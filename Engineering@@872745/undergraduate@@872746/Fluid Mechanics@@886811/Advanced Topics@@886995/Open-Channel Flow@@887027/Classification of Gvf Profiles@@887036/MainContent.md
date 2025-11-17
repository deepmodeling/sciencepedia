## Introduction
In the study of [open-channel hydraulics](@entry_id:273093), understanding how water surfaces vary along a channel is paramount for effective engineering design and environmental management. While the concept of uniform flow provides a simplified baseline, real-world flows are seldom uniform. Instead, they are typically **gradually varied flows (GVF)**, where the water depth changes subtly along the channel's length due to an imbalance between gravitational and frictional forces. This complexity gives rise to a variety of water surface profiles, and a systematic method is needed to predict and analyze their behavior.

This article provides a foundational guide to the classification of these GVF profiles. It addresses the fundamental need for a structured framework to interpret water surface behavior in rivers, canals, and hydraulic structures. By mastering this classification, you will gain the ability to predict how water levels respond to changes in channel geometry, roughness, and downstream or upstream control conditions.

Throughout the following sections, you will build a complete understanding of this topic. First, the **"Principles and Mechanisms"** section will derive the governing equation of GVF and introduce the key concepts of normal and [critical depth](@entry_id:275576), which form the basis for the entire classification system. Next, **"Applications and Interdisciplinary Connections"** will bridge theory and practice by showcasing how GVF analysis is used to solve real-world problems in civil engineering, [hydrology](@entry_id:186250), and [geomorphology](@entry_id:182022). Finally, the **"Hands-On Practices"** section will provide an opportunity to solidify your learning by working through targeted problems. We begin by exploring the core principles that govern the shape and behavior of all gradually varied flows.

## Principles and Mechanisms

The transition from the idealized state of [uniform flow](@entry_id:272775) to the more complex reality of **[gradually varied flow](@entry_id:264271) (GVF)** marks a significant step in understanding [open-channel hydraulics](@entry_id:273093). While [uniform flow](@entry_id:272775) assumes a perfect balance between gravitational and frictional forces, GVF describes the much more common scenario where the flow depth changes gradually along the length of a channel. This variation is driven by an imbalance between these forces, leading to a rich variety of water surface profiles. Understanding the principles that govern these profiles is fundamental to the design and analysis of canals, rivers, and spillways. The classification of these profiles provides a systematic framework for predicting and interpreting the behavior of water in open channels.

### The Governing Equation of Gradually Varied Flow

The behavior of all [gradually varied flow](@entry_id:264271) profiles is governed by a single differential equation that relates the change in water depth to the channel's properties and flow conditions. For a prismatic channel, this equation is expressed as:

$$
\frac{dy}{dx} = \frac{S_0 - S_f}{1 - Fr^2}
$$

Here, $y$ is the flow depth, $x$ is the distance along the channel, $S_0$ is the longitudinal slope of the channel bed, $S_f$ is the [friction slope](@entry_id:265665), and $Fr$ is the Froude number of the flow. The term $dy/dx$ represents the slope of the water surface relative to the channel bed. The sign of $dy/dx$ indicates whether the water surface is rising ($dy/dx > 0$) or falling ($dy/dx < 0$) in the direction of flow.

The physical meaning of this equation can be understood by examining its numerator and denominator:

*   The **numerator ($S_0 - S_f$)** represents the net force driving the flow. $S_0$ is a surrogate for the component of gravitational force acting along the channel, while $S_f$ represents the force of frictional resistance. If gravity's influence is stronger than friction's ($S_0 > S_f$), the flow accelerates, and if friction dominates ($S_f > S_0$), the flow decelerates.
*   The **denominator ($1 - Fr^2$)** describes the flow state relative to the critical condition. The **Froude number**, $Fr = V / \sqrt{gD}$ (where $V$ is the flow velocity, $g$ is the [acceleration due to gravity](@entry_id:173411), and $D$ is the hydraulic depth), distinguishes between **[subcritical flow](@entry_id:276823)** ($Fr < 1$) and **supercritical flow** ($Fr > 1$). The term $1 - Fr^2$ is positive for [subcritical flow](@entry_id:276823) and negative for supercritical flow.

The interplay between these two terms determines the shape of the water surface. The classification of GVF profiles is, therefore, a systematic analysis of the possible combinations of the signs of the numerator and denominator across different channel and flow conditions.

### The Foundational Parameters: Normal and Critical Depth

To systematically classify GVF profiles, we must first establish two reference depths: the **[normal depth](@entry_id:265980) ($y_n$)** and the **[critical depth](@entry_id:275576) ($y_c$)**. These two depths serve as the fundamental benchmarks against which the actual flow depth $y$ is compared.

The **[normal depth](@entry_id:265980) ($y_n$)** is the depth at which uniform flow occurs for a given discharge $Q$ and channel configuration. It is a hypothetical depth where the gravitational forces are perfectly balanced by frictional resistance, meaning the [friction slope](@entry_id:265665) equals the bed slope ($S_f = S_0$). The numerator of the GVF equation becomes zero, resulting in $dy/dx = 0$, which is the definition of [uniform flow](@entry_id:272775). The [normal depth](@entry_id:265980) is calculated using uniform flow formulas like the Manning or Chézy equations. For instance, using Manning's equation for a wide rectangular channel, we can relate the unit discharge $q$ to the [normal depth](@entry_id:265980) $y_n$:

$$
q = \frac{1}{n} y_n^{5/3} S_0^{1/2}
$$

where $n$ is Manning's roughness coefficient. This shows that $y_n$ depends on the discharge, channel roughness, and bed slope.

The **[critical depth](@entry_id:275576) ($y_c$)** is the depth at which the specific energy of the flow is at a minimum for a given discharge. This unique condition corresponds to a Froude number of unity ($Fr = 1$). At this depth, the denominator of the GVF equation becomes zero, implying that $dy/dx$ approaches infinity (a vertical water surface slope), which is physically impossible in GVF. The GVF model breaks down at this point, often signaling a transition to [rapidly varied flow](@entry_id:274873), such as a [hydraulic jump](@entry_id:266212) or a free overfall. For a rectangular channel, the [critical depth](@entry_id:275576) depends only on the discharge per unit width, $q$:

$$
y_c = \left( \frac{q^2}{g} \right)^{1/3}
$$

Unlike [normal depth](@entry_id:265980), [critical depth](@entry_id:275576) is independent of bed slope and channel roughness. It is a fundamental property of the flow itself.

### The First Axis of Classification: Channel Slope Categories

The primary classification of a channel is determined by the relationship between its [normal depth](@entry_id:265980) and [critical depth](@entry_id:275576). This comparison effectively tells us whether the [uniform flow](@entry_id:272775) in that channel would be subcritical or supercritical. This leads to five slope categories, denoted by a letter.

*   **Mild Slope (M):** A channel is classified as mild if $y_n > y_c$. This implies that uniform flow for the given discharge would be subcritical ($Fr < 1$). This is the most common condition in natural rivers and man-made canals.

*   **Steep Slope (S):** A channel is classified as steep if $y_n < y_c$. In this case, [uniform flow](@entry_id:272775) would be supercritical ($Fr > 1$). Such slopes are found in mountain torrents, spillways, and chutes.

*   **Critical Slope (C):** A channel is classified as critical if $y_n = y_c$. Here, uniform flow occurs precisely at the critical state ($Fr = 1$). This is a highly unstable condition and is rare in practice.

*   **Horizontal Slope (H):** A channel with a bed slope of $S_0 = 0$ is classified as horizontal. For uniform flow, we would need $S_f = 0$, which, for a non-zero discharge, would require an infinite flow depth. Thus, for a horizontal channel, we consider the [normal depth](@entry_id:265980) to be infinite ($y_n \to \infty$) [@problem_id:1742353] [@problem_id:1742356].

*   **Adverse Slope (A):** A channel with a negative bed slope ($S_0 < 0$), meaning it slopes uphill in the direction of flow, is classified as adverse. Uniform flow is physically impossible in such a channel because the [friction slope](@entry_id:265665) $S_f$ is always positive, and can never equal a negative $S_0$. Therefore, the [normal depth](@entry_id:265980) $y_n$ is considered undefined for an adverse slope [@problem_id:1742342].

### The Second Axis of Classification: Flow Zones

Once the slope category is determined, the space available for the flow is divided into zones based on the actual flow depth $y$ relative to $y_n$ and $y_c$.

*   **Zone 1:** The region where the flow depth is greater than both normal and [critical depth](@entry_id:275576) ($y > y_n$ and $y > y_c$).
*   **Zone 2:** The region where the flow depth is between the normal and critical depths.
*   **Zone 3:** The region where the flow depth is less than both normal and [critical depth](@entry_id:275576) ($y < y_n$ and $y < y_c$).

For Horizontal and Adverse slopes where $y_n$ is infinite or undefined, Zone 1 does not exist. The flow is simply divided into Zone 2 (subcritical, $y > y_c$) and Zone 3 (supercritical, $y < y_c$). A GVF profile is uniquely identified by combining the slope letter with the zone number (e.g., M1, S2, H3).

### A Systematic Review of GVF Profiles

By analyzing the GVF equation within each slope category and zone, we can predict the shape of all 12 possible profiles.

#### Mild Slope Profiles (M)

For a mild slope, the defining characteristic is $y_n > y_c$, and [uniform flow](@entry_id:272775) is subcritical.

*   **M1 Profile ($y > y_n > y_c$):** This is a **[backwater curve](@entry_id:271120)**. Since the flow is deeper than [normal depth](@entry_id:265980) ($y > y_n$), the velocity is lower, and the [friction slope](@entry_id:265665) is less than the bed slope ($S_f < S_0$). Thus, the numerator ($S_0 - S_f$) is positive. Since the flow is also deeper than [critical depth](@entry_id:275576) ($y > y_c$), the flow is subcritical ($Fr < 1$), and the denominator ($1 - Fr^2$) is positive. The result is $dy/dx > 0$, indicating a water surface that rises in the direction of flow. M1 profiles are caused by downstream obstructions that force the water level up, such as a dam or a reservoir [@problem_id:1742355]. This backwater effect can also be caused by less obvious downstream conditions, such as an abrupt increase in channel roughness from vegetation, which increases the downstream [normal depth](@entry_id:265980) and backs water into the smoother upstream reach [@problem_id:1742357], or a constriction like a bridge pier during a flood [@problem_id:1742352].

*   **M2 Profile ($y_n > y > y_c$):** This is a **drawdown curve**. The flow depth is between normal and critical. Since $y < y_n$, the velocity is higher than in uniform flow, so friction is greater ($S_f > S_0$), making the numerator negative. The flow remains subcritical ($y > y_c$), so the denominator is positive. This yields $dy/dx < 0$, a falling water surface. M2 profiles occur when water approaches a "free outfall" or a sudden drop in the channel bed, where the flow must accelerate and pass through the [critical depth](@entry_id:275576) [@problem_id:1742385]. The profile extends from $y_n$ far upstream and approaches $y_c$ at the control point.

*   **M3 Profile ($y_n > y_c > y$):** This is a supercritical flow profile on a mild slope. Since $y < y_c$, the flow is supercritical ($Fr > 1$), making the denominator negative. As with the M2 profile, $y < y_n$, so the numerator is also negative. The result is $dy/dx > 0$, a rising water surface. This profile is typically formed when a high-velocity jet is discharged into a mild channel, for instance, from under a [sluice gate](@entry_id:267992) [@problem_id:1742370]. This rapid flow is unstable on a mild slope and seeks to return to its natural subcritical state. The M3 profile represents the initial stage of this process, where the depth increases until it often terminates abruptly in a [hydraulic jump](@entry_id:266212) to a subcritical M1 or M2 depth.

#### Steep Slope Profiles (S)

For a steep slope, $y_n < y_c$, and uniform flow is supercritical.

*   **S1 Profile ($y > y_c > y_n$):** This is a [backwater curve](@entry_id:271120) on a steep slope. The flow is subcritical ($y > y_c$) and deeper than [normal depth](@entry_id:265980) ($y > y_n$). The analysis is identical to the M1 case: numerator is positive, denominator is positive, so $dy/dx > 0$. An S1 profile is formed upstream of a dam or obstruction that drowns out the natural supercritical flow and forces a subcritical condition [@problem_id:1742372]. Since this subcritical profile cannot extend infinitely up a steep channel (where the natural state is supercritical), it must be initiated by a [hydraulic jump](@entry_id:266212) further upstream.

*   **S2 Profile ($y_c > y > y_n$):** This is a drawdown curve. The flow is supercritical ($Fr > 1$), so the denominator is negative. The depth is greater than [normal depth](@entry_id:265980) ($y > y_n$), so the numerator ($S_0 - S_f$) is positive. This results in $dy/dx < 0$, a falling water surface. This profile is characteristic of the [entrance region](@entry_id:269854) of a long, steep channel fed from a reservoir. The flow enters at or near [critical depth](@entry_id:275576) and then accelerates down the steep slope, with the depth "drawing down" and asymptotically approaching the [normal depth](@entry_id:265980) $y_n$ far downstream [@problem_id:1742390].

*   **S3 Profile ($y_c > y_n > y$):** This is a rising supercritical profile. The flow is supercritical ($Fr > 1$), making the denominator negative. The depth is less than [normal depth](@entry_id:265980) ($y < y_n$), causing high friction ($S_f > S_0$) and a negative numerator. Therefore, $dy/dx > 0$. This profile occurs when flow is introduced onto a steep slope at a depth below the [normal depth](@entry_id:265980), such as from a [sluice gate](@entry_id:267992) with a low opening [@problem_id:1742384]. The water surface rises and asymptotically approaches the [normal depth](@entry_id:265980) $y_n$ from below.

#### Special Case Profiles: Horizontal (H) and Adverse (A)

These slopes cannot sustain uniform flow, so Zone 1 is absent.

*   **H2 and A2 Profiles ($y > y_c$):** These are subcritical drawdown curves. For both H ($S_0 = 0$) and A ($S_0 < 0$) slopes, the numerator ($S_0 - S_f$) is always negative (since $S_f > 0$). In Zone 2, the flow is subcritical ($Fr < 1$), so the denominator is positive. This invariably leads to $dy/dx < 0$. An A2 profile, for example, forms on an adverse slope leading to a free overfall, where the depth must decrease to meet the [critical depth](@entry_id:275576) at the brink [@problem_id:1742342].

*   **H3 and A3 Profiles ($y < y_c$):** These are supercritical rising curves. The numerator is again always negative. In Zone 3, the flow is supercritical ($Fr > 1$), making the denominator negative. The result is $dy/dx > 0$. An H3 profile is a common sight downstream of a [sluice gate](@entry_id:267992) on a horizontal channel, where a high-velocity jet is released. The depth increases as friction decelerates the flow, often leading to a hydraulic jump [@problem_id:1742356].

### The Role of Flow Controls

The formation of a specific GVF profile is not arbitrary; it is dictated by **flow controls**. A control is a section of the channel that establishes a definitive relationship between depth and discharge. The Froude number determines where a control's influence is felt.

In **[subcritical flow](@entry_id:276823)** ($Fr < 1$), small disturbances can travel upstream. Consequently, the flow is governed by **downstream controls**. A dam, weir, reservoir level, or even a change in slope or roughness dictates the water surface elevation, and this influence propagates upstream, creating profiles like M1, S1, and M2.

In **supercritical flow** ($Fr > 1$), disturbances are swept downstream and cannot propagate upstream. The flow is therefore governed by **upstream controls**. A [sluice gate](@entry_id:267992), a reservoir entrance, or the point where a channel slope becomes steep establishes the initial depth, and the profile evolves downstream from that point. This gives rise to profiles like M3, S2, and S3.

By first identifying the slope category and then locating the relevant [flow control](@entry_id:261428), an engineer can predict the type of GVF profile that will form, providing a powerful tool for analyzing the complex and dynamic behavior of water in open channels.