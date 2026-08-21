# Contributing to Z-Wave Alliance Open Source Project

Want to contribute? Great! First, read this page (including the small print at the end). By submitting a pull request,
you represent that you have the right to license your contribution to the community, and agree by submitting the patch
that your contributions are licensed under the BSD-3 license. Before submitting the pull request, you must have tested
your changes and check that they follow the project guidelines for contributing code.

## Contributing as a Working Group Member

As a participant of the Working Group, you can attend Working Group meetings and propose changes to the work group
documents.
You can report bugs and request features in the Issue Tracker, as well as contribute bug
fixes and features that do not impact the specification as a pull request. For example: ports to add APIs to alternative
programming languages (e.g. Java, JS), hardware ports, or an optimized implementation of existing functionality. For
features that impact the specification, please join the Core Stack or Application work group within the Alliance.
The requirements to become a member of the Repositories are:

- Must be a Participant member or higher of the Alliance
- Must be a Working Group member
- Have signed the Alliance DCO
- Agree to the Code of Conduct
- Agree to the License
- Have approval from your company's official approver

## Contributor Types

Group member - Create pull requests, Review pull requests, Create issues<br>
Community Leader - Create pull requests, Review pull requests, Create issues Merge pull requests<br>
Development Lead (only 1)- Create pull requests, Review pull requests, Merge pull requests, Bypass review requirements<br>
Vice Lead (optional) - Create pull requests, Review pull requests, Merge pull requests, Bypass review requirements<br>

The Development lead is appointed by the Community Leaders, a Development Lead must have been a Community Leader for
at least 1 year.

## Bugs

If you find a bug in the source code, you must submit a GitHub Issue. The bug report must contain a detailed
description of the issue. A step-by-step instruction for predictably reproducing the issue should be added if
possible. Even better, you can also submit a Pull Request with a fix.
If possible, the pull request should implement the relevant unit or system tests for testing that the bug is fixed.

## New Features

You can request a new feature by submitting a GitHub Issue. If you would like to implement a new feature, please
consider the scope of the new feature:

- Large feature: first submit a GitHub Issue and communicate your proposal so that the community can review and provide
  feedback. Getting early feedback will help ensure your implementation work is accepted by the community. This will also
  allow us to better coordinate our efforts and minimize duplicated effort.
- Small feature: can be implemented and directly submitted as a Pull Request.

Make sure that all new features are covered by unit or system tests, with at least 80% line coverage. If this is not
possible it must be clearly stated in the pull request with an explanation of why the line coverage is lower.

Be aware that new features might require specification work. Community Leaders can request that a feature is added to a
specification before it is merged.

## API Changes

API changes will often have a major impact on other projects or members using the code and should therefore only be used
as a last resort. Pull requests containing a API change should clearly state that this is a API change and contain a
description of the reason for the change and the impact of the API change. Reviewers must pay extra attention to pull
requests that breaks backwards compatibility of an API to ensure that the change is necessary. 

Developers are expected to update NEWS.md file with reference to the justification (or motivation) of the "breaking change".
This file should be also scrutinized by API users when updating a component, it will help them to adapt their client
code accordingly.

### APIs

The following files are considered as being APIs

