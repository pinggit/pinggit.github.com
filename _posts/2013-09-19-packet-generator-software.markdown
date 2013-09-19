---
layout: post
title: "packet generator software"
published: true
created:  2013 Sep 19 11:42:16 AM
tags: [tool]
categories: [tech]

---

# packet generators
here are some of my favorite software that can be used as packet generator.

all similar tools: http://wiki.wireshark.org/Tools

the following tools are tested and good on ubuntu 910

# packETH    :

    load a pcap file, 
    click on a packet to load it into builder, 
    go to builder to edit the packet
    go to gen-b to edit the sending behavior
    go to gen-s to edit the sending sequence
    select o/g i/f
    send it

# sendip

    #sendip -v -d r64 -p ipv4 -iv 4 -ih 5 -il 128 -is 10.0.0.1 -id 30.0.0.1 -p tcp -ts 1379 -td 23 -tt 8 30.0.0.1
        -v：运行时输出详细运行信息，如不指定，运行时不输出信息
        -d r64：用64 字节的随机数值填充IP 包中的数据段
        -p ipv4：指定协议类型为IP 协议（IP 协议有自己的相应参数，以i 开头）
        -iv 4：协议版本为4，即IPV4
        -ih 5：指定IP 头的长度为5×4＝20 字节
        -il 128：指定IP 包的总长度为128 字节
        -is 10.0.0.1：指定IP 包的源地址
        -id 30.0.0.1：指定IP 包的目的地址
        -p tcp：指定IP 包中封装的包的协议类型（TCP 协议有自己的相应参数，以t 开头）
        -ts 1379：指定TCP 包的源端口1379
        -td 23：指定TCP 包的目的端口为23
        -tt 8：指定TCP 包的偏移量即TCP 头的长度，没有TCP 选项时为5，即20 字节，有TCP 选项时需要增加。
        30.0.0.1：指定发包的目的主机

       #发送一个记录三个IP 的数据包 
       sendip –d r64 –p ipv4 –iv 4 –ih 10 –il 128 –is 10.0.0.1 –id 30.0.0.1 –iorr 10:10.0.0.234:20.0.0.234:30.0.0.234 –ioeol –p tcp –ts 1379 –td 23 –tt 8 30.0.0.1
        -ih 10 表示IP 头的长度为10×4 为40 个字节，去除标准的20 个字节长度，为IP
        选项预留为20 个字节
        -iorr 10:10.0.0.234:20.0.0.234:30.0.0.234 中第一个10 表示用16 进制表示的指针的
        位置，后面为用冒号分隔的三个用点分十进制表示的IP 地址
        -ioeol 表示用00 结束IP 选项，并用随机数填充后面未用的IP 头位置    

    在设定TCP 选项时，同样要考虑到TCP 头的长度要包括TCP 选项的长度。
    TCP 选项数据包的格式大致如下：
    Kind=3 Len=3 数据：移位数
    TCP 选项号TCP 选项长度TCP 选项数据占一个字节，总长度为三个字节
    具体命令行格式可参照如下格式：
    ＃sendip –d r64 –p ipv4 –iv 4 –ih 10 –il 128 –is 10.0.0.1 –id 30.0.0.1 –iorr 10:10.0.0.234:20.0.0.234:30.0.0.234
    –ioeol –p tcp –ts 1379 –td 23 –tt 8 –tfa 0 –tfs 1 –towscale 0 –toeol 30.0.0.1
    -towscale 0 ：指设置TCP 选项3，长度为自动3，TCP 选项的值即移位数为0
    -toeol ：表示TCP 选项结束，后面用随机数填满TCP 头
    因为用SENDIP 设定TCP 选项时，不能设定长度，所以，如果要设定长度不正确的包，
    还要借助其他工具

# packit

    looks no VLAN support?

    #following are all tested:

    #this works great
    sudo packit -s 172.25.83.73 -d fios1 -D 1-1024 -F S -v
    sudo packit -s 172.25.83.73 -d 172.25.84.204 -D 1-1024 -F S -v -T 0 
    #send 100 icmp pkt with ttl 0

    sudo packit -t icmp -s 172.25.84.207 -d 172.25.84.204 -c 100 -T 0

    #send 1000 packets(-c), with 100 (-b) each burst (default IBG is 1s, -w 1) 
    #Random source ether addr(-eR), dest ether (-E) is 00:90:1a:..
    #Random source/dest IP (-sR -dR), verbose display (-v)
    sudo packit -i eth3 -E 00:90:1a:a1:7e:59 -eR -sR -dR -v -c 1000 -b 100

