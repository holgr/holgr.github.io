---
id: 5798
title: "macOS Sonoma: There's a process stealing your windows' focus"
date: '2024-03-08T19:17:40-08:00'
author: 'Holger Eilhard'
layout: post
guid: 'https://holgr.com/?p=5798'
permalink: /blog/macos-sonoma-theres-a-process-stealing-your-window-focus/
categories:
    - Blog
tags:
    - macOS
    - Mac
---

Sean Harding finally put [into words](https://www.threads.net/@seanharding/post/C4RT42-rqD3) an issue that I've witnessed for a while now on macOS Sonoma.

This is it:
> Weird MacOS thing: the window I am working in will sometimes lose focus (without the app losing focus). Suddenly, and without any obvious cause. It will be as if no window has focus. Sometimes happens as often as every few minutes, sometimes doesn't happen for a long time. I can’t figure out any common variable. But it can be very disruptive.
Has anyone else seen this? Any ideas?

I've [adjusted the Python script](https://gist.github.com/holgr/59f8df7f81aa2b74d67e0ab95e2fd28a) mentioned in the thread to work with Python 3.x that you can get with [Homebrew](https://brew.sh) for example.
<!--more-->

This is what the output looks like:

```
> python3.11 find_focus_stealer.py
2024-03-08 17:20:34: iTerm2 [/Applications/iTerm.app]
2024-03-08 17:20:37: Safari [/System/Volumes/Preboot/Cryptexes/App/System/Applications/Safari.app]
2024-03-08 17:25:17: CoreServicesUIAgent [/System/Library/CoreServices/CoreServicesUIAgent.app]
2024-03-08 17:25:51: Safari [/System/Volumes/Preboot/Cryptexes/App/System/Applications/Safari.app]
2024-03-08 17:25:52: iTerm2 [/Applications/iTerm.app]
```

So it looks like Apple's own `CoreServicesUIAgent` is the problem. Who's going to file the Radar that will immediately be ignored by the time it's submitted?

Update 2024-07-03: Ever since removing Carrot Weather from my Mac this issue has gone away. I'm still certain it's some bug in the underlying macOS, but if this happens to you, check there first.
