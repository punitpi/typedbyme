---
title: 'The 3 AM Call: How a Fake "Customer Support" App Emptied My In-Laws'' Credit Card'
date: 2026-10-23T09:00:00+01:00
draft: false
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

## TL;DR

A caller who claimed to be from the bank spent months pushing my father-in-law into taking a credit card, then got him to install a fake "Customer Support" app. It was a remote-access trojan, and about INR 1 to 1.2 lakh left the card through Paytm. The app hid its icon and threw me out of Settings whenever I tried to uninstall it, so I removed it with `adb`. Later I broke the app open to understand what it actually does. The biggest problem was that he told nobody in the family for a month or two. If you have parents, talk to them before something like this happens.

## Introduction

Around 3 AM, my wife's phone rang. It was her father. Something was happening on his phone, he said, and they needed help. They were talking fast and none of it added up.

That was unusual. My father-in-law is highly educated, careful with money and suspicious by nature. He doesn't fall for discounts or easy-money offers, and he doesn't panic. We didn't know what was going on, so we just went. We were out the door in five minutes.

That night I removed a remote-access trojan (RAT: malware that lets someone else control a device) from his phone. The family had lost about INR 1 to 1.2 lakh. The cause was a phone call that kept coming back for months.

I'm writing this because it can happen to anyone, including someone careful and sceptical, and because the malware, which I tore apart later, explains exactly what I saw on that phone. This is the story from all our sides: mine, my father-in-law's, my mother-in-law's and my wife's. Nobody is named, and nothing here is meant to blame them.

A timing note: the incident and my `adb` (Android Debug Bridge) session were in November 2025. I analysed the saved malware much later, on 2026-10-18. Everything technical below comes from that later analysis.

## Chapter 1: The Call

When we got there, we learned they had already acted. They had called the bank's customer care, and the account, debit card and credit card were frozen. The bank told them to file a complaint on the 1930 helpline (India's national cybercrime line). They were in the middle of filing it, and I needed information we didn't have.

### Look at the phone first

From that first conversation I understood it had happened on the phone, so I asked them not to explain anything more yet. I wanted to look at the phone before hearing the full story, which could bias what I looked for. It was a Samsung Android phone.

The app drawer looked normal. Before Settings, I went through files, messages and WhatsApp. In WhatsApp there was a conversation with a contact whose profile picture was a headset-wearing support agent, with a "deleted message" marker among the other messages. Then I went to Settings > Apps and scrolled the full list. There was an app called "Customer Support", with the same picture. No app should have that name and that icon.

I tapped it to see permissions and the uninstall option. Settings closed and threw me back to the home screen. I tried again. Same thing, every time. By then it was clear the app was fighting me, so I recorded a video as evidence.

## Chapter 2: Hunting the App

### Using adb

I connected the phone to my MacBook. (USB debugging has to be on for this to work.) The first block installs the tools and lists every package.

```bash
# Install adb on macOS
brew install android-platform-tools

# Confirm the phone shows up (accept the prompt on the phone)
adb devices

# List every installed package, hiding obvious Samsung and Google ones
adb shell cmd package list packages | grep -v samsung | grep -v google
```

That still left hundreds of packages, and I didn't have the brainpower at 3 AM to sort them by hand. So I pasted the list into Claude and asked it to filter out known defaults. It returned a shortlist of 15 to 20, which is exactly the tedious sorting I'm happy to hand off at that hour.

One name stood out: `computing.publishing.occurrence`. Nobody would name a legitimate app that. Nothing in it connects it to "Customer Support", so part of my certainty was gut feeling. I confirmed it later: after I uninstalled it, the "Customer Support" app was gone.

### Evidence first, then removal

A factory reset destroys evidence, so before removing anything I copied the APK (the Android app file) to my laptop. The next block copies it, removes the app and confirms it's gone.

```bash
# Find where the app lives, then copy it to my laptop
adb shell pm path computing.publishing.occurrence
adb pull /data/app/~~<random>/computing.publishing.occurrence-<random>/base.apk

# Uninstall, then confirm (no output means it's gone)
adb uninstall computing.publishing.occurrence
adb shell pm list packages | grep computing.publishing.occurrence
```

