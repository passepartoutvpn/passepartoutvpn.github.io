---
layout: post
title: The path to an obscure crash
tags: [development, swift]
---

One month after its first, painful release, Passepartout v3 is close to being stable.

However, a couple of regressions were still haunting me.

Here I want to describe the absurd journey into one of them, that started with a report [from GitHub](https://github.com/passepartoutvpn/passepartout/issues/1204), and [one from Reddit](https://www.reddit.com/r/passepartout/comments/1j0lbqa/not_open_in_sonoma_any_idea/). Both users were reporting that the Mac app was crashing on launch.

The reports led me to think that the regression was caused by the macOS version, or the CPU architecture, as both users were using an Intel-based machine.

### The Xcode Organizer

I had several (unhelpful) crashes in the Xcode Organizer confirming the issue:

![Xcode Organizer](/s/posts/2025-03-03-01.png)

Looking further into some crashes, I could spot a few SIGILL (Illegal Hardware Instruction) that reinforced the idea of a platform-related issue. Add to that, one of the threads had intense Core Data + CloudKit activity ongoing. It must be Core Data, I thought, given that Passepartout performs its sync precisely when the app launches.

*Doubt #1: how can the app launch at all if the arch is unsupported?*

*Doubt #2: is the Core Data stack trace relevant? Is it the thread that is actually crashing?*

### Never read crash reports only once

Passepartout is a privacy-oriented app. There is no external framework e.g. Firebase to help with crash resolution, so Xcode is the only technical resource at disposal. Plus the patient support from the affected users.

Eventually, Core Data was a distraction. Every report was crashing on "Thread 0", i.e. the main thread. There were also crashes from macOS 15 and ARM64. Fewer, but non-zero.

This stack trace shed some light in that the injected AppDelegate could be the culprit. But where? And why?

```
Thread 0 Crashed:
0   Passepartout                    0x00000001029bb154 0x102764000 + 2453844
1   Passepartout                    0x00000001029baf6c 0x102764000 + 2453356
2   Passepartout                    0x00000001029bb83c 0x102764000 + 2455612
3   Passepartout                    0x00000001029ba6ac 0x102764000 + 2451116
4   Passepartout                    0x00000001029b66d4 0x102764000 + 2434772
5   Passepartout                    0x000000010276d0d4 0x102764000 + 37076
6   Passepartout                    0x000000010276c868 0x102764000 + 34920
7   libdispatch.dylib               0x000000018ab68658 _dispatch_client_callout + 20 (object.m:576)
8   libdispatch.dylib               0x000000018ab69ea0 _dispatch_once_callout + 32 (once.c:52)
9   Passepartout                    0x000000010276b2ac 0x102764000 + 29356
10  Passepartout                    0x000000010276b2f0 0x102764000 + 29424
11  Passepartout                    0x000000010276b3c0 0x102764000 + 29632
12  SwiftUI                         0x00000001b977a934 FallbackDelegateBox.delegate.getter + 68 (FallbackDelegateBox.swift:36)
13  SwiftUI                         0x00000001b9e8cea8 specialized NSApplicationDelegateAdaptor.wrappedValue.getter + 156 (FallbackDelegates_Mac.swift:93)
...
```

### Reproducing the crash (pt. 1)

Assuming that the AppDelegate was doing something wrong, there was even a much bigger issue: I could not reproduce the crash on my machine. I realized, though, that a friend of mine had an Intel MacBook with macOS 14, so I asked for his help.

He gave me access via AnyDesk to push ad hoc builds to the machine. The latest app version crashed consistently. Off to a good start. At that point, I spent a few hours trying to exclude potentially offending parts from the launch code, sadly to no avail. Consider that any change in the code implied archiving and sending a build via AnyDesk to test it. It was exhausting, and the afternoon led nowhere.

### Reproducing the crash (pt. 2)

I decide to give a shot to virtualization. Most crashes came from macOS 14, and not necessarily from Intel machines, so this could work. These were the steps:

- Get [UTM](https://mac.getutm.app/) to run a VM on Mac. *Highly recommended!*
- Download a restore image for Sonoma (~14GB)
- Regenerate the provisioning profile with the VM UDID
- Send the development build via a shared folder to the VM

The app crashes. Hooray!

### Git to the rescue

Time to locate where the regression was introduced. I rebuilt the app for each commit that sounded relevant, and after 10-20 builds, I found out that the crash was introduced in [this pull request](https://github.com/passepartoutvpn/passepartout/pull/1200) about the light/dark mode picker in the app preferences. WTF?!

It turns out, the widely used [`NSApp`](https://developer.apple.com/documentation/appkit/nsapp) singleton appearing in this bit of the PR is an **implicitly unwrapped optional**.

<script src="https://emgithub.com/embed-v2.js?target=https%3A%2F%2Fgithub.com%2Fpassepartoutvpn%2Fpassepartout%2Fblob%2Fv3.1.1%2FPackages%2FApp%2FSources%2FUILibrary%2FBusiness%2FAppearanceManager.swift%23L66-73&style=default&type=code&showBorder=on&showLineNumbers=on&showFileMeta=on&showFullPath=on&showCopy=on"></script>

### A race condition about NSApp

It's finally revealed that, very early in a Mac app lifecycle, `NSApp` may be nil. This was more often the case on macOS 14 than 15, but still a hideous race condition.

Here goes the simplified stack call:

- main
- AppDelegate.init
- AppearanceManager.init
- AppearanceManager.systemAppearance.didSet
- AppearanceManager.apply()
- NSApp.appearance = ...

In the last call, `NSApp` may be nil and implicitly unwrapped, leading to the crash.

### Lessons learned

This was one of those bugs that make you question everything—platform differences, architecture quirks, even Core Data conspiracies—before revealing a simple yet insidious root cause: a race condition with `NSApp`.

The takeaway? Even well-documented singletons aren't always safe to assume as non-nil. And when debugging obscure crashes, patience and a systematic approach (plus a good VM setup) can make all the difference.

Passepartout v3.1.5 [will handle this case properly](https://github.com/passepartoutvpn/passepartout/pull/1224), ensuring that `NSApp` is accessed only when it's actually available. Hopefully, that's one less obscure crash lurking in the shadows.

To Apple and Swift: isn't it about time to discourage/deprecate the use of implicitly unwrapped optionals?
