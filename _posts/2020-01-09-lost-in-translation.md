---
layout: post
title:  "Lost In Translation"
date:   2020-01-09 09:31:56 +0300
img: dict.jpg
tags: communication code
credit: Waldemar Brandt

---

> It's Not What You Say, It's What People Hear

Frank Luntz writes in his book [Words That Work](https://www.amazon.com/Words-That-Work-What-People/dp/1401309291) about the necessity to understand your listener and speak their language in order to be understood. 

I believe that also the inverse is true: a good communicator lets the other person speak the language the other person speaks and bears the burden of translating.

When designing API's we are telling a story of what can be done using our code. And oftentimes the story we are telling is the story of our internal architecture. `delete_subscription` and `unsubscribe` can both mean the same but are telling different stories: Deleting a subscriptions reveals the internals of the app whereas unsubscribing is what the person using the method actually wanted to accomplish.

Another great example is Git. For a long time `git checkout` was used for different purposes. Switching to an existing branch or restoring a previous version were both done using the same base command. Understanding the subtle differences and use cases involved understanding how Git works internally and that the two use cases are basically the same. For newcomers trying to use Git, this is very confusing. 

Recently Git [introduced](https://public-inbox.org/git/xmqqy2zszuz7.fsf@gitster-ct.c.googlers.com/) two new commands: `git switch` and `git restore`. Both are just aliases but their meaning is much more clear now. 

> Two new commands "git switch" and "git restore" are introduced to
   split "checking out a branch to work on advancing its history" and
   "checking out paths out of the index and/or a tree-ish to work on
   advancing the current history" out of the single "git checkout"
   command.

Git used to force its users to speak it's internal language. Today, after about 15 years of development, this is one of the most basic and used tools in our developer's tool boxes and everyone pretty much accepted the somewhat weird language. But even an accomplished and well used tool can become better, more newcomer friendly and usable. 

Kudos Git!