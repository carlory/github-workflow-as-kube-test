# github-workflow-as-kube-test

Test repository for the github-workflow-as-kube GitHub Action.

This repository contains a workflow that tests the action on various GitHub events.

## Workflow Details

The workflow file [`.github/workflows/test-action.yml`](.github/workflows/test-action.yml) triggers on:

- **Push events** to any branch
- **Pull request events** to any branch
- **Issue comment events** (created) - The action responds to slash commands like `/help`, `/woof`, `/bark` via its plugin system
- **Manual trigger** via `workflow_dispatch`
- **Scheduled** daily at midnight UTC
- **Release events** (published, edited, deleted)
- **Create/delete events** for branches/tags
- **Repository dispatch** with type `trigger-test`

The workflow uses the `carlory/github-workflow-as-kube@main` action with the `help`, `dog`, and `hold` plugins enabled.

## Supported Commands

The action supports the following slash commands when posted as issue comments:

### Help Plugin Commands

- `/help` - Adds the "help wanted" label to an issue
- `/remove-help` - Removes the "help wanted" and "good first issue" labels
- `/good-first-issue` - Adds both "good first issue" and "help wanted" labels
- `/remove-good-first-issue` - Removes the "good first issue" label

### Dog Plugin Commands

- `/woof` - Posts a random dog image
- `/bark` - Posts a random dog image
- `/this-is-fine` - Posts the "this is fine" meme

### Hold Plugin Commands

- `/hold` - Adds the "do-not-merge/hold" label to a PR, indicating it should not be merged
- `/hold cancel` - Removes the "do-not-merge/hold" label from a PR

## Labels

This repository uses automated label management via the `.github/labels.yml` file. The following labels are automatically synchronized:

- **do-not-merge/hold** - Applied by the `/hold` command to prevent a PR from being merged
- **help wanted** - Applied by the `/help` command to indicate an issue needs help from a contributor
- **good first issue** - Applied by the `/good-first-issue` command to indicate an issue is suitable for new contributors

Labels are automatically synchronized when:
- The repository is first set up
- Changes are pushed to the `.github/labels.yml` file
- The workflow is manually triggered via `workflow_dispatch`

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