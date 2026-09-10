---
name: linkedin-post
description: Draft a LinkedIn post announcing a typedbyme blog post, with a hook, key takeaways, and a link to the live post. Invoked explicitly when Puneeth is ready to announce a post, not automatically after writing one.
disable-model-invocation: true
---

# LinkedIn Post for a Blog Announcement

Draft a LinkedIn post that announces one of Puneeth's blog posts at typedbyme.puneeth.io. This is
invoked deliberately, when he's decided a post is ready to announce, not automatically right
after a post is drafted (drafting and announcing happen on different timelines).

## Input

The user will name a post (by slug, title, or path under `content/posts/`). Read that post's
frontmatter and content before drafting anything.

## Voice

Distinct from the blog's voice: LinkedIn posts are shorter, punchier, hook-first. Still
first-person, still conversational, no em dashes (same rule as the blog). Avoid corporate
LinkedIn cliches ("I'm thrilled to announce", "Excited to share").

## What Actually Drives Engagement (Researched, Not Guessed)

Most "LinkedIn growth hack" advice online is unverified SEO-farm content that cites itself in
circles (2-3 hashtags, exactly 2 emojis, post at 8am Tuesday, etc.) — ignore that tier entirely.
What follows is graded by source quality; weight it accordingly.

**From LinkedIn's own engineering blog** ("Leveraging Dwell Time to Improve Member Experiences,"
linkedin.com/blog/engineering/feed/understanding-feed-dwell-time — the actual ranking mechanism,
highest-confidence source):
- Ranking runs on a `P(skip)` model: the algorithm predicts whether a member will skip an update
  and downranks it proportionally. It does **not** reward specific formatting tricks — it
  penalizes being skipped.
- Two dwell signals matter: time spent on the post while scrolling the feed, and time spent after
  a click. A post someone actually reads for 30 seconds beats one that gets 50 quick likes and a
  0-3 second glance.
- Ranking also weighs the member's historical affinity to the specific author, not just the post
  in isolation. Consistency with an audience compounds; this isn't a one-shot optimization.
- The post explicitly does not claim any format, length, or hook produces more dwell time — don't
  attribute that claim to LinkedIn itself.

**From independent data analyses** (Dr. Daniel Usera, UT Arlington, random sample of 991 posts;
a LinkedIn consultant's self-analysis of 1,000 of their own posts — moderate confidence, real
data but not causal proof):
- **Tagging specific people beats hashtags** for both reactions and comments — it pulls people
  into the conversation and extends reach through their network. Use this when a post can
  genuinely tag someone relevant (a tool's maintainer, a person mentioned in the story) — don't
  tag people who aren't actually part of the story.
- **Posts about others outperform self-promotion.** Gratitude and crediting other people's work
  beat "I did this" framing. A blog-announcement post is inherently self-promotional, so lean the
  hook toward the story/struggle rather than the announcement itself.
- **Personal stories won decisively** over "contrarian take" or generic industry-observation
  angles, in both datasets.
- **Specific, tension-driven openings beat vague ones.** "Strong posts led with particularity or
  tension rather than vague observations" — open mid-scene or with a concrete, odd detail, not a
  summary statement.
- **901-1,200 characters was the best-performing band** in the 1,000-post analysis (averaged
  107.6 engagements). Treat this as a reasonable target, not a hard rule — don't pad a post to
  hit it, and don't cut a good draft short to stay under it.
- **Visual format outperformed text-only** in that same dataset. Attach the post's actual hero
  image (from `assets/images/posts/<slug>/hero.jpg`) as an uploaded image, not a bare link that
  relies on LinkedIn's auto-generated link-preview card.

## Template

```
[Hook - 1-2 sentences, specific and story-driven, that stand alone without needing the link.
Open mid-scene or with a concrete odd detail from the post's actual story, not a generic teaser
or a summary of the topic.]

I just published a post on [topic]. [1 sentence bridging the hook to why this is worth reading,
not a bare "here's what's in it" list unless the post genuinely is a list-shaped how-to.]

• [Key takeaway 1 - specific, drawn from the post's actual content]
• [Key takeaway 2]
• [Key takeaway 3]

[One sentence of personal insight or the post's core lesson - this is often the line worth
quoting, so make it count]

Read the full post: [live URL, https://typedbyme.puneeth.io/posts/<slug>/]

#Tag1 #Tag2 #Tag3
```

- Pull the 3 key takeaways from the post's actual headers/content, not generic restatements of
  the title.
- Pull hashtags from the post's `tags` frontmatter field, formatted without spaces. Keep it to a
  handful — hashtags are a minor signal next to tagging real people when applicable.
- If there's a real person or maintainer to credit (a tool's author, someone who inspired the
  post), consider tagging them per the research above, but only if it's genuinely warranted by
  the story, never as a growth tactic tacked on.
- Aim for roughly 900-1,200 characters as a loose target, not a hard cutoff.
- Use the real live URL (`https://typedbyme.puneeth.io/posts/<slug>/`) — confirm the slug matches
  the post's filename or `menu.sidebar.identifier` as used elsewhere on the site, and confirm the
  post is actually merged to `main` and live before handing over the link (ask the user if unsure
  rather than assuming).
- Remind the user to attach the post's hero image to the LinkedIn post itself (not just rely on
  the link preview), per the visual-format finding above.

## Output

Output the draft directly in chat for review. Don't publish it anywhere or post it — this skill
only drafts the text.