# mz

    raw mode:
        mz eth0 "00:ab:cd:ef:00 00:00:00:00:00:01 08:00 ca:fe:ba:be"

    The spaces within the byte string are optional and separate the Ethernet  fields  
    (destination and  source  address,  type field, and a short payload). 
    The only additional options supported are -a, -b, -c, and -p. The frame length MUST be greater or equal 15 bytes.

    #send 100pps(-d 10m) STP bpdu(-t bpdu) packets , indefinitly (-c 0), through eth1 i/f
    ping@ubuntu1004desktop:~$ sudo mz eth1 -c 0 -d 10m -t bpdu

        13:06:42.789911 f0:de:f1:17:cd:d6 > 01:00:0c:cc:cc:cd, ethertype 802.1Q (0x8100), length 68: LLC, dsap SNAP (0xaa) Individual, ssap SNAP (0xaa) Command, ctrl 0x03: oui Cisco (0x00000c), pid PVST (0x010b): STP 802.1d, Config, Flags [none], bridge-id 0000.f0:de:f1:17:cd:d6.0000, length 42
        message-age 0.00s, max-age 20.00s, hello-time 2.00s, forwarding-delay 15.00s
        root-id 0000.f0:de:f1:17:cd:d6, root-pathcost 0

# bitswist:
        load a pcap file and send it

# iperf

# jperf

GUI of iperf


# tcpreplay

http://tcpreplay.synfin.net/wiki/tcpreplay

                                   tcpreplay

Overview

   tcpreplay has evolved quite a bit over the years. In the 1.x days, it
   merely read packets and sent then back on the wire. In 2.x, tcpreplay was
   enhanced significantly to add various rewriting functionality but at the
   cost of complexity, performance and bloat. Now in 3.x, tcpreplay has
   returned to its roots to be a lean packet sending machine and the editing
   functions have moved to [93]tcprewrite and a powerful tcpreplay-edit which
   combines the two.

Basic Usage

   To replay a given pcap as it was captured all you need to do is specify
   the pcap file and the interface to send the traffic out interface 'eth0':

     # tcpreplay --intf1=eth0 sample.pcap

Replaying at different speeds

   You can also replay the traffic at different speeds then it was originally
   captured. Some examples:

   To replay traffic as quickly as possible:

     # tcpreplay --topspeed --intf1=eth0 sample.pcap

   To replay traffic at a rate of 10Mbps:

     # tcpreplay --mbps=10.0 --intf1=eth0 sample.pcap

   To replay traffic 7.3 times as fast as it was captured:

     # tcpreplay --multiplier=7.3 --intf1=eth0 sample.pcap

   To replay traffic at half-speed:

     # tcpreplay --multiplier=0.5 --intf1=eth0 sample.pcap

   To replay at 25 packets per second:

     # tcpreplay --pps=25 --intf1=eth0 sample.pcap

   To replay packets, one at a time while decoding it (useful for debugging
   purposes):

     # tcpreplay --oneatatime --verbose --intf1=eth0 sample.pcap

Replaying files multiple times

   Using the loop flag you can specify that a pcap file will be sent two or
   more times:

   To replay the sample.pcap file 10 times:

     # tcpreplay --loop=10 --intf1=eth0 sample.pcap

   To replay the sample.pcap forever or until CTRL-C is pressed:

     # tcpreplay --loop=0 --intf1=eth0 sample.pcap

   If the pcap file(s) you are looping are small enough to fit in available
   RAM, consider using the --enable-file-cache option. This option caches
   each packet in RAM so that subsequent reads don't have to hit the slower
   disk. It does have a slight performance hit for the first iteration of the
   loop since it has to call malloc() for each packet, but after that it
   seems to improve performance by around 5-10%. Of course if you don't have
   enough free RAM, then this will cause your system to swap which will
   dramatically decrease performance.

   Another useful option is --quiet. This suppresses printing out to the
   screen each time tcpreplay starts a new iteration. This can have a
   dramatic performance boost for systems with slower consoles.

