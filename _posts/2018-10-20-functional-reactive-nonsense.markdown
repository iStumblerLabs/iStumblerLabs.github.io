---
layout: post
title: Functional Reactive Nonsense
---

![](https://cdn-images-1.medium.com/max/309/1*sUrELFhihxAtm21dthWzxw@2x.jpeg)

There is a perverse inversion in many Senior Level engineering job postings; they rigidly dictate a particular stack of technology, which the company has typically invested considerable time in implementing and tailoring to the needs of their application. While this makes some sense for a mid-level or junior developer its he opposite of what you should be looking for in a Senior engineer:

> **“It doesn’t make sense to hire smart people and then tell them what to do; we hire smart people so they can tell us what to do.”**

> — Steve Jobs

I suspect that these postings are the result of a manager trying to maintain a system designed by a f _orward looking_ developer who sold the team on it’s benefits but never quite realized them before departing for greener pastures, leaving an big ‘ol tech stack in the repo behind them as they go. By suspicions I mean; I’ve seen this happen more than once. I might have done it myself, maybe, long ago.

Typically these stacks will provide an “Over the Top” solution to programing on the target platform, replacing some or all of the vendors native tools, with more “modern” or “advanced” or “convenient” or “expressive” or “safe” versions, often in combination, always without quantification. The sales pitches vary from sensible and desirable, such as allowing for cross platform development from a single code base to the outer orbits of architectural astronauts, looking for a [magic bullet solution](https://en.wikipedia.org/wiki/No_Silver_Bullet) to solve all software development problems with concise self documenting code.

There are a few stacks I could poke holes in but today I’m going to focus on [Reactive Cocoa](http://reactivecocoa.io) ( [React Native](https://facebook.github.io/react-native/) was a close second). Generally any framework which intends to replace a portion of the native toolkit is likely to have similar issues, namely the tradeoff between Runtime, Development time, and Maintenance time doesn’t add up for real world usage. Let’s look at each of these in turn.

#### Runtime Performance Matters

Code is CO2\. Every line of code which eventually runs on a processor [consumes energy](https://en.wikipedia.org/wiki/Landauer%27s_principle). In our current carbon economy this means that on average, nearly every line of code we write will result in the release of Carbon Dioxide into the atmosphere. Heat will need to be dissipated, blowers move air, batteries discharge, systems slow down.

Every additional layer of software on top of the hardware platform adds to the performance burden of the system. If you’re paying for the hardware and electricity (in a server farm, for e.g.) then it’s your problem, but if you’re writing software that runs on people’s devices, your convenience is [paid for by your customers](https://github.com/ReactiveCocoa/ReactiveCocoa/issues/1503). Packing an over the top framework into your app is a bit like showing up at a friends house for dinner with an entourage. It might make you feel cool, but you aren’t being a very good guest.

Physical limits aren’t something we like to admit exist in software development, “Moore’s Law will surely save us!” And for decades, it has, but as we get closer to the quantum realm (and eventually cross over into it) in the chip fabrication process, [the pace has slowed](https://qz.com/852770/theres-a-limit-to-how-small-we-can-make-transistors-but-the-solution-is-photonic-chips/), and the exponential curve for Silicon begins to look more sigmoid in shape. We can no longer expect our processors to get faster at the breakneck pace of the 90s and 00s, optical and quantum processors will eventually become a commercial reality and provide great steps in processor power, but for the foreseeable future they won’t be included in consumer devices.

> **“It takes about a year, but once you get it, you’ll be super productive.”**

> — Some Reactive Cocoa Developer

#### Developers Time Matters

[Reactive Programming](https://en.wikipedia.org/wiki/Reactive_programming) on it’s own might not over-burden your app, in fact there are applications where it is clearly the [best choice](http://conal.net/papers/icfp97/). But for most apps it doesn’t add much except Library size, runtime penalties and additional learning needed for developer to fully utilize it. This is substantial, especially when implemented on top of Apple’s platforms, which already have a highly optimized UI development tools.

Reactive programming promises a lot, including easier to understand code and better developer experience. Except that in every case I’ve seen, it takes longer to write an app this way, and it can be challenging to debug. Once when working on integrating into a Reactive Cocoa app the lead told me I’d need to maintain my own timer for a query sent to a connected hardware device, because they couldn’t reliably generate and propagate RAC signals once per second.

> Always write code like your maintenance programmer has a shotgun, and knows where you live. — Larry Wall

#### Maintenance Time Matters

Working with a new technology stack might seem exciting to you, it might even distract a little from the fact that most apps aren’t very groundbreaking and that writing a shopping cart or picture sharing app isn’t going to get you inducted into the programming hall of fame. You might become tempted by one of the constant sirens of human experience, the deep need for newness.

Without this core drive humanity would never have become the super dominant species and we wouldn’t have memes. It’s hard to imagine a world where everyone is always content actually working well in practice. If everyone is a slacker and expends minimal effort to simply survive there would be no growth, no art, no striving for a more perfect world.

While this drive for neoteny May have gotten us here, it’s not helpful when you are trying to engineer a system for performance and reliability and especially when you are planning for long term support. Newness in the service of entertaining the people working on the project isn’t doing the business or its customers any favors and it does a great disservice to whoever has to maintain the product later. In order to improve or make repairs they will have to understand all the underlying tools of the platform as well as all the over the top software, in addition.

#### User Experience Matters Most

While I’m sympathetic to the desire to do good work and to feel like the products we design and build are using the most modern tools and methods the reality of software product engineering is that it has to address a messy reality, and in doing so it becomes complex.

This complexity is not the result of architectural failure, but the day to day reality that our software must navigate the various pressures on it. Good architecture seeks to make the daily tasks of software engineers simple, repeatable and direct. The best platforms deliver this, or more precisely, are managed to consistently maintain these qualities as features are added and removed.

While the native (Objective-c) toolkits of macOS, iOS and (NDK) Android may be out of fashion, but they still deliver the best possible user experience by virtue of their being the foundation on top of which all others are built. You may be able to run fast on stilts, and the feeling of the air in your hair is exhilarating, but when you trip it’s a long fall.