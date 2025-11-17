## Introduction
The cardiovascular system is the body's essential transport network, responsible for delivering oxygen and nutrients, removing waste, and maintaining homeostasis through the intricate control of pressure and flow. Its remarkable function arises from a seamless integration of electrical, chemical, and mechanical events that span from the molecular level of a single [ion channel](@entry_id:170762) to the systemic behavior of the entire circulation. Understanding this complexity requires bridging the gap between isolated components and their collective function, a challenge this article aims to address. By dissecting the system into its core components and then reassembling them, we can appreciate both its elegant design and its vulnerabilities in disease. This article will guide you through the core tenets of [cardiovascular physiology](@entry_id:153740). The "Principles and Mechanisms" section will lay the foundation, exploring the electrical basis of the heartbeat, the mechanics of [muscle contraction](@entry_id:153054), and the [physics of blood flow](@entry_id:163012). Following this, "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied to understand [pathophysiology](@entry_id:162871) and the system's vital links with other organs. Finally, the "Hands-On Practices" section will provide opportunities to apply this knowledge to solve quantitative problems, solidifying your grasp of these critical concepts.

## Principles and Mechanisms

The cardiovascular system operates through an intricate interplay of electrical, chemical, and mechanical phenomena, seamlessly integrated from the molecular level to the whole organism. This chapter delineates the fundamental principles and mechanisms that govern cardiac function and vascular [hemodynamics](@entry_id:149983), providing a framework for understanding both physiological regulation and pathophysiological [derangement](@entry_id:190267). We will begin with the electrical signals that initiate the heartbeat, explore how these signals are transduced into mechanical force, analyze the heart's performance as a pump, investigate the physical principles of [blood flow](@entry_id:148677) through the vasculature, and conclude with the homeostatic control systems that ensure cardiovascular stability.

### The Electrical Basis of Cardiac Function

The rhythmic contraction of the heart originates from precisely orchestrated electrical events known as action potentials. The characteristics of these action potentials vary significantly between different cardiac cell types, giving rise to distinct functional roles.

#### The Ventricular Action Potential

The action potential of a ventricular myocyte is responsible for triggering the powerful contractions that eject blood into the circulation. It is characterized by a long duration and a stable resting potential, which can be divided into five distinct phases [@problem_id:2781804]. The [membrane potential](@entry_id:150996) ($V_m$) at any moment is determined by the net sum of all [ionic currents](@entry_id:170309) flowing across the cell membrane, according to the relationship $I_{\text{ion}} = g_{\text{ion}}(V_m - E_{\text{ion}})$, where $g_{\text{ion}}$ is the conductance for a specific ion and $E_{\text{ion}}$ is its Nernst equilibrium potential.

*   **Phase 4: The Resting Potential.** In a quiescent ventricular myocyte, the membrane is held at a stable, negative resting potential of approximately $-90\,\text{mV}$. This potential is close to the Nernst potential for potassium ($E_K$). It is primarily maintained by the **inward [rectifier](@entry_id:265678) potassium current ($I_{K1}$)**. The channels carrying this current have high conductance at negative potentials, allowing a small outward leak of $K^+$ ions that counteracts any small inward leak of other ions, thus clamping the membrane potential.

*   **Phase 0: The Rapid Upstroke.** Upon excitation from a neighboring cell, the membrane depolarizes to a threshold of about $-70\,\text{mV}$. This triggers the explosive activation of [voltage-gated sodium channels](@entry_id:139088), giving rise to a massive, transient **sodium current ($I_{Na}$)**. The strong electrochemical gradient for $Na^+$ (with $E_{Na} \approx +60\,\text{mV}$) drives a rapid influx of positive charge, causing the [membrane potential](@entry_id:150996) to soar to approximately $+20\,\text{mV}$ in a fraction of a millisecond.

*   **Phase 1: Early Repolarization.** Immediately following the peak of the upstroke, the fast [sodium channels](@entry_id:202769) inactivate. Simultaneously, a specific population of [potassium channels](@entry_id:174108) opens, generating the **transient outward potassium current ($I_{to}$)**. This brief efflux of $K^+$ ions causes a small, initial [repolarization](@entry_id:150957), creating a characteristic "notch" at the beginning of the action potential.

