## Introduction
The survival and well-being of mothers and their newborns is a cornerstone of global public health and a fundamental indicator of a society's health and equity. Despite significant progress, millions of preventable deaths still occur each year around the time of childbirth, representing a profound loss for families, communities, and nations. Addressing this challenge requires moving beyond isolated interventions to a structured, evidence-based approach that tackles the problem from its biological roots to its complex systems-level determinants.

This article provides a comprehensive framework for understanding and acting upon the challenges of maternal and newborn survival. Across three chapters, you will gain the knowledge and tools to analyze this [critical field](@entry_id:143575). In "Principles and Mechanisms," you will learn the foundational language of maternal and newborn health, mastering the key metrics, clinical conditions, and conceptual models used to define and measure the problem. Following this, "Applications and Interdisciplinary Connections" will demonstrate how these principles are put into practice, using analytical tools from epidemiology, economics, and [operations research](@entry_id:145535) to plan and evaluate life-saving programs. Finally, "Hands-On Practices" will give you the opportunity to apply your knowledge to solve realistic quantitative problems. We begin by establishing the bedrock of all [effective action](@entry_id:145780): a rigorous and standardized framework for measurement.

## Principles and Mechanisms

### Foundational Concepts and Measurement

To address the challenges of maternal and newborn survival, we must begin with a rigorous and standardized measurement framework. Understanding how key events are defined, measured, and compared is the bedrock upon which effective policies and interventions are built. This section delineates the core indicators of mortality and morbidity, introduces the principal clinical conditions that drive these outcomes, and presents a comprehensive metric for quantifying the total burden of disease.

#### Defining Mortality and Morbidity

The quantitative analysis of maternal and newborn health relies on several key indicators, each with a precise definition designed to answer a specific epidemiological question. A critical distinction often lies in the choice of the denominator, which determines the nature of the risk being measured.

A primary indicator is the **Maternal Mortality Ratio (MMR)**, which is the number of maternal deaths during a given time period per $100{,}000$ live births during the same period. A maternal death is defined by the World Health Organization (WHO) as the death of a woman while pregnant or within $42$ days of termination of pregnancy, from any cause related to or aggravated by the pregnancy or its management, but not from accidental or incidental causes. The MMR formula is:

$$ \text{MMR} = \frac{\text{Number of maternal deaths}}{\text{Number of live births}} \times 100{,}000 $$

The MMR is technically a ratio, not a rate, as the numerator includes women who may not be in the denominator (e.g., a woman who dies from an [ectopic pregnancy](@entry_id:271723) or a septic abortion has not had a live birth). However, live births are used as a readily available proxy for the total number of pregnancies. The MMR therefore primarily reflects the **obstetric risk**: the risk of death for a woman once she has become pregnant.

This is distinct from the **Maternal Mortality Rate (MMRate)**. The MMRate measures the risk of maternal death among the general population of women of reproductive age. Its denominator is the total person-time of exposure for women of reproductive age (typically defined as ages $15$–$49$) over a given period.

$$ \text{MMRate} = \frac{\text{Number of maternal deaths}}{\text{Total woman-years of exposure (ages 15-49)}} \times 100{,}000 $$

The MMRate thus reflects the combined effect of both the obstetric risk (MMR) and the underlying fertility rate in the population. Two countries could have the same obstetric risk (identical MMRs), but the country with a higher fertility rate will have a higher MMRate because its female population experiences the risk of pregnancy more frequently [@problem_id:4989823].

Similar precision is required when measuring mortality around the time of birth. The **perinatal period** commences at $22$ completed weeks of gestation and ends seven completed days after birth. Mortality in this period is captured by several key indicators. A **stillbirth** is a baby born with no signs of life at or after a specified threshold of viability. An **early neonatal death** is the death of a live-born infant within the first seven days of life.

The **Stillbirth Rate (SBR)** and the **Perinatal Mortality Rate (PMR)** are crucial measures, typically expressed per $1{,}000$ total births.
$$ \text{SBR} = \frac{\text{Number of stillbirths}}{\text{Total births (live births + stillbirths)}} \times 1000 $$
$$ \text{PMR} = \frac{\text{Number of stillbirths} + \text{Number of early neonatal deaths}}{\text{Total births (live births + stillbirths)}} \times 1000 $$

