---
title: 'From Stack Overflow to ChatGPT: How I Built My First AI-Assisted Project'
date: 2026-03-19T09:00:00+01:00
draft: false
author: 'Puneeth Prakash'
description: 'How I used ChatGPT as a thinking partner to build LongLeavePlanner, and what actually shifted in my workflow as an engineer.'

tags: ['AI', 'ChatGPT', 'Career', 'Learning', 'Node.js']
categories: ['Career & Learning']

hero: images/posts/ai-changed-how-i-build-part-1/hero.jpg

toc:
  enable: true

menu:
  sidebar:
    name: '1. From Stack Overflow to ChatGPT'
    identifier: 'ai-evolution-part-1'
    parent: 'ai-evolution-series'
    weight: 491
---

_Part 1 of 3 in the series "How AI Changed the Way I Build Things"_

---

## It Wasn't Magic. It Was a Better Conversation.

About two years ago, I paid for a ChatGPT subscription myself. My company wasn't offering any AI tooling at the time, and that didn't change until almost the end of 2025. I had this side project idea rattling around in my head, one of those itch-you-can't-scratch problems, and I figured it was a decent excuse to try out this AI thing everyone was talking about.

Here's the thing: I actually built it in Rishikesh, November 2024. I'd taken a long weekend to go solo backpacking, partly to clear my head, partly because I just needed to be somewhere that wasn't a desk in an office. I ended up in a cafe by the ghats, laptop open, chai going cold next to me, and I just... started building. There's something fitting about that. I was on leave, and I was building an app to help people plan their leave better.

I want to be upfront about something: I didn't walk away from that project thinking "AI is going to change everything." I walked away thinking "huh, that was actually a nicer way to get unstuck." That's a smaller, less dramatic story. But I think it's the honest one.

## The Problem I Was Trying to Solve

If you work in a country with a decent number of public holidays, you've probably played this game before. You stare at the calendar, trying to figure out if you take just _these_ two days off, do you get an eight-day weekend? Can you bridge that gap between the bank holiday on Thursday and the weekend?

I was doing this manually every year, on a spreadsheet, like some kind of leave-planning archaeologist. It worked, but it was tedious. So I decided to build LongLeavePlanner.

The idea was simple: you upload your company's bank holidays, and the app figures out which one or two days you should apply for leave to connect those holidays with nearby weekends. Maximum time off, minimum leave days burned. The algorithm groups consecutive holidays and weekends, looks for small gaps of one or two days, and tells you exactly which days to apply for. The UI colour-codes the result: green for days you're already off, yellow for "apply leave here."

I built it with Node.js and Express.js on the backend, and FullCalendar and Flatpickr for the frontend. Nothing exotic. The kind of stack you'd reach for without thinking too hard.

## My Workflow Before ChatGPT

Here's what problem-solving looked like before, and I'm guessing this sounds familiar.

Hit a problem. Open a new browser tab. Type a search query that's half-English, half-code. Land on a Stack Overflow thread from 2014. Read the top answer. Notice it's for a slightly different version of the library. Read the second answer. Check the comments. Someone says the accepted answer has a security flaw. Open three more tabs. Piece it together. Try it. It half-works. Repeat.

This workflow isn't bad, exactly. It built good instincts. You learn to triangulate answers, to read documentation sceptically, to understand that context matters enormously in software. I wouldn't trade those years.

But it was slow. And it was lonely, in a way. You were always filtering through answers written for someone else's problem, in someone else's context, with someone else's stack.

## What Actually Changed

When I started using ChatGPT on LongLeavePlanner, the workflow shifted. Instead of searching for fragments and assembling them, I could just explain my situation.

Not "FullCalendar custom event rendering," but: "I'm building a leave planner with FullCalendar and I want to colour-code events differently based on whether they're bank holidays, recommended leave days, or just weekends. Here's what I have so far."

And then I'd get something back that was actually responsive to _my_ problem. Not a generic answer. Not a Stack Overflow post that was 70% relevant. A reply that accounted for what I'd told it.

What I was doing was less "generate my code" and more "think alongside me." I still wrote most of the code. I still made the architectural decisions. But when I hit a wall, instead of going spelunking through documentation and old forum threads, I could just ask a question in plain English and get a contextual response I could interrogate.

The follow-up is where it got genuinely useful. You can't follow up on a Stack Overflow answer. You can't say "okay but what if I'm using this version, and also I need to handle this edge case." With ChatGPT, that back-and-forth was suddenly possible. It changed the texture of getting unstuck.

## A Concrete Example

The trickiest part of LongLeavePlanner was the gap-filling algorithm. The core logic: given a list of holidays and weekends, find clusters of consecutive days off, then identify small gaps between clusters (one or two working days), and flag those gaps as candidates for leave recommendations.

This isn't a hard algorithm. But I hadn't written something like it before, and I wasn't immediately sure of the cleanest way to model it. Date manipulation in JavaScript has a way of turning a simple idea into a surprisingly fiddly implementation.

