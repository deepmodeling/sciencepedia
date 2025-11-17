## Introduction
The regulation of [acid-base balance](@entry_id:139335) is a cornerstone of [animal physiology](@entry_id:140481), a critical homeostatic process that maintains the pH of body fluids within a narrow, life-sustaining range. The stability of this internal environment is paramount, as even minute deviations can drastically alter [protein structure](@entry_id:140548) and enzyme function, threatening cellular and organismal viability. This article addresses the complex challenge of understanding how animals integrate fundamental chemical laws, molecular machinery, and coordinated organ systems to achieve such precise control.

Over the following chapters, you will embark on a journey from the molecular to the macroscopic. The first chapter, **Principles and Mechanisms**, deconstructs the foundational chemical principles of buffering, the kinetics of [carbon dioxide transport](@entry_id:150438), the crucial allosteric role of hemoglobin, and the systemic models used to analyze acid-base status. Next, **Applications and Interdisciplinary Connections** explores how these core mechanisms are applied in diverse real-world contexts, from dietary challenges and intense exercise to extreme environmental adaptations, connecting physiology with ecology and evolutionary biology. Finally, **Hands-On Practices** will allow you to apply this knowledge to solve quantitative problems, reinforcing your understanding of how to diagnose and interpret acid-base disturbances.

## Principles and Mechanisms

The regulation of [acid-base balance](@entry_id:139335) is a quintessential example of physiological homeostasis, involving a sophisticated interplay of chemical buffering, enzymatic catalysis, and [membrane transport](@entry_id:156121), all coordinated by complex control systems. This chapter will deconstruct the core principles and mechanisms that enable animals to maintain the pH of their body fluids within the narrow bounds required for life, starting from fundamental chemical laws and building toward integrated organ and systemic function.

### Foundational Chemical Principles of Aqueous Buffering

At its heart, [acid-base physiology](@entry_id:153342) is the study of the concentration and dynamics of hydrogen ions ($H^+$) in an aqueous environment. The concentration of free hydrogen ions is represented on a [logarithmic scale](@entry_id:267108) as **pH**, defined as $pH = -\log_{10}(a_{H^+})$, where $a_{H^+}$ is the hydrogen ion activity. Because the rates of virtually all biochemical reactions and the structures of all proteins are exquisitely sensitive to $pH$, its precise regulation is a non-negotiable condition for cellular function.

#### The Central Role of the Proton: The Brønsted-Lowry Framework

To understand how $pH$ is regulated, we must adopt an appropriate chemical framework. While several definitions of acids and bases exist, the most direct and powerful for physiological contexts is the **Brønsted-Lowry concept**. This framework defines an **acid** as a species that can donate a proton ($H^+$) and a **base** as a species that can accept a proton. An acid, upon donating a proton, becomes its **conjugate base**, and a base, upon accepting a proton, becomes its **conjugate acid**.

Consider the major [buffer systems](@entry_id:148004) in vertebrate blood: the bicarbonate system ($\text{H}_2\text{CO}_3 / \text{HCO}_3^-$), the phosphate system ($\text{H}_2\text{PO}_4^- / \text{HPO}_4^{2-}$), and protein-based systems, such as the imidazole groups of histidine residues in hemoglobin. In each case, the buffering action involves the transfer of a proton. For example:
$$ \text{H}_2\text{CO}_3 \rightleftharpoons \text{H}^+ + \text{HCO}_3^- $$
Here, carbonic acid ($\text{H}_2\text{CO}_3$) is the Brønsted-Lowry acid, and the bicarbonate ion ($\text{HCO}_3^-$) is its conjugate base. The power of this framework lies in its focus on the currency of [physiological acid-base balance](@entry_id:169357): the proton. By describing all buffering reactions as [proton transfer](@entry_id:143444) equilibria, and applying the law of mass action along with principles of [mass conservation](@entry_id:204015) and [electroneutrality](@entry_id:157680), one can construct a complete quantitative model to predict the $pH$ of a complex solution like blood.

Other [acid-base theories](@entry_id:141841) are less suitable. The Arrhenius theory, which defines acids as producers of $H^+$ and bases as producers of hydroxide ions ($OH^-$) in water, is too restrictive; it cannot properly account for the basicity of crucial physiological species like $\text{HCO}_3^-$ or $\text{HPO}_4^{2-}$, which act by accepting protons, not by producing $OH^-$. Conversely, the Lewis theory, which defines an acid as an electron-pair acceptor and a base as an electron-pair donor, is too general. While all Brønsted-Lowry reactions can be viewed through a Lewis lens (the proton is an electron-pair acceptor), the Lewis framework encompasses many reactions that do not involve protons at all. For the specific problem of regulating $pH$, which is by definition a measure of proton activity, the Brønsted-Lowry concept provides the most direct and parsimonious descriptive and predictive power [@problem_id:2543599].

