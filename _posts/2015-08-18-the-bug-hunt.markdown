 # The Bug Hunt

<img src="/images/2015/20150818-aliens-script.webp" alt="Is this going to be a dand-up fight, Sor, or another bug-hunt?" width="512">

## HOW I LEARNED TO STOP WORRYING AND LOVE BUG REPORTS

iStumbler was free software for a long time, of course I did everything I could to make it useful and bug free but when bug reports would come in, they were tagged and fixed in the next version of the app. Sometimes that was a long time later. If someone was really upset about a particular issue, I could always direct them to the source code and suggest that a patch would always be appreciated. That was not always appreciated; but at least it was a viable option.

Now that iStumbler is neither Free nor Open Source those convenient lines of escape have been closed off, and since I’m interested in having a lot of happy paying customers, any bugs they report have to be fixed. Since the initial release of iStumbler 100 I’ve done more than ten bug-fix releases and one feature release, focused on bringing back features dropped since Release 99 because they had bugs and fixing new issues found in the field. Here’s a short list of hi-lights complied from the change log:

- Build 88: MAC Address Formatting and logging fixes, licensing bugs
- Build 90: Wi-Fi Preferences issue, adds Stripe payment processor
- Build 92: The Sparkle updater came back
- Build 104: Adds “Let’s Move” Installer, Font Scaling & Bold Chart lines
- Build 115: Bonjour plugin fixes, UI Fixes & Additions
- Build 117: Even More Bonjour Plugin fixes
- Build 121: Yosemite Compatibility, Added Crash Reporting
- Build 122: UI Issues, Crash Reporting Bugs, Added Exception Recovery
- Build 123: Licensing Bugs and UI Improvements

All these over the course of just four months, but I’m really happy with the results. Release 123 has had far fewer support issues, and continues to sell steadily. This constant improvement is the hallmark of active product development which users really love, along with responsive support, which I’ve tried to provide.

Support requests from paying customers are a completely different issue than bug reports from free users: there’s money on the table. Font Scaling and Bold Graph Lines, for example came directly from a support issue which resulted in me issuing a refund because the thin lines and small type just weren’t visible to someone without perfect eyesight. Font Scaling had existed in previous versions but had issues which made me remove it for the 100 initial release.

## IF A CRASH HAPPENS IN THE WOODS

Even with paying customers, the problem is getting people to tell you if there is a problem. Or, perhaps, to tell you there is a problem in a way that you can act on it. Vague bug reports come in to the support email saying “the app crashes”. Without any of the supporting logging, stack tracing and other technical arcana developers spend our days contending with. Normal users seldom care to see these details, and they shouldn’t have to.

Having a reporting system built into the app helps you take better care of your customers by helping them provide you with useful information.

Looking around at the currently available options, Crashlytics, long the gold standard has become a ‘Freemium’ product (-ium is Latin for ‘not really’) and been integrated into Twitter’s Fabric framework for mobile app development. There is a Mac OS X beta available, apparently on request, I didn’t bother asking.

If I’m going to take the time to call out chairman Gruber for his use of Google Analytics (though, generously, he shares the gleaned information with us) it would be painfully Hippocratic of me use Crashlytics in iStumbler. I insist on a very strong internal privacy and security policies for all the work I do, so collecting crash data is no exception: everything has to be private and under my control.

It always helps to spell out the requirements: user friendly, private and secure bug reporting which helps to improve customer satisfaction and reduce the rate of errors in the field. No problem. But I didn’t want to built it myself, so I went looking for an Open Source solution.

The first thing I found was the Plausible Labs, PLCrashReporter framework, a liberally licensed native framework for Mac OS and iOS, the only thing missing was the reporting UI and a corresponding CGI script to receive the reports. I slapped those on the side, tested the crash reporting and shipped them in Build 121 along with some Yosemite fixes. Problem solved, right?

## ERRATA AND EXCEPTIONAL SITUATIONS

Now, error handling on OS X and iOS doesn’t have the most coherent developer story. The Foundation and AppKit frameworks, along with the Objective-C runtime provide a number of different ways of dealing with different types of problems, from traditional C return codes in the low level and kernel frameworks, with the occasional use of buffer pointers to get detailed information, to the CFError/NSError abstractions built into CoreFoundation. Add in the C++ and Objective-C Exception handling mechanisms (and I guess Swift now, too) and the UNIX process signals and you have what could be described as a “toxic hell-stew” of problem sources.

