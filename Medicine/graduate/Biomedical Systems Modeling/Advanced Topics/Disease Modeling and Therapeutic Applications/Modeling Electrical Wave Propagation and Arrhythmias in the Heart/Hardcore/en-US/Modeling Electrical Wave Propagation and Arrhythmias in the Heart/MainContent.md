## Introduction
The heart's rhythmic beat is a marvel of biological engineering, orchestrated by a precisely coordinated wave of electricity. When this coordination fails, life-threatening arrhythmias can emerge. Understanding these complex electrical disorders is a profound challenge, as they are not properties of a single cell but emergent phenomena of a vast, interconnected network. This knowledge gap—between single-[cell behavior](@entry_id:260922) and whole-organ dysfunction—necessitates a systems-level approach grounded in mathematical and computational modeling.

This article provides a comprehensive guide to modeling [cardiac electrophysiology](@entry_id:166145), bridging the scales from ion channels to the whole heart. In the first chapter, **Principles and Mechanisms**, we will construct the theoretical foundation, starting with the ionic basis of [cellular excitability](@entry_id:747183) and building up to the [reaction-diffusion equations](@entry_id:170319) that govern wave propagation in anisotropic tissue. Next, in **Applications and Interdisciplinary Connections**, we will explore how these models are applied to dissect the causes of arrhythmias, understand pathological substrates like fibrosis, and design and evaluate clinical therapies. Finally, the **Hands-On Practices** chapter will offer opportunities to apply these concepts through targeted modeling exercises, solidifying your understanding of how arrhythmias are initiated and sustained.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing [cardiac electrophysiology](@entry_id:166145), from the behavior of a single cell to the complex dynamics of wave propagation and arrhythmias in the whole heart. We will construct a conceptual and mathematical framework, starting with the principles of [cellular excitability](@entry_id:747183), building up to the propagation of electrical waves through the structured, anisotropic heart tissue, and culminating in an exploration of the mechanisms that give rise to life-threatening [cardiac arrhythmias](@entry_id:909082).

### Cellular Excitability: The Engine of the Heartbeat

The ability of a cardiac cell to generate and respond to electrical stimuli is known as **excitability**. This property is the fundamental engine driving every heartbeat. Understanding excitability requires examining the [cardiac action potential](@entry_id:148407) and the concept of an [activation threshold](@entry_id:635336) from multiple perspectives.

#### The Cardiac Action Potential and its Ionic Basis

The **action potential (AP)** is a transient, all-or-none change in the transmembrane voltage, $V_m$, that constitutes the primary electrical signal in the heart. A typical ventricular action potential is characterized by several distinct phases: a rapid depolarization (upstroke), an early [repolarization](@entry_id:150957), a sustained plateau, and a final repolarization back to the resting state.

These voltage dynamics are governed by the flow of ions across the cell membrane through specialized proteins called ion channels. The net current balance at the membrane is described by the foundational equation:

$C_m \frac{dV_m}{dt} = -I_{\mathrm{ion}}$

where $C_m$ is the membrane capacitance per unit area and $I_{\mathrm{ion}}$ is the total ionic current, which is the sum of all individual currents flowing through different channel types. By convention, outward currents are positive.

The complex morphology of the [cardiac action potential](@entry_id:148407) arises from the precisely timed opening and closing of multiple types of ion channels. While detailed models can include dozens of currents, the principal behavior can be understood by considering a few key players, as explored in the modeling exercise of .
*   **Upstroke:** This phase is driven by a massive, rapid influx of positive sodium ions ($Na^+$) through fast-acting [voltage-gated channels](@entry_id:143901), creating a large inward current ($I_{\mathrm{Na}}$). This current is self-amplifying: depolarization opens more sodium channels, leading to an explosive, all-or-none rise in voltage.
*   **Plateau:** After the peak, the sodium channels quickly inactivate. The voltage is then maintained at a high, depolarized level for a prolonged period. This plateau is the result of a delicate balance between an inward current, primarily carried by calcium ions ($Ca^{2+}$) through L-type calcium channels ($I_{\mathrm{CaL}}$), and outward currents carried by potassium ions ($K^+$). The sustained calcium influx during the plateau is critical for triggering muscle contraction.
*   **Repolarization:** The action potential terminates as the inward calcium channels inactivate and various types of delayed-rectifier [potassium channels](@entry_id:174108) (such as $I_{Kr}$ and $I_{Ks}$) activate more fully. The resulting net outward current drives the membrane potential back towards its negative resting state.

The duration of the action potential, particularly the time it takes for $90\%$ of [repolarization](@entry_id:150957) to complete (a metric known as **APD90**), is a critical determinant of the heart's electrical behavior and its susceptibility to arrhythmias .