#### Quantifying Buffer Capacity: The Nonbicarbonate Buffers

A **[buffer system](@entry_id:149082)** is a solution containing a [weak acid](@entry_id:140358) and its conjugate base, which resists changes in $pH$ upon the addition of acid or base. The effectiveness of a buffer is quantified by its **buffer value** or **[buffer capacity](@entry_id:139031)**, denoted by the symbol $\beta$. It is operationally defined as the amount of strong acid or base required to change the $pH$ of a one-liter solution by one unit:
$$ \beta = \frac{d[\text{Base}]}{d(\mathrm{pH})} = -\frac{d[\text{Acid}]}{d(\mathrm{pH})} $$
The units of buffer value are typically $\text{mmol}\,\text{L}^{-1}\,\text{pH}^{-1}$. For any given weak acid [buffer system](@entry_id:149082), its capacity is a function of its total concentration, $C$, and the prevailing $pH$ relative to its [acid dissociation constant](@entry_id:138231) ($pK_a$). This relationship is captured by the Van Slyke equation, which shows that [buffer capacity](@entry_id:139031) is maximal when $pH = pK_a$.

In whole blood, the total [buffering capacity](@entry_id:167128) is the sum of contributions from the bicarbonate system and the **nonbicarbonate [buffers](@entry_id:137243)**. The nonbicarbonate buffer value, $\beta_{NB}$, represents the combined capacity of all [buffers](@entry_id:137243) other than the bicarbonate/$\text{CO}_2$ system. The principal nonbicarbonate buffers in blood are hemoglobin (contained within red blood cells), plasma proteins (primarily albumin), and inorganic and organic phosphates.

To appreciate their relative importance, we can partition the total nonbicarbonate buffer value of mammalian blood under typical physiological conditions (e.g., hemoglobin at $150\,\text{g L}^{-1}$, plasma proteins at $70\,\text{g L}^{-1}$). Detailed calculations reveal a clear hierarchy [@problem_id:2543451]:
*   **Hemoglobin**: Contributes approximately $20 - 24\,\text{mmol L}^{-1} \text{pH}^{-1}$, accounting for roughly $75-80\%$ of the total $\beta_{NB}$. Its high concentration and the presence of numerous histidine residues with $pK_a$ values near physiological $pH$ make it the dominant nonbicarbonate buffer.
*   **Plasma Proteins**: Contribute approximately $4 - 5\,\text{mmol L}^{-1} \text{pH}^{-1}$.
*   **Phosphates**: The combined contribution of inorganic phosphate and organic phosphates (like 2,[3-bisphosphoglycerate](@entry_id:169185), or 2,3-BPG, in [red blood cells](@entry_id:138212)) is relatively small, typically around $1.5\,\text{mmol L}^{-1} \text{pH}^{-1}$.

The total nonbicarbonate buffer value for whole blood is therefore on the order of $25-30\,\text{mmol L}^{-1} \text{pH}^{-1}$. This substantial intrinsic buffering provides the first line of defense against acid-base disturbances.

### The Carbon Dioxide-Bicarbonate System: Kinetics and Transport

While nonbicarbonate buffers are crucial, the bicarbonate system is unique. It is an **open system**, meaning its acidic component, dissolved carbon dioxide ($\text{CO}_2$), is volatile and its concentration is subject to physiological regulation by the lungs. This makes it the most powerful and dynamic [buffer system](@entry_id:149082) in the body. However, its effectiveness hinges on overcoming a significant kinetic barrier.

#### The Bottleneck of Uncatalyzed Hydration

The interconversion of $\text{CO}_2$ and bicarbonate actually occurs in two steps: a slow hydration/dehydration step, followed by a rapid proton [dissociation](@entry_id:144265)/association step.
$$ \text{CO}_2 + \text{H}_2\text{O} \underset{k_{dehyd}}{\stackrel{k_{hyd}}{\rightleftharpoons}} \text{H}_2\text{CO}_3 \rightleftharpoons \text{H}^+ + \text{HCO}_3^- $$
The second step, being an ionic reaction, is virtually instantaneous. The first step, however, is notoriously slow. At mammalian body temperature ($37\,^{\circ}\text{C}$), the uncatalyzed pseudo-first-order rate constant for $\text{CO}_2$ hydration, $k_{hyd}$, is only about $0.15\,\text{s}^{-1}$. This implies a characteristic reaction time ($\tau = 1/k_{hyd}$) of nearly 7 seconds.

