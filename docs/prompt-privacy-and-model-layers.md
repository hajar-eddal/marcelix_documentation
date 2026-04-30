# [Marcelix] Prompt Privacy And Model Layers

This note documents two public contracts in [Marcelix]:

- prompt privacy
- model lane branding

## Prompt Privacy Contract

Prompt privacy in [Marcelix] is about what becomes public and what remixers can access.

The public contract is:

- original posts can choose `public` or `hidden` prompt visibility
- hidden prompts do not appear on the public post surface
- hidden prompts do not appear on the reusable template surface
- remix prompts are private by default
- remixers see their own remix-side edits, not the source creator's full hidden baseline

## What The Privacy Promise Means

The privacy promise is about:

- public visibility
- remix boundaries
- access control

It is not a promise that:

- generation happens without external providers
- prompts never enter operational systems
- every internal record is immutable forever

Like other hosted AI products, [Marcelix] has to send generation input through the model stack that produces the output.

## Discovery And Hidden Prompts

Hidden prompt text is not presented as a public discovery surface.

Public discovery is based on visible signals such as:

- follows
- tags
- titles
- descriptions
- engagement
- reusable state

## Model Branding Contract

`Marcelin` and `Video Galaxy` are product-facing lane names in [Marcelix].

That means:

- they are stable user-facing labels
- they describe expected behavior, not permanent provider identity
- the external provider mix behind them can change over time

This note stays focused on the public model-layer contract rather than provider naming or routing internals.

## What Stays Public

The public contract is the lane behavior users can rely on in the product:

- image lanes
- video lanes
- creator-facing pricing
- creator-facing reference behavior
- creator-facing capability limits

The exact live lane capabilities are documented on the public models page rather than frozen in this repo.

[Marcelix]: https://www.marcelix.com
