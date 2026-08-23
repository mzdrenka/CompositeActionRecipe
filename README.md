# Composite Action Recipe

An example composite GitHub Action prepared for GitHub Marketplace publication.

## What this action does

- greets the selected user,
- exposes the `answer` output with the value `42`,
- can post a thank-you comment when a new issue is opened.

## Requirements and permissions

This action uses `actions/github-script@v6`.

If you want to use the issue-commenting behavior, your workflow must include:

```yaml
permissions:
  issues: write
```

If you only need the greeting and output behavior, no extra permissions are required.

## Usage

### Basic example

```yaml
name: Example

on:
  workflow_dispatch:

jobs:
  demo:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - id: recipe
        uses: mzdrenka/CompositeActionRecipe@v1
        with:
          who-to-greet: "@mateusz"

      - run: echo "Answer: ${{ steps.recipe.outputs.answer }}"
```

### Use on newly opened issues

```yaml
name: Thank issue reporter

on:
  issues:
    types: [opened]

jobs:
  thank-reporter:
    runs-on: ubuntu-latest
    permissions:
      issues: write
    steps:
      - uses: mzdrenka/CompositeActionRecipe@v1
        with:
          who-to-greet: "${{ github.actor }}"
```

## Inputs

| Name | Required | Default | Description |
| --- | --- | --- | --- |
| `who-to-greet` | yes | `Świat` | Name or handle of the person to greet |

## Outputs

| Name | Description |
| --- | --- |
| `answer` | Returns the value `42` |

## Versioning and publication

Before publishing in GitHub Marketplace:

1. make sure the repository is public,
2. create a release such as `v1.0.0`,
3. add a stable major tag such as `v1`,
4. reference the action as `mzdrenka/CompositeActionRecipe@v1`.

This repository already includes `action.yml`, so after the description, release, and tags are ready, it can be listed in Marketplace as a GitHub Action.