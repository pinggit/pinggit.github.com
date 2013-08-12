---
layout: post
title: "jncie log"
created:  2013 Aug 12 12:49:22 AM
published: false
---

TABLE OF CONTENT

  - - -

[TOC]

  - - -

# JNCIE logs

## pre-IGP

### TIPS: about apply-groups

it looks `apply-groups` doesn't necesarily save time/config work, and causing
inheritance to unintented interfaces. but if preconfig already have it, removing
them and reconfig bring more works.

check with:

    lab@MX80-NGGWR-01# run show interfaces routing logical-system lr2 
    Interface        State Addresses
    ge-1/2/2.12      Up    INET  10.10.12.2
                           ISO   enabled
                           MPLS  enabled
    ge-1/2/1.1000    Up    INET  192.168.100.1
    ge-1/2/1.222     Up    INET  192.168.222.1
                           INET6 ::192.168.222.1
                           INET6 fe80::fac0:100:de18:9391
    ge-1/2/1.221     Up    INET  192.168.221.1
                           INET6 ::192.168.221.1
                           INET6 fe80::fac0:100:dd18:9391
    ge-1/2/1.213     Up    INET  192.168.213.1
                           INET6 ::192.168.213.1
                           INET6 fe80::fac0:100:d518:9391
    ge-1/2/1.212     Up    INET  192.168.212.1
                           INET6 ::192.168.212.1
                           INET6 fe80::fac0:100:d418:9391
    ge-1/2/1.211     Up    INET  192.168.211.1
                           INET6 ::192.168.211.1
                           INET6 fe80::fac0:100:d318:9391
    ge-1/2/1.26      Up    INET  10.10.26.1
                           ISO   enabled
                           MPLS  enabled
                           INET6 fe80::fac0:100:1a18:9391
    ge-1/2/1.25      Up    INET  10.10.25.1
                           ISO   enabled
                           MPLS  enabled
                           INET6 fe80::fac0:100:1918:9391
    ge-1/2/1.24      Up    INET  10.10.24.1
                           ISO   enabled
                           MPLS  enabled
                           INET6 fe80::fac0:100:1818:9391
    ge-1/2/1.23      Up    INET  10.10.23.1
                           ISO   enabled
                           MPLS  enabled
                           INET6 fe80::fac0:100:1718:9391
    lo0.2            Up    INET  10.10.1.2
                           ISO   enabled
                           ISO   00.0001.2222.2222.2222
                           INET6 2011:310:1020::2
                           INET6 fe80::fac0:10f:fc18:93ff

so using `apply-group` or not, it's sufficient as long as core facing i/f (and
lo0) has the required family:

    inet6
    iso
    mpls

### QUESTION: about `apply-group-except`

in this lab, under which condition this is required?

    lab@MX80-NGGWR-01# show logical-systems lr3 interfaces                               
    apply-groups interface-group;
    +-- 47 lines: ge-1/2/1
    +-- 20 lines: ge-1/2/2
    +-- 10 lines: ae12
    +-- 13 lines: lo0

    [edit]
    lab@MX80-NGGWR-01# show logical-systems lr3 interfaces ae12                          
    unit 0 {
        family inet {
            address 10.10.36.1/30;
        }
        family iso;
        family mpls;
    }

    [edit]
    lab@MX80-NGGWR-01# show logical-systems lr3 interfaces ae12 | display inheritance    
    unit 0 {
        family inet {
            address 10.10.36.1/30;
        }
        family iso;
        family mpls;
    }
    
    lab@MX80-NGGWR-01# run show interfaces routing logical-system lr3 ae12   
    Interface        State Addresses
    ae12.0           Up    INET  10.10.36.1
                           ISO   enabled
                           MPLS  enabled
                           
have to config inet6 manually on ae bundle, to make it support an address
family?

    lab@MX80-NGGWR-01# show logical-systems lr3 interfaces ae12  
    unit 0 {
        family inet {
            address 10.10.36.1/30;
        }
        family iso;
        family inet6;
        family mpls;
    }
    
    lab@MX80-NGGWR-01# run show interfaces routing logical-system lr3 ae12    
    Interface        State Addresses
    ae12.0           Up    INET  10.10.36.1
                           ISO   enabled
                           INET6 fe80::fac0:1ff:fe18:93cc
                           MPLS  enabled
    
### transfer-on-commit

#### config

    [edit]
    lab@MX80-NGGWR-01# show system archival                                                       
    configuration {
        transfer-on-commit;
        archive-sites {
            "ftp://test:test@172.25.84.169/transfer-on-commit/";
            "scp://Ping:Juniper1%40@172.25.84.169/transfer-on-commit/";   #<------doesn't work
        }
    }

#### verify

    lab@MX80-NGGWR-02# run show log messages | match transfer 
    Aug 11 15:26:03  MX80-NGGWR-02 logger: transfer-file: Transferred /var/transfer/config/MX80-NGGWR-02_juniper.conf.gz_20130811_152551

    [edit]
    lab@abc# run show system configuration archival  

    /var/transfer/config/:
    total blocks: 8
    total files: 0

#### QUESTION: IMPORTANT: scp doesn't work

this looks succeed, but actually not working (no file a/v in the server)

    [edit]
    lab@MX80-NGGWR-01# save scp://Ping@172.25.84.169:transfer-on-commit/abc.txt    
    Ping@172.25.84.169's password:  
    tempfile 0%    0 tempfile     100%  163KB 162.7KB/s   00:00    
    Wrote 5444 lines of configuration to 'scp://Ping@172.25.84.169:transfer-on-commit/abc.txt'


### firewall filter

the target should be: block traffic coming from outside AS(like T/P), but
sourcing from IP that is same as internal networks (10.100.x).

#### config

    set logical-systems r2 firewall family inet filter filter-block-ipv4 term 1 from destination-address 192.168.100.0/24
    set logical-systems r2 firewall family inet filter filter-block-ipv4 term 1 then log
    set logical-systems r2 firewall family inet filter filter-block-ipv4 term 1 then discard
    set logical-systems r2 firewall family inet filter filter-block-ipv4 term 2 then accept
    set logical-systems r2 firewall family inet6 filter filter-block-ipv6 term 1 from destination-address 8000::/16
    set logical-systems r2 firewall family inet6 filter filter-block-ipv6 term 1 then log
    set logical-systems r2 firewall family inet6 filter filter-block-ipv6 term 1 then discard
    set logical-systems r2 firewall family inet6 filter filter-block-ipv6 term 2 then accept

    set logical-systems r2 interfaces ge-1/2/1 unit 210 family inet filter input filter-block-ipv4
    set logical-systems r2 interfaces ge-1/2/1 unit 210 family inet6 filter input filter-block-ipv6

#### TIPS: don't forget the last term of `then accept`

sam "deny all" rule as cisco

### LAG

#### config


    set interfaces ge-1/2/3 apply-groups interface-group
    set interfaces ge-1/2/3 gigether-options 802.3ad ae10

    set interfaces ge-1/2/4 apply-groups interface-group
    set interfaces ge-1/2/4 gigether-options 802.3ad ae11

    set interfaces ge-1/2/5 apply-groups interface-group
    set interfaces ge-1/2/5 gigether-options 802.3ad ae10
    
    set interfaces ge-1/2/6 apply-groups interface-group
    set interfaces ge-1/2/6 gigether-options 802.3ad ae11
    
    set logical-systems r3 interfaces ae10 unit 0 family inet address 10.100.36.1/30
    set logical-systems r3 interfaces ae10 unit 0 family iso
    set logical-systems r3 interfaces ae10 unit 0 family inet6
    set logical-systems r3 interfaces ae10 unit 0 family mpls

    set logical-systems r6 interfaces ae11 unit 0 family inet address 10.100.36.2/30
    set logical-systems r6 interfaces ae11 unit 0 family iso
    set logical-systems r6 interfaces ae11 unit 0 family inet6
    set logical-systems r6 interfaces ae11 unit 0 family mpls

### graceful restart

    set logical-systems r1 routing-options graceful-restart    
    set logical-systems r2 routing-options graceful-restart    
    set logical-systems r3 routing-options graceful-restart    
    set logical-systems r4 routing-options graceful-restart    
    set logical-systems r5 routing-options graceful-restart    
    set logical-systems r6 routing-options graceful-restart    
    set logical-systems r7 routing-options graceful-restart    
    set logical-systems r8 routing-options graceful-restart    

#### verify

    lab@MX80-NGGWR-02# run show route summary logical-system r3 
    Autonomous system number: 4012345678
    Router ID: 10.200.1.3

    inet.0: 50 destinations, 54 routes (50 active, 0 holddown, 1 hidden)
    Restart Complete
                  Direct:      9 routes,      9 active
                   Local:      8 routes,      8 active
                     BGP:     20 routes,     16 active
                   IS-IS:     17 routes,     17 active

    inet.3: 8 destinations, 9 routes (8 active, 0 holddown, 0 hidden)
    Restart Complete
                     BGP:      4 routes,      3 active
                    RSVP:      5 routes,      5 active

    iso.0: 1 destinations, 1 routes (1 active, 0 holddown, 0 hidden)
    Restart Complete
                  Direct:      1 routes,      1 active

    mpls.0: 10 destinations, 10 routes (10 active, 0 holddown, 0 hidden)
    Restart Complete
                    MPLS:      4 routes,      4 active
                    RSVP:      6 routes,      6 active

    bgp.l3vpn.0: 15 destinations, 15 routes (15 active, 0 holddown, 0 hidden)
    Restart Complete
                     BGP:     15 routes,     15 active

    inet6.0: 41 destinations, 47 routes (41 active, 0 holddown, 0 hidden)
    Restart Complete
                  Direct:     13 routes,      7 active
                   Local:     11 routes,     11 active
                     BGP:     23 routes,     23 active

    inet6.3: 8 destinations, 9 routes (8 active, 0 holddown, 0 hidden)
    Restart Complete
                     BGP:      4 routes,      3 active
                    RSVP:      5 routes,      5 active

#### QUESTION: GRES, NSR, GR

conceptual difference. need read more.

### BFD/ISIS

    set logical-systems r3 protocols isis interface ae10.0 bfd-liveness-detection minimum-interval 300 
    set logical-systems r6 protocols isis interface ae11.0 bfd-liveness-detection minimum-interval 300 

#### verify
    
    lab@MX80-NGGWR-02# run show bfd session  
                                                      Detect   Transmit
    Address                  State     Interface      Time     Interval  Multiplier
    10.100.36.1              Up        ae11.0         0.900     0.300        3   
    10.100.36.2              Up        ae10.0         0.900     0.300        3   

    2 sessions, 2 clients
    Cumulative transmit rate 6.7 pps, cumulative receive rate 6.7 pps

    [edit]
    lab@MX80-NGGWR-02# run show bfd session logical-system r3 
                                                      Detect   Transmit
    Address                  State     Interface      Time     Interval  Multiplier
    10.100.36.2              Up        ae10.0         0.900     0.300        3   

    1 sessions, 1 clients
    Cumulative transmit rate 3.3 pps, cumulative receive rate 3.3 pps

    [edit]
    lab@MX80-NGGWR-02# run show bfd session logical-system r3 detail  
                                                      Detect   Transmit
    Address                  State     Interface      Time     Interval  Multiplier
    10.100.36.2              Up        ae10.0         0.900     0.300        3   
     Client ISIS L2, TX interval 0.300, RX interval 0.300
     Session up time 00:01:17
     Local diagnostic None, remote diagnostic None
     Remote state Up, version 1
     Logical system 2, routing table index 7

    1 sessions, 1 clients
    Cumulative transmit rate 3.3 pps, cumulative receive rate 3.3 pps

    [edit]
    lab@MX80-NGGWR-02# run show bfd session logical-system r3 extensive  
                                                      Detect   Transmit
    Address                  State     Interface      Time     Interval  Multiplier
    10.100.36.2              Up        ae10.0         0.900     0.300        3   
     Client ISIS L2, TX interval 0.300, RX interval 0.300
     Session up time 00:01:23
     Local diagnostic None, remote diagnostic None
     Remote state Up, version 1
     Logical system 2, routing table index 7
     Min async interval 0.300, min slow interval 1.000
     Adaptive async TX interval 0.300, RX interval 0.300
     Local min TX interval 0.300, minimum RX interval 0.300, multiplier 3
     Remote min TX interval 0.300, min RX interval 0.300, multiplier 3
     Local discriminator 25, remote discriminator 26
     Echo mode disabled/inactive
     Remote is control-plane independent
      Session ID: 0x10003a

    1 sessions, 1 clients
    Cumulative transmit rate 3.3 pps, cumulative receive rate 3.3 pps

### BFD/OSPF

#### config

first config a whatever interval, then check session to read the RX interval
from peer. then change accordingly , if required.

    set logical-systems r2 protocols ospf area 0 interface ge-1/2/1.210 bfd-liveness-detection minimum-interval 300    

#### verity

    [edit]
    lab@MX80-NGGWR-02# run show bfd session logical-system r2 detail  
                                                      Detect   Transmit
    Address                  State     Interface      Time     Interval  Multiplier
    100.0.210.2              Up        ge-1/2/1.210   0.900     0.300        3   
     Client OSPF realm ospf-v2 Area 0.0.0.0, TX interval 0.300, RX interval 0.300
     Session up time 00:01:52
     Local diagnostic None, remote diagnostic NbrSignal
     Remote state Up, version 1
     Logical system 6, routing table index 11

    1 sessions, 1 clients
    Cumulative transmit rate 3.3 pps, cumulative receive rate 3.3 pps

## IGP

### IGP policy config

    #ospf import policy: reject some type5 : routes like 172.16.0/24~172.16.7/24 or longer prefix
    set logical-systems r2 policy-options policy-statement imp-ospf-rej-longer term 1 from protocol ospf
    set logical-systems r2 policy-options policy-statement imp-ospf-rej-longer term 1 from route-filter 172.16.0.0/21 orlonger
    set logical-systems r2 policy-options policy-statement imp-ospf-rej-longer term 1 then reject
    set logical-systems r2 policy-options policy-statement imp-ospf-rej-longer term 2 then accept
    set logical-systems r2 protocols ospf import imp-ospf-rej-longer
    
    #isis export policy: summarize 172.16.8~19/24
    set logical-systems r2 routing-options aggregate route 172.16.8.0/21
    set logical-systems r2 routing-options aggregate route 172.16.16.0/22
    set logical-systems r2 policy-options policy-statement exp-isis-from-ospf term 1 from protocol aggregate
    set logical-systems r2 policy-options policy-statement exp-isis-from-ospf term 1 from route-filter 172.16.8.0/21 exact
    set logical-systems r2 policy-options policy-statement exp-isis-from-ospf term 1 from route-filter 172.16.16.0/22 exact
    set logical-systems r2 policy-options policy-statement exp-isis-from-ospf term 1 then accept
    set logical-systems r2 protocols isis export exp-isis-from-ospf

    #ospf exprt policy: summarize internal as 10.200/16 and adv a default route to DC
    set logical-systems r2 routing-options aggregate route 10.200.0.0/16
    
    set logical-systems r2 policy-options policy-statement only-if-from-bgp term 1 from protocol bgp
    set logical-systems r2 policy-options policy-statement only-if-from-bgp term 1 from route-filter 0.0.0.0/0 prefix-length-range /0-/32
    set logical-systems r2 policy-options policy-statement only-if-from-bgp term 1 then accept
    set logical-systems r2 policy-options policy-statement only-if-from-bgp term 2 then reject
    set logical-systems r2 routing-options generate route 0.0.0.0/0 policy only-if-from-bgp
    
    set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 1 from protocol aggregate
    set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 1 from route-filter 10.200.0.0/16 exact
    set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 1 then accept
    
    set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 2 from protocol aggregate
    set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 2 from route-filter 0.0.0.0/0 exact
    set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 2 then accept
    
    set logical-systems r2 protocols ospf export exp-ospf-from-isis
    
    
### verify

#### DC => R2 => all Rs

R2 received all routes in LSAs

    lab@MX80-NGGWR-02# run show ospf database logical-system r2 

    Area 0.0.0.0
     Type       ID               Adv Rtr           Seq      Age  Opt  Cksum  Len 
    Router  *10.200.1.2       10.200.1.2       0x8000000c  1307  0x22 0x6c9c  36
    Router   100.0.210.2      100.0.210.2      0x8000000b  1471  0x22 0xa79a  36
    Network  100.0.210.2      100.0.210.2      0x80000002  1328  0x22 0x4770  32
        OSPF AS SCOPE link state database
     Type       ID               Adv Rtr           Seq      Age  Opt  Cksum  Len 
    Extern  *0.0.0.0          10.200.1.2       0x80000006   300  0x22 0x4394  36        #<------
    Extern  *10.200.0.0       10.200.1.2       0x80000008  2293  0x22 0x53af  36        #<------
    Extern   172.16.1.0       100.0.210.2      0x80000008  2756  0x22 0xba9   36        #<------
    Extern   172.16.2.0       100.0.210.2      0x80000008  2613  0x22 0xffb3  36        #<------
    Extern   172.16.3.0       100.0.210.2      0x80000008  2471  0x22 0xf4bd  36        #<------
    Extern   172.16.4.0       100.0.210.2      0x80000008  2328  0x22 0xe9c7  36        #<------
    Extern   172.16.5.0       100.0.210.2      0x80000008  2185  0x22 0xded1  36        #<------
    Extern   172.16.6.0       100.0.210.2      0x80000008  2042  0x22 0xd3db  36        #<------
    Extern   172.16.7.0       100.0.210.2      0x80000008  1899  0x22 0xc8e5  36        #<------
    Extern   172.16.8.0       100.0.210.2      0x80000008  1757  0x22 0xbdef  36
    Extern   172.16.9.0       100.0.210.2      0x80000008  1614  0x22 0xb2f9  36
    Extern   172.16.10.0      100.0.210.2      0x80000008  1186  0x22 0xa704  36
    Extern   172.16.11.0      100.0.210.2      0x80000008  1044  0x22 0x9c0e  36
    Extern   172.16.12.0      100.0.210.2      0x80000008   901  0x22 0x9118  36
    Extern   172.16.13.0      100.0.210.2      0x80000008   758  0x22 0x8622  36
    Extern   172.16.14.0      100.0.210.2      0x80000008   615  0x22 0x7b2c  36
    Extern   172.16.15.0      100.0.210.2      0x80000008   472  0x22 0x7036  36
    Extern   172.16.16.0      100.0.210.2      0x80000008   329  0x22 0x6540  36
    Extern   172.16.17.0      100.0.210.2      0x80000008   186  0x22 0x5a4a  36
    Extern   172.16.18.0      100.0.210.2      0x80000008    44  0x22 0x4f54  36
    Extern   172.16.19.0      100.0.210.2      0x80000007  2899  0x22 0x465d  36
    
