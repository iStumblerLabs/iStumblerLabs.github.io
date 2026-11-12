---
layout: post
title: "iStumbler 2.0, Part 4: Dancing with the Crab"
series: iStumbler 2.0
---

<!-- OUTLINE: part 4 of 4. Thesis: AI changed everything but the process -->

## Intro: Everything Changed

- The crab is Claude, the AI model, working in Claude Code alongside me in the terminal
- TODO: when it joined the project
- The first time it did something that would have taken me a week
- The thesis up front: the tools changed completely, the process didn't

## What Changed

- Speed of the mechanical work: Objective-C → Swift conversion, boilerplate, five platform targets (callbacks to parts 1 and 2)
- Exploring unfamiliar territory: visionOS, watchOS, new APIs, without reading every WWDC session first
- Grunt work that used to get skipped: tests, docs, link checks, release notes
- TODO: a concrete before/after, e.g. hours for a task with and without help

## What Didn't Change

- Knowing what to build, and for whom
- Small commits, code review, tests, release discipline (callback to [Code Review: You Are Doing it Wrong](/2016/04/24/code-review.html))
- Configuration management and dependency hygiene still matter, maybe more
- The finished app is still my responsibility; "the AI wrote it" is not a release note

## The Dance

- Lead and follow: when to drive and when to let it run
- Writing good instructions is just writing good specs
- Reviewing generated code like any other pull request
- TODO: house rules that emerged, e.g. style guides and project instructions the crab follows

## One Session, Start to Finish

The story of one afternoon, which started with this series and ended with a new release of KitBridge.

### 1. The Draft Asked the Pivotal Question

- I asked the crab to outline this series. In the outline for part 2 it left a TODO rather than guess: *how does KitBridge fit
  alongside SwiftUI in 2.0? Does SwiftUI replace it, wrap it, or sit underneath it?*
- That's the pivotal question: does SwiftUI patch the same holes KitBridge exists to patch?

### 2. The Crab Gave the Consensus Answer

- Its answer was careful and well organized: SwiftUI covers views, layout, app structure and the basic drawing types, and
  it's the only real option on the watch. The AppKit/UIKit split leaks back in at the edges: hosting existing views, rich text,
  Mac-assed behavior, and dense tables of live data
- Its recommendation: KitBridge "sits underneath, and gets much smaller." It even offered a headline: *"SwiftUI ate most of
  KitBridge; here's what's left and why it still matters"*
- That's the average of everything ever written on the subject: move to the new hot API as far as you can, and keep the old one
  around as a shim. Defensible, and wrong for this app, because it assumed SwiftUI was where I was going

### 3. Changing the Question

- My answer: I don't need SwiftUI to eat the app, it works well as it is. Don't shrink KitBridge, extend it: bridge the drawing
  types, bridge `NSViewRepresentable`, and keep drawing fast in tables on the Mac
- SwiftUI stopped being the replacement and became the third kit, bridged like AppKit and UIKit
- No amount of API knowledge settles that call. It came from knowing my own app and what already works in it

### 4. The Crab Does the Legwork

- With the direction set, the work was fast:
  - `ILDrawing`, one drawing that goes anywhere: a layer-backed view that doesn't redraw when a table scrolls, an `NSCell` for
    cell-based tables with no view or layer per row, an image drawn off the main thread, or SwiftUI, including the watch,
    where KitBridge's views could never go
  - `ILGradient` on UIKit, which had been on the README's to-do list for years
  - `ILViewRepresentable` and `ILViewBridge`, one spelling for hosting the kit's views in SwiftUI
  - Pixel tests on the Mac, builds for all five platforms, and KitBridge 3.1.0, tagged
- It wasn't frictionless: Swift wouldn't infer the representable's associated types through the bridging protocol. The crab
  tried a few fixes, then settled on one explicit `typealias` line for each conformer and documented why
- The upshot: KitBridge views now port to UIKit and SwiftUI and keep their performance in Mac tables, and the tests check it

### 5. And By the Way, There's a Bug

- While reading SparkKit to see how its views drew, the crab noticed that the line, meter and stack *cells* added a new layer to
  the table every time they drew a row, and never removed one. Tables got heavier the longer they ran
- The new drawing API was exactly what the fix needed. The views and cells now share one set of geometry, the views turn it into
  layers and the cells draw it straight into the table's context
- SparkKit got its first tests, including the one that would have caught the bug

## Where It Stepped on My Toes

- Confident wrong answers, invented APIs, plausible-looking bugs
- Over-eager changes outside the scope of the task
- The consensus answer to the KitBridge question (see above): fluent, well reasoned, and pointed the wrong way, because it
  answered "what is everyone doing?" and not "what does this app need?" What caught it was me knowing my own app

## Where It Surprised Me

- The bug it found on the way, in code I hadn't asked it to look at, because it read the code underneath before building on it
- Leaving a TODO instead of guessing when it didn't know how KitBridge and SwiftUI fit together, which is how the
  pivotal question surfaced in the first place
- TODO: anything else worth calling out

## Conclusion

- Everything but the process: the craft is the same, the tempo is different
- In one afternoon: a draft raised a question, the consensus answer got pushed back on, the work went in small reviewable steps
  with tests on branches, a release got tagged, and a bug got found because someone read the code underneath
- The crab is good at the consensus answer and fast at the legwork. Deciding what the app should be is still my job
- Wrap up the series: what 2.0 is, where to get it, what's next
