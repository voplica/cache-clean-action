### Self-Hosted Runner Cache Clean Action

This build action allows to trigger clean for self-hosted cache used by self-hosted GitHub runners. 
It triggers cache clean-up for a branch which was deleted, archived, or for which any of the PRs were closed.

Parameters:
- `dispatch_token` (**Required**, *string*) - Token used for a workflow dispatch. Should be `$GH_BUILDS_WORKFLOW_DISPATCH_TOKEN`.
- `gh_hosted_token` (*string*) - Token for GitHub hosted Cache to clean up. Should be: `$GITHUB_TOKEN`. If not present then GitHub
  hosted cache cleanup is skipped and only self-hosted cache will be cleaned up. Ensure proper permissions are set for the workflow. 

Example:
```yaml
name: Cleanup Branch Cache
permissions:
  contents: write
  actions: write
  pull-requests: write
on:
  pull_request:
    types:
      - closed
  delete:
    branches:
      - '*'
  repository_dispatch:
    types:
      - branch_archived

jobs:
  build:
    runs-on: "ubuntu-latest"
    steps:
      - name: Trigger cache cleanup for a branch
        uses: voplica/cache-clean-action@v1.2.0
        with:
          dispatch_token: "${{ secrets.GH_BUILDS_WORKFLOW_DISPATCH_TOKEN }}"
          gh_hosted_token: "${{ secrets.GITHUB_TOKEN }}"
```

###### © 2025 Voplica LLC
