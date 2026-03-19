---
title: 'Building for Someone You Love: VoiceScribe and Why This One Was Different'
date: 2026-03-21T09:00:00+01:00
draft: true
author: 'Puneeth Prakash'
description: 'I built VoiceScribe for my father, an author with failing eyesight. Here is what the project taught me about AI, engineering, and what we build when we really care.'

tags: ['AI', 'Claude', 'Side Projects', 'Career', 'Personal']
categories: ['Career & Learning']

toc:
  enable: true

menu:
  sidebar:
    name: '3. Building for Someone You Love'
    identifier: 'ai-evolution-part-3'
    parent: 'ai-evolution-series'
    weight: 493
---

_Part 3 of 3 in the series "How AI Changed the Way I Build Things"_

---

## The Real Reason I Built It

My father writes books.

He has for most of his adult life. He writes in Kannada, our mother tongue, and his process has always been a bit unconventional. He doesn't type well. His eyesight has been getting worse. So for years, his workflow looked like this: speak into his phone's voice-to-text, let it transcribe into a notes app, clean up what he can, send it to his editor, and the editor formats everything into chapters. Then repeat.

Hundreds of pages, done this way. Whole books.

I knew the process was clunky. His phone's voice recognition wasn't built for Kannada prose. The transcription was rough, full of dropped words and mangled sentences. My father would spend time cleaning it up, squinting at a screen he could barely read clearly. Sending files back and forth with his editor was tedious. There was no structure, no formatting, just raw text that someone else had to shape into something usable.

I'd been thinking about fixing this for a while. But "a while" is what happens to every good idea that doesn't have a deadline.

Then I started using Claude Code seriously. And I thought: what if I actually built this?

Not for a portfolio. Not for a hackathon. For my dad.

## What VoiceScribe Became

The idea, at its simplest: record your voice, get back a properly formatted document you can send to your editor.

The reality, as always, was more layered.

The app needed to handle audio recording directly in the browser, or accept uploaded files, things like MP3, M4A, WAV, the formats you end up with when you're recording on a phone. Files up to 100MB, because chapters aren't short. It needed real transcription, not phone voice-to-text quality, and it needed to work in Kannada, not just English.

I chose OpenAI's Whisper API for the transcription. It's genuinely good, $0.006 per minute of audio, and it supports Kannada. There's also the Bhashini API as a fallback for Kannada, a government-backed initiative specifically for Indian languages that handles some cases Whisper struggles with.

But transcription alone wasn't enough. Raw Whisper output is one long stream of text. No paragraphs. No structure. For an author, that's nearly useless.

So the app uses Whisper's word-level timestamps to infer paragraph breaks from pause timing. When there's a natural pause in speech, a breath between thoughts, that becomes a paragraph boundary. The app also does punctuation correction, detects spoken chapter markers ("Chapter One", "Chapter Two"), and handles spell check for both English and Kannada with a custom dictionary my father can add to over time.

The document editor had to be designed around an elderly user with poor eyesight. That means an 18px minimum base font, touch targets that are at minimum 48px so nothing is too small to tap, high contrast throughout, large buttons with clear labels, and a deliberately simple three-screen navigation. No clever UI patterns. No hidden menus. Just: record, review, send.

The output is a properly formatted PDF. A4 or Letter size, Times New Roman, double-spaced, with a table of contents automatically generated from detected chapter markers. Then the app emails it directly to his editor.

The tech stack ended up being React 19 with TypeScript on the frontend, using Material-UI and Tailwind. Node.js with Express on the backend, also TypeScript. SQLite for storage, Socket.IO for real-time transcription progress so you're not staring at a blank screen wondering if anything is happening. PDFKit for generating the documents. Nodemailer for the email delivery. Hosted for somewhere between $7 and $12 a month.

## The Repo Has a 1,075-Line Prompt File

I want to talk honestly about how this got built, because it's the whole point of this series.

VoiceScribe was built almost entirely with Claude and Claude Code. Not "I asked some questions and wrote the code myself." I mean: I had the idea, I had a clear picture of what I wanted, and I used AI to go from idea to working application, systematically.

The repository has a file called `prompt.md`. It's 1,075 lines long. It captures the full conversation that designed the architecture. Every significant decision in this app was made by thinking it through with Claude first.

