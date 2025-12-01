## Introduction
In the modern healthcare landscape, control over personal health information is a cornerstone of patient autonomy and engagement. Yet, fundamental questions about who truly "owns" a medical record and what rights a patient has to access or correct it are sources of persistent confusion for patients and providers alike. This ambiguity creates barriers to care, erodes trust, and can lead to significant legal and ethical conflicts. This article addresses this knowledge gap by providing a comprehensive legal and practical guide to a patient's rights regarding their health information.

This article will systematically deconstruct the legal framework that governs medical records. In the first chapter, **Principles and Mechanisms**, we will establish the foundational concepts under US law, defining key terms like the Designated Record Set, untangling the doctrine of ownership, and detailing the specific rights of access and amendment guaranteed by HIPAA. We will also examine the modern prohibition on information blocking. Next, **Applications and Interdisciplinary Connections** will move from theory to practice, exploring how these rights function in real-world scenarios involving billing disputes, court orders, and emerging technologies like AI and patient-facing apps. Finally, **Hands-On Practices** will allow you to apply your understanding to concrete case studies, honing your ability to navigate the procedural complexities of access and correction requests and analyze the consequences of non-compliance.

## Principles and Mechanisms

This chapter delineates the fundamental legal and ethical principles governing a patient's relationship with their own health information. We will deconstruct the core concepts of the medical record, explore the nuanced doctrine of ownership, and systematically analyze the two primary rights afforded to patients under federal law: the right of access and the right to request amendment. Finally, we will examine the modern legal framework designed to promote the free flow of health information by prohibiting practices known as "information blocking."

### Defining the Core Concepts: PHI, the Medical Record, and the Designated Record Set

To understand the rights that attach to health information, one must first master the specific terminology used in the governing legal frameworks, principally the Health Insurance Portability and Accountability Act (HIPAA). These terms are not interchangeable, and their distinctions are critical.

The broadest category is **Protected Health Information (PHI)**. PHI is defined as any individually identifiable health information held or transmitted by a covered entity (such as a health care provider or health plan) or its business associate, in any form or medium, whether electronic, paper, or oral. This expansive definition includes not just clinical data but also demographic information, billing details, and any other data point that could be used to identify an individual in relation to their health status, provision of health care, or payment for health care.

A more familiar term, the **medical record** or clinical chart, represents a subset of PHI. It is the repository of clinical observations, diagnoses, treatment plans, and test results generated during the course of care. However, a patient's rights do not attach to the medical record per se, nor to all of their PHI. Instead, they attach to a specific legal construct known as the **Designated Record Set (DRS)**.

The **Designated Record Set** is the cornerstone for patient rights. It is formally defined as the group of records maintained by or for a covered entity that comprises:
1.  The medical records and billing records about individuals.
2.  Any other records that are used, in whole or in part, by or for the covered entity to make decisions about individuals.

This "used to make decisions" criterion is the key to defining the scope of the DRS. It means that the DRS encompasses a wide array of information beyond the traditional chart. For instance, structured data fields in an electronic health record (EHR) like medication lists and demographic information, unstructured clinician narrative notes like progress notes, and even diagnostic imaging files and their corresponding radiology reports are all unequivocally part of the DRS because they are fundamental to making decisions about a patient's care [@problem_id:4470837].

Conversely, some information that qualifies as PHI may fall outside the DRS. A primary example is system **metadata**, such as the audit logs, access timestamps, and version histories within an EHR. While this data is linked to a patient and is thus PHI, its primary purpose is for security auditing and system administration, not for making clinical or administrative decisions about the individual patient. Consequently, [metadata](@entry_id:275500) is generally not considered part of the DRS, and the patient rights of access and amendment do not typically apply to it [@problem_id:4470837].

### The Doctrine of Ownership: A Bundle of Divided Rights

A common and understandable misconception is that patients "own" their medical records. While this seems intuitive, the legal reality is more complex and is best understood through the property law concept of a **bundle of rights**. Rather than a single entity having absolute ownership, the "bundle" of rights associated with a medical record is split between the provider and the patient.

The healthcare provider or institution owns the **physical or electronic medium** on which the information is stored. The paper chart, the computer server, or the electronic file itself is considered the tangible or intangible property of the provider who created and maintains it. This ownership right gives the provider the right to possess the original record. A provider's refusal to surrender an original paper chart to a patient is therefore a legitimate exercise of its property rights, reinforced by professional duties to ensure continuity of care and legal obligations to retain records for a specified period [@problem_id:4470856].