A significant challenge in global health is the international comparability of these rates. Different health systems may use different thresholds for registering births and deaths, for example, a gestational age of at least $22$ weeks versus at least $28$ weeks. Because mortality risk is much higher at lower gestational ages, a country using a more inclusive (e.g., $\ge 22$ weeks) threshold will naturally report higher SBR and PMR than a country using a more restrictive (e.g., $\ge 28$ weeks) threshold, even if the quality of care is identical. Meaningful comparison therefore requires standardizing rates to a common threshold, such as the WHO recommendation for international comparison of at least $28$ completed weeks of gestation or a birthweight of at least $1000 \, \mathrm{g}$. This often requires disaggregated data or statistical modeling to adjust for differences in registration practices [@problem_id:4989828].

#### Defining Major Clinical Conditions

Underpinning these mortality statistics are specific clinical conditions. Understanding their pathophysiology is essential for designing effective interventions.

**Postpartum Hemorrhage (PPH)** is the leading direct cause of maternal mortality worldwide. **Primary PPH** is defined as cumulative blood loss of at least $500 \, \mathrm{mL}$ within the first $24$ hours after childbirth. The physiological mechanisms of PPH are classically categorized by the "Four T's":

*   **Tone (Uterine Atony):** This is the most common cause, accounting for over $70\%$ of cases. After delivery of the placenta, the myometrium (uterine muscle) must contract forcefully to constrict the spiral arteries that supplied the placental bed. Failure of the uterus to contract—uterine atony—leaves these vessels open, leading to rapid and voluminous blood loss.
*   **Tissue (Retained Placental Tissue):** If fragments of the placenta or membranes are retained in the uterus, they can physically prevent the uterus from contracting effectively and can promote localized [fibrinolysis](@entry_id:156528), impeding clot formation at the placental site.
*   **Trauma (Genital Tract Trauma):** Lacerations to the cervix, vagina, or perineum sustained during childbirth can damage blood vessels, causing bleeding that is independent of uterine contraction.
*   **Thrombin (Coagulopathy):** Pre-existing or acquired disorders of [blood clotting](@entry_id:149972) can impair the body's ability to form a stable clot, leading to persistent oozing from the placental site or any trauma. [@problem_id:4989795]

**Preterm birth**, defined by the WHO as any birth before $37$ completed weeks of gestation, is the leading cause of neonatal mortality. It is not a single entity but a syndrome with multiple etiologies, broadly categorized into two pathways:

*   **Spontaneous Preterm Birth:** This pathway includes spontaneous preterm labor (the presence of regular uterine contractions and cervical change) and preterm prelabor rupture of membranes (PPROM). It accounts for roughly two-thirds of preterm births. Prevention strategies target modifiable risk factors (e.g., infections, smoking) and underlying biological mechanisms (e.g., prophylactic progesterone for women with a short cervix). Management of an acute episode may involve short-term use of **tocolytics** (drugs to suppress contractions) to allow for the administration of antenatal corticosteroids to mature the fetal lungs.
*   **Medically Indicated Preterm Birth:** This pathway involves a clinical decision to deliver the baby prematurely due to maternal or fetal conditions where continuing the pregnancy poses a greater risk than a preterm delivery. Common indications include severe preeclampsia, placental abruption, or fetal growth restriction with signs of compromise. Here, prevention focuses on managing the underlying disease. Tocolytics are contraindicated, as the goal is not to stop labor but to achieve a safe, planned delivery. [@problem_id:4989832]

This distinction is critical because the management strategies are diametrically opposed: one aims to delay delivery, while the other aims to expedite it.

#### Measuring the Burden of Disease

Mortality rates, while essential, only capture part of the story. Many maternal and newborn conditions lead to long-term disability. A comprehensive metric that combines both premature mortality and non-fatal health loss is the **Disability-Adjusted Life Year (DALY)**. The DALY represents the total years of healthy life lost and is calculated as the sum of two components:

