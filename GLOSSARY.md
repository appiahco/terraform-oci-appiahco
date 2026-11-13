# OCI Tenancy

The appiahco Oracle Cloud tenancy, managed as code from this repository, and the self-hosted platform it provides for running web apps, databases and game servers.

## Language

### Tenancy and ownership

**Tenancy**:
The Oracle Cloud account named `appiahco` (home region `us-ashburn-1`) and everything in it. Its root compartment is also called `appiahco`.
_Avoid_: Account, cloud, environment

**Managed Resource**:
Any resource in the Tenancy whose desired state is declared in this repository. Anything in the Tenancy that is neither a Managed Resource nor part of the Root Access is drift.
_Avoid_: Terraformed resource, IaC resource

**Root Access**:
The tenancy's built-in Administrators group, its root policy and the Break-glass Admin. Deliberately left out of this repository, so no change here can lock the owner out.
_Avoid_: Admin stuff, root

**Break-glass Admin**:
The human user in Root Access who is used only to bootstrap the Tenancy or to recover it when automation is broken.
_Avoid_: Root user, owner account

**Bootstrap**:
The one-time, human-run step that creates what the automation needs before it can run itself: the state store and the CI identity.
_Avoid_: Setup, init

### Cost

**Always Free Envelope**:
The set of Oracle's Always Free resource limits. The Tenancy is pay-as-you-go but is kept inside this envelope unless a decision explicitly says otherwise.
_Avoid_: Free tier (that's an account type, not a limit set)

**Guardrail**:
A Managed Resource whose only job is to stop the Tenancy leaving the Always Free Envelope or to warn when it does, such as a quota or a budget alert.
_Avoid_: Limit, policy (overloaded with IAM policy)

### Platform

**Dokploy Host**:
The single compute instance running Dokploy, the self-hosted platform on which Workloads are deployed.
_Avoid_: Server, VM, box, node

**Data Volume**:
The persistent block volume attached to the Dokploy Host that holds all Dokploy and Workload state. The Dokploy Host can be thrown away and rebuilt; the Data Volume cannot.
_Avoid_: Disk, storage, block volume (too generic)

**Workload**:
Anything deployed onto the Dokploy Host through Dokploy (a web app, a database or a game server). Workloads are not Managed Resources: Dokploy is their source of truth.
_Avoid_: App, service, deployment