The patient, in turn, holds a powerful, legally enforceable **informational interest** in the content of the record. This interest is not defined as traditional ownership but is composed of a set of specific rights, including:
-   **The Right to Confidentiality**: The provider's duty of confidentiality severely restricts its ability to use or disclose the patient's PHI. The provider's ownership of the record medium does not grant it the right to monetize or share the identifiable information within it without a proper legal basis, such as patient authorization.
-   **The Right of Access**: As we will explore, patients have a robust statutory right to inspect and obtain a copy of the information in their DRS.
-   **The Right to Request Correction**: Patients also have a statutory right to request that inaccuracies in their DRS be amended.

This division of rights resolves the apparent paradox: the clinic owns the chart, but the patient controls the information. A clinic that licenses identifiable patient data to an analytics firm without consent, for example, is violating the patient's informational interest and the provider's duty of confidentiality, even though it "owns" the record itself [@problem_id:4470856].

### The Right of Access

The HIPAA Privacy Rule establishes a fundamental patient right to access and obtain a copy of their PHI contained within the Designated Record Set. This right is a cornerstone of patient empowerment, enabling individuals to be more informed and engaged in their own healthcare.

#### Scope of Access and Permissible Denials

The right of access is broad, covering medical records, billing records, and any other items in the DRS used for decision-making. However, the right is not absolute. The Privacy Rule enumerates specific grounds upon which a covered entity may deny access. These grounds are strictly defined and are the only permissible reasons for withholding information. Reasons of convenience, such as a provider's preference to review records with the patient first, or coercive reasons, such as withholding records due to an outstanding bill, are impermissible grounds for denial [@problem_id:4470843].

Permissible grounds for denial fall into two categories:

**1. Unreviewable Grounds for Denial:** For certain types of information, a denial is absolute and not subject to a patient's request for review. These include:
-   **Psychotherapy Notes:** These notes receive special protection under HIPAA. They are defined as a clinician's private notes analyzing the content of counseling sessions and, crucially, must be kept separate from the rest of the medical record. The definition explicitly excludes information like medication management, session start/stop times, treatment modalities, and test results, all of which remain part of the general mental health record and are accessible to the patient. The heightened protection for true psychotherapy notes is intended to foster candid therapeutic dialogue [@problem_id:4470852].
-   **Information Compiled for Legal Proceedings:** A patient does not have a right of access to information compiled in reasonable anticipation of, or for use in, a civil, criminal, or administrative action [@problem_id:4470840] [@problem_id:4470843].
-   **Other Specific Exclusions:** Access can also be denied if the PHI was obtained from a non-provider under a promise of confidentiality, or if the patient is an inmate and obtaining the copy would jeopardize health or safety within the correctional facility.

**2. Reviewable Grounds for Denial:** In some cases, a denial is permissible but is subject to the patient's right to have the decision reviewed by another licensed professional. The primary ground for a reviewable denial is a determination by a licensed healthcare professional that granting access is **reasonably likely to endanger the life or physical safety** of the patient or another person [@problem_id:4470843]. A temporary reviewable denial is also permitted for research-related PHI if the patient agreed to a suspension of access for the duration of a clinical trial.

#### Procedural Mechanics of Access

The process for exercising the right of access is clearly defined to be patient-friendly and to minimize barriers.

-   **The Request:** A patient may make a request orally or in writing, though a covered entity may require a written request for documentation purposes. Crucially, a patient's right of access includes the right to direct the covered entity to transmit a copy of the records directly to a third party, such as another physician or an attorney. This requires only a signed, written request from the patient specifying the recipient; it does **not** require a separate, formal HIPAA authorization form [@problem_id:4470840] [@problem_id:4470832].

-   **Verification and Timing:** The entity must take reasonable steps to verify the identity of the requester but cannot create undue barriers. The entity must act on the request within **30 days**. This timeframe may be extended once for an additional 30 days, but only if the entity provides the patient with a written notice explaining the reason for the delay within the initial 30-day period [@problem_id:4470832].

-   **Fees for Access:** A covered entity is permitted to charge a **reasonable, cost-based fee** for providing a copy of the records. This fee may only include the actual costs of:
    -   Labor for the act of copying (but not for searching for or retrieving the records).
    -   Supplies for creating the copy (e.g., a CD, USB drive, or paper).
    -   Postage, if the records are mailed.

    Per-page fees are generally impermissible for electronic copies, as they do not reflect the actual labor cost of producing an electronic file. For example, if a staff member paid \$30 per hour spends 24 minutes (0.4 hours) to prepare and email an electronic record, the maximum allowable labor charge would be $0.4 \times \$30 = \$12$. Charging a retrieval fee or a flat per-page rate would be a violation [@problem_id:4470865]. As an alternative to calculating actual costs, entities can opt to charge a flat fee of no more than \$6.50 for standard electronic requests.

