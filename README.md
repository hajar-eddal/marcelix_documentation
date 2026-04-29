<p align="center">
  <a href="https://www.marcelix.com">
    <img src="./assets/logo-512.png" alt="Marcelix logo" width="112" />
  </a>
</p>

<h1 align="center"><a href="https://www.marcelix.com">Marcelix</a></h1>

<p align="center">
  <strong>An AI-native social network for reusable images, videos, remix chains, and creator payouts.</strong>
</p>

<p align="center">
  <a href="https://www.marcelix.com">marcelix.com</a>
</p>

---

Most AI products are still inference wrappers with an export button.

They generate media, hand you a file, maybe add a feed, and then the interesting part dies:

- the downstream reuse disappears
- the provenance disappears
- the monetization collapses into prompt leakage, affiliate spam, or generic engagement farming

[Marcelix] makes a different bet:

> the durable object is not the prompt  
> and it is not the exported file  
> it is the reusable creative state

That changes the loop from:

```text
prompt -> output -> download -> repost -> disappear
```

to:

```text
private generation -> public post -> reusable source -> remix -> attribution -> reward
```

This README is a public system note for [Marcelix]: the object model, the distribution model, the tag layer, and the settlement model.

## The Claim

An AI-native network should not optimize only for generation quality.

It should optimize for reusable supply.

That means a strong image or short video should be able to do more than collect impressions. It should be able to:

- attract followers
- become a reusable source
- generate derivative work inside the network
- preserve attribution across that derivative work
- create payout-eligible value when downstream paid remixes happen

That is the core claim behind [Marcelix].

## The State Model

The simplest way to understand [Marcelix] is as a state machine for creative objects.

### 1. Private generation

Everything starts private.

Generative work is iterative by default, and a serious system needs a place where creators can test, discard, and compare before anything enters public distribution.

### 2. Public post

The public post is the main distribution unit.

Not the prompt. Not the raw generation row. Not the downloaded asset.

A post carries:

- creator identity
- media
- title and description
- tags
- visibility
- remixability
- provenance
- engagement

### 3. Reusable source

Once a post is reusable, it stops behaving like ordinary content and starts behaving like upstream infrastructure.

That is the point where [Marcelix] diverges from a normal gallery.

### 4. Remix edge

Remix is not "download this and go do something elsewhere."

It is an in-product transition from one creative state to another. That matters because the system can preserve:

- source attribution
- remix counts
- creator growth
- reward eligibility

## Prompt Privacy Is Part Of The Architecture

Most AI products treat prompt visibility as a UI toggle.

[Marcelix] treats it as a structural rule.

At a high level:

- original posts can choose whether prompt text is public or hidden
- remix prompts stay private by default
- the locked source baseline remains server-side
- remixers control their own edits, not the original creator's full recipe

A reusable network only works if creators can publish valuable work, allow derivative use, and still protect the parts of the process that should remain private.

## The Distribution Model

Creator growth on [Marcelix] is not supposed to depend only on who already follows you.

There are three public feed modes:

- `For You`
- `Trending`
- `Following`

They are doing different jobs.

### `Trending`

`Trending` is about momentum, not just popularity.

The ranking combines:

- net voting
- remix activity
- comment activity
- freshness
- age decay

So the system is not only asking "what is popular?" It is asking "what is moving now?"

### `Following`

`Following` starts from explicit user intent:

- creators you follow
- tags you follow

Then it adds discovery backfill so the graph does not become sparse and brittle.

### `For You`

`For You` is the main growth surface because it connects distribution to reuse.

Conceptually, it behaves roughly like:

```ts
forYouFeed =
  diversify(
    postsFromFollowedCreators
    + postsFromFollowedTags
    + adjacentCreativeMatches(sharedTags, titleTerms, promptTerms)
    + broaderDiscoveryBackfill
  )
```

What matters is not the exact weights. What matters is the structure:

1. Start from explicit signals.
2. Expand outward through creative adjacency.
3. Enforce diversity so one creator or one template family cannot flood the page.

The adjacency step is what stops the feed from collapsing into either pure social-graph ranking or pure popularity ranking. [Marcelix] can move from:

- creators you already follow
- tags you already care about

to related work through:

- shared tags
- shared title language
- shared prompt-language terms
- rising related posts

