---
title: Encryption Standard
---

## Purpose

This document details Welkin's encryption standards and policies as applied to data in our system both in transit and at rest.

## Scope

This policy applies to Welkin's production information systems.

## Overview

 Welkin uses encryption extensively to meet and exceed HIPAA requirements and provide the maximum feasible security for our users. We use encryption in multiple places, both to encrypt data communications (i.e. "in transit") and storage (i.e. "at rest"):

*   The application transport layer (i.e. using TLS when sending communications over the Internet, including not only web server traffic but also administrative access to our servers via VPN)
*   The database storage layer (i.e. individual records in the database are encrypted)
*   The device persistence layer (i.e. the filesystems we use to store application data, including database files)

These encryption standards apply not only to Welkin's servers, but any other devices we use that may at some point contain PHI, such as development laptops.

The remainder of this document outlines how Welkin uses encryption in each of these environments, as well as the minimum standards encryption must meet in each case.

## Acceptable Storage Locations for PHI

Welkin tightly controls where PHI is allowed to reside in order to ensure that it is always appropriately encrypted. The only additional acceptable location for PHI beyond at rest in our database and in transit over HTTPS is on Welkin-approved development workstations (i.e. developer laptops) and in third-party services with which we have appropriate controls in place (e.g. BAA - see below). Development workstations must comply with our device standards, in particular they must use fully encrypted hard drives (currently the OS X Filevault is the only approved hard disk encryption program), as well as maintaining good security standards (i.e. have up to date anti-virus, strong passwords, etc; the full list of development machine standards beyond encryption is out of scope for this document).

Note that Welkin's server operations rely on some 3rd-party services that handle PHI. In all cases we have BAAs with these services ensuring that they will appropriately encrypt and store PHI.


## Welkin Health Patient-to-Coach Email

Welkin uses Mailgun, a provider of email routing services, to send and receive emails between coaches and patients through our platform. Welkin has entered into a BAA with Mailgun.  Since the default email protocol cannot be guaranteed to be encrypted in transit, Welkin cannot guarantee for our patients that any PII or PHI transmitted through Mailgun will always be encrypted at rest and in transit.

Welkin therefore disables email communications by default in all customers' Welkin environments. Email can only be manually enabled on a per-patient basis by a coach with permissions to do so. This action should only be taken by such coaches when an appropriate formal consent has been obtained from the patient, indicating that they understand the risks associated with the use of email in this manner and that they consent to those risks in return for the convenience. In some cases, these consents will be designed and gathered within the Welkin platform. In other cases, these consents may be designed and gathered outside of the Welkin platform by our partners, for example by obtaining hard-copy signatures in-person. Welkin includes instructions in the UI for enabling email that reminds coaches not to enable the feature unless they are certain that the appropriate consent has been obtained based on their organization's specific procedures for collecting such consent.

While encrypted email services exist, these services are cumbersome to use, especially for less tech-savvy patients. Large numbers of patients would refuse to use these services or be unable to. Therefore, Welkin will continue to offer unencrypted email communications with coaches to patients upon the patient's request and formal consent, since many patients will prefer the increased convenience even when it comes with some data security risk.  Patients also have the option of continuing to receive Welkin's services but to not receive PHI through unencrypted email.


## Transport Layer: Web Product Traffic and 3rd-party Data Integrations

This communication includes all web traffic (i.e. all HTTPS traffic; Welkin only supports HTTPS access to our production servers). This includes client web browser traffic, client Android and iOS app traffic, and 3rd-party service traffic. 3rd-party data integrations access Welkin's servers the same way web browsers do, i.e. by making HTTPS requests to our domains.

HTTPS communication requires TLSv1.2 using a cipher that OpenSSL deems as "high" encryption. Refer to the [OpenSSL documentation](https://www.openssl.org/docs/manmaster/apps/ciphers.html) for more information about the current meaning of the "high" setting.

The primary SSL certificates Welkin uses is a wildcard SSL Cert for \*.welkinhealth.com, but we have separate certificates used when whitelabeling the application URL for partners.

Our SSL certs are generated by Amazon Certificate Manager, and injected directly into our load balancers by AWS at startup. There is no external way to access the load balancer machines, so the certificates themselves are never exposed to any machines other than the load balancers that use them. The certs are automatically rotated and renewed by AWS. The certs use 2048-bit RSA keys.


## Transport Layer: Administrative Access

All administrative access to our servers must be done over VPN; only the VPN gateway machine and HTTPS load balancers are exposed to the public internet. VPN communications must be encrypted with TLSv1.2. We use OpenVPN as our VPN server with OpenSSL configured as its SSL/TLS engine.


## Database Records

All PHI Welkin stores in its database is encrypted with a customer-specific encryption key. This encryption happens in the Welkin application itself, so the database never handles unencrypted PHI. The encryption/decryption happens on every write/read of data by the Python web server application. Data is encrypted using AES256 keys in AES's CBC mode, using a 1-block initialization vector generated from PyCrypto's [Random function](http://pythonhosted.org/pycrypto/Crypto.Random-module.html). The AES256 keys are generated using Amazon's Key Management Service Python utility library.

The customer-specific AES keys themselves are stored in the database in a separate table. Before they are stored, they too are encrypted using a master key stored in Amazon's Key Management Service. Amazon manages the generation of and access to the master key used to encrypt/decrypt customer keys. Access to the master key is granted to our EC2 instances' IAM roles, and to Welkin administrators via the AWS console and command line tools. All KMS keys, including our master key, are encrypted using AES256 in GCM mode (see [Amazon KMS docs](http://docs.aws.amazon.com/kms/latest/developerguide/crypto-intro.html)).

In addition to encryption, customer-specific data is logically separated at the application layer by tagging all root data with a customer id.


## File persistence: Database files and logs

The database files themselves are stored on an encrypted Amazon RDS instance. This is a virtual, encrypted network filesystem managed by Amazon. The data is encrypted "at rest".

On-machine application-related logs (nginx access logs, postgres query logs, and web server logs) on each EC2 instance's encrypted volume. The database and log files are backed up and stored using a different encryption scheme (see next section).


## File persistence: Backups and User-generated Binary Data

All user-generated binary data (images, audio recordings, etc) and all database/log file backups are stored in Amazon S3 buckets with server-side encryption policies set. The encryption keys for the contents of these buckets are managed by Amazon; each object is encrypted with a unique key and those keys are encrypted with a master key. All keys are AES256, although Amazon does not specify what AES mode S3 keys uses. See the [S3 SSE-S3 documentation](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html) for additional information.

Welkin maintains an independent set of user-generated binary data S3 buckets for every customer to provide additional logical segregation of customer data, but every object is encrypted with a unique key already so this doesn't provide significant additional cryptographic protection. Database and log file backups are not segmented by customer this way; a single bucket holds all production database backups and a separate single bucket holds all log archives.


