---
title: Disaster Recovery Plan
---

## Purpose

This Disaster Recovery Plan documents the contingencies and planning that Welkin has in place to recover from a disaster that disrupts normal functioning of our IT systems. The focus of this document is on recovery from a disaster that damages or destroys the hosting infrastructure that runs our product operations, which our customers rely on in the course of their patient care.

## Scope

This document applies to Welkin's production information systems.


## Responsible Parties & Team Communication

The Welkin engineering team has an on-call rotation. At any given time one engineer is responsible for monitoring our error alerting channels and responding to production errors as they arise, including cases of catastrophic failure. This responsibility rotates weekly.

In the event of a disaster, the on-call engineer will implement the recovery plan outlined in this document. They will notify the Security Officer of the outage and delegate investigative or recovery tasks to other engineers trained in the disaster recovery process as needed. We maintain an up-to-date contact sheet with phone numbers and both professional and personal email addresses for all engineering team members.


## Goal Metrics

*   Recovery Time Objective: under 2 hours to be fully operational.
*   Recovery Point Objective: data state as of 15 minutes immediately before the disaster.

## Site Designation & Backup Processes

Welkin's computing operations are hosted on Amazon's Web Services cloud. The core services of AWS that Welkin requires to run are EC2 instances (for running database and web server virtual machines) and S3 storage (for storing binary user data and database backups).

EC2 instances are all assigned to an "availability zone." For more information on Amazon's availability zones for EC2, refer to the EC2 [documentation](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-regions-availability-zones). For the purposes of this document a "disaster" refers to an event that has rendered our entire availability zone unusable. In the event of such a disaster, we will bring up new instances of our EC2 machine images in a different availability zone. Our current availability zone is located in Amazon's "US East" region.

S3 automatically replicates stored data on multiple devices in different data center facilities within a region. It is designed to sustain the concurrent loss of data from two separate facilities at a time. For more information about S3 durability, see the [S3 documentation](http://docs.aws.amazon.com/AmazonS3/latest/dev/DataDurability.html).

Welkin's database backup strategy has two layers. First, as a part of Amazon's Relational Database Service (RDS), Welkin keeps 10 days of point-in-time recovery logs. Second, Welkin takes nightly snapshots that are permanently archived.. In the event of a disaster, after new EC2 instances have been created in a new availability zone, we load the most recent backup from before the disaster.


## Testing and Training

Product stack bringup occurs routinely as part of normal product operations. This is by design; we rely on the same tools to both administer development stacks and the production stack.

However, we do not routinely re-create the network and logging stacks, nor do we routinely bring up development stacks in different availability zones. As part of the HIPAA Risk Assessment conducted most recently before this writing, an Opportunity for Improvement was identified to do more regular and thorough tests of the Disaster Recovery Plan. Going forward, Welkin will perform a full test of its Disaster Recovery plan at least annually, including the recreation of the network, logging, and product stacks in a new availability zone. We will create separate DNS entries for these tests to avoid disrupting service during the exercise.

Welkin publishes engineering documentation on disaster recovery and trains the engineering team on their use.