That makes the feed feel more like a creative recommendation system than a chronological upload stream.

One subtle rule matters a lot:

public remixes only belong in the main discovery surface if they are themselves reusable.

That keeps the feed biased toward creative supply rather than derivative noise.

## Tags Are Not Just Metadata

Most social products treat tags as passive labels.

[Marcelix] treats them more like lightweight discovery surfaces.

There are two classes of tags in the system:

- platform-curated tags
- creator-originated tags

When a creator introduces a tag that does not already exist, [Marcelix] creates it as a creator tag and binds it back to that user.

That has product consequences:

- the tag picker can show `created by @username`
- tag search and active tag pages can show `Created by @username`
- users can click directly into the tag surface
- users can follow tags directly
- tag search can return matching tags, not only posts

In a young network, that means an early creator can turn a good tag into durable profile distribution.

If a creator is early to a useful style, meme format, character archetype, or visual niche and establishes the tag that other people keep reusing, that tag can become a lightweight acquisition channel for the creator profile itself.

In practice, that means the tag layer can do three things at once:

- organize discovery
- compress social meaning into a reusable label
- route attention back to the creator who first established the label

That gives creators a second distribution channel besides raw follower count.

## How Creators Actually Grow

The growth loop on [Marcelix] is not "post more."

It is:

1. Make a strong image or short video.
2. Get suggested in `For You`, `Trending`, or tag discovery.
3. Turn viewers into profile followers.
4. Publish the strongest work as reusable.
5. Establish reusable tags around the style or format if the niche is still open.
6. Let other creators remix the work directly in the network.
7. Accrue attribution, remix counts, tag-level discovery, and eligible downstream reward value.

That means creators are not optimizing only for beauty.

They are optimizing for posts that are:

- legible in a feed
- distinct enough to carry style identity
- reusable enough to create downstream demand

The strongest posts on [Marcelix] are not just good outputs.

They are good starting points.

## The Reward Model

[Marcelix] uses prepaid credits for generation and remix actions.

The reward side is downstream of paid reuse, not upstream of posting.

At a high level, the logic is close to:

```ts
if (creatorUserId === remixerUserId) return 0

eligiblePaidCredits =
  sum(consumedLots where cashoutEligible === true)

if (eligiblePaidCredits <= 0) return 0

baseReward =
  mediaType === 'video'
    ? videoRewardLane(duration, quality)
    : referenceMode === 'style-only' && creditCost >= 2
      ? referenceReward
      : standardReward

rewardAmount =
  baseReward * min(1, eligiblePaidCredits / creditCost)

status =
  holdCheck ? 'held' : 'pending'
```

That structure is doing several things at once:

- self-remixes do not earn
- promo-credit-only remixes do not create cashout-eligible value
- image and video remixes do not share the same payout lane
- partially paid-credit remixes can be scaled proportionally

So [Marcelix] is not paying for generic engagement. It is paying for eligible paid reuse.

There are really two gates in the system:

1. Does the remix create a reward event at all?
2. Does that reward event survive settlement and become available?

For a remix to create reward value in the normal case, the system needs all of the following to be true:

- the source work is published as reusable
- another user, not the source creator, performs the remix
- the remix spends at least some purchased credits that are eligible for cashout accounting
- the reward lane resolves from the actual remix type
- the event survives the pending window without being reversed or held

## Public Reward Lanes

These are the current public reward lanes:

| Remix lane | Creator Reward | Cash value | Credit value |
| --- | ---: | ---: | ---: |
| Standard image remix | 0.50 | $0.02 | 0.4 credits |
| Style-reference image remix | 1.00 | $0.04 | 0.8 credits |
| Video remix 5s 480p | 1.25 | $0.05 | 1.0 credits |
| Video remix 10s 480p | 1.50 | $0.06 | 1.2 credits |
| Video remix 5s 720p | 1.75 | $0.07 | 1.4 credits |
| Video remix 10s 720p | 2.25 | $0.09 | 1.8 credits |

The point is not the absolute payout table. The point is that the system recognizes different reuse lanes and prices them differently instead of flattening all derivative work into one fuzzy metric.

## The Settlement Model

A reward event on [Marcelix] is not instantly withdrawable cash.

There is a settlement path:

