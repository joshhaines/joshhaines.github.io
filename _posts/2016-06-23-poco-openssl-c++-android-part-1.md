---
layout: post
title: POCO and OpenSSL Using C++ on Android - Part 1
permalink: poco-openssl-android-part-1
comments: true
---

Recently I've had an interest in using C++ to share code between iOS and Android, and have used a project called [Djinni](https://github.com/dropbox/djinni) (created by the devs over at Dropbox) to do the behind the scenes work that would be a pain to do manually. Definitely check out Djinni if you are at all curious in pursuing this further.

I've successfully been able to use Djinni to compile simple C++ code on both iOS and Android, and it is great to be able to share a lot of business logic between the two platforms. However, one thing I've really wanted, is to use a networking library written in C++ on both iOS and Android. This would save a lot of time to have the networking logic written out once, and then just call some C++ methods from Swift/Java. One place for the code to sit, and if something breaks, then it should only need to be fixed once.

That all sounds good, but OpenSSL is a real pain to get working on Android. iOS is fairly easy compared to Android. OpenSSL has a wiki that shows how to build for Android, but it doesn't say how to compile for all Architectures. And a guy like me who is not a library engineer, and doesn't claim to be an expert in C++, does not have any inkling on how to compile for all Android architectures. I've definitely learned a lot through this whole process, but I still do not claim to know enough. I hope that these posts will serve as some much needed documentation on the process. The web has either very old documentation, or no documentation at all on many of these topics.

I plan on this being a multi-part series of articles explaining the process. In this first article I'll explain how to build OpenSSL for Android.

----

## Compiling OpenSSL for Android

Let's get this part out of the way. OpenSSL is an old and bloated library, and I really wish networking libraries would move on to something more slimmed down. Google has recently moved on to BoringSSL on Android, but POCO specifically uses OpenSSL. So I'm going to walk you through the steps of building OpenSSL for Android.

1. Make sure you have the [Android NDK](https://developer.android.com/ndk/downloads/index.html) setup on your local machine, and have set up the [Standalone Toolchain](https://developer.android.com/ndk/guides/standalone_toolchain.html). I'm not going to detail how to do this, but a good starting place is [here](https://gist.github.com/Tydus/11109634).
2. Download the latest version of [OpenSSL](https://www.openssl.org/source/) (I'm using 1.0.2h).
3. Build OpenSSL for all Android architectures:
  * OpenSSL has a [Wiki](https://wiki.openssl.org/index.php/Android) on how to build for Android. If you know what you are doing, then this might be the best place to do this step. If so, skip the next section.
  * If you don't know what you are doing like me, then download a script that will do this step for you. I'm using the script found [here](https://github.com/stdchpie/android-openssl). Follow the steps in the next section.

#### Build OpenSSL for All Android Architectures

If you already know how to do this, and you don't need to use the script found [here](https://github.com/stdchpie/android-openssl), then skip this section.

1. Clone the GitHub project mentioned in the link above ([here it is again](https://github.com/stdchpie/android-openssl) for good measure).
2. Unzip OpenSSL into a folder named `openssl`. Your folder structure should look something like this:
{% highlight bash lineanchors %}
openssl$ ls
openssl-1.0.2h/
{% endhighlight %}
<ol start="3">
<li markdown="1">
Put the `build-all-arch.sh` and `setenv-android-mod.sh` into the `openssl` folder created in the last step.
</li>
<li markdown="1">You'll need to modify the `build-all-arch.sh` script to build for your OpenSSL version. Go to line 56, and you'll see the following:
</li>
</ol>

{% include code-offset.html offset="55" %}
{% highlight bash lineanchors hl_lines="1" %}
cd openssl-1.0.1j

xCFLAGS="-DSHARED_EXTENSION=.so -fPIC -DOPENSSL_PIC -DDSO_DLFCN -DHAVE_DLFCN_H -mandroid -I$ANDROID_DEV/include -B$ANDROID_DEV/$xLIB -O3 -fomit-frame-pointer -Wall"

perl -pi -e 's/install: all install_docs install_sw/install: install_docs install_sw/g' Makefile.org{% endhighlight %}

<ol start="5">
<li markdown="1">
Change this to be your OpenSSL version. Mine looks like this:
</li>
</ol>

{% include code-offset.html offset="55" %}
{% highlight bash lineanchors hl_lines="1" %}
cd openssl-1.0.2h

xCFLAGS="-DSHARED_EXTENSION=.so -fPIC -DOPENSSL_PIC -DDSO_DLFCN -DHAVE_DLFCN_H -mandroid -I$ANDROID_DEV/include -B$ANDROID_DEV/$xLIB -O3 -fomit-frame-pointer -Wall"

perl -pi -e 's/install: all install_docs install_sw/install: install_docs install_sw/g' Makefile.org{% endhighlight %}

<ol start="6">
<li markdown="1">
Now your folder structure should look like this:
</li>
</ol>

{% highlight bash lineanchors %}
openssl$ ls
build-all-arch.sh*
openssl-1.0.2h/
setenv-android-mod.sh*
{% endhighlight %}

<ol start="7">
<li markdown="1">
Now you are ready to build! Just run:
</li>
</ol>

{% highlight bash lineanchors %}
openssl$ ./build-all-arch.sh
{% endhighlight %}

When that's done building, you should see a folder called `prebuilt` within the `openssl` folder. This will contain all of the shared libraries that will be necessary to build POCO.

Congratulations! You just got through the part that was definitely the biggest pain for me. I spent a lot of time trying to build OpenSSL through their Wiki, Gradle, Android makefiles, etc. and finally found that script.

----

In my next post I'll detail how to build POCO. I'll link the article here once it's done. Thanks for reading, and let me know if you have any questions in the comments below!
