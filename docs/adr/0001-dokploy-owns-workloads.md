# Terraform stops at the Dokploy Host; Dokploy owns Workloads

This repository is the source of truth for the Tenancy's infrastructure, up to and including a Dokploy Host that is installed and ready to use. Workloads (web apps, databases, game servers) are created and managed in Dokploy, which is their source of truth. They are not declared here. We chose this over managing Dokploy projects and apps through a community Terraform provider or its API because those providers are immature, and having two sources of truth for Workloads would guarantee drift.

## Consequences

- Rebuilding the Tenancy from this repository gives you an empty Dokploy. Recovering Workloads depends on the Dokploy Host's persistent data surviving (or being backed up), not on this repository.
