---
title: Third Party Service Delivery
---

## Purpose

This document outlines the steps that Welkin undertakes to vet and manage potential third-party suppliers and services. These policies are designed to ensure that Welkin's subcontractors maintain our high standards around information security and system reliability and enable us to remain in compliance with all applicable regulations, including HIPAA.


## Scope

This document applies to all third party services used by Welkin employees that have a non-trivial business import.

## Overview

Welkin makes use of several third-party services to support the normal course of its operations. This practice is ubiquitous in the modern software industry because of the convenience, quality, and cost benefits that come from using well-established services for key operational components. However, it also creates additional risk, since Welkin does not directly control the behavior of these third parties.

When Welkin evaluates an opportunity to use a third-party service in support of our operations, we undertake the following processes. We do a thorough investigation of the third party's published security materials and practices, their ability and willingness to undertake all required HIPAA compliance measures (if they will have access to Welkin customer PHI), and their reliability guarantees. Welkin also requires that they sign appropriate confidentiality agreements. The results of this investigation lead to an overall judgment of whether the increased risk of using the third-party service is worth the benefits. Finally, in addition to these pre-usage reviews, Welkin performs periodic checks on the third parties to ensure that they continue to maintain the necessary levels of compliance, quality, and reliability.


## Risk Assessment

An assessment must be made of the risk imposed by using the third-party service in question. This assessment is tailored to the nature of the service in question, but will generally include at least the following components.


*   How critical would the service become to Welkin's normal business operations?
    *   In particular, what level of Welkin customer impact would occur if the service suffered an outage?
*   What service level guarantees does the service offer?
    *   If these SLAs are not as strict as the SLAs that Welkin offers our customers, then the third-party service cannot be relied upon as an operationally critical component.
*   Will the third-party service have access to Welkin customer PHI?
    *   If so, ensure that the service explicitly guarantees that HIPAA compliance can be maintained under the usage patterns in question. Generally this involves Welkin obtaining a BAA with the service in question.
*   What are the service's publicly established compliance processes?
    *   Have they obtained third-party verification of compliance with certain standards such as ISO 27001?
    *   Do they perform third-party audits on a regular basis?
*   Do they have published security standards and processes?
    *   If so, they must be at least as strict as Welkin's equivalent security standards and processes, so as not to degrade the overall level of security that our system guarantees.
*   Are they a well-established, long-standing enterprise with strong customer references from trusted sources?
    *   Longevity is important evidence of quality and reliability in the enterprise software industry.
    *   Is there any public evidence that they have suffered past security breaches or major reliability incidents?


## Business Need

Welkin considers using third-party services only when there is a compelling business case for doing so. There are various business needs that third-party services may address. These include, but are not limited to:



*   Convenience/cost (the service provides already-built needed functionality that would take Welkin a long time and many resources to replicate)
*   Functionality (the service provides capabilities that Welkin could not feasibly replicate)
*   Reliability (the service enables Welkin to achieve a higher degree of reliability than we could otherwise)
*   Security (the service enhances Welkin's overall security efforts)

When usage of a third-party service is contemplated, the business need for the service is assessed along these dimensions and any others that are relevant.


## Evaluation

Once the risk assessment has been completed and the business needs assessed, Welkin's Security Officer and executive team come to an overall conclusion about whether to proceed with using the third-party service. These tradeoffs are complex and multi-faceted, so rather than using a rigid set of rules for making this determination, Welkin's leaders gather together all available evidence based on the analyses above and work together to arrive at the best conclusion.


## Monitoring

If a third-party service is approved and becomes integrated into Welkin's production systems, we institute ongoing monitoring of its performance to ensure that it meets the needs for which it is being used. The specifics of the monitoring required differ from service to service depending on its functionality. However, it generally involves at least:


*   Reliability: does the service deliver an exceptionally high level of reliability, meeting or exceeding the standards it claims?
*   Functionality: are our customers and our product design team satisfied with the functionality that the service provides?
*   Maintainability: does usage of the third-party service create an ongoing burden on our development team due to difficulties with keeping the integration working correctly as Welkin continues to make change and improvements?
*   Responsiveness: is a representative of the third party available to Welkin's team, and are they responsive to inquiries about their service's performance along all of the above dimensions (and any others that arise)?


## Periodic Review

Having qualified a third-party supplier initially, Welkin undertakes annual reviews of its suppliers under a variety of circumstances.

*   If a third-party service suffers an outage or a security incident that impacts Welkin, a thorough post-mortem is conducted as per our Incident Response Policy. Continued usage of the service is then reevaluated in full according to the rubrics above in light of the new evidence of potential unreliability.
    *   If there are any published reports of the third-party service suffering an outage or a security incident impacting one of their customers that is not Welkin, the same process applies.
*   If Welkin's customers report dissatisfaction or functionality deficits in the third-party service, the Business Need is reassessed accordingly.
*   In any event, at least annually, Welkin review the materials and factors described above in the Risk Analysis and Business Need sections for any relevant changes or updates. In the case of any such changes, this full policy will be executed anew to ascertain whether Welkin's use of the third-party service should continue.