### The Right to Correction: Amending the Record

In addition to accessing their information, patients have the right to request that a covered entity amend PHI that they believe is inaccurate or incomplete. This is not an absolute right to change the record, but a right to a formal review process that ensures the integrity and accuracy of the patient's health information.

#### The Provider's Duty of Accuracy and Grounds for Denial

A provider's duty to maintain accurate records is twofold, and the standard for liability differs accordingly. For **administrative or ministerial data**, such as a patient's contact information or documented allergies, the standard is one of **ordinary negligence**. The provider must have reasonable procedures in place to ensure this data is entered and maintained correctly. In contrast, for entries that reflect **clinical judgment**, such as a diagnosis or a clinician's professional impression, the standard is the **professional standard of care**. A provider is not negligent simply because a patient disagrees with their documented clinical opinion, as long as that opinion was formed consistent with the judgment of a reasonably prudent clinician [@problem_id:4470824].

This distinction is crucial for understanding the amendment process. A provider may deny a request for amendment if they determine that the information in question is, in fact, accurate and complete from their professional perspective. For instance, a hospital may deny a patient's request to change a documented "intolerance" to penicillin to an "[allergy](@entry_id:188097)" if the clinician's judgment was that the original entry was clinically correct. Other grounds for denial include the record not being part of the DRS or not having been created by the provider (unless the originator is no longer available).

#### Procedural Mechanics of Amendment

The procedure for handling an amendment request is grounded in administrative law principles of **reasonableness and procedural due process**, ensuring a fair and transparent process for the patient [@problem_id:4470858].

-   **The Request and Timing:** A provider may require the request to be in writing and to state a reason for the requested change. The provider has **60 days** to act on the request. This period balances the patient's need for a timely response with the provider's need to investigate the claim, which may involve consulting the original clinician. A single 30-day extension is permitted with written notice to the patient explaining the delay [@problem_id:4470832] [@problem_id:4470858].

-   **If the Amendment is Accepted:** The covered entity must make the correction. Critically, this does not mean deleting the original entry. The integrity of the original record must be preserved. The amendment is typically appended to the record or linked to the original entry. The entity must then make reasonable efforts to inform other parties who have received the incorrect information about the amendment.

-   **If the Amendment is Denied:** The denial triggers a series of due process rights for the patient. The provider must issue a **written denial** in plain language that states the basis for the denial. The notice must also inform the patient of their right to:
    1.  Submit a **written statement of disagreement**. The provider must then append this statement to the patient's record and include it with any future disclosures of the disputed information. This ensures the patient's perspective becomes a permanent part of the record, even if the original entry is unchanged.
    2.  Request that the provider include the amendment request and denial with any future disclosures.
    3.  File a formal complaint with the U.S. Department of Health and Human Services (HHS).

    No fee may ever be charged for processing a request for amendment [@problem_id:4470832].

### Modern Imperatives: The Prohibition on Information Blocking

Building upon the foundation of HIPAA, the **21st Century Cures Act** introduced a powerful new legal mandate against **information blocking**. This law makes it illegal for certain entities to engage in practices that are likely to interfere with, prevent, or materially discourage the access, exchange, or use of **Electronic Health Information (EHI)**, unless the practice is required by law or meets a specific regulatory exception.

The rule against information blocking applies to three categories of **actors**:
1.  Health care providers.
2.  Health information networks (HINs) and health information exchanges (HIEs).
3.  Developers of certified health information technology.

**EHI** is defined as the electronic version of the PHI contained in the Designated Record Set, with the same exclusions for psychotherapy notes and information prepared for litigation. The prohibition is broad and covers a wide range of practices, including:
-   **Contractual Interference:** Imposing contract or license terms that unreasonably restrict the sharing of data, such as prohibiting an application from enabling onward sharing with other networks.
-   **Technological Interference:** Designing technology in a way that impedes interoperability, such as refusing to disclose necessary application programming interface (API) documentation or imposing burdensome technical hurdles.
-   **Administrative Interference:** Implementing policies or procedures that create unnecessary delays or burdens, such as a health system's policy to automatically delay the release of most lab results to a patient portal without a specific, case-by-case justification based on preventing harm.
-   **Financial Interference:** Charging unreasonable or discriminatory fees for access to EHI or for the use of interoperability elements.

While the regulation provides for several important exceptions—for example, when a practice is necessary to prevent patient harm, protect patient privacy, or ensure the security of the system—the legal presumption has shifted decisively. The default expectation is now that EHI should flow freely to patients and their designees, and any actor that impedes this flow bears the burden of proving that their practice is legally justified [@problem_id:4470816]. This modern framework represents a significant reinforcement of the principles of access and patient control over their health information in the digital age.