*   **Phase 2: The Plateau.** The defining feature of the ventricular action potential is its long plateau, which lasts for 200-300 milliseconds. During this phase, $V_m$ is maintained at a depolarized level. This is achieved by a delicate balance between an inward, depolarizing current and outward, repolarizing currents. The primary inward current is the **L-type calcium current ($I_{CaL}$)**, carried by $Ca^{2+}$ ions flowing through slowly inactivating channels. This [calcium influx](@entry_id:269297) is not only crucial for maintaining the plateau but is also the essential trigger for muscle contraction. The inward $I_{CaL}$ is opposed by outward potassium currents, chiefly the **rapid ($I_{\mathrm{Kr}}$) and slow ($I_{\mathrm{Ks}}$) delayed rectifier potassium currents**. The inward [rectifier](@entry_id:265678) current, $I_{K1}$, is functionally suppressed at these depolarized potentials.

*   **Phase 3: Final Repolarization.** The plateau is terminated as the balance of currents shifts decisively in favor of [repolarization](@entry_id:150957). The L-type calcium channels progressively inactivate, reducing the inward $I_{CaL}$, while the delayed [rectifier](@entry_id:265678) [potassium channels](@entry_id:174108) ($I_{\mathrm{Kr}}$ and $I_{\mathrm{Ks}}$) reach their peak activation. The resulting dominant outward potassium current rapidly drives the [membrane potential](@entry_id:150996) back down towards $E_K$.

#### The Pacemaker Potential and Automaticity

Unlike ventricular myocytes, the cells of the sinoatrial (SA) node are characterized by **automaticity**—the ability to generate spontaneous action potentials. This property stems from a fundamentally different set of [ionic currents](@entry_id:170309) that prevent the establishment of a stable resting potential [@problem_id:2781741].

Instead of a stable Phase 4, SA node cells exhibit a slow, spontaneous **diastolic [depolarization](@entry_id:156483)**. This depolarization is driven by a net inward current. The key contributor is the **"funny" current ($I_f$)**, a mixed cation current carried by [hyperpolarization](@entry_id:171603)-activated cyclic nucleotide-gated (HCN) channels. These channels uniquely activate upon [hyperpolarization](@entry_id:171603) at the end of the preceding action potential. As the membrane depolarizes, the **T-type calcium current ($I_{CaT}$)** also contributes an inward current. This pacemaker depolarization is further aided by the deactivation of the potassium currents ($I_K$) that caused the prior [repolarization](@entry_id:150957).

Once the diastolic depolarization drives the membrane potential to its threshold (around $-40\,\text{mV}$), an action potential is triggered. However, because the maximum diastolic potential of SA node cells is only about $-60\,\text{mV}$, most fast sodium channels are in a permanently inactivated state. Consequently, the upstroke (Phase 0) in SA node cells is slower and is mediated primarily by the influx of calcium through **L-type calcium channels ($I_{CaL}$)**, not [sodium channels](@entry_id:202769).

The distinct ionic machinery—the presence of $I_f$ and absence of a strong $I_{K1}$ in SA node cells, versus the stable $I_{K1}$ and dominant $I_{Na}$ in ventricular cells—is the fundamental basis for their respective roles as pacemakers and followers. One can conceptually convert a ventricular myocyte into a pacemaker by removing the stabilizing $I_{K1}$ current and introducing the depolarizing $I_f$ current [@problem_id:2781741].

#### Autonomic Modulation of Pacemaking

The rate of pacemaking, and thus the heart rate, is dynamically regulated by the [autonomic nervous system](@entry_id:150808). Stimulation of $\beta_1$-[adrenergic receptors](@entry_id:169433) by norepinephrine (from sympathetic nerves) or [epinephrine](@entry_id:141672) (from the [adrenal medulla](@entry_id:150815)) leads to a positive chronotropic (rate-increasing) effect. This is mediated by an increase in intracellular cyclic AMP (cAMP). cAMP directly binds to HCN channels, shifting their activation voltage to be more positive. This increases the inward $I_f$ current at any given diastolic potential, steepening the slope of diastolic depolarization. PKA-mediated phosphorylation also enhances $I_{CaL}$. The steeper slope means the [threshold potential](@entry_id:174528) is reached more quickly, shortening the [cardiac cycle](@entry_id:147448) length. For instance, an increase in the diastolic [depolarization](@entry_id:156483) slope from $0.06\,\text{mV/ms}$ to $0.09\,\text{mV/ms}$ would shorten the time to reach a $20\,\text{mV}$ threshold from approximately $333\,\text{ms}$ to $222\,\text{ms}$, a significant acceleration of heart rate [@problem_id:2781741].

