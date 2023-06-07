---
layout: post
title:  "Super easy way to make Selenium Webdriver invisible to detectors"
date:   2023-06-07 10:12:11 +0100
categories: selenium hacking
---

Do you want to run automate your activities on a webpage with a browser controlled by Selenium Webdriver, but it's being detected ??
You can find on the Internet some solutions. There is one for Google Chrome with the use of some scripts - it works, but only in the headless mode (don't know if it's still working).
I once looked at how to do it. I checked how the browser is detected. What I have found was that the basic detection is done by the webpage, by checking in JavaScript if the property `navigator.webdriver` is `true`. You can't change this using the Selenium interface or by injecting your own JavaScript.  I have tried that. 

What I came up with was pretty simple. I was thinking: I own my computer, I own my browser, so I can use my "own" browser. You can grab the source code of the browser, modify it as you wish, and use it. So why not do it? All you have to do is to hide the use of Selenium by making the browser always say `false` when someone is
accessing the `navigator.webdriver` property. 

I haven't tried that with Chrome, but I did that with Firefox, and it worked. You just have to go to the file `/dom/base/Navigator.cpp`, line 2273 (currently as I write this post), to the definition of a function `bool Navigator::Webdriver()`, where you have to remove the whole function body and replace it with a simple `return false;` TADA!! Yes, it's so simple. The hard part is compiling the browser.

You can use the quick way, and compile it as a development version,  but your browser will be slow and will generate lots of logs. It will take some documentation reading and some compiling until you get it right. Eventually, you will succeed, don't worry. It looks big and scary, but it's not.

I'm not going to describe how to do it exactly, as I have done that around 2019 and things have changed a bit. I will try to update this post with a working solution soon. Use GitHub to contact me if you want to share your solution or if you have problems - I'll gladly help. Bye!