z-wave-stack/PAL/inc/*.h<br>
z-wave-stack/ZWave/API/*.h<br>
z-wave-stack/Apps/SerialAPI/*

# Contributing Code

The open source project follows the "Fork-and-Pull" model for accepting contributions.

## Initial Setup

Setup your GitHub fork and continuous-integration services:

1.	Fork the: [ZWA Protocol Stack](https://github.com/Z-Wave-Alliance/z-wave-stack.git) and
    [ZWA Test System](https://github.com/Z-Wave-Alliance/z-wave-test-system.git)
    by clicking "Fork" on the web UI.

2.	All contributions must pass all checks and reviews to be accepted.

## Setup Your Local Development Environment:

```bash
# Clone your fork
git clone git@github.com:USERNAME/z-wave-stack.git
git clone git@github.com:USERNAME/z-wave-test-system.git

# Configure upstream alias
git remote add upstream git@github.com:Z-Wave-Alliance/z-wave-stack.git
git remote add upstream git@github.com:Z-Wave-Alliance/z-wave-test-system.git
```

## Submitting a Pull Request

### Branch

For each new feature, create a working branch:

```bash
# Create a working branch for your new feature
git branch --track <branch-name> origin/main

# Checkout the branch
git checkout <branch-name>
```

### Create Commits

```bash
# Add each modified file you'd like to include in the commit
git add <file1> <file2>

# Create a commit
git commit
```

This will open up a text editor where you can craft your commit message.

### Commit Message

A commit message must comply with the following set of rules:

1. The commit message MUST comply with https://www.conventionalcommits.org/en/v1.0.0/
2. The body MUST describe WHY the change was made, in addition to other relevant context.
3. The footer MUST reference relevant issues, if any.
4. The footer MAY reference PRs, if relevant.

For item 3 and 4:
    - As URLs, if possible.
    - The references can be internal to a contributor as well as external.
    - Use https://dep-team.pages.debian.net/deps/dep3/ based on https://git-scm.com/docs/git-interpret-trailers.

Supported commit types:

- build
- chore
- ci (continuous integration)
- docs (documentation)
- feat (feature)
- fix
- perf (performance)
- refactor
- style
- test

Supported commit scopes might be found in CONTRIBUTING.md in each repository maintained by OSWG.
If no scopes are defined in a repository, do not use a scope.

Example based on https://github.com/Z-Wave-Alliance/z-wave-stack/pull/887:
```
feat(zaf): Updated CC Firmware Update MD to version 8

Upgrading to version 8 adds support for new error codes.

Origin: https://github.com/Z-Wave-Alliance/z-wave-stack/pull/887
Relates-to: https://github.com/Z-Wave-Alliance/AWG/blob/main/source/management_command_classes/command_class_definitions/firmware_update_command_class_version_8.rst
```

Example from https://github.com/Z-Wave-Alliance/z-wave-test-system/pull/139
```
fix: Correctly parse frames with field between length and data

In CC Firmware Update Meta Data the Firmware Md Report command has
a field in between the "Number of Firmware Targets" field and
the variant group that contains the firmware IDs. The "Number of
Firmware Targets" serves as the length of the variant group.

The existing logic would not take the length of the in-between
field(s) into consideration but simply assume a one-byte field
resulting in a wrong offset when trying to get the value of
"Number of Firmware Targets" during parsing.

This fix loops through any fields in between the length and the
data and includes the field lengths in the calculation of the
offset.
```

### License and Copyright in Files

All files must contain a license statement in the header in SPDX format.
If no header can be used, a parallel license file must be used, e.g., `ZatsBuild.sln.license` for `ZatsBuild.sln`.

The license statement must look like this:
```
SPDX-License-Identifier: BSD-3-Clause
```
prepended with a comment identifier that matches the format of the file.

The file header must also contain a copyright statement in SPDX format.
The default copyright statement that must be used is:
```
SPDX-FileCopyrightText: Z-Wave Alliance <https://z-wavealliance.org>
```
It is allowed to additionally add your company's original copyright to a new or changed file,
but it is not recommended to do so, as it can result in a long file header with multiple copyright holders.

### Upstream Sync and Clean Up

Prior to submitting your pull request, you might want to do a few things to clean up your branch and make it as simple 
as possible for the original repository's maintainer to test, accept, and merge your work.

If any commits have been made to the upstream main branch, you should rebase your development branch so that merging 
it will be a simple fast-forward that won't require any conflict resolution work.

```bash
# Fetch upstream main and merge with your repository's main branch
git checkout main
git pull upstream main

# If there were any new commits, rebase your development branch
git checkout <branch-name>
git rebase main
```

Now, it may be desirable to squash some of your smaller commits down into a small number of larger more cohesive commits. 
You can do this with an interactive rebase:

```bash
# Rebase all commits on your development branch
git checkout <branch-name>
git rebase -i main
```

This will open up a text editor where you can specify which commits to squash.

## Push and Test

```bash
# Checkout your branch
git checkout <branch-name>

# Push to your GitHub fork:
git push origin <branch-name>
```

This will trigger the continuous-integration checks. You can view the results
in the respective services. Note that the integration checks will report
failures on occasion.

### Configure Access Tokens with GitHub Actions

GitHub actions rely on other Z-Wave Alliance repositories and artifacts.
Since [Z-Wave development is not (yet)
public](https://github.com/Z-Wave-Alliance/OSWG/discussions/41), one can use
access tokens to allow the GitHub Actions to access other repositories.
This chapter explains how to configure GitHub Actions to access other
repositories using access tokens.

First, generate a personal access token. Click
[here](https://github.com/settings/tokens) or navigate to *Settings/Developer
settings/Personal access tokens/Tokens (classic)*, click on "Generate new
token" and select "Generate new token (classic)". On the next page, select the
"repo" scope (full control of private repositories) and click on "Generate
token" at the bottom of the page. Take note of the generated token.

Now, configure your fork with the access token. Go to the project's tab
"Settings", then *Security/Secrets and variables/Actions*. On the tab
"Secrets", click on "New repository secret". Set the "Name" to
"GH_ZWAVE_ACCESS_TOKEN" and paste the token generated in the previous step in
the field "Secret". Remove any space and newline characters.

Now you should be able to run the tests on your own fork.

## Review Requirements

### Documentation Best Practices

The Open Source Project uses Doxygen to markup (or markdown) all C, C++, Objective C, Objective C++, Perl, Python, and
Java code. Read our Doxygen Best Practices, Conventions, and Style Guide.

### Submit Pull Request

Once you've validated the CI results, go to the page for your fork on GitHub, select your development branch, and click
the pull request button. If you need to make any adjustments to your pull request, just push the updates to GitHub. Your
pull request will automatically track the changes on your development branch and update.

### Code Analysis

The Z-Wave source code is not safety certified and currently the Z-Wave Alliance has no ambitions to do any safety
certification. Therefore there is no static analysis tools in place to ensure that a PR is in compliance with a
specific safety standard.

### Merge Requirements
- Github Workflows pass
- Builds pass
- Tests pass
- Linking passes
- Code style passes

When can I merge? After these have been satisfied, a Community Leader will merge the PR into main

### Documentation

Documentation undergoes the same review process as code See the Documentation Style Guide for more information on how to
author and format documentation for contribution.

## Merge Processes

Merges require at least 2 approvals from Community Leaders, and all CI tests passing.

### Shorter Reviews

Development Lead & Vice Leads can merge a change with fewer then the required approvals have been submitted.

A separate "fast track" label will be created that will only require a single checkbox to be set, this label
shall only be set by the Development Lead, and/or Vice Lead (unless they’re both unavailable, in which case a
replacement can be temporarily appointed)

### Fast Track Types

"Day" here means "business day" (i.e. PRs on friday do not get fast-tracked faster).

#### Trivial Changes

Small changes or changes that do not affect the main functionality of the code can be fast tracked immediately. Examples:

- Adding/removing documentation (.md files)
- Adding tests (may include small reorganization/method adding/changes to enable testability):
  - certification tests
  - stability tests
  - integration tests
  - functional tests
  - Test scripts
  - Additional tests following a pattern (e.g. YAML tests)
- Adding/updating/fixing tooling to aid in development
- Re-running code generation
- Code readability refactors:
  - renaming enum/classes/structure members
  - moving constant header location
  - Obviously trivial build rule changes (e.g. adding missing files to build rules)
  - Changing comments
  - Adding/removing includes (include what you need and only what you need rules)
- Pulling new third-party repo files
- Platform vendors/maintainers adding platform features/logic/bug fixes to their own platforms
- Most changes to existing docker files (pulling new versions, reorganizing)
- Most changes to new dockerfile version in workflows

#### Fast Track Changes

Larger functionality changes are allowed to be fast tracked with these requirements/restrictions:

- Require at least 3 day to have passed since the creation of the PR
- Require at least 1 checkmark from someone familiar with the code or problem space
  - This requirement shall be dropped after a PR is 7 days old with stale or no feedback.
- Code is sufficiently covered by automated tests (or impossible to automatically test with a very
  solid reason)

Fast tracking these changes will involve resolving any obviously 'resolved' comments (judgment call
here: were they replied to or addressed) and merging the change.

Any "request for changes" marker on a PR will always be respected unless obviously resolved (i.e. author marked
"requesting changes because of X and X was done in the PR")
  - This requirement shall be dropped after a PR is 7 days old with stale or no feedback.

## Legal Info

SPDX-License-Identifier: BSD-3-Clause
SPDX-FileCopyrightText: Z-Wave Alliance <https://z-wavealliance.org>