### Excitation-Contraction Coupling: From Ion Flux to Force

The action potential is the electrical command that initiates mechanical contraction. The process that links these two events is known as **[excitation-contraction coupling](@entry_id:152858) (ECC)**, and at its heart lies the tightly controlled fluctuation of intracellular calcium concentration, known as the calcium transient.

#### The Mechanism of Calcium-Induced Calcium Release (CICR)

In mammalian ventricular myocytes, the influx of calcium across the sarcolemma during the action potential is insufficient on its own to activate the contractile machinery. Instead, it serves as a trigger for the release of a much larger store of calcium from the [sarcoplasmic reticulum](@entry_id:151258) (SR), an intracellular organelle. This amplification mechanism is termed **[calcium-induced calcium release](@entry_id:156792) (CICR)** [@problem_id:2781780].

The process begins during Phase 2 of the action potential. The opening of L-type calcium channels (LTCCs), which are concentrated in invaginations of the cell membrane called transverse tubules (T-tubules), allows a small amount of $Ca^{2+}$ to enter the cell. This influx occurs in a highly restricted subspace, the dyad, where the T-tubule membrane is in close proximity to the SR membrane. This local, high concentration of "trigger" $Ca^{2+}$ binds to and activates **[ryanodine receptor](@entry_id:166754) type 2 (RyR2)** channels located on the SR membrane. The opening of RyR2 channels releases a large plume of $Ca^{2+}$ from the SR into the cytosol. The summation of these elementary release events (calcium sparks) from thousands of dyads across the cell produces the global, rapid rise in cytosolic $[Ca^{2+}]$ that constitutes the upstroke of the calcium transient. This rise in $[Ca^{2+}]$ allows calcium to bind to the myofilament protein [troponin](@entry_id:152123) C, initiating [cross-bridge cycling](@entry_id:172817) and force generation.

#### Relaxation and Calcium Removal

For the muscle to relax, the calcium transient must be terminated. This requires removing $Ca^{2+}$ from the cytosol and unbinding it from [troponin](@entry_id:152123) C. This is accomplished by two primary transport systems [@problem_id:2781780]:

1.  **SERCA (Sarco/Endoplasmic Reticulum Ca²⁺-ATPase):** This is an ATP-driven pump on the SR membrane that actively transports $Ca^{2+}$ from the cytosol back into the SR, against a steep concentration gradient. This process is responsible for the majority of calcium removal and thus dictates the rate of relaxation. The activity of SERCA is regulated by a small protein called **phospholamban (PLN)**. In its dephosphorylated state, PLN inhibits SERCA. However, upon $\beta$-[adrenergic stimulation](@entry_id:172807), PLN is phosphorylated by protein kinase A, which relieves this inhibition and accelerates $Ca^{2+}$ [reuptake](@entry_id:170553), leading to faster relaxation (a positive lusitropic effect).

2.  **Sodium-Calcium Exchanger (NCX):** Located on the sarcolemma, this transporter removes the remaining calcium from the cell entirely. Operating in its "forward mode," it uses the energy stored in the sodium gradient (high $[Na^+]$ outside, low inside) to extrude one $Ca^{2+}$ ion in exchange for the entry of three $Na^+$ ions. This [stoichiometry](@entry_id:140916) results in the net influx of one positive charge, generating a small inward electrical current that contributes to the shape of the action potential plateau.

The coordinated action of LTCCs, RyR2, SERCA, and NCX sculpts the calcium transient, determining its amplitude, which governs the force of contraction, and its duration, which governs the timing of relaxation.

### The Heart as a Mechanical Pump

The electrical and chemical events described above culminate in the coordinated mechanical function of the heart as a pulsatile pump. This function is best understood by examining the sequence of pressure and volume changes during a single heartbeat, known as the [cardiac cycle](@entry_id:147448).

#### The Cardiac Cycle: A Sequence of Pressure and Flow Events

The heart's valves act as passive one-way gates, opening and closing solely in response to pressure gradients. A valve opens when the pressure upstream from it exceeds the pressure downstream ($\Delta P > 0$) and closes when this gradient is zero or reversed. Analyzing the left heart provides a clear illustration of the mechanical cycle [@problem_id:2781793].

