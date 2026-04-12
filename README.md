# Marcelix Creator Guide

Marcelix is a creator network for AI images, short videos, reusable templates, remixes, and Creator Rewards.

## The core idea is simple:

1. Create an image or video.
2. Publish it as a reusable post.
3. Other creators remix it.
4. Your best reusable ideas can keep earning attention, followers, and rewards over time.

This guide explains how Marcelix works from a creator point of view: how discovery works, how remixing works, how prompt privacy works, how rewards work, and how to create posts that people actually want to remix.

Private implementation details, exact pricing, provider names, internal scoring weights, infrastructure secrets, and reward formulas are intentionally not included here. The app shows the current credit and reward values directly inside the product.

## Why Marcelix Exists

Most AI tools stop after generation. You type a prompt, get an image or video, download it, and leave.

Marcelix is built around a different loop:

```text
create -> publish -> discover -> remix -> reward -> repeat
```

Instead of treating generations as isolated files, Marcelix treats good generations as reusable creative starting points.

A post can become:

- a visual idea people like
- a template other users remix
- a trend seed
- a style people recognize
- a reason for people to follow you
- a reward source when eligible remixes happen

The most successful creators on Marcelix are not only making good images. They are making ideas that other people want to use.

## The Basic Flow

### 1. Generate Privately

Every generation starts as a private draft. That means you can experiment without publishing unfinished work.

You can use private drafts to:

- test prompts
- compare styles
- prepare stronger titles
- write better descriptions
- decide whether the prompt should be public or hidden
- publish only the versions that are worth showing

Private drafts are for your own workflow. Public posts are for discovery.

### 2. Publish Publicly

When you publish, Marcelix asks for the parts that help people understand and find the post:

- title
- description
- tags
- remixability
- prompt visibility

If you hide the prompt, the description becomes more important. A hidden prompt post still needs public context so people can discover it, understand it, and decide whether to remix it.

Good description:

```text
A cinematic retro-future racing poster with neon rain, chrome cars, and a dramatic city skyline.
```

Bad description:

```text
ultra detailed 8k prompt text, exact camera recipe, full private prompt...
```

The description should explain the result, not leak your prompt.

### 3. Let People Remix

If a post is reusable, other creators can use it as a starting point.

Remixing is designed to feel simple:

```text
source template + user's edit idea -> new private draft -> optional public remix
```

The original template stays linked, so the creator of the source can benefit from downstream activity.

## Prompt Privacy

Prompt privacy is one of the most important parts of Marcelix.

### Original Posts

When you publish an original post, you choose whether the prompt is public or hidden.

Public prompt:

- viewers can see the prompt
- useful for educational posts
- useful when you want people to learn from your process
- useful when the prompt itself is part of the value

Hidden prompt:

- public viewers do not see the prompt
- remixers do not receive the source prompt in the browser
- the creator can still see/copy their own prompt in private owner tools
- the public post relies on title, description, tags, and visuals for discovery

### Remix Posts

Remix posts keep prompts hidden automatically.

That means:

- the original baseline is not exposed
- the remixer's edit prompt is not exposed publicly
- the published remix page does not show prompt text
- the remixer can still see their own remix edits in private creator tools

This protects both sides:

- the original creator's reusable idea
- the remixer's added direction

### Private Drafts

Private drafts are different from public posts.

Inside a private draft, the creator can still see and copy their own prompt or remix edits. This is for workflow, not public display.

The rule is:

```text
public surface: protect hidden prompts
private owner tools: let the creator manage their own prompt
```

## Recommendation Logic

Marcelix discovery is designed to reward posts that people actually interact with, not just posts that are new.

The feed looks at several categories of signals:

- freshness
- engagement
- saves
- comments
- remix activity
- creator follows
- tag follows
- post quality signals
- safety and moderation status
- whether a post is reusable
- whether the post has enough public context when the prompt is hidden

The exact scoring is private and may change over time, but the general idea looks like this:

```ts
type DiscoverySignals = {
  freshness: number;
  engagement: number;
  remixMomentum: number;
  creatorAffinity: number;
  tagAffinity: number;
  quality: number;
  safety: number;
};

function rankPost(signals: DiscoverySignals) {
  if (signals.safety <= 0) return 0;

  return (
    signals.freshness +
    signals.engagement +
    signals.remixMomentum +
    signals.creatorAffinity +
    signals.tagAffinity +
    signals.quality
  ) * signals.safety;
}
```

