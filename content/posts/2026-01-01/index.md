---
categories: What I Use
date: "2026-01-01T08:00:00Z"
description: Going through what my personal computing stack looks like as we enter 2026.
img_path: /assets/img/posts/20260101
pin: false
tags:
  - opensource
  - productivity
title: Rethinking My Personal Tech Stack
url: posts/rethinking-my-personal-tech-stack
showTableOfContents: true
---

# Origins

Like many people, I usually take the start of a new year as an opportunity to reevaluate some choices and habits I have and see if there is room for improvement. One such area up for review is the set of services, apps, and subscriptions I use outside of work. 

Much of my current computing habits can trace their origins back to the 2000’s, where Gmail marked the start of Google’s growth beyond just search and ads and smartphones began to take off. That was a very long time ago, and a lot has changed in both my own habits and the tech industry since then - so I used most of 2025 to begin researching and evaluating alternatives to what I was currently using. I placed a point on emphasis on identifying options that were cross-platform (avoiding lock in to any one operating system) and gave preference to alternatives that were open source and/or allowed me to either self host or at least keep a copy of my data synced locally, in case of account lockout. I ended up finding a lot of great options, some of which I’ve switched over to entirely. 

This post will highlight some of these alternatives - I plan on making more in depth posts about each one specifically at some point in the future.

# The Stack
## Email
I got my Gmail invite sometime in the middle of 2004, and for over twenty years it has been my main email address. I've used some others over the years for various purposes (most notably my university one), but in the end I forwarded most of those to Gmail. For many years, the benefits Gmail provided were great - a really fast interface built for modern web browsers, ample storage space, and integration with the messaging service Google Talk, which everybody migrated to from AIM in the late 2000's. 

Over time, each of these advantages have disappeared. Google fumbled Google Talk, turning it into Hangouts so it could be used in the Google+ push - and when that failed, it became Google Chat and Meet. The storage space became shared across other Google products like Drive and Photos, driving you towards buying more of it with a Google One subscription. And the Gmail interface has become pretty bloated - it's impossible to ignore the slow page load times when navigating through emails and organizing my inbox. 