$$ \text{DALY} = \text{YLL} + \text{YLD} $$

**Years of Life Lost (YLL)** are due to premature mortality. They are calculated by multiplying the number of deaths ($N$) by a standard life expectancy ($L$) at the age of death. For a neonatal death, where a newborn dies shortly after birth, the life expectancy used is that of a healthy infant, which can be as high as $80$ or more years in a standard [life table](@entry_id:139699).
$$ \text{YLL} = N \times L $$

**Years Lived with Disability (YLD)** are due to non-fatal health conditions. They are calculated by multiplying the number of incident cases ($I$) by the duration of the disease ($D$) and a **disability weight (DW)**. The disability weight is a value between $0$ (perfect health) and $1$ (equivalent to death) that reflects the severity of the health state. For example, moderate neonatal complications might have a $DW$ of $0.2$, while severe, long-term neurodevelopmental impairment could have a $DW$ of $0.6$.
$$ \text{YLD} = I \times D \times \text{DW} $$

Early methodologies for calculating DALYs included **age-weighting** (valuing years lived in young adulthood more highly than those in infancy or old age) and **[discounting](@entry_id:139170)** (valuing future years of health less than present years). However, modern approaches, such as those used in the Global Burden of Disease study, have largely abandoned these practices for ethical reasons. Applying age-weighting or discounting systematically devalues the lives of newborns by either assigning a lower [intrinsic value](@entry_id:203433) to their early life-years or by diminishing the value of the long future they have lost. The current standard of no age-weighting and no discounting ensures that a year of healthy life lost is counted equally for everyone, regardless of their age or when the loss occurs, reflecting a core principle of health equity [@problem_id:4989874].

### Frameworks for Action and Quality

With a clear understanding of the key problems and how to measure them, we can turn to frameworks for organizing a response. These include global policy targets that set the agenda, health system designs that structure service delivery, and quality of care models that guide measurement and improvement.

#### Global Policy and Targets

The international community's commitment to maternal and newborn survival is principally articulated through the **Sustainable Development Goals (SDGs)** for the period $2015-2030$. Under Goal 3, "Ensure healthy lives and promote well-being for all at all ages," two specific targets address this agenda:

*   **SDG Target 3.1:** By $2030$, reduce the global maternal mortality ratio (MMR) to less than $70$ per $100{,}000$ live births.
*   **SDG Target 3.2:** By $2030$, end preventable deaths of newborns and children under $5$ years of age, with all countries aiming to reduce the **Neonatal Mortality Rate (NMR)** to at least as low as $12$ per $1{,}000$ live births and the **Under-5 Mortality Rate (U5MR)** to at least as low as $25$ per $1{,}000$ live births.

These targets represent a shift from the relative reduction goals of the preceding Millennium Development Goals (MDGs) to absolute, universal thresholds. They are core components of the "Survive" pillar of the **Global Strategy for Women’s, Children’s and Adolescents’ Health (2016–2030)**, which aims to end preventable mortality. Progress is tracked through dedicated measurement frameworks like the **Ending Preventable Maternal Mortality (EPMM)** and **Every Newborn Action Plan (ENAP)** initiatives [@problem_id:4989836].

#### Health Systems Design for Survival

Achieving these ambitious targets requires a health system capable of delivering timely and effective care. Two conceptual frameworks are central to designing such a system: the continuum of care and the provision of emergency care.

The **continuum of care** is a systems-thinking framework that links health services for the mother-newborn dyad across two dimensions: time and place. The time dimension connects care from the preconception period, through pregnancy (antenatal care), childbirth (intrapartum care), and the crucial weeks after birth (postnatal care). The place dimension connects care delivered at different levels, from the household and community to primary care clinics and referral hospitals. This integrated approach recognizes that health outcomes are the result of a chain of events, where survival at each stage is conditional on having survived the previous ones. Interventions in one part of the continuum can have synergistic, positive feedback effects on others. For instance, high-quality antenatal care not only improves health during pregnancy but also increases the likelihood of a woman seeking skilled care for childbirth, which in turn improves the effectiveness of both intrapartum and immediate postnatal interventions. An integrated strategy that strengthens multiple points in the continuum and their linkages often yields far greater survival gains than a "vertical" strategy that focuses intensely on only one stage [@problem_id:4989885].