This kinetic bottleneck has profound physiological implications. A [red blood cell](@entry_id:140482), for instance, typically transits a systemic capillary in less than one second (e.g., $0.75\,\text{s}$). During this brief window, without catalysis, only a small fraction (on the order of $1 - \exp(-0.15 \times 0.75) \approx 10\%$) of the $\text{CO}_2$ diffusing into the cell could be converted to bicarbonate [@problem_id:2543449]. The blood's ability to load $\text{CO}_2$ in the tissues and unload it in the lungs would be severely crippled, making it impossible to transport the vast quantities of $\text{CO}_2$ produced by metabolism.

#### Carbonic Anhydrase and the Chloride Shift

Nature's solution to this kinetic problem is the enzyme **[carbonic anhydrase](@entry_id:155448) (CA)**. This remarkably efficient [metalloenzyme](@entry_id:196860), found in high concentrations within [red blood cells](@entry_id:138212) and other key locations like renal tubule cells, accelerates the hydration/[dehydration reaction](@entry_id:164777) by a factor of more than $10^7$. In the presence of CA, the [effective rate constant](@entry_id:202512) for $\text{CO}_2$ conversion becomes enormous ($k_{eff} \gg 10^3\,\text{s}^{-1}$), and the reaction reaches equilibrium in milliseconds, well within the capillary transit time.

The rapid, CA-catalyzed conversion of $\text{CO}_2$ inside the [red blood cell](@entry_id:140482) (RBC) is coupled to another critical piece of cellular machinery: the **anion exchanger 1 (AE1)**, also known as Band 3. This abundant membrane transporter facilitates the electroneutral, one-for-one exchange of intracellular bicarbonate ($\text{HCO}_3^-$) for extracellular chloride ($\text{Cl}^-$). This coupled system enables the efficient transport of $\text{CO}_2$ from tissues to lungs through the following sequence of events [@problem_id:2543538]:

1.  **In Systemic Tissues**: $\text{CO}_2$ produced by cells diffuses into the plasma and then into RBCs.
2.  Inside the RBC, CA rapidly hydrates $\text{CO}_2$ to form $\text{H}_2\text{CO}_3$, which immediately dissociates into $H^+$ and $\text{HCO}_3^-$.
3.  The protons ($H^+$) are buffered by hemoglobin (as discussed below).
4.  The rapidly accumulating bicarbonate ($\text{HCO}_3^-$) is exported from the RBC into the plasma by AE1 in exchange for chloride ions, which move into the cell. This process is known as the **[chloride shift](@entry_id:153095)**.

This elegant mechanism accomplishes two things: First, it allows the vast majority ($\sim70\%$) of $\text{CO}_2$ produced in the tissues to be transported to the lungs in the chemically converted, highly soluble form of plasma bicarbonate. Second, by continuously removing the products of the CA reaction, it maintains a steep concentration gradient for $\text{CO}_2$ to diffuse from the tissues into the blood.

In the pulmonary capillaries, the entire process reverses: low alveolar $P_{CO_2}$ causes $\text{CO}_2$ to diffuse out of the RBC. By Le Châtelier's principle, this drives the CA-catalyzed reaction in reverse. To supply the necessary substrate, the AE1 transporter mediates a **reverse [chloride shift](@entry_id:153095)**, importing $\text{HCO}_3^-$ from the plasma in exchange for $\text{Cl}^-$ efflux. The imported $\text{HCO}_3^-$ combines with protons released from hemoglobin upon [oxygenation](@entry_id:174489), and CA rapidly dehydrates the resulting $\text{H}_2\text{CO}_3$ to $\text{CO}_2$, which is then exhaled. The coordinated action of CA and AE1 is thus indispensable for both $\text{CO}_2$ uptake and release.

### Hemoglobin: An Allosteric Buffer

Hemoglobin is not merely a passive buffer; it is an active participant in acid-base dynamics, whose buffering properties are allosterically linked to its primary function of [oxygen transport](@entry_id:138803). This coupling is manifested in the Bohr and Haldane effects.

