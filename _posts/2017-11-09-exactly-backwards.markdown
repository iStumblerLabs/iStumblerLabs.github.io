---
layout: post
title: Exactly Backwards
tag:
- facebook
- privacy
- social-media
- security
- censorship
---

Facebook is trialing a revenge porn suppression system which threatens user privacy and could be implemented in a way which does not require sharing compromising photos.

[Facebook asks users for nude photos in project to combat revenge porn](https://amp.theguardian.com/technology/2017/nov/07/facebook-revenge-porn-nude-photos)

Reading the article, here are the steps required by the proposed system to prevent publication of a revenge porn image:

*   Take a compromising photo
*   Distribute said photo to 2nd party
*   Develop distrust in 2nd party
*   Send compromising photo to 3rd party
*   3rd party sends compromising photo to FB
*   FB Employeee views comprimising photo
*   Photo is hashed and included in a database
*   Existing instance of the photo are removed
*   Any future posts of the photo are not published

So: to prevent people from seeing your comprimsing photo you need to show it to a bunch of people, who will leave it sitting around for a while, just in case they need to look at tit again. Sound crazy to you?

<figure>![](https://cdn-images-1.medium.com/max/1005/1*eBPqekT8SojGnjeswmL1kg.png)</figure>

### A Better Way

The article discusses the existing solution to the problem of unseeable content on the Internet: [PhotoDNA](https://en.wikipedia.org/wiki/PhotoDNA). While there’s a lot of press-release content about the underlying technology being donated to the [National Center for Missing & Exploited Children](https://en.wikipedia.org/wiki/National_Center_for_Missing_%26_Exploited_Children) there’s no indication that the source code is generally available. Thankfully, there are some related, portable, [open source](http://phash.org) efforts which overlap the feature set of PhotoDNA considerably.

Given that we have a way to generate a perceptual hash of the photo on the users device, there is no need to send the actuall image to anyone. We can implement a sysetem with the following steps.

* Take a compromising photo
* User designates photos & videos they wish to suppress
* Perceptual Hashes are Generated on Device
* Hashs are submitted to a database of suppressed image hashes
* Existing posts matching the hash are hidden and reviewed
* Someone posts an image which matches one of the hashes
* The image is flagged for review based on content policy

There are a few things that I like better about this method but looking at the specific tradeoffs helps to understand the advantages:

#### Tradeoff One: Processor Power vs. Network Bandwidth

Sending the image over the network takes bandwidth and exposes the image to more potential viewers (which is what the system is supposed to be preventing in the first place). Generating perceptual hashes on the device takes processor resources and code, but nothing that my watch couldn’t handle. **Network bandwidth is limited relative to processor power, generating hashes locally is better resource management.**

#### **Tradeoff Two: User Privacy vs. Intellectual Property Protection**

Sending the code to generate the perceptual hash to the user exposes it to potential analysis and reverse engineering. Sending the image to a cloud service exposes the image to potentially multiple parties. **Generating the hash on the device better preserves user privacy, using open source software will keep the blood-thirsty IP lawyers at bay.**

#### **Tradeoff Three: Prior Restraint vs. Content Review**

Now, let’s say I have a photo someone sent that I don’t want published to any social network site. Doesn’t have to be compromising, could just be a bad hair day or maybe me parking my car in two handicapped spots.

**Prior restraint is always expense.** The system we’re talking about is explicitly designed to censor images and flag users who post censorable images, the use of the system to suppress content which some simply doesn’t like can’t be overlooked. **Requiring that each photo be reviewed before submitting isn’t just a privacy problem, it’s too much work.**

There is no point in having a human review the photos unless there’s a hit against the database of suppressed perceptual hashes, once an image has been submitted which appears in the database it can be held for review withouth being published (similar to the existing tag review features, which prevent auto-tagging of your face in image).

#### Is Our Machines Learning?

What confuses me about this whole project is that machine learning has been around for some time, and is becoming more and move avaliable to developers on more and more platforms, and despite that we don’t see better tools for automatically detecting this type of content.

If my phone can find all [images of a brassier](https://www.bustle.com/p/what-is-the-brassiere-folder-on-ios-apple-categorizes-your-nudes-under-this-bizarre-keyword-in-the-photos-app-3193263) in my photo albums, then why can’t Facebook identify that feature of an image, along with the face of an existing users (which it already knows) and flag it for review? Particularly if the recognized user isn’t the one posting the image?

If you liked this article, please, [send nudes](mailto:alf@istumbler.net).