---
title: Incident Response Plan
---

## Purpose

This document outlines the steps to be taken in the event of any security incident. There may exist more specific, detailed incident response plans for specific scenarios, but all will share the overall structure outlined here.

## Scope

This document applies to all of Welkin's production information systems.


## Identification

Incidents may be discovered by:

*   Members of the Engineering team
*   Members of the Customer Success team, or other Welkin Employees
*   Coach Portal users or patients
*   External sources

In all cases, the incident should be escalated to the on-call engineer. If the on-call engineer is unavailable, they will have designated a backup. If the backup is unavailable, responsibility falls to the Security Officer. This person is the primary responder.

The current on-call rotates weekly and is identified in the company directory and via internal chat. Contact information for the on-call engineer is maintained in the internal company directory.

Coach Portal users may contact their Customer Success representative and patients or other external sources may contact Welkin directly via email at [support@welkinhealth.com](mailto:support@welkinhealth.com) or [security@welkinhealth.com](mailto:security@welkinhealth.com). The on-call engineer is responsible for monitoring those inboxes at all times.

Upon being notified of an incident, the primary responder should open an incident record and record the time of notification, a description of the incident, and if applicable, contact information of the notifier. The incident description should include any information about the scope or target of the incident including server name, address, or environment.

Upon initial discovery, the primary responder should engage any other team members deemed necessary for incident assessment.


## Assessment

The primary responder and any necessary team members assess the incident by asking and answering a series of questions. These include, but need not be limited to:

1.  Is the incident real or perceived?
1.  Is the incident still in progress?
1.  What is the impact on the business should the attack succeed? Minimal, serious, or critical?
1.  What system or systems are targeted, where are they located?
1.  Is the response urgent?
1.  Can the incident be quickly contained?

The incident will then be categorized by level of severity:

*   Emergency - Threat to life or public safety
*   Sev0 - Sensitive data breach, complete disruption of critical service
*   Sev1 - Partial disruption or significant degradation of service
*   Sev2 - Moderate or minor service disruption or degradation

Depending on the severity of the incident, additional resources may be required or released prior to incident mitigation and response.


## Mitigation

After assessing the severity and urgency of the incident, mitigation steps will be identified and applied as appropriate. These may commonly include:

*   Terminating services to prevent data loss
*   Quarantining any affected servers
*   Loading data from automatic backups
*   Rebuilding services from configuration to eliminate infection or inappropriate access
*   Adding additional capacity
*   Any actions deemed appropriate by the primary responder or responsible executive officer

The response team will take notes in as much detail as is feasible during this phase. These notes must cover any issues observed and any changes made as part of the mitigation process. These notes are critical to the later production of the post-mortem report, as well as providing potential legal evidence in any proceedings related to the incident.


## Investigation

After mitigations have been applied and service is restored, members of the engineering team will investigate and understand the incident:

*   Review system logs, also observing any gaps
*   Review database logs to determine the full extent of data accesses during the incident
*   Review intrusion detection logs
*   Review platform identity & access logs
*   Review the incident log itself

While performing this review all analysis should be documented. Any additional evidence gathered to complement the evidence collected in the Mitigation step must also be documented. For example, when it is deemed that any of the reviewed data sources listed above contain relevant information that should be recorded during this step.

The  analysis should be thorough enough to provide an understanding of the root cause(s) of the incident. The root cause will be documented in the post-mortem (described below).


## Post-Mortem

Within three working days, the response team shall discuss and agree upon a post-mortem review document. This document will outline a timeline of the incident and incident response as best as it is understood, including a copy of any and all communication concerning the incident.

This document will also contain a written description of the root cause of the incident, based on the analysis performed and evidence gathered during the Mitigation, Investigation and other previous steps.

Along with a description and root-cause analysis, the post-mortem document should include suggested defenses for similar attacks in the future and an assessment of their cost and benefit. In addition, the post-mortem will review the incident response and highlight what worked and what didn't.

Insights from the incident will be used to create or refine a scenario-specific incident response plan and/or this general incident response plan, which will then be reviewed by the engineering team and all other appropriate parties.

A post-mortem review will be scheduled for a time several weeks after the incident, to review whether the suggested mitigations have been successfully implemented, and to assess if any further action is required.

## Periodic Testing

Welkin tests a selected subset of incident response plans annually.

