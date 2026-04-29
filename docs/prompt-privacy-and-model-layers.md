# [Marcelix] Prompt Privacy And Model Layers

This note documents two things that are easy to confuse:

- prompt privacy
- model branding

They are related, but they are not the same.

## Prompt Privacy Contract

Prompt privacy in [Marcelix] is about **what becomes public** and **what remixers can see**.

It is not a claim that generation happens without external providers or that prompt text never enters operational systems.

### Public rules

- original posts can choose `public` or `hidden` prompt visibility
- hidden prompts do not appear on the public post surface
- hidden prompts do not appear on the public reusable template surface
- remix prompts are hidden by default
- remixers only see their own remix-side edits

### What stays server-side

- the hidden source baseline
- draft-only prompt history
- internal generation metadata
- provider-facing request context needed for generation

### What the promise is not

[Marcelix] is not claiming:

- local-only inference
- zero provider exposure
- permanent immutability of every prompt record in every operational system

The public promise is about surface privacy, access boundaries, and remix boundaries.

## Public Discovery And Hidden Prompts

The public discovery contract is based on public signals such as:

- follows
- tags
- titles
- descriptions
- engagement
- reusable status

Hidden prompt text is not presented as a public discovery surface.

## Model Branding Contract

`Marcelin` and `Video Galaxy` are product-facing lane names in [Marcelix].

That means:

- they are the stable user-facing labels
- they describe expected behavior, not provider identity
- the external provider mix can change over time

This is deliberate. The product contract is the lane behavior, not a permanent promise about one named upstream provider forever.

## Image Lanes

Current public image lanes:

- `Marcelin ULTRA`
- `Marcelin PLUS`
- `Marcelin FAST`

Supported public image frames:

- `1:1`
- `4:5`
- `3:4`
- `16:9`
- `9:16`

Reference rules:

- up to 3 reference images
- each reference image adds 1 credit

## Video Lanes

### `Video Galaxy`

Supported public frames:

- `16:9`
- `9:16`
- `1:1`
- `4:3`
- `3:4`
- `3:2`
- `2:3`

Supported public output lanes:

- `5s 480p`
- `10s 480p`
- `5s 720p`
- `10s 720p`

Reference rules:

- use guidance references or a single start frame

### `Video Galaxy Pro`

Supported public frames:

- `16:9`
- `9:16`

Supported public output lanes:

- `4s 720p`
- `8s 720p`
- `12s 720p`

Reference rules:

- one guidance image or one start frame

## Why The Branding Layer Exists

The branding layer lets [Marcelix]:

- keep the user-facing contract stable
- tune providers behind the scenes
- improve reliability without forcing users to learn provider churn

That is a product choice, not an attempt to imply hidden ownership of a foundation model.

[Marcelix]: https://www.marcelix.com
