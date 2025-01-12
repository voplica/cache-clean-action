### Self-Hosted Runner Cache Clean Action

This build action allows to trigger clean for self-hosted cache used by self-hosted GitHub runners. 

Parameters:
- `repository` (**Required**, *string*) - Organization + Repository name. Format: `${org}/${repo}`.
- `branch` (**Required**, *string*) - Branch name for which the cache cleanup is triggered.
- `dispatch_token` (**Required**, *string*) - Token used for a workflow dispatch. Should be `$GH_BUILDS_WORKFLOW_DISPATCH_TOKEN`.

Example:
```yaml
name: Cleanup caches by a branch
on:
  pull_request:
    types:
      - closed

jobs:
  build:
    runs-on: "ubuntu-latest"
    steps:
      - name: Trigger cache cleanup for a branch
        uses: voplica/cache-clean@v1.0.0
        with:
          repository: "${{ github.repository }}"
          branch: "${{ github.ref_name }}"
          dispatch_token: "${{ secrets.GH_BUILDS_WORKFLOW_DISPATCH_TOKEN }}"
```

###### © 2025 Voplica LLC
