---
title: 'The 3 AM Call: How a Fake "Customer Support" App Emptied My In-Laws'' Credit Card'
date: 2026-10-23T09:00:00+01:00
draft: true
author: 'Puneeth Prakash'
description: 'A late-night family emergency, a phone I could not uninstall an app from, and what I found when I tore the malware apart. Plus how to protect your parents.'

tags: ['Cybersecurity', 'Android', 'Malware', 'Fraud', 'Family', 'adb', 'Incident Response']
categories: ['Life & Processes']

hero: images/posts/the-3am-call-a-fake-bank-support-app/hero.jpeg

toc:
  enable: true

menu:
  sidebar:
    name: 'The 3 AM Call'
    identifier: 'the-3am-call-a-fake-bank-support-app'
    weight: 490
---

## Introduction

Around 3 AM, my wife's phone rang. It was her father. Something was happening on his phone, he said, and they needed help. They were talking fast and saying a lot of things at once, and none of it added up.

That was unusual. My father-in-law is highly educated, careful with money, and suspicious by nature. He's not someone who falls for discounts or easy-money offers, and he doesn't panic. We didn't know what was going on, so we didn't ask more questions. We just went. We were out the door in about five minutes.

By the time I was done that night, I had removed a remote-access trojan from my father-in-law's phone. The family had also lost roughly 1 to 1.2 lakh rupees. In the morning I learned how it all started, and the answer was not a clever hack. It was a phone call that kept coming back for months.

I'm writing this for two reasons. One, the technical part is interesting: I tore the malware apart later and it explains exactly what I saw on that phone. Two, and more important, this can happen to anyone, including someone careful and sceptical who is being worked on for a long time. If this post helps you have an awkward conversation with your own parents a bit earlier than I did, it's worth it.

A note on how I'm telling this. It's the story from all of our sides: mine, my father-in-law's, my mother-in-law's and my wife's. I'm not naming anyone, and nothing here is meant to blame them. They did what most of us would do with a persistent, friendly voice on the line.

Here's what's coming:

- The night itself, and what I did on the phone with `adb`
- The morning conversation that explained everything
- What the malware does, based on my analysis
- What is known, what is inferred, and what I still don't know
- Practical steps to protect your own family

## Context: What You Need to Know

You don't need to be an Android expert. A few terms will help.

- **adb** (Android Debug Bridge) is a command line tool that lets a computer talk to an Android phone over USB, once USB debugging is turned on.
- **APK** is the file format for an Android app. Installing an app from a file or link instead of the Play Store is called _sideloading_.
- **RAT** means remote-access trojan: malware that lets someone else control your device from afar.
- **1930** is India's national cybercrime helpline.
- **C2** (command and control) is the server the malware reports to and takes orders from.

One timing note, so I'm honest with you. The incident and my `adb` session were in November 2025. The deep analysis of the malware happened much later, on 2026-10-18, about eleven months afterwards. I did it from the APK I saved that night. All the technical findings below come from that later analysis.

## The Night

### What They Had Already Done Right

When we got to their house, we learned they had lost about 1 to 1.2 lakh rupees through their credit card. To their credit, they had already acted. They called the bank's customer care in the middle of the night. The account was frozen, the debit and credit cards were frozen, and they were told to file a cyber crime ticket through the 1930 helpline and portal.

They were in the middle of filing it, and I needed information we didn't have.

### Look at the Phone First

Here's a decision I'm glad I made. I asked them not to explain anything yet. I wanted to look at the phone before hearing a story, because a story can bias what you look for. It was a Samsung Android phone.

The app drawer looked normal. No suspicious app anywhere. Before going into Settings, I went through the files, the messages and WhatsApp. In WhatsApp I noticed a conversation with a contact whose profile picture was a headset-wearing support agent. It had a "deleted message" marker among the other messages. I didn't know yet what that picture meant.

Then I went to Settings > Apps and scrolled the full list. There it was: an app called **Customer Support**, with the same picture as that WhatsApp contact. No app should exist with that name and that icon, and now I'd seen the icon in two places.

I tapped it to look at its permissions and the uninstall option. Settings closed and threw me back to the home screen. I tried again. Same thing. Every single time.

I recorded a video of it on my own phone as evidence. I'll explain later in the post exactly why the app behaved this way. At that moment, all I knew was that an app was fighting me.

### Using adb

I connected the phone to my MacBook and installed the Android platform tools with Homebrew. USB debugging had to be enabled on the phone for this to work.

```bash
# Install adb and friends on macOS
brew install android-platform-tools

# Confirm the phone shows up (accept the prompt on the phone if asked)
adb devices

# List every installed package
adb shell cmd package list packages
```

