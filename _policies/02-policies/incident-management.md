---
title: Security Incident Management
---

## Purpose

This document outlines the process Welkin follows to ensure a high level of security.

## Overview

Our approach to information security follows a five-part cycle of continual improvement.

**Prepare** to deal with incidents: develop a playbook of incident response planning, perform regular audits and incident drills, maintain a high level of information security awareness.

**Identify** and report information security incidents: practice vigilance in monitoring and investigating suspicious events, escalating if appropriate.

**Assess** incidents: identify the scope and impact of any incidents that do occur.

**Respond** to incidents: after assessing, perform any steps to ensure the immediate mitigation, containment and elimination of threats.

**Learn** the lessons: this includes not only careful reflection about the proximate and root causes of any security incident, but also implementing any fixes or additional layers of "defense in depth".

This document covers each phase in depth.


## Prepare

Preparation comprises the largest component of our effort.

At the top level, we maintain an incident response plan that outlines notification and escalation procedures, as well as assessment and mitigation strategies. To ensure continual vigilance, we do regular, holistic security reviews, typically every four weeks, and no less than every eight weeks.

These security reviews begin with an examination of all significant changes to the Welkin Platform since the last security review and an assessment by the engineering team of any new security risks or opportunities posed by these changes. In addition to looking at system changes, we maintain a list of top threats and review our stance towards them. For example, XSS vulnerabilities are a persistent risk for any web application, so we consider any new possible attack vectors, or any mitigations from the security community at large.

Security reviews typically identify some specific mitigations, and some areas for further investigation, so as a part of the security review process we track our progress towards implementing any defenses identified in a prior security review. Any high-priority or urgent items are resolved immediately. Low-priority improvements are prioritized as part of general product planning.

Outside of this periodic security review process, all new code is reviewed for security in addition to general quality and correctness. When new code touches on any of the top threats described above, it is subject to additional specific scrutiny around the top threat in question.

On an ongoing basis, we maintain an on-call rotation and escalation path with clear contact information. At any given time, an engineer who has been trained appropriately is acting as the designated on-call. They receive alerts about errors and events in the system that should be investigated and they do so promptly according to the procedures outlined below.

The engineering team subscribes to a variety of mailing lists where security updates, patch announcements, and other events of interest that are germane to our system configuration are announced. In this manner, we stay current on any new security bulletins.

We fully patch all operating system packages on both our production systems and our development systems regularly - typically weekly, and in any event no less than once every two weeks.


## Identify

Identifying security incidents has two main components: good monitoring and constant vigilance.

To ensure good monitoring, we have several layers of defense. We run AlertLogic's cluster-level Intrusion Detection Software in our AWS environment (we have a BAA in place with AlertLogic). In addition, we have machine-level alerting for unusual access patterns. These sources are aggregated for review and monitoring by the on-call engineer.

In addition to technical monitoring, we maintain constant contact with our healthcare partners to ensure we're notified of any possible security incidents outside of the Welkin system itself, or any unusual system behavior that escapes our monitoring processes. Encouraging and promptly reviewing reports from users of a system is an essential and often overlooked component of monitoring and Welkin's Customer Success and Engineering teams ensure that we maintain these open channels of communication at all times.

Finally, system security monitoring is a part of our general on-call rotation across the engineering team, so any unusual events or system behavior can be correlated, and suspicious patterns identified quickly.


## Assess

In the event of an incident report, it is the responsibility of the primary responder to investigate and assess the scope and severity of the incident. The details of this process are outlined in Welkin's Incident Response Plan, but in short, the responder will classify the incident by severity and engage resources appropriate to that level.

*   Emergency - Threat to life or public safety
*   Sev0 - Sensitive data breach, complete disruption of critical service
*   Sev1 - Partial disruption or significant degradation of service
*   Sev2 - Moderate or minor service disruption or degradation


## Respond

After assessing a security incident and engaging the appropriate resources, such as engineering team members, technical executives, medical experts, or public safety officials, the response team will respond to the security incident.

The response may include technical mitigations such as:

*   Terminating services to prevent data loss
*   Quarantining any affected servers
*   Loading data from automatic backups
*   Rebuilding services from configuration to eliminate infection or inappropriate access
*   Adding additional capacity
*   Any actions deemed appropriate by the primary responder or responsible executive officer

The response team will take detailed notes during this phase of any issues observed and any changes made, as specified in the "Mitigation" step of the Welkin Incident Response Plan.

In addition to the technical response, the team will identify and plan for how to communicate externally to partners as needed, and will do so as promptly as is feasible.


## Learn

In the event of an incident, we identify and implement changes to improve the security process. The engineering team will carry out a post-mortem as described in the Welkin Incident Response Plan and schedule a post-mortem review several weeks in the future to ensure appropriate progress is made towards the security goals identified in the post-mortem.

The post-mortem will include a thorough timeline of events including a copy of all communication concerning the incident response, as well as a written analysis of the root cause of the incident, and an assessment of processes that worked well and of improvements that could be made. Any process improvements will be incorporated into this document, the General Incident Response Plan, or a targeted scenario-specific incident response plan.