What does "accessible" actually mean for an elderly user with failing eyesight, beyond generic WCAG compliance? We worked through that together. The Whisper versus alternatives comparison, including understanding exactly what Kannada support means in practice and where the limitations are. The paragraph detection algorithm, which relies on Whisper's timestamp data in a way I wouldn't have known to use without talking through the approach. The PDF generation strategy. How to make email delivery reliable on a privately hosted app. Security considerations for something running on a home network.

None of these were questions I Googled and assembled answers from. They were conversations. I explained what I was trying to do, what I was worried about, what constraints I was working under, and I got responses that were actually relevant to my situation.

The whole thing, from first conversation to a working application my father could use, was a weekend project.

## Where the AI Got It Wrong

I said I wanted to be honest.

Some things needed to be rethought after seeing them work in reality. The initial paragraph detection algorithm was a bit too aggressive. Whisper's pause timestamps are there, but the thresholds I started with were creating paragraph breaks in the middle of sentences where my father had paused to think, not because a new idea was starting. We tuned that.

The first version of the editor was still too complicated for someone not comfortable with technology. There were options that made sense to me as a developer, that gave useful control, but that just added confusion for the person actually using it. Simplicity needed a heavier hand than the first pass gave it.

And there were a few moments where Claude was confident about something that turned out to be subtly wrong. A library API that had changed. An assumption about how Whisper returns timestamp data that was slightly off from what I saw in practice. These things needed to be caught, questioned, verified.

You still need to know what you're building well enough to evaluate what you're being told. Eight years of engineering experience isn't irrelevant when you're using AI to build something. It's what lets you notice when something feels off.

## Why This One Felt Different

I've built side projects before. I built LongLeavePlanner because I was annoyed at a spreadsheet. I built a Scotland Yard board game tracker because the scope felt achievable over a weekend. Those projects were worth doing. I learned from them.

But I built VoiceScribe because my father was squinting at a phone screen, trying to read his own words.

That changes the texture of a project entirely.

When you build something for a person you love, every UX decision has a face attached to it. When I was thinking about font size, I was thinking about my father. When I was thinking about touch target size, I was thinking about his hands on the phone screen. When I was thinking about how to make the email delivery reliable, I was thinking about him sitting at his desk, trying to send a chapter to his editor, and not wanting anything to go wrong.

This is what good engineering has always been: knowing who you're building for. It just feels different when the person is real to you, immediately, not an abstract "user."

The AI helped me build it faster than I could have alone. But the reason it's _good_, the reason it actually fits my father's needs, is because I understood those needs at a level no AI can replicate. It knew about accessibility standards. I knew my father.

## What This Series Was Actually About

I started this series talking about getting unstuck faster on LongLeavePlanner. I ended up here, writing about building something real for someone I care about.

That arc is not accidental. It's what I've actually experienced over the past two years.

AI didn't make me a better engineer in the sense of teaching me things I didn't know. I still design the systems. I still make the architectural calls. I still debug the actual running code when something breaks in production at 11pm. I still need to understand what I'm building well enough to know when I'm being pointed in the wrong direction.

What AI did was reduce the friction between having an idea and being able to act on it.

The Scotland Yard tracker got built because the scope felt achievable over a weekend. VoiceScribe got built because a weekend project could become a real, working product that helped a real person. LongLeavePlanner shipped because getting unstuck was faster and the project stayed fun long enough to finish.

The cognitive load of holding all the decisions in your head at once is genuinely exhausting. Every experienced engineer knows this feeling: you're three weeks into a project, you're holding ten interrelated decisions in your head simultaneously, and the overhead of just _thinking_ becomes its own obstacle. Having something to think alongside you, something that holds context, that remembers what you said three conversations ago, that can reason through tradeoffs without getting bored. That's not a small thing.

The tools keep getting better. Faster, more accurate, more capable of holding context across larger projects. I don't know exactly where they're going.

What I do know is this: my father records his voice, the app transcribes it, and a properly formatted PDF goes to his editor. He didn't have to fight with a phone screen to make it happen. He just told his story.

That's enough for me.

---

## Resources

- [OpenAI Whisper API](https://platform.openai.com/docs/guides/speech-to-text)
- [Bhashini API for Indian languages](https://bhashini.gov.in/)
- [PDFKit documentation](https://pdfkit.org/)
- [Socket.IO documentation](https://socket.io/docs/)

---

Questions? Reach out at contact@puneeth.io
