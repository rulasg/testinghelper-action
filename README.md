# TestingHelper GitHub Action and Reusable Workflow

Testing is key for a healthy and effitient development process.

[TestingHelper](https://github.com/rulasg/testingHelper#readme) will help you on different faces of the developmnet lifecycle of a powershell module including testing.

This Action and Reusable Workflow are wrappers around TestingHelper testing functionality so that you can very easily test your powershell module and add it to the development flow as a PullRequest check.

The following two samples are equivalent. The first one will call the action as a step and the second one will run calling the reusable workflow.

## Calling the action

This workflow will run the action as a step to prepare the runner to run tests.

```yaml
name: Test with TestingHelper-Action

on:

  # Run as check on push request
  push:

  # Run as check on pull request
  pull_request:

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

permissions:
  # To run test we only need to read the repository
  contents: read

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

        # Setup TestingHelper for later use
      - name: Setup TestingHelper
        uses: rulasg/testinghelper-setup-action@v1
        with:
          Version: '2.0'

        # Use setup TestingHelper version to run tests
      - name: Run tests
        uses: rulasg/testinghelper-action@v1
```

## Calling the reusuable workflow

This workflow will run the reusable workflow

```yaml

name: Reusable Test Workflow
on:
  pull_request:
  workflow_dispatch:

permissions:
  # To run test we only need to read the repository
  contents: read

jobs:
  # This workflow contains a single job that will call a reusable workflow
  call-reusable-testinghelper-worfklow:
    uses: rulasg/testinghelper-action/.github/workflows/testinghelper-workflow.yaml@v1
```
