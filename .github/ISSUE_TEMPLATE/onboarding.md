---
name: New engineer onboarding
about: Onboarding task list for a new engineer, their manager and their buddy
title: Onboarding <USERNAME>
labels: ''
assignees: ''

---

# Pre-onboarding

- [ ] **Manager**: send the engineer a copy of the [Pre-onboarding Reading List](https://github.com/hypothesis/onboarding/blob/main/docs/reading_list.md)

# Introduction

- [ ] **Manager**: **schedule a product walkthrough** for the engineer with someone from product or support
  - [ ] **Engineer**: check off this item once you've had the product walkthrough
- [ ] **Manager**: **assign a buddy** for the engineer's onboarding
  - [ ] **Manager**: schedule a 1:1 between the engineer and their buddy
  - [ ] **Engineer**: check off this item once you've had your first 1:1 with your buddy
- [ ] **Engineer**: (re-)read the [Hypothesis Company Principles](https://web.hypothes.is/principles/)

# Development environment

- [ ] **Engineer**: read our high-level architecture overview.
      Currently this is [Nick's H Architecture Talk](https://docs.google.com/document/d/1saDTLAniQiwV3KlUE7imo1ZP2BVSVEOQm_yfbKbCKn4/) from 2017
- [ ] **Engineer**: set up your local development environment and get everything working locally.
      Follow our [Setting up Your Hypothesis Development Environment](https://github.com/hypothesis/onboarding/blob/main/docs/DEVELOPING.md) guide
- [ ] **Engineer**: learn how the development environment works

# Making simple pull requests (PRs)

In this phase of your onboarding you'll start making PRs to Hypothesis projects
to fix simple issues, getting your PRs reviewed, and deploying your PRs to
production.

- [ ] **Buddy**: identify some good first issues and assign them to the new engineer

* **Engineer**: before making your first PR:
  - [ ] (Re-)read our [Code of Conduct](https://github.com/hypothesis/.github/blob/main/CODE_OF_CONDUCT.md)
  - [ ] (Re-)read our [Engineering Values](https://web.hypothes.is/jobs/engineering-values/)
  - [ ] Read our [guidelines for how to write a good PR](https://stackoverflow.com/c/hypothesis/questions/385/386)
    and the amazing [How to Make Your Code Reviewer Fall in Love with You](https://mtlynch.io/code-review-love/) by Michael Lynch

- [ ] **Engineer**: submit your first PR.

  Our engineering values include **Keep it simple**, and **Communicate, communicate, communicate**.

  Make sure to keep your PRs small and simple. Small PRs are easier to review,
  they get approved more quickly, and crafting them helps you write clearer,
  better organized code and spot mistakes. Simple, less demanding code is
  easier to maintain and debug.

  Write a good pull request title and description.
  Explain your thinking and include any necessary context for your reviewer and
  for future developers reading the commit and PR history.
  Include testing instructions, and screenshots if relevant.

- [ ] **Engineer**: find a reviewer for your first PR.

  It's up to the developer to find someone to review their PR. This usually
  just means `@mention`'ing certain individuals (or `@developers`) in a Slack
  channel (like `#prod-general`) with a link to your PR and asking someone to
  review it.

- [ ] **Engineer**: get your first PR approved by its reviewer.

  This may mean responding to any changes suggested by your reviewer and going
  through the review/respond/re-review cycle until your reviewer approves your
  PR. [How to Make Your Code Reviewer Fall in Love with You](https://mtlynch.io/code-review-love/)
  contains guidelines on how to respond to suggestions.

- [ ] **Engineer**: read our documentation on [how to deploy a PR](https://github.com/hypothesis/playbook/blob/main/docs/deploying.md)

  Our engineering values include **Ship quickly, but sustainably**.

  We aim to have a reliable, non-intimidating deployment mechanism that enables
  developers to deploy their own PRs and to do many small deployments a day.

  Deploying small PRs one-by-one makes deployments easier to test because each
  PR needs fewer cases to be tested. It also makes problems easier to debug
  because fewer changed lines of code have been deployed at once.

  Deploying frequently enables fixes and improvements to get to users faster
  and avoids the risk of moving too far in the wrong direction without getting
  real feedback.

- [ ] **Engineer**: deploy your first PR to production.

  You should deploy the PR to QA, test it on QA, deploy it to production, then
  test it on production.

  We mostly rely on automated tests (which you'll have written as part of your
  PR), testing locally, and code review. So testing your PR on QA and
  production should just be a final quick check and shouldn't take more than a
  few minutes.

# Deploying Dependabot PRs

We use [Dependabot](https://github.com/dependabot) to keep the dependencies of
all our apps up to date by sending
[automated dependency update PRs](https://github.com/pulls?q=org%3Ahypothesis+is%3Apr+sort%3Acreated-desc+label%3Adependencies+)
to our repos.

In this phase of your onboarding you'll begin handling your share of Dependabot PRs:

- [ ] **Buddy**: identify some good first Dependabot PRs and assign them to the engineer
- [ ] **Engineer**: review, merge and deploy your first batch of [Dependabot PRs](https://github.com/pulls?q=org%3Ahypothesis+is%3Apr+sort%3Acreated-desc+label%3Adependencies+).

  See [How do I handle a pull request from Dependabot?](https://stackoverflow.com/c/hypothesis/questions/181)
