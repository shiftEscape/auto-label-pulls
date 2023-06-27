# Branch-Based Labeler

A GitHub action that automates the process of assigning labels to your pull requests based on the target branch. This action simplifies your project management by automatically categorizing your PRs, enabling you to filter and review them more efficiently.

## Features

- Automatic Label Assignment: Labels are automatically assigned to new pull requests based on the target branch, removing the need for manual labelling.
- Customizable: You can configure which labels correspond to which branches, allowing you to use `BranchBasedLabeler` in a way that suits your project's needs.
- Easy to Integrate: Simply add this action to your repository's workflow and it will start working immediately.

## Usage

To use, you'll need to add it as a step in your GitHub workflow file i.e (`.github/workflows/main.yml`), providing the necessary inputs.

```yaml
name: Assign Labels

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  label:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Assign labels based on target branch
        uses: shiftEscape/branch-based-labeler@v1
        with:
          repo-token: "${{ secrets.GITHUB_TOKEN }}"
          configuration-path: ".github/labeler-config.yml" # configuration file
```

## Configuration

You can configure this by creating a configuration file (like `.github/labeler-config.yml`) in your repository. In this file, you define the labels that should be added to pull requests for each branch. Here's a sample configuration:

```yaml
master:
  - label1
  - label2

develop:
  - label3
  - label4
```

In the example above, when a pull request is made to `master`, `label1` and `label2` will be added to the PR. If a PR is made to `develop`, `label3` and `label4` will be added.
