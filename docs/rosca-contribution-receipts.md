# Contribution Receipts in ROSCA

## Overview

Every contribution made to an `ahjoor-rosca` group is recorded on-chain as a `ContributionReceipt`. Receipts give members a verifiable, per-contribution proof of payment that can be queried independently of the group's aggregate balances. They are issued automatically by the contract whenever a contribution is accepted, so members and integrators do not need to request them explicitly.

This document describes what a `ContributionReceipt` captures, how receipt IDs are assigned, and how to look a receipt up via `get_contribution_receipt`.

## What a `ContributionReceipt` Captures

A `ContributionReceipt` is the on-chain record of a single accepted contribution. It captures:

- **Receipt ID** — the unique identifier assigned to the receipt (see below).
- **Group ID** — the ROSCA group the contribution was made to.
- **Member** — the address credited with the contribution.
- **Round** — the round in which the contribution was recorded.
- **Amount** — the token amount contributed.
- **Timestamp / ledger** — when the contribution was accepted, as recorded by the contract.

Because the receipt is stored on-chain, it can be used as an auditable proof of contribution for a given member, group, and round.

## How Receipt IDs Are Assigned

The contract assigns receipt IDs sequentially as contributions are accepted. Each new receipt receives the next ID in the sequence, so IDs are unique and monotonically increasing. This makes it possible to enumerate receipts and to reference a specific contribution by its ID without ambiguity.

## Looking Up a Receipt

Use `get_contribution_receipt` to fetch a receipt by its ID:

```rust
let receipt = client.get_contribution_receipt(&receipt_id);
```

The call returns the `ContributionReceipt` for the given ID, or `None` if no receipt exists with that ID. Callers should handle the missing-receipt case explicitly.

## Related Documentation

- [On-Chain Audit Trail in ROSCA](rosca-audit-trail.md)
- [ROSCA Reinvestment Flow](rosca-reinvestment.md)
