# Root Access is deliberately not managed by Terraform

Everything in the Tenancy is a Managed Resource except Root Access: the built-in Administrators group, its root policy and the Break-glass Admin. Without this exception, a bad `apply`, or a compromised CI identity applying a malicious change, could remove the only human route back into the Tenancy. That exception matters more than a strictly "everything in code" Tenancy.
