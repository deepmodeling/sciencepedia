## Introduction
Fever is one of the most common reasons infants and children present for medical care, representing both a physiological defense mechanism and a potential sign of life-threatening illness. For clinicians, the central challenge lies in distinguishing the minority of children with serious bacterial infections (SBI) from the vast majority with self-limited viral illnesses. This requires a sophisticated understanding of pathophysiology, a command of evidence-based risk stratification, and the ability to recognize subtle signs of impending clinical deterioration. An incorrect assessment can lead to devastating outcomes from delayed treatment or, conversely, contribute to antibiotic overuse and unnecessary hospitalizations.

This article provides a comprehensive, graduate-level guide to mastering this critical aspect of pediatric care. The following chapters will systematically build your expertise. The first chapter, **Principles and Mechanisms**, will lay the scientific groundwork, deconstructing the febrile response from its molecular origins in the hypothalamus to its clinical manifestations and costs. Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, will translate theory into practice, demonstrating how to apply risk-stratification algorithms, manage specific febrile syndromes like UTIs and MIS-C, and navigate complex scenarios in special populations. Finally, **Hands-On Practices** will provide opportunities to solidify these concepts through practical, case-based problem-solving. We begin by exploring the fundamental principles that govern the febrile response.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern fever in infants and children. We will deconstruct the febrile response, moving from its precise physiological definition and the biophysics of heat generation to the intricate molecular cascade that initiates it. Subsequently, we will analyze fever as a strategic, yet costly, host defense mechanism. Finally, we will translate these foundational principles into the clinical context, exploring how age-dependent risks and the recognition of specific "red flags" guide the evaluation and management of the febrile child.

### Defining and Measuring Fever: A Matter of Precision

A clear understanding of fever begins with its precise definition and the challenges associated with its measurement. It is critical to distinguish the regulated process of fever from the pathological state of hyperthermia, to understand the physical mechanisms the body employs to raise its temperature, and to appreciate the metrological principles that dictate our choice of measurement tools.

#### Fever versus Hyperthermia: A Regulated Response

Fever, or **pyrexia**, is a regulated elevation of the body's core temperature resulting from an increase in the **hypothalamic thermoregulatory [set-point](@entry_id:275797)**. This process is an active, adaptive host response, typically to infection or inflammation. In contrast, **hyperthermia** is an unregulated rise in body temperature that occurs when heat production or environmental heat load overwhelms the body's capacity for heat dissipation. In hyperthermia, the hypothalamic [set-point](@entry_id:275797) remains at its normal level; the body attempts to cool itself but fails.

This distinction is not merely academic; it has profound clinical implications. Consider a 3-month-old infant brought to the emergency department after being bundled in blankets, with an initial axillary temperature of $37.5^\circ\mathrm{C}$ and a subsequent rectal temperature of $38.2^\circ\mathrm{C}$ after a period of unbundled rest [@problem_id:5139866]. The persistence of an elevated core temperature after removing the external heat source (the blankets) argues against simple environmental hyperthermia. The definitive clue, however, lies in the response to an **antipyretic** such as acetaminophen. Antipyretics work by inhibiting the synthesis of prostaglandins in the central nervous system, thereby lowering the elevated hypothalamic [set-point](@entry_id:275797). A decrease in temperature following antipyretic administration, as observed in this infant, is a hallmark of a cytokine-mediated fever. Hyperthermia, being a failure of heat dissipation against a normal set-point, does not respond to antipyretics and must be managed with external cooling.

#### The Biophysics of Temperature Elevation

Once the hypothalamic set-point is elevated, the body perceives its current temperature as being "too cold." To close this gap, it initiates a coordinated set of physiological responses to conserve heat and increase its production. This period is often referred to as the **chill phase** of fever. The governing principle is the [first law of thermodynamics](@entry_id:146485), which states that the rate of change in the body's heat content is the difference between metabolic heat production ($M$) and the rate of heat loss to the environment ($q_{\mathrm{loss}}$).
$$ m c \frac{dT_{\mathrm{core}}}{dt} = M - q_{\mathrm{loss}} $$
where $m$ is body mass, $c$ is the specific heat of the body, and $T_{\mathrm{core}}$ is the core body temperature.

