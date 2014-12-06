---
layout: post
title: "2014-0923-0732 l3 incomplete"
published: true
created:  2014 Sep 24 01:11:44 PM
tags: [junos, att, l3 incomplete]
categories: [tech]

---


    Physical interface: ge-3/1/0, Enabled, Physical link is Up
        Errors: 32, Drops: 0, Framing errors: 0, Runts: 0, Policed discards: 0, L3 incompletes: 32, L2 channel errors: 0, L2 mismatch timeouts: 0, FIFO errors: 0, Resource errors: 0
    Physical interface: ge-3/2/0, Enabled, Physical link is Up
        Errors: 41, Drops: 0, Framing errors: 0, Runts: 0, Policed discards: 0, L3 incompletes: 41, L2 channel errors: 0, L2 mismatch timeouts: 0, FIFO errors: 0, Resource errors: 0
    Physical interface: ge-3/3/0, Enabled, Physical link is Up
        Errors: 35, Drops: 0, Framing errors: 0, Runts: 0, Policed discards: 0, L3 incompletes: 35, L2 channel errors: 0, L2 mismatch timeouts: 0, FIFO errors: 0, Resource errors: 0
    Physical interface: pfe-4/0/0, Enabled, Physical link is Up
    --
    Physical interface: ge-4/1/0, Enabled, Physical link is Up
        Errors: 936427, Drops: 0, Framing errors: 0, Runts: 0, Policed discards: 0, L3 incompletes: 936427, L2 channel errors: 0, L2 mismatch timeouts: 0, FIFO errors: 0, Resource errors: 0
    Physical interface: ge-4/2/0, Enabled, Physical link is Up
        Errors: 934126, Drops: 0, Framing errors: 0, Runts: 0, Policed discards: 0, L3 incompletes: 934126, L2 channel errors: 0, L2 mismatch timeouts: 0, FIFO errors: 0, Resource errors: 0
    Physical interface: ge-4/3/0, Enabled, Physical link is Up
        Errors: 658667, Drops: 0, Framing errors: 0, Runts: 0, Policed discards: 0, L3 incompletes: 658667, L2 channel errors: 0, L2 mismatch timeouts: 0, FIFO errors: 0, Resource errors: 0
    Physical interface: pc-5/0/0, Enabled, Physical link is Up

    root@cgcil401me3> show pfe statistics traffic
    Packet Forwarding Engine Input IPv4 Header Checksum Error and Output MTU Error statistics:
        Input Checksum             :              3892718
        Output MTU                 :                26397

# links/resources

[l3-incomplete.potx](https://matrix.juniper.net/docs/DOC-114161)
