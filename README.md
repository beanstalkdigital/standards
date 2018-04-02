# Introduction
Below is the git workflow and conventions to use when developing. If anything is not clear or requires more explination, create an issue describing what needs to be improved.

## Table of Contents
- [Git Flow](#git-flow)
  - [Branches](#branch-naming)
    - [Feature Branches](#feature-branches)
    - [Hotfix Branches](#hotfix-branches)
    - [Releast Branches](#release-branches)
  - [Changelog](#changelog)
  - [Pull Requests](#pull-requests)
  - [Labels](#labels)
- More To Come...

# Git Flow
The following clearly outlines the various processes and rules for using Git in conjunction with Github on any development project.
## Branches
There are two main branches; `develop` and `master`. The default branch of a repo is set to `master` for showing what code is active upon first load of the repo.

This is important to note, because when you try to make a pull request for your branch it will default to going into `master`. Which may not be the correct branch for your PR (90% of the time this is the case).

Different branch types are broken out and described below so one understands what branching convention to use for every scenario.

_Note_
You may notice the use of `/` in alot of the branching conventions. The reason behind that is if you are using a git GUI program (i.e. Tower, or Git for Desktop) the `/` act as folders in the visual represation of the repo. An example of this is shown below.

![Example](https://cl.ly/3t1W113F3i2n/Image%202018-04-02%20at%203.30.58%20PM.png)

### Feature Branches
Feature branches are for, as the name implies, developing a new feature for the code base. If you are writing new code to the code base odds are it will be in a feature branch. This is the primary branch that will get used most often.

**Pull Requests**
These branches are to be based off of `develop` and their cooresponding PR will subsiquently get `Squash Merged` (affectionatly known as "squerging") into the `develop` branch. The reason for squerging here is that all of the commits you made on a specific feature get condensed into a tidy singular commit.

**Naming Convention**
`feature/three-letter-initials/branch-name`
Example - `feature/jjs/homepage-design`

### Hotfix Branches
Hotfix branches are for patching code. They fall under code changes that aren't big enough to be a feature. But they are still code changes that have to be made.

**Important** - Once a hotfix branch has been merged into `master` you must rebase the `develop` branch off of `master` or you will have terrible merge conflicts.

**Pull Requests**
99.9% of the time these branches will be based off of `master` as they are primarly used for fixing bugs or errors that are found on production. However, there are cases where a hotfix branch can be based off of `develop` for fixing a small bug that a new feature introducted into the code base. The PR that is attached to this type of branch will get `Merged` into its branch. The reason for this is we want to have the commit history for the commits that were made (As they are mostly done on `master`).

**Naming Convention**
`hotfix/three-letter-initials/branch-name`
Example - `hotfix/jjs/caching-bug`

### Release Branches
These branches are the only way new feature branches get into the `master` branch. These branches will be the ones that get deployed to a staging server for testing. But only if a staging server and auto deploys exist for the current project.

You are allowed to make commits to this branch just like you would a feature. As the primary goal of this branch is to catch any bugs before code gets into `master`.

**Important** - Once a release branch has been merged into `master` you must rebase the `develop` branch off of `master` or you will have terrible merge conflicts.

**Pull Requests**
These branches will be based off of `develop` and the PR associated with this branch gets `Merged` into the `master` branch. The reason we merge here is so we have a record of all of the features and any commits that were made once they go into `master`

**Naming Convention**
`release/YYYYMMDD`
Example - `release/20180613`

## Changelog
Every repo should have a `CHANGELOG.md` at its' root directory. If the file doesn't exist, well, you're in luck cause you should make one for the repo! The format of a changelog based on [keepachangelog.com](http://keepachangelog.com/).

The purpose for keeping a changelog is, as the name implies, to have a easily accesible historical record of everything that has gone on in a repo.

_Note_: Your PR will not get squerged or merged without a changelog entry.

**Changelog Template**
```
# Change Log
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/)

## Unreleased
### Pull Requests
- [Pull Request Title Here](https://github.com/(org)/repo-name/pull/pull-request-number)

### (Added|Changed|Fixed)
- Things were done. They were nice. @github-handle
```

## Pull Requests
Every pull request (PR) should contain documentation as to what the code does and or fixes. It should include pictures if relevant (i.e. if any design changes or made). A checklist has been included below of all of the steps that should be done before a PR is created.

_PR Creation Checklist_
- [ ] Base branch is correct (`develop` or `master`)
- [ ] You assigned yourself to the PR
- [ ] Appropriate reviewers have been requested
- [ ] Accurate description and images are attached
- [ ] Appropriate labels are attached (See [labels](#labels))

A PR is required to have a completed review by one or more developer(s) and any status checks that are performed. Like automated testing, deploys, etc. Once a PR has been approved and reviewed it is good to be squerged or merged.

_Example of a Good PR_
![Good PR](https://cl.ly/272K1k1p2L2E/Image%202018-04-02%20at%204.25.02%20PM.png)

_Example of a Bad PR_
![Bad PR](https://cl.ly/3E1x062I3U1D/Image%202018-04-02%20at%204.27.19%20PM.png)

## Labels
Below are a list of all of the labels that should exist on a repo. These are useful for a busy repo that has alot of pull request to get a pulse on what the state of each PR is in the PR list view. _If the labels don't exist on the repo they should be added_

_Note_ - You should only use one label out of each category below. (i.e. You wouldn't have a label of **Status: Blocked** and of **Status: In Progress**)
### Status

![Status: Blocked](https://cl.ly/0y2b0H0v0o2U/download/Image%202018-04-02%20at%204.35.10%20PM.png)
If this PR is blocked by something. _a comment or note about why the PR is on hold is required._

![Status: In Progress](https://cl.ly/410f0J371D3n/download/Image%202018-04-02%20at%204.36.01%20PM.png)
When the code is still being working on that relates to this PR.

![Status: On Hold](https://cl.ly/0w1V0k3O3B0d/download/Image%202018-04-02%20at%204.36.33%20PM.png)
When the PR is waiting for something to be completed. _a comment or note about why the PR is on hold is required._

![Status: Review Required](https://cl.ly/1n2a0Z2m2U01/download/Image%202018-04-02%20at%204.38.00%20PM.png)
When a PR requires another party's review before completion.

![Status: Revision Required](https://cl.ly/340M1g0y2C3F/download/Image%202018-04-02%20at%204.38.24%20PM.png)
When a PR has been reviewed and changes are needed by the PR owner.

### Priority

![Priority: Code Red](https://cl.ly/1v2C0r223t2X/Image%202018-04-02%20at%204.32.13%20PM.png)
If the PR is absolutely mission critical, i.e. look at this down or else everything is broken

![Priority: High](https://cl.ly/382p1U2U0b2E/download/Image%202018-04-02%20at%204.32.39%20PM.png)
If the PR is fairly critical but the project could continue working without having this right away.

![Priority: Medium](https://cl.ly/063r3I0b1o39/download/Image%202018-04-02%20at%204.32.59%20PM.png)
If the PR is semi important but not urgent by any means.

![Priority: Low](https://cl.ly/3Y1k021F112f/download/Image%202018-04-02%20at%204.33.19%20PM.png)
If the PR can wait a while until it is looked at and won't hurt anything by having it sit for a while.