1. A paid remix happens.
2. A reward event is created.
3. The event enters a pending window.
4. If the underlying transaction remains valid, the reward becomes available.
5. The creator can convert it to credits or request PayPal withdrawal.

Current public settlement rules:

- pending window: `7 days`
- conversion rate: `1 reward = 0.8 credits`
- cash value: `1 reward = $0.04`
- minimum cashout: `$50`

That distinction matters because it separates gross remix activity from stable payout value.

## When A Remix Does Not Produce Reward Value

These are the common cases where a remix either does not create a reward event or does not survive to settlement in [Marcelix]:

- private generations and non-public drafts
- public posts that are not reusable
- self-remixes
- remixes paid only with promo or bonus credits
- the promo-credit portion of a mixed paid-plus-promo remix
- remixes whose underlying paid purchase is later refunded, disputed, or reversed
- remix activity that is held for abuse review, coordinated farming, or payout-risk review

That is a deliberate choice. [Marcelix] is not rewarding derivative activity in the abstract. It is rewarding attributable reuse that is both paid and defensible.

## PayPal Settlement Is A Product Surface

The payout path in [Marcelix] is explicit:

1. Connect a PayPal payout destination.
2. Get that destination verified.
3. Wait for enough rewards to clear the pending window.
4. Submit a payout request.
5. Let the payout worker finalize, defer, reject, requeue, or reverse the request based on outcome.

[Marcelix] tracks a creator through meaningful economic states:

- pending
- available
- requested
- paid or reversed

That is the difference between a cosmetic wallet and an actual settlement system.

To request PayPal cashout, the creator needs:

- rewards that have cleared the pending window
- enough available balance to meet the minimum cashout threshold
- a verified PayPal payout destination
- an account in good standing with no active payout hold

## What Can Still Block Or Reverse Value

Even after a remix happens, [Marcelix] can still block, hold, reduce, or reverse value when:

- the underlying paid purchase is refunded
- the underlying paid purchase is disputed
- abuse patterns or coordinated reward farming are detected
- the account falls into policy or payout-risk review
- a payout has already been processed and the underlying transaction is later reversed

That is not a peripheral policy layer. It is part of the product contract. A creator economy that cannot defend itself does not stay an economy for long.

## Why This Is Not A Prompt Marketplace

Prompt marketplaces make the prompt the product.

[Marcelix] makes reuse the product.

That changes everything downstream:

- the public unit is the post, not the raw prompt
- derivative work stays inside the network
- provenance survives
- discovery can care about remixability
- creator value can come from downstream paid usage instead of prompt leakage or affiliate detours

That is what makes [Marcelix] feel closer to a creative graph than a static gallery.

## Public Product Surfaces

### Explore

The home feed is the discovery and reuse surface.

<img src="./assets/marcelix-home.webp" alt="Marcelix explore feed" width="100%" />

### Post page

A post page in [Marcelix] is both media distribution and an upstream remix node.

<img src="./assets/marcelix-post.webp" alt="Marcelix public post page" width="100%" />

### Rewards and settlement

[Marcelix] exposes reward lanes, the pending window, conversion, and PayPal cashout rules directly in the product.

<img src="./assets/marcelix-rewards.webp" alt="Marcelix creator rewards and payout rules" width="100%" />

## Why This Might Compound

A normal AI app produces outputs.

A normal social app produces attention.

[Marcelix] is trying to produce reusable creative supply.

If that works, one strong post can:

- pull in new followers
- become a reusable source
- generate a remix chain
- keep attribution attached to the origin
- create reward value when downstream paid reuse happens

That is the network effect [Marcelix] is betting on:

not more prompts,  
not more exports,  
but more reusable creative work that stays alive inside the network.

## In One Sentence

[Marcelix] is a bet that AI-generated images and videos should not end as disposable files; they should become reusable, attributable, feed-native, and economically connected social objects.

## Links

- Product: <a href="https://www.marcelix.com">marcelix.com</a>
- Creator Rewards: <a href="https://www.marcelix.com/creator-rewards">marcelix.com/creator-rewards</a>
- Public post example: <a href="https://www.marcelix.com/post/fa85a896d0d2/hajareddal-cartoon-trailer-the-blue-cat">cartoon trailer - The blue Cat</a>

[Marcelix]: https://www.marcelix.com
