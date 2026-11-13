# Pay-as-you-go Tenancy, held inside the Always Free Envelope by Guardrails

The Tenancy is upgraded to pay-as-you-go so that it gets priority for Ampere A1 capacity in `us-ashburn-1`. It is still treated as if it were an Always Free tenancy: Guardrails (compartment quotas capped at the Always Free limits and a near-zero budget alert) turn an accidental paid resource into a failed `apply` or an alert, not a bill. Going beyond the Always Free Envelope needs an explicit decision recorded here.

## Consequences

- In mid-2026 Oracle halved the Always Free A1 allowance to 1,500 OCPU-hours and 9,000 GB-hours a month (2 OCPU / 12 GB). Its docs disagree about whether paid tenancies still get the old 3,000 / 18,000. We plan against the smaller number (2 OCPU / 12 GB), so a later clarification from Oracle can only give us headroom, never a bill.
- Whether idle-instance reclamation applies to pay-as-you-go tenancies is unconfirmed. Do not rely on being exempt.
