---
title: "Software Development Strategy - Monorepo vs. Polyrepo"
tags:
  - Software Development Life Cycle
  - Software Development Strategy
  - Monorepo
  - Polyrepo
---

## Introduction

### What is monorepo?

Monorepo (syllabic abbreviation of monolithic repository) is a nickname that means "using one repository for the source code management version control system (VCS)".

Advantages of monorepo:
* Ease of code reuse
* Simplified dependency management
* Atomic commits
* Large-scale code refactoring
* Coherence codebase
* Cheap workflows

Limitations of monorepo:
* Loss of version information per project
* Lack of per-project security (Not an issue with code owners by github)
* More storage needed (Not an issue with SVN)
* Long build time

Proponents of monorepo:
* If components need to release together, then use a monorepo.
* If components need to share common code, then use a monorepo.
* In less-mature, high-churn codebase, use a monorepo.

#### Monorepo Scaling Problem

Monorepo scaling becomes a problem when a typical developer can't work well with the code by using typical tools such as vanilla git.

Monorepo scaling seems to become an issue, in pratice, at approximately these kinds of metrics:
* 10 - 100 developers writing code full time.
* 10 - 100 projects in progress at the same time.
* 10 - 100 packaging processes during the same time period.
* 1K - 10K lines of code
* 1K - 10K versioned dependencies

Monorepo scaling can be improved by:
* Some type of virtual file system (VFS) that allows a portion of the code to be present locally.
* Sophisticated source code indexing/searching/discovery capabilities as a service.
* Git's commands to clone repo with a very long history:
  - git shallow clone
  - git filter-branch
  - git clone only one branch

### What is polyrepo?

Polyrepo (syllabic abbreviation of poly repository) is a nickname that means "using multiple repositories for the source code management version control system (VCS)".

Advantages of polyrepo:
* Strict isolation of components
* Quickly build independent components
* Short build time

Limitations of polyrepo:
* Large-scale code refactoring
* Dependency hell (Diamond dependency problem)
* Multiple pull request for a feature
* Onboarding junior developer

Proponents of polyrepo:
* At scale, a monorepo must solve every problem that a polyrepo must solve, with the downside of encouraging tight coupling, and the additional herculean effort of tackling VCS scalability
* Coupling between unrelated projects
* Visible organization

## Comparisons

### Key similarities

Both architectures ultimately track the same source code files, and do it by using source code management (SCM) version control systems (VCS) such as git or mercurial.

### Key differences

<table>
  <thead>
    <tr>
      <th></th>
      <th>Monorepo</th>
      <th>Polyrepo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Contents</th>
      <td>Typically a repo contains multiple projects, programming languages, packaging processes, etc.</td>
      <td>Typically a repo contains one project, programming language, packaging process, etc.</td>
    </tr>
    <tr>
      <th>Projects</th>
      <td>Manages projects in one repository, together, holistically.</td>
      <td>Manages projects in multiple repositories, separately, independently.</td>
    </tr>
    <tr>
      <th>Workflows</th>
      <td>Enables workflows in all projects simultaneously, all within the monorepo. </td>
      <td>Enables workflows in each project one at a time, each in its own repo.</td>
    </tr>
    <tr>
      <th>Changes</th>
      <td>Ensures changes affect all the projects, can be tracked together, tested together, and released together.</td>
      <td>Ensures changes affect only one project, can be tracked separately, tested separately, and released separately.</td>
    </tr>
    <tr>
      <th>Collaboration</th>
      <td>Encourages collaboration and code sharing within an organization. </td>
      <td>Encourages collaboration and code sharing across organizations.</td>
    </tr>
    <tr>
      <th>Testing</th>
      <td>Good white box testing because all projects are testable together, and verifiable holistically.</td>
      <td>Good black box testing because each project is testable separately, and verifiable independently.</td>
    </tr>
    <tr>
      <th>Releases</th>
      <td>Coordinated releases are inherent, yet must use a polygot of tooling.</td>
      <td>Coordinated releases must be programmed, yet can use vanilla tooling.</td>
    </tr>
    <tr>
      <th>State</th>
      <td>The current state of everything is one commit in one repo.</td>
      <td>The current state of everything is a commit per repo.</td>
    </tr>
    <tr>
      <th>Coupling</th>
      <td>Tight coupling of projects.</td>
      <td>No coupling of projects.</td>
    </tr>
    <tr>
      <th>Thinking</th>
      <td>Encourages thinking about conjoins among projects.</td>
      <td>Encourages thinking about contracts between projects.</td>
    </tr>
    <tr>
      <th>Access</th>
      <td><p>Access control defaults to all projects.<p>Some teams use tools for finer-grained access control.<p>Gitlab offers ownership control where you can say who owns what directories for things like approving merge requests that affect those directories. Google Piper has finer-grained access control. Phabricator offers herald rules that stop a merge from happening if a file has changed in a specific subdirectory. Some teams use service owners, so when a change spans multiple services, they are all added automatically as blocking reviewers.</td>
      </td>
      <td><p>Access control defaults per project.<p>Some teams use tools for broader-granted access control.<p>GitHub offers teams where you can say one team owns many projects and for things like approving requests that affect multiple repos.</td>
    </tr>
    <tr>
      <th>Scaling</th>
      <td>Scaling needs specialized tooling. It is currently not practical to use vanilla git with very large repos, or very large files, without any extra tooling. For monorepo scaling, teams invest in writing custom tooling and providing custom training.</td>
      <td>Scaling needs specialized coordination. It is currently not practical to use vanilla git with many projects across many repos, where a team wants to coordinate code changes, testing, packaging, and releasing. For polyrepo scaling, teams invest in writing coordination scripts and careful cross-version compatibility.</td>
    </tr>
    <tr>
      <th>Tooling</th>
      <td>Google wrote the tool “bazel”, which tracks internal dependencies by using directed acyclic graphs.</td>
      <td>Lyft wrote the tool “refactorator”, which automates making changes in multiple repos, including opening PRs, tracking status, etc.</td>
    </tr>
  </tbody>
