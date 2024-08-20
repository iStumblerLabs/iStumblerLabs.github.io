---
layout: post
title: Updating Objective-C Frameworks for Swift Package Manager
---

# Updating Objective-C Frameworks for Swift Package Manager

## Intro

You have a dusty old Objective-C framework that you want to publish as a [Swift Package Manager](https://developer.apple.com/documentation/xcode/swift-packages) Library.

iStumbler Labs publishes a number of Objective-C frameworks and they all need updating to work with Swift Package Manager:

- [KitBridge](https://github.com/iStumblerLabs/KitBridge) — KitBridge allows you to create views which can be used in iOS, iPadOS, macOS, and tvOS applications.
  - [SparkKit](https://github.com/iStumblerLabs/SparkKit) - Small, Simple and Fast; Line, Pie, Dial, Bar, Ring, Stack and Grid Views for macOS, iOS and tvOS
  - [CardView](https://github.com/iStumblerLabs/CardView) – A Good looking subclasses of NSTextView & UITextView
  - [FourCorners](https://github.com/iStumblerLabs/FourCorners) - Utilities to make working with CoreLocation easier
- [LiveBundle](https://github.com/iStumblerLabs/LiveBundle) — LiveBundle is a category which provides dynamic updating of resources from your web server
- [Soup](https://github.com/iStumblerLabs/Soup) – An object oriented persistence framework from iStumbler Labs modeled on the Apple Newton API
- [IcedHTTP](https://github.com/iStumblerLabs/IcedHTTP) - A very small HTTP Server framework suitable for embedding into iOS or Mac OS Apps

Updating all of these for Swift Package Manager was a bit of a chore but there's an easy to implement process to make it less painless.

## Follow the Project Layout Conventions

Swift Package Manager (SPM) expects a particular source code layout, e.g. 

	Project/
	  Project.xcodeproj  ← Not strictly necessary for a Swift Package, nice to have
	  Package.swift      ← Defines the products, dependencies, and targets for Project
	  Sources            ← Source code for all your projects
	    Project          ← Name of the library target
	      includes       ← Header files go here
	    Tests            ← Test target
	    projectctl       ← Command Line Tool

It's possible to configure different locations for source files and includes, however it's easiest to follow the SPM convention, as this simplifies the package description and makes it easier for other developers to understand the project structure.

## Example Project

We’ll use IcedHTTP as an example, here is the finder layout:

<img src="/images/2024/OSPM-01-project-layout.png" width="512">

And the Xcode project layout:

<img src="/images/2024/OSPM-02-xcode-layout.png" width="512">

First create the expected structure in the Finder: 

<img src="/images/2024/OSPM-03-expected-layout.png" width="512">

Then add Sources to your Xcode project as a Group:

<img src="/images/2024/OSPM-04-add-Sources.png" width="512">

Move all the `.m` files and the `Info.plist` to the Project folder (`Sources/IcedHTTP` in this example), and move all the `.h` files to `Sources/includes` in the Xcode Project Navigator.

You will need to adjust the `Info.plist File` Build Setting for each Target, this is a good time to update your build schemes (in particular, I like to add a Composite Target for building All the targets in the project):

<img src="/images/2024/OSPM-05-build-settings.png" width="512">

At this point check to make sure all your targets build correctly from the Xcode Project

<img src="/images/2024/OSPM-06-xcode-build-check.png" width="512">

Now we can define our Swift Package, create `Package.swift` at the root of the project, next to the Xcode Project

<img src="/images/2024/OSPM-07-add-new-file.png" width="512">

<img src="/images/2024/OSPM-08-create-package-swift.png" width="512">

Content of the `Package.swift` file should look like:

	// swift-tools-version:5.10
	import PackageDescription
	
	let package = Package(
	  name: "IcedHTTP",
	  platforms: [.macOS(.v10_14), .iOS(.v14), .tvOS(.v14)],
	  products: [
	    .library( name: "IcedHTTP", type: .dynamic, targets: ["IcedHTTP"])
	  ],
	  targets: [
	    .target(name: "IcedHTTP")
	  ]
	)

Once that file is saved we can open the Swift Package in Xcode (you don’t have the close the Xcode Project, they can both be open which is handy for cross-checking the Package definition and Xcode builds. Note that the Package Icon replaces the Xcode Project icon in the upper left corner:

<img src="/images/2024/OSPM-09-open-package-swift.png" width="512">

<img src="/images/2024/OSPM-10-browse-package.png" width="512">

Any issues with the Package definition will show up automatically, error messages are generally helpful.

<img src="/images/2024/OSPM-11-pacakge-build-check.png" width="512">

If you get errors like `'Framework/Framework.h' file not found` you will need to wrap imports using the `SWIFT_PACKAGE` compile time `#define`:

	#if SWIFT_PACKAGE
	#import "Framework.h"
	#else
	#import <Framework/Framework.h>
	#endif


Once your package definition is correct, you can see the built product, depending on which run destination you have selected. Choose `Product -> Show Build Folder in Finder`

<img src="/images/2024/OSPM-12-built-products.png" width="512">

Double check your Xcode Project to make sure you can still build using your configured targets.

Commit your changes to the git repo (you have a git repo, right?) and push them to your favorite git hosting service.

When you want to [publish a version of your pacakge](https://developer.apple.com/documentation/xcode/publishing-a-swift-package-with-xcode), tag your repo with a [Sepantic Version String](https://semver.org) and push to a public repo.

