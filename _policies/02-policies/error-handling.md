---
title: Error Handling
---

## Purpose

This document explains Welkin's policies, procedures, and technical measures for monitoring our production environment for errors and for addressing those errors when they arise.

## Scope

This document applies to Welkin's production information system.

## Monitoring Policies

### On-call duties

Each week, a qualified member of the engineering team is designated as the on-call. The process for qualifying members of the engineering team is described below. On-call responsibilities rotate each week through all qualified engineers.

The on-call sets their Welkin-controlled devices (laptop/workstation and mobile phone) to enable audible push notifications for our consolidated error-reporting channel (see below for details). Any time an error is triggered, the on-call investigates it as soon as they receive the notification and works until the issue is resolved. The investigation and resolution processes are detailed later in this document.


### Qualifying engineers to be on-call

When new engineers join the Welkin team, they spend a period of time, usually a few months, learning about all parts of the codebase and infrastructure. Once they have completed projects in every major area, they are inserted into the on-call rotation as a "provisional" on-call. When it is their turn, they become the on-call with a fully qualified engineer designated as backup. The provisional on-call makes the first attempt to investigate all reported issues. If he or she is not able to quickly understand and resolve a given error, he/she escalates to the backup on-call and they work through the resolution together. Once a "provisional" on-call makes it through a full week without needing atypical levels of support from their backup, the provisional designation is removed.


## Technical Systems

All Welkin product surfaces and infrastructure are instrumented to report all errors to our unified error reporting system.

### Infrastructure

We use a combination of Sumologic and Amazon CloudWatch to monitor system resource usage and performance. Alarms will be triggered in the error reporting system if resource usage thresholds are crossed, or persistently exceeded. In addition, we use an external monitoring system (Pingdom) to catch any catastrophic failures that might also prevent the internal monitoring systems from functioning.


### Load Balancer

Our load balancers are run as a part of Amazon Web Services, so we use Amazon CloudWatch to monitor their load and performance.


### Web Server

Web servers are co-located with application servers, and record access and error logs directly on those machines. Web server logs are backed up to Amazon S3 and rotated daily. Error logs are also synced to the error reporting system.


### Application Server

Our application server records logs in system files, which are backed up and rotated daily. Any errors or warnings are additionally directed immediately to the error reporting system.


### Search Service

We monitor the freshness and availability of our search service by making special requests to it from our application servers where it reports the time it last indexed an update. If the index becomes stale or the search service unresponsive, the error reporting system is notified. Further, once a minute, new objects are indexed, and any failure to index is reported.


### Task Queue

Our automatic task queue communicates to the error reportin system if it fails to run any job, or if it encounters any errors communicating with the database. It is also monitored via a health check similar to the search service.


### Third-party services

Welkin integrates with several third party services. In most cases, this is done via the Welkin Task Queue system in a manner that will report failures and retry in the face of them in a manner appropriate to that third party service.


### Database

Our application servers and task queue maintain a connection pool with our database at all times. Any unavailability of our database will be immediately noticed by one or more of our application servers and reported to errbit.


## User Reports

As part of each of our partnerships, Welkin designates one or more members of our Customer Success team as assigned representative(s) for that partner. The Customer Success rep establishes relationships and communication channels (generally email) with the appropriate points of contact and "super-users" within the partner organization.

As part of this relationship-building, the CS rep and the partner team work to establish processes by which Welkin users in the partner organization can report confusing or erroneous behavior they observe in the product to the Welkin team. While we strive to have accurate and high-quality automated monitoring across our entire infrastructure, user reports are an important failsafe mechanism for ensuring that pernicious silent errors do not remain uncorrected.

As of this writing, the process for user reports is managed through Welkin's Zendesk account. If the CS rep determines that the message constitutes an error report, they will add the engineering on-call alias to the Zendesk ticket. This sends a Slack notification to the on-call and alerts them to investigate the report in the ticket.


## Investigation Process

The on-call investigates every error that is triggered. In many cases, these errors are determined to be spurious; most of our error reporting pipelines are tuned to be overly permissive, so that we don't suppress legitimate errors, even at the cost of passing through false alerts. In the case that the error is determined to be legitimate, the on-call immediately investigates the error through whatever means necessary, which may include, but is not limited to:

*   Reviewing the captured stack trace and reading the relevant sections of the code
*   Logging in to a test account in the relevant environment and attempting to reproduce the behavior
*   Asking the Customer Success team to reach out to the affected customer user for further information
*   Investigating system logs surrounding the error to discover the error context
*   Investigating database state to identify unexpected results


## Resolution Process

Once an error has been fully understood, it is categorized by severity.

The most severe errors will be fixed immediately by the on-call and this fix will be deployed into the production environment after the appropriate rounds of code review, automated testing, and manual testing. This may be done as a full deploy of the master branch or as a cherry-pick, depending on the context. Since Welkin's environment supports "zero-downtime" production updates, these severe bugs can be fixed swiftly for all affected users without causing downtime.

Moderate severity errors will be fixed right away and will go through code review and automated/manual testing. However, the deployment of the fix will be delayed until the next scheduled production release (usually 2-3x/week).

Non-severe errors are recorded in our project management tool, Asana, and will be prioritized as part of our regular project planning processes.


## Customer Communication

For any user-visible error of moderate severity or higher, the on-call will alert the appropriate member of the Customer Success team about what happened. The Customer Success representative will then reach out to all affected users, letting them know that Welkin is aware of the error, offering short-term workarounds, and providing a timeline for when the error will be resolved. The Customer Success rep and the on-call engineer will remain in contact about any subsequent communications with the users in question so that their input can be incorporated into the on-call's assessment of the error's severity and status. This customer outreach component is a crucial part of error handling. It is not enough to handle errors efficiently; we must ensure that our customers come to trust our vigilance in monitoring their experience of our software and we must establish open lines of communication with them so that they view themselves as partners in ensuring a very high level of ongoing product quality and support.