I looked around at a bunch of different email providers including Proton, Tuta, even Mailbox.org. In the end, I went with [Fastmail](https://www.fastmail.com/), a service that has been around since 1999 but I had never paid much attention to before now. Fastmail earns its name with how quick its web interface is, and it focuses just on email, calendar, and contacts - although it does have some basic support for Files. Unlike Gmail, it has first class support for using your own domain name and many aliases, giving you flexibility in how you want to setup your mailbox and rules. Its ability to effortlessly migrate my Gmail inbox and calendar cannot be overlooked, and I love how it integrates with my password manager of choice, 1Password, to generate [masked emails](https://www.fastmail.com/features/masked-email/) automatically if I have to sign up for something on a website. Fastmail also seems to be the only service that supports push notifications on the Apple Mail app (on both macOS and iOS) if that matters to you - a feature that not even iCloud Mail can claim! 

If you end up checking out Fastmail, feel free to use my [referral link](https://join.fastmail.com/59d4c1b7) to save some money. 

## Photos
I was a pretty early user of Picasa, and that eventually morphed into Google Photos, transitioning my photos through to it. Through both Android devices and iPhone, I have been steadily adding to Google Photos over the years, but the number of pictures I store there really exploded once my kids were born. It has been a solid service all this time, but recently they have been shoving AI features to the forefront all over the app, which greatly annoys me. I had two other concerns with continuing to entrust all my photos to Google: being on a subscription treadmill to a company that will most likely raise rates constantly over the years to come, and the lack of support if I was to ever become locked out of my Google account. 

So for most of 2025, I've been experimenting with two different services - [Ente Photos](https://ente.io/) and [Immich](https://immich.app/). Both are open source and both can be self hosted, but Ente Photos allows you to pay for them to operate the service and backup your photos. All of the machine learning for facial recognition is done on your device and then the results are synced synced across the other devices. Immich relies on a server (more specifically, a machine learning container) to do all of that work. I like Immich's interface a little bit more, but I am not yet at the point where my home lab is robust enough to entrust it with being the primary mechanism to organize and store my photos for me and the rest of the family. 

So for now, I've moved onto Ente Photos, which I quite like. The facial recognition confused my two sons quite a bit initially, but once I spent a little time training it, it's been much better. The iOS app also feels a lot snappier than either Google Photos or Immich, which the less technical members of my family appreciate. One day in the future I may switch over to Immich, once its a little more mature and my home lab is built out a bit more (including a robust backup strategy).

If you want to check out Ente, you can use the referral code MISCZAK to get 10 GB for free once you sign up. 

## Browser
I've been using Firefox for a number of years due to its [Multi-Account Containers](https://support.mozilla.org/en-US/kb/containers) feature to isolate trackers from companies like Facebook, Amazon, and Google, and I doubled down on my usage of it this past year when Chrome disabled Manifest V2, thereby curtailing support for extensions like uBlock Origin. I am not opposed to paying for content and services on the web (as this blog post will illustrate), but I find it hard to tolerate the onslaught of ad tech that appears everywhere. Firefox also added vertical tabs this year, a feature that I've found that I cannot live without - it's just a much smarter way of keeping tabs organized and readable, even when you have a bunch of them open.

One area where I'm not satisfied is my ability to use the same browser on iOS. Firefox is essentially a reskin of Safari there, but it can't use any extensions, which means that I'm once again without ad blocking. Because of this, I have tended to use Safari on my iPhone with some ad blocking extensions installed. If Apple would allow true browser competition in the app store, I would most likely use an enhanced version of Firefox there. 

## Files
Much like I used Gmail and Google Photos previously, Google Drive became my de facto way of keeping files synced across machines. However, I can count on one hand the number of times over the last decade that I've needed access to some documents when I'm not at home - and when that does happen, I usually have time to prepare and bring them with me. 

Therefore, I've moved my primary file storage to my Synology NAS, which allows me to keep them synced across my desktop and laptop when at home. I can also use Synology's built in backup and sync features to keep a copy with a cloud provider if I want to - which I do with Dropbox. 

I had forgotten that I had about 17 GB of free storage there, as I was an early adopter and beta tester of their Linux client in 2008, and was able to refer a number of friends in exchange for free storage. 17 GB is more enough to keep an off-site backup of some of my most important files, and their [integration with Fastmail](https://www.fastmail.com/blog/files-and-dropbox/) makes it easy to include them as attachments if I do need them one day. 

## Notes
Finally, a service that isn't Google! While I did try Google Keep about a decade ago when I had an Android phone, Apple Notes has been the go-to for a lot of quick notes over the last few years. I have been using [Obsidian](https://obsidian.md/) during that time for more detailed notes, like technical documentation that relies on Markdown, which Apple Notes doesn't support. I like how Obsidian is essentially a nested folder structure of .md files on my local storage, so I have consolidated all my note taking into Obsidian for now. 

One thing that has held me back from Obsidian in the past is the difficulty in syncing it to all platforms I want to use. I use Obsidian on my iPhone, my laptop (Macbook Pro), and my desktop PC. To keep Obsidian in sync on the iPhone, I could keep it in iCloud Storage - but then that complicates syncing it to Windows/Linux devices. If I use something like Dropbox, then I don't have automatic, consistent sync on iPhone. In the end, I ended up resubscribing to Obsidian's built-in sync service, where I am grandfathered into an early bird discount. 

I did pick up a trial of [Notesnook](https://notesnook.com/) in order to take it for a spin, but I don't like the interface as much as Obsidian. 

## Search
While I have used Google Search for a long time, their results have recently fallen off a cliff. It's become almost impossible to find good results when entering search queries; most times, I'm relieved if there's a Reddit discussion as one of the top results since it will usually have some relevance and quality. 

For that reason, I'm switched to [Kagi](https://kagi.com/) as my search engine. The professional plan seems quite steep at first ($10/month for search!) but it cannot be overstated how nice it is to have search results that are actually usable again. Kagi also has a lot of features that make it really easy to finetune your results to improve your signal-to-noise ratio, such as raising/lowering domains in your search results (and comparing your choices to a global leaderboard) and the ability to filter results through lenses, which are preconfigured lists of sources, so that you can get meaningful results even for queries that contain common names or phrases.  

Kagi is also working on a browser (Orion) and a Maps service, both of which I'll be keeping an eye on. 
## Operating System
While I continue to use a Macbook Pro for my day job and as a personal laptop, I've maintained a personal desktop for nearly 20 years that has always been Windows based as its primary purpose is PC gaming. However, Windows has become so enshittified over the last year or two that i felt like my hand was forced to jump into Linux on the PC, even if there will be some casualties (like multiplayer games that use anticheat that is unsupported on Linux).

So before the holidays last month, I installed [CachyOS](https://cachyos.org/) on my desktop and haven't looked back. This will definitely get a more in depth post at some point, but I am enjoying how lightweight and snappy it feels. I haven't noticed any adverse impact on game performance in the titles I've tried - which include Star Wars Jedi Survivor, Witcher 3, Dead Space Remake, and Hades 2. It's my first time really using an Arch-based distro as a daily driver, and the fact that most of the stuff I need can be installed right out of the Arch User Repository has made everything really easy. 

# Refreshing the List
I plan on continuing to evaluate additional options, and will keep an up to date list on what I currently use on my [About page](../../about). I also plan on making a post every year with any major changes or developments. 