That gave me somewhere between 200 and 300 packages, mostly system defaults. It was the middle of the night and I did not have the brainpower to sort defaults from strangers by hand. I tried a quick filter first.

```bash
# Rough filter: hide the obvious vendor and Google packages
adb shell cmd package list packages | grep -v samsung | grep -v google
```

That wasn't enough. So I pasted the package list into Claude and asked it to filter out the known default apps. It handed me back a shortlist of 15 to 20, which is exactly the kind of tedious sorting I'm happy to hand off at 3 AM.

One name on that list stood out: `computing.publishing.occurrence`. Nobody would name a legitimate app that. Nothing in the name connects it to "Customer Support", so I couldn't prove it was the one from the package name alone. Part of it was gut feeling, and I checked it before acting.

### Evidence First, Then Removal

I looked at the package more through `adb` and it looked very suspicious. Now came the order of operations, which was deliberate. A factory reset destroys evidence, so before removing anything, I copied the APK to my laptop.

```bash
# Find where the app's APK lives on the phone
adb shell pm path computing.publishing.occurrence

# Copy it to my laptop as a backup (the path has random segments, so use the real output from the previous command)
adb pull /data/app/~~<random>/computing.publishing.occurrence-<random>/base.apk
```

With the APK saved, I removed the app and checked that it was gone. That settled it: after the uninstall, the "Customer Support" app was no longer on the phone.

```bash
# Uninstall the package
adb uninstall computing.publishing.occurrence

# Confirm it's gone (no output means no match)
adb shell pm list packages | grep computing.publishing.occurrence
```

Then I wiped the device. I ran `adb shell recovery --wipe` from my laptop, rebooted, and then did a hard reset again from the phone's own menu, to be safe.

**Fair warning:** I'm showing what I ran on this one Samsung phone. I haven't verified that `adb shell recovery --wipe` behaves the same on every device, so please don't treat it as a universal recipe. The phone's built-in factory reset is the safer, supported path for most people. And again, wiping destroys evidence, so save what you need first.

The phone was clean. I handed it back and said we'd talk in the morning.

## The Morning

In the morning we sat down together: my father-in-law, my mother-in-law, my wife and me. I asked them to explain everything from the beginning. What follows is what my father-in-law told us.

For days, and then months, a person who said he was from the bank kept calling him and pushing him to take a credit card. He kept saying no. Eventually he agreed. When the card arrived, he couldn't activate it.

I think I know why. As I understand this bank's process, when you apply for a credit card you check your eligibility, pick a card from a list, and order it, and along the way the form asks for a phone number. That number is the one used to activate the card. It doesn't have to be the number on a bank account, because people can order these cards without holding an account at all. If the caller supplied his own number during the application, then the only person who could activate the card was the scammer. He still needed details from my father-in-law, who was the one holding the card. That is my reading of it, not something I could confirm with the bank.

The same caller kept ringing, still saying he was from the bank, and offered to help activate it. He was persistent. Eventually my father-in-law agreed. He shared his phone number and details.

Somewhere along the way he was convinced to install an app and grant it permissions. There was a WhatsApp message where the caller sent the app and then deleted the message. My father-in-law vaguely remembered being asked to install something, but wasn't sure. It had all stretched over a couple of months.

### What I Saw, and What I Suspect

Some of this I saw myself in the bank statements. The money left the credit card in two or three transactions, totaling about 1 to 1.2 lakh rupees. They went through Paytm and on to a different bank account. The Paytm phone number appeared in the transaction description. When we tried it, the number was disconnected.

The rest is my inference. Paytm has a feature to pay rent using a credit card, and I've read about people using it to move money from a credit card into a bank account. That fits what I saw, but I'm guessing at the mechanism.

As I described above, I suspect the card was registered to a phone number the caller controlled, not my father-in-law's. That would explain why the card could only be activated through the caller, and why the bank's alerts never reached my father-in-law. Exactly what details the caller got from him to use the card, I don't know.

### The Timeline Around the Theft

On the way back from their first trip, my father-in-law's phone went black. He assumed it was broken. I'll come back to why that detail matters in the teardown. Soon after they got home, they left on another trip, this time for 10 to 15 days.

When they got back, there was a credit card bill in the post they hadn't looked at yet. The bank's SMS and call alerts never reached them. The most likely reason is that the phone number registered on the card was the attacker's, not theirs. The bank had also emailed my mother-in-law's address multiple times about the transaction. One of those emails even said the bank had called several times and nobody picked up. Later came the bill. But nobody was monitoring that email.

Only when they looked at the bank account did they notice the money was gone. By the time I pieced it together, it was weeks late, and the money was long gone.

### The Biggest Mistake

