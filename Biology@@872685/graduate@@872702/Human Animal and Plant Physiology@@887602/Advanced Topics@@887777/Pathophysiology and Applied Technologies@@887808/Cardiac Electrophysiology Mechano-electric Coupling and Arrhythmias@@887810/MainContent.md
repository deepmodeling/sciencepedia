## Introduction
The rhythmic beating of the heart is a marvel of [biological engineering](@entry_id:270890), orchestrated by a complex interplay of electrical signals and mechanical forces. At its core, [cardiac electrophysiology](@entry_id:166145) governs every heartbeat, from the spontaneous impulse in the [pacemaker cells](@entry_id:155624) to the coordinated contraction of the ventricles. However, disruptions in this intricate system can lead to life-threatening arrhythmias. A comprehensive understanding requires bridging the gap between the behavior of single ion channels and the emergent properties of the whole heart in both health and disease. This article provides a deep dive into this essential topic, elucidating the fundamental mechanisms that govern cardiac rhythm and its pathologies. The first chapter, **Principles and Mechanisms**, will lay the groundwork by exploring the ionic basis of the action potential, its propagation, and the genesis of arrhythmias. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these principles are applied to understand regional specializations, mechano-electric feedback, and the basis for pharmacological and electrical therapies. Finally, **Hands-On Practices** will offer computational exercises to solidify these concepts, allowing you to simulate and explore the dynamics of conduction, reentry, and electrical instability.

## Principles and Mechanisms

The orchestrated contraction of the heart originates from a highly coordinated sequence of electrical events. This chapter delves into the fundamental principles and mechanisms governing [cardiac electrophysiology](@entry_id:166145), from the generation of electrical potentials across a single cell membrane to the propagation of this signal throughout the multicellular cardiac [syncytium](@entry_id:265438). We will then explore the link between electrical excitation and mechanical contraction, and finally, dissect the pathophysiological mechanisms that disrupt this orderly process, leading to cardiac arrhythmias.

### The Electrochemical Foundations of Cardiac Excitability

The ability of a cardiac cell to generate and conduct electrical impulses is rooted in the carefully maintained ionic concentration gradients across its membrane and the [selective permeability](@entry_id:153701) of the membrane to these ions.

#### The Nernst Potential: An Ion's Equilibrium

Each ion species ($i$) distributed across the myocyte membrane has a unique **Nernst equilibrium potential** ($E_i$). This potential represents the specific transmembrane voltage at which the electrical force acting on the ion exactly counterbalances the chemical force arising from its concentration gradient. At this voltage, there is no net movement of the ion across the membrane, assuming the membrane is permeable only to that ion. The Nernst potential is derived by equating the electrochemical potentials of the ion on the inside and outside of the cell, and is given by the Nernst equation:

$E_{i} = \dfrac{RT}{z_{i}F} \ln \dfrac{[i]_{\mathrm{o}}}{[i]_{\mathrm{i}}}$

where $R$ is the [universal gas constant](@entry_id:136843), $T$ is the absolute temperature, $F$ is Faraday’s constant, $z_i$ is the valence of the ion, and $[i]_{\mathrm{o}}$ and $[i]_{\mathrm{i}}$ are its extracellular and intracellular concentrations, respectively.

For a typical ventricular myocyte at $310\,\mathrm{K}$ ($37^\circ\mathrm{C}$), with intracellular concentrations of $[\mathrm{K}^{+}]_{\mathrm{i}} \approx 140\,\mathrm{mM}$ and $[\mathrm{Na}^{+}]_{\mathrm{i}} \approx 10\,\mathrm{mM}$, and extracellular concentrations of $[\mathrm{K}^{+}]_{\mathrm{o}} \approx 4\,\mathrm{mM}$ and $[\mathrm{Na}^{+}]_{\mathrm{o}} \approx 140\,\mathrm{mM}$, the Nernst potentials are approximately $E_{\mathrm{K}} \approx -95\,\mathrm{mV}$ and $E_{\mathrm{Na}} \approx +70\,\mathrm{mV}$ [@problem_id:2555253]. This large, negative potential for potassium and large, positive potential for sodium establish the electrochemical driving forces that power the [cardiac action potential](@entry_id:148407).

#### The Resting Membrane Potential: A Multi-Ion System

