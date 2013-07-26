---
layout: post
title: "tcpreplay"
published: true
created:  2013 Apr 03 02:40:17 PM
tags: [tcpreplay]
categories: [tech]
---

when I got a problem that needs a pcap file being replayed,
I was confident about the good-looking [ethpack](http://packeth.sourceforge.net/packeth/Home.html)
and I was trying what I could think of (for the whle morning at least), to make
it replay a captured pcap file that was provided by customer, which, was
believed to be able to "simply reproduce" the issue ..

ethpack worked fine, but only for simple cases, just it couldn't replay EVERY
BIT of file. for some reason CRC/checksum/padding/total length/etc, was
constantly changed unintentionally by itself. after nearly 3 hours I realized,
this is not the right tool, so now there is a need to seek for another tool.

I heard of [tcpreplay](http://tcpreplay.synfin.net/) for a while, but never got
a change to really use it (never needed it). I looked at it, installed, tested
-- it works surprisingly good/stable.

## some cheatsheet (from tcpreplay website)

* To replay a given pcap as it was captured all you need to do is specify
the pcap file and the interface to send the traffic out interface 'eth0':

    tcpreplay --intf1=eth0 sample.pcap

* Replaying at different speeds:
You can also replay the traffic at different speeds then it was originally
captured. Some examples:
To replay traffic as quickly as possible:

    tcpreplay --topspeed --intf1=eth0 sample.pcap

* To replay traffic at a rate of 10Mbps:

    tcpreplay --mbps=10.0 --intf1=eth0 sample.pcap

* To replay traffic 7.3 times as fast as it was captured:

    tcpreplay --multiplier=7.3 --intf1=eth0 sample.pcap

* To replay traffic at half-speed:

    tcpreplay --multiplier=0.5 --intf1=eth0 sample.pcap

* To replay at 25 packets per second:

    tcpreplay --pps=25 --intf1=eth0 sample.pcap

* To replay packets, one at a time while decoding it (useful for debugging
purposes):

    tcpreplay --oneatatime --verbose --intf1=eth0 sample.pcap

* Replaying files multiple times
Using the loop flag you can specify that a pcap file will be sent two or
more times:
To replay the sample.pcap file 10 times:

    tcpreplay --loop=10 --intf1=eth0 sample.pcap

* To replay the sample.pcap forever or until CTRL-C is pressed:

    tcpreplay --loop=0 --intf1=eth0 sample.pcap

* Splitting Traffic Between Two Interfaces
This allows tcpreplay to send traffic through a device and
emulate both client and server sides of the connection, thereby
maintaining state. Using a tcpprep cache file to split traffic between two
interfaces (eth0 & eth1) with tcpreplay is simple:

    tcpreplay --cachefile=sample.prep --intf1=eth0 --intf2=eth1 sample.pcap

* Alternatively, if you have already split your traffic into two files- as
in the case of capturing traffic using a network tap, then tcpreplay can
read two files at the same time, one for each interface:

    tcpreplay --dualfile --intf1=eth0 --intf2=eth1 side-a.pcap side-b.pcap


## case folder

    " ============================================================================
    " Netrw Directory Listing                                        (netrw v144a)
    "   /data/backup/cisco/dailywork/cases/2013-0214-0602/tcp-telnet-sessionHangreport-20130204-1710-53[1].pdf
    "   Sorted by      name
    "   Sort sequence: [\/]$,\<core\%(\.\d\+\)\=\>,\.h$,\.c$,\.cpp$,\~\=\*$,*,\.o$,\.obj$,\.info$,\.swp$,\.bak$,\~$
    "   Hiding:        ^\..*
    "   Quick Help: <F1>:help  -:go up dir  D:delete  R:rename  s:sort-by  x:exec
    " ============================================================================
    ../
    2013-0214-0602/
    | TCP-for-IPv4-Server-results/
    | | dump.pcap*
    | | main.log*
    | | notes.xml*
    | | run-time-info.xml*
    | | statistics.csv*
    | | summary.txt*
    | | summary.xml*
    | | testrun.set*
    | mylabtest/
    | | ack.pcap*
    | | allfromtester-original.pcap*
    | | dump.pcap*
    | | get-synack-back.pcap*
    | | mysync.pcap*
    | | mysync1.pcap*
    | | syn*
    | | syn-ack*
    | | synack-original*
    | | synackdata-original*
    | | temp.pcap*
    | | temp.txt*
    | | testresult1.pcap*
    | | testresult2-replay-all-from-tester.pcap*
    | tcp-telnet-sessionHangreport-20130204-1710-53[1].pdf/
    | | tcp-telnet-sessionHangreport-20130204-1710-53.pdf*
    | FIOS-NG-2-config-13FEB13.txt*
    | FIOS-NG-2-config-set-13FEB13.txt*
    | TCP-for-IPv4-Server-results.zip*
    | VZ Codenomicon Best Practices and Guidelines.pdf*
    | dump.pcap*
    | tcp-telnet-sessionHangreport-20130204-1710-53.pdf*
    | tcp-telnet-sessionHangreport-20130204-1710-53[1].pdf.tar.gz*


