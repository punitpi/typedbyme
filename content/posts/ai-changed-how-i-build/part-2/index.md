---
title: "I Didn't Plan to Use This Many AI Tools. Here's How It Happened."
date: 2026-03-20T09:00:00+01:00
draft: false
author: 'Puneeth Prakash'
description: 'From a single Copilot tab to a full pipeline of orchestrated agents. How my AI workflow grew one step at a time, without me really planning it.'

tags: ['AI', 'GitHub Copilot', 'Career', 'Learning', 'Productivity']
categories: ['Career & Learning']

toc:
  enable: true

menu:
  sidebar:
    name: '2. How It Happened'
    identifier: 'ai-evolution-part-2'
    parent: 'ai-evolution-series'
    weight: 492
---

_Part 2 of 3 in the series "How AI Changed the Way I Build Things"_

---

## The Moment It Moved Into the IDE

In [Part 1](/posts/ai-changed-how-i-build/part-1/), I wrote about using ChatGPT as a thinking partner on LongLeavePlanner. Useful. Genuinely useful. But there was still a gap: AI was in a browser tab, and my code was in the IDE (the Integrated Development Environment, the software where you actually write and edit code). Every time I needed help, I was switching contexts. Copy code, paste into chat, read response, switch back. The friction was low enough to be worthwhile, but it was still friction.

Then GitHub Copilot arrived in VS Code, and that gap closed.

This sounds minor. It wasn't. Having AI actually inside the IDE, watching what you type, aware of the file you're in and the files around it, is a different experience from having a chat window open beside it. Copilot didn't just autocomplete tokens. It autocompleted intent. You'd start writing a function signature and it would suggest the whole body, correctly, because it had context from the rest of your codebase. You'd type a comment describing what you needed and it would draft the implementation.

The workflow started changing. Not dramatically, not overnight, but it started.

## Then Agent Mode Changed Everything Again

Once I had Copilot in the editor, the natural next question was: what else can it do? And the answer kept expanding.

Agent mode in VS Code Copilot was the next step change. Instead of autocompleting the line you were on, you could give it a task: "Add input validation to all these route handlers," or "Write tests for this module." And it would go do it. Multiple steps. Multiple files. You'd review the result, ask it to adjust something, and it would iterate.

This felt qualitatively different from autocomplete. It wasn't filling in what you'd half-started. It was executing something you'd described in plain language. Past me would have spent an hour on that test scaffolding. Agent-mode me spent ten minutes reviewing what it produced and tweaking a few things.

I started thinking of this less as a tool and more as a pair programming partner with infinite patience and no strong opinions about indentation style.

## The CLI Arrived Next

Around the same time, AI started showing up in the terminal too. ChatGPT had Codex. Anthropic had Claude Code. GitHub had Copilot CLI.

The CLI tools moved AI out of the editor UI entirely and into the place where a lot of the actual work happens. You could describe a task in a prompt, and the tool would write code, run it, check the output, and iterate. Not in a chat window. In your actual project, in your actual terminal.

This was the point where I started to feel like my relationship with AI had genuinely shifted. It wasn't an assistant you consulted. It was something closer to a collaborator that could act on your behalf.

## My Toolkit Today

Right now, I have Claude, Gemini, GitHub Copilot, and ChatGPT. Some of these come through work, some I pay for personally. I've had a mix of both at different points in my career. When I was at OneAdvanced, the company provided GitHub Copilot, and that was the AI tooling we had in the editor.

I'm not going to do a feature-by-feature breakdown because honestly, the tools blur together depending on the task. What I'll say is this: I reach for different ones for different things.

**Gemini** is where I go first when I want to refine a prompt or think through a problem before committing to an approach. It's good at expanding a rough idea into something more considered.

**Claude Code** is what I use to plan architecture and then execute. It's thorough, it's careful, and it pushes back when something seems off.

**GitHub Copilot** lives in the editor and handles the in-flow stuff: autocomplete, drafting tests, filling in config I know the shape of but don't want to type from memory. No context switching required.

**ChatGPT** is where I do longer design conversations when I want to talk through multiple options.

None of these is universally best. Knowing which one to reach for is itself a skill I'm still developing.

## Where the Workflow Is Today: Orchestrated Agents

Here's what building a project looks like for me now, and it's a fair bit different from two years ago.

I start with a prompt. Not a detailed spec, just a clear description of what I'm trying to build and why. Then I'll use Gemini to expand and refine that prompt: fill in the gaps, surface questions I hadn't thought to ask, sharpen the constraints.

That refined prompt goes to Claude Code, which plans the architecture. And then things get interesting. Instead of one agent doing everything sequentially, I run multiple agents in parallel, each with a specific job:

- One to build the core implementation
- One to write tests
- One to do code review
- One to check visual quality (for anything with a UI)
- One to run a security review
- One to simplify the code where it's gotten unnecessarily complex
- A final agent to sign off on the whole thing

From a single well-formed prompt to a production-ready project, with all of these running together. The whole thing can move faster than I'd have believed possible two years ago.

That said, I still make the calls. The agents surface things, flag issues, produce drafts. I'm reviewing, deciding, redirecting. The orchestration speeds up execution. The judgment is still mine.

## Three Projects That Show the Progression

I want to trace this journey through three real things I built, because the abstract description of "the workflow evolved" doesn't quite convey what actually changed.

### Project 1: [my-express-template](https://github.com/punitpi/my-express-template)

