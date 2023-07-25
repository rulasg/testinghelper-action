# testinghelper-action

GitHub Action to test PowerShell modules using TestingHelper from GitHub.

The following two samples calling the action and the reusable workflow are equivalent.


## Calling the action

This workflow will run the action as a step.


```yaml
name: Test with TestingHelper-Action

# Controls when the workflow will run
on:

  # Run as check on pull request
  pull_request:

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

permissions:
  # To run test we only need to read the repository
  contents: read

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  test:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v3

      # Runs a single command using the runners shell
      - uses: rulasg/testinghelper-action@v1
```

## Calling the reusuable workflow

This workflow will run the reusable workflow

```yaml

name: Reusable Test Workflow

# Controls when the workflow will run
on:

  # Run as check on pull request
  pull_request:

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

permissions:
  # To run test we only need to read the repository
  contents: read

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  call-reusable-testinghelper-worfklow:
    # The type of runner that the job will run on
    uses: rulasg/testinghelper-action/.github/workflows/testinghelper-workflow.yaml@v1
```