1.  **Ventricular Filling:** This phase begins when the left [ventricular pressure](@entry_id:140360) ($P_{LV}$) falls below the left atrial pressure ($P_{LA}$), causing the mitral valve to open. Blood flows passively from the atrium into the relaxing ventricle. This phase includes early rapid filling and a slower period called diastasis.

2.  **Atrial Systole:** Late in diastole, the atrium contracts, actively pushing an additional volume of blood into the ventricle. Throughout filling and atrial [systole](@entry_id:160666), $P_{LV}$ remains lower than aortic pressure ($P_{Ao}$), so the aortic valve is closed.

3.  **Isovolumic Contraction:** Following atrial [systole](@entry_id:160666), the ventricle begins to contract. $P_{LV}$ rises sharply. As soon as $P_{LV}$ exceeds $P_{LA}$, the mitral valve closes. For a brief period, $P_{LV}$ is still lower than $P_{Ao}$, so the aortic valve remains closed. With both valves closed, the ventricle contracts around a constant volume of blood—hence, "isovolumic."

4.  **Ejection:** Ventricular contraction continues, and when $P_{LV}$ surpasses $P_{Ao}$, the aortic valve is forced open, and blood is ejected into the aorta. Throughout ejection, $P_{LV}$ remains higher than $P_{LA}$, so the mitral valve stays closed.

5.  **Isovolumic Relaxation:** As the ventricle begins to relax at the end of [systole](@entry_id:160666), $P_{LV}$ falls. The moment it drops below $P_{Ao}$, the aortic valve snaps shut. Because $P_{LV}$ is still higher than $P_{LA}$, the mitral valve also remains closed. The ventricle relaxes with both valves shut, and its volume is again constant. This continues until $P_{LV}$ falls below $P_{LA}$, initiating the next filling phase.

#### The Pressure-Volume Loop and Determinants of Cardiac Performance

A powerful graphical representation of the [cardiac cycle](@entry_id:147448) is the **pressure-volume (PV) loop**. Plotting left [ventricular pressure](@entry_id:140360) against left ventricular volume over a single cycle traces a closed loop. The width of the loop represents the **[stroke volume](@entry_id:154625) ($SV$)**—the volume of blood ejected per beat ($SV = EDV - ESV$, where $EDV$ is the end-diastolic volume and $ESV$ is the end-systolic volume). The area within the loop represents the mechanical work done by the ventricle.

Cardiac performance, quantified by **[cardiac output](@entry_id:144009) ($CO = HR \times SV$)**, is determined by four key factors: [preload](@entry_id:155738), afterload, contractility, and [heart rate](@entry_id:151170) [@problem_id:2781771].

*   **Preload:** This refers to the load on the ventricle at the end of diastole, best represented by the EDV or the degree of myocardial stretch. The **Frank-Starling mechanism** describes the heart's intrinsic ability to adjust its output in response to changes in [preload](@entry_id:155738). An increase in [preload](@entry_id:155738) (e.g., due to increased [venous return](@entry_id:176848)) leads to a more forceful contraction and an increased [stroke volume](@entry_id:154625). On a PV loop, this is seen as a rightward shift to a higher EDV, resulting in a wider loop and thus a larger SV. Critically, this occurs along a fixed **end-systolic pressure-volume relation (ESPVR)**, which defines the maximum pressure the ventricle can generate at a given volume. The cellular basis for this mechanism is **[length-dependent activation](@entry_id:171390)**: stretching the sarcomeres increases the sensitivity of the myofilament protein [troponin](@entry_id:152123) C to calcium, leading to more force production for the same calcium transient [@problem_id:2781770].

*   **Contractility (Inotropy):** This refers to the intrinsic force-generating capacity of the myocardium, independent of [preload](@entry_id:155738) or afterload. An increase in contractility, such as that caused by $\beta$-[adrenergic stimulation](@entry_id:172807), results in a more forceful and rapid contraction for any given [preload](@entry_id:155738). On the PV loop, an increase in contractility is represented by an upward and leftward shift of the ESPVR, indicating a higher end-systolic [elastance](@entry_id:274874) ($E_{es}$). This allows the ventricle to eject blood more completely, resulting in a smaller ESV and a larger SV. The cellular mechanism is an increase in the amplitude and kinetics of the cytosolic calcium transient [@problem_id:2781770]. It is crucial to distinguish the Frank-Starling mechanism (moving along a fixed contractility curve) from a true change in contractility (shifting to a new curve).