Advanced Usage

  Splitting Traffic Between Two Interfaces

   By utilizing [94]tcpprep cache files, tcpreplay can split traffic between
   two interfaces. This allows tcpreplay to send traffic through a device and
   emulate both client and server sides of the connection, thereby
   maintaining state. Using a tcpprep cache file to split traffic between two
   interfaces (eth0 & eth1) with tcpreplay is simple:

     # tcpreplay --cachefile=sample.prep --intf1=eth0 --intf2=eth1
     sample.pcap

   Alternatively, if you have already split your traffic into two files- as
   in the case of capturing traffic using a network tap, then tcpreplay can
   read two files at the same time, one for each interface:

     # tcpreplay --dualfile --intf1=eth0 --intf2=eth1 side-a.pcap side-b.pcap

  Viewing Packets as They are Sent

   The --verbose flag turns on basic tcpdump decoding of packets. If you
   would like to alter the way tcpreplay invokes tcpdump to decode packets,
   then you can use the --decode flag. Note: Use of the --verbose flag is not
   recommended when performance is important. Please see the tcpdump(1) man
   page for options to pass to the --decode flag.

  Editing Packets

   tcpreplay now comes in two flavors: tcpreplay and tcpreplay-edit. The only
   difference between the two is that tcpreplay-edit embeds all the packet
   editing functionality found in [95]tcprewrite. This is nice because you
   can edit and send all in one step, but it does have a performance hit.

Choosing a Timing Method

   tcpreplay as of v3.3.0 now supports multiple methods for creating delays
   between two packets.

   First a refresher:

     * There are 1,000 milliseconds (msec) in 1 second
     * There are 1,000,000 microseconds (usec) in 1 second
     * There are 1,000,000,000 nanoseconds (nsec) in 1 second

   And a little math:

   Let's say you want to send 125,000 packets/sec (pps). That means you need
   to send a packet on average every 8usec. That's doable on most hardware
   assuming you can find a timing method with 1usec accuracy. The problem
   gets a lot more difficult when you want to send at 130,000 pps- now you
   need 7.7usec delay, requiring .1usec accuracy! That's a 10x increase in
   accuracy for a small change in performance. Most timing methods on general
   purpose hardware/software can't do that.

   So what are the expected accuracies of each timing method?

     * nanosleep() - Theoretically 1nsec accuracy, but is probably closer to
       1usec. Can be off by up to +/- 10msec depending on the operating
       system.
     * gettimeofday() - 1usec accuracy at best
     * OS X's AbsoluteTime() - 1nsec accuracy
     * select() - Theoretically 1usec accuracy, but tends to be off by +/-
       10msec
     * IO Port 80 - 1usec accuracy, but can cause system crashes with certain
       versions of hardware/OS's
     * Intel/AMD/SPARC [96] RDTSC - Theoretically better then 1usec accurate,
       but many recent multi-core Intel CPU's are horribly inaccurate and
       unusable
     * [97] Intel HPET - A 10Mhz timer giving .1usec accuracy

   As you see above, only AbsoluteTime and the HPET provide the necessary
   resolution to hit our 130,000pps mark. Hence, if you're using one of the
   other methods, I'll use weighted averages or rounding to provide better
   accuracy. What that means is, when each packet is being sent at a constant
   rate (packets/sec) I'll sleep 8usec 7 times, and then 7usec 3 times to
   average out to the necessary 7.7usec. If you're using a variable timing
   method (Mbps or multiplier) then I'll round to the nearest 1usec (8usec in
   this case of 7.7usec)- the hope is that over many packets, it will average
   out correctly.

  AbsoluteTime

   So what does this all mean? Well, if you're running OS X, then using
   --timer=abstime is the clear winner. After that it gets more complicated.
   AbsoluteTime is currently the only timing method which doesn't need
   weighted averages or rounding.

  HPET/gettimeofday

   First, tcpreplay currently doesn't have native support for the Intel HPET.
   The good news is that some operating systems (like recent Linux kernels)
   use the HPET for calls to gettimeofday(). So while you loose some accuracy
   (gettimeofday() is accurate to 1usec no matter what the underlying
   implementation looks like), it's probably the best option for non-OS X
   users. If your gettimeofday() isn't backed by the HPET, you can still use
   it, just realize it might be a bit unreliable. Even if your gettimeofday()
   uses the HPET, you still only get 1usec accuracy, so part about using
   weighted averages and rounding still applies. Specify --timer=gtod to use
   gettimeofday()

  nanosleep

   Some implimentations of nanosleep() are good, others are horrible- it even
   may depend on how long you're sleeping for since the implementation might
   switch between going to sleep (bad) or using a tight loop (good).
   Generally speaking it's worth trying: --timer=nano

  RDTSC

   Using the RDTSC via --timer=rdtsc. This tends to work great on some
   hardware and is completely worthless for others. I've got an Intel P4
   3.2Ghz box which it works great on, but my Core2Duo MacBook Pro is really
   bad. If you don't specify a --rdtsc-clicks value, tcpreplay will introduce
   a short delay on startup in order to calculate this value. If your
   hardware has a properly working RDTSC it's usually the speed of the
   processor (expressed in Mhz, so a 3.2Ghz CPU == --rdtsc-clicks=3200) or a
   fraction thereof.

  IO Port 80

   I don't have much experience with this, so give it a try and let me know
   what you find: --timer=ioport

  select

   This is crap for 99% of the situations out there. Hence you probably don't
   want to specify --timer=select

  Accelerating Time

   Regardless of which timing method you use, you can try specifying
   --sleep-accel to reduce the amount of time to sleep in usec. I've found
   this is useful for providing a "fudge factor" in some cases.

