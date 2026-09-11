---
title: 'Treating My Resume Like a CI/CD Pipeline'
date: 2026-09-10T09:00:00+02:00
draft: false
author: 'Puneeth Prakash'
description: 'How years of failed attempts to learn LaTeX ended with a resume that builds and deploys itself, the same way I ship software.'

tags: ['LaTeX', 'CI/CD', 'GitHub Actions', 'DevOps', 'Career', 'Open Source']
categories: ['Career & Learning']

hero: images/posts/treating-my-resume-like-a-cicd-pipeline/hero.jpeg

toc:
  enable: true

menu:
  sidebar:
    name: 'Resume as a Pipeline'
    identifier: 'resume-as-cicd-pipeline'
    weight: 495
---

## TL;DR

This is a decade-long story more than a how-to, so if you just want the setup, [skip straight to how it actually works](#how-it-actually-works). Otherwise, here's the short version:

- I failed to learn LaTeX for close to a decade, every attempt died from trying to master it end to end before writing a single line.
- I used Novoresume, then RxResume (open source), for every resume until now, and both got the job done.
- Watching my wife fight a paid resume builder, then losing track of my own current resume, is what actually pushed me to fix this.
- `my-resume` treats a resume like RaC, resume as code: a push to `main` compiles it with XeLaTeX, publishes it as a GitHub release, and syncs the PDF into this site automatically.
- A separate private build adds my phone number, kept out of anything public by construction, not by remembering to redact it.
- I built the same setup for my wife, producing an English and a German version instead of a public and private one.

## The Long Version

After 12th, I wrote CET (Common Entrance Test) and got into an engineering college for Computer Science. Before classes started, I went to see a relative for some life advice, the kind of relative who felt more like an elder brother than a distant name at family functions. He was already a software engineer, and he sat me down and gave me a short list of things to learn. SQL made sense. A programming language made sense. Then he told me to learn LaTeX, and to this day I have no idea why that one came up. But out of everything he said that day, LaTeX is the one that stuck with me the hardest.

That one piece of advice followed me around for close to a decade. And for most of that decade, I failed at it.

## The Zero-to-Expert Trap

Here's the thing about learning LaTeX (a typesetting system people use to produce documents that look like they came out of an academic journal, resumes included): it's not actually that hard. What was hard was how I kept trying to learn it.

Past me tried to learn LaTeX the way you're supposed to learn a language you'll never actually speak: cover to cover, grammar first. Every attempt started the same way. Open a tutorial, decide I was going to understand the entire package ecosystem before writing a single line, and quietly give up two days later. I tried during engineering. I tried again early in my career at Samsung, right when I was preparing to move to OneAdvanced. Same pattern, same outcome. Zero to expert on day one isn't how anyone learns anything, and LaTeX was no exception.

So when I actually needed a resume that got me the OneAdvanced job, I didn't use LaTeX at all. I used Novoresume, a drag-and-drop resume builder, and it did the job. No hard feelings there: it worked, and sometimes "it worked" is the only bar that matters.

## The Two-Year Advice, and Why I Switched Tools

A while later, I started planning my next move out of OneAdvanced, partly on the back of one of the worst pieces of career advice I've ever taken seriously: that you have to switch jobs every two years to "survive in the industry." Several people around me at the time said versions of this, confidently enough that I didn't push back on it the way I should have.

I won't relitigate that advice here, but it did lead to a practical problem: Novoresume is a paid tool, and I wasn't thrilled about paying for something I only needed a few times a year. So I went looking for an alternative and found RxResume, an open-source resume builder built by someone in India. I genuinely loved it. This was also around the time I'd started actively seeking out open-source tools over commercial ones wherever I could, a preference that hasn't gone away since. RxResume served me well. It's what got me through job hunting all the way to my current role at OMICRON in Austria.

So far, nothing about this story screams "and then I built a CI/CD pipeline for it." That part came later, and it came from watching someone else struggle.

## Watching My Wife Fight the Tool Instead of the Content

My wife needed a resume, and we'd even paid for a subscription to get her set up properly. What I watched instead was her fighting the tool. Alignment that wouldn't hold. Text that was too big in one section and too small in another. Whitespace that showed up uninvited and refused to leave. None of it was about what her resume said. All of it was about wrestling a drag-and-drop editor into behaving.

That's a frustrating way to spend an afternoon, and it planted a seed I didn't act on right away.

The seed sprouted a few weeks later, for a much smaller reason than you'd expect. A friend asked me for my latest resume, and I couldn't find it. I dug through RxResume, found an old version, then a slightly newer one, and eventually pieced together something current, but the process told me everything I needed to know: "where even is my current resume" should never be a hard question. If I can't answer it in ten seconds, the setup itself is broken, not just inconvenient.

## Jake's Resume, Overleaf, and Still Not Satisfied

That sent me looking again, and this time I found [Jake's Resume](https://www.overleaf.com/latex/templates/jakes-resume/syzfjbzwjncs) and the Awesome-CV LaTeX template, which is the actual template underneath both. I used Overleaf, an online LaTeX editor, filled in my details, and the output looked genuinely good. Clean, easy to tweak, easy to download as a PDF.

And I still wasn't satisfied. Overleaf was nicer than RxResume, better looking output, less fighting with alignment, but it was still the same category of problem: my resume lived on someone else's cloud service, and my ability to get to it depended on that service being up, my account being active, and me remembering yet another login. Swapping RxResume for Overleaf was a better version of the same dependency, not a different one.

That's when the DevOps part of my brain, the part that spends its working hours thinking about pipelines and build artifacts, finally connected the dots: what if the resume just lived in a git repo like everything else I care about keeping? Version-controlled, diffable, backed up in the most boring and reliable way possible. And instead of a pipeline deploying a piece of software, its job would be to produce a resume as the build artifact.

That reframing is the whole idea behind `my-resume`, and once I saw it that way, the actual build felt almost incidental. The insight wasn't that LaTeX suddenly got easier. It's that all my previous attempts had failed for the same reason: I had no real problem to solve and no template to start from, just an abstract goal of "learn LaTeX" with nothing pulling me through it. This time I had both.

## How It Actually Works

I built `my-resume` working with Claude, and the setup is simpler than it probably sounds. `resume.tex` is the primary file: a two-page resume with a photo, built on the [Awesome-CV](https://github.com/posquit0/Awesome-CV) LaTeX class, vendored locally with a few font tweaks. There's also `resume-plain.tex`, the original single-column template, kept around as a backup but not rebuilt automatically since it's stable and doesn't need CI time on every push.

A push to `main` that touches the resume source triggers the whole thing:

```yaml
on:
  push:
    branches: [main]
    paths:
      - 'resume.tex'
      - 'awesome-cv.cls'
      - 'fonts/**'
      - 'images/**'
      - '.github/workflows/build-and-sync.yml'
```

GitHub Actions compiles it with XeLaTeX, renames the output to `Puneeth-Prakash-Resume.pdf`, and publishes it as a rolling GitHub Release under a fixed `latest` tag, so the download link never changes even though what's behind it does:

```yaml
- name: Publish rolling GitHub Release
  uses: softprops/action-gh-release@v3
  with:
    tag_name: latest
    make_latest: true
    files: Puneeth-Prakash-Resume.pdf
```

From there, the workflow clones this portfolio repo using a token stored as a secret, copies the fresh PDF into `static/files/Resume.pdf`, and commits and pushes automatically, but only if the PDF actually changed. It checks for a real diff first, so an unchanged resume never creates an empty commit. That push is what makes the live resume link on this site always serve whatever I most recently committed to `resume.tex`. Change the source, push it, and a few minutes later the site is up to date. No manual export, no manual upload, no remembering which cloud account has the latest copy.

There's a second wrinkle worth mentioning: I keep a private variant of the same resume with my phone number on it, built from the exact same `resume.tex`. It only picks up a `private.tex` file when a specific flag is passed on the command line, so the public build can never accidentally include it. Locally, that's:

```bash
latexmk -xelatex -usepretex='\def\privatebuild{}' -jobname=resume-private resume.tex
```

In CI, `private.tex` is reconstructed from a secret, used for exactly one compile, and deleted from the runner immediately after. The private PDF gets published to a separate private repo's release, never to anything public, because on a public repo like `my-resume`, release assets and workflow artifacts are downloadable by anyone who can see the repo. There's no private-artifact setting to lean on, so a separate private repo is the only real option. The public build also runs first, before any private data exists in the workspace at all, so a failure later in the pipeline can never leak the phone number into the public PDF.

One thing that isn't private: my EU Blue Card status, which sits right on the address line of the public resume. In the DACH region (Germany, Austria, Switzerland), work authorization is one of the first things a recruiter checks, so hiding it would only slow down the one filter I actually want to pass quickly.

## The Version for My Wife

I ended up building something similar for my wife's resume, based on the same repo and the same approach. It lives in its own private repository rather than this public one, so there's no link to share here, but the idea carries over directly: source-controlled `.tex` files, a build pipeline instead of a drag-and-drop editor, and a PDF that comes out the other end without her fighting alignment or whitespace ever again.

The one real difference is language rather than privacy. Instead of a public and private variant of the same English resume, hers produces an English version and a German version from two parallel source files, built and released together on every push. Same mechanism, applied to a different axis of "which version do I need right now."

## Conclusion

None of the individual pieces here are exotic. GitHub Actions, a rolling release tag, a secret that gets used once and shredded. What made the difference wasn't the tooling, it was finally having a reason to reach for it. LaTeX wasn't the hard part. Not having a real problem to solve was.

- **A resume that never goes missing**: it's in a git repo with full history, not scattered across whichever tool I was using two years ago.
- **A live site that's never stale**: the portfolio's resume link updates itself within minutes of a push, no manual export required.
- **A private variant that stays private by construction**: not by discipline or by remembering to redact something, but because the pipeline is built so it structurally can't leak.

### Your Next Steps

1. **If you've been putting off learning something technical for years**: check whether you actually have a problem for it to solve yet. Mine didn't stick until I had one.
2. **If your resume lives in a tool you don't fully control**: consider what it would take to move the source of truth into something you own, even something as simple as a plain text file in a folder you back up.
3. **If you want to try this yourself**: fork [my-resume](https://github.com/punitpi/my-resume), swap in your own details, and tweak the layout until it's yours. If it saves you the years I spent avoiding LaTeX, a star on the repo is more than enough thanks.

---

## Resources

- [my-resume on GitHub](https://github.com/punitpi/my-resume)
- [Download my current resume (always up to date)](https://github.com/punitpi/my-resume/releases/latest/download/Puneeth-Prakash-Resume.pdf)
- [Jake's Resume (GitHub)](https://github.com/jakegut/resume)
- [Awesome-CV LaTeX template](https://github.com/posquit0/Awesome-CV)

---

Questions? Reach out at contact@puneeth.io