Low level errors typically boil up to crashes or exceptions so for our purposes we don’t need to touch on them, while uncaught NSExceptions will eventually crash the app, unrecovered NSErrors aren’t reported by most CrashReporting tools. My next task was to generalize the reporting tool to catch the three big issues: Crash Reports, uncaught NSExceptions and NSErrors which are not recoverable, as well as bug reports from users who have some other problem they want help with.

So, I added support the CrashReporter for catching and displaying these as well, by intercepting the NSApplication error presentation mechanism the library can provide a report window in place of the standard alert dialog. Similarly, unhanded exceptions which would normally crash the app are caught and presented to the user. Finally, an open ended bug report window allows users to submit any request they like, quickly and right in the app. There’s even a keyboard shortcut: Command + !

## GETTING BURIED

Now, the downside of casting a wide net is that you catch a lot of fish, or in this case email Trouble Reports. Incoming support requests went for an easily manageable handful a day to a completely overwhelming 30–100 a day, most of which could not be responded to since they lacked email addresses. With my support inbox overflowing I started looking at options for reducing the deluge to a manageable stream of actionable information.

The first step, of course, it to stop the bleeding. Serious issues which are frequently reported get fixed fast. This is why duplicating Radar bugs gets issues fixed at Apple. Incident count is very hard to argue with, and having robust reporting infrastructure in place really helps get a representative sample of the problems that users are having with your app.

Once the frequently repeated problems are resolved there is a class of less frequently encountered issues which cause disproportionate user distress. Any issue having to do with updates, licensing and installing the app need to be addressed quickly to help smooth over the rough spots in the application lifecycle. Many of the fixes made to Release 100 dealt with this (and to be fair, licensing was a new feature in this release so you can expect some bugs to shake out of all that new code).

## RECOVERY AND REDEMPTION

Once the bleeding has been stopped, and the loudest complaints taken care of what next? Well, now that the popular and painful issues are out of the way it’s time to go for the really ugly problems. You know the ones: they lurk in the corners of your user experience and wreak such havoc that the only recommended solution is “Just blow everything away and re-install the app.”

<img src="/images/2015/20150818-trinity-shot.webp" alt="Trinity Shot" width="512">

We’ll have to nuke the site from orbit. It’s the only way to be sure.
Tacking those kind of issues often time means running some code at the time the exception occurs. To facilitate that I added Exception Handlers to my ReportWindow framework. The first case that required their usage goes something like this:

- An old version of the ClickToFlash Safari plugin is installed on your computer 
- This old version of ClickToFlash plugin contains on old version of the Sparkle updater
- When Sparkle detects there is an update it tries to show a window to the user which tells them about the changes and asks for permission to install
- This window contains a WebView, which loads the old ClickToFlash plugin which contains an old Sparkle framework
- The old Sparkle framework over-writes the newer one you included in your application
- All this happens less than a second, long before the window is drawn on the screen
= By the time your user clicks the ‘Upgrade Now’ button the outlet it was attached to is long gone, having been added sometime between the old and new verions of Sparkle

As you might imagine, it took some time to work this all out and devise and test a solution, thanks to the help of a very patient and responsive user as well as the developers of ClickToFlash, I was able to wrap the diagnostic process (a particular Exception signature is detected) and remediation: prompt the user for permission to remove the old ClickToFlash plugin and restart the app, into a ExceptionRecovery object.

## GIVING BACK

Now, I noted at the beginning of the article that iStumbler used to be Open Source. I’ve always believed in open source software development and kept it that way for more than a decade, but eventually I was curious to see if iStumbler could support me and my family as an indy product. I’ve tried this before on a more limited scale but this time was pretty much a “go for broke” attempt.

Well, I ended up broke. Possibly because I spent to much time fixing bug and not enough marketing and developing new features. But, now that I’m gainfully employed again and feeling generous, here’s the source of my ReportWindow framework so your app doesn’t suffer the same fate:

[Report Window](https://github.com/iStumblerLabs/ReportWindow)