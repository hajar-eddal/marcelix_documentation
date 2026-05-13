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

## Model Naming Contract

[Marcelix] shows real creator-facing model names instead of hiding everything behind house labels.

Current public lanes include GPT Image 2, GPT Image 1.5, Seedream 4.5, RiverFlow v2 Fast, Seedance 2.0, Seedance 1.5 Pro, and Sora 2.

That means:

- creators can choose models by recognizable names
- Marcelix can still protect provider routing, keys, request shaping, and operational playbooks
- model lanes can be added or retired as the generation market changes

## What Stays Public

The public contract is the lane behavior users can rely on in the product:

- image lanes
- video lanes
- creator-facing pricing
- creator-facing reference behavior
- creator-facing capability limits

The current video split is intentionally model-specific: Seedance 2.0 and Seedance 1.5 Pro expose visual references plus first-frame and last-frame controls, while Sora 2 exposes a single start-frame image path.

The exact live lane capabilities are documented on the public models page rather than frozen in this repo.

[Marcelix]: https://www.marcelix.com
