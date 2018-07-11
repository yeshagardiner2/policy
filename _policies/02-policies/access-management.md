---
title: Access Management
---

## Purpose

This document outlines how Welkin:

*   Manages Amazon Web Services accounts that govern access to our production servers
*   Manages Welkin administrative interface accounts
*   Manages customer accounts
*   Specifies and enforces policies governing access to patient data from customer accounts
*   Securely authenticates both administrative and customer accounts

##  Scope

This policy covers all information and systems in Welkin's environments, including any personal devices interfacing with Welkin systems.

## Access to Information Systems {#access-to-information-systems}

All access to Welkin information assets and information systems must be controlled to ensure only authorized users or groups of users are granted rights. All access must comport with the Welkin Technology Acceptable Use Policy and applicable legal, statutory, or regulatory compliance requirements.

Access and access controls must abide by the following principles:

*   Deny by Default: Controls must deny access by default, unless access is expressly configured.
*   Need-To-Know: Only users and processes that require access to information or information systems to perform authorized job functions may be permitted access.
*   Least Privilege: Users and processes must be granted the least level of permissions necessary to perform their intended function(s).
*   Unique User Identification: Systems that store or process Welkin Sensitive/Regulated information (as specified by the Welkin Data Classification Policy), must assign a unique identifier for tracking user or process activity.
*   Shared accounts may be used for services that do not handle Sensitive/Regulated information, but access must still be restricted to teams/groups based on business needs.


### Robot Users

Automated programs, scripts, and processes are permitted, but access must satisfy the same principles as human users. Each automated user must have an identifiable individual or team owner.


## Amazon Web Services Accounts

These accounts provide access to the production servers (although note that access is only possible over VPN, see the Remote Access Policy for more information). They are administered using Amazon's IAM product; every system administrator who has access to the production machines has a unique IAM account and associated set of permission grants. These systems administrators have access to all production servers, however only some are "admins" who can add/remove/modify other IAM users. IAM administrative status is controlled by the Security Officer.

Authentication to the AWS console containing the Amazon IAM product is guarded by standard AWS account password requirements with 2-factor authentication and enforced password rotation enabled. Welkin uses LastPass to store AWS account passwords and Google Authenticator for 2-factor.


## Welkin Administrative Interface Account Management

New Welkin administrative accounts may only be created by a current administrator with the approval of the Security Officer. This operation requires credentials both to Welkin's VPN and SSH key credentials to one of the production web servers (see the Welkin Health Remote Access Policy for more information).


## Welkin Customer Account Management

Customer accounts can be created, modified, and removed through Welkin's internal administrative interface. Customer accounts are also assigned specific access roles through the administrative interface.

### Account Authentication

Welkin uses the same authentication system for both its administrative interface and the coach portal product. This authentication system is password-based. When a customer account logs in the password is verified, and if verification succeeds an authentication ticket is issued to the client using cookies. This authentication ticket expires after 3 hours. All subsequent requests verify the ticket , which identifies the account and provides basic access to the API routes that provide data (static assets can be accessed without authorization, for instance to load the login page). This ticket _only_ provides basic access to these API route; the data to be returned by the route is checked against the grants that the current account (as identified by the ticket) holds. This check uses  the access enforcement scheme outlined above. If the basic access check passes but the access enforcement check fails no data will be returned (the system behaves as if the data does not exist, to prevent leaking the existence of data).

All passwords must be at least 8 characters long and contain three of the following: mixed case, numbers, special characters, and no repeating characters; passwords must be changed every 90 days. Passwords may not be re-used.

