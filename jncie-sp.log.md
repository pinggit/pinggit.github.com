---
layout: page
title: jncie-sp logs
published: false
tagline: -- my collection of tips of life, tech, thought , everything ...
---

{% include JB/setup %}

TABLE OF CONTENT

* auto-gen TOC:
  {:toc}
  
  - - -



# logs

## transfer-on-commit

### config

    [edit]
    lab@MX80-NGGWR-01# show system archival                                                       
    configuration {
        transfer-on-commit;
        archive-sites {
            "ftp://test:test@172.25.84.169/transfer-on-commit/";
            "scp://Ping:Juniper1%40@172.25.84.169/transfer-on-commit/";   #<------doesn't work
        }
    }

### verify

    [edit]
    lab@abc# run show log messages | match transfer 
    Jul 26 20:30:57  abc logger: transfer-file: Transferred /var/transfer/config/abc_juniper.conf.gz_20130726_203043

    [edit]
    lab@abc# run show system configuration archival  

    /var/transfer/config/:
    total blocks: 8
    total files: 0

### QUESTION

this looks succeed, but actually not working (no file a/v in the server)

    [edit]
    lab@MX80-NGGWR-01# save scp://Ping@172.25.84.169:transfer-on-commit/abc.txt    
    Ping@172.25.84.169's password:  
    tempfile 0%    0 tempfile     100%  163KB 162.7KB/s   00:00    
    Wrote 5444 lines of configuration to 'scp://Ping@172.25.84.169:transfer-on-commit/abc.txt'


## IGP

### DC => R2 => all Rs

.R2 learned routes from DC

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

.R2 then adv via ISIS to all internal Rs

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
       IP prefix: 172.16.8.0/21                   Metric:       10 External Up
       IP prefix: 172.16.16.0/22                  Metric:       10 External Up

### R2 => DC

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


### ipv6


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

    [edit]
    lab@MX80-NGGWR-01# run show route receive-protocol bgp 192.168.34.0 logical-system lr7 table inet6.0 extensive           

    inet6.0: 8 destinations, 15 routes (3 active, 0 holddown, 10 hidden)
    Restart Complete
    * 4444:4444:4444::/48 (1 entry, 1 announced)
         Accepted
         Nexthop: ::ffff:192.168.34.0   <------ ?not working?
         AS path: 400 I

#### QUESTION: next-hop peer-address didn't really change the nexthop?

#### how C routers got the IPv6 routes? 

"accept-remote-nexthop" must have been pre-configured


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

#### change next-hop to local IPv6 address of export policy in LR 

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

#### install R7/8 host

lr2/lr3:

    //before:
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

    //after:
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