*   **Afterload:** This is the load or pressure the ventricle must work against to eject blood, primarily determined by arterial pressure and vascular resistance. An increase in afterload impedes ventricular ejection. For a given [preload](@entry_id:155738) and contractility, a higher afterload will cause the aortic valve to close earlier in ejection, resulting in a larger ESV and a correspondingly smaller SV.

*   **Heart Rate (Chronotropy):** While an increase in heart rate ($HR$) directly increases cardiac output by the formula $CO = HR \times SV$, this effect is not limitless. As heart rate increases, the time available for diastolic filling decreases. At very high rates, this can compromise [preload](@entry_id:155738) ($EDV$) to such an extent that the resulting fall in [stroke volume](@entry_id:154625) outweighs the increase in rate, causing cardiac output to plateau or even decline.

### Hemodynamics: The Physics of Blood Flow and Pressure

The vascular network serves as the conduit for blood delivery, and the principles governing flow through these vessels are rooted in fluid dynamics.

#### Fundamental Quantities: Pressure, Flow, and Resistance

The three primary variables in [hemodynamics](@entry_id:149983) are pressure, flow, and resistance. **Volumetric flow rate ($Q$)** is the volume of blood passing a point per unit time (e.g., $\text{m}^3/\text{s}$ or $\text{L/min}$). **Pressure ($P$)** is the force exerted by the blood per unit area of the vessel wall (e.g., Pascals or mmHg); its physical dimension is also energy per unit volume. The gradient of pressure is the driving force for blood flow [@problem_id:2781760].

For steady, non-[pulsatile flow](@entry_id:191445), the relationship between these variables is described by a hydraulic equivalent of Ohm's law: $\Delta P = Q \times R$. Here, **[hydraulic resistance](@entry_id:266793) ($R$)** is a scalar quantity representing the opposition to flow. It is defined as the ratio of the mean pressure drop ($\Delta \bar{P}$) to the mean flow ($\bar{Q}$). This simple concept is useful for analyzing mean [blood flow](@entry_id:148677) through the systemic or pulmonary circulations.

#### The Challenge of Pulsatile Flow: Vascular Impedance

In the arterial system, flow is not steady but pulsatile, driven by the intermittent ejection from the heart. For pulsatile phenomena, the simple concept of resistance is inadequate because it neglects the dynamic effects of blood inertia and vessel elasticity. The more comprehensive parameter is **vascular impedance ($Z(\omega)$)** [@problem_id:2781760].

Vascular impedance is a complex, frequency-dependent measure defined as the ratio of the oscillatory components of pressure to flow at each frequency ($\omega$) present in the pulse. As a complex number, it contains information about both magnitude and phase.
*   The **real part** of impedance represents the dissipative, frictional energy losses, analogous to resistance.
*   The **imaginary part** ([reactance](@entry_id:275161)) represents [energy storage](@entry_id:264866) elements: the inertia of the blood mass (which acts like an inductor) and the compliance of the elastic vessel walls (which acts like a capacitor).

The units of impedance are the same as resistance ($\text{Pa} \cdot \text{s} \cdot \text{m}^{-3}$). In the specific case of zero frequency (i.e., steady flow), the magnitude of the impedance, $|Z(0)|$, reduces to the [hydraulic resistance](@entry_id:266793), $R$.

#### Arterial Wall Properties: Compliance and Viscoelasticity

A key property determining vascular impedance and arterial function is **compliance ($C$)**, defined as the change in volume per unit change in pressure ($C = \Delta V / \Delta P$). Its reciprocal is **[elastance](@entry_id:274874) ($E = \Delta P / \Delta V$)**. The high compliance of large arteries like the aorta allows them to stretch during [systole](@entry_id:160666), storing a portion of the [stroke volume](@entry_id:154625), and then recoil during diastole, maintaining blood flow and pressure. This "Windkessel effect" smooths the pulsatile output of the heart into a more continuous flow in the periphery.

Arterial walls are not perfectly elastic; they are **viscoelastic**. This means their mechanical response depends on the rate of deformation [@problem_id:2781734]. When measured dynamically (at physiological frequencies), arteries appear stiffer (have a lower compliance and higher [elastance](@entry_id:274874)) than when measured under quasi-static (very slow) conditions. This frequency-dependent stiffening is a hallmark of [viscoelasticity](@entry_id:148045). Furthermore, in a viscoelastic vessel, the pressure waveform leads the volume waveform by a certain phase angle. This [phase lag](@entry_id:172443) reflects [energy dissipation](@entry_id:147406) as heat within the vessel wall during each cycle of stretching and recoil, a phenomenon known as hysteresis.

