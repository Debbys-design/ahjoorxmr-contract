# ROSCA Collective Savings Goals

This document describes the group-wide collective savings goal feature of the
`ahjoor-rosca` contract. A collective savings goal lets a ROSCA group pool
contributions toward a shared target, track progress against that target, and
finalize the goal once it is met.

The feature is implemented in
`contracts/ahjoor-rosca/src/savings_goal_tracking_impl.rs` and is separate from
the per-milestone reward mechanism.

## Overview

A collective savings goal is a group-scoped target amount. Members fund the
goal over time by contributing to it, and the contract tracks the accumulated
total against the target. The lifecycle is:

1. **Create** the goal with `create_goal`.
2. **Fund** the goal with `contribute_to_goal`.
3. **Inspect** progress with `get_goal_progress`.
4. **Finalize** the goal with `complete_goal` once the target is reached.

## Creating a goal

`create_goal` establishes the group's collective savings goal. It records the
target amount for the group and initializes the tracked progress. A group has a
single collective goal at a time; the goal is created before any contributions
are made toward it.

## Funding a goal

`contribute_to_goal` adds a member's contribution to the group's collective
goal. Each call increases the accumulated amount tracked for the goal. Members
may contribute repeatedly until the target is reached.

## Checking progress

`get_goal_progress` reports the current state of the collective goal. It
returns the progress of the goal, including the amount contributed so far
relative to the target, so callers can determine how much remains before the
goal can be completed.

## Completing a goal

`complete_goal` finalizes the collective savings goal. It is called once the
goal's target has been met, marking the goal as completed and closing out the
collective savings effort for the group.
