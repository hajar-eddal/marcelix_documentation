# [Marcelix] Rewards And Payouts

This document explains the public contract for Creator Rewards in [Marcelix].

It is deliberately precise about states and edge cases, and deliberately abstract about anti-abuse thresholds and internal reserve formulas.

## Program Positioning

Creator Rewards in [Marcelix] are:

- optional
- tied to eligible paid remix activity
- subject to settlement, review, and reversal rules

They are not:

- wages
- employment compensation
- guaranteed income
- a promise that every remix event turns into withdrawable cash

## What Creates A Reward Event

At a high level, a reward event can be created when:

- a public reusable source is remixed
- the remixer is not the source creator
- the remix uses at least some purchased credits that qualify for reward funding
- the remix resolves to a reward lane

Publicly documented cases that do **not** create stable reward value:

- self-remixes
- promo-only remixes
- non-public drafts
- non-reusable public posts
- refunded, disputed, or reversed funding
- activity held for abuse or payout-risk review

## Direct-Source Rule

Rewards in [Marcelix] are attached to the **direct reusable source** selected for the remix.

This public contract does not promise:

- a parent + grandparent + original-source split
- recursive multi-hop royalty sharing
- automatic revenue sharing across an entire remix tree

That keeps the user contract simple and the accounting surface bounded.

## Reward Event States

| State | Meaning |
| --- | --- |
| `pending` | Event created, inside settlement window |
| `held` | Event created, temporarily locked for review |
| `available` | Cleared and spendable as reward value |
| `converted` | Converted into Marcelix credits |
| `requested` | Reserved into a payout request |
| `paid` | Included in a completed payout |
| `reversed` | Removed or offset after correction |

## Wallet Rules

The creator reward wallet tracks multiple balances, not just one number.

Publicly meaningful buckets include:

- pending
- held
- available
- requested / in-flight payout value
- negative adjustment

The negative adjustment bucket matters because a creator can receive value first and correction later.

## Reconciliation Principle

[Marcelix] does not try to infer money state from one balance number.

Publicly, the system keeps separate records for:

- credit purchases
- credit lots
- reward events
- payout accounts
- payout requests
- payout reversals and negative adjustments

That separation is what makes it possible to reconcile:

- a successful paid purchase
- credit delivery
- reward creation
- reward conversion
- payout submission
- payout success or failure
- later refund, dispute, or reversal corrections

## Negative Adjustment Rule

If a reward was already:

- converted to credits
- requested for payout
- or paid out

and the underlying funding is later reversed, [Marcelix] can apply a negative adjustment balance.

That correction must be cleared before new conversions or new payout requests continue.

## Payout Account States

| State | Meaning |
| --- | --- |
| `not_connected` | No payout destination on file |
| `pending` | Destination saved, but not yet fully ready |
| `verified` | Destination is usable for payout submission |
| `restricted` | Destination or account is blocked pending review |

### What `verified` means

In public-contract terms, `verified` means [Marcelix] has a payout destination that is usable for provider submission.

That can involve:

- a saved payout email
- a successful provider-side payout identity link
- provider-compatible destination details
- an unrestricted payout account state

It does **not** mean that Marcelix is making a public promise about a single exact verification mechanism forever.

## Payout Request States

| State | Meaning |
| --- | --- |
| `pending_review` | Internal review state reserved for requests that exist before queue submission |
| `submitted` | Accepted into the payout queue |
| `processing` | Claimed by payout processing |
| `paid` | Provider confirmed success |
| `rejected` | Provider or risk flow rejected the request |
| `reversed` | Already-paid request was later corrected |
| `canceled` | Request canceled before completion |

Current creator cashout requests normally enter `submitted` once the request passes eligibility checks. `pending_review` remains part of the broader state model for queue-control and manual handling paths.

## Provider Status Mapping

[Marcelix] uses its own internal states and then maps provider outcomes into them.

Example public mapping:

| Provider-style outcome | Marcelix effect |
| --- | --- |
| Success / succeeded | `paid` |
| Blocked / failed / unclaimed | request rejected, account may become restricted |
| Returned / canceled | request rejected without necessarily restricting the account |
| Later funding reversal after payout | payout reversal record or negative adjustment flow |

The point is not to mirror every provider string one-to-one. The point is to preserve a stable user-facing state machine.

## Cashout Requirements

To request a cash redemption in [Marcelix], a creator needs:

- rewards that have cleared the pending window
- enough available value to meet the minimum cashout threshold
- a payout destination that is usable for payout submission
- an account in good standing
- no blocking negative adjustment review

## Processing Timing

Payout requests are not guaranteed instant money movement.

Processing depends on:

- provider status
- payout destination readiness
- reserve health
- request review
- network/provider availability

That is why the public contract is "eligible payout requests are processed through the payout workflow," not "every request is paid immediately on a fixed promise."

## Reserve Safety

Before submitting creator payouts, [Marcelix] tracks reserve pressure against:

- captured net purchase cash
- unspent paid-credit liability
- pending reward liability
- held reward liability
- available reward liability
- requested payout liability
- estimated payout-fee reserve

The public contract is that payouts are constrained by these liabilities and correction risks. The exact reserve formula is internal.

## Correction Example

Here is the important accounting scenario:

1. A user buys a credit pack.
2. The user spends part of that paid pack on remix activity.
3. Several creators receive reward events.
4. Some of those events may become available, converted, requested, or paid.
5. If the original purchase is later refunded, disputed, or reversed, [Marcelix] can remove unused paid credits, reverse linked reward value, and apply negative adjustments when already-processed value must be corrected.

That is why reward accounting is treated as a ledger problem, not as a simple engagement bonus.

## Country And Provider Constraints

Creator Rewards participation is subject to payout-provider reality.

Publicly, that means:

- not every country or payout destination is guaranteed supported
- not every account stays eligible forever
- [Marcelix] can restrict or reject payout access when provider, policy, risk, or compliance constraints require it

[Marcelix]: https://www.marcelix.com
