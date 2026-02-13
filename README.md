# github-workflow-as-kube-test

Test repository for the github-workflow-as-kube GitHub Action.

This repository contains a workflow that tests the action on various GitHub events.

## Workflow Details

The workflow file [`.github/workflows/test-action.yml`](.github/workflows/test-action.yml) triggers on:

- **Push events** to any branch
- **Pull request events** to any branch
- **Issue comment events** (created) - allows responding to dog commands like `/woof`, `/bark`, `/this-is-fine`, etc.
- **Manual trigger** via `workflow_dispatch`
- **Scheduled** daily at midnight UTC
- **Release events** (published, edited, deleted)
- **Create/delete events** for branches/tags
- **Repository dispatch** with type `trigger-test`

The workflow uses the `carlory/github-workflow-as-kube@main` action with the required `milliseconds` input set to 1000.

## Triggering via Repository Dispatch

To trigger the workflow from an external service (like another repository), use the GitHub API:

```bash
curl -X POST \
  -H "Authorization: token <GITHUB_TOKEN>" \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/carlory/github-workflow-as-kube-test/dispatches \
  -d '{"event_type": "trigger-test"}'
```

## Repository URL

https://github.com/carlory/github-workflow-as-kube-test