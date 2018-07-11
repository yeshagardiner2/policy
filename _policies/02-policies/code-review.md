---
title: Code Review
---

## Purpose

This document outlines Welkin's code review processes and policies. They are designed to ensure quality, correctness, and security.

## Scope

This document applies to all code and documentation that is checked in to Welkin's repository. As a matter of policy, we check in any software engineering work that impacts the production system. This includes the code for Welkin's application, configuration utilities used to administer our infrastructure, and any scripts that operate on production data. The processes described here are applied to all such changes before they are submitted to the repository.

## Definitions

*   Security review: a portion of a code review that is focused specifically on the potential security implications of the change.
*   Reviewer: the role of the person responsible for conducting a given code review.
*   Implementer: the person primarily responsible for the implementation of the new code in question.
*   Customer: an organization that has contracted with Welkin Health to license our cloud software services.
*   Github: a company that produces a piece of version control software (also called Github) that Welkin uses for both version control and code reviews.

## Procedure


### Version Control

Welkin uses Github for version control. As is typical with git, each developer maintains branches corresponding to the longer-lived projects/features they work on.

### Pull Requests

Welkin uses Github's "Pull Request" feature to conduct our code reviews. As it is integrated with our version control system and is a fully featured tool, it is the industry-standard choice.


### Mandatory reviews

Any change that will impact production must receive a code review from another engineer, with very restricted exceptions for trivial changes. Trivial changes are those with no functionality impact, such as changing strings in the product, adding an internal logging statement, or checking in a script that performs read-only calculations when invoked. Changes to configuration or mobile clients may be reviewed, but it is not required.


### Focus of reviews

Welkin's code reviews are designed to ensure a high standard of quality, correctness, and security is constantly maintained throughout our product. Code reviewers pay special attention to the following areas.


#### Security

All code reviews include a security review. Some changes have minimal security impact. Many changes, however, are in parts of the product that have potential security implications. Some core areas that all code reviews should assess as either irrelevant or well handled are:

*   XSS
*   SQL injection
*   User authentication and credential management
*   Cache usage
*   Data access policy
*   Network layout and security group / firewall settings
*   Any security implications that don't fit neatly into any of the above categories

#### Testing

All new features should include automated tests covering new functionality to ensure the implementation is correct and to avoid future regressions. The reviewer may ask the implementer to add additional tests for certain use cases that are not initially well covered. In some cases, automated testing is inefficient or inadequate, so implementing engineers may rely on manual testing.


#### System stability

The reviewer must assess how risky the change is in terms of system stability. If the change impacts core parts of the product or infrastructure, the reviewer will ensure that the implementer has taken appropriate steps to address these risks and ensure they will not manifest in practice.


#### Documentation

Documentation for proposed changes may come in the form of comments in the code and/or companion documents with more detailed writeups of design and implementation decisions. The reviewer will use the provided documentation when they are in the process of understanding what the change entails. The reviewer will assess whether the provided documentation is sufficiently robust and detailed such that all future readers will be able to understand the change. If it is not, the reviewer will ask for expanded documentation until they believes this standard is met.


#### Release plan

Changes will be assessed based on whether they require a database migration, an infrastructure change, or some other cause of application downtime. If this is the case, the reviewer will assess whether the implementer has designed a clear plan for shipping this change to the production environment in a way that eliminates or minimizes customer-facing impacts.


#### Other considerations

Of course, this is not an exhaustive list of things that reviewers will look for. They will also evaluate correctness, elegance, efficiency, readability, and all the other common elements that code reviews are designed to address.


#### Review process

The reviewer will discuss with the implementer and read the documentation to understand the product spec, the intent of the change, and any particularly important implementation decisions that were made. The reviewer will then look at the code in the Github Pull Request, checking it out locally as needed for their own testing. Pull Requests allow the reviewers to leave comments directly inline attached to the parts of the code that have changed.

When the reviewer is finished, the implementer will respond to those comments, both by writing in the Pull Request and also by making changes to the code in accordance with the reviewer's suggestions and insights.

There may be only a single round of back-and-forth for simple changes, but complex changes will generally entail multiple rounds of discussion and iteration.

