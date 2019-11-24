---
layout: post
title:  "It's Rarely The Vacuum - Thoughts on Debugging"
date:   2019-11-21 09:31:56 +0300
img: vacuum.jpg
tags: debugging
credit: Lukas ter Poorten

---

Last week our vacuum cleaner suddenly stopped working. You plug it in, press the on button and it doesn't work. The first thought was: its broken. The next thought was about how we can repare it or where and when should we get a new one. 

But then it hit me - lets look around. The next minute or so I tried to answer a series of questions in order to try to find the real problem.

* Is the small lamp on the extension cord on? It should indicate if the vacuum gets power. No, it was not.
* Are the lights on the router blinking? It should tell me if there is electricity through out the room. No, they wern't.
* Did a fuse pop? Let's check the fuse box. No, all were up.
* Lets go to the stairs where the power meters for the apartments are located. Here we go, all meters were standing still. 

**The problem was power outage in the neighborhood.** Sure thing, a few minutes later everything came back to normal and the vacuum started working again.

I find that the same approach to debugging can make us find bugs much faster.

It is certainly possible that there is a bug in my programming language (aka the vacuum is broken), but it is more likely that there is a bug in my framework. Even more likely is it a bug in a third party library I am using.

But most likely is it a bug in the code I just wrote, **even if I don't see it now**.

So in order to pinpoint the problem quickly, here are the steps I've tried to follow when debugging over the last couple of years. 

#### 1. Hardcode return values

Start as close as possible to the place where you are experiencing the bug. If you're building a web page, hard code the value in the webpage itself. If you see it, hard code it in the code that provides the data for your page, e.g. your JavaScript component, controller, etc.

#### 2. Move out slowly

Slowly zoom out and move further away from the place you see the bug. 


#### 3. Keep repeating step 1 and 2 until you find the issue

It's easier said than done, but at some point while doing step 2 (repeating step 1) you will find yourself between two states - a working one and the next one that doesn't work. Congratutalations, you just found where the problem actually lies.

#### 4. Fix the issue

Now that you know where exactly the issue lies, you can begin the real work. It can be hard and you may have to spend a lot of time finding a solution, but at least you can be (almost) sure that you are not wasting your time trying to fix the vacuum cleaner.



Remember, it's rarely the vacuum!