The dynamics of each [ion channel](@entry_id:170762)'s conductance are described by a system of [ordinary differential equations](@entry_id:147024) for its "[gating variables](@entry_id:203222)," a formalism first established by Hodgkin and Huxley. Each gating variable, $z$, typically follows first-order kinetics of the form $\frac{dz}{dt} = (z_{\infty}(V_m) - z) / \tau_z(V_m)$, relaxing towards a voltage-dependent steady state $z_{\infty}$ with a time constant $\tau_z$. The complete description of a single cell's electrical activity is thus a high-dimensional, nonlinear dynamical system.

#### The Concept of Threshold: Two Perspectives

A hallmark of excitability is the existence of a **threshold**: a subthreshold stimulus elicits only a small, passive response, while a suprathreshold stimulus triggers a full, regenerative action potential. We can formalize this concept from two complementary viewpoints.

**A Biophysical Perspective: The Strength–Duration Relationship**

From a practical standpoint, related to artificial pacemakers, threshold is defined by the stimulus required to initiate an AP. If we model a small patch of membrane as a simple passive resistor-capacitor (RC) circuit, we can derive the relationship between the strength (amplitude $I$) and duration ($t_p$) of a rectangular current pulse needed to depolarize the membrane to a fixed threshold voltage, $\Delta V_{\mathrm{th}}$. This leads to the classic **strength–duration relationship** . The threshold current $I_{\mathrm{th}}$ is given by:

$I_{\mathrm{th}}(t_{p}) = \frac{\Delta V_{\mathrm{th}}}{R \left( 1 - \exp(-t_p/\tau_m) \right)}$

where $R$ and $C$ are the total [membrane resistance](@entry_id:174729) and capacitance, and $\tau_m = RC$ is the [membrane time constant](@entry_id:168069).

From this relationship, we define two fundamental parameters of excitability:
*   **Rheobase ($I_r$):** The minimum current amplitude that can elicit an action potential, corresponding to a stimulus of infinite duration. Mathematically, $I_r = \lim_{t_p \to \infty} I_{\mathrm{th}}(t_p) = \Delta V_{\mathrm{th}} / R$.
*   **Chronaxie ($\tau$):** The stimulus duration required to elicit an action potential when the current amplitude is twice the [rheobase](@entry_id:176795). It can be shown that $\tau = \tau_m \ln(2)$.

The [strength-duration curve](@entry_id:899679) is well approximated by the simpler Weiss-Lapicque formula, $I_{\mathrm{th}}(t_p) \approx I_r (1 + \tau/t_p)$, which captures the essential trade-off: a shorter stimulus requires a stronger current to inject the necessary threshold charge before the current is turned off .

**A Dynamical Systems Perspective: Phase-Plane Analysis**

A deeper understanding of threshold emerges from analyzing simplified mathematical models of excitability, such as the **FitzHugh-Nagumo (FHN) model**. By reducing the complex ionic dynamics to just two variables—an activator-like voltage variable $v$ and a slower recovery variable $w$—we can visualize the system's behavior in a 2D **phase plane** .

The dynamics are defined by a system of two ODEs:
$\frac{dv}{dt} = f(v,w) + I_{\mathrm{ext}}$
$\frac{dw}{dt} = g(v,w)$

The **nullclines** are curves in the $(v,w)$ plane where one of the variables has zero rate of change. The $v$-nullcline ($dv/dt = 0$) is typically a cubic-shaped curve, while the $w$-nullcline ($dw/dt = 0$) is often monotonic. The intersection of these nullclines defines the fixed points, or steady states, of the system. For an excitable cell at rest, there is a single, stable fixed point.

A stimulus $I_{\mathrm{ext}}$ effectively shifts the $v$-nullcline. A small stimulus results in a trajectory that quickly returns to the rest state. However, if the stimulus is large enough, it pushes the system's state across a [separatrix](@entry_id:175112) in the phase plane, initiating a long excursion that corresponds to the action potential before eventually returning to rest. The threshold behavior is not a fixed voltage but a dynamic property of the system's state space geometry.

The excitability threshold can be precisely defined as the critical stimulus value, $I^\star$, at which a bifurcation occurs. Specifically, $I^\star$ is the current at which the resting fixed point vanishes through a collision of fixed points, geometrically corresponding to the point where the $v$- and $w$-[nullclines](@entry_id:261510) become tangent to one another . This event represents a loss of stability of the resting state, making an action potential inevitable.

### Electrical Propagation in Cardiac Tissue