To increase $T_{\mathrm{core}}$, the body must ensure that $M > q_{\mathrm{loss}}$. It accomplishes this through two primary mechanisms [@problem_id:5139888]:
1.  **Heat Conservation via Vasoconstriction:** The sympathetic nervous system triggers intense vasoconstriction in the skin's blood vessels. This shunts warm blood away from the body's surface, reducing skin temperature ($T_s$). According to the laws of heat transfer, both convective heat loss ($q_{\mathrm{conv}} = hA(T_s - T_{\mathrm{env}})$) and radiative heat loss ($q_{\mathrm{rad}} = \epsilon \sigma A(T_s^4 - T_{\mathrm{env}}^4)$) are directly dependent on the skin-to-environment temperature gradient. By lowering $T_s$, the body dramatically reduces heat loss. This is why a child in the chill phase of fever may feel cold and clammy to the touch, despite a rising core temperature.

2.  **Heat Production via Thermogenesis:** The body actively increases its [metabolic rate](@entry_id:140565) to generate more heat. The primary mechanism for rapid heat production is **shivering**, which involves involuntary, high-frequency [skeletal muscle](@entry_id:147955) contractions. The ATP hydrolysis that powers these contractions is biochemically inefficient in terms of producing external work, so the vast majority of the chemical energy is degraded into heat. In infants, **[non-shivering thermogenesis](@entry_id:150796)** in [brown adipose tissue](@entry_id:155869) (BAT) also plays a significant role.

For a hypothetical $10$-kg infant, the combined effect of lowering skin temperature from $35^\circ\mathrm{C}$ to $31^\circ\mathrm{C}$ and shivering increasing metabolic power from $40\ \mathrm{W}$ to $100\ \mathrm{W}$ can shift the body's net energy balance from a net loss to a net gain of approximately $40\ \mathrm{W}$. This positive heat storage results in a predictable rise in core temperature, on the order of $0.7^\circ\mathrm{C}$ over $10$ minutes, driving the body toward its new, higher febrile [set-point](@entry_id:275797) [@problem_id:5139888].

#### Thermometry: The Challenge of Accurate Measurement

Clinically, the diagnosis of fever hinges on an accurate temperature measurement. In young infants, **rectal [thermometry](@entry_id:151514)** is considered the gold standard, with fever typically defined as a rectal temperature $\ge 38.0^\circ\mathrm{C}$. The justification for this preference can be rigorously formalized using the principles of [measurement theory](@entry_id:153616) and statistical decision analysis [@problem_id:5139925].

Any measurement ($M$) of a true value ($T$) can be modeled as having a systematic error, or **bias** ($b$), and a random error, or **imprecision** (characterized by its standard deviation, $\sigma$).
$$ M = T + b + \epsilon $$
Rectal temperature provides the closest, most stable approximation of core body temperature, exhibiting near-zero bias ($b_r \approx 0.0^\circ\mathrm{C}$) and high precision (low imprecision, $\sigma_r \approx 0.2^\circ\mathrm{C}$).

In contrast, peripheral methods are less reliable. **Axillary (armpit) [thermometry](@entry_id:151514)** measures skin temperature and is known to have a significant negative bias ($b_a \approx -0.5^\circ\mathrm{C}$) and poor precision ($\sigma_a \approx 0.5^\circ\mathrm{C}$). **Tympanic (ear) [thermometry](@entry_id:151514)**, while theoretically measuring infrared radiation from the tympanic membrane (which shares a blood supply with the hypothalamus), is highly operator-dependent and prone to error from improper technique or obstruction by cerumen (earwax), resulting in a negative bias ($b_t \approx -0.2^\circ\mathrm{C}$) and moderate imprecision ($\sigma_t \approx 0.4^\circ\mathrm{C}$) [@problem_id:5139866] [@problem_id:5139925].

In the context of evaluating a febrile infant under 3 months of age, the clinical stakes are exceptionally high. The consequence of a **false-negative** result (missing a true fever, $M  38.0^\circ\mathrm{C}$ when $T \ge 38.0^\circ\mathrm{C}$) is the potential to miss a life-threatening Serious Bacterial Infection (SBI), a harm we can quantify as a large loss, $L_{\mathrm{FN}}$. The consequence of a **false-positive** result is an unnecessary and costly workup, a smaller loss, $L_{\mathrm{FP}}$. Given that $L_{\mathrm{FN}} \gg L_{\mathrm{FP}}$, the primary goal of our measurement strategy must be to minimize the probability of a false negative.

