---
layout: post
title: "iStumbler 2.0, Part 1: The Swift Conversion"
series: iStumbler 2.0
---

<!-- OUTLINE: part 1 of 4. Series: Swift conversion → KitBridge on every platform → the frameworks → AI and process -->

## Intro: Objective-C Gives Me the Ick

- Hook: two decades of square brackets, and one day the feeling just changes
- What the ick actually is, beyond "it's old":
  - header/implementation duplication, nullability annotations as an afterthought
  - every new Apple API is designed Swift-first, Objective-C gets the leftovers
  - the shrinking pool of people who want to read it (including future me)
- What Objective-C still does better, honestly (dynamism, categories, fast compiles); this isn't a takedown
- Why now, for 2.0, and not five years ago

## The Starting Point

- Shape of the codebase going in: app, plugins, frameworks
- TODO: rough size (files / lines of Objective-C) before the conversion
- What had to keep working the whole time: shipping app, existing users, plugin model

## Strategy: Big Bang or Strangler Fig?

- Options considered: rewrite from scratch, convert file-by-file, wrap and replace
- What was chosen and why
- Order of operations: leaf frameworks first, or app shell first?
- Living with a mixed codebase: bridging headers, `@objc` everywhere, the generated `-Swift.h` header

## What Translated Cleanly

- Model types becoming structs and enums
- Optionals replacing nil-messaging (and the bugs nil-messaging had been hiding)
- TODO: one before/after code sample that shows the win

## What Fought Back

- Categories → extensions, and where that's not a one-to-one swap
- Runtime tricks: KVO, selectors, swizzling, `NSClassFromString` plugin loading
- C APIs (CoreWLAN, IOKit, BSD sockets) and unsafe pointers
- Concurrency: GCD and delegates → async/await, actors, and Sendable warnings
- TODO: the single nastiest bug the conversion introduced (or revealed)

## Tooling and Packaging

- Swift Package Manager all the way down (link back to the [SPM post](/2024/08/19/Objective-Swift-Package-Manager.html))
- Build times, test coverage before and after
- TODO: Swift language mode / minimum OS versions chosen, and why

## Results

- TODO: line counts after, crash rate, build time, anything measurable
- What it feels like to work in now
- Was it worth it? The honest answer

## Next Up

- Teaser for part 2: one codebase, five "-assed" apps