Cardiac cells do not operate in isolation. They are electrically coupled into a functional **[syncytium](@entry_id:265438)**, allowing the action potential to propagate from cell to cell, coordinating the heart's contraction.

#### Anisotropy: The Influence of Microstructure

The speed and pattern of electrical propagation are profoundly influenced by the heart's intricate architecture. Cardiomyocytes are elongated, rod-shaped cells organized into bundles that form laminar sheets. This structure creates preferential pathways for current flow. Electrical conduction is not uniform in all directions; it is **anisotropic**.

To model this, we define a local orthonormal coordinate system based on the tissue microstructure :
*   $\mathbf{f}$: The local **fiber direction**, tangent to the long axis of the myocytes.
*   $\mathbf{s}$: The **sheet direction**, lying within the muscle sheet but orthogonal to the fibers.
*   $\mathbf{n}$: The **normal direction**, orthogonal to the plane of the sheet.

Current flows most readily along the fiber direction ($\mathbf{f}$) due to the high density of low-resistance [gap junctions](@entry_id:143226) at the ends of the cells. Flow is more impeded side-to-side within a sheet ($\mathbf{s}$), and most impeded when crossing between sheets ($\mathbf{n}$). This results in principal conductivities with the ordering $d_f > d_s > d_n$. This anisotropy is mathematically captured by a symmetric, [positive definite](@entry_id:149459) **[conductivity tensor](@entry_id:155827)** (or diffusion tensor in [reaction-diffusion models](@entry_id:182176)), which in its principal coordinate system is diagonal. In a global coordinate system, it takes the form:

$D = d_f \mathbf{f}\mathbf{f}^{\mathsf{T}} + d_s \mathbf{s}\mathbf{s}^{\mathsf{T}} + d_n \mathbf{n}\mathbf{n}^{\mathsf{T}}$

where $\mathbf{v}\mathbf{v}^{\mathsf{T}}$ denotes the [outer product](@entry_id:201262) of a vector with itself. This tensor is a cornerstone of realistic tissue-level simulations.

#### Modeling the Tissue: Reaction-Diffusion Systems

The [propagation of the action potential](@entry_id:154745) through cardiac tissue is modeled by **[reaction-diffusion equations](@entry_id:170319)**. These partial differential equations (PDEs) combine a "reaction" term, representing the local [ionic currents](@entry_id:170309) from single-cell models like Hodgkin-Huxley or FHN, with a "diffusion" term, representing the electrical current flow between cells.

The **[monodomain model](@entry_id:1128131)** is a common and computationally efficient formulation, represented by a single PDE for the transmembrane potential $V_m$:

$C_m \frac{\partial V_m}{\partial t} = \nabla \cdot (D \nabla V_m) - I_{\mathrm{ion}}(V_m)$

Here, $\nabla \cdot (D \nabla V_m)$ is the divergence of the diffusive current, with $D$ being the effective monodomain [conductivity tensor](@entry_id:155827). This model is a simplification of the more comprehensive **[bidomain model](@entry_id:1121551)**, which explicitly solves for both intracellular and extracellular potentials. The monodomain tensor $D$ can be derived from the bidomain intracellular ($G_i$) and extracellular ($G_e$) conductivity tensors, and is equivalent to their harmonic mean along each principal axis: $(D)_{kk} = (G_i)_{kk}(G_e)_{kk} / ((G_i)_{kk} + (G_e)_{kk})$ . A common simplifying assumption, the **equal anisotropy ratio assumption**, posits that $G_e = \lambda G_i$ for some scalar $\lambda$, though this can introduce errors when the true anisotropy ratios of the intra- and extracellular spaces differ.

#### Conduction Velocity: The Speed of the Wave

A primary emergent property of a reaction-diffusion system is the **conduction velocity ($c$)** of the propagating wave. For a one-dimensional cable, we can approximate the leading edge of the action potential upstroke with a simpler reaction term, such as the logistic growth in the Fisher-Kolmogorov-Petrovsky-Piskunov (KPP) equation. This simplification yields a celebrated result for the minimum stable [wave speed](@entry_id:186208) :

$c = 2\sqrt{D\alpha}$

where $D$ is the diffusion coefficient (proportional to conductivity) and $\alpha$ is a parameter representing the rate of [ionic current](@entry_id:175879) activation at the leading edge of the wave. This elegant formula reveals that conduction velocity is determined by the interplay of two fundamental properties: passive tissue conductivity ($D$) and active membrane excitability ($\alpha$).

#### The Cardiac Conduction System

The heart possesses a specialized fast conduction system, the **His-Purkinje network**, to ensure rapid and coordinated activation of the ventricles. Purkinje fibers are characterized by very high conductivity compared to the surrounding ventricular muscle, resulting in significantly faster conduction velocities (e.g., 2-4 m/s vs. 0.3-0.9 m/s) .

