---
title: Software Development
---

## Purpose

This document is an overview of Welkin Health's software development processes. It outlines the phases that projects go through before, during, and after development. It focuses on Welkin's approaches to maintaining a consistently high standard of quality throughout the process and the resulting systems. Each phase of the software development lifecycle is described in the appropriate section below.

## Scope

Projects of different kinds and scopes may require different approaches to the details of some of these phases, or they may require additional processes beyond the basic ones outlined here. This document focuses on the components of the software development process that apply to most or all software development conducted at Welkin.


## Requirements Analysis

Before development begins on a new project, the first phase is requirements analysis. This includes both system and software requirements.


### System Requirements

What capabilities, broadly stated, must Welkin's system support in order to achieve the goals of the project? The capabilities in question would include existing software modules, system architecture configuration patterns, libraries of supporting functionality, etc. If a gap is identified in system requirements, it implies that the project timelines will likely be much longer than if the system requirements are already satisfactory. For this reason, this is an important initial planning step, since it has big implications for the trajectory of the project.


### Software Requirements

What new and improved capabilities is this project designed to deliver? This part of the requirements specification sometimes takes the form of a Product Requirements document, although for simple projects a straightforward tracking task in Welkin's project management tool may be sufficient. (As of this writing, Welkin uses Asana for project management.)

This process should include any relevant feedback from customers, the history of previous related projects, and any important timeline considerations.


## Design

Once the requirements for the project have been identified, the design phase can begin. This phase includes product design, architecture design, interface design if needed, and an implementation plan. The level of detail needed for each of these phases differs based on the project complexity.


### Product

Welkin's product design team reviews the requirements specs created above in conjunction with the designated Project Manager. Any necessary product design work is conducted up front before implementation begins (though it may proceed in parallel with the engineering design considerations in the rest of this section). The finalized product designs are recorded in Welkin's project management tool and made available for the implementing team to review and discuss with the product designers.


### Architecture

Analogously to the System Requirements phase above, the architecture design phase has the biggest potential for dramatically increasing the scope and complexity of the implementation. For this reason, it is the first part of the Engineering team's design process.

Generally speaking, architecture design will only be complex in cases where the System Requirements has identified a gap. However, even in cases where the System Requirements are satisfactory, there may still be architectural modifications that are desirable to make because these modifications will improve efficiency, maintainability, or other considerations.

If the architecture design process results in changes to be made, this will usually have a big impact on project timelines. Additionally, it will commonly result in a more complex upgrade process for shipping the project as a whole into Welkin's production environment, which is considered in the Risk Assessment phase as well as in the Delivery phase.


### Interfaces

Once the system architecture needed to support the project has been identified, any necessary interfaces can be designed. Interface design includes HTTPS interfaces (i.e. APIs) as well as internal interfaces between different modules in Welkin's codebase.