This one I built the old-fashioned way, about five years ago. Every line of code written by hand, no AI anywhere near it. This is what I would have called "normal" back then.

I was creating a lot of projects at the time and kept setting up the same Express scaffolding from scratch. So I built a boilerplate to stop repeating myself.

The thing about building a boilerplate is that the hard part isn't the code. It's the decisions. What goes in by default? How opinionated should it be? If I clone this in a year, will it be a helpful starting point or an annoying set of assumptions I have to unpick?

I figured it out by doing. Made my own calls, got some of them wrong, iterated. The result is a template I've actually used as the foundation for other projects since. No AI involved, no shortcuts. Just me thinking through what I'd want every time I started something new.

### Project 2: [Scotland Yard Tracker](https://github.com/punitpi/scotland-yard-tracker)

[Scotland Yard Tracker](https://github.com/punitpi/scotland-yard-tracker) is a full-stack app for tracking Mr. X's movements in the board game Scotland Yard in real time. React frontend, Node.js and Express backend, MongoDB, Socket.IO for live sync across all connected devices.

This one has a longer history than it looks. I started building it four or five years ago, the traditional way: wrote a lot of the logic by hand, got a decent chunk done, then abandoned it. Life got in the way. The project sat.

When I decided to revive it, I came back with a different toolkit. I'd been using ChatGPT for ideas and to help me think through how to describe what I wanted, which at the time was new territory. I didn't really know what good prompt writing looked like yet. I was figuring it out as I went.

I used GitHub Copilot in agent mode in VS Code to build the first working version. Not as an autocomplete tool. As a builder: give it a task, review what comes back, steer it toward what I actually wanted. This was genuinely different from how I'd worked before. I wasn't writing the code myself and getting help when stuck. I was directing the build and editing what was produced.

Then I brought in Claude Code to improve it further: cleaning up the architecture, tightening the real-time sync logic, making it something I was actually happy with.

The finished version is much better than anything I'd have shipped on my own in the same amount of time. But the story of how it got there is also a map of how my workflow changed.

### Project 3: [Spotify Now Playing](https://github.com/punitpi/spotify-now-playing)

[Spotify Now Playing](https://github.com/punitpi/spotify-now-playing) is a lightweight proxy service that connects to Spotify's API and exposes your currently playing track as a simple JSON endpoint. I added it to this site recently, and if you look at the top of any page, you can see it working.

This one was built just a week or so before writing this post, and it's the clearest example of what the modern orchestrated workflow looks like. Refined prompt, architecture plan, then a set of parallel agents handling implementation, tests, code review, and security in parallel. It came together faster than any comparable project I've built.

There are no production dependencies. The core logic is decoupled from the runtime, so it runs on Cloudflare Workers, Node.js, and Docker with no code changes between them. That kind of clean architecture isn't something I'd have arrived at as quickly working alone. Having dedicated agents focused on review and simplification caught things I'd have only noticed later.

## The Honest Part

Agent mode gets things wrong. Confidently, sometimes.

I've had it produce code that looked clean on first read and had a subtle bug that took longer to find than writing it from scratch would have taken. I've had it over-engineer solutions, under-engineer others, and occasionally go in a direction that was technically reasonable but completely wrong for my context.

The skill here isn't just using the tools. It's knowing when to trust them and when to push back. That requires enough domain knowledge to evaluate what you're getting. A senior engineer using agent mode is a different thing from a junior engineer using agent mode, and not just because the output gets filtered more carefully. The direction-setting is different too.

There are also tasks where closing the chat window/terminal and thinking quietly is the right move. Not every problem benefits from a conversation. Some just need you.

## What Actually Shifted

The biggest change over the past two years isn't the tools. It's the posture.

AI started in a browser tab I'd open when I was stuck. Then it moved into my editor. Then into my terminal. And now into coordinated pipelines that can take a prompt and return something production-ready.

Each of those steps changed how I work, not just how fast I work. The questions I ask up front are different. The amount of time I spend on execution versus direction is different. The things I consider to be "my job" versus "something the agents handle" keep shifting.

I don't think that's a bad thing. But it's worth being clear-eyed about. The craft isn't gone. The judgment is still yours. The accountability is still yours. What's changed is the leverage.

## TL;DR

The shift from Part 1 to here isn't just more tools. It's a different relationship with what building something means.

- **AI moved into the workflow**: from browser tab, to editor, to terminal, to orchestrated pipelines. Each step reduced friction and raised the ceiling on what's practical to attempt.
- **The best projects used AI at multiple stages**: design conversations before writing, agents during execution, review and simplification afterward.
- **The judgment stays with you**: agents can build fast, but direction, evaluation, and the final call are still yours.

### Up Next: Part 3

**Part 3 is the most personal one.** It's about a project I built for my father, VoiceScribe, and what that project taught me about the gap between technically working and actually useful. My father is an author with failing eyesight who writes in Kannada. The brief was simple. The build got complicated quickly. And AI played a different role in it than it had in any of the projects I've written about here.

---

## Resources

- [my-express-template on GitHub](https://github.com/punitpi/my-express-template)
- [scotland-yard-tracker on GitHub](https://github.com/punitpi/scotland-yard-tracker)
- [spotify-now-playing on GitHub](https://github.com/punitpi/spotify-now-playing)
- [GitHub Copilot documentation](https://docs.github.com/en/copilot)
- [Claude Code documentation](https://docs.anthropic.com/en/docs/claude-code)

---

Questions? Reach out at contact@puneeth.io