Then I wiped the phone with `adb shell recovery --wipe`, rebooted, and hard reset it again from the phone's own menu. A warning: that is what I ran on this one Samsung, and I haven't verified it works on other devices. The phone's built-in factory reset is the safer path for most people. I handed the phone back and said we'd talk in the morning.

## Chapter 3: The Morning After

We sat down together, all four of us, and I asked them to explain everything from the beginning.

For days, then months, a person who said he was from the bank kept calling my father-in-law and pushing him to take a credit card. He kept saying no. Eventually he agreed. When the card arrived, he couldn't activate it.

I think I know why. As I understand this bank's process, when you apply for a credit card the form asks for a phone number, and that number is used to activate the card. It needn't be an account holder's number, since you can order these cards without an account. If the caller entered his own number, only he could activate it. He still needed details from my father-in-law, who held the card. That's my reading, not something the bank confirmed.

So the same caller kept ringing, still saying he was from the bank, and offered to help activate it. My father-in-law eventually agreed and shared his phone number and details. Somewhere along the way he was also convinced to install an app and grant it permissions. There was a WhatsApp message where the caller sent the app and then deleted it. My father-in-law vaguely remembered being asked to install something, but it had all stretched over a couple of months.

## Chapter 4: Where the Money Went

### What I saw, and what I suspect

In the bank statements, I saw the money leave the credit card in two or three transactions, totalling about INR 1 to 1.2 lakh. It went through Paytm and on to a different bank account. The Paytm phone number was in the transaction description, and when we tried it, it was disconnected.

The rest is inference. Paytm can pay rent from a credit card, and I've read about people using that to move money from a credit card to a bank account. That fits, but I'm guessing at the mechanism. I also suspect the card was registered to a number the caller controlled. That would explain the activation and why the bank's alerts never reached my father-in-law. I don't know what other details the caller got from him to use the card.

### The timeline

On the way back from their first trip, my father-in-law's phone went black and he assumed it was broken. Soon after, they left on another trip for 10 to 15 days.

When they got back there was a credit card bill in the post they hadn't opened. The bank's SMS and call alerts never reached them, most likely because the number on the card was the attacker's. The bank had also emailed my mother-in-law's address several times, once saying it had called repeatedly with no answer. Other emails carried the credit card statement, the last date for paying the bill and so on. Nobody was watching that inbox. They only found out when they looked at the account. By the time I pieced it together, the money was long gone.

We filed the 1930 complaint and took its reference to the local police station. They said the money had already been withdrawn and there was little they could do, though they would try. We knew it was gone.

### The biggest mistake

For one to two months, through the calls, the card, the failed activation and the offers of help, my father-in-law told nobody in the family. That silence was the main problem.

I don't know exactly why, and I haven't pushed him. It happened to a careful, educated, suspicious person. Months of calls from a persistent voice claiming to be your bank is a long game, and these callers play it for a living.

## Chapter 5: Inside the App

Months later, I analysed the saved APK. I did static analysis only: I read the decompiled code with `jadx` and `androguard` and never installed or ran it. I'm describing what the code makes possible, not what I watched it do.

It is a RAT built with the SpyMax/SpyNote toolkit family, posing as a bank "Customer Support" app with a headset-agent icon. Once the victim enabled Accessibility and Device Admin, an operator could control the phone over a raw TCP connection to `173.225.111[.]161:7771` (defanged). One caveat: the family name rests on a builder string left in the app. That its configuration names are characteristic of SpyNote is from my memory and I haven't checked it against a published write-up.

### Why the icon vanished

The malware disables its own launcher entry, so it isn't in the app drawer. That's why I only found it in Settings > Apps.

### Why Settings kept closing

The app's accessibility service can see the screen in every app. When it spots its own name next to words like uninstall, force stop or turn off (in English, Turkish, Chinese and Arabic), it presses back and sends you home. The malware was watching me tap and throwing me out whenever I got near the uninstall screen.

### What else it can do

- Remote control and screen streaming: the operator sees your screen and taps for you. It also clicks "Allow" on permission dialogs for itself.
- Black-screen cover: an overlay hides what the operator is doing from anyone looking at the phone.
- Unlock capture and replay: it records your unlock taps and replays them to unlock the phone remotely.
- Screen text and notification capture: it sends on-screen text and notifications, including one-time passwords, to the operator.
- Device admin: it can lock or wipe the phone.
- Per-app firewall: it can cut chosen apps, like a bank app, off from the internet.
- Plugin loader: it downloads extra code from the server and runs it in memory.

