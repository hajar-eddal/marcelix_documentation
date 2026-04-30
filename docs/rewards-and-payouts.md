# [Marcelix] Rewards And Payouts

This note explains the public contract for Creator Rewards in [Marcelix].

It is written for creators who want to understand how reward value behaves without turning the repo into a payout operations manual.

## Program Positioning

Creator Rewards in [Marcelix] are:

- optional
- tied to eligible paid remix activity
- subject to settlement, review, correction, and provider constraints

They are not:

- wages
- employment compensation
- guaranteed income
- a promise that every remix event becomes immediate cash

## What Generally Creates Reward Value

At a public level, reward value can be created when:

- a public reusable source is remixed inside [Marcelix]
- the remixer is not the original source creator
- the remix uses paid credit value that qualifies for creator funding
- the activity remains valid through settlement and review

The creator-facing rule is simple:

> rewards attach to the reusable source that was actually remixed

The repo stays at the creator-facing contract level rather than documenting internal accounting and routing logic.

## What Usually Does Not Count

These common cases do not create stable withdrawable reward value:

- self-remixes
- private drafts
- non-reusable public posts
- promo-only activity
- refunded, disputed, or reversed funding
- activity paused for abuse, risk, or compliance review

## Settlement Principle

[Marcelix] treats rewards as a settlement problem, not an instant engagement bonus.

That means:

- reward value can be created before it becomes usable
- usable value can later be corrected if the underlying funding is reversed
- payout access depends on both product state and provider reality

Creators can view the live public rules, current reward lanes, waiting windows, and payout thresholds in the product and policy surfaces.

## Conversion And Cashout

Eligible reward value can generally be used in two ways:

- converted into Marcelix credits
- submitted for payout when the account is eligible and the request passes platform and provider requirements

Cash redemption depends on things such as:

- cleared reward value
- minimum thresholds
- payout destination readiness
- account standing
- review and reserve checks
- provider availability

## Corrections And Reversals

If an underlying paid purchase is later refunded, disputed, reversed, or otherwise invalidated, [Marcelix] can:

- remove linked unused paid credits
- reverse linked reward value
- apply negative adjustments where already-processed value needs correction
- restrict further conversion or payout until the balance is resolved

This is part of keeping the system financially safe, not a special-case exception.

## Provider Reality

[Marcelix] supports creator payout through a provider-backed payout flow, but provider reality still matters.

That means:

- not every region or destination is guaranteed supported
- payout access can be limited by provider, policy, risk, or compliance constraints
- provider-side outcomes can affect whether a payout request proceeds, pauses, or fails

This note stays at the product-contract level rather than publishing provider-control or reconciliation internals.

## Why This Note Stays High Level

The goal of this note is to define the creator-facing contract clearly enough to build trust without turning the repo into a payout operations manual.

[Marcelix]: https://www.marcelix.com