I described the problem to ChatGPT. I explained what I was trying to do and what I'd already tried. It walked me through a way to model the calendar as a set of date ranges, showed me how to sort and merge overlapping ranges, and then explained how to detect small gaps between ranges. It explained the _why_, not just the code.

I didn't copy and paste the solution. I read through it, understood the approach, then implemented it myself with my own variable names and my own edge case handling (turns out bank holidays on Mondays and Fridays need special attention if you want the recommendations to actually make sense).

But the conversation got me unstuck in maybe twenty minutes instead of two hours. That felt significant.

## The Thing Nobody Tells You

Here's something I didn't expect: ChatGPT made me a better asker of questions.

When you're searching Stack Overflow, you can get away with a vague query. "FullCalendar event colour" returns results. Some of them are useful. But you haven't had to think very clearly about what you actually need.

When you're talking to ChatGPT, the quality of your explanation directly affects the quality of what you get back. You have to think about your problem clearly enough to articulate it. You have to provide context. You have to describe what you've already tried and why it didn't work.

That process, before you even get a response, is genuinely useful. Rubber duck debugging has always worked for the same reason. ChatGPT is just a rubber duck that talks back.

I noticed I was getting better at describing problems. Which, not coincidentally, is also one of the most important skills in software engineering.

## What Didn't Change

I want to be honest about the limits too.

I still hit situations where ChatGPT gave me confidently wrong answers. Version-specific stuff was a common offender. It would explain how to do something in a library, and I'd discover the API it described had changed two major versions ago. It's gotten better at this, but it's not gone.

I still needed to understand what I was building well enough to evaluate the answers. A junior engineer who doesn't yet have that foundation would have a harder time knowing when to trust the output and when to push back. That context, built over years, still matters.

And the debugging loop was still on me. ChatGPT can suggest hypotheses. It can say "this sounds like it might be a timezone issue" (and honestly, it usually is). But tracking down the actual bug, in your actual running code, is still your job.

AI didn't remove the craft. It just made some of the in-between bits faster.

## So What Actually Shifted?

The metaphor I keep coming back to is this: before, getting help felt like going to a library. You could find the answer if you searched well enough, but you had to navigate the stacks yourself, and nothing knew what you were actually looking for.

With ChatGPT, it felt more like having a knowledgeable colleague one Slack message away. Not a colleague who'd do the work for you, but one you could think out loud with. One who'd respond to what you actually said, not what you'd managed to encode into a search query.

For LongLeavePlanner, that meant I shipped something. Not because the AI wrote the code, but because I got unstuck faster. The friction of building was lower. That matters, especially on side projects, which die a quiet death the moment they stop being fun.

## Conclusion

This wasn't a story about AI doing the work. It was about finding a better thinking partner for the moments when you're stuck.

Here's what actually changed for me:

- **Getting unstuck faster**: The back-and-forth of a conversation beats assembling fragments from ten browser tabs.
- **Asking better questions**: Having to explain your problem clearly to get a useful answer is a skill, and it transfers everywhere.
- **Shipping things**: Lower friction means side projects survive long enough to become something real.

The craft is still yours. The decisions, the debugging, the judgment calls, none of that moved. What changed was the quality of the conversation you can have when you hit a wall.

### What's Next

This is Part 1 of a three-part series. **Part 2 goes deeper.** By the time I'm writing it, my use of AI has changed again. It's no longer just answering questions. I'm starting to use it differently, closer to a co-pilot than a reference tool. That shift, what prompted it, what it looks like day-to-day, and where it starts to feel uncomfortable, is what the next post is about.

---

**P.S.** There's a certain irony to this post that I feel obliged to acknowledge. LongLeavePlanner, the project that started all of this, has since been completely rebuilt. Not tweaked. Rebuilt. The Node.js, Express, and FullCalendar stack described above is now sitting on a `backup/main` branch, preserved like a very small fossil.

The new version is Next.js 14 with the App Router, TypeScript, Tailwind CSS, proper test coverage with Vitest, server-side caching, rate limiting, and deployment on Vercel with analytics. You can try it at [leavewise.puneeth.io](https://leavewise.puneeth.io/). It's the kind of project I'd have taken weeks to scope and plan before. This time, it happened faster and with far more confidence because of the workflow I describe in Parts 2 and 3 of this series.

So the project that taught me AI could be a better thinking partner has now become a showcase of exactly how that thinking evolved. I find that genuinely funny. Past me, sitting in that cafe in Rishikesh with cold chai and a half-working FullCalendar integration, would not have predicted it.

The old code is still there if you're curious. Consider it a before photo.

---

## Resources

- [LongLeavePlanner on GitHub](https://github.com/punitpi/longleaveplanner)
- [LongLeavePlanner (live)](https://leavewise.puneeth.io/)

---

Questions? Reach out at contact@puneeth.io