The negative bias and high imprecision of axillary and tympanic methods dramatically increase the false-negative rate. For an infant with a true temperature of $38.5^\circ\mathrm{C}$, the axillary method could have up to a $50\%$ chance of yielding a measurement below the $38.0^\circ\mathrm{C}$ threshold. The rectal method, with its minimal bias and high precision, reduces this probability to less than $1\%$. Therefore, the preference for rectal [thermometry](@entry_id:151514) is not arbitrary; it is a direct consequence of a risk-management strategy that prioritizes the avoidance of catastrophic false negatives in a high-risk population [@problem_id:5139925].

### The Molecular and Cellular Basis of Fever

The elevation of the hypothalamic [set-point](@entry_id:275797) is the culmination of a sophisticated signaling cascade that translates the presence of a pathogen into a specific neurochemical change. This pathway is a cornerstone of our understanding of fever.

#### The Febrile Cascade: From Pathogen to Prostaglandin

The febrile response is initiated by molecules known as **pyrogens**. **Exogenous pyrogens** are microbial products that originate outside the host. In the case of a Gram-negative bacterial infection, such as urosepsis from *E. coli*, the most potent exogenous pyrogen is **[lipopolysaccharide](@entry_id:188695) (LPS)**, a component of the bacterial outer membrane [@problem_id:5139871].

The pathway unfolds in a series of steps:
1.  **Recognition:** LPS in the bloodstream is recognized by **pattern-recognition receptors** on host immune cells (e.g., monocytes, macrophages) and endothelial cells. The primary receptor for LPS is **Toll-like receptor 4 (TLR4)**.

2.  **Cytokine Release:** Activation of TLR4 triggers intracellular signaling cascades (e.g., via NF-$\kappa$B), leading to the synthesis and release of **endogenous pyrogens**. These are the host's own signaling molecules, primarily the pro-inflammatory cytokines **interleukin-1$\beta$ (IL-1$\beta$)**, **interleukin-6 (IL-6)**, and **tumor necrosis factor-$\alpha$ (TNF-$\alpha$)**.

3.  **CNS Signaling:** These circulating cytokines must transmit their signal to the brain. They do so primarily by acting on the vascular endothelium at specific sites called **circumventricular organs (CVOs)**, where the blood-brain barrier is "leaky." The most critical CVO for fever induction is the **organum vasculosum of the lamina terminalis (OVLT)**.

4.  **Prostaglandin Synthesis:** At the OVLT, IL-1$\beta$ and IL-6 bind to their receptors on endothelial and perivascular cells. This binding upregulates the expression of two key enzymes: **cyclooxygenase-2 (COX-2)** and **microsomal prostaglandin E synthase-1 (mPGES-1)**. These enzymes work in sequence to convert arachidonic acid into the final, critical mediator: **prostaglandin E$_2$ (PGE$_2$)**.

#### Resetting the Thermostat: PGE$_2$ Action in the Hypothalamus

The newly synthesized PGE$_2$ is the key that turns the thermostat up. It diffuses a short distance from the OVLT into the adjacent **preoptic area (POA)** of the hypothalamus, the brain's primary thermoregulatory control center [@problem_id:5139871].

Within the POA, PGE$_2$ binds predominantly to the **prostaglandin E receptor subtype 3 (EP3)**. These receptors are located on a specific population of **warm-sensitive neurons**. These neurons are GABAergic (inhibitory) and, when active, promote heat-loss mechanisms (like vasodilation and sweating) and inhibit heat-production pathways. The EP3 receptor is G$_i$-protein coupled, meaning its activation *inhibits* the neuron.

Therefore, the binding of PGE$_2$ to EP3 receptors suppresses the firing of these warm-sensitive neurons. This suppression removes their [tonic inhibition](@entry_id:193210) of downstream heat-promoting centers. This "disinhibition" of heat conservation and heat production pathways is the cellular mechanism that effectively raises the thermoregulatory set-point. With the set-point now elevated, the body initiates the physiological responses of vasoconstriction and shivering described earlier, driving the core temperature upward until it matches the new febrile [set-point](@entry_id:275797).

### Fever as a Double-Edged Sword: Risks and Benefits

