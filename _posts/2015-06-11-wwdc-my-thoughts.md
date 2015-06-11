---
layout: post
title: WWDC 2015 - Happy to be an iOS Developer
permalink: wwdc-2015-my-thoughts
comments: true
---

![WWDC15](/assets/wwdc15.jpg){: .center-image }

I took off Monday and Tuesday of this week to watch the WWDC 2015 keynote, and any of the live sessions I could catch. It's crazy how huge these events are, and seeing the App Store stats just makes me realize how large the iOS ecosystem is. I feel really blessed to be able to do what I love, and to live in a time where mobile development is necessary anywhere you turn. I know this may change over time, but I'm excited to see where technology goes throughout my lifetime. I hope I can make it to WWDC in person one of these years!

I wanted to take a little bit of time to write a little on my thoughts from WWDC 2015.

----

## Swift 2.0

*Definitely* interested in playing around with this. I've done a little coding with Swift over the past year, and it was definitely not as polished as Objective-C. While I'm not expecting it to be at that level yet, I'm really interested to see the improvements like...

### Syntax Updates

The `guard` statement really has me looking forward to playing with it. It reminds me a little of the `check` statement in SAP-ABAP. It will allow you to check a BOOL or equivalent, and if it fails then you can return. It really helps to cut down on many embedded `if` statements.

`defer` sounds cool too. You could call some cleanup code that only gets called right when execution is about to leave the scope. I'd need to play around with it to see its usefulness.

### Error Handling

I'm looking forward to this. I'm used to throwing and catching exceptions in SAP-ABAP quite regularly. I haven't noticed me having to do this much in Objective-C. It will be nice to have this functionality in Swift.

{% highlight objective-c %}
func loadData() throws { }

func test() {
   ￼do {
	￼    try loadData()
   } catch {
	     print(error)
   }
}
{% endhighlight %}

### Open-Source

This was an unnexpected announcement. Apple will be open-sourcing Swift by the end of this year. They will be encouraging contributions from the community, *and* a Linux port will be available. I think this is a great step for Apple to take.

----

## Xcode 7

Xcode has some really great updates too.

### Playgrounds

My excitement for Playgrounds last year died off rather quickly. I played around with some Swift code in a Playground, but that's really all that happened. I can see now that Apple plans to make Playgrounds a way to make documentation and demonstrations. That's a really cool idea. Plus it accepts Markup within comments for formatted text.

### Address Sanitizer

This sounds like a really nice tool to point out weak areas in your code when a crash happens. It's especially useful when you can't pinpoint the issue. It will show the exact code that's to blame, *and* show potential issues. I really want to get my hands on this, but I guess I need some bugs to fix first... Time to create some! (?)

### Interface Builder

Some cool affects have been added to Interface Builder, like the rendering of blurs and transparencies. That certainly makes it easier to make your storyboard look exactly how it will render on the device.

Stack views sound like an interesting way to group views so that they behave consistently together. I'd like to see a demo on this as it sounds interesting, but the terminology doesn't really spark any solid ideas in my mind.

----

## App Slicing

App slicing is a new method that Apple is taking to slim down applications for download on to a user's device. Instead of downloading all assets, the user will only download the assets that are necessary for their device. It's a very nice way to slim down those larger apps that *just* go over the download size limit.

----

## Summary

I didn't mention a few things, like WatchOS 2. I don't have any experience with the Apple Watch, but do hope to eventually branch out to it. I also didn't mention the multi-tasking on an iPad, which I think is *really* cool, but I can never find a use for my iPad in my daily routine. I'd rather have my MacBook Pro and my iPhone. However, I know I'll have to start accounting for it when making an iPad app. It's definitely something I want to look more in to.

I'm really excited to start trekking more into the realm of Swift. I really like the style of the language, and the fact that it's going open-source really has me intrigued. Apple's new developer tools look like a great way to tweak and refine an app, so I'll definitely be giving them a spin. All-in-all I'm really excited to start working with iOS 9.
