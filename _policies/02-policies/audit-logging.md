---
title: Audit Logging
---

## Purpose

The purpose of this policy is to define requirements for and providing a reliable audit trail of system events and activity in order to identify unauthorized access or activities.

## Scope

This policy applies to all Welkin information, information systems, workforce members, and contractors.

## Audit Logging

Information system logs are critical to tracking Welkin operations, user activities and identifying security events, incidents and/or breaches. In addition, information system logs are a prerequisite for incident response and remediation.

Welkin information systems that store or process Sensitive/Regulated information must:

*   Link access events to individual users or processes
*   Synchronize system clocks using industry accepted sources, and protect system time configuration from tampering
*   Protect audit logs from alteration or deletion
*   Back up audit logs to a centralized logging system
*   Limit access to audit logs to those with a job-related need

## Logged Events

Welkin information systems that store or process Sensitive/Regulated must ensure that the following events are logged in audit trails:

*   User access to production systems and data, including Welkin workforce members, contractors, and vendors
*   Failed access attempts (invalid login, failed SSH, etc.)
*   Initialization of audit logging systems, if applicable
*   Stopping or pausing of audit logging systems
*   Elevation of privileges or impersonation
*   Changes to baseline configurations and virtual machine images

## Log Content and Format

Each log entry must retain the following information at a minimum:

*   User identification
*   Type of event
*   Timestamp


## Audit Log Review

The Security Officer must review audit logs for information systems that store or process Sensitive/Regulated data, either manually or via an automated system. Anomalies must be investigated as potential security incidents.