Fever is not merely a symptom; it is an evolutionarily conserved, complex adaptive response. However, this defense strategy is not without significant physiological costs. Understanding the trade-offs between the benefits and risks of fever is essential for rational clinical management.

#### The Adaptive Value of Fever

The febrile response confers several advantages to the host in its fight against infection [@problem_id:5139921].
-   **Direct Antimicrobial Effects:** The replication rates of many pathogens are temperature-sensitive. While some thermotolerant bacteria may grow well at febrile temperatures, many viruses, particularly respiratory viruses like rhinovirus, have optimal replication temperatures in the cooler range of the upper airways ($33-35^\circ\mathrm{C}$). Elevating the core body temperature to $39-40^\circ\mathrm{C}$ can directly inhibit their replication.

-   **Enhanced Immune Function:** Moderate hyperthermia has been shown to potentiate multiple arms of the immune system. It can enhance the motility, [chemotaxis](@entry_id:149822), and phagocytic activity of neutrophils. It also improves the trafficking of lymphocytes to sites of infection and increases the efficacy of [interferons](@entry_id:164293), key antiviral proteins.

#### The Physiological Cost of Fever

The benefits of fever are paid for with a substantial increase in the body's metabolic expenditure, which carries inherent risks, particularly for vulnerable children [@problem_id:5139921].
-   **Increased Metabolic Demand:** The rate of most biochemical reactions increases with temperature, a relationship often described by the **[temperature coefficient](@entry_id:262493), $Q_{10}$**, which is the factor by which a rate increases for a $10^\circ\mathrm{C}$ rise in temperature. For whole-body metabolism in humans, $Q_{10}$ is approximately $2-3$. Using a conservative $Q_{10}$ of $2$, a fever of $39^\circ\mathrm{C}$ (a $2^\circ\mathrm{C}$ rise from a baseline of $37^\circ\mathrm{C}$) increases the [basal metabolic rate](@entry_id:154634) by a factor of $2^{(2/10)} \approx 1.15$. This represents a nearly **15% increase in basal energy expenditure and oxygen consumption**. For a healthy child, this is typically manageable. However, for a child with compromised cardiac or pulmonary function, this added metabolic stress can precipitate cardiorespiratory distress.

-   **Increased Dehydration Risk:** Fever significantly increases insensible water loss. This loss, which occurs through evaporation from the skin and respiratory tract, increases by approximately **10% for each degree Celsius** the core temperature rises above $37^\circ\mathrm{C}$. A fever of $39^\circ\mathrm{C}$ thus increases these losses by about $20\%$. Infants are particularly vulnerable to this effect due to their higher surface-area-to-[mass ratio](@entry_id:167674), which results in a greater baseline insensible water loss per kilogram of body weight. In a febrile infant with decreased oral intake, this accelerated fluid loss can rapidly lead to clinically significant dehydration.

The decision to treat fever with antipyretics, therefore, is not about "curing" the illness but about managing these costs. In a child who is uncomfortable, has poor oral intake due to malaise, or has underlying cardiopulmonary disease, reducing fever can decrease metabolic demand and fluid loss, improve comfort, and thereby provide significant benefit.

### Clinical Context: Age, Risk, and Recognition of Severe Illness

While the fundamental mechanisms of fever are universal, their clinical interpretation is profoundly influenced by the patient's age and clinical state. The evaluation of a febrile child is a process of risk stratification, aimed at identifying the small subset of children with life-threatening infections who require immediate intervention.

#### The Vulnerable Neonate: An Immunological Perspective

Neonates ($0-28$ days of age) and young infants represent the highest-risk group among febrile children. Their marked vulnerability to invasive bacterial infection (IBI) is not a single deficit but a confluence of factors spanning barrier function, pathogen exposure, and profound immune immaturity [@problem_id:5139839].

