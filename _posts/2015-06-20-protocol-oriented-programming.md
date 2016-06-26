---
layout: post
title: Protocol Oriented Programming in Swift 2.0
permalink: protocol-oriented-programming
comments: true
---

So I'm really curious about this video at WWDC this year. I'm trying to wrap my mind around this concept, which is definitely a challenge. Through my career of programming I've only used Object-Oriented Programming (OOP); so Protocol-Oriented Programming (POP?) sounds like a pretty cool concept. However, POP has some limitations with the current usage of classes in iOS development.

See video [here](https://developer.apple.com/videos/wwdc/2015/?id=408).

----

## Protocols and Structs Instead of Classes

The underlying theme seems to be using protocols and structs where possible instead of classes. That seems all fine-and-dandy until you try conforming to a class protocol to call some delegate methods. Structs can't conform to class protocols, such as NSURLConnectionDelegate. I tried doing this today on an app prototype of mine using the Sqoot API. I had a class for helper methods for accessing Sqoot. I wanted to try out this POP stuff, so I decided I'd try to change around my logic. Well when I changed my class to a struct like so:

{% highlight swift %}
struct SqootHelper: NSObject, NSURLConnectionDataDelegate {}
{% endhighlight %}

Well... I got the following error:

{% highlight swift %}
"Non-class type 'SqootHelper' cannot conform to class protocol 'NSURLConnectionDataDelegate'"
{% endhighlight %}

I think I'm just going to have my view controller conform to the NSURLConnectionDataDelegate, and make a JSONParser struct/protocol combo.

## Benefits worth it?

I understand that POP provides many benefits, but when I can't find a use for it I have a hard time accepting it as part of my workflow. I'm going to try to force myself to refactor my code each time to include POP. So maybe... eventually... It'll start to naturally come to me as a viable option when starting new code.

I do think the benefits are ultimately worth it, and I'm sure Apple will continue to expand on this approach. They are calling Swift 2.0 the first Protocol-Oriented Programming language, which of course it is, but it's also Object-Oriented. I'm curious to see what others can do with this.

What do you think?
