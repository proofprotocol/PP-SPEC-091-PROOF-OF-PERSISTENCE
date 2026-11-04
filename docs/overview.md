# Overview

*Informative. [SPEC.md](../SPEC.md) controls.*

## The question

**Does the efficacy still hold over time?**

Proof of Persistence is the claim that a control's measured efficacy held over a declared span: across every epoch of a PP-SPEC-077 Production Stream Mode run, or a declared series of Bounded Mode runs, its Efficacy Rate and False Block Rate stayed within tolerances declared in advance, and no Silent Drift event occurred. Every DUT Fingerprint change inside the span is recorded and ends the claim at that change.

## Why it matters

A proof from one day is a proof about that day. A buyer, insurer or regulator relying on a proof of efficacy also needs this question answered, and answered by evidence the measured party did not produce.

## What it is not

- It is not a guarantee about the future. It covers the declared span, and nothing after it.
- It does not carry across a DUT Fingerprint change. A changed control is a new control.

## The three answers

- **proven:** Every epoch in the Persistence Span is valid and meets the declared minimum rates, no Silent Drift event occurred, and the DUT Fingerprint did not change inside the span.
- **refuted:** Any valid epoch falls below the declared minimum rates, or a Silent Drift event occurred.
- **insufficient:** Fewer valid epochs than declared, a gap between epochs longer than declared, or a fingerprint change before the span ends (the claim then covers only the span before the change).
