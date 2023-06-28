# Branch-Based Labeler

⚡️🔖 Automates the process of assigning labels to your pull requests based on the target branch. This action simplifies your project management by automatically categorizing your PRs, enabling you to filter and review them more efficiently.

## Features

- Automatic Label Assignment: Labels are automatically assigned to new pull requests based on the target branch, removing the need for manual labelling.
- Customizable: You can configure which labels correspond to which branches, allowing you to use in a way that suits your project's needs.
- Easy to Integrate: Simply add this action to your repository's workflow and it will start working immediately.

## Usage

To use, you'll need to add it as a step in your GitHub workflow file i.e (`.github/workflows/main.yml`), providing the necessary inputs.

```yaml
name: Assign Labels

on:
  pull_request:
    types: [opened]

jobs:
  label:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Assign labels based on target branch
        uses: shiftEscape/auto-label-pr@v1.0.0
        with:
          token: "${{ secrets.GITHUB_TOKEN }}"
          config-path: ".github/config/branch-labels.json" # JSON config file
```

> NOTE: Use this action only for **`*pull_request`** event of type **`opened`**.

## Configuration

You can configure this by creating a JSON configuration file (i.e `.github/config/branch-labels.json`) in your repository. In this file, you define the labels that should be added to pull requests for each branch. Here's a sample configuration:

```json
{
  "master": "🚀 Production Deployment",
  "staging": "🚀 UAT Deployment",
  "development": "🚀 SIT Deployment"
}
```

In the example above, when a `Pull Request` is made to `master`, `🚀 Production Deployment` label will be assigned to that PR and so on and so forth.
