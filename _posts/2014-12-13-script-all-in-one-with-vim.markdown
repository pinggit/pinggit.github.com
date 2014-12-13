---
layout: post
title: "script all in one with vim"
published: true
created:  2014 Dec 13 04:26:12 PM
tags: [script, vim]
categories: [tech]

---

I recently wrote a script, that makes it easy to automate interactions to
remote hosts in shell script...but I'm not going to say anything about
[that](https://github.com/pinggit/crtc) in here...

I found it interesting to put everything in one file. source code, config file
template, even help docs.

people may think it's stupid - considering of "scalability", a better idea is
to program "modularly"... but just because of putting everything in one file
does not necessarily means it's NOT scalable. 

the tool is vim VOom plugin - It seems not a problem to maintain 2M+ lines of
texts (e.g. codes), and still you have a good overview of the whole structure.
plus now you don't need to spend much time to design the "interfaces" between
modules . why breaking things into pieces when they can work just fine in one?

here is how the problems of "one-file" method can be worked-around:

* when the script grows, it's hard to maintain...

  * with a code structure tree showing the whole code structure, it's not a
    problem to get a highlevel overview to the whole file.
  * you can jump back and forth between different points of a work flow
    quickly, without getting lost.

![code](/images/crtc-2.gif "code")

* when you want to write the doc, change the tree from "code tree" to a "doc
  tree"
  * now the document structure will be displayed in the tree, other things like
    the source code will be ignored.
  * you can jump in the doc structure the same way as you do in the source code.

![doc](/images/crtc-3.gif "doc")
