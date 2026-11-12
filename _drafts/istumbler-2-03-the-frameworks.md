---
layout: post
title: "iStumbler 2.0, Part 3: The Frameworks, and How They Fit Together"
series: iStumbler 2.0
---

<!-- OUTLINE: part 3 of 4. TODO: confirm which frameworks ship in 2.0 and their current names -->

## Intro: An App Is a Stack of Small Libraries

- Philosophy: small, focused, open source frameworks, each useful on its own
- Contrast with Automated Dependency Management Considered Harmful (TODO: link once that draft is published): few dependencies, all of them yours
- TODO: which of these are public on GitHub, and under what license

## The Map

- TODO: a layer diagram, from platform APIs at the bottom up to the app
- Rough layering:
  - **Platform glue:** KitBridge
  - **Data and services:** Soup, LiveBundle, IcedHTTP, FourCorners
  - **Views:** SparkKit, CardView
  - **App:** iStumbler and its plugins

## Framework by Framework

For each: what it does, why it exists, what changed for 2.0, and one small code sample.

### KitBridge

- Shared NS/UI view and controller APIs across all five platforms (more in part 2)

### SparkKit

- Small, fast line, pie, dial, bar, ring, stack and grid views
- Signal strength over time is the obvious one in iStumbler

### CardView

- Styled text and graphics in a single text view, originally extracted from DeskLamp
- Where it shows up in iStumbler (inspectors, info panes)

### FourCorners

- CoreLocation helpers; tying scan results to place

### Soup

- Object persistence modeled on the Newton soup API
- Why not Core Data or SwiftData?

### LiveBundle

- Updating resources from the web without shipping a new build

### IcedHTTP

- A tiny embedded HTTP server; TODO: what iStumbler uses it for

## How They Work Together

- Follow one piece of data end to end: a Wi-Fi scan result → model → Soup → SparkKit graph → CardView detail → each platform's UI
- Where the seams are, and what keeps them from tangling (protocols, no circular dependencies)

## Maintaining a Family of Frameworks

- Versioning and releasing them together vs. independently
- Swift Package Manager as the glue
- TODO: anything you would split, merge, or retire after 2.0

## Next Up

- Teaser for part 4: how all of this got built, and who (or what) helped
