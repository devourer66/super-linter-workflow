# Super Linter Reusable Workflow Examples

[![Lint all the codes](https://github.com/BretFisher/super-linter-workflow/actions/workflows/super-linter.yaml/badge.svg)](https://github.com/BretFisher/super-linter-workflow/actions/workflows/super-linter.yaml)

The GitHub [Super-Linter](https://github.com/marketplace/actions/super-linter) project is a fantastic way to lint all your file types with a single GitHub Actions Workflow. A great way to implement it everywhere is to use GHA's [Reusable Workflows](https://docs.github.com/en/actions/learn-github-actions/reusing-workflows) (see below).

[My video walkthrough of this repository](https://youtu.be/aXZgQM8DqXg)

## Features of this custom Super-Linter example

- All the features of [Super-Linter](https://github.com/marketplace/actions/super-linter) in a *Reusable* Workflow
- Bonus: Optionally turn off non-DevOps linters (CSS, JS, HTML, etc.) when you want to ignore code (in my case it's to ignore sample code I stick in DevOps projects)
- Bonus: I added Job steps to correctly determine which branch to diff files with (in the case of having multiple release branches)
- Bonus: Lints only changed files on a PR, but lints all files on merge to main (or any release) branch

## How to reuse this example as a *Reusable* Workflow

1. Fork this repository for you to customize your linters
2. Add a workflow to all your other repositories that calls your linter workflow using GitHub's "Reusable Workflow"
3. Add something similar to this to those workflows:

```yaml
---
name: Lint Code Base

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  call-super-linter:
    # use Reusable Workflows to call my linter config remotely
    # https://docs.github.com/en/actions/learn-github-actions/reusing-workflows
    #FIXME: customize uri to point to your forked linter repository
    uses: bretfisher/super-linter-workflow/.github/workflows/super-linter.yaml@main
```

## How to run Super-Linter locally

Option 1: Use [nektos/act](https://github.com/nektos/act) to run an existing GitHub Action workflow on your local repository clone.

Option 2: Use Docker to [run the Super-Linter image directly](https://github.com/github/super-linter/blob/main/docs/run-linter-locally.md).