For creators, the lesson is simple:

```text
make people stop, react, save, comment, follow, and remix
```

The best Marcelix posts usually do at least one of these:

- look instantly shareable
- match a current online mood
- make people laugh
- make people imagine themselves inside the concept
- solve a creative need
- offer a reusable transformation
- create a style that others want to apply to their own face, pet, brand, product, or story

## Creator Rewards

Creator Rewards are designed to reward useful reusable work.

At a high level:

1. You publish a reusable post.
2. Another creator remixes it.
3. If the remix meets eligibility rules, a reward event can be created for you.
4. Rewards go through a pending period.
5. After clearing, available rewards can be used in supported ways inside Marcelix.

The app can support reward actions like:

- converting eligible rewards into credits
- requesting payout when requirements are met
- tracking pending, available, held, converted, requested, and paid states

Exact rates, thresholds, timing, and payout rules are shown inside the app and may change as Marcelix grows.

Important: rewards are not guaranteed income. They depend on eligible remix activity, platform rules, payment status, fraud checks, refunds, reversals, and payout availability.

## How To Earn More Attention And Rewards

The best strategy is not to only make beautiful images. The best strategy is to build a remix loop.

Think in two phases.

## Phase 1: Build Attention

First, make posts people want to look at, like, save, and share.

Good early content types:

- memes
- funny visual reactions
- clean profile-picture ideas
- dramatic poster concepts
- trend-based images
- before/after concepts
- aesthetic wallpapers
- pet transformations
- fashion looks
- cinematic portraits
- short video loops
- visual jokes around a current topic

The goal of Phase 1 is to earn:

- follows
- likes
- saves
- comments
- profile visits
- recognition

Use tags honestly. If your post is about animals, use animal-related tags. If it is a fashion portrait, use fashion tags. If it is a short video loop, make that clear.

Do not spam irrelevant tags. It may get clicks once, but it weakens trust.

### Phase 1 Example

Instead of:

```text
cool image
```

Try:

```text
Tiny cat CEO announcing a chaotic company meeting in a glass skyscraper
```

Why it works:

- clear subject
- funny situation
- easy to understand
- shareable
- remixable into other animals, jobs, or locations

## Phase 2: Build Remix Engines

Once people recognize your work, start publishing posts designed to be remixed.

A remix engine is a post where another person can easily imagine uploading a reference, changing one detail, and getting something personal.

Strong remix-engine formats:

- face-to-theme transformations
- outfit transformations
- pet poster transformations
- profile-picture filters
- video effects
- cinematic intro clips
- sports-card style portraits
- magazine cover styles
- album-cover styles
- retro game character looks
- fantasy character upgrades
- old-me / young-me emotional concepts
- glow-up edits
- product mockup styles
- creator brand templates

The key question:

```text
Can another person make this about themselves in one sentence?
```

If yes, it can become a strong remix template.

## Remix Ideas That Can Travel Online

Use culturally familiar formats without copying protected characters, logos, or exact copyrighted designs.

Better:

```text
open-world crime game poster energy, neon city, dramatic pose, custom outfit
```

Risky:

```text
make me the exact main character from a famous game with the real logo
```

Better:

```text
superhero comic cover energy, bold ink, dramatic skyline, original costume
```

Risky:

```text
make me an exact famous superhero
```

Better:

```text
pirate-anime adventure poster style, ocean wind, original crew outfit, bright expressive colors
```

Risky:

```text
make me a specific copyrighted anime character
```

Better:

```text
romantic ocean-era movie poster mood, elegant formal clothing, golden sunset, original characters
```

Risky:

```text
copy a famous movie poster exactly
```

This keeps your content more brand-safe, more platform-safe, and more remixable.

## What Makes A Post Remixable

A strong remixable post usually has:

- a clear transformation
- a strong visual promise
- a simple title
- a description people understand quickly
- tags that match the use case
- a result that looks good even before reading the prompt

Examples:

```text
"Turn your pet into a royal oil painting"
```

