# Dokploy Host is sized to the Always Free A1 allowance; Workloads build off-host

The Dokploy Host is a single `VM.Standard.A1.Flex` instance with 2 OCPU and 12 GB of memory, which is the post-2026 Always Free A1 allowance (see ADR 0003). It has a 50 GB boot volume and a 150 GB data volume, which together use up the 200 GB block storage allowance. The data volume holds all Dokploy and Workload state, so the instance itself can be replaced at any time.

This size only works if Workloads with a build step (Next.js and similar) build their images in their own repository's CI, push them to GHCR, and Dokploy only pulls and runs them. Building on the host would starve a running Minecraft server of CPU and memory. A 4 GB swap file on the boot volume protects against occasional out-of-memory kills.

## Consequences

- No block storage is left for the two Always Free AMD micro instances, so their quota is capped at 0.
- Only one Minecraft server is expected to run at a time.
- Moving to 4 OCPU / 24 GB is a resize (stop and start), not a rebuild. Whether a pay-as-you-go tenancy still gets 4/24 free is unconfirmed (Oracle's docs contradict each other), and we chose to settle it from the real bill, not by asking Oracle support. The process is: raise the A1 quota and the shape together in one PR, run for about 72 hours, then check Cost Analysis. If the A1 lines are $0, record a new ADR that moves the Always Free Envelope's A1 limit to 4/24. If not, revert. The worst case is roughly $3.