In reality, the cell membrane is permeable to multiple ions simultaneously. The **[reversal potential](@entry_id:177450)** of an [ion channel](@entry_id:170762) is the membrane voltage at which the net current through that specific channel is zero. If a channel is exclusively permeable to one ion, its [reversal potential](@entry_id:177450) is simply the Nernst potential for that ion. However, for channels permeable to multiple ions (e.g., a non-selective cation channel), the [reversal potential](@entry_id:177450) is a weighted average of the Nernst potentials of the permeant ions, determined by their relative permeabilities.

Under the [constant-field assumption](@entry_id:199980), the **Goldman-Hodgkin-Katz (GHK) voltage equation** describes the steady-state [membrane potential](@entry_id:150996) ($V_m$) that results from the contributions of multiple permeant ions. For the key monovalent ions $\mathrm{K}^{+}$, $\mathrm{Na}^{+}$, and $\mathrm{Cl}^{-}$, it is:

$V_{m} = \dfrac{RT}{F} \ln \dfrac{P_{\mathrm{K}}[\mathrm{K}^{+}]_{\mathrm{o}} + P_{\mathrm{Na}}[\mathrm{Na}^{+}]_{\mathrm{o}} + P_{\mathrm{Cl}}[\mathrm{Cl}^{-}]_{\mathrm{i}}}{P_{\mathrm{K}}[\mathrm{K}^{+}]_{\mathrm{i}} + P_{\mathrm{Na}}[\mathrm{Na}^{+}]_{\mathrm{i}} + P_{\mathrm{Cl}}[\mathrm{Cl}^{-}]_{\mathrm{o}}}$

Here, $P_i$ represents the [membrane permeability](@entry_id:137893) for ion $i$. Note that for the anion $\mathrm{Cl}^{-}$, the intracellular and extracellular concentrations are inverted in the equation due to its negative valence [@problem_id:2555253].

In a resting ventricular myocyte, the membrane has a much higher permeability to potassium than to other ions ($P_{\mathrm{K}} \gg P_{\mathrm{Na}}, P_{\mathrm{Cl}}$). This high resting [potassium permeability](@entry_id:168417) is primarily due to the activity of a specific class of channels known as **inward-rectifier potassium channels** ($I_{\mathrm{K1}}$). Consequently, the resting membrane potential (RMP) of ventricular myocytes lies very close to the Nernst potential for potassium, typically around $-85$ to $-90\,\mathrm{mV}$. The small deviation from the true $E_{\mathrm{K}}$ is due to a minor, persistent inward "leak" current, carried mainly by $\mathrm{Na}^{+}$ ions. The critical role of the $\mathrm{Na}^{+}/\mathrm{K}^{+}$ ATPase pump is not to directly set this potential, but to expend energy to maintain the underlying [ionic gradients](@entry_id:171010) against these leaks. Pathological increases in extracellular potassium ($[\mathrm{K}^{+}]_{\mathrm{o}}$), a condition known as [hyperkalemia](@entry_id:151804), make $E_{\mathrm{K}}$ less negative, thereby depolarizing the RMP. This [depolarization](@entry_id:156483) can significantly alter excitability and conduction, creating a substrate for arrhythmias [@problem_id:2555253].

### The Ionic Symphony: Currents of the Cardiac Action Potential

The [cardiac action potential](@entry_id:148407) (AP) is a transient, regenerative [depolarization](@entry_id:156483) of the cell membrane, driven by the precisely timed opening and closing of numerous [voltage-gated ion channels](@entry_id:175526). Each current contributes to a specific phase of the AP, and its properties—voltage-dependence, kinetics of activation and inactivation—are critical to its function [@problem_id:2555232].

#### Depolarizing and Plateau Currents

*   **Fast Sodium Current ($I_{\mathrm{Na}}$):** This current is responsible for the rapid upstroke (Phase 0) of the action potential in atrial, ventricular, and Purkinje cells. Gated by channels that activate and inactivate extremely rapidly upon depolarization past a threshold of about $-60$ to $-40\,\mathrm{mV}$, $I_{\mathrm{Na}}$ provides a massive, transient influx of $\mathrm{Na}^{+}$ ions, driven by the large difference between the membrane potential and $E_{\mathrm{Na}}$.

*   **L-type Calcium Current ($I_{\mathrm{Ca,L}}$):** Activating at more positive potentials (threshold near $-30\,\mathrm{mV}$) and with much slower activation and inactivation kinetics than $I_{\mathrm{Na}}$, this current is carried by $\mathrm{Ca}^{2+}$ ions. The sustained influx of calcium throughout the AP plateau (Phase 2) counteracts the repolarizing potassium currents, holding the membrane potential at a depolarized level. This current is the essential link between electrical excitation and mechanical contraction.