-   **Immune Immaturity:** The neonatal immune system is functionally hyporesponsive.
    -   **Innate Immunity:** They have a smaller storage pool of neutrophils, and these cells exhibit impaired [chemotaxis](@entry_id:149822) and bactericidal activity. Levels of complement proteins, critical for opsonizing bacteria for [phagocytosis](@entry_id:143316), are significantly reduced.
    -   **Adaptive Immunity:** The adaptive system is naive. There is a physiological bias towards T-helper 2 ($T_H2$) responses, with diminished T-helper 1 ($T_H1$) activity (characterized by IFN-$\gamma$), which is crucial for clearing [intracellular pathogens](@entry_id:198695). The ability to produce their own antibodies is limited, with low levels of IgM upon first encounter with a pathogen.
    -   **Passive Immunity:** The neonate depends almost entirely on **maternal IgG** antibodies transferred across the placenta. This provides protection against pathogens the mother has previously encountered but is a finite resource that wanes over months. Crucially, **secretory IgA**, the primary antibody protecting mucosal surfaces, is not transferred placentally and must be acquired through breast milk, leaving the gut and respiratory tract of many neonates vulnerable.

-   **Barrier Dysfunction:** The physical barriers of the neonate are underdeveloped. The skin's stratum corneum is thinner. The gastrointestinal mucosa is more permeable ("[leaky gut](@entry_id:153374)"), facilitating bacterial translocation into the bloodstream. The blood-brain barrier is more susceptible to inflammatory disruption, increasing the risk of meningitis during bacteremia.

-   **Pathogen Exposure and Microbiome:** During birth, the neonate is exposed to and colonized by maternal flora. This can include highly virulent pathogens such as **Group B *Streptococcus* (GBS)** and specific strains of ***Escherichia coli***. This occurs at a time when the infant's own protective microbiome is not yet established.

#### Age-Specific Pathogens and Evaluation Strategies

This unique neonatal vulnerability dictates an aggressive and standardized approach to evaluation. As infants mature, their immune systems develop and pathogen epidemiology shifts, allowing for more nuanced, risk-stratified approaches [@problem_id:5139900].

-   **Age 0–28 Days:** Due to the high risk of IBI and the specific pathogen profile (**GBS, *E. coli*, *Listeria monocytogenes***), any neonate with a documented fever requires a full evaluation for sepsis. This includes blood culture, urinalysis and urine culture (obtained by a sterile method like catheterization), and a **lumbar puncture (LP)** for cerebrospinal fluid (CSF) analysis. All such infants are admitted to the hospital for parenteral antibiotics. Empiric therapy must cover the likely pathogens, typically with **ampicillin** (for *Listeria*) plus an aminoglycoside like **gentamicin** or a third-generation cephalosporin like **cefotaxime**. Note: *ceftriaxone is avoided in neonates due to risks of hyperbilirubinemia and calcium [precipitation](@entry_id:144409).*

-   **Age 29–60 Days:** The risk of IBI remains significant, but the epidemiology begins to shift. Urinary tract infections (UTIs), predominantly from *E. coli*, become the most common SBI. The incidence of *Listeria* decreases substantially. Evaluation still includes blood and urine studies, but the decision to perform an LP can be guided by the infant's clinical appearance and inflammatory markers (e.g., CRP, procalcitonin). Well-appearing infants who meet strict low-risk criteria may be managed as outpatients, while those requiring admission are often treated with a third-generation cephalosporin like **ceftriaxone**.

-   **Age 61–90 Days:** The pathogen profile and risk of IBI begin to resemble those of older infants. UTIs remain the most common SBI. Evaluation is further risk-stratified, focusing heavily on screening for UTI. LPs are reserved for infants who appear ill or have specific signs of CNS involvement.

#### Recognizing Sepsis: Beyond Fever and Tachycardia

The ultimate goal of risk stratification is to identify children with **sepsis**, now defined as life-threatening organ dysfunction caused by a dysregulated host response to infection. A critical concept in pediatrics is that children, unlike adults, can maintain a normal blood pressure for a prolonged period during shock by mounting an intense compensatory vasoconstrictive response. This state is known as **compensated shock**. Waiting for hypotension to diagnose shock in a child is a dangerous delay; hypotension is a late sign of decompensation and impending cardiovascular collapse.

Therefore, an effective bedside screen for pediatric sepsis must detect the clinical signs of organ dysfunction that manifest during compensated shock [@problem_id:5139844]. Three domains are key:
1.  **Perfusion:** Signs of intense vasoconstriction are windows into circulatory dysfunction. These include cool or mottled extremities, a **prolonged capillary refill time (CRT)** (typically $2$ seconds), and weak peripheral pulses compared to central pulses.
2.  **Mental Status:** The brain is highly sensitive to inadequate oxygen delivery. Any new alteration in mental status from baseline—from irritability to lethargy or unresponsiveness—is a sign of CNS dysfunction.
3.  **Lactate:** An elevated serum lactate level (e.g., $\ge 2.0 \ \mathrm{mmol/L}$) is a direct biochemical marker of [anaerobic metabolism](@entry_id:165313), indicating that cellular oxygen delivery is failing to meet demand.

