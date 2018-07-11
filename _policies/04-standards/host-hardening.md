---
title: Host Hardening
---

## Purpose

The purpose of this Standard is to specify requirements for hardening end devices (servers and clients) that Welkin controls.

## Scope

This Standard applies to all production hosts that Welkin configures and maintains.


## OS Hardening Requirements
All production host operating systems shall be configured as follows:

* Operating systems shall be installed on hosts only from bare images, and only via automated configuration management.
* Host password logins shall be disabled. SSH root keys shall not be permitted.
* Swap shall be disabled to avoid writing in-memory secrets to unencrypted volumes.
* No password-based services shall be installed automatically. Password-based services (such as PostgreSQL) shall provisioned only with unique, per-resource credentials. No default passwords shall be permitted.
* All host ports shall be opened only via whitelist.
* Host clocks shall be synchronized via NTP.