#### Repolarizing Currents

*   **Transient Outward Potassium Current ($I_{\mathrm{to}}$):** This current activates rapidly upon depolarization and inactivates within tens of milliseconds. The transient outward flux of $\mathrm{K}^{+}$ it provides is responsible for the early, partial [repolarization](@entry_id:150957) (Phase 1) that creates the "notch" following the upstroke in certain cell types.

*   **Delayed Rectifier Potassium Currents ($I_{\mathrm{Kr}}$ and $I_{\mathrm{Ks}}$):** These are the primary currents responsible for AP [repolarization](@entry_id:150957) (Phase 3).
    *   The **rapid component ($I_{\mathrm{Kr}}$)** activates upon [depolarization](@entry_id:156483) but also exhibits a peculiar rapid inactivation at positive plateau voltages. This limits its current during Phase 2 but allows a surge of current upon [repolarization](@entry_id:150957), accelerating the final return to rest.
    *   The **slow component ($I_{\mathrm{Ks}}$)** activates much more slowly and does not inactivate. Its magnitude is significantly enhanced by beta-[adrenergic stimulation](@entry_id:172807), a key mechanism that allows the AP to shorten at high heart rates, preserving diastolic filling time. The sum of these currents constitutes the heart's "[repolarization](@entry_id:150957) reserve".

*   **Inward Rectifier Potassium Current ($I_{\mathrm{K1}}$):** As discussed, this current is responsible for stabilizing the RMP (Phase 4). Its unique property of **inward [rectification](@entry_id:197363)** means it conducts $\mathrm{K}^{+}$ions poorly at depolarized potentials (during the plateau), effectively "getting out of the way" to allow the plateau to be sustained. As the cell repolarizes, its conductance increases, helping to clamp the membrane potential near $E_{\mathrm{K}}$.

#### Pacemaker Currents

*   **Funny Current ($I_f$):** Found predominantly in [pacemaker cells](@entry_id:155624) (e.g., in the [sinoatrial node](@entry_id:154149)), this current has the unique property of activating upon **[hyperpolarization](@entry_id:171603)**. It is a mixed $\mathrm{Na}^{+}/\mathrm{K}^{+}$ current with a [reversal potential](@entry_id:177450) around $-20$ to $-30\,\mathrm{mV}$. During diastole, this inward current slowly depolarizes the cell, driving the spontaneous **diastolic depolarization** (Phase 4) that underlies automaticity. Its activity is directly enhanced by cyclic AMP (cAMP), providing the primary mechanism for sympathetic heart rate regulation [@problem_id:2555232].

### A Diversity of Waveforms: Heterogeneity of Cardiac Action Potentials

The expression profile of these [ionic currents](@entry_id:170309) varies significantly throughout the heart, giving rise to distinct action potential morphologies and physiological roles for different cell types [@problem_id:2555258].

#### Regional Specialization: From Pacemakers to Working Myocytes

*   **Sinoatrial (SA) Node Cells:** As the heart's primary pacemaker, these cells lack a stable resting potential and significant $I_{\mathrm{Na}}$ and $I_{\mathrm{K1}}$. Their Phase 4 is a spontaneous diastolic [depolarization](@entry_id:156483) driven by $I_f$ and calcium currents. The AP upstroke (Phase 0) is slow and mediated by $I_{\mathrm{Ca,L}}$, not $I_{\mathrm{Na}}$. There are no distinct Phase 1 or 2, and [repolarization](@entry_id:150957) (Phase 3) is driven by $I_{\mathrm{Kr}}$ and $I_{\mathrm{Ks}}$.

*   **Atrial Myocytes:** These working cells have a rapid, $I_{\mathrm{Na}}$-mediated upstroke and a stable resting potential due to $I_{\mathrm{K1}}$. Their action potential is relatively short and triangular, featuring a brief plateau (Phase 2) that is quickly terminated by a robust set of repolarizing currents, including the **ultra-rapid delayed rectifier potassium current ($I_{\mathrm{Kur}}$)**, which is prominent in atria.

*   **Purkinje Fibers:** These specialized conduction cells have the fastest $I_{\mathrm{Na}}$-driven upstroke in the heart. They have a long AP with a prominent plateau (Phase 2). Crucially, they express $I_f$ and have weak $I_{\mathrm{K1}}$, giving them **latent automaticity**; their slow Phase 4 [depolarization](@entry_id:156483) allows them to function as secondary pacemakers if the SA node fails.

