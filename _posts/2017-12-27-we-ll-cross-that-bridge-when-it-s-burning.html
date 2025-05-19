---
layout: post
title: We’ll Cross That Bridge When It’s Burning
tag:
- uikit
- appkit
- ios
---
#### Developing Apps for macOS, iOS and tvOS using KitBridge

<figure>![](https://cdn-images-1.medium.com/max/1024/1*4M3tUZsNN2Owjy4tCijm-w.png)

<figcaption>Behold, OrangeCard running on macOS, tvOS and iOS!</figcaption>

</figure>

So, you want to write an app for iOS, macOS and maybe even tvOS? There’s been [a lot of talk](https://daringfireball.net/2017/12/marzipan) lately about the [UXKit.framework](https://github.com/insidegui/UXKitDemo) inside of Photos.app or possibly another replacement framework to bridge the AppKit/UIKit divide. While this may yet come to pass, there’s nothing stopping us from improving the portability of code across macOS, iOS and tvOS _right now_.

#### So, What’s All This About, Then?

While UIKit is clearly derived from the experience of developing AppKit it was a sort of green-field for the developers to create a more modern framework with none of the baggage of AppKit. This lack of baggage makes for more streamlined development but there is collateral damage for experienced AppKit developers who will find some of the changes are hard to adapt to, especially if they need to go back and forth often.

In particular, there are a number of support classes which could have been shared between UIKit and AppKit but weren’t: NS/UIImage, NS/UIColor, NS/UIBezierPath and the foundation class NS/UIView. The difference are more than just name deep, the APIs lack some of the the [impedance matching](https://en.wikipedia.org/wiki/Object-relational_impedance_mismatch) which makes pairing them with other existing frameworks simpler and faster to implement.

### Bridge Over Troubled Waters

First, a little history, [KitBridge](https://github.com/alfwatt/KitBridge) is fairly new hotness, started just this year based on some initial ideas prototyped in [QRKit](https://github.com/alfwatt/QRKit), which implements a very limited cross-platform view framework using a simple [bridging heade](https://github.com/alfwatt/QRKit/blob/master/QRKit/QRDefines.h)r, an NSImage category and strategic use of **#ifdef** directives in the implementations. That simple header and category allows QRKit to provide the same API across all it’s target platforms.

KitBridge takes that starting point and expands on it to include more classes and more categories, which bring balance to view development. With KitBridge you can always use the UIKit API for the bridged classes on either platform. On iOS and tvOS the native methods are used and on macOS (where there is typically more CPU and memory to go around) the methods are provided by categories. There are some cases where UIKit lacks a trusty AppKit method and those are provided as well.

Besides expanding on the number of classes that the bridge supports, KitBridge also makes it easier for projects to share a single implementation file between versions, at least for Views, App Delegates and Controllers.

### Building On Top of the Bridge

<figure>![](https://cdn-images-1.medium.com/max/1024/1*0pWKqZ41IoelUFRczGjLBw.png)

<figcaption>Who doesn’t love a good block diagram?</figcaption>

</figure>

While KitBridge does not cover every possible porting issue (I’ve been adding affordances one by one as I need them for various apps) it does provide a lot of support for writing protable Views and Controllers and already supports two other frameworks which provide a useful set of views: [CardView.framework](https://github.com/alfwatt/CardView) and [SparkKit.framework](https://github.com/alfwatt/SparkKit).

CardView.framework provides a NS/UITextView subclass with a single interface for adding styled text and graphics. CardView was originally extracted from [DeskLamp](https://desklampx.com), and made it’s way into OrangeCard and iStumbler. Now that the framework has been integrated with KitBridge, I’ll be bringing OrangeCard to iOS and tvOS from macOS, once the non-UI platform differences are taken into account.

SparkKit.framework provides a set of data visualization tools with pie, ring, bar, stack, grid and columnar data views, also built on top of BridgeKit. It is enabled by harmonizing the NS/UIBezierCurve interface so that the views have the same drawing code. The most recent release of iStumbler uses SparkKit to draw the Channels and WiPry plugins grid views, and I expect to replace the line graphs and level indicators in an upcoming update.

### Remaining Work

While spackling over the difference between the App and UI Kits helps make portable apps easier, there’s lots to be done still. As the apps I’m building on top of these frameworks evolve I expect KitBridge to evolve as well. Since there seems to be some interest, I wanted to introduce the frameworks because I think they save time when porting apps from macOS to iOS and vice versa, and I hope you enjoy working with them.