For one to two months, through the calls, the card, the failed activation and the offers of help, my father-in-law told nobody in the family. That silence was the main problem. Not the app, not the card.

I don't know exactly why he kept it to himself, and I haven't pushed him on it. What I do know is that it happened to a careful, educated, suspicious person, so this isn't about being gullible. Months of calls from a persistent voice that claims to be your bank is a long game, and it's a game these callers play for a living.

### Reporting It

We filed the 1930 complaint, then took the complaint reference to the local police station. They checked and told us the money had already been withdrawn and there was little they could do, though they would try. We knew it was gone.

## The Teardown

Eleven months later, I finally sat down with the APK I'd saved. A few ground rules first. I did **static analysis only**: I read the decompiled code and never installed or ran the app. I used `jadx` and `androguard` for that. I'm describing behavior the code makes possible, not what I watched it do.

### What It Is

The app is a remote-access trojan built with a toolkit from the SpyMax/SpyNote family. It posed as a bank "Customer Support" app, with an icon of an agent wearing a headset and the word "SUPPORT". Once the victim granted it Accessibility and Device Admin permissions, an operator could control the phone over a raw TCP connection to a server I'll defang as `173.225.111[.]161` on port 7771.

**A caveat on the family name:** it rests on a leftover string from the builder tool inside the app. The configuration field names fit that family too, but my claim that they are characteristic of SpyNote came from memory and I haven't checked it against a published write-up. I also found no public record of this exact file or package name.

### Why the Icon Vanished

Remember that the app wasn't in the app drawer? The malware disables its own launcher entry, so the icon disappears. That's why I could only find it under Settings > Apps.

### Why Settings Kept Closing

This was the part that made sense of my video. The app runs an accessibility service, which can see what's on screen in every app. When it spots its own name next to words like uninstall, force stop or turn off (it checks in English, Turkish, Chinese and Arabic), it presses back and sends you to the home screen.

So Settings wasn't crashing. The malware was watching me tap, recognizing the screen, and throwing me out. Every time.

### What It Can Do

Here are the capabilities that matter most for this incident. Each one is visible in the code.

| Capability | What it means in plain words |
|---|---|
| **Accessibility service** | Reads everything on screen, performs taps and swipes, and clicks "Allow" on permission dialogs for itself |
| **Device admin** | Can lock the phone, and can wipe it |
| **Remote control and screen streaming** | The operator sees your screen live and taps on it for you |
| **Black-screen cover** | Draws a black overlay with custom text so nobody looking at the phone sees what is happening |
| **Unlock capture and replay** | Records the taps you make to unlock the phone, then replays them to unlock it remotely |
| **Screen text and notification capture** | Sends on-screen text and notification text, including one-time passwords (OTPs), to the operator |
| **Plugin loader** | Downloads extra code from the server and loads it in memory |
| **Per-app firewall** | Can cut chosen apps, like a bank or security app, off from the internet |

The black-screen cover is the one that stuck with me. While my father-in-law was travelling, the phone went black. He assumed it was broken. If an operator was using it at that moment, that is exactly what it would look like from the outside. I can't prove that's what happened, but the fit is uncomfortable.

The unlock replay matters too. Put those together and the operator could use the phone, including banking apps, whenever it sat idle, without anyone noticing.

### The App Is Only a Stub

The APK I recovered is a stub. When it connects to the server, it can receive more code and load it, then delete the file. So what I analyzed is the **minimum** the malware could do. Things like reading the SMS inbox, contacts and files most likely live in plugins, and those weren't in the APK.

Another honest limit: the server address can be changed remotely, so the server in use during the fraud may differ from the one built in.

### Was the Factory Reset Enough?

Very likely yes. I found no root exploit, no writes to the system partition and no native libraries. The app runs as an ordinary app holding Accessibility and Device Admin, and its files live in user storage, which a factory reset erases. The caveat is that I never saw the plugins. They would run inside the same app with the same limits, though.

We didn't rely on that, though. As a precaution, we bought my father-in-law a new phone and disposed of the old one.

### What I Don't Know

I'd rather be candid than tidy. These are the open questions.

- **How the card details and any one-time passwords were obtained.** Possible routes include the live screen stream, the operator watching what was typed or shown on screen, the victim reading them out to the "agent", or the app's "Simple Keyboard" input method, if it was ever switched on. The stub doesn't show which one.
- **The exact fraud sequence.** The steps I could describe, a phone call, installing the app, enabling permissions, then an operator driving the phone while idle, are what the code makes _possible_. They are inferred, not observed.
- **How the APK was delivered.** I'm fairly sure it came over WhatsApp, since I saw a message from the caller there, but the file itself wasn't recoverable, so I can't prove it.
- **What the plugins did.** Not in the APK.
- **Who owns the server.** I didn't do any lookup on the address.