*   **Ventricular Myocytes:** These cells exhibit a rapid $I_{\mathrm{Na}}$ upstroke, a long and stable plateau (Phase 2) sustained by a fine balance between inward $I_{\mathrm{Ca,L}}$ and outward $I_{\mathrm{Kr}}$/$I_{\mathrm{Ks}}$, and a stable resting potential anchored by a strong $I_{\mathrm{K1}}$.

#### Transmural Heterogeneity: A Gradient Across the Ventricular Wall

Even within the ventricular wall, there is significant electrical heterogeneity from the outer surface (epicardium) to the inner surface (endocardium) [@problem_id:2555249].

*   **Epicardial (Epi) Cells:** These cells are characterized by a very large **transient outward current ($I_{\mathrm{to}}$)**. This produces a prominent Phase 1 "notch" and contributes to a shorter Action Potential Duration (APD) compared to other ventricular cell types.

*   **Endocardial (Endo) Cells:** These cells have a much smaller $I_{\mathrm{to}}$, resulting in a less prominent notch and a longer APD than epicardial cells.

*   **Mid-myocardial (M) Cells:** Located between the epicardium and endocardium, M-cells have the longest APD of all ventricular myocytes. This is due to a unique combination of a weaker **slow delayed rectifier current ($I_{\mathrm{Ks}}$)** and a slightly larger **late sodium current ($I_{\mathrm{NaL}}$)**. This combination reduces their [repolarization](@entry_id:150957) reserve, making them particularly susceptible to excessive APD prolongation and arrhythmias under conditions of repolarizing current blockade [@problem_id:2555249]. This intrinsic difference in APDs creates a transmural voltage gradient that shapes the T-wave of the surface [electrocardiogram](@entry_id:153078).

### From Signal to Force: Excitation-Contraction Coupling

The primary function of the action potential in working myocytes is to trigger cellular contraction. This process, known as **excitation-contraction (EC) coupling**, is mediated by calcium ions.

#### Calcium-Induced Calcium Release

In cardiac myocytes, the influx of calcium via the L-type calcium current ($I_{\mathrm{Ca,L}}$) during the AP plateau serves as a trigger, but it does not directly supply the bulk of the calcium needed for contraction. Instead, it initiates a process called **Calcium-Induced Calcium Release (CICR)** [@problem_id:2555271]. The sequence of events is as follows:
1.  The AP propagates along the sarcolemma and into the T-tubules.
2.  Depolarization opens L-type calcium channels, allowing a small amount of "trigger" $\mathrm{Ca}^{2+}$ to enter the cell in the restricted space of the dyadic cleft.
3.  This local rise in $\mathrm{Ca}^{2+}$ concentration activates nearby **[ryanodine receptors](@entry_id:149864) (RyR2)**, which are calcium-release channels on the membrane of the [sarcoplasmic reticulum](@entry_id:151258) (SR), the cell's main internal calcium store.
4.  The opening of RyR2 channels releases a much larger, amplified amount of $\mathrm{Ca}^{2+}$ from the SR into the cytosol.
5.  This global rise in cytosolic $\mathrm{Ca}^{2+}$ (the "calcium transient") binds to the myofilament protein [troponin](@entry_id:152123) C, initiating [cross-bridge cycling](@entry_id:172817) and cell contraction.

Thus, the amplitude of the cytosolic calcium transient, and therefore the force of contraction, is primarily determined by the amount of calcium released from the SR, with $I_{\mathrm{Ca,L}}$ acting as a graded trigger.

#### Calcium Homeostasis: Removal and Steady-State Balance

For the muscle to relax, cytosolic calcium must be returned to its low diastolic levels. This is accomplished by two main mechanisms [@problem_id:2555271]:
*   The **sarco/endoplasmic reticulum $\mathrm{Ca}^{2+}$-ATPase (SERCA)** pump actively transports the majority of the calcium (~70-90%) from the cytosol back into the SR, replenishing the store for the next beat. SERCA activity is a key determinant of SR calcium load and, therefore, the amplitude of subsequent calcium transients.
*   The **[sodium-calcium exchanger](@entry_id:143023) (NCX)**, operating in its forward mode, uses the sodium gradient to extrude the remaining calcium (~10-30%) from the cell. This is the primary mechanism for maintaining long-term cellular [calcium balance](@entry_id:153005), ensuring that the calcium that enters via $I_{\mathrm{Ca,L}}$ on each beat is ultimately removed.

