---
layout: post
title: JHCollapsingNavbar
permalink: jhcollapsingnavbar
comments: true
---

![Navbar](/assets/navbar.gif){: .center-image }

I'm happy to announce my first contribution to the iOS development community on Github: JHCollapsingNavbar! I've been in the process of creating my first app, which is about 75% complete, and one of the features I made was a collapsing view at the top when the user scrolls. This is *very* similar to what the Facebook and Gmail apps do, which were my inspiration for this. I'll talk a little about the background of how I wrestled with the challenge of creating this, but if you'd like to use the code for your own project then go ahead and head on over to [JHCollapsingNavbar](https://github.com/personary/JHCollapsingNavbar).

----

## The Challenge

I wanted a collapsing view like what is seen in the Facebook app. There are other projects out there that do something similar, but I figured - how hard can it be? Well I ran in to some challenges along the way. I'll try to recall most of them here.

### First Approach

I first tried using a wide combination of UIEdgeInsets, "y" values of the views, scroll deltas, and at one point I was even using "delta of delta" (I was getting the scroll direction with this). I just could *not* get everything to work correctly with each other. I'd get one direction working, but then the other direction would break. I'd get the second direction working, but then snapping would break. I'd get snapping working, and then the view would glitch to a random location.

Getting that smooth 1-to-1 movement like you see in Facebook and Gmail was also a challenge. Certain approaches would move the navbar, but there'd be lag, which caused it too not look at all comparable to what is seen in Facebook.

Looking at my old code, I have so much commented out code, so I just wrote "lol" at the top because I laugh whenever I look at it. I had so much random code that it was getting to be too much to handle for one feature. So I decided to start another project with a different approach.

### Using Constraints

*This* is the approach that I was looking for. I set a top constraint on my custom navbar view. My table view was constrained to my navbar. So whenever my navbar moves, my table view should resize. I hooked up my constraint to my view controller as a property, then got to work.

One of the things I noticed that I needed was a second pan gesture recognizer added to my table view. The pan gesture recognizer that is included with the table view is read-only, and I needed to add my own logic. There's a method in the UIGestureRecognizerDelegate, `(BOOL)gestureRecognizer: shouldRecognizeSimultaneouslyWithGestureRecognizer:`, that allows a second gesture recognizer to be evaluated simultaneously when returning YES. Now that I had my own pan gesture recognizer I was able to add my logic.

### Animations and Pan Gesture States

At first I decided to try out UIView animations. I could get them to work, but the smooth transition I wanted didn't seem to work correctly - more on that in a little. I then used Facebook Pop for my animations. Facebook Pop was very easy to understand and use on my constraints.

I also wanted to react to the changes in the pan gesture state, so I found out about KVO and ReactiveCocoa. I decided to give ReactiveCocoa a shot, and was able to easily listen to a change in the pan gesture state. This allowed me to snap the navbar when the user stopped scrolling, and I used a Pop animation for this snapping logic.

*However*, now that I wanted to publish this on Github, I wanted to remove dependance on third party libraries if possible, so this prompted me to try to figure out how to match my Pop animations with UIView animations. I noticed that when I did this that my tableView would *not* transition smoothly when my navbar would snap. What I learned was that not only did the navbar need a call to `layoutIfNeeded` on the view, but the table view also needed this call. That triggered something in my mind where I think I now understand UIView animations a lot better now.

Removing dependance on ReactiveCocoa was a small challenge. I effectively just checked for UIGestureRecognizerStateEnded in my gesture recognizer selector. For some reason that idea never entered my mind before, and I just want to slap my forehead.

So now after removing those two library dependancies I had clean code that anyone could use without downloading Facebook Pop and ReactiveCocoa.

----

## Summary

I'm really excited to get some feedback on this project, and anyone looking to contribute, please do. I know this could be expanded to include other views that inherit from UIScrollView. I'd love to hear any ideas or questions in the comments below. Thanks for reading!
