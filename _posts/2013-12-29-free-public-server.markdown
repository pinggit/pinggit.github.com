---
layout: post
title: "free public server"
published: true
created:  2013 Dec 29 02:27:45 PM
tags: [web, server, ssh]
categories: [tech]

---

for long time I had an idea that a lot of things/hacks can be done only if we
have a public SSH server available. when I think about this a lot of options can be listed:

1. corporation provided, with an public IP
1. a running server at home, with public IP assigned from ISP
1. some old servers that your friends ever provided for various purposes
1. some "free" unknown servers published from some websites
1. non-free server you rent from a vendor

NO1&2 are usually handy when yo need them. but sometime hard to get.  in terms
of option2, it's good to know that verizon Fios provide a fixed IP bound to
your home router/modem, so simply define some policy rules (NAT/PAT stuff) in
the router will make your home server available from public Internet, which was
what I did.

NO3&4 are useful if you are lucky. those type of resources are normally just
available temporarily, one time , and will quickly gone or become not available
over the time. so they are just FYI type of things.

NO5 service could be reliable. But overall it's not a "must have" to have these
service but just a plus, so few people are interested to pay for the service,
unless you have some serious requirements like setup a website or sth, or ----
unless it's free AND cool.

I was just told of (and tested) [*amazon aws service*][], it looks really nice.
basically you can create and run some virtual instance(ubuntu, redhat,
suse,windows,etc) in the cloud and get the full control, and good thing is your
servers are assigned with a public IP. 

and it is [free][] , for [a year][ec2]. enough to decide proceed or terminate?


[*amazon aws service*]: http://aws.amazon.com
[free]:                 https://aws.amazon.com/cn/free/
[ec2]:                  https://aws.amazon.com/cn/ec2/