### The Spread of Excitation: Conduction in Cardiac Tissue

The heart functions as an electrical syncytium, where the impulse generated in the SA node spreads rapidly and in a coordinated fashion to the rest of the myocardium.

#### Intercellular Communication: Gap Junctions

Individual cardiac myocytes are electrically coupled by **gap junctions**, which are clusters of intercellular channels located at the **intercalated disks** that join cells end-to-end. These channels are formed by proteins called **[connexins](@entry_id:150570)**. The predominant connexin in the working ventricle is **[connexin](@entry_id:191363) 43 (Cx43)**, while **connexin 40 (Cx40)** is abundant in the faster-conducting atrial and His-Purkinje tissues. These channels provide a low-resistance pathway for [ionic current](@entry_id:175879) to flow directly from the cytoplasm of one cell to the next, enabling the [propagation of the action potential](@entry_id:154745) [@problem_id:2555289].

#### The Heart as a Cable: Passive Properties and Propagation

The passive spread of voltage in cardiac tissue can be understood using **linear [cable theory](@entry_id:177609)**. A strand of cardiac tissue can be modeled as a core conductor (the cytoplasm) surrounded by a leaky capacitor (the cell membrane). Two key parameters emerge from this model [@problem_id:2555228]:

*   The **[space constant](@entry_id:193491) ($\lambda = \sqrt{r_m/r_i}$)**, where $r_m$ is the [membrane resistance](@entry_id:174729) and $r_i$ is the axial intracellular resistance per unit length. $\lambda$ describes the distance over which a steady-state voltage change decays to $1/e$ (about 37%) of its original value. A larger [space constant](@entry_id:193491) (resulting from higher [membrane resistance](@entry_id:174729) or lower [axial resistance](@entry_id:177656)) allows for more efficient spatial spread of current and faster conduction.

*   The **[time constant](@entry_id:267377) ($\tau = r_m c_m$)**, where $c_m$ is the [membrane capacitance](@entry_id:171929) per unit length. $\tau$ describes the time it takes for the membrane potential to charge to approximately 63% of its final value in response to a step current. A smaller time constant allows the membrane to depolarize more quickly.

The effective diffusion coefficient for voltage in this system can be defined as $D = \lambda^2 / \tau = 1/(r_i c_m)$, which encapsulates how quickly voltage gradients are smoothed out spatially and temporally.

#### Anisotropy and Source-Sink Dynamics

Cardiac tissue is **anisotropic**: its electrical properties depend on direction. Myocytes are elongated and coupled end-to-end, with [gap junctions](@entry_id:143226) concentrated at these ends. This architecture results in a much lower [axial resistance](@entry_id:177656) (and thus higher conductivity) for current flowing along the fiber axis (longitudinal direction) compared to across it (transverse direction). This difference in resistivity leads directly to [anisotropic conduction](@entry_id:136935) velocity. Since [conduction velocity](@entry_id:156129) ($v$) scales with the square root of conductivity ($1/\rho$), the velocity ratio is $v_L / v_T = \sqrt{\rho_T / \rho_L}$. For typical ventricular tissue with $\rho_T / \rho_L \approx 4$, the longitudinal [conduction velocity](@entry_id:156129) is approximately twice the transverse velocity [@problem_id:2555289]. A uniform reduction in gap junction function will increase both $\rho_L$ and $\rho_T$, slowing conduction in both directions but leaving the anisotropy ratio unchanged [@problem_id:2555289].

This cable structure also gives rise to the concept of **source-sink mismatch**. For propagation to succeed, the depolarizing current provided by the "source" (upstream excited tissue) must be sufficient to charge the membrane of the downstream "sink" tissue to its threshold. At a site of abrupt tissue expansion, such as the Purkinje-ventricular junction, the large mass of ventricular muscle presents a huge capacitive load (a large sink). This can slow depolarization and, particularly for premature or weak impulses, may lead to conduction failure or block [@problem_id:2555228].

### Pathophysiological Mechanisms: The Genesis of Arrhythmias

Arrhythmias arise from abnormalities in either impulse generation or impulse conduction.

#### Disorders of Impulse Generation: Afterdepolarizations

Afterdepolarizations are abnormal secondary depolarizations that can trigger action potentials. There are two main types [@problem_id:2555246]:

*   **Early Afterdepolarizations (EADs):** These occur during the plateau or [repolarization](@entry_id:150957) phase (Phase 2 or 3) of the action potential, before the cell has fully repolarized. They are caused by a shift in the balance of currents that favors depolarization. This typically occurs when APD is significantly prolonged (e.g., due to [bradycardia](@entry_id:152925) or drugs that block $I_{\mathrm{Kr}}$), which reduces [repolarization](@entry_id:150957) reserve and allows for the reactivation of inward currents like $I_{\mathrm{Ca,L}}$ to interrupt [repolarization](@entry_id:150957).

*   **Delayed Afterdepolarizations (DADs):** These occur after the action potential is complete, during diastole (Phase 4). The underlying cause is cellular **[calcium overload](@entry_id:177336)**. Spontaneous, arrhythmogenic release of calcium from an overloaded SR elevates cytosolic calcium, which in turn activates the electrogenic **[sodium-calcium exchanger](@entry_id:143023) (NCX)** in its forward mode ($3\,\mathrm{Na}^{+}$ in for $1\,\mathrm{Ca}^{2+}$ out). This generates a net inward, depolarizing current ($I_{\mathrm{NCX}}$) that can bring the cell to threshold. DADs are typically promoted by tachycardia, catecholaminergic stress, and digitalis toxicity.

#### Disorders of Impulse Conduction: Refractoriness and Reentry

*   **Refractoriness:** Following an action potential, the cell enters a refractory period during which it is less excitable or completely inexcitable.
    *   The **Absolute Refractory Period (ARP)** is the interval during which no stimulus, no matter how strong, can elicit another AP. This is because the fast [sodium channels](@entry_id:202769) are in an inactivated state.
    *   The **Relative Refractory Period (RRP)** follows the ARP. During this time, a stronger-than-normal stimulus is required to elicit an AP, and the resulting AP will have a slower upstroke and reduced amplitude.
    The basis for refractoriness lies in the recovery from inactivation of the $I_{\mathrm{Na}}$ channels. These channels have both fast ($h$) and slow ($j$) inactivation gates that close during the AP plateau. Recovery of excitability requires these gates to reopen during diastole, a time-dependent process. The ARP lasts until a critical fraction of channels have recovered. Near-normal excitability is restored only after a much longer period, governed primarily by the slow recovery of the $j$ gate [@problem_id:2555278].

*   **Reentry:** Reentry is the most common mechanism of clinical tachyarrhythmias. It occurs when an electrical impulse does not terminate but instead propagates repeatedly through a closed loop. Three conditions are required [@problem_id:2555262]:
    1.  An anatomical or functional circuit with at least two pathways.
    2.  **Unidirectional block** in one of the pathways. This often occurs when a premature impulse arrives at a point where the two pathways have different refractory periods. The impulse is blocked in the pathway with the longer refractory period but conducts down the other.
    3.  Slow conduction through the unblocked pathway, such that by the time the impulse reaches the other end of the blocked pathway, that tissue has recovered excitability and can be activated retrogradely.

If the [wavefront](@entry_id:197956) can then re-enter the originally blocked pathway (now proximally) after it has recovered, a sustained circus movement is established. Differentiating a reentrant tachycardia from one caused by a focal automatic source can be done by observing the activation sequence (centrifugal spread from a focus vs. a looping pattern in reentry) and the response to overdrive pacing (a technique known as entrainment, which elicits characteristic responses in reentrant circuits) [@problem_id:2555262].

#### Mechano-Electric Coupling: A Link Between Force and Rhythm

The electrical and mechanical functions of the heart are bidirectionally linked. Just as electricity causes contraction, mechanical forces can alter electrical properties. This **[mechano-electric coupling](@entry_id:163204) (MEC)** can be arrhythmogenic. Myocardial stretch, as occurs in acute volume overload or [heart failure](@entry_id:163374), can activate **stretch-activated channels (SACs)**. These are typically non-selective cation channels. When open, they provide a depolarizing inward current [@problem_id:2555253]. This [depolarization](@entry_id:156483) can bring a resting cell closer to its firing threshold, potentially initiating triggered activity. Furthermore, by increasing [membrane conductance](@entry_id:166663), stretch can decrease the membrane resistance ($r_m$), which in turn shortens the [space constant](@entry_id:193491) ($\lambda$), impairing conduction and potentially contributing to reentrant arrhythmias [@problem_id:2555228].