The molecular basis for this behavior lies in the [conformational change](@entry_id:185671) hemoglobin undergoes upon binding oxygen. Deoxygenated hemoglobin exists primarily in the low-affinity **T (tense) state**, while fully oxygenated hemoglobin adopts the high-affinity **R (relaxed) state**. This T-R transition alters the local electrostatic microenvironment of several [amino acid side chains](@entry_id:164196), critically shifting their $pK_a$ values [@problem_id:2543554].

Most importantly, the $pK_a$ values of several key histidine residues are significantly higher in the T state than in the R state. For example, the formation of a [salt bridge](@entry_id:147432) in the T state raises the $pK_a$ of the imidazole group of histidine-146 on the $\beta$-chain from about 6.0 to nearly 8.0. The consequence is that at the physiological pH of blood ($\sim7.2-7.4$), deoxygenated hemoglobin is more protonated—it binds more $H^+$—than oxygenated hemoglobin.

This phenomenon gives rise to two distinct, but mechanistically linked, effects:

*   The **Haldane Effect**: This refers to the observation that deoxygenated blood can carry more total $\text{CO}_2$ than oxygenated blood at the same $P_{CO_2}$. The mechanism is that upon deoxygenation in the tissues, hemoglobin becomes a stronger base, readily accepting the protons generated from the hydration of incoming $\text{CO}_2$. This buffering of protons facilitates further bicarbonate formation, thus increasing the blood's capacity to load $\text{CO}_2$.
*   The **Bohr Effect**: This refers to the observation that hemoglobin's affinity for oxygen is reduced by decreases in pH (increases in $[H^+]$). The mechanism is the [thermodynamic linkage](@entry_id:170354) between proton binding and [oxygen binding](@entry_id:174642). Since protons bind preferentially to and stabilize the low-affinity T state, an increase in proton concentration (as occurs in metabolically active tissues) pushes the allosteric equilibrium toward the T state, promoting the release of oxygen.

The Bohr and Haldane effects represent a perfect synergy for [respiratory gas exchange](@entry_id:154764). In the tissues, high $\text{CO}_2$ levels lead to proton production, which via the Bohr effect drives oxygen unloading from hemoglobin. The resulting deoxygenated hemoglobin, via the Haldane effect, becomes a better proton buffer, facilitating the transport of that very same $\text{CO}_2$ as bicarbonate. In the lungs, high oxygen levels drive proton release from hemoglobin, which helps convert bicarbonate back into $\text{CO}_2$ for exhalation.

### System-Level Regulation

Having established the chemical and molecular mechanisms, we can now examine how they are integrated into systemic models and controlled at the organ level.

#### Two Perspectives: Henderson-Hasselbalch vs. Stewart

Traditionally, systemic acid-base status is analyzed using the **Henderson-Hasselbalch (HH) equation** applied to the bicarbonate system:
$$ pH = pK_a' + \log_{10}\left(\frac{[\text{HCO}_3^-]}{\alpha_{CO_2} P_{CO_2}}\right) $$
In this view, $pH$ is determined by the ratio of a "metabolic component" ($[\text{HCO}_3^-]$) and a "respiratory component" ($P_{CO_2}$). While clinically useful for classification, the HH framework can be misleading about causality, as it treats $[\text{HCO}_3^-]$ as an [independent variable](@entry_id:146806) that can be manipulated directly.

A more fundamental and causally explicit framework is the **physicochemical approach**, developed by Peter Stewart. This approach begins from first principles: the law of [electroneutrality](@entry_id:157680) and the law of mass action for all weak acids in the system. It posits that the acid-base state of a solution like plasma is determined by three, and only three, **independent variables** [@problem_id:2543446]:

1.  **Strong Ion Difference ($SID$)**: The charge difference between all fully dissociated, "strong" cations (e.g., $Na^+, K^+, Ca^{2+}, Mg^{2+}$) and strong anions (e.g., $Cl^-$, sulfate). In essence, $SID = [\text{Strong Cations}] - [\text{Strong Anions}]$.
2.  **Total Weak Acid Concentration ($A_{tot}$)**: The total concentration of all non-volatile weak acids, primarily plasma proteins (albumin) and inorganic phosphate.
3.  **Partial Pressure of Carbon Dioxide ($P_{CO_2}$)**: The respiratory variable, regulated by ventilation.

