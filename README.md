### Self-Hosted Runner Cache Clean Action

This build action allows to trigger clean for self-hosted cache used by self-hosted GitHub runners. 
It triggers cache clean-up for a branch which was deleted, archived, or for which any of the PRs were closed.

Parameters:
- `dispatch_token` (**Required**, *string*) - Token used for a workflow dispatch. Should be `$GH_BUILDS_WORKFLOW_DISPATCH_TOKEN`.

Example:
```yaml
name: Cleanup Branch Cache
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
        uses: voplica/cache-clean-action@v1.1.0
        with:
          dispatch_token: "${{ secrets.GH_BUILDS_WORKFLOW_DISPATCH_TOKEN }}"
```

###### © 2025 Voplica LLC