Tuning for High-Performance

  Choosing a Packet Interval Method

   The first recommendation is simple, use: --topspeed. This will always be
   the fastest method to send packets. If however you need some level of
   control, using --pps to specify packets/second is recommended. Using
   --pps-multi will cause multiple packets to be sent between each sleep
   interval, thus providing higher throughput potential then just --pps
   alone, but at the cost of traffic being more "spikey" then flat. Higher
   --pps-multi values improve performance and make the traffic more "spikey".

   Using --mbps or --multiplier for high performance situations is not
   recommended as the overhead for calculating packet intervals tends to
   limit real world throughput.

  Tuning your Operating System/Hardware

   Regardless of the size of physical memory, UNIX kernels will only allocate
   a static amount for network buffers. This includes packets sent via the
   "raw" interface, like with tcpreplay. Most kernels will allow you to tweak
   the size of these buffers, drastically increasing performance and
   accuracy.

   NOTE: The following information is provided based upon my own experiences
   or the reported experiences of others. Depending on your hardware and
   specific hardware, it may or may not work for you. It may even make your
   system horribly unstable, corrupt your harddrive, or worse.

   NOTE: Different operating systems, network card drivers, and even hardware
   can have an effect on the accuracy of packet timestamps that tcpdump or
   other capture utilities generate. And as you know: garbage in, garbage
   out.

   NOTE: If you have information on tuning the kernel of an operating system
   not listed here, please send it to me so I can include it.

  General Tips

    1. Use a good network card. This is probably the most important buying
       decision you can make. I recommend Intel e1000 series cards. El-cheapo
       cards like Realtek are known to give really crappy performance.
    2. Tune your OS. See below for recommendations.
    3. Faster is better. If you want really high-performance, make sure your
       disk I/O, CPU and the like is up to the task.
    4. For more details, check out the [98]FAQ
    5. If you're looping file(s), make sure you have enough free RAM for the
       pcap file(s) and use --enable-file-cache
    6. Use --quiet
    7. Use --topspeed or --pps and a high value for --pps-multi
    8. Use tcprewrite to pre-process all the packet editing instead of using
       tcpreplay-edit
    9. Virtualization technologies like VMWare and Xen may cause a lot of
       problems with packet timings. YMMV.

  Linux

   The following is known to apply to the 2.4.x and 2.6.x series of kernels.
   By default Linux's tcpreplay performance isn't all that stellar. However,
   with a simple tweak, relatively decent performance can be had on the right
   hardware. By default, Linux specifies a 64K buffer for sending packets.
   Increasing this buffer to about half a megabyte does a good job:

    echo 524287 >/proc/sys/net/core/wmem_default
    echo 524287 >/proc/sys/net/core/wmem_max
    echo 524287 >/proc/sys/net/core/rmem_max
    echo 524287 >/proc/sys/net/core/rmem_default

   On one system, we've seen a jump from 23.02 megabits/sec (5560
   packets/sec) to 220.30 megabits/sec (53212 packets/sec) which is nearly a
   10x increase in performance. Depending on your system and capture file,
   different numbers may provide different results.

  BSD

   BSD systems typically allow you to specify the size of network buffers
   with the NMBCLUSTERS option in the kernel config file. Experiment with
   different sizes to see which yields the best performance. See the
   options(4) man page for more details.