In the Stewart model, these three independent variables—which are determined by the physiological functions of the gut, kidneys, and lungs—set the electrical and chemical landscape of the plasma. All other variables, including $[H^+]$ (and thus $pH$) and $[\text{HCO}_3^-]$, are **[dependent variables](@entry_id:267817)** that must adjust to satisfy the fundamental constraint of [electroneutrality](@entry_id:157680). For example, an infusion of sodium bicarbonate ($\text{NaHCO}_3$) raises blood $pH$. In the HH view, this is because we added bicarbonate. In the Stewart view, the causal agent is the addition of the strong ion $Na^+$, which increases the $SID$. To maintain [electroneutrality](@entry_id:157680), the concentrations of weak [anions](@entry_id:166728) must increase, which requires a decrease in $[H^+]$—hence, the pH rises. The added bicarbonate simply joins the pool of dependent weak ions. This approach provides a more rigorous understanding of the causal chains in acid-base disturbances.

#### Cellular pH Regulation: A Toolkit of Transporters

Just as the body regulates the pH of the extracellular fluid, individual cells must regulate their own intracellular pH ($pH_i$). They do so using a diverse toolkit of [membrane transport](@entry_id:156121) proteins that move acid or base equivalents across the cell membrane. The direction of transport is determined by the electrochemical gradients of the transported ions. Major families of $pH_i$ regulators include [@problem_id:2543492]:

*   **Acid Extruders (raise $pH_i$)**:
    *   **$Na^+/H^+$ Exchanger (NHE)**: Uses the strong inward gradient for $Na^+$ to drive the extrusion of $H^+$.
    *   **$Na^+$-Bicarbonate Cotransporter (NBC)**: Uses the $Na^+$ gradient to drive the influx of base equivalents ($\text{HCO}_3^-$).
    *   **V-type $H^+$-ATPase**: A primary active transporter that uses ATP to pump $H^+$ out of the cell.
*   **Acid Loaders (lower $pH_i$)**:
    *   **$Cl^-/\text{HCO}_3^-$ Exchanger (Anion Exchanger, AE)**: Typically mediates the electroneutral exchange of intracellular $\text{HCO}_3^-$ for extracellular $Cl^-$, resulting in a net loss of base.
*   **Lactic Acid Transport**:
    *   **Monocarboxylate Transporter (MCT)**: Mediates the electroneutral [cotransport](@entry_id:137109) of a proton with a monocarboxylate like lactate. In a glycolytic muscle fiber producing lactic acid, this transporter is crucial for extruding both the lactate anion and the proton, thereby defending $pH_i$.

The specific combination of transporters expressed by a cell is tailored to its unique physiological role and environment. A gill epithelial cell in a freshwater fish, for instance, might rely heavily on apical V-type H$^+$-ATPases to excrete acid into a low-$Na^+$ environment, while simultaneously using basolateral NBCs to absorb bicarbonate from the blood. A mammalian muscle fiber, in contrast, would rely on NHE and MCT to rapidly clear the massive acid load generated during intense exercise.

#### The Kidney: The Ultimate Regulator of Bicarbonate

While the lungs provide rapid control over $P_{CO_2}$, the kidneys are responsible for the long-term regulation of the body's [acid-base balance](@entry_id:139335) by controlling the concentration of plasma bicarbonate. This is achieved through two primary processes: reclamation of filtered bicarbonate and generation of new bicarbonate.

The vast majority ($\sim80-90\%$) of the bicarbonate filtered at the glomerulus is reclaimed in the **proximal tubule**. This process is an elegant demonstration of the principles discussed earlier [@problem_id:2543475]. It involves apical $H^+$ secretion (primarily via NHE3), which titrates luminal bicarbonate. This reaction is accelerated by a luminal, membrane-bound CA (CA-IV), forming $\text{CO}_2$ that diffuses into the cell. Inside the cell, cytosolic CA (CA-II) rapidly re-hydrates the $\text{CO}_2$ back to $H^+$ and $\text{HCO}_3^-$. The $H^+$ is recycled back into the [lumen](@entry_id:173725) via NHE3, while the "reclaimed" $\text{HCO}_3^-$ is transported across the basolateral membrane into the blood, primarily by an electrogenic $Na^+$-bicarbonate cotransporter (NBCe1). The overall rate of this reclamation process is limited by the maximal transport capacity of the slowest step in the sequence, which under many conditions is the basolateral [extrusion](@entry_id:157962) via NBCe1.

