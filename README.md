# Yoast Community Health

## Community Health

Default [community health files] for all repositories in this organisation.

* [SECURITY](SECURITY.md)

Individual repositories can overrule the default file(s) by committing their own version of one or more of these files to the repository in question.

Additional community health files may be added over time and/or when GitHub adds support for them.


## Re-usable workflows

Aside from the community health files, this repository also offers a number of re-usable GitHub Actions workflows.

### Available re-usable workflows

The following re-usable workflows are available:
* [`reusable-actionlint.yml`][reusable-actionlint] which runs a [static analysis check][actionlint] on GitHub Actions workflow files only.
    **Inputs**:
    - `shellcheck`: Optional. Whether to enable shellcheck. Defaults to 'true'.
    - `pyflakes`: Optional. Whether to enable pyflakes. Defaults to 'true'.
    - `args`: Optional. Command line arguments to pass to the actionlint command. Defaults to no arguments.

* [`reusable-merge-conflict-check.yml`][reusable-mergeconflict] to check whether open PRs are in a merge conflict state.
    **Inputs**:
    - `dirtyLabel`: Optional. Name of the label which indicates that the branch is dirty. Defaults to 'merge conflict'.
    - `removeOnDirtyLabel`: Optional. Name of the label which should be removed. Defaults to none.
    - `commentOnDirty`: Optional. Comment to add when the pull request is conflicting. Supports markdown.
        Defaults to: _"A merge conflict has been detected for the proposed code changes in this PR. Please resolve the conflict by either rebasing the PR or merging in changes from the base branch."_.
    - `commentOnClean`: Optional. Comment to add when the pull request is not conflicting anymore. Supports markdown.
        Defaults to _no comment_.


## A .github repository with versioning ?

While it may be uncommon for a `.github` repository to contain tags, the tags are to allow workflows in repositories which _use_ the above mentioned re-usable workflows to "pin" to a specific version of a workflow in a way that Dependabot can still update them.

This has two benefits:
1. **Stability**  
    A change in the re-usable workflow itself, or in an action runner used by a re-usable workflow, can "break" builds.
    Pinning and letting Dependabot update these pins prevents these type of "unmanaged" CI breaks.
2. **Security**
    With commit-hash pinned workflows, the dependencies used are fixed to specific versions and updates are managed, which means that it is more difficult for an attacker to be able to infiltrate the workflow runs and get access to secrets and/or cause other havoc.

> [!IMPORTANT]
> It is best practice for tags for repositories which will be used in GitHub Actions workflows to be prefixed with `v` before the version number, so tags in this repository should start with a `v` prefix too.


[community health files]:  https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file

[reusable-actionlint]:     https://github.com/Yoast/.github/blob/main/.github/workflows/reusable-actionlint.yml
[actionlint]:              https://github.com/rhysd/actionlint

[reusable-mergeconflict]:  https://github.com/Yoast/.github/blob/main/.github/workflows/reusable-merge-conflict-check.yml
