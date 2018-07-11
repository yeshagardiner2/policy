---
title: Deployment
---

## Purpose

This document describes Welkin Health's processes for deploying new code to our various environments, both for testing and for production updates.

## Scope

This document applies to Welkin's production information systems.


## Version Control

Welkin uses Github for version control. As is typical with git, each developer maintains branches corresponding to the longer-lived projects/features they work on. This document assumes the reader has some familiarity with the git version control system.


## Continuous Integration (Automated Testing)

When a developer works on a change, they always do so in a branch. Whenever they reach a checkpoint and wish to save their work, they commit to their branch and push the branch to the repository.

Welkin uses CircleCI for continuous integration testing. We have configured our Github account to link with our CircleCI account. Any time any branch is pushed, CircleCI runs every automated test in the Welkin codebase against the most recent version of that branch. The results of all of these test runs are reported to a consolidated channel in our Slack environment.

The effect of this setup is that all engineers see the full results of Welkin's complete automated test suite run against their code at every checkpoint in their development process. This ensures that they are aware of what work they still need to do in order to avoid having their change introduce regressions in the product.


## Local Testing

### Testing in local environment

On an ongoing basis as engineers develop new features, they perform manual testing in their local environment. They also write new automated tests to cover the most important and/or complex workflows that are impacted by their changes.


### Push branch

At periodic checkpoints, the engineer will push new work from their local branch to the Github repository. As described above, this causes CircleCI to run all automated tests against the newly checked-in code. Once all local tests, both manual and automated, are passing reliably, and the CircleCI test run also passes fully, the branch is eligible to be merged to master.


## Production Deployment


### Release coordinator responsibility

For any deployment, one engineer will be in the role of the Release Coordinator.

#### Stage 1

The first stage of the production deployment creates a parallel copy of our production environment, accessible via an internal URL. The release coordinator and the involved engineers exercise the new changes in this parallel production environment to ensure everything is as expected.


#### Stage 2

After testing is complete in the parallel production environment, the on-call engineer initiates the switchover of the live production environment to the new code.


### Manual testing in production

The release coordinator monitors the production deployment as it proceeds and when it is finished. If there are any issues at all with the deployment, the on-call will immediately roll back the deployment to the previous version of production, which can be done in a single command from any qualified engineer's local environment.


### Merging to master

As is typical, Welkin has a branch called "master" that is treated specially. Engineers never develop directly on the master branch. When a feature is complete and has been released to production, the developer merges the relevant branch into the master branch.