The black-screen cover stuck with me. If an operator was using the phone while my father-in-law travelled, a black screen is exactly how it would look from outside. I can't prove that's what happened, but the fit is uncomfortable. Combined with the unlock replay, the operator could use the phone, including banking apps, whenever it sat idle.

### Limits and open questions

The APK is a stub, so what I analysed is the minimum the malware could do. Reading SMS, contacts and files most likely lives in plugins that weren't in the APK. The server address can also be changed remotely, so the server in use during the fraud may differ.

Was the factory reset enough? Very likely. I found no root exploit, no writes to the system partition and no native libraries. It runs as an ordinary app, and its files live in user storage, which a reset erases. We didn't rely on that, though: we bought my father-in-law a new phone and disposed of the old one.

What I don't know:

- How the card details and one-time passwords were obtained. It could be the live screen stream, the operator watching what was typed, my father-in-law reading them out, or the app's "Simple Keyboard" input method if it was ever switched on.
- The exact fraud sequence. The steps I described are what the code makes possible, so they are inferred and were never observed.
- How the APK was delivered. I'm fairly sure it was WhatsApp, since I saw a message from the caller there, but I can't prove it.
- What the plugins did, and who owns the server. I did no lookup on the address.

For anyone who handles security, here are the defanged identifiers of the file I recovered. They come with no link or instructions to obtain it.

```text
package  computing.publishing.occurrence
sha256   01ecf6c82762d997c57fe62deb64c002b006e6ab1b92bec68410b917231d8cda
c2       173.225.111[.]161:7771/tcp
```

## Chapter 6: Protecting Your Family

None of this requires technical skill.

### Talk before it happens

When we were kids, our parents drilled the rules into us: don't talk to strangers, don't go anywhere with a stranger, don't let a stranger touch you, don't accept candy from a stranger. It's funny, or maybe just strange, that we now have to tell them the grown-up version: don't talk to strangers on the phone, and don't give them your personal information or any information at all.

- Have the conversation now, and keep it casual: "If anyone calls, emails or messages asking for personal information, or about your bank, cards or accounts, tell me first, even if it seems fine."
- Make it safe to tell. The silence was the biggest problem in our case, so say out loud that nobody will be judged. Shame keeps people quiet, and callers like this depend on that.
- Agree on one rule. If anyone asks for personal information, or wants you to do something involving your bank, cards or accounts, don't give or do anything. Hang up and contact the organization yourself, using a number from its official website or printed on your card.
- Never install an app because a caller asks, for any reason, and never install an APK sent over WhatsApp or a link. Use the official store.
- Never read out a PIN, an OTP or any personal information, however official the caller sounds.
- Make sure the phone number and email on your bank accounts and cards are yours, and read what arrives there, including the routine-looking messages. The warning that would have helped us sat unread in an inbox.
- Check the phone together. In Settings, look at Apps for names you don't recognise, and at Accessibility and device admin apps, since few apps need those. Keep Google Play Protect on. Menu names vary by brand.

### If you suspect something

Move fast. Money gets harder to recover as days pass.

1. Call the bank and get cards and accounts frozen.
2. File a complaint with the 1930 helpline (India), even at night.
3. Preserve evidence if you can: screen-record what you see, and if you're technical, pull the APK before any reset.
4. Then clean the phone, ideally with the phone's own factory reset.

I'm deliberately not claiming anything about bank policies, refund rules or recovery timelines. I haven't verified them, and they vary. Ask your bank.

## This week

Call your parents and share the one rule from chapter 6. Check that the phone number and email on their bank accounts and cards are theirs, and that someone reads what arrives there. Then look at their phone together: Settings > Apps, Accessibility and device admin, with Play Protect on. Keep it a coffee-table chat.

It's an awkward conversation. In our case, one sentence to someone in the family when the calls started would likely have changed the outcome.

---

## Resources

- [Android Debug Bridge (adb) documentation](https://developer.android.com/tools/adb)
- [Google Play Protect help](https://support.google.com/googleplay/answer/2812853)
- [National Cyber Crime Reporting Portal (India)](https://cybercrime.gov.in/)

---

Questions? Reach out at contact@puneeth.io