To compensate for metabolic acid loads, the kidneys must also generate **new bicarbonate**. This is accomplished in more distal parts of the [nephron](@entry_id:150239) and involves the [excretion](@entry_id:138819) of protons in the form of titratable acids (e.g., buffered by phosphate) and ammonium ions ($\text{NH}_4^+$). For every proton excreted in the urine, one "new" bicarbonate ion is effectively added to the blood.

#### Principles of Homeostatic Control: Why Compensation is Incomplete

When a primary acid-base disturbance occurs, the body mounts a **compensatory response**. A [metabolic acidosis](@entry_id:149371), for example, is compensated for by a [respiratory alkalosis](@entry_id:148343) (hyperventilation), and a [respiratory acidosis](@entry_id:156771) is compensated for by renal retention of bicarbonate. A fundamental rule of physiology is that this compensation is almost never complete; it moves the pH back *toward* the normal value, but not all the way back.

This is a direct consequence of the fact that physiological regulation operates via **negative [feedback [control system](@entry_id:274717)s](@entry_id:155291)** [@problem_id:2543500]. In these systems, a sensor (e.g., a chemoreceptor) detects the deviation of a regulated variable (e.g., pH) from its set-point. This deviation, or **error signal**, drives an effector response (e.g., increased ventilation) that counteracts the initial disturbance. As the effector corrects the disturbance, the pH moves closer to the [set-point](@entry_id:275797), and the error signal diminishes. Because the compensatory response is driven by the [error signal](@entry_id:271594), the drive for compensation is progressively reduced as the correction proceeds. If the pH were to return completely to its set-point, the [error signal](@entry_id:271594) would become zero, and the stimulus for compensation would vanish, causing the primary disturbance to re-emerge. Therefore, in a compensated steady state, a small, residual pH deviation must persist to provide the continuous drive needed to maintain the compensatory action. This principle explains why, for example, a patient with chronic [respiratory acidosis](@entry_id:156771) will have a high plasma bicarbonate and an arterial pH that is low but close to normal (e.g., 7.34), but will not be able to "overcorrect" back to or beyond 7.40.

### Comparative and Environmental Perspectives

The fundamental principles of acid-base regulation are conserved across the animal kingdom, but their implementation varies dramatically in response to different metabolic demands and environmental challenges.

#### Ectothermy and the Alphastat Hypothesis

One of the most fascinating comparative topics is acid-base regulation in ectothermic ("cold-blooded") animals, whose body temperature fluctuates with the environment. A key challenge is that the $pK_a$ of many chemical groups is temperature-dependent. The $pK_a$ of the imidazole group of histidine, the dominant non-bicarbonate buffer in intracellular proteins, changes by approximately $-0.017$ units for every $1\,^{\circ}\text{C}$ increase in temperature.

If an ectotherm were to maintain a constant blood pH as its body temperature changed (a "pH-stat" strategy), the changing difference between pH and the imidazole $pK_a$ would cause a significant change in the fractional protonation, and thus the net electrical charge, of its proteins. This would disrupt the function of enzymes, receptors, and [ion channels](@entry_id:144262), with particularly dire consequences for the nervous system.

Instead, most ectotherms employ an **alphastat regulation** strategy [@problem_id:2543586]. The goal of this strategy is to maintain a constant fractional protonation ($\alpha$) of protein imidazole groups. As shown by the [equilibrium equation](@entry_id:749057):
$$ \alpha = \frac{1}{1+10^{\mathrm{pH}-\mathrm{p}K_a}} $$
To keep $\alpha$ constant, the difference $(\mathrm{pH}-\mathrm{p}K_a)$ must be kept constant. This means that the animal must regulate its blood pH to change in parallel with the temperature-dependent changes in the imidazole $pK_a$. As the animal cools down, the imidazole $pK_a$ increases; to maintain alphastat, the animal must increase its blood pH by a corresponding amount. For example, a $20\,^{\circ}\text{C}$ decrease in temperature would cause the imidazole $pK_a$ to rise by about $0.34$ units, and the animal must induce a [respiratory alkalosis](@entry_id:148343) to raise its blood pH by the same amount. This is achieved by adjusting ventilation to lower the systemic $P_{CO_2}$.

By allowing pH to vary in this controlled manner, the animal stabilizes the charge state and conformation of its proteins, thereby preserving critical physiological functions, such as [neuronal excitability](@entry_id:153071), across a wide range of body temperatures. Alphastat regulation is a profound example of how [physiological control systems](@entry_id:151068) are adapted to solve fundamental biophysical problems imposed by the environment.