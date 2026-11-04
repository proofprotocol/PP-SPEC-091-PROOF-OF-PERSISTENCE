# Proof of Persistence

*A Proof Protocol claim specification*

> **Ownership and Attribution Notice**
>
> This specification is authored by **Craig Thomas Ellrod** and is published as part of **Proof Protocol**. Copyright (c) 2026 Craig Thomas Ellrod.
>
> Any use, implementation, derivative, citation, or incorporation of this specification, in whole or in part, MUST attribute **Craig Thomas Ellrod and Proof Protocol**. This requirement applies to standards bodies, working groups, consortia, and commercial implementations.
>
> Licensed under the Proof Protocol License 1.1 (see LICENSE.md); text CC BY 4.0 under Part A, which grants no patent rights. Original inventor: Craig Thomas Ellrod (ORCID 0009-0004-1058-7666).
>
> **Patents.** Patent terms are in [PATENT-SCHEDULE.md](PATENT-SCHEDULE.md). Claims not listed there are reserved by Craig Thomas Ellrod. Licensing: 1proofprotocol@gmail.com.
>
> This specification is related to the Proof Economy Prior Art Declaration, DOI [10.5281/zenodo.21379780](https://doi.org/10.5281/zenodo.21379780).

| Field | Value |
|---|---|
| Spec ID | PP-SPEC-091 |
| Version | 0.1.0 (Draft) |
| Date | 2026-11-04 |
| Status | Draft for public record |
| Maintainer | Craig Thomas Ellrod (Proof Protocol) |
| Claim | Proof of Persistence |
| Question | Does the efficacy still hold over time? |
| Builds on | PP-SPEC-077 (Dead Canary), PP-SPEC-079 (Coal Mine), PP-SPEC-004 (ProofRegister API) |

---

## Abstract

Proof of Persistence is the claim that a control's measured efficacy held over a declared span: across every epoch of a PP-SPEC-077 Production Stream Mode run, or a declared series of Bounded Mode runs, its Efficacy Rate and False Block Rate stayed within tolerances declared in advance, and no Silent Drift event occurred. Every DUT Fingerprint change inside the span is recorded and ends the claim at that change.

*A proof from one day is a proof about that day.*

Proof of Persistence is one member of the Proof of X claim family (PP-SPEC-082, PP-SPEC-089 to PP-SPEC-099 and PP-SPEC-101). Each member answers exactly one question. Only Proof of Efficacy answers whether a control worked; the other members answer the questions a buyer, insurer, regulator or auditor must also have answered before a proof of efficacy can be relied on. No member is a substitute for any other.

**What this is not.**

- It is not a guarantee about the future. It covers the declared span, and nothing after it.
- It does not carry across a DUT Fingerprint change. A changed control is a new control.

## 1. Conventions

The key words MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, NOT RECOMMENDED, MAY, and OPTIONAL in this document are to be interpreted as described in BCP 14 (RFC 2119, RFC 8174) when, and only when, they appear in all capitals.

References of the form "077" refer to PP-SPEC-077; other three-digit numbers refer to the Proof Protocol specification with that number. Unprefixed section references are to this specification.

## 2. Terminology

Terms defined in PP-SPEC-077, PP-SPEC-078 and PP-SPEC-079 have the same meaning here. In addition:

- **Claim:** The statement that Proof of Persistence holds for a named subject, scope and period.
- **Claim Declaration:** The record, registered and bound to a Time Anchor pulse before any evidence it relies on is produced, that states the claim, its subject, its scope and its limits (Section 4).
- **Claim Record:** The record of a determination of the claim (Section 9).
- **Determination:** Exactly one of `proven`, `refuted` or `insufficient` (Section 6).
- **Declarant:** The party that registers a Claim Declaration.
- **Resolver:** The party that computes a Determination from registered records (Section 10).
- **Persistence Span:** The declared period over which the claim is made.
- **Epoch:** One committed clutch of canaries in Production Stream Mode, or one Bounded Mode run in a declared series.
- **Drift Tolerance:** The declared maximum movement of each rate between epochs and from the first epoch.

## 3. The Question

3.1. Proof of Persistence answers one question:

> **Does the efficacy still hold over time?**

3.2. A party describing a record MUST NOT present Proof of Persistence as an answer to any other question, and MUST NOT present an answer to any other question as Proof of Persistence.

3.3. "Proof" is a term of art in Proof Protocol. A party MUST NOT describe Proof of Persistence as verification, validation, attestation, assurance, or testing, and MUST NOT describe any of those as Proof of Persistence. A claim built on the measured party's own records is verification, not proof (PP-SPEC-024).

## 4. Claim Declaration

4.1. **Declare first.** The Declarant MUST register a Claim Declaration bound to a Time Anchor pulse before any evidence whose outcome the claim's limits are applied to is produced. Such evidence produced before the Claim Declaration's pulse MUST NOT be counted toward the claim. Records the claim only refers to, such as an original proof, a registered Mine Plan or an Interface Manifest, MAY predate the Claim Declaration if they were registered before it.

4.2. The Claim Declaration MUST contain:

- The subject: the DUT Fingerprint, and the AUT or CUT where applicable
- The Declarant, its interest in the outcome, and the funding tier and Sponsor (079 Section 6)
- The validity period of the claim
- The Persistence Span and the epoch cadence
- The minimum rates per epoch and the Drift Tolerances
- The minimum number of valid epochs and the maximum gap between epochs
- A publication commitment: that every Determination will be published whatever its result

4.3. **Limits before results.** Every limit, minimum and tolerance in the Claim Declaration is fixed at registration. It MUST NOT change afterward. A Declarant that wants different limits MUST register a new Claim Declaration.

4.4. **Who may declare.** Any party MAY register a Claim Declaration, including the Holder, an Implementor, an insurer, a regulator, an auditor, or a competitor of the Provider. The Declarant's interest MUST be declared.

## 5. Evidence Basis

5.1. Proof of Persistence is determined only from the following registered records:

| Record | What it contributes |
|---|---|
| PP-SPEC-077 Production Stream Mode clutches | Every committed epoch batch in the span, with its rates. |
| Silent Drift events | Any rate movement beyond tolerance with no change in DUT Fingerprint. |
| DUT Fingerprint history | Every fingerprint captured in the span, captured independently of the Provider. |

5.2. Every basis record MUST be Conformant under its own specification and Registered. A record produced outside Proof Protocol, under any framework, is verification evidence and MUST NOT be a basis record.

5.3. The measured party's own logs, consoles, alerts, receipts and reports MUST NOT be a basis record.

## 6. Determination

6.1. The Resolver computes exactly one Determination:

| Determination | Rule |
|---|---|
| `proven` | Every epoch in the Persistence Span is valid and meets the declared minimum rates, no Silent Drift event occurred, and the DUT Fingerprint did not change inside the span. |
| `refuted` | Any valid epoch falls below the declared minimum rates, or a Silent Drift event occurred. |
| `insufficient` | Fewer valid epochs than declared, a gap between epochs longer than declared, or a fingerprint change before the span ends (the claim then covers only the span before the change). |

6.2. **Precedence.** Where the rules for both `refuted` and `insufficient` are met, the Determination is `refuted`. A claim is `proven` only when neither of the others applies.

6.3. **Mechanical.** The Determination MUST be computed from the Claim Declaration and the registered basis records alone, with no other input, so that any party applying this section to the same records obtains the same Determination.

6.4. **Insufficient is not a result.** `insufficient` is neither `proven` nor `refuted` and MUST NOT be presented as either.

## 7. Scope, Validity and Expiry

7.1. A Claim Record states its scope exactly as declared. A party MUST NOT present a claim as covering anything outside that scope.

7.2. A `proven` Determination expires at the first of: the end of the declared validity period; any change of the subject's DUT Fingerprint; or the Revocation of any basis record (077 Section 21).

7.3. An expired claim MUST NOT be presented as current. It remains a record of what was proven for its period.

7.4. Where a proof is reproduced under PP-SPEC-081, a Claim Record MAY carry the Reproof Status of its basis records. It MUST NOT carry it if the reproof scope differs from the claim scope.

## 8. Independence

8.1. The Provider of the subject MUST NOT act as Resolver and MUST NOT occupy any Integration Point of any basis record.

8.2. The Resolver MUST NOT be a member of the Party Set of any basis record.

8.3. Every separation rule of the specification that produced each basis record applies to that record unchanged.

8.4. An undisclosed affiliation discovered after a Determination invalidates it. Any party MAY publish a Revocation with the evidence of the affiliation.

## 9. Records

9.1. The Claim Declaration and the Claim Record are records under 077 Section 21. Their Record IDs are computed as `SHA-256("POPS-1:record" || canonical_form)` under the exclusions of 077 Section 21.

9.2. A Claim Record MUST carry: the Claim Declaration's Record ID; the Record IDs of every basis record; the Determination; the scope; the validity period and any expiry reason; and the result fields of [schemas/persistence-claim.schema.json](schemas/persistence-claim.schema.json).

9.3. **Publication.** Every Determination, including `refuted` and `insufficient`, MUST be registered. A claim shown without its history of Determinations is non-conforming.

9.4. **Disclosure.** A Claim Record MUST be at Disclosure Level `public` whenever its basis result records are `public`.

9.5. **Humans and machines.** A Determination computed by a machine from the Registry and by a person from the human renderings MUST be the same.

9.6. **Authorship Disclosure.** 077 Section 21.15 applies to this specification and to every Resolver implementing it.

## 10. Integration Points

10.1. Every basis record occupies the Integration Points of its own specification. The Proof of X claim family adds two, common to PP-SPEC-082, PP-SPEC-089 to PP-SPEC-099 and PP-SPEC-101:

| ID | Integration Point | What plugs in | MUST do | MUST emit |
|---|---|---|---|---|
| **IP-C1** | Declarant | Holders, Implementors, insurers, regulators, auditors, independent laboratories | Register the Claim Declaration before any evidence measured against its limits is produced; commit to publication | Claim Declaration, anchored |
| **IP-C2** | Resolver | Registries, verifiers, agents, dashboards | Compute the Determination under Section 6 from registered records alone; identical output to the reference resolver on the conformance vectors | Claim Record |

10.2. **Separation.** The Resolver MUST NOT be the Provider, MUST NOT be a member of any basis record's Party Set, and SHOULD NOT be the Declarant.

## 11. Relationship to Proof of Efficacy and the Family

11.1. The Proof of X claim family:

| Claim | Spec | Question |
|---|---|---|
| Proof of Efficacy | PP-SPEC-077 | Did the control produce the required outcome under adversarial pressure? |
| Proof of Containment | PP-SPEC-082 | Did the containment control hold the agent? |
| Proof of Conduct | PP-SPEC-089 | Did the agent stay inside its committed boundary? |
| Proof of Restraint | PP-SPEC-090 | Did the control avoid stopping legitimate work? |
| Proof of Persistence | PP-SPEC-091 | Does the efficacy still hold over time? |
| Proof of Attribution | PP-SPEC-092 | Which control actually stopped the attack? |
| Proof of State | PP-SPEC-093 | Is the control in production the same control that was proven? |
| Proof of Parity | PP-SPEC-094 | Did the test environment match production? |
| Proof of Coverage | PP-SPEC-095 | What was tested, and what was claimed but not tested? |
| Proof of Capture | PP-SPEC-096 | Was the evidence honest at the moment it was captured? |
| Proof of Reproduction | PP-SPEC-097 | Did an independent party get the same result? |
| Proof of Response | PP-SPEC-098 | Did detection or containment happen within the required window? |
| Proof of Recovery | PP-SPEC-099 | After a failure, was the system restored? |
| Proof of Delegation | PP-SPEC-101 | Did the agent hold and use only the authority it was granted? |

11.2. A reader MAY require several claims together. PP-SPEC-080 Acceptance Profiles MAY name any member of the family as a condition of acceptance.

11.3. A Proof of Efficacy published without its Proof of Restraint result (PP-SPEC-090) is non-conforming.

## 12. Framework Mappings (informative)

Frameworks that ask the question this claim answers include:

- EU DORA (PP-SPEC-057)
- FedRAMP 20x (PP-SPEC-056)
- NIST SP 800-53 continuous monitoring (PP-SPEC-055)

A mapping identifies where this claim may be relevant. It does not establish compliance, certification or endorsement by any framework's owner.

## 13. Security Considerations

- **Best epoch shown:** Every epoch in the span is published; a claim over a subset is a claim over a shorter span.
- **Quiet reconfiguration:** Fingerprint capture runs every epoch; a change ends the claim at the change.
- **Declaration after the fact:** Evidence measured against the claim's limits never counts if it was produced before the Claim Declaration's pulse (4.1).
- **Claim shopping:** Every Determination is published, including `refuted` and `insufficient` (9.3).
- **Tuned limits:** Limits are fixed at declaration (4.3) and published with every Determination, so PP-SPEC-080 profiles can set the minimum limits a reader will accept.

## 14. Interpretation

Craig Thomas Ellrod, as maintainer of Proof Protocol, is responsible for the editorial text of this specification. Whether a Claim Declaration, Determination or Claim Record conforms is determined from its records against the normative text, and is not decided by the maintainer.

## Revision History

| Version | Date | Notes |
|---|---|---|
| 0.1.0 | 2026-11-04 | Initial draft. Proof of Persistence defined as the answer to one question: Does the efficacy still hold over time? Claim Declaration before evidence; evidence basis; mechanical Determination (`proven`, `refuted`, `insufficient`); scope, validity and expiry; independence; records under the `POPS-1:record` tag; IP-C1 and IP-C2. |