If the project involves integration with a third party (i.e. the development of APIs that cross the boundary of Welkin's system), this phase is crucially important and involves a high level of scrutiny. The RIsk Assessment phase incorporates some relevant considerations around security, privacy, and reliability. In addition to these aspects, interface design with third parties involves an often-complex process of finding the approach that best fits the existing systems while delivering on the requirements identified above. The designated Project Manager will manage communications with the third party team and coordinate the design process as well as implementation and integration testing (see below).


### Implementation plan

The implementing Engineer(s) will synthesize the above considerations into an overall implementation plan. Again, the scope and nature of this plan will depend on the complexity of the project itself. For simple changes, no formal plan may be recorded. But for any changes requiring architectural components, new interfaces, or complex product design requirements, an implementation plan is created that lays out the phases that the implementers will go through and the estimated timelines involved.


## Risk Assessment

Once the detailed implementation plan is in place, a risk assessment occurs. This risk assessment evaluates what risks the project entails. These risks can take many forms; some of the most important and common considerations are outlined here. Depending on the risks assessed, additional project resources will be brought in in the form of additional internal reviewers, modified requirements intended to reduce risk, new policies and/or procedures, etc.


### Third party dependencies

Any time a third party is involved, there are many risks that must be managed. The full process is described in Welkin's Third Party Service Delivery Management Policy. But in brief, Welkin must evaluate the security, privacy, and reliability implications of involving third-party functionality in any project.


### Architectural changes

If architectural changes to Welkin's system are needed, a higher level of risk is incurred. The most common types of risk involved in architectural changes are stability risks, security risks, and risks around the upgrade process necessary to ship the changes to Welkin's production systems.


### Security and privacy

All changes are evaluated for security and privacy implications. Certain types of simple changes are very safe in terms of their potential security and privacy impacts, but many other types of changes bear additional scrutiny. Examples include, but are not limited to:

*   Any architectural changes trigger a security review.
*   Any third-party integrations trigger both a security and a privacy review.
*   Any alterations to Welkin's web front-end trigger a review for potential XSS and SQL injection vulnerabilities.
*   Any new HTTPS interfaces have their access permissions reviewed.


### Scope of new functionality introduced

If the project represents substantial new functionality, the risks will almost always be higher than cases where the project is an upgrade or alteration to existing functionality. The standard of scrutiny on new features is therefore higher than it is on bug fixes and other analogous modifications.


## Implementation

A lead implementer is always designated for any given project. The lead implementer may delegate certain implementation tasks to other team members, for reasons of project timeline, differences in expertise, or convenience. However, the lead implementer is ultimately responsible for ensuring that all project requirements are met and for keeping the Project Manager informed of any changes in timelines.

Welkin practices pair programming when necessary or convenient to do so. We do not enforce pair programming for all projects. However, we do require code reviews of all production changes (see below).

Welkin uses Github for version control.


## Testing

All changes to Welkin's production system must be thoroughly tested both manually and automatedly.


### Continuous integration

Welkin uses Welkin uses a continuous integration framework for all software development. Our provider of these services is CircleCI. Any time a new change is pushed to any branch, including the master branch, a full run of our entire automated test suite is queued in CircleCI. The results of these automated tests are communicated to the full Engineering team via our internal communication system (as of the time of this writing, test results are sent to Slack). In this manner, all Engineering team members are kept apprised of whether our test suite is passing on both their projects and others' projects.

Whenever the master branch has a successful full test run, it is automatically deployed to Welkin's staging environment. This ensures that all manual testing conducted on the staging environment is being done on the most up-to-date synthesis of every Engineer's in-progress changes. Additionally, it ensures that system reliability is being tested, since the staging environment will not successfully deploy if some combination of in-progress changes causes system instability or unavailability.


### Unit and end-to-end tests

Welkin's test suite includes both unit tests for the individual building blocks of a new software project as well as end-to-end tests that exercise the full user flows involved in the project. All production changes must include any necessary new tests of both types, which is enforced during code review (see below).


### Integration testing

In cases where the project involves integration, there is an extensive integration testing phase. The specific case of third-party integrations (e.g. for new APIs) is described in more detail here.

Welkin collaborates with the third party to design the specifications and functionality requirements for the new interfaces as described above. Once the specifications have been agreed upon and the implementation is underway, a testing plan is created collaboratively between Welkin and the third party in question.

This testing plan involves specifications for the API calls the integration will support and a suite of success and failure cases to test. Integration testing is performed manually in a staging environment throughout implementation, with a final and complete integration test suite being run when implementation is finished. Additionally, Welkin implements internal tests that mock out the third-party service's functionality assuming it is functioning correctly, so that our automated test suite will ensure that future changes we make don't introduce bugs in the Welkin side of the integration.


## Delivery

When the lead implementer believes the project is ready to be delivered into Welkin's production environment, they undertake the final steps below.


### Documentation

The lead implementer for any project is responsible for producing internal documentation of the changes they made. This documentation is primary intended for future consumption by other Engineering team members or Project Managers who must plan projects in light of the changes that were made. This documentation is reviewed by the Project Manager to ensure that the final delivery matches up with the initial requirements and design.


### Code review

Welkin does code reviews for every non-trivial production change. We use Github's code review tool. These code reviews are conducted by a member of the Engineering team other than the lead implementer for the project. The code reviews focus on a variety of areas including correctness, correspondence with project requirements, and future maintainability. Some especially important considerations during code review are:


*   Security
    *   Was this change assessed as risky from a security point of view? If so, did the lead implementer take steps to mitigate those risks appropriately?
*   Testing
    *   Did the lead implementer include sufficient automated testing coverage to protect against future regressions?
*   Upgrade plan
    *   Is there a clear plan for shipping this change to the production environment in a way that eliminates or minimizes customer-facing impacts? In cases where architectural changes were needed, this plan will need to be more detailed and complex than usual.


### Shipping

Changes getting released to production go through at least the following steps:

*   Change review
    *   What changes are going live? The responsible parties must be present and ready to validate these changes as per the process below.
*   Production update
*   Validation
    *   See below for details.


## Validation

Once the production environment has been updated, the designated on-call is responsible for validating the changes that were made. This validation involves multiple steps, including an ongoing process of gathering customer feedback and iterating through this entire development process again for any needed improvements.


### Manual testing

All production environment updates should be manually tested by either the designated on-call or the lead implementer of the project in question. This manual testing should happen immediately after the production environment is updated to minimize any customer impact from issues that are uncovered.

In the case where a new third-party integration was included in the production update, the testing phase is more complex and especially important. The full set of end-to-end integration tests will be undertaken, ideally in conjunction with a representative from the third party, to verify that the functionality is all working correctly in both systems.


### Customer feedback

Once manual testing has concluded, the Project Manager and Customer Success teams communicate the changes to the customers who will benefit from them. They then gather feedback from those customers' Coach Portal users to ensure both that the new functionality meets the original project requirements, and also that any new requirements can be collated and ultimately turned into future projects of their own.


### Iterate

The feedback we gather from our customers, as well as further review from our own internal product design teams, informs future projects that will be undertaken. These iterations follow the same process outlined above. Usually, these processes will become less complex for iterations or revisions of the same project over time, but projects also often lead to requirements for entirely new features or functionality of similar complexity.