```text
"Make your selfie look like a cinematic racing poster"
```

```text
"Create a dreamy young-me-meets-future-me portrait"
```

```text
"Convert a product photo into a luxury ad campaign frame"
```

```text
"Make a 5-second neon intro from a single portrait"
```

These are strong because the viewer immediately understands what they can do with it.

## How To Write Better Titles

Your title should sell the result, not describe every technical detail.

Good titles:

- Neon Rain Racing Poster
- Royal Pet Portrait
- Future Me Hugging Young Me
- Cyberpunk Fashion Cover
- Dream Kitchen Product Ad
- Anime Adventure Crew Portrait
- Vintage Sports Card Hero Shot

Weak titles:

- My image
- Test generation
- Prompt 44
- Cool style
- Remix this please

## How To Write Better Descriptions

Descriptions help people understand your post when the prompt is hidden.

Good description:

```text
A cinematic profile-poster concept for turning a portrait into a neon racing character with rain, motion blur, and a dramatic city backdrop.
```

Why it works:

- explains the result
- does not expose the full prompt
- helps search and discovery
- tells remixers what the template is for

Weak description:

```text
full prompt pasted here with every private detail
```

The public description should be a user-facing explanation, not your private recipe.

## How To Use Tags

Tags help the right audience find the post.

Use tags that describe:

- subject
- style
- format
- use case
- community interest

Examples:

- `#Fashion`
- `#Anime`
- `#Animals`
- `#Travel`
- `#Architecture`
- `#Food`
- `#Fantasy`
- `#Realistic`
- `#Artistic`
- `#Abstract`

If you share externally, match the external audience too.

For example:

- AI art communities
- creator communities
- meme communities
- design communities
- pet communities
- fashion communities
- short-video communities

Do not spam. Share where the content actually fits.

## External Sharing Strategy

Marcelix posts are strongest when they leave Marcelix and come back with new users.

Good places to share:

- your Instagram page
- short-video platforms
- Reddit communities that allow AI content
- Discord creator groups
- design communities
- personal newsletters
- group chats
- portfolio pages

When sharing externally, do not only say "check my post."

Say what the person can do with it:

```text
I made a remixable template that turns a portrait into a neon racing poster. Try it with your own selfie.
```

That is more effective because it gives people a reason to click.

## The Best Creator Loop

Use this loop:

1. Publish eye-catching posts.
2. Watch which ones get saves, comments, and remixes.
3. Turn winners into clearer reusable templates.
4. Share those templates externally.
5. Reply to comments and remixers.
6. Make sequels based on what people actually use.
7. Repeat.

In practice:

```text
post 10 ideas -> find 2 winners -> make 5 variations -> share the best one -> repeat
```

## Safety And Trust

Marcelix is built for mainstream creative use.

Avoid:

- unsafe sexual content
- hateful or abusive content
- impersonation
- copying private people without permission
- exact copyrighted characters or logos
- misleading political or medical claims
- harassment
- illegal content

Good creative work lasts longer when it is safe to remix and safe to share.

## Why Hidden Prompts Matter

Hidden prompts let creators publish strong work without giving away every detail.

That matters because creators often spend time learning:

- wording
- structure
- style direction
- composition language
- remix patterns
- reference strategy

Marcelix lets creators share the result and keep the recipe private when they want.

At the same time, public prompts remain useful for creators who want to teach, share, or build openly.

The creator chooses for original posts. Remix posts stay protected automatically.

## A Simple Creator Plan

If you are new, start here:

### Day 1

- Make 5 public posts.
- Use clear titles.
- Use honest tags.
- Hide prompts unless you want to teach.
- Add real descriptions.

### Day 2

- Check which posts got reactions.
- Make 3 variations of the strongest idea.
- Share one externally.

### Day 3

- Create one remix-engine template.
- Make the result personal and easy to understand.
- Use a title that tells people what they can become or create.

### Week 1

- Keep publishing.
- Watch what people remix.
- Make more of what people actually use.
- Build a recognizable style.

## Final Idea

Marcelix rewards creative leverage.

One normal post can get a like.

One strong reusable post can become a template.

One strong template can become a remix chain.

One remix chain can become a creator loop.

That is the product:

```text
make something people want to use, not just something people scroll past
```

