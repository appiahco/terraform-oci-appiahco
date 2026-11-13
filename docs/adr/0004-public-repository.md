# This repository is public

The `appiahco` GitHub organization is on the free plan. In private repositories on that plan, Environments, environment secrets, required reviewers, branch-restricted deployments and rulesets are unavailable, so the admin-equivalent `manage` credentials could not be gated. Making the repository public gives us all of these for free. In return, nothing sensitive may ever be committed: secrets, OCIDs, the Object Storage namespace and IP allowlists come from GitHub Actions secrets or variables, state lives only in the private OCI bucket, and sensitive values are marked `sensitive` so `plan` output posted to PRs stays masked.

## Considered Options

- Private repo with ungated secrets: any workflow on any branch could read the `manage` key.
- GitHub Team (about $4 per user per month): rejected to keep the whole setup free.