R2 rejected 172.16.0-7/24 routes from DC

    [edit]
    test@MX80-NGGWR-02# run show route logical-system lr2 protocol ospf       

    inet.0: 57 destinations, 59 routes (56 active, 0 holddown, 1 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    172.16.8.0/24      *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.9.0/24      *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.10.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.11.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.12.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.13.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.14.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.15.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.16.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.17.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.18.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    172.16.19.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                        > to 192.168.100.2 via ge-1/3/0.1000
    224.0.0.5/32       *[OSPF/10] 10:08:17, metric 1
                          MultiRecv

.R2 then adv via ISIS to all internal Rs, but as 2 summarized routes

    test@MX80-NGGWR-02# run show isis database logical-system lr2 MX80-NGGWR-02-lr2.00 detail  
    IS-IS level 1 link-state database:

    MX80-NGGWR-02-lr2.00-00 Sequence: 0x56, Checksum: 0x6b1f, Lifetime: 1193 secs
       IP prefix: 172.16.8.0/21                   Metric:       10 External Up
       IP prefix: 172.16.16.0/22                  Metric:       10 External Up

    IS-IS level 2 link-state database:

    MX80-NGGWR-02-lr2.00-00 Sequence: 0x58, Checksum: 0x611, Lifetime: 1193 secs
       IS neighbor: MX80-NGGWR-02-lr2.02          Metric:        5
       IS neighbor: MX80-NGGWR-02-lr3.03          Metric:        5
       IS neighbor: MX80-NGGWR-02-lr4.02          Metric:        5
       IS neighbor: MX80-NGGWR-02-lr5.02          Metric:        5
       IS neighbor: MX80-NGGWR-02-lr6.03          Metric:        5
       IP prefix: 10.10.1.2/32                    Metric:        0 Internal Up
       IP prefix: 10.10.12.0/30                   Metric:        5 Internal Up
       IP prefix: 10.10.23.0/30                   Metric:        5 Internal Up
       IP prefix: 10.10.24.0/30                   Metric:        5 Internal Up
       IP prefix: 10.10.25.0/30                   Metric:        5 Internal Up
       IP prefix: 10.10.26.0/30                   Metric:        5 Internal Up
       IP prefix: 172.16.8.0/21                   Metric:       10 External Up  #<------
       IP prefix: 172.16.16.0/22                  Metric:       10 External Up  #<------
       
       
    lab@MX80-NGGWR-02# run show route protocol isis logical-system r3 172.16/16     

    inet.0: 52 destinations, 71 routes (52 active, 0 holddown, 2 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    172.16.8.0/21      *[IS-IS/165] 00:55:26, metric 15
                        > to 100.0.23.1 via ge-1/2/2.203
    172.16.16.0/22     *[IS-IS/165] 00:55:26, metric 15
                        > to 100.0.23.1 via ge-1/2/2.203

#### R2 => DC: summarization

    lab@MX80-NGGWR-02# run show ospf database logical-system r2 
    Extern  *0.0.0.0          10.200.1.2       0x80000006   300  0x22 0x4394  36        #<------
    Extern  *10.200.0.0       10.200.1.2       0x80000008  2293  0x22 0x53af  36        #<------
    
    lab@MX80-NGGWR-02# run show route protocol ospf logical-system r0 table dc.inet.0 

    dc.inet.0: 24 destinations, 24 routes (24 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    0.0.0.0/0          *[OSPF/150] 01:15:12, metric 0, tag 0
                        > to 100.0.210.1 via ge-1/2/2.210
    10.200.0.0/16      *[OSPF/150] 01:15:12, metric 0, tag 0
                        > to 100.0.210.1 via ge-1/2/2.210
    224.0.0.5/32       *[OSPF/10] 05:44:28, metric 1
                          MultiRecv
                          
#### R2 => DC: conditional default routes

DC got sum route of internal addr, but no default since not in R2's bgp route

    test@MX80-NGGWR-02# run show ospf route logical-system ldc 
    Topology default Route Table:

    Prefix             Path  Route      NH       Metric NextHop       Nexthop      
                       Type  Type       Type            Interface     Address/LSP
    10.10.1.2          Intra AS BR      IP            1 ge-1/3/1.1000 192.168.100.1
    10.10.0.0/16       Ext2  Network    IP            0 ge-1/3/1.1000 192.168.100.1     <------
    192.168.100.0/24   Intra Network    IP            1 ge-1/3/1.1000

    test@MX80-NGGWR-02# run show route logical-system lr2 0.0.0.0/0 exact  

    inet.0: 57 destinations, 59 routes (56 active, 0 holddown, 1 hidden)
    Restart Complete

### TIPS: conditional routes

the conditional routes can be either normal aggregation routes or generate route

### config:no IPv6 routes allowed in ISIS
    
    set logical-systems r1 protocols isis no-ipv6-routing  
    set logical-systems r2 protocols isis no-ipv6-routing  
    set logical-systems r3 protocols isis no-ipv6-routing  
    set logical-systems r4 protocols isis no-ipv6-routing  
    set logical-systems r5 protocols isis no-ipv6-routing  
    set logical-systems r6 protocols isis no-ipv6-routing  
    set logical-systems r7 protocols isis no-ipv6-routing  
    set logical-systems r8 protocols isis no-ipv6-routing  

### verify

    lab@MX80-NGGWR-02# run show isis route logical-system r1         
     IS-IS routing table             Current version: L1: 1 L2: 100
    IPv4/IPv6 Routes
    ----------------
    Prefix             L Version   Metric Type Interface       NH   Via
    10.100.36.0/24     2     100        7 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
    10.200.1.0/24      2     100       15 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
                                               ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    10.200.1.2/32      2     100        5 int  ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    10.200.1.3/32      2     100        5 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
    10.200.1.4/32      2     100       10 int  ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    10.200.1.5/32      2     100       10 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
                                               ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    10.200.1.6/32      2     100        7 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
    10.200.1.7/32      2     100       15 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
                                               ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    10.200.1.8/32      2     100       12 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
    100.0.23.0/24      2     100       10 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
                                               ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    100.0.24.0/24      2     100       10 int  ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    100.0.25.0/24      2     100       10 int  ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    100.0.26.0/24      2     100       10 int  ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    100.0.35.0/24      2     100       10 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
    100.0.46.0/24      2     100       12 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
    100.0.56.0/24      2     100       12 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
    100.0.57.0/24      2     100       15 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
                                               ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    100.0.68.0/24      2     100       12 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
    100.0.78.0/24      2     100       17 int  ge-1/2/1.103    IPV4 MX80-NGGWR-02-r3   
    172.16.8.0/21      2     100       15 int  ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    172.16.16.0/22     2     100       15 int  ge-1/2/1.102    IPV4 MX80-NGGWR-02-r2   
    
### config: isis metric

    set logical-systems r1 protocols isis reference-bandwidth 5g
    set logical-systems r2 protocols isis reference-bandwidth 5g
    set logical-systems r3 protocols isis reference-bandwidth 5g
    set logical-systems r4 protocols isis reference-bandwidth 5g
    set logical-systems r5 protocols isis reference-bandwidth 5g
    set logical-systems r6 protocols isis reference-bandwidth 5g
    set logical-systems r7 protocols isis reference-bandwidth 5g
    set logical-systems r8 protocols isis reference-bandwidth 5g

### verify

    lab@MX80-NGGWR-02# run show isis interface logical-system r1 
    IS-IS interface database:
    Interface             L CirID Level 1 DR        Level 2 DR        L1/L2 Metric
    ge-1/2/1.102          2   0x1 Disabled          MX80-NGGWR-02-r2.02      5/5
    ge-1/2/1.103          2   0x1 Disabled          MX80-NGGWR-02-r3.03      5/5
    lo0.1                 0   0x1 Passive           Passive                 0/0

## MPLS

### config:MPLS interfaces

    set logical-systems r1 protocols mpls interface ge-1/2/1.102
    set logical-systems r1 protocols mpls interface ge-1/2/1.103
    
    set logical-systems r2 protocols mpls interface ge-1/2/2.102
    set logical-systems r2 protocols mpls interface ge-1/2/1.203
    set logical-systems r2 protocols mpls interface ge-1/2/1.204
    set logical-systems r2 protocols mpls interface ge-1/2/1.205
    set logical-systems r2 protocols mpls interface ge-1/2/1.206
    
    set logical-systems r3 protocols mpls interface ge-1/2/2.103
    set logical-systems r3 protocols mpls interface ge-1/2/2.203
    set logical-systems r3 protocols mpls interface ge-1/2/1.305
    set logical-systems r3 protocols mpls interface ge-1/2/1.306
    
    set logical-systems r4 protocols mpls interface ge-1/2/2.204
    set logical-systems r4 protocols mpls interface ge-1/2/1.406
    
    set logical-systems r5 protocols mpls interface ge-1/2/2.305
    set logical-systems r5 protocols mpls interface ge-1/2/2.205
    set logical-systems r5 protocols mpls interface ge-1/2/1.506
    set logical-systems r5 protocols mpls interface ge-1/2/1.507
    set logical-systems r5 protocols mpls interface ge-1/2/1.522

    set logical-systems r6 protocols mpls interface ge-1/2/2.506
    set logical-systems r6 protocols mpls interface ge-1/2/2.306
    set logical-systems r6 protocols mpls interface ge-1/2/2.206
    set logical-systems r6 protocols mpls interface ge-1/2/2.406
    set logical-systems r6 protocols mpls interface ge-1/2/1.608
    
    set logical-systems r7 protocols mpls interface ge-1/2/1.708
    set logical-systems r7 protocols mpls interface ge-1/2/2.507

    set logical-systems r8 protocols mpls interface ge-1/2/2.608
    set logical-systems r8 protocols mpls interface ge-1/2/2.708

### TIP: `interface family mpls` vs. `protocol mpls interface`

both is about data plane, one from `interface` standpoint and the other from
`prototol` standpoint

### ipv6-tunneling & icmp-tunneling
    
    set logical-systems r1 protocols mpls ipv6-tunneling
    set logical-systems r1 protocols mpls icmp-tunneling
    set logical-systems r2 protocols mpls ipv6-tunneling
    set logical-systems r2 protocols mpls icmp-tunneling
    set logical-systems r3 protocols mpls ipv6-tunneling
    set logical-systems r3 protocols mpls icmp-tunneling
    set logical-systems r4 protocols mpls ipv6-tunneling
    set logical-systems r4 protocols mpls ipv6-tunneling
    set logical-systems r5 protocols mpls ipv6-tunneling
    set logical-systems r5 protocols mpls ipv6-tunneling
    set logical-systems r6 protocols mpls icmp-tunneling
    set logical-systems r6 protocols mpls icmp-tunneling
    set logical-systems r7 protocols mpls icmp-tunneling
    set logical-systems r7 protocols mpls icmp-tunneling
    set logical-systems r8 protocols mpls icmp-tunneling
    set logical-systems r8 protocols mpls icmp-tunneling
    

### config:RSVP

    set logical-systems r1 protocols rsvp interface ge-1/2/1.102
    set logical-systems r1 protocols rsvp interface ge-1/2/1.103
    
    set logical-systems r2 protocols rsvp interface ge-1/2/2.102
    set logical-systems r2 protocols rsvp interface ge-1/2/1.203
    set logical-systems r2 protocols rsvp interface ge-1/2/1.204
    set logical-systems r2 protocols rsvp interface ge-1/2/1.205
    set logical-systems r2 protocols rsvp interface ge-1/2/1.206

    set logical-systems r3 protocols rsvp interface ge-1/2/2.103
    set logical-systems r3 protocols rsvp interface ge-1/2/2.203
    set logical-systems r3 protocols rsvp interface ge-1/2/1.305
    set logical-systems r3 protocols rsvp interface ge-1/2/1.306

    set logical-systems r4 protocols rsvp interface ge-1/2/2.204
    set logical-systems r4 protocols rsvp interface ge-1/2/1.406
    
    set logical-systems r5 protocols rsvp interface ge-1/2/2.305
    set logical-systems r5 protocols rsvp interface ge-1/2/2.205
    set logical-systems r5 protocols rsvp interface ge-1/2/1.506
    
    set logical-systems r6 protocols rsvp interface ge-1/2/2.206
    set logical-systems r6 protocols rsvp interface ge-1/2/2.306
    set logical-systems r6 protocols rsvp interface ge-1/2/2.406
    set logical-systems r6 protocols rsvp interface ge-1/2/2.506

### config:LDP

    set logical-systems r1 protocols ldp interface lo0.1
    set logical-systems r4 protocols ldp interface lo0.4
    
    set logical-systems r5 protocols ldp interface lo0.5
    set logical-systems r5 protocols ldp interface ge-1/2/1.506
    set logical-systems r5 protocols ldp interface ge-1/2/1.507
    
    set logical-systems r6 protocols ldp interface lo0.6
    set logical-systems r6 protocols ldp interface ge-1/2/1.608
    set logical-systems r6 protocols ldp interface ge-1/2/2.506

    set logical-systems r7 protocols ldp interface ge-1/2/1.708
    set logical-systems r7 protocols ldp interface ge-1/2/2.507
    set logical-systems r7 protocols ldp interface lo0.7

    set logical-systems r8 protocols ldp interface ge-1/2/2.608
    set logical-systems r8 protocols ldp interface ge-1/2/2.708
    set logical-systems r8 protocols ldp interface lo0.8
    
            
### verify LDP

LDP sessions: Link LDP & Target LDP

              TLDPoRSVP            LLDP
         R1 ---------------   R5 ---------------  R7
            __            __  |                   |
              \_        _/    |                   |
                \__  __/      |                   |
               TLDPoRSVP      |                   |
                __/   \_      |                   |
              _/        \__   |                   |
            _/             \_ |                   |
         R4 ---------------   R6 ---------------  R8
              TLDPoRSVP             LLDP


    lab@MX80-NGGWR-02# run show ldp session logical-system r1 
      Address           State        Connection     Hold time  Adv. Mode
    10.200.1.5          Operational  Open             23         DU
    10.200.1.6          Operational  Open             23         DU

    [edit]
    lab@MX80-NGGWR-02# run show ldp session logical-system r4    
      Address           State        Connection     Hold time  Adv. Mode
    10.200.1.5          Operational  Open             21         DU
    10.200.1.6          Operational  Open             21         DU

    [edit]
    lab@MX80-NGGWR-02# run show ldp session logical-system r5    
      Address           State        Connection     Hold time  Adv. Mode
    10.200.1.1          Operational  Open             28         DU
    10.200.1.4          Operational  Open             28         DU
    10.200.1.6          Operational  Open             28         DU
    10.200.1.7          Operational  Open             28         DU

    [edit]
    lab@MX80-NGGWR-02# run show ldp session logical-system r6    
      Address           State        Connection     Hold time  Adv. Mode
    10.200.1.1          Operational  Open             26         DU
    10.200.1.4          Operational  Open             26         DU
    10.200.1.5          Operational  Open             26         DU
    10.200.1.8          Operational  Open             26         DU

    [edit]
    lab@MX80-NGGWR-02# run show ldp session logical-system r7    
      Address           State        Connection     Hold time  Adv. Mode
    10.200.1.5          Operational  Open             24         DU
    10.200.1.8          Operational  Open             24         DU

    [edit]
    lab@MX80-NGGWR-02# run show ldp session logical-system r8    
      Address           State        Connection     Hold time  Adv. Mode
    10.200.1.6          Operational  Open             22         DU
    10.200.1.7          Operational  Open             22         DU
    
### config:R2:to R5 ERO

    set logical-systems r2 protocols mpls label-switched-path r2-r5 to 10.200.1.5
    set logical-systems r2 protocols mpls label-switched-path r2-r5 primary via-r4-r6
    set logical-systems r2 protocols mpls path via-r4-r6 10.200.1.4 loose
    set logical-systems r2 protocols mpls path via-r4-r6 10.200.1.6 loose

### verify:ERO

    lab@MX80-NGGWR-02# run show mpls lsp logical-system r2 name r2-r5 ingress extensive  
    Ingress LSP: 5 sessions

    10.200.1.5
      From: 10.200.1.2, State: Up, ActiveRoute: 0, LSPname: r2-r5
      ActivePath: via-r4-r6 (primary)   #<------
      LSPtype: Static Configured, Penultimate hop popping
      LoadBalance: Random
      Encoding type: Packet, Switching type: Packet, GPID: IPv4
     *Primary   via-r4-r6        State: Up
        Priorities: 7 0
        SmartOptimizeTimer: 180
        Computed ERO (S [L] denotes strict [loose] hops): (CSPF metric: 15)
     100.0.24.2 S 100.0.46.2 S 100.0.56.1 S     #<------
        Received RRO (ProtectionFlag 1=Available 2=InUse 4=B/W 8=Node 10=SoftPreempt 20=Node-ID):
              100.0.24.2 100.0.46.2 100.0.56.1  #<------
        6 Aug 11 15:01:43.138 Selected as active path
        5 Aug 11 15:01:43.137 Record Route:  100.0.24.2 100.0.46.2 100.0.56.1
        4 Aug 11 15:01:43.137 Up
        3 Aug 11 15:01:43.043 Originate Call
        2 Aug 11 15:01:43.043 CSPF: computation result accepted  100.0.24.2 100.0.46.2 100.0.56.1
        1 Aug 11 15:01:13.569 CSPF failed: no route toward 10.200.1.4
      Created: Sun Aug 11 15:00:14 2013
    Total 1 displayed, Up 1, Down 0
    
### config:R2:to R6 link-protection
    
    set logical-systems r2 protocols mpls label-switched-path r2-r6 to 10.200.1.6
    set logical-systems r2 protocols mpls label-switched-path r2-r6 link-protection
    set logical-systems r2 protocols rsvp interface ge-1/2/1.206 link-protection
    set logical-systems r6 protocols rsvp interface ge-1/2/2.206 link-protection

### verify:link-protection

    [edit]
    lab@MX80-NGGWR-02# run show rsvp session logical-system r2 ingress                         
    Ingress RSVP: 6 sessions
    To              From            State   Rt Style Labelin Labelout LSPname 
    10.200.1.1      10.200.1.2      Up       0  1 FF       -        3 r2-r1
    10.200.1.3      10.200.1.2      Up       0  1 FF       -        3 r2-r3
    10.200.1.4      10.200.1.2      Up       0  1 FF       -        3 r2-r4
    10.200.1.5      10.200.1.2      Up       0  1 FF       -   299776 r2-r5
    10.200.1.6      10.200.1.2      Up       0  1 SE       -        3 r2-r6
    10.200.1.6      10.200.1.2      Up       0  1 SE       -   299920 Bypass->100.0.26.2        #<------
    Total 6 displayed, Up 6, Down 0

    [edit]
    lab@MX80-NGGWR-02# run show rsvp session logical-system r2 ingress name r2-r5 extensive    
    Ingress RSVP: 6 sessions

    10.200.1.5
      From: 10.200.1.2, LSPstate: Up, ActiveRoute: 0
      LSPname: r2-r5, LSPpath: Primary
      LSPtype: Static Configured
      Suggested label received: -, Suggested label sent: -
      Recovery label received: -, Recovery label sent: 299776
      Resv style: 1 FF, Label in: -, Label out: 299776
      Time left:    -, Since: Sun Aug 11 15:01:43 2013
      Tspec: rate 0bps size 0bps peak Infbps m 20 M 1500
      Port number: sender 1 receiver 31216 protocol 0
      PATH rcvfrom: localclient 
      Adspec: sent MTU 1500
      Path MTU: received 1500
      PATH sentto: 100.0.24.2 (ge-1/2/1.204) 1122 pkts
      RESV rcvfrom: 100.0.24.2 (ge-1/2/1.204) 1116 pkts
      Explct route: 100.0.24.2 100.0.46.2 100.0.56.1 
      Record route: <self> 100.0.24.2 100.0.46.2 100.0.56.1  
    Total 1 displayed, Up 1, Down 0
    
    [edit]
    lab@MX80-NGGWR-02# run show rsvp session logical-system r2 ingress name Bypas->100.0.26.2 extensive  
    Ingress RSVP: 6 sessions
    Total 0 displayed, Up 0, Down 0

### config:R4:to R3 secondary path

### in here <--------

### R1

    set logical-systems r3 protocols mpls interface ge-1/2/1.305 admin-group blue
    set logical-systems r5 protocols mpls interface ge-1/2/2.305 admin-group blue
    
    set logical-systems r1 protocols mpls label-switched-path r1-r2 to 10.200.1.2
    set logical-systems r1 protocols mpls label-switched-path r1-r3 to 10.200.1.3
    set logical-systems r1 protocols mpls label-switched-path r1-r4 to 10.200.1.4
    set logical-systems r1 protocols mpls label-switched-path r1-r4-green to 10.200.1.4
    set logical-systems r1 protocols mpls label-switched-path r1-r4-blue to 10.200.1.4
    set logical-systems r1 protocols mpls label-switched-path r1-r5 to 10.200.1.5
    set logical-systems r1 protocols mpls label-switched-path r1-r5 ldp-tunneling
    set logical-systems r1 protocols mpls label-switched-path r1-r6 to 10.200.1.6
    set logical-systems r1 protocols mpls label-switched-path r1-r6 ldp-tunneling
    set logical-systems r1 protocols mpls label-switched-path r1-r6 priority 7 7
    

### R2

    
    set logical-systems r2 protocols mpls explicit-null
    
    set logical-systems r2 protocols mpls label-switched-path r2-r1 to 10.200.1.1
    set logical-systems r2 protocols mpls label-switched-path r2-r3 to 10.200.1.3
    set logical-systems r2 protocols mpls label-switched-path r2-r4 to 10.200.1.4

### R3

    set logical-systems r3 protocols mpls admin-groups blue 4
    
    set logical-systems r3 protocols mpls label-switched-path r3-r1 to 10.200.1.1
    set logical-systems r3 protocols mpls label-switched-path r3-r2 to 10.200.1.2
    set logical-systems r3 protocols mpls label-switched-path r3-r4 to 10.200.1.4
    set logical-systems r3 protocols mpls label-switched-path r3-r5 to 10.200.1.5
    set logical-systems r3 protocols mpls label-switched-path r3-r5 admin-group exclude blue
    set logical-systems r3 protocols mpls label-switched-path r3-r6 to 10.200.1.6
    set logical-systems r3 protocols mpls label-switched-path r3-r6 policing filter lsp-60m
    
### R4

    set logical-systems r4 protocols mpls label-switched-path r4-r1 to 10.200.1.1
    set logical-systems r4 protocols mpls label-switched-path r4-r2 to 10.200.1.2
    set logical-systems r4 protocols mpls label-switched-path r4-r3 to 10.200.1.3
    set logical-systems r4 protocols mpls label-switched-path r4-r3 bandwidth 600m
    set logical-systems r4 protocols mpls label-switched-path r4-r3 adaptive
    set logical-systems r4 protocols mpls label-switched-path r4-r3 primary via-r2
    set logical-systems r4 protocols mpls label-switched-path r4-r3 secondary via-r2-r5 standby
    set logical-systems r4 protocols mpls label-switched-path r4-r5 to 10.200.1.5
    set logical-systems r4 protocols mpls label-switched-path r4-r5 ldp-tunneling
    set logical-systems r4 protocols mpls label-switched-path r4-r6 to 10.200.1.6
    set logical-systems r4 protocols mpls label-switched-path r4-r6 ldp-tunneling
    set logical-systems r4 protocols mpls path via-r2 10.200.1.2 strict
    set logical-systems r4 protocols mpls path via-r2-r5 10.200.1.2 strict
    set logical-systems r4 protocols mpls path via-r2-r5 10.200.1.5 loose
    

## BGP

lr5/lr6 <==inet/inet6 RR==> lr1/2/3/4/7/8

    test@MX80-NGGWR-02# run show bgp summary logical-system lr5    
    Groups: 3 Peers: 9 Down peers: 2
    Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
    bgp.l3vpn.0          
                           0          0          0          0          0          0
    inet.0               
                           0          0          0          0          0          0
    inet6.0              
                           0          0          0          0          0          0
    Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
    10.10.1.1        4012345678          3          5       0       0          35 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.2        4012345678          3          4       0       0          31 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.3        4012345678          2          3       0       0          27 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.4        4012345678          2          3       0       0          23 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.6        4012345678       3028       3027       0       0    23:04:54 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.7        4012345678          2          3       0       0          19 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.8        4012345678          2          3       0       0          15 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    192.168.11.0           1000          1          2       0       0    23:05:48 Active
    192.168.13.0           2000          1          2       0       0    23:05:48 Active


    test@MX80-NGGWR-02# run show bgp summary logical-system lr6    
    Groups: 2 Peers: 7 Down peers: 0
    Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
    bgp.l3vpn.0          
                           0          0          0          0          0          0
    inet.0               
                           0          0          0          0          0          0
    inet6.0              
                           0          0          0          0          0          0
    Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
    10.10.1.1        4012345678       3044       3030       0       0    23:05:56 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.2        4012345678       3038       3032       0       0    23:06:19 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.3        4012345678       3033       3030       0       0    23:06:13 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.4        4012345678       3059       3031       0       0    23:06:14 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.5        4012345678       3030       3030       0       0    23:05:51 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.7        4012345678       3057       3030       0       0    23:06:13 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0
    10.10.1.8        4012345678       3042       3030       0       0    23:06:13 Establ
      inet.0: 0/0/0/0
      inet6.0: 0/0/0/0

lr2/lr3 <==inet-vpn RR==> all PE:lr1/4/8

    test@MX80-NGGWR-02# run show bgp summary logical-system lr2    
    Groups: 3 Peers: 6 Down peers: 0
    Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
    bgp.l3vpn.0          
                           9          7          0          0          0          0
    inet.0               
                           2          0          0          0          0          0
    inet6.0              
                           0          0          0          0          0          0
    Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
    10.10.1.1        4012345678         31         29       0       1       10:46 Establ
      bgp.l3vpn.0: 3/3/3/0
    10.10.1.3        4012345678         27         28       0       0        9:29 Establ
      bgp.l3vpn.0: 0/0/0/0
    10.10.1.4        4012345678         30         29       0       1       10:46 Establ
      bgp.l3vpn.0: 4/4/4/0
    10.10.1.5        4012345678          7          5       0       1        1:44 Establ
      inet.0: 0/1/1/0
      inet6.0: 0/0/0/0
    10.10.1.6        4012345678       3032       3037       0       0    23:06:35 Establ
      inet.0: 0/1/1/0
      inet6.0: 0/0/0/0
    10.10.1.8        4012345678         27         34       0       1       10:46 Establ
      bgp.l3vpn.0: 0/2/2/0


    test@MX80-NGGWR-02# run show bgp summary logical-system lr3    
    Groups: 3 Peers: 6 Down peers: 0
    Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
    bgp.l3vpn.0          
                           9          7          0          0          0          0
    inet.0               
                           2          1          0          0          0          0
    inet6.0              
                           0          0          0          0          0          0
    Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
    10.10.1.1        4012345678         28         28       0       1       11:15 Establ
      bgp.l3vpn.0: 3/3/3/0
    10.10.1.2        4012345678         29         29       0       0       10:02 Establ
      bgp.l3vpn.0: 0/0/0/0
    10.10.1.4        4012345678         28         28       0       1       11:15 Establ
      bgp.l3vpn.0: 4/4/4/0
    10.10.1.5        4012345678          8          6       0       1        2:13 Establ
      inet.0: 1/1/1/0
      inet6.0: 0/0/0/0
    10.10.1.6        4012345678       3033       3035       0       0    23:07:02 Establ
      inet.0: 0/1/1/0
      inet6.0: 0/0/0/0
    10.10.1.8        4012345678         27         32       0       1       11:15 Establ
      bgp.l3vpn.0: 0/2/2/0


### P/T block

before policy, p/t route goes to each other

.t1's ipv4 bgp routes: got p1-3 routes:

    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table t1.inet.0 

    t1.inet.0: 13 destinations, 19 routes (13 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    10.10.0.0/16       *[BGP/170] 02:02:32, localpref 100
                          AS path: 4012345678 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321
    192.168.33.0/24    *[BGP/170] 02:02:29, localpref 100
                          AS path: 4012345678 300 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321
                        [BGP/170] 02:02:23, localpref 100
                          AS path: 4012345678 300 I, validation-state: unverified
                        > to 192.168.221.1 via ge-1/2/2.221
    192.168.44.0/24    *[BGP/170] 02:02:38, localpref 100
                          AS path: 4012345678 400 I, validation-state: unverified
                        > to 192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 02:02:32, localpref 100
                          AS path: 4012345678 400 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321
    212.100.0.0/16     *[BGP/170] 02:02:38, localpref 100
                          AS path: 4012345678 1002 I, validation-state: unverified
                        > to 192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 02:02:28, localpref 100
                          AS path: 4012345678 1002 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321
    215.1.0.0/16       *[BGP/170] 02:02:38, localpref 100
                          AS path: 4012345678 1000 I, validation-state: unverified
                        > to 192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 02:02:32, localpref 100
                          AS path: 4012345678 1000 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321
    218.2.0.0/16       *[BGP/170] 02:02:40, localpref 100
                          AS path: 4012345678 2000 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321
                        [BGP/170] 02:02:38, localpref 100
                          AS path: 4012345678 2000 I, validation-state: unverified
                        > to 192.168.221.1 via ge-1/2/2.221
    223.3.0.0/16       *[BGP/170] 02:02:38, localpref 100
                          AS path: 4012345678 3000 I, validation-state: unverified
                        > to 192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 02:02:32, localpref 100
                          AS path: 4012345678 3000 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321

t1 ipv6 routes, got all routes from both t and p:

    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table t1.inet6.0   

    t1.inet6.0: 14 destinations, 20 routes (14 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32     *[BGP/170] 16:17:53, localpref 100
                          AS path: 4012345678 1000 I, validation-state: unverified
                        > to ::192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 16:17:44, localpref 100
                          AS path: 4012345678 1000 I, validation-state: unverified
                        > to ::192.168.21.1 via ge-1/2/2.321
    2000:2000::/32     *[BGP/170] 16:17:49, localpref 100
                          AS path: 4012345678 2000 I, validation-state: unverified
                        > to ::192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 16:17:44, localpref 100
                          AS path: 4012345678 2000 I, validation-state: unverified
                        > to ::192.168.21.1 via ge-1/2/2.321
    2000:3000::/32     *[BGP/170] 16:17:59, localpref 100
                          AS path: 4012345678 3000 I, validation-state: unverified
                        > to ::192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 16:17:43, localpref 100
                          AS path: 4012345678 3000 I, validation-state: unverified
                        > to ::192.168.21.1 via ge-1/2/2.321
    3000:2000::/32     *[BGP/170] 16:17:57, localpref 100
                          AS path: 4012345678 1002 I, validation-state: unverified
                        > to ::192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 16:17:43, localpref 100
                          AS path: 4012345678 1002 I, validation-state: unverified
                        > to ::192.168.21.1 via ge-1/2/2.321


after policy application, t/p won't get routes from each other

    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table p3.inet6.0          

    p3.inet6.0: 9 destinations, 10 routes (9 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32     *[BGP/170] 17:02:46, localpref 100
                          AS path: 4012345678 1000 I, validation-state: unverified
                        > to ::192.168.213.1 via ge-1/2/2.213
    2000:2000::/32     *[BGP/170] 17:02:42, localpref 100
                          AS path: 4012345678 2000 I, validation-state: unverified
                        > to ::192.168.213.1 via ge-1/2/2.213

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table t1.inet0.0    
    error: No routing tables matching specification.

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table t1.inet.0     

    t1.inet.0: 10 destinations, 13 routes (10 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    10.10.0.0/16       *[BGP/170] 17:03:03, localpref 100
                          AS path: 4012345678 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321
    192.168.33.0/24    *[BGP/170] 17:03:00, localpref 100
                          AS path: 4012345678 300 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321
                        [BGP/170] 17:02:54, localpref 100
                          AS path: 4012345678 300 I, validation-state: unverified
                        > to 192.168.221.1 via ge-1/2/2.221
    192.168.44.0/24    *[BGP/170] 17:03:09, localpref 100
                          AS path: 4012345678 400 I, validation-state: unverified
                        > to 192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 17:03:03, localpref 100
                          AS path: 4012345678 400 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321
    212.100.0.0/16     *[BGP/170] 17:03:09, localpref 100
                          AS path: 4012345678 1002 I, validation-state: unverified
                        > to 192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 17:02:59, localpref 100
                          AS path: 4012345678 1002 I, validation-state: unverified
                        > to 192.168.21.1 via ge-1/2/2.321

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table t1.inet6.0   

    t1.inet6.0: 11 destinations, 14 routes (11 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    3000:2000::/32     *[BGP/170] 17:03:48, localpref 100
                          AS path: 4012345678 1002 I, validation-state: unverified
                        > to ::192.168.221.1 via ge-1/2/2.221
                        [BGP/170] 17:03:34, localpref 100
                          AS path: 4012345678 1002 I, validation-state: unverified
                        > to ::192.168.21.1 via ge-1/2/2.321

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table p1.inet.0     

    p1.inet.0: 12 destinations, 16 routes (12 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    192.168.33.0/24    *[BGP/170] 17:03:47, localpref 100
                          AS path: 4012345678 300 I, validation-state: unverified
                        > to 192.168.211.1 via ge-1/2/2.211
                        [BGP/170] 00:16:56, localpref 100
                          AS path: 4012345678 300 I, validation-state: unverified
                        > to 192.168.11.1 via ge-1/2/2.511
    192.168.44.0/24    *[BGP/170] 17:04:08, localpref 100
                          AS path: 4012345678 400 I, validation-state: unverified
                        > to 192.168.211.1 via ge-1/2/2.211
                        [BGP/170] 00:16:56, localpref 100
                          AS path: 4012345678 400 I, validation-state: unverified
                        > to 192.168.11.1 via ge-1/2/2.511
    218.2.0.0/16       *[BGP/170] 17:04:11, localpref 100
                          AS path: 4012345678 2000 I, validation-state: unverified
                        > to 192.168.211.1 via ge-1/2/2.211
                        [BGP/170] 00:16:56, localpref 100
                          AS path: 4012345678 2000 I, validation-state: unverified
                        > to 192.168.11.1 via ge-1/2/2.511
    223.3.0.0/16       *[BGP/170] 17:04:10, localpref 100
                          AS path: 4012345678 3000 I, validation-state: unverified
                        > to 192.168.211.1 via ge-1/2/2.211
                        [BGP/170] 00:16:56, localpref 100
                          AS path: 4012345678 3000 I, validation-state: unverified
                        > to 192.168.11.1 via ge-1/2/2.511

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table p1.inet6.0   

    p1.inet6.0: 12 destinations, 16 routes (12 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    2000:2000::/32     *[BGP/170] 17:04:13, localpref 100
                          AS path: 4012345678 2000 I, validation-state: unverified
                        > to ::192.168.211.1 via ge-1/2/2.211
                        [BGP/170] 00:19:56, localpref 100
                          AS path: 4012345678 2000 I, validation-state: unverified
                        > to ::192.168.31.1 via ge-1/2/2.311
    2000:3000::/32     *[BGP/170] 17:04:17, localpref 100
                          AS path: 4012345678 3000 I, validation-state: unverified
                        > to ::192.168.211.1 via ge-1/2/2.211
                        [BGP/170] 17:04:07, localpref 100
                          AS path: 4012345678 3000 I, validation-state: unverified
                        > to ::192.168.31.1 via ge-1/2/2.311

c router can still get routes from both p/t:

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table c3.inet.0     

    c3.inet.0: 10 destinations, 10 routes (9 active, 0 holddown, 1 hidden)
    + = Active Route, - = Last Active, * = Both

    1.0.0.0/8          *[BGP/170] 17:06:53, localpref 100
                          AS path: 65513 4012345678 1001 I, validation-state: unverified
                        > to 192.168.133.1 via ge-1/2/2.133
    10.10.0.0/16       *[BGP/170] 17:06:59, localpref 100
                          AS path: 65513 4012345678 I, validation-state: unverified
                        > to 192.168.133.1 via ge-1/2/2.133
    212.100.0.0/16     *[BGP/170] 17:06:53, localpref 100
                          AS path: 65513 4012345678 1002 I, validation-state: unverified
                        > to 192.168.133.1 via ge-1/2/2.133
    215.1.0.0/16       *[BGP/170] 17:06:59, localpref 100
                          AS path: 65513 4012345678 1000 I, validation-state: unverified
                        > to 192.168.133.1 via ge-1/2/2.133
    218.2.0.0/16       *[BGP/170] 17:06:53, localpref 100
                          AS path: 65513 4012345678 2000 I, validation-state: unverified
                        > to 192.168.133.1 via ge-1/2/2.133
    223.3.0.0/16       *[BGP/170] 17:06:59, localpref 100
                          AS path: 65513 4012345678 3000 I, validation-state: unverified
                        > to 192.168.133.1 via ge-1/2/2.133


### TIP: unverified route

<http://www.juniper.net/techpubs/en_US/junos12.2/topics/topic-map/bgp-origin-as-validation.html>

### TIP: missing RID on a pure IPv6 router

in the IPv6 network (only IPv6), BGP router id need to be specified 32 bit. OPEN message  need to be add on both CEs router.

Quote from RFC 2544:
  "Note that the information referred above is distinct from the BGP
   Identifier used in the BGP-4 tie breaking procedure. The BGP
   Identifier is a 32 bit unsigned integer exchanged between two peers
   at session establishment time, within an OPEN message. This is a
   system wide value determined at startup which must be unique in the
   network and should be derived from an IPv4 address regardless of the
   network protocol(s) a particular BGP-4 instance is configured to
   convey at a given moment."

If you are not configure router ID on CE router, OPEN message will fail.  BGP session cannot established. Debug will show why IPv6 BGP session failed when CE router have no router id.

    Mar  1 08:57:35  prime pe2: rpd[3251]: bgp_get_open: NOTIFICATION sent to 11::2+4597 (proto): 
    code 2 (Open Message Error) subcode 3 (bad BGP ID), Reason: peer 11::2+4597 (proto): 
    invalid BGP identifier 0x0


### TIP: policy "internal/exteral" vs. "route-type internal/external"

<http://www.juniper.net/techpubs/en_US/junos/topics/usage-guidelines/policy-configuring-match-conditions-in-routing-policy-terms.html>

    external [ type metric-type ]   
    Standard        
    (OSPF and IS-IS only) Match IGP external routes. For IS-IS routes, the external
    condition also matches routes that are exported from one IS-IS level to
    another. The type keyword is optional and is applicable only to OSPF external
    routes. When you do not specify type, the external condition matches all IGP
    external (OSPF and IS-IS) routes. When you specify type, the external condition
    matches only OSPF external routes with the specified OSPF metric type. The
    metric type can either be 1 or 2.

To match BGP external routes, use the route-type match condition.

    route-type value        
    Standard        
    Type of BGP route. The value can be one of the following:
    external—External route.
    internal—Internal route.

To match IGP external routes, use the external match condition.


### ipv6

#### TIP: Configuring IPv6 BGP Routes over IPv4 Transport

<http://www.juniper.net/techpubs/en_US/junos10.4/topics/usage-guidelines/routing-configuring-ipv6-bgp-routes-over-ipv4-transport.html>

##### accept-remote-nexthop                                                

Q: how to make C router (BGP ipv4 neighbor) accept V6 routes without 
configuring "accept-remote-nexthop" on it?                           
                                                                     
A: no way, C should have that pre-configured already.                
Kevin: is it possible to use IPv4-compatible address as next-hop to carry ipv6 routes? 
http://www.juniper.net/techpubs/en_US/junos12.2/topics/example/bgp-ipv6.html


#### accept-remote-nexthop

.initially got no ipv6 route from a v4 peer, not even as hidden

    lab@MX80-NGGWR-01# show logical-systems lr7 protocols bgp group c4                                                              
    family inet {
        unicast;
    }
    family inet6 {
        unicast;
    }
    neighbor 192.168.34.0 {
        peer-as 400;
    }

    lab@MX80-NGGWR-01# run show route receive-protocol bgp 192.168.34.0 logical-system lr7 table inet6.0 hidden extensive  

    inet6.0: 7 destinations, 14 routes (2 active, 0 holddown, 10 hidden)
    Restart Complete

.add `accept-remote-nexthops`: showing as hidden

    [edit]
    lab@MX80-NGGWR-01# show | compare  
    [edit logical-systems lr7 protocols bgp group c4]
    +     accept-remote-nexthop;

    [edit]
    lab@MX80-NGGWR-01# commit  
    commit complete

    [edit]
    lab@MX80-NGGWR-01# run show route receive-protocol bgp 192.168.34.0 logical-system lr7 table inet6.0 hidden extensive    

    inet6.0: 8 destinations, 15 routes (2 active, 0 holddown, 11 hidden)
    Restart Complete
      4444:4444:4444::/48 (1 entry, 0 announced)
         Accepted
         Nexthop: ::ffff:192.168.34.0   <------
         AS path: 400 I

#### policy: set next-hop with "next-hop peer-address"

    [edit]
    lab@MX80-NGGWR-01# show | compare  
    [edit logical-systems lr7 protocols bgp group c4]
    +     import imp-bgp-fix-nh;
    [edit logical-systems lr7 policy-options]
    +    policy-statement imp-bgp-fix-nh {
    +        term 1 {
    +            from {
    +                protocol bgp;
    +                neighbor 192.168.34.0;
    +            }
    +            then {
    +                next-hop peer-address;
    +                accept;
    +            }
    +        }
    +    }

    [edit]
    lab@MX80-NGGWR-01# commit  
    commit complete


##### QUESTION(solved): next-hop peer-address didn't really change the nexthop?

check `rib` (after input policy applied) or `rib-out`(after input&output policy
applied), not `rib-in` (before policy applied)

use `show route protocol`, instead of `show route received-protocol bgp`

`rib-in`:

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr7 receive-protocol bgp 192.168.34.0 4444:4444:4444::/48 extensive  

    inet6.0: 24 destinations, 39 routes (22 active, 0 holddown, 9 hidden)
    Restart Complete
    * 4444:4444:4444::/48 (1 entry, 1 announced)
         Accepted
         Nexthop: ::ffff:192.168.34.0
         AS path: 400 I

`rib`:

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr7 protocol bgp table inet6.0 4444:4444:4444::/48 extensive           

    inet6.0: 24 destinations, 39 routes (22 active, 0 holddown, 9 hidden)
    Restart Complete
    4444:4444:4444::/48 (1 entry, 1 announced)
    TSI:
    KRT in-kernel 4444:4444:4444::/48 -> {192.168.34.0}
    Page 0 idx 1 Type 1 val 286a108
        Flags: Nexthop Change
        Nexthop: Self
        Localpref: 100
        AS path: [4012345678] 400 I
        Communities:
    Path 4444:4444:4444:: from 192.168.34.0 Vector len 4.  Val: 1
            *BGP    Preference: 170/-101
                    Next hop type: Router, Next hop index: 2221
                    Address: 0x28886e4
                    Next-hop reference count: 3
                    Source: 192.168.34.0
                    Next hop: 192.168.34.0 via ge-1/2/1.734, selected
                    Session Id: 0x100001
                    State: <Active Ext>
                    Local AS: 4012345678 Peer AS:   400
                    Age: 4d 4:12:27 
                    Validation State: unverified 
                    Task: BGP_400.192.168.34.0+179
                    Announcement bits (3): 0-KRT 3-BGP_RT_Background 4-Resolve tree 5 
                    AS path: 400 I
                    Accepted
                    Localpref: 100
                    Router ID: 44.44.1.1

`rib-out`:

    [edit]
    lab@MX80-NGGWR-01# run show route advertising-protocol bgp 10.10.1.5 logical-system lr7 4444:4444:4444::/48 extensive  

    inet6.0: 24 destinations, 39 routes (22 active, 0 holddown, 9 hidden)
    Restart Complete
    * 4444:4444:4444::/48 (1 entry, 1 announced)
     BGP group to-rr type Internal
         Nexthop: Self
         Flags: Nexthop Change
         Localpref: 100
         AS path: [4012345678] 400 I

##### knowledge base

RFC1771/4271 BGP Routing Information Base consists of three parts as explained below:

* The Adj-RIBs-In: BGP RIB-In stores BGP routing information received from
different peers. The stored information is used as an input to BGP decision
process. In other words this is the information received from peers before
applying any attribute modifications or route filtering to them.

* The Local RIB: The local routing information base stores the resulted
information from processing the RIBs-In database’s information. These are the
routes that are used locally after applying BGP policies and decision process.

* The Adj-RIBs-out: This one stores the routing information that was selected by
the local BGP router to advertise to its peers through BGP update messages. Do
not forget;  BGP only advertises best routes if they are allowed by local
outbound policies.

#### how C routers got the IPv6 routes? 

"accept-remote-nexthop" must have been pre-configured in C.

    [edit]
    lab@MX80-NGGWR-01# run show route receive-protocol bgp 192.168.133.1 logical-system lptc table c3.inet6.0 all

    c3.inet6.0: 4 destinations, 4 routes (4 active, 0 holddown, 0 hidden)

    [edit]
    lab@MX80-NGGWR-01# set logical-systems lptc routing-instances c3 protocols bgp group to-r1 accept-remote-nexthop

    [edit]
    lab@MX80-NGGWR-01# commit
    commit complete

    [edit]
    lab@MX80-NGGWR-01# run show route receive-protocol bgp 192.168.133.1 logical-system lptc table c3.inet6.0 all
                                                                                                              ^^^
                                                                                                         (hidden)

    c3.inet6.0: 11 destinations, 11 routes (4 active, 0 holddown, 7 hidden)
      Prefix                  Nexthop              MED     Lclpref    AS path
      2000:1000::/32          ::ffff:192.168.133.1                    65513 4012345678 1000 I
      2000:2000::/32          ::ffff:192.168.133.1                    65513 4012345678 2000 I
      2000:3000::/32          ::ffff:192.168.133.1                    65513 4012345678 3000 I
      3000:1000::/32          ::ffff:192.168.133.1                    65513 4012345678 1001 I
      3000:2000::/32          ::ffff:192.168.133.1                    65513 4012345678 1002 I
      4444:4444:4444::/48     ::ffff:192.168.133.1                    65513 4012345678 400 I
      5555:5555:5555::/48     ::ffff:192.168.133.1                    65513 4012345678 500 I
                              ^^^^^^^^^^^^^^^^^^^^
                              ipv4-mapped ipv6 address
                              generated by system

##### change next-hop to local IPv6 address of export policy in LR

    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table c3.inet6.0 hidden 4444:4444:4444::/48 extensive  

    c3.inet6.0: 13 destinations, 13 routes (6 active, 0 holddown, 7 hidden)
    4444:4444:4444::/48 (1 entry, 0 announced)
             BGP    Preference: 170/-101
                    Next hop type: Unusable     <------
                    Address: 0x23f3f04
                    Next-hop reference count: 10
                    State: <Hidden Ext>
                    Local AS:   300 Peer AS: 65513
                    Age: 10:16 
                    Task: BGP_65513_300.192.168.133.1+52133
                    AS path: 65513 4012345678 400 I
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.1
                    Indirect next hops: 1
                            Protocol next hop: ::ffff:192.168.133.1     <------
                            Indirect next hop: 0 -

    lab@MX80-NGGWR-01# show logical-systems lr1 policy-options policy-statement exp-bgp-fix-nh  
    term 1 {
        from {
            protocol bgp;
            route-filter ::0/0 prefix-length-range /0-/128;
        }
        then {
            next-hop ::192.168.133.1;
        }
    }

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table c3.inet6.0  4444:4444:4444::/48 extensive          

    c3.inet6.0: 13 destinations, 13 routes (13 active, 0 holddown, 0 hidden)
    4444:4444:4444::/48 (1 entry, 1 announced)
    TSI:
    KRT in-kernel 4444:4444:4444::/48 -> {::192.168.133.1}      <------
            *BGP    Preference: 170/-101
                    Next hop type: Router, Next hop index: 2361
                    Address: 0x282ea38
                    Next-hop reference count: 21
                    Source: 192.168.133.1
                    Next hop: ::192.168.133.1 via ge-1/2/2.133, selected        <------
                    State: <Active Ext>
                    Local AS:   300 Peer AS: 65513
                    Age: 36 
                    Task: BGP_65513_300.192.168.133.1+52133
                    Announcement bits (2): 0-KRT 2-Resolve tree 4 
                    AS path: 65513 4012345678 400 I
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.1

#### TIP: all 4 solutions 

the issue: 
    no consistent LDP/RSVP (R2/3 run RSVP vs. R7/8 run LDP)     => 
    R2/3 <--> R7/8 can't resolve each other as BGP NH           =>
    R2/3 , R7/8 are missing each other in inet.3                =>
    R2/3 , R7/8 are missing each other in inet6.3               =>
    R2/3 , R7/8: routes learned from each other show as hidden

the solutions:

1. RSVP install R7/8 @ R2/3 + 
   LDP adv host @ R5/6 for R7/8(no RSVP)
2. change NH @ RR(R5/6): because both R1/2 and R7/8 can resolve RR as NH
3. mix 1/2
4. RRs (R5/6) BGP: adv R2/3/7/8 , so all R has each other's lo0
   all Rs(R2/3/5/6/7/8) BGP: 
       inet labeld-unicast rib inet.3 => put learned BGP NH learned in inet.3
   R2/3,R7/8 BGP:
       inet labeld-unicast rib-group 6pe (inet.3=>inet6.3) 
 
notes:
maybe R8 is not involved here (no C/P/T router attached, only for MPLS/VPN)

#### solution 1: install@R2/3 + adv addr@R5/6

##### install R7/R8 host into R2/3 inet6.3

install R7/8 host in R2/R3 at LSP

    activate logical-systems lr2 protocols mpls label-switched-path r2-r5 install 10.10.1.7/32  
    activate logical-systems lr2 protocols mpls label-switched-path r2-r5 install 10.10.1.8/32    
    activate logical-systems lr2 protocols mpls label-switched-path r2-r6 install 10.10.1.7/32    
    activate logical-systems lr2 protocols mpls label-switched-path r2-r6 install 10.10.1.8/32    
    
    activate logical-systems lr3 protocols mpls label-switched-path r3-r5 install 10.10.1.7/32  
    activate logical-systems lr3 protocols mpls label-switched-path r3-r5 install 10.10.1.8/32    
    activate logical-systems lr3 protocols mpls label-switched-path r3-r6 install 10.10.1.7/32    
    activate logical-systems lr3 protocols mpls label-switched-path r3-r6 install 10.10.1.8/32    
    
r2/r3: before install:

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr2 table inet6.3    

    inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[RSVP/7/1] 3d 18:20:35, metric 5
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    ::ffff:10.10.1.3/128
                       *[RSVP/7/1] 3d 18:20:36, metric 5
                        > to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
    ::ffff:10.10.1.4/128
                       *[RSVP/7/1] 3d 18:20:36, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    ::ffff:10.10.1.5/128
                       *[RSVP/7/1] 3d 18:20:35, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
    ::ffff:10.10.1.6/128
                       *[RSVP/7/1] 3d 18:20:36, metric 5
                        > to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6

    lab@MX80-NGGWR-01# run show route logical-system lr3 table inet6.3               

    inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[RSVP/7/1] 3d 18:52:18, metric 5
                        > to 10.10.13.1 via ge-1/2/2.13, label-switched-path r3-r1
    ::ffff:10.10.1.2/128
                       *[RSVP/7/1] 3d 18:52:19, metric 5
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
    ::ffff:10.10.1.4/128
                       *[RSVP/7/1] 3d 18:52:19, metric 10
                        > to 10.10.36.2 via ae12.0, label-switched-path r3-r4
    ::ffff:10.10.1.5/128
                       *[RSVP/7/1] 3d 18:52:19, metric 5
                        > to 10.10.35.2 via ge-1/2/1.35, label-switched-path r3-r5
    ::ffff:10.10.1.6/128
                       *[RSVP/7/1] 3d 18:52:18, metric 5
                        > to 10.10.36.2 via ae12.0, label-switched-path r3-r6

r2/lr3 after install:

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr2 table inet6.3    

    inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[RSVP/7/1] 3d 18:58:42, metric 5
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    ::ffff:10.10.1.3/128
                       *[RSVP/7/1] 3d 18:58:43, metric 5
                        > to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
    ::ffff:10.10.1.4/128
                       *[RSVP/7/1] 3d 18:58:43, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    ::ffff:10.10.1.5/128
                       *[RSVP/7/1] 3d 18:58:42, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
    ::ffff:10.10.1.6/128
                       *[RSVP/7/1] 00:00:21, metric 5
                        > to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
    ::ffff:10.10.1.7/128        <------
                       *[RSVP/7/1] 00:00:21, metric 5
                          to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                        > to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
    ::ffff:10.10.1.8/128        <------
                       *[RSVP/7/1] 00:00:21, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr3 table inet6.3              
     
    inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[RSVP/7/1] 3d 18:58:32, metric 5
                        > to 10.10.13.1 via ge-1/2/2.13, label-switched-path r3-r1
    ::ffff:10.10.1.2/128
                       *[RSVP/7/1] 3d 18:58:33, metric 5
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
    ::ffff:10.10.1.4/128
                       *[RSVP/7/1] 3d 18:58:33, metric 10
                        > to 10.10.36.2 via ae12.0, label-switched-path r3-r4
    ::ffff:10.10.1.5/128
                       *[RSVP/7/1] 00:00:12, metric 5
                        > to 10.10.35.2 via ge-1/2/1.35, label-switched-path r3-r5
    ::ffff:10.10.1.6/128
                       *[RSVP/7/1] 00:00:12, metric 5
                        > to 10.10.36.2 via ae12.0, label-switched-path r3-r6
    ::ffff:10.10.1.7/128        <------
                       *[RSVP/7/1] 00:00:12, metric 5
                          to 10.10.35.2 via ge-1/2/1.35, label-switched-path r3-r5
                        > to 10.10.36.2 via ae12.0, label-switched-path r3-r6
    ::ffff:10.10.1.8/128        <------
                       *[RSVP/7/1] 00:00:12, metric 5
                        > to 10.10.35.2 via ge-1/2/1.35, label-switched-path r3-r5
                          to 10.10.36.2 via ae12.0, label-switched-path r3-r6


lr7/lr8:

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr7 table inet6.3    

    inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 3d 19:02:35, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299808
    ::ffff:10.10.1.4/128
                       *[LDP/9] 3d 19:02:33, metric 1
                          to 10.10.78.2 via ge-1/2/1.78, Push 299824
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299824
    ::ffff:10.10.1.5/128
                       *[LDP/9] 3d 19:02:48, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.6/128
                       *[LDP/9] 3d 19:02:40, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78, Push 299792
    ::ffff:10.10.1.8/128
                       *[LDP/9] 3d 19:02:42, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr8 table inet6.3    

    inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 3d 19:02:40, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68, Push 299856
    ::ffff:10.10.1.4/128
                       *[LDP/9] 3d 19:02:40, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68, Push 299872
    ::ffff:10.10.1.5/128
                       *[LDP/9] 3d 19:02:40, metric 1
                        > to 10.10.78.1 via ge-1/2/2.78, Push 299776
    ::ffff:10.10.1.6/128
                       *[LDP/9] 3d 19:02:47, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68
    ::ffff:10.10.1.7/128
                       *[LDP/9] 3d 19:02:49, metric 1
                        > to 10.10.78.1 via ge-1/2/2.78

    set logical-systems lr5 policy-options policy-statement egr-ldp-adv-235 term 1 from route-filter 10.10.1.2/32 exact
    set logical-systems lr5 policy-options policy-statement egr-ldp-adv-235 term 1 from route-filter 10.10.1.3/32 exact
    set logical-systems lr5 policy-options policy-statement egr-ldp-adv-235 term 1 then accept

    set logical-systems lr6 policy-options policy-statement egr-ldp-adv-236 term 1 from route-filter 10.10.1.2/32 exact
    set logical-systems lr6 policy-options policy-statement egr-ldp-adv-236 term 1 from route-filter 10.10.1.3/32 exact
    set logical-systems lr6 policy-options policy-statement egr-ldp-adv-236 term 1 then accept

    //after:

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr7 table inet6.3    

    inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 3d 19:28:26, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299808
    ::ffff:10.10.1.2/128
                       *[LDP/9] 00:16:26, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.3/128
                       *[LDP/9] 00:16:26, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.4/128
                       *[LDP/9] 3d 19:28:24, metric 1
                          to 10.10.78.2 via ge-1/2/1.78, Push 299824
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299824
    ::ffff:10.10.1.8/128
                       *[LDP/9] 3d 19:28:33, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr8 table inet6.3          

    inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 3d 19:12:08, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68, Push 299856
    ::ffff:10.10.1.2/128        <------
                       *[LDP/9] 00:00:10, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68
    ::ffff:10.10.1.3/128        <------
                       *[LDP/9] 00:00:10, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68
    ::ffff:10.10.1.4/128
                       *[LDP/9] 3d 19:12:08, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68, Push 299872
    ::ffff:10.10.1.7/128
                       *[LDP/9] 3d 19:12:17, metric 1
                        > to 10.10.78.1 via ge-1/2/2.78

have to add lr5/6 lo0:

    set logical-systems lr5 policy-options policy-statement egr-ldp-adv-235 term 1 from route-filter 10.10.1.5/32 exact
    set logical-systems lr6 policy-options policy-statement egr-ldp-adv-236 term 1 from route-filter 10.10.1.6/32 exact

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr7 table inet6.3                                                                                         

    inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 3d 20:41:40, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299808
    ::ffff:10.10.1.2/128
                       *[LDP/9] 01:29:40, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.3/128
                       *[LDP/9] 01:29:40, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.4/128
                       *[LDP/9] 3d 20:41:38, metric 1
                          to 10.10.78.2 via ge-1/2/1.78, Push 299824
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299824
    ::ffff:10.10.1.5/128
                       *[LDP/9] 00:00:22, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.6/128
                       *[LDP/9] 00:00:22, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78, Push 299792
    ::ffff:10.10.1.8/128
                       *[LDP/9] 3d 20:41:47, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr8 table inet6.3    

    inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 3d 20:41:52, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68, Push 299856
    ::ffff:10.10.1.2/128
                       *[LDP/9] 01:29:54, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68
    ::ffff:10.10.1.3/128
                       *[LDP/9] 01:29:54, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68
    ::ffff:10.10.1.4/128
                       *[LDP/9] 3d 20:41:52, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68, Push 299872
    ::ffff:10.10.1.5/128
                       *[LDP/9] 00:00:36, metric 1
                        > to 10.10.78.1 via ge-1/2/2.78, Push 299776
    ::ffff:10.10.1.6/128
                       *[LDP/9] 00:00:36, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68
    ::ffff:10.10.1.7/128
                       *[LDP/9] 3d 20:42:01, metric 1
                        > to 10.10.78.1 via ge-1/2/2.78

C3 inet6.0 route:

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table c3.inet6.0 

    c3.inet6.0: 13 destinations, 13 routes (13 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32     *[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                          AS path: 65513 4012345678 1000 I
                        > to ::192.168.133.1 via ge-1/2/2.133
    2000:2000::/32     *[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                          AS path: 65513 4012345678 2000 I
                        > to ::192.168.133.1 via ge-1/2/2.133
    2000:3000::/32     *[BGP/170] 2d 01:01:03, localpref 100, from 192.168.133.1
                          AS path: 65513 4012345678 3000 I
                        > to ::192.168.133.1 via ge-1/2/2.133
    3000:1000::/32     *[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                          AS path: 65513 4012345678 1001 I
                        > to ::192.168.133.1 via ge-1/2/2.133
    3000:2000::/32     *[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                          AS path: 65513 4012345678 1002 I
                        > to ::192.168.133.1 via ge-1/2/2.133
    4444:4444:4444::/48*[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                          AS path: 65513 4012345678 400 I
                        > to ::192.168.133.1 via ge-1/2/2.133
    5555:5555:5555::/48*[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                          AS path: 65513 4012345678 500 I
                        > to ::192.168.133.1 via ge-1/2/2.133

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table c4.inet6.0    

    c4.inet6.0: 13 destinations, 13 routes (13 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32     *[BGP/170] 01:39:10, localpref 100, from 192.168.34.1
                          AS path: 4012345678 1000 I
                        > to ::192.168.34.1 via ge-1/2/2.734
    2000:2000::/32     *[BGP/170] 01:39:10, localpref 100, from 192.168.34.1
                          AS path: 4012345678 2000 I
                        > to ::192.168.34.1 via ge-1/2/2.734
    2000:3000::/32     *[BGP/170] 01:39:10, localpref 100, from 192.168.34.1
                          AS path: 4012345678 3000 I
                        > to ::192.168.34.1 via ge-1/2/2.734
    3000:1000::/32     *[BGP/170] 01:39:10, localpref 100, from 192.168.34.1
                          AS path: 4012345678 1001 I
                        > to ::192.168.34.1 via ge-1/2/2.734
    3000:2000::/32     *[BGP/170] 01:39:10, localpref 100, from 192.168.34.1
                          AS path: 4012345678 1002 I
                        > to ::192.168.34.1 via ge-1/2/2.734
    3333:3333:3333::/48*[BGP/170] 2d 00:16:27, localpref 100, from 192.168.34.1
                          AS path: 4012345678 300 I
                        > to ::192.168.34.1 via ge-1/2/2.734
    5555:5555:5555::/48*[BGP/170] 2d 00:16:27, localpref 100, from 192.168.34.1
                          AS path: 4012345678 500 I
                        > to ::192.168.34.1 via ge-1/2/2.734

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table c5.inet6.0    

    c5.inet6.0: 13 destinations, 13 routes (13 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32     *[BGP/170] 2d 01:17:46, localpref 100
                          AS path: 4012345678 1000 I
                        > to 33b1::1 via ge-1/2/2.435
    2000:2000::/32     *[BGP/170] 2d 01:17:39, localpref 100
                          AS path: 4012345678 2000 I
                        > to 33b1::1 via ge-1/2/2.435
    2000:3000::/32     *[BGP/170] 2d 01:17:42, localpref 100
                          AS path: 4012345678 3000 I
                        > to 33b1::1 via ge-1/2/2.435
    3000:1000::/32     *[BGP/170] 2d 01:17:46, localpref 100
                          AS path: 4012345678 1001 I
                        > to 33b1::1 via ge-1/2/2.435
    3000:2000::/32     *[BGP/170] 2d 01:17:42, localpref 100
                          AS path: 4012345678 1002 I
                        > to 33b1::1 via ge-1/2/2.435
    3333:3333:3333::/48*[BGP/170] 2d 01:17:46, localpref 100
                          AS path: 4012345678 300 I
                        > to 33b1::1 via ge-1/2/2.435
    4444:4444:4444::/48*[BGP/170] 2d 01:17:46, localpref 100
                          AS path: 4012345678 400 I
                        > to 33b1::1 via ge-1/2/2.435

##### make R2/3 inet6.3 reachable from R7

###### R7 inet6.3

    lab@MX80-NGGWR-01# run show route logical-system lr7 table inet6.3    

    inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 4d 04:38:10, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299808
    ::ffff:10.10.1.4/128
                       *[LDP/9] 4d 04:38:09, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299824
                          to 10.10.78.2 via ge-1/2/1.78, Push 299840
    ::ffff:10.10.1.5/128
                       *[LDP/9] 4d 04:38:20, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.6/128
                       *[LDP/9] 4d 04:38:20, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78, Push 299808
    ::ffff:10.10.1.8/128
                       *[LDP/9] 3d 17:24:26, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78

###### config: adv R2/R3 from R5/R6

    lab@MX80-NGGWR-01# show logical-systems lr5 policy-options policy-statement egr-ldp-adv-235  
    term 1 {
        from {
            route-filter 10.10.1.2/32 exact;
            route-filter 10.10.1.3/32 exact;
            route-filter 10.10.1.5/32 exact;
        }
        then accept;
    }
    
    lab@MX80-NGGWR-01# set logical-systems lr5 protocols ldp egress-policy egr-ldp-adv-235  
    
###### R7 iet6.3 after policy

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr7 table inet6.3    

    inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 4d 04:42:00, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299808
    ::ffff:10.10.1.2/128
                       *[LDP/9] 00:00:57, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.3/128
                       *[LDP/9] 00:00:46, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.4/128
                       *[LDP/9] 4d 04:41:59, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299824
                          to 10.10.78.2 via ge-1/2/1.78, Push 299840
    ::ffff:10.10.1.5/128
                       *[LDP/9] 4d 04:42:10, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.6/128
                       *[LDP/9] 4d 04:42:10, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78, Push 299808
    ::ffff:10.10.1.8/128
                       *[LDP/9] 3d 17:28:16, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78
                        
R8 inet6.3 table is still missing R2/R3

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr8 table inet6.3    

    inet6.3: 6 destinations, 6 routes (6 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 4d 04:50:49, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68, Push 299824
    ::ffff:10.10.1.3/128
                       *[LDP/9] 00:00:04, metric 1
                        > to 10.10.78.1 via ge-1/2/2.78, Push 299776
    ::ffff:10.10.1.4/128
                       *[LDP/9] 4d 04:50:44, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68, Push 299888
    ::ffff:10.10.1.5/128
                       *[LDP/9] 4d 04:50:55, metric 1
                        > to 10.10.78.1 via ge-1/2/2.78, Push 299776
    ::ffff:10.10.1.6/128
                       *[LDP/9] 4d 04:50:55, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68
    ::ffff:10.10.1.7/128
                       *[LDP/9] 4d 04:50:55, metric 1
                        > to 10.10.78.1 via ge-1/2/2.78

config same on R6:
 
    [edit]
    lab@MX80-NGGWR-01# show | compare  
    [edit logical-systems lr6 protocols ldp]
    -    inactive: egress-policy egr-ldp-adv-236;
    +    egress-policy egr-ldp-adv-236;
     
    [edit]
    lab@MX80-NGGWR-01# commit  
    commit complete
     
     
R8 inet6.3 :

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr8 table inet6.3    

    inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 4d 04:56:45, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68, Push 299824
    ::ffff:10.10.1.2/128
                       *[LDP/9] 00:00:27, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68
    ::ffff:10.10.1.3/128
                       *[LDP/9] 00:00:27, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68
    ::ffff:10.10.1.4/128
                       *[LDP/9] 4d 04:56:40, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68, Push 299888
    ::ffff:10.10.1.5/128
                       *[LDP/9] 4d 04:56:51, metric 1
                        > to 10.10.78.1 via ge-1/2/2.78, Push 299776
    ::ffff:10.10.1.6/128
                       *[LDP/9] 4d 04:56:51, metric 1
                        > to 10.10.68.1 via ge-1/2/2.68
    ::ffff:10.10.1.7/128
                       *[LDP/9] 4d 04:56:51, metric 1
                        > to 10.10.78.1 via ge-1/2/2.78

###### QUESTION: do we need do the same on R6?

there is no C router attached in R8.
R8 has nothing to do with the IPv6 task here
so R8 don't need to reach R2/R3's lo0 in inet6.3
it looks no need to config R6 ldp also adv R2/R3 lo0

##### install both host routes in both LSPs in both router R2/3

this is just for completeness, seems not help

    lab@MX80-NGGWR-01# show | compare  
    [edit logical-systems lr2 protocols mpls label-switched-path r2-r5]
    !       active: install 10.10.1.7/32 { ... }
    !       active: install 10.10.1.8/32 { ... }
    [edit logical-systems lr2 protocols mpls label-switched-path r2-r6]
    !       active: install 10.10.1.7/32 { ... }
    [edit logical-systems lr3 protocols mpls label-switched-path r3-r5]
    !       active: install 10.10.1.7/32 { ... }
    !       active: install 10.10.1.8/32 { ... }
    [edit logical-systems lr3 protocols mpls label-switched-path r3-r6]
    !       active: install 10.10.1.8/32 { ... }

#### QUESTION: ipv6 not end2end pingable

    [edit]
    lab@MX80-NGGWR-01# run ping 4444:4444:4444::1 logical-system lptc routing-instance c3   
    PING6(56=40+8+8 bytes) ::192.168.133.0 --> 4444:4444:4444::1
    ^C
    --- 4444:4444:4444::1 ping6 statistics ---
    8 packets transmitted, 0 packets received, 100% packet loss
    
    lab@MX80-NGGWR-01# run ping inet6 4444:4444:4444::1 logical-system lptc routing-instance c3 source 3333:3333:3333::1 
    PING6(56=40+8+8 bytes) 3333:3333:3333::1 --> 4444:4444:4444::1
    ^C
    --- 4444:4444:4444::1 ping6 statistics ---
    6 packets transmitted, 0 packets received, 100% packet loss
    
    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lptc table c4.inet6.0 3333:3333:3333::1    

    c4.inet6.0: 23 destinations, 23 routes (23 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    3333:3333:3333::/48*[BGP/170] 4d 08:39:09, localpref 100, from 192.168.34.1
                          AS path: 4012345678 300 I, validation-state: unverified
                        > to ::192.168.34.1 via ge-1/2/2.734

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lptc table c3.inet6.0 4444:4444:4444::1    

    c3.inet6.0: 26 destinations, 29 routes (26 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    4444:4444:4444::/48*[BGP/170] 4d 08:39:41, localpref 100, from 192.168.133.1
                          AS path: 65513 4012345678 400 I, validation-state: unverified
                        > to ::192.168.133.1 via ge-1/2/2.133


#### solution2 : change next-hop at RR ("no install")

##### remove solution1

    deactivate logical-systems r2 protocols mpls label-switched-path r2-r5 install 10.10.1.7/32  
    deactivate logical-systems r2 protocols mpls label-switched-path r2-r5 install 10.10.1.8/32    
    deactivate logical-systems r2 protocols mpls label-switched-path r2-r6 install 10.10.1.7/32    
    deactivate logical-systems r2 protocols mpls label-switched-path r2-r6 install 10.10.1.8/32    
    
    deactivate logical-systems r3 protocols mpls label-switched-path r3-r5 install 10.10.1.7/32  
    deactivate logical-systems r3 protocols mpls label-switched-path r3-r5 install 10.10.1.8/32    
    deactivate logical-systems r3 protocols mpls label-switched-path r3-r6 install 10.10.1.7/32    
    deactivate logical-systems r3 protocols mpls label-switched-path r3-r6 install 10.10.1.8/32    
    
    deactivate logical-systems r5 protocols ldp egress-policy    
    deactivate logical-systems r6 protocols ldp egress-policy    

    commit
    run clear bgp neighbor soft logical-system r2
    run clear bgp neighbor soft logical-system r3
    
##### add solution 2
    
    change bgp nh from rr R4/5 when reflecting between R2/3 and R7

    set logical-systems lr5 protocols bgp group rr neighbor 10.10.1.2 export exp-bgp-nhs-from-r7  
    set logical-systems lr5 protocols bgp group rr neighbor 10.10.1.3 export exp-bgp-nhs-from-r7    
    set logical-systems lr5 protocols bgp group rr neighbor 10.10.1.7 export exp-bgp-nhs-from-r2-r3                           
    set logical-systems lr6 protocols bgp group rr neighbor 10.10.1.2 export exp-bgp-nhs-from-r7  
    set logical-systems lr6 protocols bgp group rr neighbor 10.10.1.3 export exp-bgp-nhs-from-r7    
    set logical-systems lr6 protocols bgp group rr neighbor 10.10.1.7 export exp-bgp-nhs-from-r2-r3                           
    
    commit
    run clear bgp neighbor soft logical-system lr5
    run clear bgp neighbor soft logical-system lr6
    
#### solution 3: mixed solution1&2

##### remove solution 2: 

    delete logical-systems lr5 protocols bgp group rr neighbor 10.10.1.2 export exp-bgp-nhs-from-r7  
    delete logical-systems lr5 protocols bgp group rr neighbor 10.10.1.3 export exp-bgp-nhs-from-r7    
    delete logical-systems lr5 protocols bgp group rr neighbor 10.10.1.7 export exp-bgp-nhs-from-r2-r3                           
    delete logical-systems lr6 protocols bgp group rr neighbor 10.10.1.2 export exp-bgp-nhs-from-r7  
    delete logical-systems lr6 protocols bgp group rr neighbor 10.10.1.3 export exp-bgp-nhs-from-r7    
    delete logical-systems lr6 protocols bgp group rr neighbor 10.10.1.7 export exp-bgp-nhs-from-r2-r3                           
    
    commit
    run clear bgp neighbor soft logical-system lr5
    run clear bgp neighbor soft logical-system lr6
    
this solution does not look great. no extra benefit also.

#### solution 4: rib + rib-group


##### config

    #R5/6: advertise R2/3/7/8 from R2/3 via BGP:

    set logical-systems r5 policy-options policy-statement exp-bgp-adv-2378 term 1 from route-filter 10.10.1.2/32 exact  
    set logical-systems r5 policy-options policy-statement exp-bgp-adv-2378 term 1 from route-filter 10.10.1.3/32 exact  
    set logical-systems r5 policy-options policy-statement exp-bgp-adv-2378 term 1 from route-filter 10.10.1.7/32 exact  
    set logical-systems r5 policy-options policy-statement exp-bgp-adv-2378 term 1 from route-filter 10.10.1.8/32 exact  
    set logical-systems r5 policy-options policy-statement exp-bgp-adv-2378 term 1 then accept
    
    set logical-systems r6 policy-options policy-statement exp-bgp-adv-2378 term 1 from route-filter 10.10.1.2/32 exact  
    set logical-systems r6 policy-options policy-statement exp-bgp-adv-2378 term 1 from route-filter 10.10.1.3/32 exact  
    set logical-systems r6 policy-options policy-statement exp-bgp-adv-2378 term 1 from route-filter 10.10.1.7/32 exact  
    set logical-systems r6 policy-options policy-statement exp-bgp-adv-2378 term 1 from route-filter 10.10.1.8/32 exact  
    set logical-systems r6 policy-options policy-statement exp-bgp-adv-2378 term 1 then accept
    
    set logical-systems r5 protocols bgp group rr export exp-int-agg exp-bgp-adv-2378
    set logical-systems r6 protocols bgp group rr export exp-int-agg exp-bgp-adv-2378


    #R2/3/5/6: allow both unlabeled (`unicast`) and labeled (`labeled-unicast`) BGP routes; and place labeled routes in inet.3
    #R2/3: also copy table inet.3 into inet6.3

    set logical-systems r2 routing-options rib-groups 6pe import-rib [ inet.3 inet6.3 ]
    set logical-systems r2 protocols bgp group to-rr family inet labeled-unicast rib-group 6pe
    set logical-systems r2 protocols bgp group to-rr family inet labeled-unicast rib inet.3
    
    set logical-systems r3 routing-options rib-groups 6pe import-rib [ inet.3 inet6.3 ]
    set logical-systems r3 protocols bgp group to-rr family inet labeled-unicast rib-group 6pe
    set logical-systems r3 protocols bgp group to-rr family inet labeled-unicast rib inet.3
    
    set logical-systems r7 routing-options rib-groups 6pe import-rib [ inet.3 inet6.3 ]
    set logical-systems r7 protocols bgp group to-rr family inet labeled-unicast rib-group 6pe
    set logical-systems r7 protocols bgp group to-rr family inet labeled-unicast rib inet.3
    
    set logical-systems r5 protocols bgp group to-rr family inet labeled-unicast rib inet.3
    set logical-systems r6 protocols bgp group to-rr family inet labeled-unicast rib inet.3
    

##### before

    lab@MX80-NGGWR-01# run show route logical-system r2 10.10.1.7    

    inet.0: 62 destinations, 62 routes (62 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    10.10.1.7/32       *[IS-IS/18] 06:13:33, metric 10
                        > to 10.10.25.2 via ge-1/2/1.25

    lab@MX80-NGGWR-01# run show route logical-system r2 table inet.3     

    inet.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    10.10.1.1/32       *[RSVP/7/1] 05:55:13, metric 5
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    10.10.1.3/32       *[RSVP/7/1] 05:55:14, metric 5
                        > to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
    10.10.1.4/32       *[RSVP/7/1] 05:55:13, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.5/32       *[RSVP/7/1] 05:55:13, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
    10.10.1.6/32       *[RSVP/7/1] 05:55:13, metric 5
                        > to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
                          

##### after

    lab@MX80-NGGWR-01# run show route logical-system r2 10.10.1.7    

    inet.0: 67 destinations, 83 routes (67 active, 0 holddown, 2 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    10.10.1.7/32       *[IS-IS/18] 06:13:40, metric 10
                        > to 10.10.25.2 via ge-1/2/1.25
                        [BGP/170] 00:00:03, MED 5, localpref 100, from 10.10.1.5
                          AS path: I
                        > to 10.10.25.2 via ge-1/2/1.25
                        [BGP/170] 00:00:05, MED 10, localpref 100, from 10.10.1.6
                          AS path: I
                        > to 10.10.25.2 via ge-1/2/1.25
                          to 10.10.26.2 via ge-1/2/1.26
                          
    lab@MX80-NGGWR-01# run show route logical-system r2 table inet.3    

    inet.3: 8 destinations, 9 routes (8 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    10.10.1.1/32       *[RSVP/7/1] 05:55:36, metric 5
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    10.10.1.2/32       *[BGP/170] 00:00:01, MED 5, localpref 4294967294, from 10.10.1.5
                          AS path: I
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
    10.10.1.3/32       *[RSVP/7/1] 05:55:37, metric 5
                        > to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
                        [BGP/170] 00:00:01, MED 5, localpref 4294967294, from 10.10.1.5
                          AS path: I
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
    10.10.1.4/32       *[RSVP/7/1] 05:55:36, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.5/32       *[RSVP/7/1] 05:55:36, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
    10.10.1.6/32       *[RSVP/7/1] 05:55:36, metric 5
                        > to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
    10.10.1.7/32       *[BGP/170] 00:00:01, MED 1, localpref 100, from 10.10.1.5
                          AS path: I
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
    10.10.1.8/32       *[BGP/170] 00:00:01, MED 1, localpref 100, from 10.10.1.5
                          AS path: I
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5


##### verification of rib-group

before rib-group applied at R7:

    family inet labeled-uncast rib-group 6pe

inet.3 is good but inet6.3 are still not complete:

    [edit]
    lab@MX80-NGGWR-01# run show route table inet.3 logical-system r7                                              

    inet.3: 8 destinations, 9 routes (8 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    10.10.1.1/32       *[LDP/9] 07:21:14, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299824
    10.10.1.2/32       *[BGP/170] 00:00:20, MED 5, localpref 4294967294, from 10.10.1.5         #<------
                          AS path: I
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299968
    10.10.1.3/32       *[BGP/170] 00:00:20, MED 5, localpref 4294967294, from 10.10.1.5         #<------
                          AS path: I
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299984
    10.10.1.4/32       *[LDP/9] 07:21:15, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78, Push 299840
                          to 10.10.57.1 via ge-1/2/2.57, Push 299808
    10.10.1.5/32       *[LDP/9] 07:21:44, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    10.10.1.6/32       *[LDP/9] 07:21:43, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78, Push 299776
    10.10.1.7/32       *[BGP/170] 00:00:20, MED 1, localpref 100, from 10.10.1.5
                          AS path: I
                        > to 10.10.57.1 via ge-1/2/2.57, Push 300000
    10.10.1.8/32       *[LDP/9] 07:21:43, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78
                        [BGP/170] 00:00:20, MED 1, localpref 100, from 10.10.1.5
                          AS path: I
                        > to 10.10.57.1 via ge-1/2/2.57, Push 300016

    [edit]
    lab@MX80-NGGWR-01# run show route table inet6.3 logical-system r7   

    inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 07:21:28, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299824
    ::ffff:10.10.1.4/128
                       *[LDP/9] 07:21:29, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78, Push 299840
                          to 10.10.57.1 via ge-1/2/2.57, Push 299808
    ::ffff:10.10.1.5/128
                       *[LDP/9] 07:21:58, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.6/128
                       *[LDP/9] 07:21:57, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78, Push 299776
    ::ffff:10.10.1.8/128
                       *[LDP/9] 07:21:57, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78
                        
    [edit]
    lab@MX80-NGGWR-01# run show route table inet6.3 logical-system r7             

    inet6.3: 8 destinations, 9 routes (8 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[LDP/9] 07:36:12, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299824
    ::ffff:10.10.1.2/128        #<------
                       *[BGP/170] 00:10:46, MED 5, localpref 4294967294, from 10.10.1.5
                          AS path: I
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299968
    ::ffff:10.10.1.3/128        #<------
                       *[BGP/170] 00:10:46, MED 5, localpref 4294967294, from 10.10.1.5
                          AS path: I
                        > to 10.10.57.1 via ge-1/2/2.57, Push 299984
    ::ffff:10.10.1.4/128
                       *[LDP/9] 07:36:13, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78, Push 299840
                          to 10.10.57.1 via ge-1/2/2.57, Push 299808
    ::ffff:10.10.1.5/128
                       *[LDP/9] 07:36:42, metric 1
                        > to 10.10.57.1 via ge-1/2/2.57
    ::ffff:10.10.1.6/128
                       *[LDP/9] 07:36:41, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78, Push 299776
    ::ffff:10.10.1.7/128        #<------
                       *[BGP/170] 00:10:46, MED 1, localpref 100, from 10.10.1.5
                          AS path: I
                        > to 10.10.57.1 via ge-1/2/2.57, Push 300000
    ::ffff:10.10.1.8/128
                       *[LDP/9] 07:36:41, metric 1
                        > to 10.10.78.2 via ge-1/2/1.78
                        [BGP/170] 00:10:46, MED 1, localpref 100, from 10.10.1.5
                          AS path: I
                        > to 10.10.57.1 via ge-1/2/2.57, Push 300016
                        

##### TIPS: about rib/rib-group/inet.3/inet6.3

R2/3 inet.3 won't change before R5/6 and R2/3 configured:

    family inet labeled-unicast rib inet.3

R2/3 inet6.3 won't updated before R2/3 configured:

    family inet labeled-uncast rib-group 6pe

#### QUESTION: `family inet unicast` vs. `family inet labeled-unicast`

    lab@MX80-NGGWR-01# show logical-systems lr2 protocols bgp group to-rr  
    type internal;
    local-address 10.10.1.2;
    import imp-bgp-rtbh;
    family inet {
        unicast;                #<------these are fine being configured 
        labeled-unicast {       #<------together
            rib-group 6pe;
            rib {
                inet.3;
            }
        }
    }
    family inet6 {
        labeled-unicast {       #<------can't co-exist with unicast.
            explicit-null;
        }
    }
    export [ exp-bgp-nhs exp-bgp-lo0-v6 ];
    neighbor 10.10.1.5;
    neighbor 10.10.1.6;
    
error message:

    lab@MX80-NGGWR-01# set logical-systems lr2 protocols bgp group to-rr family inet6 unicast  

    [edit]
    lab@MX80-NGGWR-01# commit  
    [edit logical-systems lr2 protocols]
      'bgp'
        Error in neighbor 10.10.1.5 of group to-rr:
    peer cannot have both inet6 unicast and inet6 labeled-unicast nlri
    error: configuration check-out failed
    
#### QUESTION: why `family inet labeled-unicast` in this solution?

according to 6PE spec, `family inet6 labeled-unicast explicit-null` is used to
assign label (2) to ipv6 prefixes at PE, why again `family inet
labeled-unicast`? 

is it just because `rib` and `rib-group` feature only supported under
labeled-unicast by design?

<http://www.juniper.net/techpubs/software/junos/junos94/swconfig-routing/rib_2.html>
<http://www.juniper.net/techpubs/en_US/junos12.1/topics/topic-map/bgp-multiprotocol.html>

You can allow both labeled and unlabeled routes to be exchanged in a single
session. The labeled routes are placed in the inet.3 routing table, and both
labeled and unlabeled unicast routes can be sent to or received by the routing
device. 

To allow both labeled and unlabeled routes to be exchanged, include the rib
inet.3 statement:

    rib inet.3;


#### TIP: `inet labeled-unicast rib inet.3`

manual about "rib inet.3":

You can allow both labeled and unlabeled routes to be exchanged in a single
session. The labeled routes are placed in the inet.3 routing table, and both
labeled and unlabeled unicast routes can be sent or received by the router.

(WRONG) this looks also inherit all behavior of `inet unicast`

(correct):
without rib inet.3, following can't co-exist:

    inet unicast 
    inet labeled-unicast

so only one address family can't be supported

with rib inet.3 ,these are fine:
    
    inet unicast
    inet labeled-unicast rib inet.3

so now "You can allow both labeled and unlabeled routes to be exchanged in a single
session"

#### TIP: policy "from rib inet.3"

    R1             (BGP route NLRI addr family)         R5
       ============================================>
    inet.0          inet unicast                        inet.0
    inet.3          inet labeled-unicast                inet.3
    
    inet unicast: 传递unicast的路由，放入inet.0
    labeled-unicast：传递unciast路由，放入inet.0
    labeld-unicast rib inet.3: 传递inet.3的路由，放入inet.3
    inet unicast+rib inet.3：传递inet.0和inet.3的路由，unicast的放入inet.0, rib inet.3的放入inet.3 
   这就是为什么无法同时配置inet uncast 和labeled-unicast，而可以同时配置inet unicast和rib inet.3 
    
    lab@MX80-NGGWR-01# show logical-systems r5 policy-options policy-statement exp-bgp-adv-1    
    term 1 {
        from {
            protocol isis;                      #<------taken from inet.0
            route-filter 10.10.1.1/32 exact;    #<--will be adv. as `inet-unicast`
        }
        then accept;
        
    }
    term 2 {
        from {
            rib inet.3;                         #<------taken from inet.0
            route-filter 10.10.1.1/32 exact;    #<--will be adv. as `inet-labeled-unicast`
        }
        then accept;
    }

#### TIP: 6PE basic

* like MPLS/VPN. but no vrf, 
* bgp assign either reserved label 2(ipv6 explicit) or any lable as inner
  label(like vpn label).
* running on top of LSP
* Juniper PE core facing i/f `must` enable ipv6 => troubleshooting tip.
  (seems only if use label 2). otherwise forwarding issue.

##### simple topo

    <--ipv6 (AS1000)-> <---------ipv4 AS(3000)-------> <--ipv6 (AS2000)->
    +-----+        +-----+         +-----+         +-----+       +-----+
    | ce1 |--------| pe1 |---------|  p  |---------| pe2 |-------| ce2 |
    +-+---+ V1501  +-+---+ V1503   +--+--+ V1502   +--+--+ V1504 +--+--+
      |  10::1/126   | 192.168.0.0/30 | 192.168.0.4/30|   11::0/126 |
      |              | 1.1.1.1/32     |       2.2.2.2 |             |
      |98::1/128                  10.10.10.10/32          98::1/128 |

##### PE1 config

    logical-routers 6pepe1 {
        routing-options {
            autonomous-system 3000;
        }
        interfaces {
            ge-1/2/1 {
                unit 1501 {
                    vlan-id 1501;
                    family inet {
                        address 192.168.0.1/30;
                    }
                    family inet6;
                    family mpls;
                }
            }
            ge-1/2/1 {
                unit 1503 {
                    description "PE1 to CE1 IPV6 Customer";
                    vlan-id 1503;
                    family inet6 {
                        address 10::1/126;
                    }
                }
            }
            lo0 {
                unit 1501 {
                    family inet {
                        address 1.1.1.1/32;
                    }
                }
            }
        }
        protocols {
            bgp {
                group ibgp {
                    type internal;
                    local-address 1.1.1.1;
                    family inet6 {
                        labeled-unicast {       #<------
                            explicit-null;      #<------
                        }
                    }
                    neighbor 2.2.2.2;
                }
                group ipv6 {
                    family inet6 {
                        unicast;
                    }
                    neighbor 10::1 {
                        peer-as 1000;
                    }
                }
            }
            mpls {
                ipv6-tunneling;         #<------
                label-switched-path pe1-to-pe2 {
                    to 2.2.2.2;
                }
                interface ge-1/2/1.1501;
            }
        }
    }

##### PE2 config

    logical-systems 6pepe2 {                   
        routing-options {
            autonomous-system 3000;
        }
        interfaces {                    
            ge-1/2/1 {
                unit 1504 {
                    vlan-id 1504;
                    family inet6 {
                        address 11::1/126;
                    }
                }
            }
            ge-1/2/1 {
                unit 1502 {
                    vlan-id 1502;
                    family inet {
                        address 192.168.0.6/30;
                    }
                    family inet6;
                    family mpls;
                }
            }
            lo0 {
                unit 1502 {
                    family inet {
                        address 2.2.2.2/32;
                    }
                }
            }
        }
        protocols {
            mpls {
                ipv6-tunneling;
                label-switched-path pe2-to-pe1 {
                    to 1.1.1.1;
                }
                interface ge-1/2/1.1502;
            }
            bgp {
                group ipv6 {
                    traceoptions {
                        file debug-ipv6;
                        flag all detail;
                    }
                    neighbor 11::2 {
                        peer-as 2000;
                    }
                }
                group ibgp {
                    type internal;
                    local-address 2.2.2.2;
                    family inet6 {
                        labeled-unicast {
                            explicit-null;
                        }
                    }
                    neighbor 1.1.1.1;
                }
            }
        }
    }


##### resources

* [6PE](http://tools.ietf.org/html/rfc4798)
* [reserved IPv6 Explicit NULL Label](http://tools.ietf.org/html/rfc3032)
* [ipv6-tunnel](http://www.juniper.net/techpubs/en_US/junos13.1/topics/reference/configuration-statement/ipv6-tunneling-edit-protocols-mpls.html)
* [vedio](http://www.youtube.com/watch?v=zraAfs3bY5E)
* [example](http://www.juniper.net/techpubs/en_US//junos/topics/example/mpls-tunneling-ipv6-over-mpls-ipv4.html)

##### family inet6 `labeled-unicast` vs `unicast`

    delete logical-systems lr1 protocols bgp group to-rr family inet6 unicast
    delete logical-systems lr2 protocols bgp group to-rr family inet6 unicast
    delete logical-systems lr3 protocols bgp group to-rr family inet6 unicast
    delete logical-systems lr4 protocols bgp group to-rr family inet6 unicast
    delete logical-systems lr5 protocols bgp group rr family inet6 unicast
    delete logical-systems lr6 protocols bgp group rr family inet6 unicast
    delete logical-systems lr7 protocols bgp group to-rr family inet6 unicast
    delete logical-systems lr8 protocols bgp group to-rr family inet6 unicast
    set logical-systems lr1 protocols bgp group to-rr family inet6 labeled-unicast explicit-null
    set logical-systems lr2 protocols bgp group to-rr family inet6 labeled-unicast explicit-null
    set logical-systems lr3 protocols bgp group to-rr family inet6 labeled-unicast explicit-null
    set logical-systems lr4 protocols bgp group to-rr family inet6 labeled-unicast explicit-null
    set logical-systems lr5 protocols bgp group rr family inet6 labeled-unicast explicit-null
    set logical-systems lr6 protocols bgp group rr family inet6 labeled-unicast explicit-null
    set logical-systems lr7 protocols bgp group to-rr family inet6 labeled-unicast explicit-null
    set logical-systems lr8 protocols bgp group to-rr family inet6 labeled-unicast explicit-null

### rtbh


#### initial routes


    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet.0 33.33.33.33/32           

    inet.0: 67 destinations, 76 routes (67 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    33.33.33.33/32     *[BGP/170] 01:05:50, localpref 100, from 10.10.1.5
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                        [BGP/170] 01:05:48, localpref 100, from 10.10.1.6
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet.0 33.33.33.33/32 detail       

    inet.0: 67 destinations, 76 routes (67 active, 0 holddown, 0 hidden)
    Restart Complete
    33.33.33.33/32 (2 entries, 1 announced)
            *BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2826c00
                    Next-hop reference count: 16
                    Source: 10.10.1.5
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: 10.10.1.1
                    Indirect next hop: 2a2c740 1048600
                    State: <Active Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:06:28    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.5+179
                    Announcement bits (4): 2-KRT 5-Aggregate 6-BGP_RT_Background 7-Resolve tree 4 
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000      <------
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.5
             BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2826c00
                    Next-hop reference count: 16
                    Source: 10.10.1.6
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: 10.10.1.1
                    Indirect next hop: 2a2c740 1048600
                    State: <NotBest Int Ext>
                    Inactive reason: Not Best in its group - Update source
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:06:26    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.6+179
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000      <------
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.6

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet.0 3.3.3.0/24                         

    inet.0: 67 destinations, 76 routes (67 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    3.3.3.0/24         *[BGP/170] 01:07:39, localpref 100, from 10.10.1.5
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                        [BGP/170] 01:07:37, localpref 100, from 10.10.1.6
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet.0 3.3.3.0/24 detail 

    inet.0: 67 destinations, 76 routes (67 active, 0 holddown, 0 hidden)
    Restart Complete
    3.3.3.0/24 (2 entries, 1 announced)
            *BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2826c00
                    Next-hop reference count: 16
                    Source: 10.10.1.5
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: 10.10.1.1
                    Indirect next hop: 2a2c740 1048600
                    State: <Active Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:07:42    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.5+179
                    Announcement bits (4): 2-KRT 5-Aggregate 6-BGP_RT_Background 7-Resolve tree 4 
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.5
             BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2826c00
                    Next-hop reference count: 16
                    Source: 10.10.1.6
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: 10.10.1.1
                    Indirect next hop: 2a2c740 1048600
                    State: <NotBest Int Ext>
                    Inactive reason: Not Best in its group - Update source
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:07:40    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.6+179
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.6


    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet6.0 ::3.3.3.0/126       

    inet6.0: 26 destinations, 37 routes (26 active, 0 holddown, 3 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::3.3.3.0/126      *[BGP/170] 01:08:32, localpref 100, from 10.10.1.5
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                        [BGP/170] 01:08:28, localpref 100, from 10.10.1.6
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

    inet6.0: 26 destinations, 37 routes (26 active, 0 holddown, 3 hidden)
    Restart Complete
    ::3.3.3.0/126 (2 entries, 1 announced)
            *BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2824730
                    Next-hop reference count: 12
                    Source: 10.10.1.5
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: ::ffff:10.10.1.1
                    Indirect next hop: 28507e0 1048639
                    State: <Active Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:08:39    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.5+179
                    Announcement bits (3): 0-KRT 3-BGP_RT_Background 4-Resolve tree 5 
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000      <------
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.5
             BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2824730
                    Next-hop reference count: 12
                    Source: 10.10.1.6
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: ::ffff:10.10.1.1
                    Indirect next hop: 28507e0 1048639
                    State: <NotBest Int Ext>
                    Inactive reason: Not Best in its group - Update source
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:08:35    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.6+179
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000      <------
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.6

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet6.0 ::33.33.33.33/128       

    inet6.0: 26 destinations, 37 routes (26 active, 0 holddown, 3 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::33.33.33.33/128  *[BGP/170] 01:08:54, localpref 100, from 10.10.1.5
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                        [BGP/170] 01:08:50, localpref 100, from 10.10.1.6
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet6.0 ::33.33.33.33/128 detail  

    inet6.0: 26 destinations, 37 routes (26 active, 0 holddown, 3 hidden)
    Restart Complete
    ::33.33.33.33/128 (2 entries, 1 announced)
            *BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2824730
                    Next-hop reference count: 12
                    Source: 10.10.1.5
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: ::ffff:10.10.1.1
                    Indirect next hop: 28507e0 1048639
                    State: <Active Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:09:00    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.5+179
                    Announcement bits (3): 0-KRT 3-BGP_RT_Background 4-Resolve tree 5 
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000      <------
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.5
             BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2824730
                    Next-hop reference count: 12
                    Source: 10.10.1.6
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: ::ffff:10.10.1.1
                    Indirect next hop: 28507e0 1048639
                    State: <NotBest Int Ext>
                    Inactive reason: Not Best in its group - Update source
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:08:56    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.6+179
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000      <------
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.6

#### config

    set logical-systems lr2 policy-options community rtbh members [ 65412:100 target:4012345678L:2000 ] 
    set logical-systems lr2 policy-options policy-statement imp-bgp-rtbh term 1 from protocol bgp community rtbh route-filter 0/0 prefix-length-range /32-/32
    set logical-systems lr2 policy-options policy-statement imp-bgp-rtbh term 1 then next-hop discard                                                                        
    set logical-systems lr2 policy-options policy-statement imp-bgp-rtbh term 1 then accept              
    set logical-systems lr2 policy-options policy-statement imp-bgp-rtbh term 2 from protocol bgp community rtbh route-filter ::0/0 prefix-length-range /128-/128 
    set logical-systems lr2 policy-options policy-statement imp-bgp-rtbh term 2 then next-hop discard                                                                        
    set logical-systems lr2 policy-options policy-statement imp-bgp-rtbh term 2 then accept              
    set logical-systems lr2 policy-options policy-statement imp-bgp-rtbh term 3 from protocol bgp community rtbh 
    set logical-systems lr2 policy-options policy-statement imp-bgp-rtbh term 3 then community delete rtbh          

    set logical-systems lr3 policy-options community rtbh members [ 65412:100 target:4012345678L:2000 ] 
    set logical-systems lr3 policy-options policy-statement imp-bgp-rtbh term 1 from protocol bgp community rtbh route-filter 0/0 prefix-length-range /32-/32
    set logical-systems lr3 policy-options policy-statement imp-bgp-rtbh term 1 then next-hop discard                                                                        
    set logical-systems lr3 policy-options policy-statement imp-bgp-rtbh term 1 then accept              
    set logical-systems lr3 policy-options policy-statement imp-bgp-rtbh term 2 from protocol bgp community rtbh route-filter ::0/0 prefix-length-range /128-/128 
    set logical-systems lr3 policy-options policy-statement imp-bgp-rtbh term 2 then next-hop discard                                                                        
    set logical-systems lr3 policy-options policy-statement imp-bgp-rtbh term 2 then accept              
    set logical-systems lr3 policy-options policy-statement imp-bgp-rtbh term 3 from protocol bgp community rtbh 
    set logical-systems lr3 policy-options policy-statement imp-bgp-rtbh term 3 then community delete rtbh          

    set logical-systems lr5 policy-options community rtbh members [ 65412:100 target:4012345678L:2000 ] 
    set logical-systems lr5 policy-options policy-statement imp-bgp-rtbh term 1 from protocol bgp community rtbh route-filter 0/0 prefix-length-range /32-/32
    set logical-systems lr5 policy-options policy-statement imp-bgp-rtbh term 1 then next-hop discard                                                                        
    set logical-systems lr5 policy-options policy-statement imp-bgp-rtbh term 1 then accept              
    set logical-systems lr5 policy-options policy-statement imp-bgp-rtbh term 2 from protocol bgp community rtbh route-filter ::0/0 prefix-length-range /128-/128 
    set logical-systems lr5 policy-options policy-statement imp-bgp-rtbh term 2 then next-hop discard                                                                        
    set logical-systems lr5 policy-options policy-statement imp-bgp-rtbh term 2 then accept              
    set logical-systems lr5 policy-options policy-statement imp-bgp-rtbh term 3 from protocol bgp community rtbh 
    set logical-systems lr5 policy-options policy-statement imp-bgp-rtbh term 3 then community delete rtbh          




#### result


    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet.0 3.3.3.0/24                         

    inet.0: 67 destinations, 76 routes (67 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    3.3.3.0/24         *[BGP/170] 01:13:15, localpref 100, from 10.10.1.5
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                        [BGP/170] 01:13:13, localpref 100, from 10.10.1.6
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet.0 3.3.3.0/24 detail  

    inet.0: 67 destinations, 76 routes (67 active, 0 holddown, 0 hidden)
    Restart Complete
    3.3.3.0/24 (2 entries, 1 announced)
            *BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2826c00
                    Next-hop reference count: 12
                    Source: 10.10.1.5
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: 10.10.1.1
                    Indirect next hop: 2a2c740 1048600
                    State: <Active Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:13:22    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.5+179
                    Announcement bits (4): 2-KRT 5-Aggregate 6-BGP_RT_Background 7-Resolve tree 4 
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.5
             BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2826c00
                    Next-hop reference count: 12
                    Source: 10.10.1.6
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: 10.10.1.1
                    Indirect next hop: 2a2c740 1048600
                    State: <NotBest Int Ext>
                    Inactive reason: Not Best in its group - Update source
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:13:20    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.6+179
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.6

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet6.0 ::33.33.33.33/128           

    inet6.0: 26 destinations, 37 routes (26 active, 0 holddown, 3 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::33.33.33.33/128  *[BGP/170] 01:13:11, localpref 100, from 10.10.1.5
                          AS path: 300 I
                          Discard
                        [BGP/170] 01:13:07, localpref 100, from 10.10.1.6
                          AS path: 300 I
                          Discard

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet6.0 ::33.33.33.33/128 detail  

    inet6.0: 26 destinations, 37 routes (26 active, 0 holddown, 3 hidden)
    Restart Complete
    ::33.33.33.33/128 (2 entries, 1 announced)
            *BGP    Preference: 170/-101
                    Next hop type: Discard
                    Address: 0x23f36e8
                    Next-hop reference count: 8
                    State: <Active Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:13:17 
                    Task: BGP_4012345678.10.10.1.5+179
                    Announcement bits (3): 0-KRT 3-BGP_RT_Background 4-Resolve tree 5 
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.5
             BGP    Preference: 170/-101
                    Next hop type: Discard
                    Address: 0x23f36e8
                    Next-hop reference count: 8
                    State: <NotBest Int Ext>
                    Inactive reason: Not Best in its group - Update source
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:13:13 
                    Task: BGP_4012345678.10.10.1.6+179
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.6

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet6.0 ::3.3.3.0/126               

    inet6.0: 26 destinations, 37 routes (26 active, 0 holddown, 3 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::3.3.3.0/126      *[BGP/170] 01:13:28, localpref 100, from 10.10.1.5
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                        [BGP/170] 01:13:24, localpref 100, from 10.10.1.6
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet6.0 ::3.3.3.0/126 detail        

    inet6.0: 26 destinations, 37 routes (26 active, 0 holddown, 3 hidden)
    Restart Complete
    ::3.3.3.0/126 (2 entries, 1 announced)
            *BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2824730
                    Next-hop reference count: 8
                    Source: 10.10.1.5
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: ::ffff:10.10.1.1
                    Indirect next hop: 28507e0 1048639
                    State: <Active Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:13:34    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.5+179
                    Announcement bits (3): 0-KRT 3-BGP_RT_Background 4-Resolve tree 5 
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.5
             BGP    Preference: 170/-101
                    Next hop type: Indirect
                    Address: 0x2824730
                    Next-hop reference count: 8
                    Source: 10.10.1.6
                    Next hop type: Router, Next hop index: 2363
                    Next hop: 10.10.12.1 via ge-1/2/2.12 weight 0x1, selected
                    Label-switched-path r2-r1
                    Protocol next hop: ::ffff:10.10.1.1
                    Indirect next hop: 28507e0 1048639
                    State: <NotBest Int Ext>
                    Inactive reason: Not Best in its group - Update source
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:13:30    Metric2: 5 
                    Task: BGP_4012345678.10.10.1.6+179
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.6

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet6.0 ::33.33.33.33/128           

    inet6.0: 26 destinations, 37 routes (26 active, 0 holddown, 3 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::33.33.33.33/128  *[BGP/170] 01:13:42, localpref 100, from 10.10.1.5
                          AS path: 300 I
                          Discard
                        [BGP/170] 01:13:38, localpref 100, from 10.10.1.6
                          AS path: 300 I
                          Discard

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet6.0 ::33.33.33.33/128 detail  

    inet6.0: 26 destinations, 37 routes (26 active, 0 holddown, 3 hidden)
    Restart Complete
    ::33.33.33.33/128 (2 entries, 1 announced)
            *BGP    Preference: 170/-101
                    Next hop type: Discard
                    Address: 0x23f36e8
                    Next-hop reference count: 8
                    State: <Active Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:13:44 
                    Task: BGP_4012345678.10.10.1.5+179
                    Announcement bits (3): 0-KRT 3-BGP_RT_Background 4-Resolve tree 5 
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.5
             BGP    Preference: 170/-101
                    Next hop type: Discard
                    Address: 0x23f36e8
                    Next-hop reference count: 8
                    State: <NotBest Int Ext>
                    Inactive reason: Not Best in its group - Update source
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:13:40 
                    Task: BGP_4012345678.10.10.1.6+179
                    AS path: 300 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.1
                    Communities: 65412:100 target:4012345678L:2000
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.6


### ipv6 lo0 aggr

#### QUESTION:

R2/R3 don't have R7/8 host in inet6.3 =>
any routes adv.ed by R7/8 will be hidden in R2/3


solution: 
1) install routes in R2/3       not allowed
2) set next-hop self in R5/6       may not optimal routes



## VPN

### basic interconnections

#### results

R1:

    lab@MX80-NGGWR-01# run show route logical-system lr1 table GREEN.inet.0          

    GREEN.inet.0: 11 destinations, 28 routes (11 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    1.1.1.1/32         *[Direct/0] 3d 13:40:48
                        > via lo0.11
                        [BGP/170] 2d 19:15:40, MED 52, localpref 100, from 10.10.1.2
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 2d 19:15:40, MED 52, localpref 100, from 10.10.1.3
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    4.4.4.4/32         *[OSPF/10] 2d 19:15:40, metric 52
                        > to 20.20.19.1 via ge-1/2/1.691
                        [BGP/170] 2d 20:00:30, localpref 100, from 10.10.1.2
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 2d 20:00:30, localpref 100, from 10.10.1.3
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.1.11/32      *[OSPF/150] 2d 19:15:45, metric 0, tag 0
                        > to 20.20.19.1 via ge-1/2/1.691
                        [BGP/170] 2d 19:15:40, MED 0, localpref 100, from 10.10.1.2
                          AS path: I, validation-state: unverified
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 2d 19:15:40, MED 0, localpref 100, from 10.10.1.3
                          AS path: I, validation-state: unverified
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.1.22/32      *[OSPF/150] 2d 19:15:40, metric 0, tag 0
                        > to 20.20.19.1 via ge-1/2/1.691
                        [BGP/170] 2d 19:15:45, MED 0, localpref 100, from 10.10.1.2
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 2d 19:15:45, MED 0, localpref 100, from 10.10.1.3
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.1.33/32      *[OSPF/150] 05:21:45, metric 0, tag 103
                        > to 20.20.19.1 via ge-1/2/1.691
                        [BGP/170] 05:21:50, localpref 100, from 10.10.1.2
                          AS path: 65000 I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 05:21:50, localpref 100, from 10.10.1.3
                          AS path: 65000 I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.19.0/24      *[Direct/0] 3d 13:39:14
                        > via ge-1/2/1.691
                        [BGP/170] 2d 19:15:40, MED 52, localpref 100, from 10.10.1.2
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 2d 19:15:40, MED 52, localpref 100, from 10.10.1.3
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.19.2/32      *[Local/0] 3d 13:39:23
                          Local via ge-1/2/1.691
    20.20.42.0/24      *[OSPF/10] 2d 19:15:40, metric 52
                        > to 20.20.19.1 via ge-1/2/1.691
                        [BGP/170] 3d 02:19:17, localpref 100, from 10.10.1.2
                          AS path: I, validation-state: unverified
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 3d 11:37:33, localpref 100, from 10.10.1.3
                          AS path: I, validation-state: unverified
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.100.0/31     *[BGP/170] 3d 02:19:17, localpref 100, from 10.10.1.2
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 3d 11:37:33, localpref 100, from 10.10.1.3
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.120.0/24     *[OSPF/10] 2d 19:15:45, metric 51
                        > to 20.20.19.1 via ge-1/2/1.691
                        [BGP/170] 2d 19:15:45, MED 51, localpref 100, from 10.10.1.2
                          AS path: I, validation-state: unverified
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 2d 19:15:45, MED 51, localpref 100, from 10.10.1.3
                          AS path: I, validation-state: unverified
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    224.0.0.5/32       *[OSPF/10] 3d 13:41:03, metric 1
                          MultiRecv
                          
#### issue: no CE4/5 routes


#### check routes in RR

no CE4/5 routes:

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr2 table bgp.l3vpn.0     
     
    bgp.l3vpn.0: 20 destinations, 20 routes (16 active, 0 holddown, 4 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    10.10.1.1:1:1.1.1.1/32                
                       *[BGP/170] 3d 02:22:31, localpref 100, from 10.10.1.1
                          AS path: I, validation-state: unverified
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    10.10.1.1:1:4.4.4.4/32                
                       *[BGP/170] 2d 19:18:54, MED 52, localpref 100, from 10.10.1.1
                          AS path: I, validation-state: unverified
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    10.10.1.1:1:20.20.1.11/32                
                       *[BGP/170] 2d 19:18:59, MED 0, localpref 100, from 10.10.1.1
                          AS path: I, validation-state: unverified
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    10.10.1.1:1:20.20.1.22/32                
                       *[BGP/170] 2d 19:18:54, MED 0, localpref 100, from 10.10.1.1
                          AS path: I, validation-state: unverified
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    10.10.1.1:1:20.20.19.0/24                
                       *[BGP/170] 3d 02:22:31, localpref 100, from 10.10.1.1
                          AS path: I, validation-state: unverified
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    10.10.1.1:1:20.20.42.0/24                
                       *[BGP/170] 2d 19:18:54, MED 52, localpref 100, from 10.10.1.1
                          AS path: I, validation-state: unverified
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    10.10.1.1:1:20.20.120.0/24                
                       *[BGP/170] 2d 19:18:59, MED 51, localpref 100, from 10.10.1.1
                          AS path: I, validation-state: unverified
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    10.10.1.4:1:1.1.1.1/32                
                       *[BGP/170] 2d 19:18:54, MED 52, localpref 100, from 10.10.1.4
                          AS path: I, validation-state: unverified
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.4:1:4.4.4.4/32                
                       *[BGP/170] 2d 20:03:44, localpref 100, from 10.10.1.4
                          AS path: I, validation-state: unverified
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.4:1:20.20.1.11/32                
                       *[BGP/170] 2d 19:18:54, MED 0, localpref 100, from 10.10.1.4
                          AS path: I, validation-state: unverified
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.4:1:20.20.1.22/32                
                       *[BGP/170] 2d 19:18:59, MED 0, localpref 100, from 10.10.1.4
                          AS path: I, validation-state: unverified
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.4:1:20.20.1.33/32                
                       *[BGP/170] 05:25:04, localpref 100, from 10.10.1.4
                          AS path: 65000 I, validation-state: unverified
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.4:1:20.20.19.0/24                
                       *[BGP/170] 2d 19:18:54, MED 52, localpref 100, from 10.10.1.4
                          AS path: I, validation-state: unverified
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.4:1:20.20.42.0/24                
                       *[BGP/170] 3d 02:22:31, localpref 100, from 10.10.1.4
                          AS path: I, validation-state: unverified
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.4:1:20.20.100.0/31                
                       *[BGP/170] 3d 02:22:31, localpref 100, from 10.10.1.4
                          AS path: I, validation-state: unverified
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.4:1:20.20.120.0/24                
                       *[BGP/170] 2d 19:18:59, MED 51, localpref 100, from 10.10.1.4
                          AS path: I, validation-state: unverified
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
                        
check RR bgp.l3vpn.0 =>  CE4/5 route in "hidden":

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lr2 table bgp.l3vpn.0 all 20.20.1.44/32 extensive  

    bgp.l3vpn.0: 20 destinations, 20 routes (16 active, 0 holddown, 4 hidden)
    Restart Complete
    10.10.1.8:1:20.20.1.44/32 (1 entry, 0 announced)
             BGP    Preference: 170/-101
                    Route Distinguisher: 10.10.1.8:1
                    Next hop type: Unusable
                    Address: 0x244ce94
                    Next-hop reference count: 6
                    State: <Hidden Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 2d 18:40:04 
                    Validation State: unverified 
                    Task: BGP_4012345678.10.10.1.8+57274
                    AS path: 65000 I
                    Communities: 65000:4 target:2:65000
                    Accepted
                    VPN Label: 16
                    Localpref: 100
                    Router ID: 10.10.1.8
                    Indirect next hops: 1
                            Protocol next hop: 10.10.1.8
                            Push 16
                            Indirect next hop: 0 - INH Session ID: 0x0
                          
reason is no next hop resolvation, => check inet.3. 

    lab@MX80-NGGWR-01# run show route logical-system lr2 table inet.3                                     

    inet.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    10.10.1.1/32       *[RSVP/7/1] 3d 13:52:24, metric 5
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    10.10.1.3/32       *[RSVP/7/1] 3d 13:52:23, metric 5
                        > to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
    10.10.1.4/32       *[RSVP/7/1] 3d 13:52:22, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    10.10.1.5/32       *[RSVP/7/1] 3d 13:52:24, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
    10.10.1.6/32       *[RSVP/7/1] 3d 13:52:23, metric 5
                        > to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
                        
no LSP to R8. that's the issue.
solution:
   1) create LSP
   2) install host routes
   3) adv inactive (inactive = hidden ?)
   4) ?
   
 
#### solution (non-work):adv-inactive in RR

doesn't work


#### solution: install R8 in R2/R3 lsp


    lab@MX80-NGGWR-01# show | compare  
    [edit logical-systems lr2 protocols mpls label-switched-path r2-r6]
    !       active: install 10.10.1.8/32 { ... }
    [edit]
    lab@MX80-NGGWR-01# commit  

 
    [edit]
    lab@MX80-NGGWR-01# run show route advertising-protocol bgp 10.10.1.1 logical-system lr2                    

    bgp.l3vpn.0: 20 destinations, 20 routes (20 active, 0 holddown, 0 hidden)
    Restart Complete
      Prefix                  Nexthop              MED     Lclpref    AS path
      10.10.1.4:1:1.1.1.1/32                    
    *                         10.10.1.4            52      100        I
      10.10.1.4:1:4.4.4.4/32                    
    *                         10.10.1.4                    100        I
      10.10.1.4:1:20.20.1.11/32                    
    *                         10.10.1.4            0       100        I
      10.10.1.4:1:20.20.1.22/32                    
    *                         10.10.1.4            0       100        I
      10.10.1.4:1:20.20.1.33/32                    
    *                         10.10.1.4                    100        65000 I
      10.10.1.4:1:20.20.19.0/24                    
    *                         10.10.1.4            52      100        I
      10.10.1.4:1:20.20.42.0/24                    
    *                         10.10.1.4                    100        I
      10.10.1.4:1:20.20.100.0/31                    
    *                         10.10.1.4                    100        I
      10.10.1.4:1:20.20.120.0/24                    
    *                         10.10.1.4            51      100        I
      10.10.1.8:1:20.20.1.44/32                                         #<------
    *                         10.10.1.8                    100        65000 I
      10.10.1.8:1:20.20.1.55/32                    
    *                         10.10.1.8                    100        65000 I
      10.10.1.8:1:20.20.150.0/31                    
    *                         10.10.1.8                    100        I
      10.10.1.8:1:20.20.200.0/31                    
    *                         10.10.1.8                    100        I
    
    
### backdoor routes and sham-link

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system lce table green-ce1.inet.0 

    green-ce1.inet.0: 16 destinations, 17 routes (16 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    1.1.1.1/32         *[OSPF/10] 2d 19:49:33, metric 1
                        > to 20.20.19.2 via ge-1/2/2.691
    4.4.4.4/32         *[OSPF/10] 2d 19:49:23, metric 51
                        > to 20.20.120.1 via ge-1/2/2.120
    20.20.1.11/32      *[Direct/0] 2d 19:49:39
                        > via ge-1/2/2.4001
                        [Local/0] 2d 19:49:39
                          Local via ge-1/2/2.4001
    20.20.1.22/32      *[OSPF/150] 2d 19:49:23, metric 0, tag 0         #<------
                        > to 20.20.120.1 via ge-1/2/2.120
    20.20.1.33/32      *[OSPF/150] 05:55:33, metric 0, tag 103          #<------
                        > to 20.20.120.1 via ge-1/2/2.120
    20.20.1.44/32      *[OSPF/150] 00:06:30, metric 0, tag 3489696078   #<------
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.1.55/32      *[OSPF/150] 00:06:30, metric 0, tag 3489696078   #<------
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.19.0/24      *[Direct/0] 3d 14:13:02
                        > via ge-1/2/2.691
    20.20.19.1/32      *[Local/0] 3d 14:13:14
                          Local via ge-1/2/2.691
    20.20.42.0/24      *[OSPF/10] 2d 19:49:23, metric 51
                        > to 20.20.120.1 via ge-1/2/2.120
    20.20.100.0/31     *[OSPF/150] 05:45:57, metric 0, tag 3489696078
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.120.0/24     *[Direct/0] 3d 14:13:02
                        > via ge-1/2/2.120
    20.20.120.2/32     *[Local/0] 3d 14:13:12
                          Local via ge-1/2/2.120
    20.20.150.0/31     *[OSPF/150] 00:06:30, metric 0, tag 3489696078
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.200.0/31     *[OSPF/150] 00:06:30, metric 0, tag 3489696078
                        > to 20.20.19.2 via ge-1/2/2.691
    224.0.0.5/32       *[OSPF/10] 3d 14:14:52, metric 1
                          MultiRecv


vpn route prefer the backdoor exit, need to fix it with shamlink



#### solution:sham-link

    lab@MX80-NGGWR-01# show | compare  
    [edit logical-systems lr1 routing-instances GREEN protocols ospf]
    +       sham-link local 1.1.1.1;
    [edit logical-systems lr1 routing-instances GREEN protocols ospf area 0.0.0.0]
    +        sham-link-remote 4.4.4.4;

    lab@MX80-NGGWR-01# show | compare  
    [edit logical-systems lr4 routing-instances GREEN protocols ospf]
    +       sham-link local 4.4.4.4;
    [edit logical-systems lr4 routing-instances GREEN protocols ospf area 0.0.0.0]
    +        sham-link-remote 1.1.1.1;


    [edit]
    lab@MX80-NGGWR-01# run show ospf neighbor logical-system lr1 instance all    
    Instance: GREEN
    Address          Interface              State     ID               Pri  Dead
    20.20.19.1       ge-1/2/1.691           Full      20.20.1.11       128    38
    4.4.4.4          shamlink.0             Full      4.4.4.4            0    38
    
now the ce1 prefer backbone instead of backdoor:
    
    lab@MX80-NGGWR-01# run show route logical-system lce table green-ce1.inet.0 
     
    green-ce1.inet.0: 16 destinations, 17 routes (16 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    1.1.1.1/32         *[OSPF/150] 00:06:03, metric 0, tag 3489696078
                        > to 20.20.19.2 via ge-1/2/2.691
    4.4.4.4/32         *[OSPF/150] 00:06:13, metric 0, tag 3489696078
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.1.11/32      *[Direct/0] 2d 20:24:38
                        > via ge-1/2/2.4001
                        [Local/0] 2d 20:24:38
                          Local via ge-1/2/2.4001
    20.20.1.22/32      *[OSPF/150] 00:06:03, metric 0, tag 0    #<------
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.1.33/32      *[OSPF/150] 00:06:03, metric 0, tag 103  #<------
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.1.44/32      *[OSPF/150] 00:41:29, metric 0, tag 3489696078
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.1.55/32      *[OSPF/150] 00:41:29, metric 0, tag 3489696078
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.19.0/24      *[Direct/0] 3d 14:48:01
                        > via ge-1/2/2.691
    20.20.19.1/32      *[Local/0] 3d 14:48:13
                          Local via ge-1/2/2.691
    20.20.42.0/24      *[OSPF/10] 00:06:03, metric 3
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.100.0/31     *[OSPF/150] 06:20:56, metric 0, tag 3489696078
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.120.0/24     *[Direct/0] 3d 14:48:01
                        > via ge-1/2/2.120
    20.20.120.2/32     *[Local/0] 3d 14:48:11
                          Local via ge-1/2/2.120
    20.20.150.0/31     *[OSPF/150] 00:41:29, metric 0, tag 3489696078
                        > to 20.20.19.2 via ge-1/2/2.691
    20.20.200.0/31     *[OSPF/150] 00:41:29, metric 0, tag 3489696078
                        > to 20.20.19.2 via ge-1/2/2.691
    224.0.0.5/32       *[OSPF/10] 3d 14:49:51, metric 1
                          MultiRecv

#### TIP: sham-link

by default all type5 LSA

    ce1--------vrf1:pe1-----------//-----------PE2:vrf2----------ce2
       (OSPF)          (MP-BGP)                 (OSPF)
              <-------                         <------
           type5


sham-link: (benefit over domain-id ?)

                 sham-link(unnumbered lo i/f)
                ....................<.................
                .                                    .
                v                                    A
                .                                    .
    ce1--------vrf1:pe1-----------//-----------PE2:vrf2----------ce2
       (OSPF)          (MP-BGP)                 (OSPF)
              <-------                         <------
           type5

routes learned via sham-link , but spf won't install them (why?)

<http://www.cisco.com/en/US/docs/ios-xml/ios/iproute_ospf/configuration/15-sy/iro-sham-link.html#GUID-45F321D9-7482-447A-B642-01ADC624A4F7>

Before you create a sham-link between PE routers in an MPLS VPN, you must:

Configure a separate /32 address on the remote PE so that OSPF packets can be
sent over the VPN backbone to the remote end of the sham-link. The /32 address
must meet the following criteria:

1. Belong to a VRF.
1. Not be advertised by OSPF.
1. Be advertised by BGP.
1. You can use the /32 address for other sham-links.

Associate the sham-link with an existing OSPF area.

seem no need 2 in my case:

    lab@MX80-NGGWR-01# show logical-systems lr1 routing-instances GREEN            
    instance-type vrf;
    interface ge-1/2/1.691;
    interface lo0.11;
    route-distinguisher 10.10.1.1:1;
    vrf-import vrf-imp;
    vrf-export vrf-exp;
    vrf-table-label;
    protocols {
        ospf {
            export exp-ospf-ce1;
            sham-link local 1.1.1.1;
            area 0.0.0.0 {
                sham-link-remote 4.4.4.4;
                interface ge-1/2/1.691;
                interface all;
                interface lo0.11;
            }
        }
    }
    
but, the router seems to be able to handle this automatically:

before sham-link up:

    lab@MX80-NGGWR-01# run show route logical-system lr1 table GREEN 4.4.4.4/32 

    GREEN.inet.0: 15 destinations, 34 routes (15 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    4.4.4.4/32         *[OSPF/10] 2d 20:04:12, metric 52        #<------
                        > to 20.20.19.1 via ge-1/2/1.691
                        [BGP/170] 2d 20:49:02, localpref 100, from 10.10.1.2
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 2d 20:49:02, localpref 100, from 10.10.1.3
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green

but after sham-link up:

    lab@MX80-NGGWR-01# run show route logical-system lr1 table GREEN 4.4.4.4/32    

    GREEN.inet.0: 15 destinations, 29 routes (15 active, 0 holddown, 3 hidden)
    + = Active Route, - = Last Active, * = Both

    4.4.4.4/32         *[BGP/170] 2d 21:07:49, localpref 100, from 10.10.1.2
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 2d 21:07:49, localpref 100, from 10.10.1.3
                          AS path: I, validation-state: unverified
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
 
 
 
#### TIP: domain-id
    
    determine type3(same) vs type5(diff)
    make it unique at all PE routers to ensure that the Type 3 summary LSAs, which
    advertise the CE router’s loopback address, are correctly distributed to the remote PE as an
    AS external (LSA Type 5). When no domain ID is configured, or when the configured value
    matches, network summary LSAs are distributed to the remote CE as a network summary

### TIP: traceroute under mpls vpn

* [how traceroute works](http://forums.juniper.net/t5/Routing/what-does-quot-icmp-tunneling-quot-mean-in-mpls-vpn/td-p/164284)
* icmp-tunnel

### TIP: vrf-table-lable vs. tunneled-interface

LSI: LSP sub i/f abstract
enable the knob => create 1 LSI for this vrf => assign lable to LSI (1024-2048)

    RE1                              PE2
                                      | VRF1                        
                         label1 ------|---- LSI1 
                                      | VRF2
                         label2 ------|---- LSI2 
                                      | VRF3     
                         label3 ------|---- LSI3 
                                      |
vrf-table-label:

* Uses LSP sub-interface abstract 
* Creates an LSI that maps to each VRF table
* Supported core-facing interfaces map reserved MPLS labels to each VRF LSI Caveats:
    Only supported on limited interface types
    Not supported for MP-BGP-labeled routes (interprovider and carrier-of-carrier VPNs)
                        
VPN tunnel interface :

* Requires a tunnel services PIC
* Causes Internet Processor II lookups on the Egress PE
* Rather than forward the packet directly out the physical VRF interface, the
  resulting IP packet from the first lookup is sent to the tunnel service
  interface (next hop equals the vt-x/y/z interface)                        

### VPN Internet access

#### solution 1

##### solution1 config

    #R1 global add static route summarizing all vpn routes, pointing intoto vrf
    set logical-systems r1 routing-options static route 20.20.0.0/16 next-table GREEN.inet.0

    #then adv to all internet via bgp
    set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 from protocol static
    set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 from route-filter 20.20.0.0/16 exact
    set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 then next-hop self
    set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 then accept
    
    set logical-systems r1 protocols bgp group to-rr export exp-bgp-vpn-agg
    set logical-systems r1 protocols bgp group c3 export exp-bgp-vpn-agg

    #R1 vrf adv a default route to CE1 
    set logical-systems r1 routing-instances GREEN routing-options aggregate route 0.0.0.0/0

    set logical-systems r1 policy-options policy-statement exp-ospf-default term 1 from protocol aggregate
    set logical-systems r1 policy-options policy-statement exp-ospf-default term 1 from route-filter 0.0.0.0/0 exact
    set logical-systems r1 policy-options policy-statement exp-ospf-default term 1 then accept
    
    set logical-systems r1 routing-instances GREEN protocols ospf export exp-ospf-default
    
    #R1 vrf also need to adv the default route to all other CE sites
    set logical-systems r1 policy-options policy-statement vrf-exp term 3 from protocol aggregate
    set logical-systems r1 policy-options policy-statement vrf-exp term 3 from route-filter 0.0.0.0/0 exact
    set logical-systems r1 policy-options policy-statement vrf-exp term 3 then community add GREEN
    set logical-systems r1 policy-options policy-statement vrf-exp term 3 then accept
    
    #R1 leak the Internet table(only bgp part in this case, so under BGP) to vrf
    set logical-systems r1 routing-options rib-groups imp-inet.0-to-vrf import-rib inet.0
    set logical-systems r1 routing-options rib-groups imp-inet.0-to-vrf import-rib GREEN.inet.0
    set logical-systems r1 protocols bgp group to-rr family inet unicast rib-group imp-inet.0-to-vrf
    

##### source Internet => R1 : adv aggr. vpn routes from R1
##### R1 => R1:vrf : R1: static route with next table

###### other R got aggr. vpn routes from R1

    lab@MX80-NGGWR-01# run show route logical-system r5 protocol bgp 20.20/16 

    inet.0: 50 destinations, 56 routes (50 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    20.20.0.0/16       *[BGP/170] 00:02:33, localpref 100, from 10.10.1.1
                          AS path: I
                        > to 10.10.25.1 via ge-1/2/2.25, label-switched-path r5-r1


##### R1:vrf => dest CE : current behavior, no need extra config

##### source CE -> R1:vrf : R1:vrf adv a default to CE via ospf

###### ce1 routes after R1:GREEN exp default to ce1 via ospf

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system r0 table green-ce1.inet.0 0/0 exact  

    green-ce1.inet.0: 24 destinations, 25 routes (24 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    0.0.0.0/0          *[OSPF/150] 00:01:57, metric 0, tag 0
                        > to 20.20.19.2 via ge-1/2/2.691

##### same for other CE -> adjacent R:VRF : R1:vrf export the default route to all sites

##### R1:vrf -> R1 -> Internet : R1 leak Internet (means bgp) table into R1 vrf

###### original R1:vrf(GREEN.inet.0) table

    lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN.inet.0  

    GREEN.inet.0: 15 destinations, 29 routes (15 active, 0 holddown, 3 hidden)
    + = Active Route, - = Last Active, * = Both

    1.1.1.1/32         *[Direct/0] 00:17:19
                        > via lo0.11
    4.4.4.4/32         *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:16:58, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.1.11/32      *[OSPF/150] 00:16:23, metric 0, tag 0
                        > to 20.20.19.1 via ge-1/2/1.691
    20.20.1.22/32      *[BGP/170] 00:16:22, MED 0, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:16:22, MED 0, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.1.33/32      *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                          AS path: 65000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:16:58, localpref 100, from 10.10.1.3
                          AS path: 65000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.1.44/32      *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                          AS path: 65000 I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                        [BGP/170] 00:16:56, localpref 100, from 10.10.1.3
                          AS path: 65000 I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
    20.20.1.55/32      *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                          AS path: 65000 I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                        [BGP/170] 00:16:56, localpref 100, from 10.10.1.3
                          AS path: 65000 I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
    20.20.19.0/24      *[Direct/0] 00:17:19
                        > via ge-1/2/1.691
    20.20.19.2/32      *[Local/0] 00:17:19
                          Local via ge-1/2/1.691
    20.20.42.0/24      *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                          AS path: I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:16:58, localpref 100, from 10.10.1.3
                          AS path: I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.100.0/31     *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:16:58, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.120.0/24     *[OSPF/10] 00:16:23, metric 51
                        > to 20.20.19.1 via ge-1/2/1.691
                        [BGP/170] 00:16:22, MED 51, localpref 100, from 10.10.1.2
                          AS path: I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:16:22, MED 51, localpref 100, from 10.10.1.3
                          AS path: I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.150.0/31     *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                        [BGP/170] 00:16:56, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
    20.20.200.0/31     *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                        [BGP/170] 00:16:56, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
    224.0.0.5/32       *[OSPF/10] 00:17:44, metric 1
                          MultiRecv

    [edit]
    lab@MX80-NGGWR-01#  

###### R1:GREEN.inet.0 , after rib-group: R1:inet.0 -> R1:GREEN.inet.0

    lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN.inet.0                                                 

    GREEN.inet.0: 22 destinations, 43 routes (22 active, 0 holddown, 3 hidden)
    + = Active Route, - = Last Active, * = Both

    1.0.0.0/8          *[BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                          AS path: 1001 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
                        [BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                          AS path: 1001 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
    1.1.1.1/32         *[Direct/0] 00:19:50
                        > via lo0.11
    4.4.4.4/32         *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:19:29, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    10.10.0.0/16       *[BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r5
                        [BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                          AS path: I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
    20.20.1.11/32      *[OSPF/150] 00:18:54, metric 0, tag 0
                        > to 20.20.19.1 via ge-1/2/1.691
    20.20.1.22/32      *[BGP/170] 00:18:53, MED 0, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:18:53, MED 0, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.1.33/32      *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                          AS path: 65000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:19:29, localpref 100, from 10.10.1.3
                          AS path: 65000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.1.44/32      *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                          AS path: 65000 I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                        [BGP/170] 00:19:27, localpref 100, from 10.10.1.3
                          AS path: 65000 I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
    20.20.1.55/32      *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                          AS path: 65000 I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                        [BGP/170] 00:19:27, localpref 100, from 10.10.1.3
                          AS path: 65000 I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
    20.20.19.0/24      *[Direct/0] 00:19:50
                        > via ge-1/2/1.691
    20.20.19.2/32      *[Local/0] 00:19:50
                          Local via ge-1/2/1.691
    20.20.42.0/24      *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                          AS path: I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:19:29, localpref 100, from 10.10.1.3
                          AS path: I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.100.0/31     *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:19:29, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.120.0/24     *[OSPF/10] 00:18:54, metric 51
                        > to 20.20.19.1 via ge-1/2/1.691
                        [BGP/170] 00:18:53, MED 51, localpref 100, from 10.10.1.2
                          AS path: I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:18:53, MED 51, localpref 100, from 10.10.1.3
                          AS path: I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
    20.20.150.0/31     *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                        [BGP/170] 00:19:27, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
    20.20.200.0/31     *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                        [BGP/170] 00:19:27, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
    44.44.0.0/16       *[BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                          AS path: 400 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r5
                        [BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                          AS path: 400 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r5
    212.100.0.0/16     *[BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                          AS path: 1002 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
                        [BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                          AS path: 1002 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
    215.1.0.0/16       *[BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                          AS path: 1000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
                        [BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                          AS path: 1000 I
                        > to 10.10.13.2 via ge-1/2/1.13
                          to 10.10.12.2 via ge-1/2/1.12
    218.2.0.0/16       *[BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                          AS path: 2000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
                        [BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                          AS path: 2000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
    223.3.0.0/16       *[BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                          AS path: 3000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
                        [BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                          AS path: 3000 I
                          to 10.10.13.2 via ge-1/2/1.13
                        > to 10.10.12.2 via ge-1/2/1.12
    224.0.0.5/32       *[OSPF/10] 00:20:15, metric 1
                          MultiRecv

#### solution 2
    
##### remove solution1

    #R1 global add static route summarizing all vpn routes, pointing intoto vrf
    delete logical-systems r1 routing-options static route 20.20.0.0/16

    #then adv to all internet via bgp
    delete logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg
    
    delete logical-systems r1 protocols bgp group to-rr export exp-bgp-vpn-agg
    delete logical-systems r1 protocols bgp group c3 export exp-bgp-vpn-agg

    #R1 vrf adv a default route to CE1 
    delete logical-systems r1 routing-instances GREEN routing-options aggregate route 0.0.0.0/0
    delete logical-systems r1 policy-options policy-statement exp-ospf-default
    delete logical-systems r1 routing-instances GREEN protocols ospf export exp-ospf-default
    
    #R1 also need to adv the default route to all other CE sites
    delete logical-systems r1 policy-options policy-statement vrf-exp term 3
    
    #R1 leak the Internet table(only bgp part in this case, so under BGP) to vrf
    delete logical-systems r1 routing-options rib-groups imp-inet.0-to-vrf
    delete logical-systems r1 protocols bgp group to-rr family inet unicast rib-group imp-inet.0-to-vrf
 
##### solution2 config
    
    set logical-systems r1 routing-options static route 0/0 next-hop [ 10.10.12.2 10.10.13.2 ] 
    set logical-systems r1 routing-options rib-groups imp-inet.0-to-vrf import-rib [ inet.0 GREEN.inet.0 ] 
    set logical-systems r1 routing-options static rib-group imp-inet.0-to-vrf 

    set logical-systems r1 policy-options policy-statement vrf-exp term 3 from protocol static route-filter 0/0 exact  
    set logical-systems r1 policy-options policy-statement vrf-exp term 3 then community add GREEN                       
    set logical-systems r1 policy-options policy-statement vrf-exp term 3 then accept                 
    
    
    #config an aggr route in R1 and adv to all R
    set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 from protocol aggregate route-filter 20.20/16 exact  
    set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 then accept                                            
    set logical-systems r1 protocols bgp group to-rr export exp-bgp-vpn-agg  
    
    #aggr. routes need at least one contributor, import some contributing routes from vrf table
    set logical-systems r1 routing-instances GREEN protocols ospf rib-group imp-vrf-to-inet.0    
    set logical-systems r1 routing-options rib-groups imp-vrf-to-inet.0 import-rib [GREEN.inet.0 inet.0]    
    
    set logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg term 1 from rib inet.0 protocol aggregate route-filter 20.20/16 exact    
    set logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg term 1 then next-hop next-table GREEN.inet.0 
    set logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg term 1 then accept                                            
    
    set logical-systems r1 routing-options forwarding-table export exp-fwd-vpn-agg  



##### R1 => Internet : R1 : static to R2/3

    set logical-systems r1 routing-options static route 0/0 next-hop [ 10.10.12.2 10.10.13.2 ] 
    
    
    lab@MX80-NGGWR-01# run show route 0/0 exact logical-system r1  

    inet.0: 48 destinations, 55 routes (48 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    0.0.0.0/0          *[Static/5] 00:02:28
                        > to 10.10.13.2 via ge-1/2/1.13
                          to 10.10.12.2 via ge-1/2/1.12


##### R1:vrf => R1 => Internet : R1 copy route into vrf
    
    set logical-systems r1 routing-options rib-groups imp-inet.0-to-vrf import-rib [ inet.0 GREEN.inet.0 ] 
    set logical-systems r1 routing-options static rib-group imp-inet.0-to-vrf 



    lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN.inet.0 protocol static          

    GREEN.inet.0: 16 destinations, 30 routes (16 active, 0 holddown, 3 hidden)
    + = Active Route, - = Last Active, * = Both

    0.0.0.0/0          *[Static/5] 00:00:55
                          to 10.10.13.2 via ge-1/2/1.13
                        > to 10.10.12.2 via ge-1/2/1.12

##### other R:vrf => R1:vrf (=> Internet) : adv default to other site

    set logical-systems r1 policy-options policy-statement vrf-exp term 3 from protocol static route-filter 0/0 exact  
    set logical-systems r1 policy-options policy-statement vrf-exp term 3 then community add GREEN                       
    set logical-systems r1 policy-options policy-statement vrf-exp term 3 then accept                 
    
    
    
    [edit]
    lab@MX80-NGGWR-01# run show route table GREEN.inet.0 logical-system r4 0/0 exact  

    GREEN.inet.0: 17 destinations, 29 routes (17 active, 0 holddown, 2 hidden)
    + = Active Route, - = Last Active, * = Both

    0.0.0.0/0          *[BGP/170] 00:02:06, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.24.1 via ge-1/2/2.24, label-switched-path r4-r1
                        [BGP/170] 00:02:06, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.24.1 via ge-1/2/2.24, label-switched-path r4-r1

    [edit]
    lab@MX80-NGGWR-01# run show route table GREEN.inet.0 logical-system r8 0/0 exact    

    GREEN.inet.0: 16 destinations, 28 routes (16 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    0.0.0.0/0          *[BGP/170] 00:02:17, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.68.1 via ge-1/2/2.68, Push 16, Push 300544(top)
                        [BGP/170] 00:02:17, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.68.1 via ge-1/2/2.68, Push 16, Push 300544(top)

##### Internet => R1 : R1: adv an aggr route out

    #config an aggr route in R1 and adv to all R
    set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 from protocol aggregate route-filter 20.20/16 exact  
    set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 then accept                                            
    set logical-systems r1 protocols bgp group to-rr export exp-bgp-vpn-agg  
    
    #aggr. routes need at least one contributor, import some contributing routes from vrf table
    set logical-systems r1 routing-instances GREEN protocols ospf rib-group imp-vrf-to-inet.0    
    set logical-systems r1 routing-options rib-groups imp-vrf-to-inet.0 import-rib [GREEN.inet.0 inet.0]    
    
        lab@MX80-NGGWR-01# run show route protocol ospf logical-system r1 table GREEN.inet.0    

        GREEN.inet.0: 16 destinations, 30 routes (16 active, 0 holddown, 3 hidden)
        + = Active Route, - = Last Active, * = Both

        20.20.1.11/32      *[OSPF/150] 00:05:42, metric 0, tag 0
                            > to 20.20.19.1 via ge-1/2/1.691
        20.20.120.0/24     *[OSPF/10] 00:05:42, metric 51
                            > to 20.20.19.1 via ge-1/2/1.691
        224.0.0.5/32       *[OSPF/10] 00:07:16, metric 1
                              MultiRecv
                          
        [edit]
        lab@MX80-NGGWR-01# run show route protocol bgp logical-system r2 20.20/16 exact    

        inet.0: 75 destinations, 93 routes (75 active, 0 holddown, 2 hidden)
        Restart Complete
        + = Active Route, - = Last Active, * = Both

        20.20.0.0/16       *[BGP/170] 00:00:07, localpref 100, from 10.10.1.5
                              AS path: I
                            > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                            [BGP/170] 00:00:07, localpref 100, from 10.10.1.6
                              AS path: I
                            > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

##### R1 => vrf : look up vpn aggr routes (of R1 inet.0) also in vrf table

    set logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg term 1 from rib inet.0 protocol aggregate route-filter 20.20/16 exact    
    set logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg term 1 then next-hop next-table GREEN.inet.0 
    set logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg term 1 then accept                                            
    
    set logical-systems r1 routing-options forwarding-table export exp-fwd-vpn-agg  

    #before
    lab@MX80-NGGWR-01# run show route logical-system r1 20.20.1.33                       

    inet.0: 54 destinations, 61 routes (51 active, 0 holddown, 3 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    20.20.0.0/16       *[Aggregate/130] 01:08:05
                          Reject

    GREEN.inet.0: 16 destinations, 30 routes (16 active, 0 holddown, 3 hidden)
    + = Active Route, - = Last Active, * = Both

    20.20.1.33/32      *[BGP/170] 01:06:57, localpref 100, from 10.10.1.2
                          AS path: 65000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 01:06:57, localpref 100, from 10.10.1.3
                          AS path: 65000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green

##### ping test
    
    lab@MX80-NGGWR-01# run ping 10.10.1.5 logical-system r0 routing-instance green-ce3 source 20.20.1.33              
    PING 10.10.1.5 (10.10.1.5): 56 data bytes
    64 bytes from 10.10.1.5: icmp_seq=0 ttl=60 time=1.432 ms
    64 bytes from 10.10.1.5: icmp_seq=1 ttl=60 time=0.665 ms
    ^C
    --- 10.10.1.5 ping statistics ---
    2 packets transmitted, 2 packets received, 0% packet loss
    round-trip min/avg/max/stddev = 0.665/1.048/1.432/0.384 ms

##### remove solution 2

    delete logical-systems r1 routing-options static route 0/0
    delete logical-systems r1 routing-options rib-groups imp-inet.0-to-vrf
    delete logical-systems r1 routing-options static rib-group imp-inet.0-to-vrf 

    delete logical-systems r1 policy-options policy-statement vrf-exp term 3
    
    #config an aggr route in R1 and adv to all R
    delete logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg
    delete logical-systems r1 protocols bgp group to-rr export exp-bgp-vpn-agg  
    
    #aggr. routes need at least one contributor, import some contributing routes from vrf table
    delete logical-systems r1 routing-instances GREEN protocols ospf rib-group imp-vrf-to-inet.0    
    delete logical-systems r1 routing-options rib-groups imp-vrf-to-inet.0
    
    delete logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg
    delete logical-systems r1 routing-options forwarding-table export exp-fwd-vpn-agg  

#### TIP: about `next-hop next-table GREEN.inet.0`

* this only change where to "lookup" , not any routing tables themselves.
* once next-table is used, the `from` statement must exclude the table in the
  `next-table` action (meaning specifying a different table) 
  
    from ...
    
        rib inet.0      #<------this can't be omitted

    then ...
        
        next-hop next-table GREEN.inet.0
        
                                                    
#### TIP: icmp-tunneling

    set logical-systems r1 protocols mpls icmp-tunneling       
    set logical-systems r2 protocols mpls icmp-tunneling       
    set logical-systems r3 protocols mpls icmp-tunneling       
    set logical-systems r4 protocols mpls icmp-tunneling       
    set logical-systems r5 protocols mpls icmp-tunneling       
    set logical-systems r6 protocols mpls icmp-tunneling       
    set logical-systems r7 protocols mpls icmp-tunneling       
    set logical-systems r8 protocols mpls icmp-tunneling       

#### TIP: about `local-as`

configured local-as under RI without `autonomous-system` under routing-option,
will lead to unexpected behavior at least in the lab simulation

    lab@MX80-NGGWR-01# run show route logical-system r0 table green-ce5.inet.0 hidden 0/0 exact extensive    

    green-ce5.inet.0: 14 destinations, 16 routes (13 active, 0 holddown, 2 hidden)
    0.0.0.0/0 (1 entry, 0 announced)
             BGP   
                    Next hop type: Router, Next hop index: 2795
                    Address: 0x2be0b0c
                    Next-hop reference count: 21
                    Source: 20.20.150.1
                    Next hop: 20.20.150.1 via ge-1/2/2.658, selected
                    State: <Hidden Ext>
                    Peer AS: 4012345678
                    Age: 52 
                    Task: BGP_4012345678_65000.20.20.150.1+65053
                    AS path: 4012345678 {4012345678 400 1000 1001 1002 2000 3000} I (Looped: 400)  Aggregator: 4012345678 10.10.1.1
                    Communities: target:2:65000
                    Router ID: 20.20.150.1
                    
    same to ce3,4,5.

    changing C4 as from `local-as` to `autonomous-system XX` solved the issue.
    
    lab@MX80-NGGWR-01# run show route logical-system r0 table green-ce5.inet.0 0/0 exact extensive      #<------(not hidden)

    green-ce5.inet.0: 14 destinations, 16 routes (14 active, 0 holddown, 1 hidden)
    0.0.0.0/0 (1 entry, 1 announced)
    TSI:
    KRT in-kernel 0.0.0.0/0 -> {20.20.150.1}
            *BGP    Preference: 170/-101
                    Next hop type: Router, Next hop index: 2795
                    Address: 0x2be0b0c
                    Next-hop reference count: 22
                    Source: 20.20.150.1
                    Next hop: 20.20.150.1 via ge-1/2/2.658, selected
                    State: <Active Ext>
                    Peer AS: 4012345678
                    Age: 5 
                    Task: BGP_4012345678_65000.20.20.150.1+65053
                    Announcement bits (1): 0-KRT 
                    AS path: 4012345678 {4012345678 400 1000 1001 1002 2000 3000} I Aggregator: 4012345678 10.10.1.1
                    Communities: target:2:65000
                    Accepted
                    Localpref: 100
                    Router ID: 20.20.150.1

#### TIP: import-rib and export-rib

example:

    set logical-systems r1 routing-instances GREEN protocols ospf rib-group imp-vrf-to-inet.0    
    set logical-systems r1 routing-options rib-groups imp-vrf-to-inet.0 import-rib [GREEN.inet.0 inet.0]    

one common understanding is : import rib from a "source" vrf table GREEN.inet.0,
into the global routing table inet.0

but a more accurate understanding should be:

from the routing table's standspoint:
"import" routes from protocol ospf under vrf GREEN, into "primary" routing table
-- under vrf its the vrf table GREEN.inet.0 (default behavior) , and because of this
import-rib config, also import into a "backup" routing table -- inet.0 , meaning
the global routing table.

            
    from protocol:      ospf/static/interface/etc...                    into protocol
                               ||                           AA
                               ||                           ||
    import into:        -------++---------------------------++-------   export
                       (import)||                   (export)||
                               vv                           ||
    routing table:      
         default:       inet.0 (def. )              inet.0 (def. w/o export-rib)
         rib-group:     inet.0 + GREEN.inet.0       inet.3(need some test)


### vpn lsp map

#### config

    set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 1 from protocol bgp community ce2
    set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 1 then install-nexthop lsp r1-r4-blue
    set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 1 then accept
    set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 2 from protocol bgp community ce3
    set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 2 then install-nexthop lsp r1-r4-green
    set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 2 then accept
    
    set logical-systems r1 routing-options forwarding-table export exp-fwd-lspmap

#### verify

    [edit]
    lab@MX80-NGGWR-01# run traceroute 20.20.1.33 logical-system r0 routing-instance green-ce1              
    traceroute to 20.20.1.33 (20.20.1.33), 30 hops max, 40 byte packets
     1  20.20.19.2 (20.20.19.2)  0.651 ms  33.948 ms  0.438 ms
     2  10.10.12.2 (10.10.12.2)  0.556 ms  0.516 ms  0.506 ms
         MPLS Label=299824 CoS=0 TTL=1 S=0
         MPLS Label=16 CoS=0 TTL=1 S=1
     3  20.20.100.1 (20.20.100.1)  0.465 ms  0.568 ms  0.448 ms
     4  20.20.1.33 (20.20.1.33)  0.583 ms  0.845 ms  0.703 ms

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN 20.20.1.22                         

    GREEN.inet.0: 16 destinations, 30 routes (16 active, 0 holddown, 3 hidden)
    + = Active Route, - = Last Active, * = Both

    20.20.1.22/32      *[BGP/170] 00:41:23, MED 0, localpref 100, from 10.10.1.2
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #<------default:all pick blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:41:23, MED 0, localpref 100, from 10.10.1.3
                          AS path: I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #<------
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN 20.20.1.33    

    GREEN.inet.0: 16 destinations, 30 routes (16 active, 0 holddown, 3 hidden)
    + = Active Route, - = Last Active, * = Both

    20.20.1.33/32      *[BGP/170] 00:41:33, localpref 100, from 10.10.1.2
                          AS path: 65000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #<------default:all pick blue
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                        [BGP/170] 00:41:33, localpref 100, from 10.10.1.3
                          AS path: 65000 I
                        > to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #<------
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green

    [edit]
    lab@MX80-NGGWR-01# set logical-systems r1 routing-options forwarding-table export exp-fwd-lspmap  

    [edit]
    lab@MX80-NGGWR-01# show | compare  
    [edit logical-systems r1 routing-options forwarding-table]
    -    export exp-fwd-vpn-agg;
    +    export [ exp-fwd-vpn-agg exp-fwd-lspmap ];
     
    [edit]
    lab@MX80-NGGWR-01# commit  
    commit complete
     
    [edit]
    lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN 20.20.1.22                          

    GREEN.inet.0: 16 destinations, 30 routes (16 active, 0 holddown, 3 hidden)
    + = Active Route, - = Last Active, * = Both

    20.20.1.22/32      *[BGP/170] 00:01:00, MED 0, localpref 100, from 10.10.1.2
                          AS path: I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #<------
                        [BGP/170] 00:01:00, MED 0, localpref 100, from 10.10.1.3
                          AS path: I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #<------

    [edit]
    lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN 20.20.1.33    

    GREEN.inet.0: 16 destinations, 30 routes (16 active, 0 holddown, 3 hidden)
    + = Active Route, - = Last Active, * = Both

    20.20.1.33/32      *[BGP/170] 00:01:05, localpref 100, from 10.10.1.2
                          AS path: 65000 I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green        #<------
                        [BGP/170] 00:01:05, localpref 100, from 10.10.1.3
                          AS path: 65000 I
                          to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green        #<------

    [edit]
    lab@MX80-NGGWR-01# run traceroute 20.20.1.33 logical-system r0 routing-instance green-ce1            
    traceroute to 20.20.1.33 (20.20.1.33), 30 hops max, 40 byte packets
     1  20.20.19.2 (20.20.19.2)  0.640 ms  0.585 ms  0.492 ms
     2  10.10.12.2 (10.10.12.2)  0.548 ms  0.541 ms  0.565 ms
         MPLS Label=299824 CoS=0 TTL=1 S=0
         MPLS Label=16 CoS=0 TTL=1 S=1
     3  20.20.100.1 (20.20.100.1)  0.640 ms  0.561 ms  0.438 ms
     4  20.20.1.33 (20.20.1.33)  0.625 ms  0.694 ms  0.544 ms 

    [edit]
    lab@MX80-NGGWR-01# run traceroute 20.20.1.22 logical-system r0 routing-instance green-ce1    
    traceroute to 20.20.1.22 (20.20.1.22), 30 hops max, 40 byte packets
     1  20.20.19.2 (20.20.19.2)  0.617 ms  0.436 ms  0.424 ms
     2  10.10.12.2 (10.10.12.2)  0.546 ms  0.747 ms  0.732 ms
         MPLS Label=299856 CoS=0 TTL=1 S=0
         MPLS Label=16 CoS=0 TTL=1 S=1
     3  20.20.42.2 (20.20.42.2)  0.477 ms  0.460 ms  0.552 ms
     4  20.20.1.22 (20.20.1.22)  0.682 ms  0.689 ms  0.618 ms

## InterAS VPN

### solution1: `inet (uncast+labeled-unicast rib inet.3)`

#### config

    ###R5: adv R1 lo0 to peer ASBR via policy, as inet-unicast&labeled-unicast
    ###    so peer ASBR can install R1 lo0 in both inet.0 & inet.3
    #match r1 lo0 from inet.0 (serving `inet-unicast` bgp family only)
    set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 1 from protocol isis
    set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 1 from route-filter 10.10.1.1/32 exact
    set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 1 then accept
    #match r1 lo0 from inet.3 (serving `inet-labeled-unicast` family only)
    set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 2 from rib inet.3
    set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 2 from route-filter 10.10.1.1/32 exact
    set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 2 then accept
    
    #`family inet unicast` =>                    r1 lo0 from inet.0 will be adv.ed as `inet-unicast` bgp routes
    #`family inet labeled-unicast rib inet.3` => r1 lo0 from inet.3 will be adv.ed as `inet-labeled-unicast` routes
    set logical-systems r5 protocols bgp group l3vpn neighbor 172.16.5.5 family inet unicast
    set logical-systems r5 protocols bgp group l3vpn neighbor 172.16.5.5 family inet labeled-unicast rib inet.3
    set logical-systems r5 protocols bgp group l3vpn neighbor 172.16.5.5 export exp-bgp-adv-1
    set logical-systems r5 protocols bgp group l3vpn neighbor 172.16.5.5 peer-as 2
    
    ###R1-R5-peerASBR : all need to have both family enabled, to pass along the lo0 as both NLRI
    set logical-systems r5 protocols bgp group rr family inet unicast
    set logical-systems r5 protocols bgp group rr family inet labeled-unicast rib inet.3 
    set logical-systems r1 protocols bgp group to-rr family inet unicast
    set logical-systems r1 protocols bgp group to-rr family inet labeled-unicast rib inet.3 
    set logical-systems r9 protocols bgp group to-r5 family inet unicast
    set logical-systems r9 protocols bgp group to-r5 family inet labeled-unicast rib inet.3 
    
### TIP: interAS VPN options

Option A: Unlabeled VPN-IPv4 (b2b vrf)
    
    vrf1                              vrf1                                 vrf1
        PE1---------------------ASBR1-------ASBR2-----------------------PE2
    vrf2                              vrf2                                 vrf2

* ASBR:
    - carry all routes in: bgp.v3vpn.0, and each VRFs
* least scale, not good

Option B: Labeled VPN-IPv4

* ASBR:
    - retain all VPN routes , in bgp.l3vpn.0
    - labeled-unicast to assign label(stitching e2e LSP)
    
    vrf1                                                                   vrf1
        PE1---------------------ASBR1-------ASBR2-----------------------PE2
    vrf2                                                                   vrf2
    
            <....(ldp label).......(BGP label).....(ldp label)......>
 

Option C: Multihop MP-BGP

    vrf1                                                                   vrf1
        PE1---------------------ASBR1-------ASBR2-----------------------PE2
    vrf2                                                                   vrf2
    
            <....(ldp label).......(BGP label).....(ldp label)......>
            
* PE:
    - multi-hop MP-EBGP betw PE
* ASBR: 
    - no need to maintain VPN routes
    - leak PE1 lo0 into peer AS
    - labeled-unicast to assign label

### TIP: family in diff levels

without configs in more specific level, it "inherit" from upper level
once configured in more specific level, it "overide", no more inheritence

same as policys, anything else in JUNOS

### TIP: bgp keep-all

keep all bgp.l3vpn.0 regardless of RT

### remove solution1

### solution2: `inet resolved-vpn`
    
    set logical-systems r1 protocols bgp group to-rr family inet labeled-unicast resolve-vpn    
    set logical-systems r5 protocols bgp group l3vpn family inet labeled-unicast
    set logical-systems r9 protocols bgp group to-r5 family inet labeled-unicast

### remove solution2

### TIP: `inet labeled-unicast resolve-vpn`

Allow labeled routes to be placed in the inet.3 routing table for route
resolution. These routes are then resolved for PE router connections where the
remote PE is located across another AS. For a PE router to install a route in
the VRF, the next hop must resolve to a route stored within the inet.3 table

### QUESTION: bgp flaps duing config

noticed bgp flaps during inter-AS vpn configs,might be normal

    Aug  4 04:39:35  MX80-NGGWR-01 r1:rpd[1401]: RPD_OSPF_NBRDOWN: OSPF neighbor 4.4.4.4 (realm ospf-v2 shamlink.0 area 0.0.0.0) state changed f
    rom Full to Down due to KillNbr (event reason: interface went down)
    Aug  4 04:39:34  MX80-NGGWR-01 r1: rpd[1401]: bgp_adv_main_update:7762: NOTIFICATION sent to 10.10.1.2 (Internal AS 4012345678): code 6 (Cea
    se) subcode 6 (Other Configuration Change), Reason: Configuration change - VPN table advertise
    Aug  4 04:39:34  MX80-NGGWR-01 r1: rpd[1401]: bgp_adv_main_update:7762: NOTIFICATION sent to 10.10.1.3 (Internal AS 4012345678): code 6 (Cea
    se) subcode 6 (Other Configuration Change), Reason: Configuration change - VPN table advertise

### toggle `traffic-engineering mpls-forwarding`

    delete logical-systems r1 protocols mpls traffic-engineering  
    delete logical-systems r5 protocols mpls traffic-engineering     
    delete logical-systems r9 protocols mpls traffic-engineering     

## VPLS

### config

    set logical-systems r1 routing-instances vpls instance-type vpls
    set logical-systems r1 routing-instances vpls interface ge-1/2/1.121
    set logical-systems r1 routing-instances vpls interface ge-1/2/1.122
    set logical-systems r1 routing-instances vpls interface ge-1/2/3.100
    set logical-systems r1 routing-instances vpls route-distinguisher 1.1.1.1:1
    set logical-systems r1 routing-instances vpls vrf-target target:6500:1
    set logical-systems r1 routing-instances vpls protocols vpls site-range 10
    set logical-systems r1 routing-instances vpls protocols vpls interface-mac-limit 500
    set logical-systems r1 routing-instances vpls protocols vpls no-tunnel-services
    set logical-systems r1 routing-instances vpls protocols vpls site r1 site-identifier 1
    set logical-systems r1 routing-instances vpls protocols vpls site r1 active-interface any
    set logical-systems r1 routing-instances vpls protocols vpls site r1 interface ge-1/2/1.121
    set logical-systems r1 routing-instances vpls protocols vpls site r1 interface ge-1/2/1.122

    set logical-systems r7 routing-instances vpls instance-type vpls
    set logical-systems r7 routing-instances vpls interface ge-1/2/1.678
    set logical-systems r7 routing-instances vpls route-distinguisher 2.2.2.2:1
    set logical-systems r7 routing-instances vpls vrf-target target:6500:1
    set logical-systems r7 routing-instances vpls protocols vpls site-range 10
    set logical-systems r7 routing-instances vpls protocols vpls no-tunnel-services
    set logical-systems r7 routing-instances vpls protocols vpls site r7 site-identifier 7
    set logical-systems r7 routing-instances vpls protocols vpls site r7 multi-homing
    set logical-systems r7 routing-instances vpls protocols vpls site r7 site-preference 150
    set logical-systems r7 routing-instances vpls protocols vpls site r7 active-interface any
    set logical-systems r7 routing-instances vpls protocols vpls site r7 interface ge-1/2/1.678

    set logical-systems r8 routing-instances vpls instance-type vpls
    set logical-systems r8 routing-instances vpls interface ge-1/2/1.687
    set logical-systems r8 routing-instances vpls interface ge-1/2/5.100
    set logical-systems r8 routing-instances vpls route-distinguisher 2.2.2.2:1
    set logical-systems r8 routing-instances vpls vrf-target target:6500:1
    set logical-systems r8 routing-instances vpls protocols vpls site-range 10
    set logical-systems r8 routing-instances vpls protocols vpls no-tunnel-services
    set logical-systems r8 routing-instances vpls protocols vpls site r8 site-identifier 7
    set logical-systems r8 routing-instances vpls protocols vpls site r8 multi-homing
    set logical-systems r8 routing-instances vpls protocols vpls site r8 site-preference 200
    set logical-systems r8 routing-instances vpls protocols vpls site r8 active-interface any
    set logical-systems r8 routing-instances vpls protocols vpls site r8 interface ge-1/2/1.687

        

### show vpls connection

    lab@MX80-NGGWR-01# run show vpls connections logical-system r1 extensive          
    Layer-2 VPN connections:

    Legend for connection status (St)   
    EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
    EM -- encapsulation mismatch     WE -- interface and instance encaps not same
    VC-Dn -- Virtual circuit down    NP -- interface hardware not present 
    CM -- control-word mismatch      -> -- only outbound connection is up
    CN -- circuit not provisioned    <- -- only inbound connection is up
    OR -- out of range               Up -- operational
    OL -- no outgoing label          Dn -- down                      
    LD -- local site signaled down   CF -- call admission control failure      
    RD -- remote site signaled down  SC -- local and remote site ID collision
    LN -- local site not designated  LM -- local site ID not minimum designated
    RN -- remote site not designated RM -- remote site ID not minimum designated
    XX -- unknown connection status  IL -- no incoming label
    MM -- MTU mismatch               MI -- Mesh-Group ID not available
    BK -- Backup connection          ST -- Standby connection
    PF -- Profile parse failure      PB -- Profile busy
    RS -- remote site standby        SN -- Static Neighbor
    VM -- VLAN ID mismatch

    Legend for interface status 
    Up -- operational           
    Dn -- down

    Instance: vpls
      Local site: r1 (1)
        Number of local interfaces: 2
        Number of local interfaces up: 1
        IRB interface present: no
        ge-1/2/1.121       
        ge-1/2/1.122       
            Interface flags: VC-Down
        vt-1/2/10.235929600 7         Intf - vpls vpls local site 1 remote site 7
        Label-base        Offset     Size  Range     Preference
        800000            1          8      8         100   
        connection-site           Type  St     Time last up          # Up trans
        7                         rmt   Up     Aug  7 01:29:36 2013           1
          Remote PE: 10.10.1.8, Negotiated control-word: No
          Incoming label: 800006, Outgoing label: 800000
          Local interface: vt-1/2/10.235929600, Status: Up, Encapsulation: VPLS
            Description: Intf - vpls vpls local site 1 remote site 7
        Connection History:
            Aug  7 01:29:36 2013  status update timer  
            Aug  7 01:29:36 2013  loc intf up           vt-1/2/10.235929600
            Aug  7 01:29:36 2013  PE route changed     
            Aug  7 01:29:36 2013  Out lbl Update                    800000
            Aug  7 01:29:36 2013  In lbl Update                     800006
            Aug  7 01:29:36 2013  loc intf down        

### show route forwarding-table

#### with tunne-service

    lab@MX80-NGGWR-01# run show route forwarding-table | find vpls.vpls
    Logical system: r1
    Routing table: vpls.vpls
    VPLS:
    Destination        Type RtRef Next hop           Type Index NhRef Netif
    default            perm     0                    dscd   728     1
    vt-1/2/10.235929600 intf     0                   indr 1048693     4
                                  10.10.12.2        Push 800000, Push 299808, Push 299792(top)  3007     2 ge-1/2/1.12
    0x3000b/51         user     0                    comp  3016     2
    f8:c0:01:18:93:92/48 user     0                  ucst  1986     5 ge-1/2/1.121      #<------
    ge-1/2/1.121       intf     0                    ucst  1986     5 ge-1/2/1.121
    0x3000a/51         user     0                    comp  1997     2
    0x30007/51         user     0                    comp  1994     2
    
    Logical system: r8
    Routing table: vpls.vpls
    VPLS:
    Destination        Type RtRef Next hop           Type Index NhRef Netif
    default            perm     0                    dscd   716     1
    vt-1/2/10.202375168 intf     0                   indr 1048659     5
                                  10.10.68.1        Push 800006, Push 299872(top)  3052     2 ge-1/2/2.68
    0x3000c/51         user     0                    comp  3061     2
    f8:c0:01:18:93:92/48 user     0                  indr 1048659     5         #<------
                                  10.10.68.1        Push 800006, Push 299872(top)  3052     2 ge-1/2/2.68
    ge-1/2/1.687       intf     0                    ucst  1973     4 ge-1/2/1.687
    0x30009/51         user     0                    comp  1983     2
    0x30006/51         user     0                    comp  1980     2
    
turn off tunnel service:

    lab@MX80-NGGWR-01# show | compare  
    [edit logical-systems r1 routing-instances vpls protocols vpls]
    +      no-tunnel-services;
    [edit logical-systems r8 routing-instances vpls protocols vpls]
    +      no-tunnel-services;
    
    
#### without tunnel service

    Logical system: r1
    Routing table: vpls.vpls
    VPLS:
    Destination        Type RtRef Next hop           Type Index NhRef Netif
    default            perm     0                    dscd   728     1
    lsi.235929600      intf     0                    indr 1048699     4
                                  10.10.12.2        Push 262145, Push 299808, Push 299792(top)  3014     2 ge-1/2/1.12
    0x3000a/51         user     0                    comp  3062     2
    f8:c0:01:18:93:92/48 user     0                  ucst   716     5 ge-1/2/1.121      #<------
    ge-1/2/1.121       intf     0                    ucst   716     5 ge-1/2/1.121
    0x30006/51         user     0                    comp  1998     2
    0x30007/51         user     0                    comp  1995     2

    Logical system: r8
    Routing table: vpls.vpls
    VPLS:
    Destination        Type RtRef Next hop           Type Index NhRef Netif
    default            perm     0                    dscd  1986     1
    lsi.202375168      intf     0                    indr 1048698     5
                                  10.10.68.1        Push 262151, Push 299872(top)  3005     2 ge-1/2/2.68
    0x3000d/51         user     0                    comp  1984     2
    f8:c0:01:18:93:92/48 user     0                  indr 1048698     5         #<------
                                  10.10.68.1        Push 262151, Push 299872(top)  3005     2 ge-1/2/2.68
    ge-1/2/1.687       intf     0                    ucst  1980     4 ge-1/2/1.687
    0x3000b/51         user     0                    comp  3146     2
    0x30008/51         user     0                    comp  3143     2


    ge-1/2/1: Current address: f8:c0:01:18:93:91, Hardware address: f8:c0:01:18:93:91
    ge-1/2/2: Current address: f8:c0:01:18:93:92, Hardware address: f8:c0:01:18:93:92
  
### TIP: `encapsulation extended-vlan-vpls` and `flexible-ethernet-services`

Gigabit Ethernet, 4-port Fast Ethernet, MX Series router Gigabit Ethernet,
Tri-Rate Ethernet copper, 10-Gigabit Ethernet, and aggregated Ethernet
interfaces with VLAN tagging enabled can use extended VLAN CCC or VLAN VPLS,
which allow 802.1Q tagging.

flexible-ethernet-services—For Gigabit Ethernet IQ interfaces and Gigabit
Ethernet PICs with small form-factor pluggable transceivers (SFPs) (except the
10-port Gigabit Ethernet PIC and the built-in Gigabit Ethernet port on the M7i
router), use flexible Ethernet services encapsulation when you want to
configure multiple per-unit Ethernet encapsulations. Aggregated Ethernet
bundles can use this encapsulation type. This encapsulation type allows you to
configure any combination of route, TCC, CCC, Layer 2 virtual private networks
(VPNs), and VPLS encapsulations on a single physical port. If you configure
flexible Ethernet services encapsulation on the physical interface, VLAN IDs
from 1 through 511 are no longer reserved for normal VLANs.

## cos

    IP Prec          111         110             other
    fwd-class        EF          AF              BE


R1:

    #firewall policers:5m,7m,10m
    set logical-systems r1 firewall policer 5m if-exceeding bandwidth-limit 5m    
    set logical-systems r1 firewall policer 5m if-exceeding burst-size-limit 15k   
    set logical-systems r1 firewall policer 5m then discard                         

    set logical-systems r1 firewall policer 7m if-exceeding bandwidth-limit 7m    
    set logical-systems r1 firewall policer 7m if-exceeding burst-size-limit 15k   
    set logical-systems r1 firewall policer 7m then discard                         

    set logical-systems r1 firewall policer 10m if-exceeding bandwidth-limit 10m    
    set logical-systems r1 firewall policer 10m if-exceeding burst-size-limit 15k   
    set logical-systems r1 firewall policer 10m then discard                         
    
    #firewall filter: Jfilter
    set logical-systems r1 firewall filter Jfilter term 1 from precedence 7                                    
    set logical-systems r1 firewall filter Jfilter term 1 then forwarding-class expedited-forwarding accept policer 5m 
    set logical-systems r1 firewall filter Jfilter term 2 from precedence 6                                    
    set logical-systems r1 firewall filter Jfilter term 2 then forwarding-class assured-forwarding accept policer 10m 
    set logical-systems r1 firewall filter Jfilter term 3 then forwarding-class best-effort accept policer 7m 
    
    #apply firewall filter on PE ingress i/f
    set logical-systems r1 interfaces ge-1/2/2 unit 133 family inet filter input Jfilter
    
R5:

    #R5: cos classifier (not supported under LR)
    set class-of-service classifiers inet-precedence class-ippre import default
    set class-of-service classifiers inet-precedence class-ippre forwarding-class expedited-forwarding loss-priority low code-points 111
    set class-of-service classifiers inet-precedence class-ippre forwarding-class assured-forwarding loss-priority low code-points 110 
    set class-of-service interfaces ge-1/2/2 unit 35 classifiers inet-precedence class-ippre

### TIP: QoS/CoS

#### key concepts

unidirectonal

#### IP TOS(RFC791)

    P2      P1      P0      D      T      R      CU1     CU0
    
*  IP precedence—three bits (P2 to P0)
  
    network         Match packets with network control precedence (7)
    internet        Match packets with internetwork control precedence (6)
    critical        Match packets with critical precedence (5)
    flash-override  Match packets with flash override precedence (4)
    flash           Match packets with flash precedence (3)
    immediate       Match packets with immediate precedence (2)
    priority        Match packets with priority precedence (1)
    routine         Match packets with routine precedence (0)

*  Delay, Throughput and Reliability—three bits (D T R)
*  CU (Currently Unused)—two bits(CU1-CU0)

#### DSCP

##### DiffServ field

Original IPv4 ToS byte (ping: just a new name in the context of diffserv)


RFC2474

    DS5     DS4     DS3     DS2     DS1     DS0     ECN     ECN
   
##### Behavior aggregate (BA): forwarding class

**Classification** 
based / indexed on DSCP 
Packets with a common DSCP belong to the same BA (forwarding class)

##### Per-hop behavior (PHB): scheduling algorithm based on fwd class

Forwarding treatment associated with a given BA
Packets with the same DSCP value have the same PHB

PHB group:
A set of one or more PHBs with related forwarding behavior 

Example: 
assured forwarding (AF) is a PHB group, consisting of PHBs AF1, AF2, AF3, and
AF4


###### EF(Expedited Forwarding): 101110

RFC3246

###### AF(Assured Forwarding): (001/010/011/100)BB0

RFC2597

    DSCP        AAA BB0
    =====================        
    AF1         001 BB0
    
        AF11    001 01       low
        AF11    001 10       medium
        AF11    001 11       high

    AF2         010
    
    AF3         011
    
    AF4         100
        
    


###### NC or CS(Code Selector): AAA000(001000-111000)
RFC2474: 
defined for backward compatible with RFC791 (IP precedence)
"code selector code point"
for network control traffic

AAA: 001 - 111
BBB: 000        #<------this is how to diff with other PHB

###### BE(Best Effort): 000000

no spec

###### redback device table:

    ============================================================
    <0-63>   Differentiated services codepoint value 
    af11     Match packets with AF11 dscp (001010) 
    af12     Match packets with AF12 dscp (001100) 
    af13     Match packets with AF13 dscp (001110) 
    af21     Match packets with AF21 dscp (010010) 
    af22     Match packets with AF22 dscp (010100) 
    af23     Match packets with AF23 dscp (010110) 
    af31     Match packets with AF31 dscp (011010) 
    af32     Match packets with AF32 dscp (011100) 
    af33     Match packets with AF33 dscp (011110) 
    af41     Match packets with AF41 dscp (100010) 
    af42     Match packets with AF42 dscp (100100) 
    af43     Match packets with AF43 dscp (100110) 
    cs1      Match packets with CS1(precedence 1) dscp (001000) 
    cs2      Match packets with CS2(precedence 2) dscp (010000) 
    cs3      Match packets with CS3(precedence 3) dscp (011000) 
    cs4      Match packets with CS4(precedence 4) dscp (100000) 
    cs5      Match packets with CS5(precedence 5) dscp (101000) 
    cs6      Match packets with CS6(precedence 6) dscp (110000) 
    cs7      Match packets with CS7(precedence 7) dscp (111000) 
    be(def)  Match packets with default dscp (000000) 
    ef       Match packets with EF dscp (101110) 
 
###### JUNOS default forwarding-class

    lab@MX80-NGGWR-01# set logical-systems r1 firewall filter Jfilter term 1 then forwarding-class ?
    Possible completions:
      <forwarding-class>   Classify packet to forwarding class
      BusCriticalHigh_FWCLSS  
      BusCriticalMed_FWCLSS  
      Interactive_FWCLSS   
      Network-Control_FWCLSS  
      NonCriticalHigh_FWCLSS  
      NonCriticalLow_FWCLSS  
      RealTime_FWCLSS      
      
      assured-forwarding   
      best-effort          
      expedited-forwarding  
      network-control      

##### JUNOS default code-point-aliases

    lab@rams# run show class-of-service code-point-aliases (inet-precedence|exp|dscp)
      
    Alias              Bit pattern 
    ===================================
                PRE     EXP     DSCP
                ---------------------
    af11        001     100     001010
    af12                101     001100
    af13                        001110
    af21        010             010010
    af22                        010100
    af23                        010110
    af31        011             011010
    af32                        011100
    af33                        011110
    af41        100             100010
    af42                        100100
    af43                        100110
    be          000     000     000000
    be1                 001 
    cs1                         001000  
    cs2                         010000
    cs3                         011000
    cs4                         100000
    cs5                         101000
    cs6         110     110     110000
    cs7         111     111     111000
    ef          101     010     101110
    ef1                 011 
    nc1         110     110     110000
    nc2         111     111     111000
                                       
#### IPv6: RFC2460 TC(Traffic Class) 8b



#### Ethernet: 802.1p PCP(Priority Code Point) 3b

#### MPLS: TC(Traffic Class) or EXP 3b

#### JUNOS tool chains

              +-----------+     +-----------+    +-----------+    +-----------+
       Ingress|classifier |     |policer    |    |multi-field|    |policy     |
        -->---+           +-----+           +----+classifier +----+           +
              +-----------+     +-----------+    +-----------+    +-----+-----+
                                                                        |
                                                                        |
                                                                        |
                                                                        |
              +-----------+     +-----------+    +-----------+    +-----+-----+
        Egress|rewrite    |     |scheduler  |    |multi-field|    |policer    |
        <-----+marker     +-----+shaper/RED +----+classifier +----+           +
              +-----------+     +-----------+    +-----------+    +-----------+


##### classifier: ingress traffic ==> Q (forwarding class)

##### policer: traffic limit

##### policy: Cos Based Forwarding

##### scheduler: RED/WRED/PWFQ/etc

##### rewrite marker

## misc (obsoleted)

### ipv6

#### p1/p3 got all ipv6 routes

    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table p1.inet6.0   

    p1.inet6.0: 20 destinations, 31 routes (20 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    2000:2000::/32     *[BGP/170] 00:54:04, localpref 100
                          AS path: 4012345678 2000 I
                        > to ::192.168.211.1 via ge-1/2/2.211
                        [BGP/170] 00:54:04, localpref 100
                          AS path: 4012345678 2000 I
                        > to ::192.168.31.1 via ge-1/2/2.311
                        [BGP/170] 00:54:04, localpref 100
                          AS path: 4012345678 2000 I
                        > to ::192.168.11.1 via ge-1/2/2.511
    2000:3000::/32     *[BGP/170] 00:54:04, localpref 100
                          AS path: 4012345678 3000 I
                        > to ::192.168.211.1 via ge-1/2/2.211
                        [BGP/170] 00:54:04, localpref 100
                          AS path: 4012345678 3000 I
                        > to ::192.168.31.1 via ge-1/2/2.311
                        [BGP/170] 00:54:04, localpref 100
                          AS path: 4012345678 3000 I
                        > to ::192.168.11.1 via ge-1/2/2.511
    3000:1000::/32     *[BGP/170] 00:54:08, localpref 100
                          AS path: 4012345678 1001 I
                        > to ::192.168.11.1 via ge-1/2/2.511
    3000:2000::/32     *[BGP/170] 00:54:08, localpref 100
                          AS path: 4012345678 1002 I
                        > to ::192.168.11.1 via ge-1/2/2.511
    3333:3333:3333::/48*[BGP/170] 00:54:12, localpref 100
                          AS path: 4012345678 300 I
                        > to ::192.168.31.1 via ge-1/2/2.311
                        [BGP/170] 00:54:12, localpref 100
                          AS path: 4012345678 300 I
                        > to ::192.168.211.1 via ge-1/2/2.211
                        [BGP/170] 00:54:08, localpref 100
                          AS path: 4012345678 300 I
                        > to ::192.168.11.1 via ge-1/2/2.511
    4444:4444:4444::/48*[BGP/170] 00:54:08, localpref 100
                          AS path: 4012345678 400 I
                        > to ::192.168.11.1 via ge-1/2/2.511
    5555:5555:5555::/48*[BGP/170] 00:54:12, localpref 100
                          AS path: 4012345678 500 I
                        > to ::192.168.211.1 via ge-1/2/2.211
                        [BGP/170] 00:43:48, localpref 100
                          AS path: 4012345678 500 I
                        > to ::192.168.31.1 via ge-1/2/2.311
                        [BGP/170] 00:54:08, localpref 100
                          AS path: 4012345678 500 I
                        > to ::192.168.11.1 via ge-1/2/2.511

#### p2 is missing some IPv6 routes

    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table p2.inet6.0   

    p2.inet6.0: 14 destinations, 20 routes (14 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32     *[BGP/170] 00:56:48, localpref 100
                          AS path: 4012345678 1000 I
                        > to ::192.168.212.1 via ge-1/2/2.212
                        [BGP/170] 00:56:48, localpref 100
                          AS path: 4012345678 1000 I
                        > to ::192.168.32.1 via ge-1/2/2.312
    2000:3000::/32     *[BGP/170] 00:56:48, localpref 100
                          AS path: 4012345678 3000 I
                        > to ::192.168.212.1 via ge-1/2/2.212
                        [BGP/170] 00:56:48, localpref 100
                          AS path: 4012345678 3000 I
                        > to ::192.168.32.1 via ge-1/2/2.312
    3333:3333:3333::/48*[BGP/170] 00:56:48, localpref 100
                          AS path: 4012345678 300 I
                        > to ::192.168.212.1 via ge-1/2/2.212
                        [BGP/170] 00:56:48, localpref 100
                          AS path: 4012345678 300 I
                        > to ::192.168.32.1 via ge-1/2/2.312
    5555:5555:5555::/48*[BGP/170] 00:56:48, localpref 100
                          AS path: 4012345678 500 I
                        > to ::192.168.212.1 via ge-1/2/2.212
                        [BGP/170] 00:46:32, localpref 100
                          AS path: 4012345678 500 I
                        > to ::192.168.32.1 via ge-1/2/2.312


P2 is missing C4 routes, T1/T2 routes, need to check R2/R3

#### R2/R3 routes

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table p2.inet6.0 hidden  

    p2.inet6.0: 14 destinations, 20 routes (14 active, 0 holddown, 0 hidden)

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp table inet6.0 logical-system lr2                             

    inet6.0: 24 destinations, 33 routes (23 active, 0 holddown, 4 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32     *[BGP/170] 01:00:39, localpref 100
                          AS path: 1000 I
                        > to ::192.168.211.0 via ge-1/2/1.211
    2000:2000::/32     *[BGP/170] 01:00:31, localpref 100
                          AS path: 2000 I
                        > to ::192.168.212.0 via ge-1/2/1.212
    2000:3000::/32     *[BGP/170] 01:00:31, localpref 100
                          AS path: 3000 I
                        > to ::192.168.213.0 via ge-1/2/1.213
    3000:1000::/32     *[BGP/170] 01:00:39, localpref 100
                          AS path: 1001 I
                        > to ::192.168.221.0 via ge-1/2/1.221
    3000:2000::/32     *[BGP/170] 01:00:31, localpref 100
                          AS path: 1002 I
                        > to ::192.168.222.0 via ge-1/2/1.222
    3333:3333:3333::/48*[BGP/170] 01:00:39, localpref 100, from 10.10.1.5
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                        [BGP/170] 01:00:39, localpref 100, from 10.10.1.6
                          AS path: 300 I
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    5555:5555:5555::/48*[BGP/170] 01:00:39, localpref 100, from 10.10.1.5
                          AS path: 500 I
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
                        [BGP/170] 01:00:39, localpref 100, from 10.10.1.6
                          AS path: 500 I
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4

    lab@MX80-NGGWR-01# run show route protocol bgp table inet6.0 logical-system lr3    

    inet6.0: 21 destinations, 36 routes (20 active, 0 holddown, 4 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32     *[BGP/170] 01:01:07, localpref 100
                          AS path: 1000 I
                        > to ::192.168.31.0 via ge-1/2/1.311
                        [BGP/170] 01:01:07, localpref 100, from 10.10.1.6
                          AS path: 1000 I
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
    2000:2000::/32     *[BGP/170] 01:00:59, localpref 100
                          AS path: 2000 I
                        > to ::192.168.32.0 via ge-1/2/1.312
                        [BGP/170] 00:50:42, localpref 100, from 10.10.1.5
                          AS path: 2000 I
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
                        [BGP/170] 01:00:59, localpref 100, from 10.10.1.6
                          AS path: 2000 I
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
    2000:3000::/32     *[BGP/170] 01:00:59, localpref 100, from 10.10.1.6
                          AS path: 3000 I
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
    3000:1000::/32     *[BGP/170] 01:00:59, localpref 100
                          AS path: 1001 I
                        > to ::192.168.21.0 via ge-1/2/1.321
                        [BGP/170] 00:50:42, localpref 100, from 10.10.1.5
                          AS path: 1001 I
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
                        [BGP/170] 01:01:07, localpref 100, from 10.10.1.6
                          AS path: 1001 I
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
    3000:2000::/32     *[BGP/170] 01:01:07, localpref 100
                          AS path: 1002 I
                        > to ::192.168.22.0 via ge-1/2/1.322
                        [BGP/170] 00:50:42, localpref 100, from 10.10.1.5
                          AS path: 1002 I
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
                        [BGP/170] 01:00:59, localpref 100, from 10.10.1.6
                          AS path: 1002 I
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
    3333:3333:3333::/48*[BGP/170] 01:01:07, localpref 100, from 10.10.1.5
                          AS path: 300 I
                        > to 10.10.13.1 via ge-1/2/2.13, label-switched-path r3-r1
                        [BGP/170] 01:01:07, localpref 100, from 10.10.1.6
                          AS path: 300 I
                        > to 10.10.13.1 via ge-1/2/2.13, label-switched-path r3-r1
    5555:5555:5555::/48*[BGP/170] 01:01:07, localpref 100, from 10.10.1.5
                          AS path: 500 I
                        > to 10.10.36.2 via ae12.0, label-switched-path r3-r4
                        [BGP/170] 01:01:07, localpref 100, from 10.10.1.6
                          AS path: 500 I
                        > to 10.10.36.2 via ae12.0, label-switched-path r3-r4


problem:
* R2/R3 have all routes except C4 routes
* because of policy config, p/t won't exchange routes, so that's why lr2 won't
  export t routes to p.
* why R2/R3 don't have C4 route?

#### R2/R3 routes from R5/R6 are hidden 

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp table inet6.0 logical-system lr2 hidden                                

    inet6.0: 24 destinations, 33 routes (23 active, 0 holddown, 4 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32      [BGP/170] 01:16:05, localpref 100, from 10.10.1.5
                          AS path: 1000 I
                          Unusable
    2000:3000::/32      [BGP/170] 01:16:05, localpref 100, from 10.10.1.5
                          AS path: 3000 I
                          Unusable
    4444:4444:4444::/48 [BGP/170] 01:25:16, localpref 100, from 10.10.1.6
                          AS path: 400 I
                          Unusable
                        [BGP/170] 01:25:16, localpref 100, from 10.10.1.5
                          AS path: 400 I
                          Unusable

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp table inet6.0 logical-system lr3 hidden    

    inet6.0: 21 destinations, 36 routes (20 active, 0 holddown, 4 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32      [BGP/170] 01:16:56, localpref 100, from 10.10.1.5
                          AS path: 1000 I
                          Unusable
    2000:3000::/32      [BGP/170] 01:16:56, localpref 100, from 10.10.1.5
                          AS path: 3000 I
                          Unusable
    4444:4444:4444::/48 [BGP/170] 01:26:07, localpref 100, from 10.10.1.6
                          AS path: 400 I
                          Unusable
                        [BGP/170] 01:26:07, localpref 100, from 10.10.1.5
                          AS path: 400 I
                          Unusable


    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp table inet6.0 logical-system lr2 hidden 4444:4444:4444::/48 extensive   

    inet6.0: 24 destinations, 33 routes (23 active, 0 holddown, 4 hidden)
    Restart Complete
    4444:4444:4444::/48 (2 entries, 0 announced)
             BGP    Preference: 170/-101
                    Next hop type: Unusable
                    Address: 0x23f3f04
                    Next-hop reference count: 6
                    State: <Hidden Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:41:59 
                    Task: BGP_4012345678.10.10.1.6+179
                    AS path: 400 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.7
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.6
                    Indirect next hops: 1
                            Protocol next hop: ::ffff:10.10.1.7
                            Indirect next hop: 0 -
             BGP    Preference: 170/-101
                    Next hop type: Unusable
                    Address: 0x23f3f04
                    Next-hop reference count: 6
                    State: <Hidden Int Ext>
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:41:59 
                    Task: BGP_4012345678.10.10.1.5+179
                    AS path: 400 I (Originator) Cluster list:  1.1.1.1
                    AS path:  Originator ID: 10.10.1.7
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.5
                    Indirect next hops: 1
                            Protocol next hop: ::ffff:10.10.1.7
                            Indirect next hop: 0 -

next-hop is R7's "ipv4-mapped ipv6" address, need to check inet6.3 for this
address.

#### R2/R3 inet6.3: missing R7/R8

    [edit]
    lab@MX80-NGGWR-01# run show route table inet6.3 logical-system lr2    

    inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[RSVP/7/1] 01:18:25, metric 5
                        > to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
    ::ffff:10.10.1.3/128
                       *[RSVP/7/1] 01:18:25, metric 5
                        > to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
    ::ffff:10.10.1.4/128
                       *[RSVP/7/1] 01:18:25, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
    ::ffff:10.10.1.5/128
                       *[RSVP/7/1] 01:18:25, metric 5
                        > to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                          to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
    ::ffff:10.10.1.6/128
                       *[RSVP/7/1] 01:18:25, metric 5
                        > to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6


    [edit]
    lab@MX80-NGGWR-01# run show route table inet6.3 logical-system lr3    

    inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    ::ffff:10.10.1.1/128
                       *[RSVP/7/1] 01:18:28, metric 5
                        > to 10.10.13.1 via ge-1/2/2.13, label-switched-path r3-r1
    ::ffff:10.10.1.2/128
                       *[RSVP/7/1] 01:18:28, metric 5
                        > to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
    ::ffff:10.10.1.4/128
                       *[RSVP/7/1] 01:18:27, metric 10
                        > to 10.10.36.2 via ae12.0, label-switched-path r3-r4
    ::ffff:10.10.1.5/128
                       *[RSVP/7/1] 01:18:28, metric 5
                        > to 10.10.35.2 via ge-1/2/1.35, label-switched-path r3-r5
    ::ffff:10.10.1.6/128
                       *[RSVP/7/1] 01:18:27, metric 5
                        > to 10.10.36.2 via ae12.0, label-switched-path r3-r6

R2/R3 are missing R3/R2/R7/R8 lo0 host routes in inet6.3, making all IPv6 routes
coming from them listed in "hidden".

solutions:
* "install" the missing R7 entry
* change NH of those hidden routes to RRs (R5/R6) instead of R7


#### QUESTION: R2 hidden P1/P3 route , from R5?

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp table inet6.0 logical-system lr2 hidden 2000:1000::/32 extensive  

    inet6.0: 24 destinations, 33 routes (23 active, 0 holddown, 4 hidden)
    Restart Complete
    2000:1000::/32 (2 entries, 1 announced)
    TSI:
    KRT in-kernel 2000:1000::/32 -> {::192.168.211.0}
    Page 0 idx 0 Type 1 val 2815ef4
        Flags: Nexthop Change
        Nexthop: Self
        Localpref: 100
        AS path: [4012345678] 1000 I
        Communities: 65513:200
    Page 0 idx 1 Type 1 val 2815a5c
        Nexthop: ::192.168.211.0
        AS path: [4012345678] 1000 I
        Communities: 65513:200
        Advertise: 00000006
    Path 2000:1000:: from ::192.168.211.0 Vector len 4.  Val: 0 1
             BGP    Preference: 170/-101
                    Next hop type: Unusable
                    Address: 0x23f3f04
                    Next-hop reference count: 6
                    State: <Hidden Int Ext>
                    Inactive reason: Unusable path
                    Local AS: 4012345678 Peer AS: 4012345678
                    Age: 1:23:38 
                    Task: BGP_4012345678.10.10.1.5+179
                    AS path: 1000 I
                    Communities: 65513:200
                    Accepted
                    Localpref: 100
                    Router ID: 10.10.1.5
                    Indirect next hops: 1
                            Protocol next hop: ::192.168.11.0
                            Indirect next hop: 0 -

A: might need to define some dedicated VLANs in LS lptc to adv routes



#### NH self on RR (R5/R6) when reflecting between R2/R3 and R7

    set logical-systems lr5 policy-options policy-statement exp-nhs-from-r2-r3 term 1 from protocol bgp neighbor 10.10.1.2 
    set logical-systems lr5 policy-options policy-statement exp-nhs-from-r2-r3 term 1 from protocol bgp neighbor 10.10.1.3    
    set logical-systems lr5 policy-options policy-statement exp-nhs-from-r2-r3 term 1 then next-hop self                              
    set logical-systems lr5 policy-options policy-statement exp-nhs-from-r7 term 1 from protocol bgp neighbor 10.10.1.7 
    set logical-systems lr5 policy-options policy-statement exp-nhs-from-r7 term 1 then next-hop self  
    set logical-systems lr5 protocols bgp group rr neighbor 10.10.1.2 export exp-int-agg  
    set logical-systems lr5 protocols bgp group rr neighbor 10.10.1.3 export exp-int-agg    
    set logical-systems lr5 protocols bgp group rr neighbor 10.10.1.7 export exp-int-agg    

    set logical-systems lr6 policy-options policy-statement exp-nhs-from-r2-r3 term 1 from protocol bgp neighbor 10.10.1.2 
    set logical-systems lr6 policy-options policy-statement exp-nhs-from-r2-r3 term 1 from protocol bgp neighbor 10.10.1.3    
    set logical-systems lr6 policy-options policy-statement exp-nhs-from-r2-r3 term 1 then next-hop self                              
    set logical-systems lr6 policy-options policy-statement exp-nhs-from-r7 term 1 from protocol bgp neighbor 10.10.1.7 
    set logical-systems lr6 policy-options policy-statement exp-nhs-from-r7 term 1 then next-hop self  
    set logical-systems lr6 protocols bgp group rr neighbor 10.10.1.2 export exp-int-agg  
    set logical-systems lr6 protocols bgp group rr neighbor 10.10.1.3 export exp-int-agg    
    set logical-systems lr6 protocols bgp group rr neighbor 10.10.1.7 export exp-int-agg    

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table p2.inet6.0  

    p2.inet6.0: 15 destinations, 22 routes (15 active, 0 holddown, 0 hidden)
    + = Active Route, - = Last Active, * = Both

    2000:1000::/32     *[BGP/170] 02:13:02, localpref 100
                          AS path: 4012345678 1000 I
                        > to ::192.168.212.1 via ge-1/2/2.212
                        [BGP/170] 02:13:02, localpref 100
                          AS path: 4012345678 1000 I
                        > to ::192.168.32.1 via ge-1/2/2.312
    2000:3000::/32     *[BGP/170] 02:13:02, localpref 100
                          AS path: 4012345678 3000 I
                        > to ::192.168.212.1 via ge-1/2/2.212
                        [BGP/170] 02:13:02, localpref 100
                          AS path: 4012345678 3000 I
                        > to ::192.168.32.1 via ge-1/2/2.312
    3333:3333:3333::/48*[BGP/170] 02:13:02, localpref 100
                          AS path: 4012345678 300 I
                        > to ::192.168.212.1 via ge-1/2/2.212
                        [BGP/170] 02:13:02, localpref 100
                          AS path: 4012345678 300 I
                        > to ::192.168.32.1 via ge-1/2/2.312
    4444:4444:4444::/48*[BGP/170] 00:02:43, localpref 100
                          AS path: 4012345678 400 I
                        > to ::192.168.212.1 via ge-1/2/2.212
                        [BGP/170] 00:02:43, localpref 100
                          AS path: 4012345678 400 I
                        > to ::192.168.32.1 via ge-1/2/2.312
    5555:5555:5555::/48*[BGP/170] 02:13:02, localpref 100
                          AS path: 4012345678 500 I
                        > to ::192.168.212.1 via ge-1/2/2.212
                        [BGP/170] 02:02:46, localpref 100
                          AS path: 4012345678 500 I
                        > to ::192.168.32.1 via ge-1/2/2.312

