# Proof of Persistence

> **Ownership and Attribution Notice**
>
> Proof of Persistence (PP-SPEC-091) is authored by **Craig Thomas Ellrod** and is published as part of **Proof Protocol**. Copyright (c) 2026 Craig Thomas Ellrod.
>
> Any use, implementation, derivative, citation, or incorporation of this specification, in whole or in part, MUST attribute **Craig Thomas Ellrod and Proof Protocol**. This requirement applies to standards bodies, working groups, consortia, and commercial implementations.
>
> Licensed under the Proof Protocol License 1.1 (see LICENSE.md); text CC BY 4.0 under Part A, which grants no patent rights. Original inventor: Craig Thomas Ellrod (ORCID 0009-0004-1058-7666).
>
> **Patents.** Patent terms are in [PATENT-SCHEDULE.md](PATENT-SCHEDULE.md). Claims not listed there are reserved by Craig Thomas Ellrod. Licensing: 1proofprotocol@gmail.com.

---

**Does the efficacy still hold over time?**

*A proof from one day is a proof about that day.*

Proof of Persistence is the claim that a control's measured efficacy held over a declared span: across every epoch of a PP-SPEC-077 Production Stream Mode run, or a declared series of Bounded Mode runs, its Efficacy Rate and False Block Rate stayed within tolerances declared in advance, and no Silent Drift event occurred. Every DUT Fingerprint change inside the span is recorded and ends the claim at that change.

## How it works

1. **Declare first.** The claim, its subject, scope and limits are registered and anchored before the evidence they are measured against is produced.
2. **Evidence from the family.** The claim is determined only from Conformant, registered Proof Protocol records:
- **PP-SPEC-077 Production Stream Mode clutches**
- **Silent Drift events**
- **DUT Fingerprint history**
3. **Determine mechanically.** Exactly one of `proven`, `refuted` or `insufficient`, computed the same way by a person and a machine.
4. **Publish everything.** Every Determination is registered, whatever its result.
5. **Expire honestly.** A changed control, a revoked basis record, or the end of the declared period ends the claim.

## Part of the Proof of X family

Only Proof of Efficacy answers whether a control worked. Proof of Persistence answers one other question a reader needs answered. See SPEC.md Section 11 for the whole family, PP-SPEC-082, PP-SPEC-089 to PP-SPEC-099 and PP-SPEC-101.

## Repository

| Path | Contents |
|---|---|
| [SPEC.md](SPEC.md) | The normative specification, PP-SPEC-091 |
| [docs/overview.md](docs/overview.md) | Plain-English walkthrough |
| [docs/glossary.md](docs/glossary.md) | Terms |
| [docs/conformance.md](docs/conformance.md) | Conformance checklist |
| [schemas/persistence-claim.schema.json](schemas/persistence-claim.schema.json) | Claim Declaration and Claim Record schemas |
| [schemas/ai-disclosure.schema.json](schemas/ai-disclosure.schema.json) | Authorship Disclosure schema (077 21.15) |
| [CHANGELOG.md](CHANGELOG.md) | Version history |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to engage |
| [GOVERNANCE.md](GOVERNANCE.md) | How this specification is governed |
| [NOTICE.md](NOTICE.md) | Attribution requirements |
| [AI_DISCLOSURE.md](AI_DISCLOSURE.md) | What was human-authored and what was AI-drafted |
| [FUNDING.md](FUNDING.md) | Funding disclosure |
| [REVIEWERS.md](REVIEWERS.md) | Review disclosure |
| [ACKNOWLEDGEMENTS.md](ACKNOWLEDGEMENTS.md) | Credits |
| [ETHICS.md](ETHICS.md) | Proof Economy Code of Ethics |
| [CITATION.cff](CITATION.cff) | Citation metadata |
| [SECURITY.md](SECURITY.md) | Reporting protocol flaws |
| [PATENT-SCHEDULE.md](PATENT-SCHEDULE.md) | Patent terms |
| [LICENSE.md](LICENSE.md) | License terms |
| [LICENSE-CC-BY-4.0.md](LICENSE-CC-BY-4.0.md) | CC BY 4.0, specification text |
| [LICENSE-APACHE-2.0.md](LICENSE-APACHE-2.0.md) | Apache License 2.0, reference text |

## Status

Draft, version 0.1.0, 2026-11-04. Maintained by Craig Thomas Ellrod as part of Proof Protocol.

Builds on PP-SPEC-077 (Dead Canary), PP-SPEC-079 (Coal Mine). Records are registered to a [PP-SPEC-004](https://github.com/proofprotocol/registry-api-spec) registry; the public instance is [proofregister.com](https://proofregister.com).

Glossary: [Proof of Persistence](https://proofeconomy.com/glossary/proof-of-persistence/). Specifications: [proofprotocol.io](https://proofprotocol.io/).

Archived on Zenodo: pending.

Related: Proof Economy Prior Art Declaration, DOI [10.5281/zenodo.21379780](https://doi.org/10.5281/zenodo.21379780).

## Cite

```
Ellrod, C. (2026). Proof of Persistence (PP-SPEC-091), v0.1.0.
Craig Thomas Ellrod, Proof Protocol. https://github.com/proofprotocol/PP-SPEC-091-PROOF-OF-PERSISTENCE
```