In a child with a suspected infection, the presence of **at least one** of these abnormalities—abnormal perfusion, altered mental status, or elevated lactate—should be considered a major red flag that triggers immediate resuscitation, even if blood pressure is normal.

#### Quantifying Risk: The Predictive Value of Red Flags

Certain clinical signs, or "red flags," carry a particularly high predictive value for IBI. The power of these signs can be quantified using principles of evidence-based medicine, such as the **likelihood ratio (LR)**, which describes how much a test result changes the odds of having a disease [@problem_id:5139876].

-   **Toxic Appearance:** This clinical gestalt refers to a child with signs of severe systemic illness: lethargy, poor perfusion, and altered responsiveness. It carries a significant positive [likelihood ratio](@entry_id:170863) ($\mathrm{LR}^+ \approx 5$) for IBI.
-   **Hypoxia:** An oxygen saturation $90-92\%$ on room air indicates severe ventilation-perfusion mismatch or shunt, a sign of severe respiratory or circulatory compromise with a high $\mathrm{LR}^+$.
-   **Prolonged Capillary Refill:** A CRT $3$ seconds is a direct sign of poor microcirculatory flow from shock and has an $\mathrm{LR}^+ \approx 3$ for IBI.
-   **Petechial Rash:** A non-blanching petechial or purpuric rash in a febrile child is a particularly ominous sign. It results from endothelial injury, platelet consumption, and disseminated intravascular coagulation (DIC), often driven by [endotoxins](@entry_id:169231) from bacteria like ***Neisseria meningitidis*** (meningococcus). It carries a very high likelihood ratio ($\mathrm{LR}^+ \approx 12$) for meningococcemia or other IBI.

The presence of multiple red flags multiplies their diagnostic power. For an infant with a baseline IBI risk of $5\%$, the simultaneous presence of a toxic appearance, hypoxia, prolonged CRT, and a petechial rash can increase the post-test probability of IBI to over $95\%$. This confirms the need for immediate, aggressive resuscitation and empiric antibiotic therapy.

#### The Role of Biomarkers: CRP vs. Procalcitonin

Inflammatory biomarkers can aid in risk stratification, though they must always be interpreted in the full clinical context. The two most common are C-reactive protein (CRP) and procalcitonin (PCT) [@problem_id:5139845].

-   **C-Reactive Protein (CRP):** A non-specific acute-phase reactant synthesized by the liver in response to IL-6. It rises in a wide range of inflammatory conditions, including bacterial, viral, and [autoimmune diseases](@entry_id:145300). Its synthesis is relatively slow, beginning $4-6$ hours after a stimulus and peaking at $36-50$ hours. This slow kinetic profile means an early CRP can be falsely reassuring.

-   **Procalcitonin (PCT):** A peptide precursor of calcitonin. In severe bacterial infections, its gene is induced throughout the body, leading to a rapid rise in serum levels. Importantly, its production is strongly suppressed by **[interferon-gamma](@entry_id:203536) (IFN-$\gamma$)**, a cytokine produced during viral infections. This differential regulation makes PCT a more specific marker for bacterial infection. Its kinetics are also faster than CRP, rising within $2-4$ hours and peaking at $12-24$ hours.

This distinct biology leads to differential utility:
-   **Early Discrimination:** In the first hours of a fever, PCT is superior to CRP for distinguishing a likely bacterial versus viral etiology due to its faster kinetics and higher specificity.
-   **Guiding Antibiotic Use:** In classic viral syndromes like bronchiolitis, a low PCT level has a high negative predictive value for concurrent bacterial infection and can support a decision to withhold antibiotics more reliably than a low CRP.
-   **Specific Syndromes:** In sterile hyperinflammatory states like Multisystem Inflammatory Syndrome in Children (MIS-C), CRP is often massively elevated, reflecting the overall inflammatory burden, while PCT is often only modestly elevated. This discrepancy can be a clue that the underlying process is not an active bacterial infection.