This network can be modeled as a branching tree structure, where electrical signals propagate from the root (the His bundle) to the leaves (Purkinje-muscle junctions on the endocardial surface). By applying the simple kinematic principle of time = distance / velocity ($t = \ell/v$) along each branch of the tree, one can accurately predict the sequence of ventricular activation, a critical tool in both basic science and clinical applications like [cardiac resynchronization therapy](@entry_id:1122090) .

### Mechanisms of Arrhythmias

Arrhythmias arise when the orderly sequence of cardiac activation is disrupted. Modeling helps us understand the underlying mechanisms, such as conduction block and reentry.

#### Stability of Propagation: The Safety Factor

Successful propagation requires that each excited cell provides enough current to its downstream neighbor to bring it to threshold. This balance can be quantified by the **safety factor (SF)**, defined as the ratio of the charge delivered by an upstream cell (the source) to the charge required to excite a downstream cell (the sink) .

$SF = \frac{\text{Charge Source}}{\text{Charge Sink}}$

If $SF > 1$, the source is more than sufficient, and propagation is robust. If $SF  1$, the source is insufficient to excite the next cell, and propagation fails. This failure is known as **conduction block**. The safety factor can be compromised by either reduced membrane excitability (e.g., a smaller peak sodium current $I_{Na,max}$) or by poor intercellular coupling (e.g., a lower [gap junction](@entry_id:183579) conductance $g_{gap}$). Pathological conditions that reduce cell-to-cell coupling can therefore create regions of conduction block, a key ingredient for arrhythmia formation.

#### Geometric Effects: The Curvature-Velocity Relationship

Conduction velocity is not always constant; it is also affected by the geometry of the [wavefront](@entry_id:197956). The **curvature-velocity relationship**, a fundamental property of [reaction-diffusion systems](@entry_id:136900), states that the local normal speed of a [wavefront](@entry_id:197956), $c$, depends on its curvature, $\kappa$:

$c(\kappa) \approx c_0 - D \kappa$

where $c_0$ is the speed of a planar wave ($\kappa=0$) and $D$ is the diffusion coefficient . By convention, a wavefront that is convex in the direction of propagation (like the front of a wave spreading out from a point) has [positive curvature](@entry_id:269220) ($\kappa > 0$). According to the relation, this [wavefront](@entry_id:197956) will travel slower than a planar wave. Conversely, a concave [wavefront](@entry_id:197956) ($\kappa  0$) will travel faster. This effect is crucial for understanding how waves navigate around anatomical obstacles (like blood vessels or scar tissue) or functional heterogeneities. The slowing of a wave as it bends around an obstacle is a critical mechanism for initiating reentrant arrhythmias.

#### Reentry: The Heart's Vicious Cycle

**Reentry** is a mechanism responsible for many clinically important tachyarrhythmias, including [atrial fibrillation](@entry_id:926149) and [ventricular tachycardia](@entry_id:893614). It occurs when an electrical impulse does not terminate but instead continuously circulates within the heart tissue, repeatedly re-exciting the same regions.

For reentry to be sustained, two fundamental conditions must be met:
1.  There must be a closed conduction path or **circuit**.
2.  The time it takes for the impulse to travel around the circuit must be longer than the refractory period of the tissue in the circuit.

This second condition is elegantly captured by the concept of **wavelength ($\lambda$)**. The wavelength is the spatial extent of the action potential, or the "footprint" of the wave in the tissue. It is the product of the [conduction velocity](@entry_id:156129) ($c$) and the effective refractory period ($ERP$) :

$\lambda = c \cdot \text{ERP}$

For a reentrant wave to persist in a circuit of path length $L$, its head must find excitable tissue to propagate into when it returns to its starting point. This means the tail of the wave must have already passed. The condition for sustained reentry is therefore that the path length must be greater than the wavelength:

$L > \lambda$

This inequality is arguably the most important relationship in [arrhythmogenesis](@entry_id:905177). It reveals that reentry is promoted by factors that shorten the wavelength: slow conduction (decreased $c$) or a short refractory period (decreased $ERP$). Conversely, anti-arrhythmic strategies often aim to terminate reentry by increasing the wavelength, for example, by administering drugs that prolong the ERP (such as $I_{Kr}$ blockers), thereby violating the condition $L > \lambda$ and extinguishing the reentrant circuit . This fundamental principle links cellular-level properties (ion channel function) and tissue-level properties (conduction, anatomy) directly to the stability of life-threatening arrhythmias.