### Microcirculation and Systemic Integration

While large arteries serve as conduits, the ultimate purpose of the circulation is to facilitate exchange of nutrients, gases, and waste products between blood and tissues. This occurs in the vast network of capillaries.

#### Fluid Exchange in the Capillaries: The Starling Principle

Fluid movement across the capillary endothelium is governed by the balance of hydrostatic and colloid osmotic (oncotic) pressures, a relationship known as the **Starling principle** [@problem_id:2781748]. Four forces are at play:

1.  **Capillary Hydrostatic Pressure ($P_c$):** The [blood pressure](@entry_id:177896) inside the capillary, which tends to push fluid *out* of the capillary into the interstitial space ([filtration](@entry_id:162013)).
2.  **Interstitial Hydrostatic Pressure ($P_i$):** The [fluid pressure](@entry_id:270067) in the interstitial space, which tends to push fluid *into* the capillary (opposing [filtration](@entry_id:162013)).
3.  **Capillary Oncotic Pressure ($\pi_c$):** The osmotic pressure generated by plasma proteins (mainly albumin) that are largely confined to the capillary. It tends to draw water *into* the capillary (absorption).
4.  **Interstitial Oncotic Pressure ($\pi_i$):** The osmotic pressure generated by the small amount of protein that has leaked into the [interstitial fluid](@entry_id:155188). It tends to draw water *out* of the capillary.

The [net filtration pressure](@entry_id:155463) is given by the Starling equation. The effectiveness of the oncotic pressure gradient is modulated by the **reflection coefficient ($\sigma$)**, a dimensionless number between 0 and 1. A $\sigma$ of 1 means the barrier is completely impermeable to protein, yielding the full osmotic effect. A $\sigma$ of 0 means the barrier is freely permeable, and proteins exert no osmotic force. For a typical continuous capillary, $\sigma$ is close to 1. The balance of these forces determines whether there is net filtration or net absorption at any point along the capillary.

#### Systemic Control: The Arterial Baroreflex

To maintain cardiovascular stability in the face of perturbations, the body employs numerous control systems. The most important rapid-acting mechanism for regulating systemic arterial pressure is the **[arterial baroreflex](@entry_id:148008)** [@problem_id:2781795]. This is a classic [negative feedback loop](@entry_id:145941).

*   **Sensors:** Mechanoreceptors (stretch receptors) located in the walls of the carotid sinuses and the aortic arch. These receptors are nerve endings that increase their [firing rate](@entry_id:275859) in response to increased arterial stretch, which is proportional to arterial pressure.

*   **Afferent Pathways:** The signals from the [carotid sinus](@entry_id:152256) receptors travel to the brainstem via the glossopharyngeal nerve (cranial nerve IX). Signals from the aortic arch receptors travel via the [vagus nerve](@entry_id:149858) (cranial nerve X).

*   **Central Integration:** These afferent nerves terminate in the nucleus tractus solitarius (NTS) in the medulla. The NTS processes this information and projects to other medullary centers that control autonomic outflow. An increase in baroreceptor input excites parasympathetic centers (like the nucleus ambiguus) and inhibits sympathetic centers (like the rostral ventrolateral medulla).

*   **Efferent Pathways:** The reflex response is carried by two autonomic efferent limbs: (1) an increase in parasympathetic (vagal) activity to the heart, and (2) a decrease in sympathetic activity to the heart and blood vessels.

*   **Effectors and Response:** The manipulated variables are adjusted to counteract the initial pressure change. An increase in arterial pressure thus reflexively causes:
    *   A decrease in [heart rate](@entry_id:151170) (due to increased vagal tone and decreased sympathetic tone at the SA node).
    *   A decrease in [myocardial contractility](@entry_id:175876) (due to decreased sympathetic tone).
    *   Vasodilation of arterioles and veins (due to decreased sympathetic tone on [vascular smooth muscle](@entry_id:154801)), which reduces [total peripheral resistance](@entry_id:153798) and promotes venous pooling.

Together, these responses decrease [cardiac output](@entry_id:144009) and [total peripheral resistance](@entry_id:153798), lowering arterial pressure back toward its homeostatic set-point. This entire reflex arc operates on a timescale of seconds, providing powerful, moment-to-moment stabilization of blood pressure.