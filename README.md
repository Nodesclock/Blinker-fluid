<img width="100" height="100" alt="New Project 20  0B9169A" src="https://github.com/user-attachments/assets/67a507ac-e528-4720-abd8-23930b242dc0" />

# Blinker Fluid
(WARNING: THIS IS EXPERIMENTAL AND IS PRONE TO CRASHING AND BREAKING)

## Chromium Blink + V8 browser engine ported to iOS 15.4 with no WebKit.

Blinker-fluid is an experimental browser for jailbroken iPhones that runs a real Chromium rendering engine on iOS without using Apple's WebKit engine.

## Why did I start this project?
I started this project mainly because my main browser on my PC is Ungoogled Chromium so why not try porting it onto iOS? Also, the fact most sites I use require updated webkits annoyed me. (This is my first major project I'm building in a long time)

## What are the requirements for Blinker fluid and How do I install it?
 Tested & functional: An arm64e device on iOS 15.4 is recommended (This was only tested on an iPhone 13 pro running iOS 15.4 jailbroken)
 
 Untested: This should work on any arm64e device running any iOS 15 version, but I haven't tested it on any other device and other iOS 15 version. (Make an issue ticket if your iOS version is not iOS 15.4 and it doesn't work/crashes. This works on iOS 16 and 26.1 when using livecontainer too apparently :D)

# Features (Current)

- Loads most modern websites that the iOS 15 webkit doesn't support (Some sites are still broken)
- Real Blink rendering engine
- Real V8 JavaScript engine
- Video playback (Fullscreen broken)
- Search / URL bar
- Tabs (Does not save after app restart!)
- Bookmarks 
- Downloads (Broken)
- Dark mode support (Buggy and works on only certain sites) 
- Custom start page 
- Different search engines (Google and DuckDuckGo were the only ones I tested)
- Desktop and mobile site (Untested)
- Optional SOCKS5 / Tor proxy support (Untested, most likely broken)

# Trollstore method:
1. Download the IPA file from releases.
2. Open the import the IPA file to Trollstore.
3. tap install and let it download.
4. Go to your homescreen and open the app.
5. Blinker fluid opens, use it or not.

### Any other IPA signing tool (Esign, Gbox, etc)
- No idea if anything other than Trollstore works, but they hopefully should work too!

### DISCLAIMER: THIS IS JITLESS EVEN WITH TROLLSTORE!
#### What to expect with Blinker Fluid being jitless?
- Expect heavy performance issues.
- Expect frequent crashing.
- Expect a lot of lag.

#### Why is this jitless?
I tried getting it to run with JIT enabled through Trollstore, but it kept crashing so I'll leave problem for future me. :/

## Screenshots of Blinker Fluid Working (iOS 15.4 on an iPhone 13 pro):

| [Github](https://github.com) | [Pinterest](https://pinterest.com) | [Gemini](https://gemini.google.com) |
|---|---|---|
| <img width="500" height="1000" alt="8252CD69-29BF-42EA-8C7E-41ACCB40BC5D" src="https://github.com/user-attachments/assets/20717283-7353-4880-beaa-413aea0ad65b" />| <img width="500" height="1000" alt="1B3CE020-188F-4FF4-9F52-D6A526BF6E12" src="https://github.com/user-attachments/assets/b03ae5e3-6fd0-475a-8508-63712f4be516" />| <img width="500" height="1000" alt="60853588-4371-4231-B516-78F635F9C1FA" src="https://github.com/user-attachments/assets/da35d2e6-2507-4bf9-af3a-1ed14321ab7d" />

# What is being worked on or will be added in the future:
- Better iOS version compatibility (iOS 16 confirmed to work and 26.1 through live container is also confirmed to work already. Working on an iOS 14 backport!)
- Video playback full screen support
- Adding JIT support (Main priority at the moment, will probably fix many issues alone)
- ChatGPT website crashing the app (Already working on it)
- Built-in ad blocker (Planned for later on, too complex for me at the moment)
- Crashing caused by tapping on links too fast. (Another main priority)

# What will most likely never be added:
- Extension support/ad blocker (Very time consuming and complicated. Might add a built in ad blocker, but not my priority at the moment.)
- Password Manager (Same reason, very time consuming and complicated. Will most likely never be added)
- Reader mode & translation (I've already tried and I just can't... Also, who uses Reader mode anyways?)
- Website History (Too complicated for me)
- Incognito mode (Yeah... it's pretty much impossible to my knowledge...)

# Known issues:
- Downloads being broken.
- Tabs not saving after restart. (Already working on a fix)
- App crashing randomly. (Most likely because of it being jitless)
- ChatGPT website crashes app almost instantly. (Already working on a fix too, please make a ticket if you find any sites that crash when opened in the issues page! :D)
- App crashes if you click on links or change sites too quickly without letting the first site load properly.
- Dark mode only working on some websites.
- Some weird audio issues.
- A lot more issues.

# How does Blink/V8 run on iOS?

Apple requires every iOS browser to use WebKit and all browsers on the appstore are basically just reskins of Safari... The only alternative, BEK (BrowserEngineKit), requires iOS 17.4+ and an Apple entitlement and below that, there is genuinely no supported path at all. Getting Blink to even show a web page on iOS 15.4 was pretty annoying so here are the steps and problems I ran into while trying to port this on iOS. To port it, I had to solve a couple problems like how V8's JIT causes the app to just die at launch, so it runs jitless under basic fakesigning. Chromium tries to reserve a lot more virtual memory than iOS's 4GB limit allows, so the sandbox, pointer compression, and caged heap were disabled and the allocator was basically tricked into using 256MB memory pools. The rendered page normally gets displayed through a BEK class that literally just doesn't exist on any iOS version before 17.4, causing a black screen, so the render layer is attached to a plain UIView. This really only works because everything runs in a single process (which is why incognito is basically impossible to add to my understanding). Also, a few iOS 17 only APIs had to be removed to stop the app from crashing instantly on iOS 15.. A custom boot log and crash handler had to be written and made it actually possible to be able to find and fix these annoying problems. (This took about a month or so to complete)

## DISCLAIMER: AI WAS USED IN THE PROCESS OF BUILDING THIS!!
### AI was specifically used as assistant as it should in:
- A decent amount of the UI. (specifically main menu UI, UI will be completely redone by me when I'm done fixing the main issues)
- Research about how Blink/V8 could be ported onto iOS.
- Some small quick bug fixes.

## Where's the source code?
no

# Credits:
- Reynard Browser by Minh Ton heavily inspired the making of this
- Chromium open-source project
- @miku_draws_random_stuff on Instagram for the app icons! (Great friend, great artist)
