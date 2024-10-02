---
layout: default
title: The browser you use sucks!
description: And no, it doesn't matter which one it is.
---

*I explicitly state my own, personal opinion in this article. You are entitled to your own.*

### What?

Yeah, you heard me.

But let's begin at the start. Back in the day, when ol' Steppy still was an elementary school student, he got his first internet connected PC at home. It was ISDN - for those of you that never heard of it: [It could supply you with a whopping 2 Mbit/s](https://en.wikipedia.org/wiki/ISDN#Rollout).

My dad always was a pretty big nerd, and by the time I got connected to the internet, he used Firefox 1.5. It was a time where tabs were the hot new feature. Not to say a revolutionary feature, even. This was a time where I didn't really use my PC that much, and I really wasn't a savvy PC user at all. I could install software and that's about it.

When I really got into the PC game, the current version of Firefox was Firefox 3.6.

Again, back then, you needed Adobe Flash installed if you wanted to play YouTube videos - or any online videos at all, really - and some websites wanted you to install Microsoft Silverlight or QuickTime plugins. AVG Free Antivirus was the prime choice, next to Avira AntiVir and Avast!

You don't need to remind me, I know I'm getting there, age wise. 

I was using this for a good while, and this was also when I started to make friends with some other nerds from higher grades in school. 

In 2008, Google released Google Chrome which didn't gain much real popularity until 2010-2012. I was wary of using it, because I read online that you get a UUID attached to your browser, and Google would be able to see what you did on the web. Mind you, this was pre-GDPR and is 13 years ago at this point. The Snowden leak didn't happen yet and we all still had the sensation of online privacy. 

I still fondly remember this conversation in my local school's tech club:

> **Me:** I don't know, with the Google ID and all... I don't trust it, man  
> **Dude 1:** Pfft, two words: Hacker News.  
> **Dude 2:** Yeah, my ID number is from somewhere in Russia, good luck Google.

It really were simpler times, eh?

So I installed Chrome with a sketchy registry tweak and was blown away. Websites loaded fast, extensions were really cool, and it looked much better than Firefox did, in my opinion. 

And I was a Chrome user ever since, with a nice assortment of plugins. I witnessed the Adblock Plus enshittification and switched over to uBlock Origin. All was good.

Until, in 2022, I updated Chrome one morning and for some reason, I had trouble loading YouTube. I checked all the usual things. I cleared my DNS cache, I cleared the cookies and browser cache. I tried it all, it didn't even load in Incognito. I finally caved and checked reddit if anyone has a similar issue. And well, what should I say? I wasn't the only one with that problem. It seemed like specifically, uBlock Origin users in Germany were experiencing such harsh throttling of YouTube, that even the home page would take *minutes* to load correctly.

I had no choice really, so I switched to Firefox again. Firefox has come a long way, but it does have its flaws, even though I like it a lot.

Alright, now enough of the preamble. Let's get into the meat of this article. Why do *I* think the currently popular browsers suck?

### Google Chrome

There's a lot to unpack about why Google Chrome sucks. Despite the [Privacy, Tracking and Advertisement issues](https://en.wikipedia.org/wiki/Google_Chrome#Criticism) there's also the ongoing discussion about Manifest V3, which imposes some API limits that prove a serious challenge to ad blocking extensions, it's still the most popular webbrowser as of the writing of this article (citation needed).

Here are some more reasons why I believe that it sucks:

* [There are a number of malicious and/or scam extensions on the Chrome Web Store](https://palant.info/2023/05/31/more-malicious-extensions-in-chrome-web-store/)
* I find the settings interface confusing and it keeps obfuscating simple functionality
* 

### Mozilla Firefox

While I consider Firefox to be one of the better choices, it's still a far cry from the perfect browser. It's a good bit more privacy friendly than Chrome, yet [still tracks you by default](https://noyb.eu/en/firefox-tracks-you-privacy-preserving-feature) and [used to send every address bar keystroke to Mozilla](https://www.howtogeek.com/760425/firefox-now-sends-your-address-bar-keystrokes-to-mozilla/).

Since I've been dailying Firefox on my personal machines, I have a lot to talk about. Here's my list of Firefox annoyances (devs, if you read this, would be cool if you could fix some of this):

* The performance has gotten a lot better over the years, but in some cases, the Chromium based alternatives still run circles around Firefox.
* Extension support is good, but there could be more.
* Whoever thought that displaying ads in the address bar (in a default Firefox configuration) is a good idea should be let go immediately.
* The Tab management needs some overhauling. Where's tab groups, where's tab search with a keyboard shortcut (I have a plugin for this), where's color coding of tabs?
* Adding support for more APIs would be super swell, then I wouldn't have to rely on Chrome or Edge for some websites.
* There's no support for Progressive Web Apps (PWAs). Come on you guys. It's 2024. I adore Microsoft Loop but it's website only, so I installed the PWA in Edge... is it really that hard?
* The UI feels clunky, dated and slow.

Adding insult to injury, [Mozilla as a company is catching the spotlight in a rather negative way](https://old.reddit.com/r/browsers/comments/129ul1t/controversial_please_stop_supporting_mozilla/) which isn't helping. At all.

### Microsoft Edge

Edge earns much of the same criticism that Chrome does, being a Chromium based browser. However, Microsoft seems to one-up Google in the most stupid ways.

I daily Edge at work because I enforce Edge as the default (easier policy management across a fleet of computers). And well, I eat my own dog food. 

Edge has gotten bad press due to [Hijacking website content](https://arstechnica.com/gadgets/2021/12/microsoft-edge-will-now-warn-users-about-the-dangers-of-downloading-google-chrome/), [essentially forcing itself to be the default on Windows](https://www.theverge.com/23935029/microsoft-edge-forced-windows-10-google-chrome-fight) and the new tab page which is riddled with malvertising and news (citation needed).

From my personal observations:

* The settings interfacs is borderline unusable due to the confusing labels and organisation
* It forces its AI, Microsoft Copilot, down your throat
* It pops up an annoying sidebar for links from Outlook etc. which nobody asked for
* I find its dev tools extremely frustrating to use
* If you make one wrong click in the context menu, be prepared for an AI-fueled joyride through the depths of Bing

### "You should try out Bluelibrerabbit, it's a new browser by a small team...

Think about it... if you were to get a tetanus shot, would you rather trust Repevax, the tetanus shot that has been around for a while and used on millions of people with well understood side effects, or would you trust some dude that might have a degree in human medicine but gives you a shot that the creator claims they "basically downloaded the recipe from Repevax's GitHub and modified it a bit so it's better"?

This is how I think about browsers. This thing has a plugin for my password manager and I online shop using it... I wouldn't trust anything non name brand.

### And what do I use?

I'm keeping Firefox, despite shitting on it a bit. There are two reasons.

1. It's still the least bad choice compared to the alternatives.
2. If nothing else, we absolutely need an alternative to Chromium, otherwise we'll be at the mercy of whoever leads that project.