</table>

## Tips to handle polyrepo in companies

### A single top level repo

Sorting the signal from the noise can be accomplished by managing a top level repo that allows users to start from a single place.

This is extremely useful for new starters, but also for ongoing meta-management of your local environment.

I would recommend doing git clones for this. People may jump into the idea of using Git submodules or similar which will end up biting you in the future.

### Templates

The problem you will have as the number of repositories grows is your ability to rapidly roll out changes.

Use templates as a solution that enables you to raise a single pull request, test it, and then instantly copy that change over all existing repos.

Consistency is key. Templates should contain the skeleton of the directory structure of a new repo. Plus, define a standardised build workflow for that template type.

### CI in a PR

99% of your CI workflow should happen when somebody opens a pull request.

A pull request opens, tests happen, this results in a green tick against the PR in Github. Somebody can now review the code with the assurance that at least some tests passed.

### Code Owners

Code Owners, as defined in a `CODEOWNERS` file in the root of each repo, should contain one or more people who are aware of the context behind the repository being created in the first place.

They are aware of what should and should not be put into the repository and how it fits into the greater system. This is a tricky thing to articulate but without this filtering layer you end up with some code being put into completely the wrong repo. With enough code going into the wrong place you end up with tightly coupled systems and a distributed monolotith.

A good code review involves somebody reviewing the code itself. Plus a code owner giving a quick review of the intent behind the pull request.

A secondary useful purpose is to help new people reach out to somebody more knowledgeable. In larger teams it helps to look up the code owner for a repo and reach out to them on chat. Ideally this would happen for some quick guidance before work is started to avoid closed PR's with requests the code move elsewhere.

### Versioning

For simplicity this is exclusively git tags on master.

This should be standardised as part of the template and often it's identical across templates.

Versioning each repository individually allows for dependency management between repositories.

### Automated Pull Requests

People generally don't remember where dependencies are used. Event if they do, or there is well maintained readme of what to do next after your PR is merged, people forget.

Example of an API that our CI system curls after success and versioning.

The API has logic to automatically determine which other repositories use the repository just updated. It then automatically raises a pull request against each.

The PR will be a simple versioning bump. It also carries across the original pull request title and description, as well as appending the repo it originated from.

### Deployable modules

Not everything repo gets deployed directly as most are simply for dependencies.

To correctly integration test and release these as a tested unit these need to be bundled up into a single release version. Often this is done by storing these versions behind an API. Then integrating this into a release pipeline.

Not many CI/CD systems are designed for this. Jenkins has some plugins that allow for fan-in/fan-out across multiple repos.

### An Environement repo

A single repository used for environment configuration. With a directory structure that's easy to browse and initiate deployments from.

This allows for a single command whole environment creation and upgrades via terragrunt apply-all for example.

**Resources**:

- [Monorepo](https://en.wikipedia.org/wiki/Monorepo)
- [Monorepo vs. polyrepo](https://dzone.com/articles/microservices-difference-between-mono-repo-and-mul?fromrel=true)
- [Monorepos: Please do!](https://medium.com/@adamhjk/monorepo-please-do-3657e08a4b70)
- [Monorepos: Please don't!](https://medium.com/@mattklein123/monorepos-please-dont-e9a279be011b)
- [Monorepos and the Fallacy of Scale](https://presumably.de/monorepos-and-the-fallacy-of-scale.html)
- [Advantages of monorepos](http://danluu.com/monorepo/)
- [big-repositories](https://medium.com/@alessiopieruccetti/the-importance-of-making-meaningful-commits-fd68e869f185)
- [Tips for multi-repo companies](https://www.linkedin.com/pulse/tips-multi-repo-companies-steven-acreman/)
