# [Marcelix] Discovery, Tags, And Moderation

This note explains how public discovery works in [Marcelix] without turning ranking or moderation internals into a public abuse manual.

## Feed Goals

The discovery system has to do three things at once:

- reward quality
- create openings for newer creators
- keep the feed from collapsing into repetition

That is why [Marcelix] uses distinct feed modes instead of one universal ranking list.

## Public Ranking Inputs

Across the public surfaces, the documented input classes include:

- followed creators
- followed tags
- shared tags
- title and public-text overlap
- net votes
- remix counts
- comment counts
- freshness
- age decay
- reusable eligibility

The stable public contract is the input classes and hard constraints, not the exact weights.

## Hard Constraints

The important public constraints are:

- remixes only compete broadly in public discovery when they are themselves reusable
- one creator is capped before the feed widens again
- one near-duplicate cluster is capped before the feed widens again
- report-hidden or removed content is not treated as normal public inventory

Those rules matter more to trust than the exact numeric weight on a vote or a remix.

## Why Tags Matter

Tags in [Marcelix] are:

- searchable
- followable
- visible on post surfaces
- visible on tag pages
- attributable when they originate from a creator

That makes them a real distribution layer, not just post metadata.

## Tag Attribution Is Not Tag Ownership

Creator-originated tags can display creator attribution in the product.

But [Marcelix] does not treat tag attribution as permanent property.

The platform can:

- merge tags
- rename tags
- feature or suppress tags
- remove abusive or impersonating tags
- override squatted or misleading tags

That keeps the tag system useful without turning it into a permanent land-grab mechanic.

## Moderation Model

[Marcelix] moderates at multiple layers:

- prompt-time safety checks
- generation-time safety checks
- publication-time visibility rules
- community reports
- manual review

Publicly visible consequences include:

- request blocked before generation
- post stays private
- post goes public
- post is auto-hidden under report pressure
- post is restored after review
- post is removed after review

## Report And Review Flow

At a public level, the report path looks like:

1. A user reports a public post.
2. Report pressure and threshold logic determine whether the post stays visible, gets flagged, or is auto-hidden.
3. The creator can request manual review.
4. Admin review can restore or remove the post.

That gives [Marcelix] a fast protection path while still preserving a manual review step for important decisions.

## Abuse And Reward Interaction

Discovery, remix, and rewards are connected.

That means abuse review can affect more than feed visibility. It can also affect:

- reward event state
- payout eligibility
- payout account restrictions

This is a necessary boundary in any product where discovery can create money-linked events.

[Marcelix]: https://www.marcelix.com
