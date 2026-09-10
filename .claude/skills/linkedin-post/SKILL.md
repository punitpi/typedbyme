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

## Template

```
[Hook - 1-2 sentences that stand alone without needing the link, drawn from the post's actual
angle or story, not a generic teaser]

I just published a post on [topic]. Here's what's in it:

• [Key takeaway 1]
• [Key takeaway 2]
• [Key takeaway 3]

[One sentence of personal insight or the post's core lesson]

Read the full post: [live URL, https://typedbyme.puneeth.io/posts/<slug>/]

#Tag1 #Tag2 #Tag3
```

- Pull the 3 key takeaways from the post's actual headers/content, not generic restatements of
  the title.
- Pull hashtags from the post's `tags` frontmatter field, formatted without spaces.
- Use the real live URL (`https://typedbyme.puneeth.io/posts/<slug>/`) — confirm the slug matches
  the post's filename or `menu.sidebar.identifier` as used elsewhere on the site, and confirm the
  post is actually merged to `main` and live before handing over the link (ask the user if unsure
  rather than assuming).

## Output

Output the draft directly in chat for review. Don't publish it anywhere or post it — this skill
only drafts the text.
