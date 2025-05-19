---
layout: post
title: The Sad State of Wi-Fi APIs in Apple Platforms
tag:
- wi-fi
- apple
- api
- wwdc
- wwdr
---

It’s [WWDC](https://developer.apple.com/wwdc/) prediction season again. Spring break for Nerds will soon descend on San Jose with it’s sessions all day, parties all night schedule. Rumors and speculation fly along with wish lists for new features that might be announced in the big keynote. Legions of fans sit huddled over glowing screens watching the video and refreshing news sites to see what other people watching the video are saying about the video.

#### My Wishlist is Short

I only ever have one wish for WWDC: **a single, comprehensive Wi-Fi API on all Apple platforms which can be used for apps released in the App Stores**.

Seems simple enough, we have had [CoreWLAN](https://developer.apple.com/library/mac/documentation/Networking/Reference/CoreWLANFrameworkRef/index.html) on macOS since [10.6](http://www.apple.com/shop/product/MC573Z/A/mac-os-x-106-snow-leopard). In fact, your truly got to introduce the feature at WWDC [citation needed] after working with World Wide Developer Relations organization and spending a lot of time persuading my colleges to just let it happen already.

Just one small wrinkle; there was a question about _which_ Wi-Fi API was going to be published. That WWDC video isn’t available, I presume, because the API that I got up on stage and presented, wasn’t CoreWLAN, and neither the placeholder or the eventual incumbent were my first choice. But no matter, there was an API, it did everything that was needed and it replaced the reverse engineered [Apple80211.h](http://www.macstumbler.com/Apple80211.h) file everyone had been using up to that point.

![](https://cdn-images-1.medium.com/max/460/1*FumEQDdB_Z_EsAlBTk_chg.jpeg "We’re done here, right?")

#### Let’s Roll Some Wi-Fi Apps!

As happy as I was to help publish the Wi-Fi API and get it introduced it to the world, my real motivation was to update iStumbler. It took a little while after the release of SnowLeopard until I was able to get permission to ship [iStumbler Release 99](https://istumbler.net/archive/release99/) in February 2010.

Despite my selfish motivation, I am very proud to have enabled a number of other Wi-Fi apps, which eventually made their way to, the Mac App store. Even if one of them is an [unbelievable facile](https://itunes.apple.com/us/app/wifi-manager/id483772322?mt=12) compile and submit of the example code for CoreWLAN:

![](https://cdn-images-1.medium.com/max/1024/1*cXnkMrtRyKMIfQJOae3zMA.png "Something is missing…")

#### But then iOS

The development of iOS and iPhone was famously segregated from the existing Mac and OS X development. As such, they did not share their Wi-Fi Client stack (the user-space software which keeps the list of preferred networks and manages the automatic-join process) until fairly recently, after the teams where eventually merged in Apple’s [Deforistallizaion](https://www.youtube.com/watch?v=tVq1wgIN62E) process.

The iOS Wi-Fi team decided early that they were not going to offer a public API and have been doggedly hardening each release to prevent access to apps who try to use it, even on Jailbroken devices. My understanding is that it’s considered a privacy risk, as a Wi-Fi scan list can be submitted to a number of online services to determine the user’s location (which is exactly what CoreLocation does). If only there were some way to notify the user that an App wanted access to a hardware feature with some privacy or security implication…

![](https://cdn-images-1.medium.com/max/1024/1*gFXC-lcHAPbGtCECHg3MLQ.png "I just can’t think of a way to get affirmative consent from a user…")


#### Enter Sandbox

Much has been written about the limitations of the App Sandbox and the Mac App store over the past few years, despite the (relatively modest) amount of work involved, I’d be very happy to have iStumbler in the Mac App store. Sadly, I missed the window to submit it before the App Sandbox became a requirement, which as you can see from the [App Sandbox Design Guide](https://developer.apple.com/library/mac/documentation/Security/Conceptual/AppSandboxDesignGuide/DesigningYourSandbox/DesigningYourSandbox.html) precludes using CoreWLAN:

> With App Sandbox, your app cannot modify the system’s network configuration (whether with the System Configuration framework, the CoreWLAN framework, or other similar APIs) because doing so requires administrator privileges.

Which means iStumbler stuck outside of the App Store and it’s throngs of paying customers, and instead has to rely on discovery and sales via my [web site](https://istumbler.net/store.html) (hint-hint). But it’s worse for the developers who have Wi-Fi apps already on the store: they can’t be updated with new features, because that would require sandboxing. Which isn’t allowed.

This creates a tenuous situation for people trying to make a living writing applications which utilize Wi-Fi. You can imagine my dismay when 10.11 shipped and iStumbler started emitting this warning:

> airportd[#]: WARNING: iStumbler (#) is not entitled for com.apple.wifi.scan, temporarily allowing request with background priority — — all entitlement requirements will be strictly enforced in a future release

Thankfully the warning is gone from 10.12, but for a year or so there it looked like we were headed deep into Kafka territory: A Public Wi-Fi API exists, but you can’t use it outside of the sandbox without entitlements and we don’t allow [those entitlements](http://stackoverflow.com/questions/37529193/what-is-the-entitlement-for-a-mac-app-to-use-corewlan-to-access-wi-fi-in-the-san) to be used for Developer ID or Mac App Store apps.

#### But Who Cares? Really?

You really should. If you’ve ever stared at your screen waiting for something to load, spent an evening debugging a family member’s broken Wi-Fi connection, had to call a nerdy family member over to fix a broken Wi-Fi connection or generally wondered “how does this magic technology which brings me kitten photos by the exabyte work?” then you have some skin in the game.

Access to the internal workings of your computer might break the feeling of magic for some, and there are things which you don’t need or want to see, but we all care very much about our connection to the rest of humanity and having the tools to make sure that our Wi-Fi is connected, performing well and reliably is critically important to our sense of well-being in a more and more interconnected world.

#### A Modest Proposal

I’m going to preface this by admitting that it’s a big ask to get Apple to change their course on this. User privacy protections, concerns over battery usage, the need for additional testing to make sure that even aggressive use of the public APIs don’t degrade system performance unacceptably all take time and political will to make happen.

**Apple should publish a single, well documented and comprehensive Wi-Fi API which works on all Apple Devices which can be deployed to the App Stores**. Let the user know that an app wants to use Wi-Fi, and let them decide if they want to enable Wi-Fi access in the foreground or background in the same manner as location services, the address book or camera.

It might seem like a niche feature, **but network connectivity problems are difficult problems to diagnose and resolve.** Hard problems require a robust and ever changing set tools to collect information and improve the user experience.

Pretty please?
