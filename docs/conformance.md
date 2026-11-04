# Conformance Checklist

*Informative summary of the MUST requirements in [SPEC.md](../SPEC.md). A declaration, determination or record that fails any item is non-conforming.*

## Question (SPEC 3)
- [ ] Presented only as the answer to: Does the efficacy still hold over time?
- [ ] Never described as verification, validation, attestation, assurance or testing

## Claim Declaration (SPEC 4)
- [ ] Registered and anchored before any evidence measured against its limits is produced; referenced records registered before it
- [ ] Subject, Declarant and interest, funding tier, Sponsor, validity period
- [ ] Declares: The Persistence Span and the epoch cadence
- [ ] Declares: The minimum rates per epoch and the Drift Tolerances
- [ ] Declares: The minimum number of valid epochs and the maximum gap between epochs
- [ ] Limits unchanged after registration
- [ ] Publication commitment

## Evidence (SPEC 5)
- [ ] Basis: PP-SPEC-077 Production Stream Mode clutches
- [ ] Basis: Silent Drift events
- [ ] Basis: DUT Fingerprint history
- [ ] Every basis record Conformant and Registered
- [ ] No measured-party logs, consoles, alerts, receipts or reports used

## Determination (SPEC 6)
- [ ] Exactly one of `proven`, `refuted`, `insufficient`
- [ ] `refuted` takes precedence over `insufficient`
- [ ] Computed from the declaration and basis records alone
- [ ] `insufficient` never presented as a result

## Scope and expiry (SPEC 7)
- [ ] Scope stated exactly as declared
- [ ] Expired on period end, DUT Fingerprint change, or basis Revocation

## Independence (SPEC 8, 10)
- [ ] Resolver is not the Provider and not in any basis Party Set

## Records (SPEC 9)
- [ ] Record IDs use the `POPS-1:record` tag
- [ ] Every Determination registered, including `refuted` and `insufficient`
- [ ] Public whenever basis results are public
