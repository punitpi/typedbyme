---
title: 'Building My Homelab: A Journey into Self-Hosting'
date: 2025-09-20T15:00:00Z
draft: false
author: 'Puneeth Prakash'
description: 'My experience setting up a homelab for learning, experimentation, and self-hosting various services.'

tags: ['Homelab', 'Self-Hosting', 'Infrastructure', 'Learning']
categories: ['Life & Processes']

# hero: images/posts/homelab/hero.jpg

toc:
  enable: true

menu:
  sidebar:
    name: 'Homelab Setup'
    identifier: 'homelab-setup-guide'
    weight: 504
---

## How I Fell Down the Rabbit Hole

It all started innocently enough. I was scrolling through Reddit (as one does), stumbled upon r/homelab and r/selfhosted, and thought "Oh, that's neat." Famous last words. What began as casual browsing turned into a full-blown obsession with self-hosting everything and learning how the internet _actually_ works.

Spoiler alert: It's complicated, occasionally painful, and absolutely worth it.

## Act I: The pfSense Router Adventure

### The Hardware

I went all in with my first purchase:

- **Intel NUC** (i5, 32GB RAM, 250GB SSD)
- **Intel Dual Port NIC** (because one network port is for amateurs)

**Total damage:** ₹15,000

### What I Actually Learned (The Hard Way)

Turning that NUC into a pfSense router was my crash course in networking fundamentals. And I mean _crash_ both literally and figuratively. Here's what I actually learned:

- **Firewall & Firewall Rules** - Turns out, "deny all" is easy. Making things _work_ while staying secure? That's the art.
- **VLANs** - Network segmentation sounds fancy until you lock yourself out at 2 AM
- **Network Layers** - Finally understood why the OSI model isn't just exam material
- **Ad Blocking** - Because life's too short for YouTube ads
- **DNS & DHCP** - The unsung heroes that make typing `google.com` actually work
- **VPN** - My passport to accessing home services from anywhere
- **Static IPs** - For when DHCP's randomness becomes your enemy

The satisfaction of successfully setting up firewall rules that didn't break everything? _Chef's kiss._

## Act II: Proxmox and the Self-Hosting Saga

Once I had a proper network, I couldn't stop. I set up a Proxmox server and went absolutely wild with self-hosted services:

- **Paperless-ngx** - Digitizing everything like I'm running a paperless office (narrator: he still prints things)
- **Various IT tools** - Because why use cloud services when you can host your own?
- **Nginx Proxy Manager** - Reverse proxying like a boss
- **Home Assistant** - Making my home "smart" (results may vary)
- **Audiobookshelf** - My personal audiobook library, because Audible subscriptions add up

## Act III: Domains, Email, and Public Exposure

At this point, I was hooked. I bought a couple of domains (you know, as you do) and decided to run my own email server.

**Hot take:** Running your own email server in 2025 is like showing up to a knife fight with a spoon. Technically possible, but why would you? After fighting with SPF records, DKIM, DMARC, and getting blacklisted by every spam filter known to humanity, I waved the white flag and migrated to Tuta and Proton Mail.

Then I set up a VPN to safely expose services to the public internet. Because sometimes you want to access your stuff from a coffee shop without broadcasting "HACK ME" to the world.

## Act IV: Immich, Backups, and Other Essentials

- **Immich** - Spun up my own photo server because Google Photos wanted to charge me money (the audacity!)
- **Offsite Backups** - Learned the hard way that "it's in the cloud" means "it's on someone else's computer," so I set up proper offsite backups

## The Security Awakening

Here's the thing they don't tell you: self-hosting is a masterclass in security practices. I learned to:

- Keep everything sanitized and secure
- Update religiously (because vulnerabilities wait for no one)
- Monitor everything (paranoia is a feature, not a bug)
- Actually read documentation (shocking, I know)

## The Unspoken Truth About Homelabs

You know what's hilarious? The moment when something breaks at midnight, the app says "Contact your system administrator," and you realize with dawning horror that **you ARE the system administrator.**

There's no ticket to file. No on-call engineer to page. Just you, a broken service, an increasingly cold cup of coffee, and the GitHub issues page at 3 AM. I've lost count of the nights spent burning the midnight oil debugging why Nginx decided to throw a tantrum or why that container won't start after an update.

And you know what the culprit usually is after hours of debugging? **It's always DNS.** Every. Single. Time. You'll suspect the firewall, blame the proxy, question your Docker configs, and then realize you typo'd a DNS record or forgot to update it. The internet's favorite debugging mantra exists for a reason.

But honestly? Those late-night debugging sessions taught me more than any certification course ever could.

## What I'd Tell My Past Self

### 1. You Will Break Things (And That's Fine)

Seriously, embrace it. Every broken service is a learning opportunity. Just make sure you have backups before you break things in _creative_ ways.

### 2. Document EVERYTHING

Future you will have absolutely no memory of why you configured that firewall rule that specific way. Trust me. Write it down. Past me learned this lesson at least five times before it stuck.

### 3. Start Small, Scale Smart

Don't try to host everything on day one. Start with a couple of services, learn the basics, then expand. I didn't follow this advice and spent a weekend untangling my own mess.

### 4. The Community is Gold

r/homelab and r/selfhosted are genuinely amazing communities. When you're stuck at 2 AM wondering why your reverse proxy hates you, someone there has probably fought that same battle.

### 5. Security Isn't Optional

It's tempting to skip security steps when you're excited to get something working. Don't. Learning to do things securely from the start is way easier than trying to retrofit security later.

### 6. Your Family Will Not Share Your Enthusiasm for Downtime

When you're tinkering and services go down, your family will not appreciate your technical explanations. Keep critical stuff stable, or prepare for justified complaints.

## The Reality Check

**Is running a homelab worth it?**

If you enjoy:

- Learning by breaking things
- Having complete control over your data
- Debugging at ungodly hours
- The satisfaction of building something from scratch
- Saving money long-term while spending it upfront

Then yes, absolutely.

If you just want stuff to work without thinking about it? Stick with cloud services. No shame in that.

## What This Journey Taught Me

Running a homelab transformed how I think about infrastructure, security, and self-reliance. It's hands-on learning at its finest. Every problem I've solved, every late night spent debugging, every time I successfully configured something complex—it all adds up to real, practical knowledge you can't get from tutorials alone.

Plus, there's something deeply satisfying about saying "Yeah, I host that myself" when someone asks what photo service I use.

## The Journey Continues

This is just the beginning. There are always more services to self-host, more optimizations to make, more things to learn. And honestly? I wouldn't have it any other way.

If you're thinking about starting your own homelab journey, my advice is simple: Just start. Pick one thing you want to self-host, dive in, and see where it takes you. The Reddit communities are there when you need help, the documentation is (mostly) available, and the learning never stops.

Welcome to the club. Your sleep schedule will never be the same.

## Resources

- [r/homelab](https://reddit.com/r/homelab) - Amazing community
- [Self-Hosted Podcast](https://selfhosted.show/)
- [Awesome Self-Hosted](https://github.com/awesome-selfhosted/awesome-selfhosted)

---

Running a homelab? I'd love to hear about your setup! Contact me at contact@puneeth.io