### Indicators of Compromise

If you handle security for others, here is a small defanged set. These are identifiers of the file I recovered, with no link or instructions to obtain it.

```text
package  computing.publishing.occurrence
sha256   01ecf6c82762d997c57fe62deb64c002b006e6ab1b92bec68410b917231d8cda
c2       173.225.111[.]161:7771/tcp
label    "Customer Support" (launcher), "Simple Keyboard" (input method)
```

The signing certificate was the public Android test key, which anyone can use. So it tells you nothing about who made it.

## What You Can Do for Your Own Family

Now the part I care about most. None of this requires technical skill.

### Talk Before Something Happens

When we were kids, our parents drilled the rules into us: don't talk to strangers, don't go anywhere with a stranger, don't let a stranger touch you, don't accept candy or anything else from a stranger. Now the roles have flipped, and it's funny, or maybe just strange, that we have to tell them the grown-up version: don't talk to strangers on the phone, and don't give them your personal information or any information at all.

- **Have the conversation now.** Not after. Make it casual: "If anyone ever calls, emails or messages asking for personal information, or about your bank, cards or accounts, tell me first, even if it seems fine."
- **Make it safe to tell.** The biggest lesson from our case was the silence. Say out loud that nobody will be judged, whatever happens. Shame keeps people quiet, and quiet is what these callers depend on.
- **Agree on one rule.** If anyone contacts you by phone, email or message and asks for personal information, or wants you to do something involving your bank, cards or accounts, don't give or do anything. Hang up and contact the organization yourself, on a number from its official website or printed on your card.

### Simple Rules That Help

- **Never install an APK sent over WhatsApp or a link.** Install apps only from the official store.
- **Don't install an app because a caller asks you to**, for any reason: activating a card, fixing an account, or anything else. If someone asks, hang up.
- **Never read out a PIN, an OTP or any personal information** to anyone, however friendly or official they sound.
- **Make sure the phone number and email on the bank account and cards are yours**, and that you actually check them. In our case, alerts probably went to the attacker's number and to an email nobody watched.
- **Watch your emails.** Read what your bank sends you, including the ones that look routine. The warning that would have helped us was sitting in an inbox.

### Check the Phone

- Open Settings > Apps and look for names you don't recognize.
- Check Settings > Accessibility and the device admin apps list. Few apps need these. A "Customer Support" app asking for both is a red flag.
- Keep Google Play Protect turned on.

**Pro tip:** menu names differ between phone brands, so look around if you don't see these exact labels.

### If You Suspect Something

1. **Call the bank immediately** and get cards and accounts frozen.
2. **File a complaint with the 1930 helpline right away** (India). Don't wait until morning if it's night. Speed matters, because money gets harder to recover as days pass.
3. **Preserve evidence if you can.** Screen-record what you see. If you're technical, pull the APK before any reset, like I did.
4. **Then clean the phone.** A factory reset from the phone's own settings is the straightforward option.

I'm deliberately not claiming anything specific about bank policies, refund rules or recovery timelines. I haven't verified those, and they vary. Ask your bank directly.

## Conclusion: Quiet Is the Real Risk

This wasn't a story about a careless person. It was about a long, patient campaign aimed at someone who is educated, careful and suspicious about money. The malware was sophisticated enough to hide itself and fight removal. But the real opening was a few months of phone calls and a silence in the family.

Here's what I took from it:

- **Early disclosure beats everything**: one sentence to a family member in week one would likely have changed the outcome.
- **Monitored contact details matter**: alerts that go to the wrong number or an unread inbox are no alerts at all.
- **Evidence before wiping**: saving the APK is the only reason I could write the second half of this post.
- **Be honest about what you know**: much of what I wrote above is inferred, and I'd rather say so than invent a neat story.

### Your Next Steps

1. **Call your parents this week**: share the one rule: if anyone asks for personal information or wants them to act on their bank, cards or accounts, hang up and contact the organization themselves.
2. **Check the registered contact details**: confirm the phone number and email on their bank accounts and cards are theirs, and that someone reads them.
3. **Look at their phone together**: Settings > Apps, Accessibility and device admin, with Play Protect on. Make it a coffee-table chat, not an audit.

It's an awkward conversation. Have it anyway. Your future self will thank you.

---

## Resources

- [Android Debug Bridge (adb) documentation](https://developer.android.com/tools/adb)
- [Google Play Protect help](https://support.google.com/googleplay/answer/2812853)
- [National Cyber Crime Reporting Portal (India)](https://cybercrime.gov.in/)

---

Questions? Reach out at contact@puneeth.io
