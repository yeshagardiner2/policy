---
title: Risk Analysis
---

## Purpose

This document outlines the process and contents of a holistic risk analysis focusing on risk to Welkin's information systems with a particular focus on the confidentiality, integrity, and availability of ePHI.

## Scope

This policy covers the whole of Welkin Health's services and operations.

## Summary

The purpose of this document is to provide a process for understanding risks to Welkin's information systems with a particular focus on the confidentiality, integrity, and availability of ePHI. Welkin has reviewed many sources, both external (e.g. NIST guidelines) and internal (e.g. system architecture documentation), to generate the list of threats that this document contemplates.

Our classification process and risk assessment thresholds are explained in full in the sections below. The risks that met our threshold for more detailed mitigation analysis are as follows. Detailed analysis of current and future mitigations for each of these risks is in the final section of this document.


## Risk Analysis Process

This section is an overview of Welkin Health's risk analysis process. We proceed by asking a series of questions, each of which will be described in more detail below.


1.  What PHI do we create/receive/maintain/transmit?
1.  What THREATS are there to that PHI's CONFIDENTIALITY, INTEGRITY and AVAILABILITY?
1.  What SECURITY MEASURES do we have to protect us from those vulnerabilities?
1.  How LIKELY are the threats to manifest?
1.  What would be the IMPACT of a threat?
1.  What is the total RISK associated with the threat?
1.  What additional mitigations might we invest in?
1.  Would the proposed mitigations be effective, safe and reliable?


### Identifying the scope of analysis

The scope of analysis is all PHI that interacts with Welkin Health's information systems, as well as threats from vendors. The first step of the analysis must be the identification and enumeration of all PHI.

This is performed as a series of interviews and audits. First, a code and system audit is performed to identify any PHI that interact with Welkin Health's core system. Further, members of the engineering team as well other team members with a clinical function are interviewed to identify PHI that they interact with as a part of their role outside of Welkin's information systems.


### Risk modeling

In order to rigorously assess risk to the PHI identified in the previous step, we use a threat-oriented semi-qualitative risk model.

Risk begins with a THREAT SOURCE, a description of the intent or situation that may create threats to Welkin's systems. For a given threat source, there may be many THREAT EVENTS, which is a description of a specific threat that stems from that threat source. A threat event may come from multiple threat sources, and sources may produce many threat events.

A threat event in our format of analysis encompasses the notion of a VULNERABILITY as outlined in NIST 800-30—a threat event is included in analysis if and only if there is a vulnerability in Welkin's systems that allows for the possibility of the threat event to obtain.

A given combination of a threat source and event is referred to as a THREAT VECTOR.

Given a threat vector, we assess an overall LIKELIHOOD score, measured on the 1, 3, 9 likelihood scale, discussed below. This score represents the rough probability of an incident occurring along this particular vector.

Given a threat vector, we assess an overall IMPACT score, measured on on the 1, 3, 9 impact scale. This score represents the size of the potential damage to the confidentiality, integrity or availability of PHI along this particular vector.

We ultimately identify a level of RISK on a 1-81 scale by multiplying the likelihood score and the impact score.


#### The 1, 3, 9 Likelihood scale

The 1, 3, 9 Likelihood scale describes a rough level of probability on an exponential scale in attempt to capture the intuition that there is a wide range of possible values with large confidence intervals. The three scores with a short description of where each would be appropriate is given below.

*   **Likelihood Level 1:** Low likelihood. While an adverse impact is possible, there are extremely low odds of it being exploited, due to existing technical or procedural mitigations, difficulty of execution, or motivation of threat source.
*   **Likelihood Level 3:** Medium likelihood. A threat source would plausibly interact with this vulnerability, and may succeed in spite of some difficulty.
*   **Likelihood Level 9:** High likelihood. Incident is likely to occur unless mitigating action is taken.


#### The 1, 3, 9 Impact scale

The 1, 3, 9 Impact scale describes a rough level of severity on an exponential scale in attempt to capture the intuition that there is a wide range of possible values with large confidence intervals. The three scores with a short description of where each would be appropriate is given below.


*   **Impact Level 1:** Minor impact. Temporary degradation of availability for some patient data for some workers, or an obvious and correctable data error. No breach of confidentiality can be considered a 1.
*   **Impact Level 3:** Moderate impact. Permanent loss of a small amount of non-essential data. Significant but short degradation or loss of availability, or a moderate duration but narrow loss of data availability. Minor or temporary exposure of patient health data to workers within same health organization.
*   **Impact Level 9:** High impact. External breach of patient confidentiality. Permanent loss of essential patient data. Temporary but total system outage.


### Identification and assessment of countermeasures

Following the risk assessment, a "risk mitigation threshold" will be chosen based on an assessment of value of information—risks under this threshold will be considered out of scope for mitigation analysis. Similar threat vectors may be grouped for mitigation analysis.

Any risk above the mitigation threshold will be analyzed to identify potential countermeasures. Countermeasures will be evaluated in terms of their effectiveness and operational burden and will ultimately be given a priority.


### Scope of analysis

The scope of analysis is all PHI that interacts with Welkin's information systems, considering both what data Welkin's systems touch and the various ways that information is handled. This means we must consider what data goes where -- i.e. considering both storage in the database, storage in cloud services, transmission over the Internet, etc.


#### Data Welkin Stores

Welkin stores the following categories of patient information:

*   Demographic data (e.g. birthday/age, sexual orientation, race)
*   Contact information (e.g. addresses, phone numbers, email addresses)
*   Results of lab tests (e.g. HbA1C values, height, weight)
*   Completed assessments (e.g. the [WHO-5](http://www.ncbi.nlm.nih.gov/pubmed/25831962))
*   Patient correspondence (e.g. messages sent in the Welkin smartphone app, emails, text messages[^1])
*   Appointment records (e.g. records of an in-clinic "diabetes checkup" visit, records of a "blood pressure goals" phone call)
*   Patient diagnoses (e.g. hypertension, diabetes)
*   Prescription names and dosages (e.g. ativan, metformin)
*   Program enrollment (e.g. )
*   Audio recordings (e.g. patient voicemails, recordings of phone calls)
*   Images (e.g. x-rays)


#### Information System Touchpoints

The PHI identified above may be present in any of the following locations:


*   In Welkin's database
*   In Amazon's S3 file storage service
*   In a Welkin user's browser (including browser cache; not including localstorage, websql or any other persistent web APIs)
*   In transit between the user's browser and Welkin's servers using TLS
*   In transit between Welkin's servers inside Welkin's Virtual Private Cloud using SSL/TLS
*   For Welkin app users only:
    *   In transit between a patient's smartphone and Welkin's servers using SSL/TLS
    *   In temporary storage caches on patient smartphones