To respond to the life-threatening complications that cause the vast majority of maternal and newborn deaths, health systems must be equipped to provide **Emergency Obstetric and Newborn Care (EmONC)**. This care is organized into two levels, defined by a set of critical, life-saving "signal functions":

**Basic Emergency Obstetric and Newborn Care (BEmONC)** consists of seven signal functions that should be available at primary care facilities:
1.  Administer parenteral antibiotics (for sepsis).
2.  Administer parenteral uterotonic drugs (for PPH).
3.  Administer parenteral anticonvulsants (magnesium sulfate for eclampsia).
4.  Perform manual removal of the placenta (for PPH).
5.  Perform removal of retained products of conception (for bleeding/sepsis).
6.  Perform assisted vaginal delivery (e.g., vacuum extraction for obstructed labor).
7.  Perform basic neonatal resuscitation (bag-and-mask ventilation for birth asphyxia).

**Comprehensive Emergency Obstetric and Newborn Care (CEmONC)** includes all seven BEmONC functions plus two additional signal functions that require surgical and laboratory capacity, typically available only at referral hospitals:
8.  Perform caesarean section (for obstructed labor, etc.).
9.  Provide blood transfusion (for severe hemorrhage).

This nine-function framework provides a clear, measurable standard for health system capability. It directly links the system's capacity to the primary causes of maternal and newborn death, ensuring that facilities are equipped to perform the specific actions needed to save lives [@problem_id:4989826].

#### Conceptualizing and Measuring Quality of Care

The availability of services is not enough; the quality of those services is paramount. The **Donabedian framework**, proposed by Avedis Donabedian, is a powerful model for conceptualizing and measuring quality of care by dividing it into three interconnected domains:

*   **Structure:** The context in which care is delivered. This includes the attributes of the care setting, such as physical infrastructure, the availability of equipment and supplies (e.g., functional resuscitation equipment, stock of [oxytocin](@entry_id:152986)), and human resources (e.g., presence of skilled birth attendants). Structural measures assess the system's readiness to provide high-quality care.
*   **Process:** The content of care—what is actually done in giving and receiving it. This domain measures the actions of health providers and patients, such as the proportion of deliveries monitored with a partograph, the timeliness of emergency interventions (e.g., decision-to-incision time for a caesarean section), or the proportion of women receiving recommended preventive care.
*   **Outcome:** The effects of care on the health status of patients and populations. This includes measures of mortality (e.g., neonatal mortality rate) and morbidity (e.g., incidence of postpartum hemorrhage).

This framework provides a logical causal chain: good Structure increases the likelihood of good Process, which in turn increases the likelihood of good Outcomes [@problem_id:4989845].

In recent years, the understanding of "process quality" has expanded beyond technical proficiency to include the patient's experience of care. **Respectful Maternity Care (RMC)** has emerged as a critical, rights-based component of quality. It encompasses a woman's right to dignity, privacy, informed consent, freedom from mistreatment, and supportive care. RMC is not merely a matter of "courtesy"; it is a fundamental aspect of person-centered care. Evidence demonstrates that a woman's experience of care has profound instrumental value. Positive, respectful care builds trust and encourages future service utilization, such as returning for postnatal care or choosing a facility birth for a subsequent pregnancy. Conversely, disrespectful and abusive care is a powerful deterrent to seeking care. Moreover, the quality of communication and support inherent in RMC can directly improve health outcomes, for instance by facilitating early breastfeeding or reducing maternal stress. Statistical evidence shows that RMC is associated with improved utilization and better neonatal outcomes, even after accounting for the technical quality of clinical care. Therefore, RMC must be considered an essential and measurable domain of quality, justified both on normative human rights grounds and on its instrumental role in improving maternal and newborn survival [@problem_id:4989794].