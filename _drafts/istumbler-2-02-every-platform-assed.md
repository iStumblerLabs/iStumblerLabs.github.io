---
layout: post
title: "iStumbler 2.0, Part 2: Mac-assed, iOS-assed, Watch-assed, TV-assed and Vision-assed"
series: iStumbler 2.0
---

<!-- OUTLINE: part 2 of 4. Builds on the 2017 post "We'll Cross That Bridge When It's Burning" -->

## Intro: What "-assed" Means

- The "Mac-assed Mac app" idea: an app that behaves like it was born on the platform, not ported to it
- TODO: link the origin of the phrase
- The goal for 2.0: one codebase, five apps, each fully native to its platform
- Why not just Catalyst, "Designed for iPad", or a single SwiftUI view tree everywhere?

## KitBridge, Then and Now

- Quick recap of the [2017 KitBridge post](/2017/12/27/we-ll-cross-that-bridge-when-it-s-burning.html): bridging NS/UI classes so views and controllers share one implementation
- What changed: Swift, new platforms (watchOS, visionOS), and SwiftUI arriving in the middle of it all
- TODO: how KitBridge fits alongside SwiftUI in 2.0 (replaces, wraps, or sits underneath?)

## What's Shared, What's Not

- The shared core: models, scanning, data, and most of the drawing
- The per-platform shell: app lifecycle, navigation, menus, windows, input
- TODO: a diagram or rough percentage of shared vs. platform-specific code

## Platform by Platform

### Mac-assed

- Menus, multiple windows, keyboard shortcuts, inspectors, AppleScript/Shortcuts
- What the Mac app can do that nothing else can (CoreWLAN, full scan data)

### iOS-assed

- What a Wi-Fi tool can actually do under iOS sandboxing and API limits
- Touch, size classes, widgets

### Watch-assed

- Glanceable: what's worth showing on a wrist?
- Complications, tiny screens, and short-lived sessions

### TV-assed

- Focus engine, ten-foot UI, the remote
- Why anyone wants Wi-Fi info on their TV (TODO: the real use case)

### Vision-assed

- Windows and volumes in space; spatial signal visualization?
- What visionOS got right for this kind of app, and what was awkward

## Lessons

- Where bridging pays off and where it leaks
- Testing five targets without losing your mind: CI, previews, simulators
- TODO: the platform that was hardest to get right, and why

## Next Up

- Teaser for part 3: the frameworks underneath all of this
