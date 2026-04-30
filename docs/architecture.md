# [Marcelix] Architecture

This is not a deployment diagram or an implementation manual.

It is a short design-decisions note for [Marcelix]: why the product is structured around public posts, reusable sources, remix paths, and creator rewards instead of just generation plus export.

## Design Decision 1: private generation and public post are different objects

Most AI apps flatten creation into one thing: you generate, then you publish or download the result.

[Marcelix] splits those states on purpose.

Private generation is where creators experiment, fail, compare, and iterate. Public posting is where work becomes part of the network. That separation matters because serious creators need room to create privately before anything becomes a public social object.

## Design Decision 2: reusable source is not the same thing as a public post

Not every public post should automatically become remixable infrastructure.

That is why [Marcelix] keeps a real distinction between:

- a post that is public
- a post that is reusable

Public visibility answers "can people see this?"

Reusable answers "can other creators build from this directly inside the product?"

Those are different permissions, and separating them makes the product more legible for creators.

## Design Decision 3: prompt privacy is separate from remixability

In many AI products, remixability and prompt exposure get tangled together.

[Marcelix] treats them separately.

A post can be reusable without forcing the creator to turn the full underlying prompt workflow into a public artifact. That is the product line between:

- a work that can be built from
- a recipe that must become fully visible

That distinction is one of the main reasons remix can exist here without collapsing into pure prompt leakage.

## Design Decision 4: rewards are downstream of paid reuse, not upstream of attention

[Marcelix] is not trying to pay creators for vague engagement or raw views.

The product is designed so that creator upside appears when a piece of reusable work causes valid downstream paid reuse inside the network. That keeps the reward layer tied to actual creation flow rather than to generic social noise.

## The Main Line Between Public And Private

The simplest design line in [Marcelix] is this:

some objects belong to the creator's private workflow, and some become public network surfaces.

That line is what keeps the product understandable.

| Object | Public surface | Private surface |
| --- | --- | --- |
| Private generation | None | Creator draft and generation context |
| Public post | Feed, profile, post page | Internal generation metadata |
| Reusable source | Remix entry point and public post state | Hidden prompt baseline and private context |
| Reward value | Creator-facing totals and actions | Internal ledger detail and funding linkage |
| Payout request | Creator-facing request status | Provider submission detail and review history |

## Why This Repo Stays At The Product Layer

[Marcelix] is happy to document the creator-facing contract publicly.

This repo is meant to help users and technical readers understand the shape of the product, not to publish the operational implementation behind it.

[Marcelix]: https://www.marcelix.com
