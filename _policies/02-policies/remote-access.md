---
title: Remote Access
---

## Purpose

Welkin stores PHI on many of its servers and exposes PHI in the coach portal product. It's therefore important that access to both the product and our servers be done only through secure channels. This document outlines the minimum requirements for such secure access.

## Scope

This policy applies to all of Welkin's information systems.


## Connection Security

Connections to Welkin's coach portal application must use a standard, up-to-date web browser. This web browser must support current SSL/TLS encryption standards (see the PHI Encryption Standards & Policies document for a definition of what this means). The procedure Welkin employees use to access the coach portal application is the same as the procedure that Welkin's customers use, and has the same requirements.

Connections to Welkin's servers themselves for administrative access, rather than the coach portal application, must only occur over Welkin's secure VPN. This is indeed the only way to access Welkin's servers, which are firewalled from all network traffic except VPN connections to the VPN gateway and HTTP/S connections to the web server load balancers. Access to the server occurs over VPN, but must be additionally authenticated by the target server using an RSA private key; password-only authentication is not permitted.

The sole exception to the above is that administrative access to the VPN machine is also exposed outside the firewall to prevent the possibility of lock-outs; only Welkin's network administrators have access credentials to the VPN software's administrative interface, not any other employees.

Access to Welkin's VPN (i.e. the granting of a VPN credential) must be approved by the company's Security Officer. VPN connections must use TLS 1.2 and use client certificates with 128-bit keys. Password-only credentials are not permitted; employees are only ever to be granted VPN credentials that meet Welkin's minimum encryption requirements.

Connections to Welkin's servers must occur only from Welkin-approved devices. These devices must comply with all requirements for Welkin employee machines, including having encrypted hard drives, secure passwords, and up-to-date anti-virus software, as described in Welkin's Device Security Policy.

No remote access is allowed to Welkin's office computer network. Welkin's servers are all located in AWS, and are not in any way connected to the office network.
