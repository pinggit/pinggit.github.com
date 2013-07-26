
* auto-gen TOC:
{:toc}

# issues

LSANCA-VFTTP-301 and NYCMNY-VFTTP-312 have both crashed. NYCMNY-VFTTP-303
dropped 0.5MB in a day. PRVDRI-VFTTP-302 and PRVDRI-VFTTP-303 look ok so far
but maybe it’s because there has been less NWG activity?

# ralated PR/cases

2013-0612-1000 PR777765 661685

# pending issue

<!--

how to config query-pr

-->

# log infos

## show system core-dumps

    z427047@LSANCA-VFTTP-301_RE0> show system core-dumps  
    -rw-r--r--  1 root  wheel   55254626 Jun 15 15:24 /var/crash/core-NPC0.gz.core.1
    -rw-r--r--  1 root  wheel   55755670 Jun 15 15:24 /var/crash/core-NPC1.gz.core.0

## show syslog messages (FPC0)

    NPC0(LSANCA-VFTTP-301_RE0 uart0)# show syslog messages
    [Jun 15 15:26:31.408 LOG: Debug] hsl2_avago_65nm_link_power: Starting RX MQCHIP(1)-Avago 65NM-link-102  71
    [Jun 15 15:26:31.408 LOG: Debug] hsl2_avago_65nm_link_power: Starting RX MQCHIP(1)-Avago 65NM-link-103  72
    [Jun 15 15:26:31.409 LOG: Debug]  hsl2_primitive_channel_init pfe 1, plane 5 ,mq_phy_plane 1 tx channel 36 rx channel 8 
    [Jun 15 15:26:31.409 LOG: Debug] hsl2_avago_65nm_link_power: Starting TX MQCHIP(1)-Avago 65NM-link-52  53
    [Jun 15 15:26:31.418 LOG: Debug] hsl2_avago_65nm_link_power: Starting TX MQCHIP(1)-Avago 65NM-link-53  54
    [Jun 15 15:26:31.426 LOG: Debug] hsl2_avago_65nm_link_power: Starting TX MQCHIP(1)-Avago 65NM-link-54  55
    [Jun 15 15:26:31.435 LOG: Debug] hsl2_avago_65nm_link_power: Starting TX MQCHIP(1)-Avago 65NM-link-55  56
    [Jun 15 15:26:31.444 LOG: Debug] hsl2_avago_65nm_link_power: Starting RX MQCHIP(1)-Avago 65NM-link-84  53
    [Jun 15 15:26:31.444 LOG: Debug] hsl2_avago_65nm_link_power: Starting RX MQCHIP(1)-Avago 65NM-link-85  54
    [Jun 15 15:26:31.444 LOG: Debug] hsl2_avago_65nm_link_power: Starting RX MQCHIP(1)-Avago 65NM-link-86  55
    [Jun 15 15:26:31.444 LOG: Debug] hsl2_avago_65nm_link_power: Starting RX MQCHIP(1)-Avago 65NM-link-87  56
    [Jun 15 15:26:31.494 LOG: Debug] hsl2_primitive_channel_train_rx pfe 1, plane 1 , mq_phy_plane 3 rx channel 15 
    [Jun 15 15:26:31.494 LOG: Debug] hsl2_primitive_channel_start_tx pfe 1, plane 1 ,mq_phy_plane 3 , tx chan 43
    [Jun 15 15:26:31.494 LOG: Debug] hsl2_primitive_channel_train_rx pfe 1, plane 3 , mq_phy_plane 5 rx channel 22 
    [Jun 15 15:26:31.495 LOG: Debug] hsl2_primitive_channel_start_tx pfe 1, plane 3 ,mq_phy_plane 5 , tx chan 50
    [Jun 15 15:26:31.495 LOG: Debug] hsl2_primitive_channel_train_rx pfe 1, plane 5 , mq_phy_plane 1 rx channel 8 
    [Jun 15 15:26:31.496 LOG: Debug] hsl2_primitive_channel_start_tx pfe 1, plane 5 ,mq_phy_plane 1 , tx chan 36
    [Jun 15 15:26:31.496 LOG: Debug] hsl2_primitive_channel_enable_tx pfe 1, plane 1 ,mq_phy_plane 3 tx channel 43 
    [Jun 15 15:26:31.496 LOG: Debug] hsl2_primitive_channel_enable_tx pfe 1, plane 3 ,mq_phy_plane 5 tx channel 50 
    [Jun 15 15:26:31.496 LOG: Debug] hsl2_primitive_channel_enable_tx pfe 1, plane 5 ,mq_phy_plane 1 tx channel 36 
    [Jun 15 15:26:31.562 LOG: Debug] CMTFPC: enabling fabric streams L 0, H 128 pfe index 0 
    [Jun 15 15:26:31.562 LOG: Debug] CMTFPC: enabling fabric streams L 0, H 128 pfe index 1 
    [Jun 15 15:26:31.563 LOG: Info] PFE[0]Aliveness Turning Destination 0 on
    [Jun 15 15:26:31.563 LOG: Info] PFE[1]Aliveness Turning Destination 0 on
    [Jun 15 15:26:31.564 LOG: Debug] CMTFPC: enabling fabric streams L 1, H 129 pfe index 0 
    [Jun 15 15:26:31.564 LOG: Debug] CMTFPC: enabling fabric streams L 1, H 129 pfe index 1 
    [Jun 15 15:26:31.564 LOG: Info] PFE[0]Aliveness Turning Destination 1 on
    [Jun 15 15:26:31.565 LOG: Info] PFE[1]Aliveness Turning Destination 1 on
    [Jun 15 15:26:31.566 LOG: Debug] CMTFPC: enabling fabric streams L 4, H 132 pfe index 0 
    [Jun 15 15:26:31.566 LOG: Debug] CMTFPC: enabling fabric streams L 4, H 132 pfe index 1 
    [Jun 15 15:26:31.566 LOG: Info] PFE[0]Aliveness Turning Destination 4 on
    [Jun 15 15:26:31.566 LOG: Info] PFE[1]Aliveness Turning Destination 4 on
    [Jun 15 15:26:31.567 LOG: Debug] CMTFPC: enabling fabric streams L 5, H 133 pfe index 0 
    [Jun 15 15:26:31.567 LOG: Debug] CMTFPC: enabling fabric streams L 5, H 133 pfe index 1 
    [Jun 15 15:26:31.567 LOG: Info] PFE[0]Aliveness Turning Destination 5 on
    [Jun 15 15:26:31.568 LOG: Info] PFE[1]Aliveness Turning Destination 5 on
    [Jun 15 15:26:31.569 LOG: Debug] CMTFPC: enabling fabric streams L 40, H 168 pfe index 0 
    [Jun 15 15:26:31.569 LOG: Debug] CMTFPC: enabling fabric streams L 40, H 168 pfe index 1 
    [Jun 15 15:26:31.571 LOG: Debug] CMTFPC: enabling fabric streams L 41, H 169 pfe index 0 
    [Jun 15 15:26:31.572 LOG: Debug] CMTFPC: enabling fabric streams L 41, H 169 pfe index 1 
    [Jun 15 15:26:31.574 LOG: Debug] CMTFPC: enabling fabric streams L 44, H 172 pfe index 0 
    [Jun 15 15:26:31.574 LOG: Debug] CMTFPC: enabling fabric streams L 44, H 172 pfe index 1 
    [Jun 15 15:26:31.576 LOG: Debug] CMTFPC: enabling fabric streams L 45, H 173 pfe index 0 
    [Jun 15 15:26:31.577 LOG: Debug] CMTFPC: enabling fabric streams L 45, H 173 pfe index 1 
    [Jun 15 15:26:33.473 LOG: Notice] MIC(0/0) link 4 SFP receive power low  alarm set
    [Jun 15 15:26:33.473 LOG: Notice] MIC(0/0) link 4 SFP receive power low  warning set
    [Jun 15 15:26:33.477 LOG: Notice] MIC(0/0) link 5 SFP receive power low  alarm set
    [Jun 15 15:26:33.477 LOG: Notice] MIC(0/0) link 5 SFP receive power low  warning set
    [Jun 15 15:26:33.482 LOG: Notice] MIC(0/0) link 6 SFP receive power low  alarm set
    [Jun 15 15:26:33.482 LOG: Notice] MIC(0/0) link 6 SFP receive power low  warning set
    [Jun 15 15:26:33.486 LOG: Notice] MIC(0/0) link 7 SFP receive power low  alarm set
    [Jun 15 15:26:33.486 LOG: Notice] MIC(0/0) link 7 SFP receive power low  warning set
    [Jun 15 15:26:33.497 LOG: Notice] MIC(0/1) link 0 SFP receive power low  alarm set
    [Jun 15 15:26:33.497 LOG: Notice] MIC(0/1) link 0 SFP receive power low  warning set
    [Jun 15 15:26:33.501 LOG: Notice] MIC(0/1) link 1 SFP receive power low  alarm set
    [Jun 15 15:26:33.501 LOG: Notice] MIC(0/1) link 1 SFP receive power low  warning set
    [Jun 15 15:26:33.506 LOG: Notice] MIC(0/1) link 2 SFP receive power low  alarm set
    [Jun 15 15:26:33.506 LOG: Notice] MIC(0/1) link 2 SFP receive power low  warning set
    [Jun 15 15:26:33.510 LOG: Notice] MIC(0/1) link 3 SFP receive power low  alarm set
    [Jun 15 15:26:33.510 LOG: Notice] MIC(0/1) link 3 SFP receive power low  warning set
    [Jun 15 15:26:33.514 LOG: Notice] MIC(0/1) link 4 SFP receive power low  alarm set
    [Jun 15 15:26:33.514 LOG: Notice] MIC(0/1) link 4 SFP receive power low  warning set
    [Jun 15 15:26:33.518 LOG: Notice] MIC(0/1) link 5 SFP receive power low  alarm set
    [Jun 15 15:26:33.518 LOG: Notice] MIC(0/1) link 5 SFP receive power low  warning set
    [Jun 15 15:26:33.522 LOG: Notice] MIC(0/1) link 6 SFP receive power low  alarm set
    [Jun 15 15:26:33.522 LOG: Notice] MIC(0/1) link 6 SFP receive power low  warning set
    [Jun 15 15:26:33.526 LOG: Notice] MIC(0/1) link 7 SFP receive power low  alarm set
    [Jun 15 15:26:33.526 LOG: Notice] MIC(0/1) link 7 SFP receive power low  warning set
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/0, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/1, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/2, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/3, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/4, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/5, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/6, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/7, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/8, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/9, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/0, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/1, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/2, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/3, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/4, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/5, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/6, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/7, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/8, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/9, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:xe-0/2/0, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:xe-0/2/1, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:xe-0/3/0, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:40.234 LOG: Debug] UPDN msg to kernel for ifd:xe-0/3/1, flag:2, speed: 0, duplex:0
    [Jun 15 15:27:29.429 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/0, flag:1, speed: 0, duplex:0
    [Jun 15 15:27:56.407 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/1, flag:1, speed: 0, duplex:0
    [Jun 15 15:27:57.407 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/2, flag:1, speed: 0, duplex:0
    [Jun 15 15:28:21.015 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/3, flag:1, speed: 0, duplex:0
    [Jun 15 15:28:38.019 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/8, flag:1, speed: 0, duplex:0
    [Jun 15 15:28:38.019 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/8, flag:1, speed: 0, duplex:0
    [Jun 15 15:28:42.055 LOG: Debug] UPDN msg to kernel for ifd:ge-0/0/9, flag:1, speed: 0, duplex:0
    [Jun 15 15:28:42.055 LOG: Debug] UPDN msg to kernel for ifd:ge-0/1/9, flag:1, speed: 0, duplex:0
       

## show nvram (FPC0)

    NPC0(LSANCA-VFTTP-301_RE0 vty)# show nvram
    System NVRAM :
     32751 available bytes, 32751 used, 0 free
     Contents:

    mory, dwords 524288
    [Jun 15 15:21:41.361 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:41.361 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x561 add_prefix_tbl failed, status 8
    [Jun 15 15:21:41.420 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:41.832 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:41.832 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:41.832 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x134f add_prefix_tbl failed, status 8
    [Jun 15 15:21:42.009 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:42.071 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:42.215 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:42.276 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:42.583 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:42.583 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:42.642 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:42.791 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:42.973 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.008 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.145 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:43.269 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.407 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.551 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.686 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:43.897 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.956 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:44.296 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:44.296 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:44.355 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:44.495 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:44.573 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:44.840 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:44.840 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, ktree does not have enough room
    [Jun 15 15:21:44.962 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:45.240 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:45.240 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:45.384 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:45.470 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:45.594 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:45.885 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:45.885 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:45.956 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:46.116 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:46.240 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:46.324 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:46.494 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:47.270 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:47.270 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:47.270 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x392 add_prefix_tbl failed, status 8
    [Jun 15 15:21:47.287 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:47.287 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:47.287 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0xa10 add_prefix_tbl failed, status 8
    [Jun 15 15:21:47.382 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:47.583 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:47.642 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:47.756 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:47.944 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:48.232 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:48.232 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:48.232 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x392 add_prefix_tbl failed, status 8
    [Jun 15 15:21:48.387 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:48.510 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:48.753 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:48.753 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:49.374 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:49.374 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:49.374 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x7f9 add_prefix_tbl failed, status 8
    [Jun 15 15:21:49.401 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:49.401 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:49.626 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:49.626 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:49.766 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:49.923 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:50.007 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:50.511 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:50.511 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:50.511 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x424 add_prefix_tbl failed, status 8
    [Jun 15 15:21:50.553 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:51.107 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:51.107 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:51.107 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x22ee add_prefix_tbl failed, status 8
    [Jun 15 15:21:51.167 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:51.305 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:51.305 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:51.458 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:51.568 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:51.945 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:51.945 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:52.013 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:52.478 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:52.478 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:52.478 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0xbea add_prefix_tbl failed, status 8
    [Jun 15 15:21:52.540 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:52.780 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:52.780 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:52.839 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:53.001 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:53.108 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:53.369 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:53.369 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:53.481 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:53.588 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:55.043 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:55.043 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:55.043 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x3998 add_prefix_tbl failed, status 8
    [Jun 15 15:21:55.102 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:55.102 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, ktree does not have enough room
    [Jun 15 15:21:55.102 LOG: Err] <163>RT-HAL,rt_entry_add_msg_proc,2366: rt_halp_vectors->rt_create failed
    [Jun 15 15:21:55.102 LOG: Err] <163>RT-HAL,rt_entry_add_msg_proc,2416: proto ipv4,len 64 prefix 232.192.0.0.96.228.255.75/64 nh 1049690
    [Jun 15 15:21:55.102 LOG: Err] <163>RT-HAL,rt_msg_handler,580: route process failed
    [Jun 15 15:21:55.264 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:55.264 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:55.264 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x6cc add_prefix_tbl failed, status 8
    [Jun 15 15:21:55.283 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:55.283 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:55.322 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:55.525 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:55.584 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:56.351 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:56.351 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:56.351 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x2709 add_prefix_tbl failed, status 8
    [Jun 15 15:21:56.410 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:56.410 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, ktree does not have enough room
    [Jun 15 15:21:56.410 LOG: Err] <163>RT-HAL,rt_entry_add_msg_proc,2366: rt_halp_vectors->rt_create failed
    [Jun 15 15:21:56.469 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:56.646 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:56.829 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:56.888 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:57.042 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:57.104 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:57.327 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:57.395 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:57.498 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:57.727 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:57.727 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:57.857 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:58.115 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:58.115 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:58.284 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:58.393 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:58.525 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:58.797 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:58.797 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:59.051 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.083 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.143 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:59.272 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.429 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.566 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.753 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.812 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:59.916 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:00.170 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:00.170 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:00.243 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:00.384 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:00.538 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:00.854 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:00.854 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:00.905 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:01.023 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:01.149 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:01.270 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:01.421 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:01.527 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:01.678 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:01.816 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:01.915 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:02.171 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:02.171 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:02.356 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:02.415 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:02.588 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:02.944 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:02.944 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:02.944 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x8e1 add_prefix_tbl failed, status 8
    [Jun 15 15:22:03.186 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:03.186 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:03.460 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:03.460 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:03.596 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:03.717 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:03.795 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:03.985 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:04.043 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:04.184 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:04.630 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:04.630 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:04.630 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x5fb add_prefix_tbl failed, status 8
    [Jun 15 15:22:04.695 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:05.105 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:05.105 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:05.105 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x6cb add_prefix_tbl failed, status 8
    [Jun 15 15:22:05.171 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:05.456 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:05.456 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:05.595 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:05.654 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:05.803 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:05.959 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:06.255 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:06.255 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:06.298 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:06.439 LOG: Err] <163>RT-HAL,rt_msg_handler,565: route check failed
    [Jun 15 15:22:06.594 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:06.768 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:06.827 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:07.049 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:07.127 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:07.249 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:07.658 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:07.658 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:07.658 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x6b4 add_prefix_tbl failed, status 8
    [Jun 15 15:22:07.780 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:07.903 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:08.437 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:08.437 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:08.437 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x78b add_prefix_tbl failed, status 8
    [Jun 15 15:22:08.441 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:08.827 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:08.827 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:08.827 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0xc47 add_prefix_tbl failed, status 8
    [Jun 15 15:22:08.956 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:09.063 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:09.191 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:09.307 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:09.462 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:09.816 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:09.816 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:09.816 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x3248 add_prefix_tbl failed, status 8
    [Jun 15 15:22:09.986 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:10.111 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:10.451 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:10.452 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:10.510 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:10.646 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:10.886 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:10.886 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:11.059 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:11.119 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:11.271 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:11.625 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:11.625 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:11.625 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0xa21 add_prefix_tbl failed, status 8
    [Jun 15 15:22:11.870 LOG: Err] <163>jnh_call_init(1859): Failed to allocate 2 entries
    [Jun 15 15:22:11.871 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [LOG] -----------------------------------------------------
          PANIC PANIC PANIC PANIC PANIC PANIC PANIC PANIC PANIC
          (caller pc: 0x402e09f4)

    [Jun 15 15:21:07.170 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288

    System Exception: Vector/Code 0x00900, Signal -1
    Event occurred at: Jun 15 15:23:24.993507 

    Juniper Embedded Microkernel Version 11.2S7.4
    Built by builder on 2013-01-09 22:37:02 UTC
    Copyright (C) 1998-2013, Juniper Networks, Inc.
    All rights reserved.
    Reason string: "Panic"
    Context: Thread (PFE Manager)

    Registers:
    R00: 0x4003f1cc R01: 0x4384a610 R02: 0x43846da0 R03: 0x0000005d 
    R04: 0x00000000 R05: 0x4384a618 R06: 0x00000000 R07: 0x20000000 
    R08: 0x4384a543 R09: 0x0000005d R10: 0x4384ae00 R11: 0x41240000 
    R12: 0x44022022 R13: 0xcfa6cc96 R14: 0x4165efc0 R15: 0x4165efc0 
    R16: 0x4165efc0 R17: 0x410d8de0 R18: 0x4384a6c0 R19: 0x40fa0000 
    R20: 0x40cd0000 R21: 0x00000000 R22: 0x00000001 R23: 0x4384a6c8 
    R24: 0x00000001 R25: 0x27fffff8 R26: 0x0000000c R27: 0x57cf4510 
    R28: 0x00000001 R29: 0x00000000 R30: 0x402e09f4 R31: 0x40e50c5c 
    MSR: 0x00029200 CTR: 0x000ee9a4 Link: 0x4003f1cc SP: 0x4384a610
     CR: 0x44022082 XER: 0x20000000 DEAR: 0x00000000 PC: 0x4003f1d0
    ESR: 0x00000000 K_MSR: 0x00021200

    Stack Traceback:
    Frame 01: sp = 0x4384a610, pc = 0x4003f1cc
    Frame 02: sp = 0x4384a658, pc = 0x402e09f4
    Frame 03: sp = 0x4384a6a8, pc = 0x4082de08
    Frame 04: sp = 0x4384a840, pc = 0x4082f120
    Frame 05: sp = 0x4384a898, pc = 0x40830084
    Frame 06: sp = 0x4384a8d8, pc = 0x408305e8
    Frame 07: sp = 0x4384a930, pc = 0x4081f864
    Frame 08: sp = 0x4384a988, pc = 0x407f5b84
    Frame 09: sp = 0x4384ab78, pc = 0x407da0c0
    Frame 10: sp = 0x4384acc0, pc = 0x406e2220
    Frame 11: sp = 0x4384ace0, pc = 0x406e5e24
    Frame 12: sp = 0x4384ad98, pc = 0x4002e2ac

    [LOG] syslog called with interrupts off (caller pc:0x4005cd84)
    [LOG] Registered network packet handlers
    [LOG] syslog called with interrupts off (caller pc:0x40a47018)
    [LOG] Dumping core-NPC0 to 1
    [LOG] syslog called with interrupts off (caller pc:0x40a45d6c)
    [LOG] Coredump finished[LOG] chassis_db_set_dpc_simulation: options = 0!!
    [LOG] Set the IP IRI for table #1 to 0x80000010
    [LOG] IPV4 Init: Set the IP IRI to 0x80000010
    [LOG] if_notify_init: IF notify list already initialized 

    MPC: Reset reason (0x0): No reason?


    ROM NVRAM:
     0 available bytes, 0 used, 0 free

    NPC0(LSANCA-VFTTP-301_RE0 vty)# exit



## show syslog messages (FPC1)

    NPC1(LSANCA-VFTTP-301_RE0 vty)# show syslog messages
    [Jun 15 15:26:30.522 LOG: Debug] hsl2_avago_65nm_link_power: Starting TX MQCHIP(1)-Avago 65NM-link-52  53
    [Jun 15 15:26:30.531 LOG: Debug] hsl2_avago_65nm_link_power: Starting TX MQCHIP(1)-Avago 65NM-link-53  54
    [Jun 15 15:26:30.539 LOG: Debug] hsl2_avago_65nm_link_power: Starting TX MQCHIP(1)-Avago 65NM-link-54  55
    [Jun 15 15:26:30.548 LOG: Debug] hsl2_avago_65nm_link_power: Starting TX MQCHIP(1)-Avago 65NM-link-55  56
    [Jun 15 15:26:30.557 LOG: Debug] hsl2_avago_65nm_link_power: Starting RX MQCHIP(1)-Avago 65NM-link-84  53
    [Jun 15 15:26:30.557 LOG: Debug] hsl2_avago_65nm_link_power: Starting RX MQCHIP(1)-Avago 65NM-link-85  54
    [Jun 15 15:26:30.557 LOG: Debug] hsl2_avago_65nm_link_power: Starting RX MQCHIP(1)-Avago 65NM-link-86  55
    [Jun 15 15:26:30.557 LOG: Debug] hsl2_avago_65nm_link_power: Starting RX MQCHIP(1)-Avago 65NM-link-87  56
    [Jun 15 15:26:30.600 LOG: Debug] hsl2_primitive_channel_train_rx pfe 1, plane 1 , mq_phy_plane 3 rx channel 15 
    [Jun 15 15:26:30.601 LOG: Debug] hsl2_primitive_channel_start_tx pfe 1, plane 1 ,mq_phy_plane 3 , tx chan 43
    [Jun 15 15:26:30.601 LOG: Debug] hsl2_primitive_channel_train_rx pfe 1, plane 3 , mq_phy_plane 5 rx channel 22 
    [Jun 15 15:26:30.601 LOG: Debug] hsl2_primitive_channel_start_tx pfe 1, plane 3 ,mq_phy_plane 5 , tx chan 50
    [Jun 15 15:26:30.602 LOG: Debug] hsl2_primitive_channel_train_rx pfe 1, plane 5 , mq_phy_plane 1 rx channel 8 
    [Jun 15 15:26:30.602 LOG: Debug] hsl2_primitive_channel_start_tx pfe 1, plane 5 ,mq_phy_plane 1 , tx chan 36
    [Jun 15 15:26:30.602 LOG: Debug] hsl2_primitive_channel_enable_tx pfe 1, plane 1 ,mq_phy_plane 3 tx channel 43 
    [Jun 15 15:26:30.602 LOG: Debug] hsl2_primitive_channel_enable_tx pfe 1, plane 3 ,mq_phy_plane 5 tx channel 50 
    [Jun 15 15:26:30.602 LOG: Debug] hsl2_primitive_channel_enable_tx pfe 1, plane 5 ,mq_phy_plane 1 tx channel 36 
    [Jun 15 15:26:30.633 LOG: Debug] CMTFPC: enabling fabric streams L 4, H 132 pfe index 0 
    [Jun 15 15:26:30.633 LOG: Debug] CMTFPC: enabling fabric streams L 4, H 132 pfe index 1 
    [Jun 15 15:26:30.633 LOG: Info] PFE[0]Aliveness Turning Destination 4 on
    [Jun 15 15:26:30.634 LOG: Info] PFE[1]Aliveness Turning Destination 4 on
    [Jun 15 15:26:30.635 LOG: Debug] CMTFPC: enabling fabric streams L 5, H 133 pfe index 0 
    [Jun 15 15:26:30.635 LOG: Debug] CMTFPC: enabling fabric streams L 5, H 133 pfe index 1 
    [Jun 15 15:26:30.635 LOG: Info] PFE[0]Aliveness Turning Destination 5 on
    [Jun 15 15:26:30.636 LOG: Info] PFE[1]Aliveness Turning Destination 5 on
    [Jun 15 15:26:30.636 LOG: Debug] CMTFPC: enabling fabric streams L 40, H 168 pfe index 0 
    [Jun 15 15:26:30.637 LOG: Debug] CMTFPC: enabling fabric streams L 40, H 168 pfe index 1 
    [Jun 15 15:26:30.639 LOG: Debug] CMTFPC: enabling fabric streams L 41, H 169 pfe index 0 
    [Jun 15 15:26:30.640 LOG: Debug] CMTFPC: enabling fabric streams L 41, H 169 pfe index 1 
    [Jun 15 15:26:30.641 LOG: Debug] CMTFPC: enabling fabric streams L 44, H 172 pfe index 0 
    [Jun 15 15:26:30.642 LOG: Debug] CMTFPC: enabling fabric streams L 44, H 172 pfe index 1 
    [Jun 15 15:26:30.644 LOG: Debug] CMTFPC: enabling fabric streams L 45, H 173 pfe index 0 
    [Jun 15 15:26:30.645 LOG: Debug] CMTFPC: enabling fabric streams L 45, H 173 pfe index 1 
    [Jun 15 15:26:30.699 LOG: Notice] xfp-1/3/0 plugged in
    [Jun 15 15:26:31.550 LOG: Debug] CMTFPC: enabling fabric streams L 0, H 128 pfe index 0 
    [Jun 15 15:26:31.550 LOG: Debug] CMTFPC: enabling fabric streams L 0, H 128 pfe index 1 
    [Jun 15 15:26:31.550 LOG: Info] PFE[0]Aliveness Turning Destination 0 on
    [Jun 15 15:26:31.551 LOG: Info] PFE[1]Aliveness Turning Destination 0 on
    [Jun 15 15:26:31.551 LOG: Debug] CMTFPC: enabling fabric streams L 1, H 129 pfe index 0 
    [Jun 15 15:26:31.552 LOG: Debug] CMTFPC: enabling fabric streams L 1, H 129 pfe index 1 
    [Jun 15 15:26:31.552 LOG: Info] PFE[0]Aliveness Turning Destination 1 on
    [Jun 15 15:26:31.552 LOG: Info] PFE[1]Aliveness Turning Destination 1 on
    [Jun 15 15:26:35.483 LOG: Notice] MIC(1/0) link 4 SFP receive power low  alarm set
    [Jun 15 15:26:35.483 LOG: Notice] MIC(1/0) link 4 SFP receive power low  warning set
    [Jun 15 15:26:35.487 LOG: Notice] MIC(1/0) link 5 SFP receive power low  alarm set
    [Jun 15 15:26:35.487 LOG: Notice] MIC(1/0) link 5 SFP receive power low  warning set
    [Jun 15 15:26:35.491 LOG: Notice] MIC(1/0) link 6 SFP receive power low  alarm set
    [Jun 15 15:26:35.491 LOG: Notice] MIC(1/0) link 6 SFP receive power low  warning set
    [Jun 15 15:26:35.495 LOG: Notice] MIC(1/0) link 7 SFP receive power low  alarm set
    [Jun 15 15:26:35.495 LOG: Notice] MIC(1/0) link 7 SFP receive power low  warning set
    [Jun 15 15:26:35.507 LOG: Notice] MIC(1/1) link 0 SFP receive power low  alarm set
    [Jun 15 15:26:35.507 LOG: Notice] MIC(1/1) link 0 SFP receive power low  warning set
    [Jun 15 15:26:35.511 LOG: Notice] MIC(1/1) link 1 SFP receive power low  alarm set
    [Jun 15 15:26:35.511 LOG: Notice] MIC(1/1) link 1 SFP receive power low  warning set
    [Jun 15 15:26:35.516 LOG: Notice] MIC(1/1) link 2 SFP receive power low  alarm set
    [Jun 15 15:26:35.516 LOG: Notice] MIC(1/1) link 2 SFP receive power low  warning set
    [Jun 15 15:26:35.520 LOG: Notice] MIC(1/1) link 3 SFP receive power low  alarm set
    [Jun 15 15:26:35.520 LOG: Notice] MIC(1/1) link 3 SFP receive power low  warning set
    [Jun 15 15:26:35.524 LOG: Notice] MIC(1/1) link 4 SFP receive power low  alarm set
    [Jun 15 15:26:35.524 LOG: Notice] MIC(1/1) link 4 SFP receive power low  warning set
    [Jun 15 15:26:35.528 LOG: Notice] MIC(1/1) link 5 SFP receive power low  alarm set
    [Jun 15 15:26:35.528 LOG: Notice] MIC(1/1) link 5 SFP receive power low  warning set
    [Jun 15 15:26:35.532 LOG: Notice] MIC(1/1) link 6 SFP receive power low  alarm set
    [Jun 15 15:26:35.532 LOG: Notice] MIC(1/1) link 6 SFP receive power low  warning set
    [Jun 15 15:26:35.536 LOG: Notice] MIC(1/1) link 7 SFP receive power low  alarm set
    [Jun 15 15:26:35.536 LOG: Notice] MIC(1/1) link 7 SFP receive power low  warning set
    [Jun 15 15:26:35.551 LOG: Notice] MIC(1/1) link 8 SFP receive power low  alarm set
    [Jun 15 15:26:35.551 LOG: Notice] MIC(1/1) link 8 SFP receive power low  warning set
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/0, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/1, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/2, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/3, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/4, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/5, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/6, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/7, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/8, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/9, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/0, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/1, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/2, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/3, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/4, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/5, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/6, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/7, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/8, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/9, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:xe-1/2/0, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:xe-1/2/1, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:xe-1/3/0, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.428 LOG: Debug] UPDN msg to kernel for ifd:xe-1/3/1, flag:2, speed: 0, duplex:0
    [Jun 15 15:26:41.837 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/0, flag:1, speed: 0, duplex:0
    [Jun 15 15:26:55.626 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/1, flag:1, speed: 0, duplex:0
    [Jun 15 15:26:56.619 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/2, flag:1, speed: 0, duplex:0
    [Jun 15 15:27:18.225 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/3, flag:1, speed: 0, duplex:0
    [Jun 15 15:27:33.226 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/8, flag:1, speed: 0, duplex:0
    [Jun 15 15:27:37.249 LOG: Debug] UPDN msg to kernel for ifd:ge-1/0/9, flag:1, speed: 0, duplex:0
    [Jun 15 15:28:38.233 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/8, flag:1, speed: 0, duplex:0
    [Jun 15 15:28:42.246 LOG: Debug] UPDN msg to kernel for ifd:ge-1/1/9, flag:1, speed: 0, duplex:0

## show nvram (FPC1)
    NPC1(LSANCA-VFTTP-301_RE0 vty)# show nvram
    System NVRAM :
     32751 available bytes, 32751 used, 0 free
     Contents:

    1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:41.358 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:41.418 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:41.830 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:41.830 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:41.830 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x134f add_prefix_tbl failed, status 8
    [Jun 15 15:21:41.888 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:42.068 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:42.211 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:42.273 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:42.581 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:42.581 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:42.640 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:42.730 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:42.869 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:42.970 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.123 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.266 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.404 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.516 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:43.624 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.894 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:43.894 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:44.293 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:44.293 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:44.293 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x21f1 add_prefix_tbl failed, status 8
    [Jun 15 15:21:44.433 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:44.512 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:44.669 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:44.837 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:44.959 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:45.238 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:45.238 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:45.297 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:45.441 LOG: Err] <163>RT-HAL,rt_msg_handler,565: route check failed
    [Jun 15 15:21:45.591 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:45.882 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:45.882 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:45.953 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:46.070 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:46.175 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:46.282 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:46.432 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:46.576 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:47.267 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:47.267 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:47.267 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x392 add_prefix_tbl failed, status 8
    [Jun 15 15:21:47.285 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:47.285 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:47.326 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:47.438 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:47.580 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:47.713 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:47.877 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:47.941 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:48.232 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:48.232 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:48.297 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:48.427 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:48.753 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:48.753 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:48.810 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:49.372 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:49.372 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:49.372 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x7f9 add_prefix_tbl failed, status 8
    [Jun 15 15:21:49.398 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:49.436 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:49.624 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:49.701 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:49.920 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:49.945 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:50.508 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:50.508 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:50.508 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x424 add_prefix_tbl failed, status 8
    [Jun 15 15:21:50.550 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:50.609 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:51.104 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:51.104 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:51.104 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x22ee add_prefix_tbl failed, status 8
    [Jun 15 15:21:51.164 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:51.302 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:51.504 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:51.504 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:51.943 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:51.943 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:51.943 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x309e add_prefix_tbl failed, status 8
    [Jun 15 15:21:52.003 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:52.475 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:52.475 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:52.475 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0xbea add_prefix_tbl failed, status 8
    [Jun 15 15:21:52.537 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:52.778 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:52.778 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:52.999 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:53.043 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:53.366 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:53.367 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:53.439 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:53.525 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:55.040 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:55.040 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:55.040 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x3998 add_prefix_tbl failed, status 8
    [Jun 15 15:21:55.100 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:55.100 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, ktree does not have enough room
    [Jun 15 15:21:55.100 LOG: Err] <163>RT-HAL,rt_entry_add_msg_proc,2366: rt_halp_vectors->rt_create failed
    [Jun 15 15:21:55.100 LOG: Err] <163>RT-HAL,rt_entry_add_msg_proc,2416: proto ipv4,len 64 prefix 232.192.0.0.96.228.255.75/64 nh 1049690
    [Jun 15 15:21:55.100 LOG: Err] <163>RT-HAL,rt_msg_handler,580: route process failed
    [Jun 15 15:21:55.261 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:55.261 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:55.261 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x6cc add_prefix_tbl failed, status 8
    [Jun 15 15:21:55.280 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:55.280 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:55.280 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0xb5b add_prefix_tbl failed, status 8
    [Jun 15 15:21:55.339 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:55.522 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:56.348 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:56.348 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:56.348 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x2709 add_prefix_tbl failed, status 8
    [Jun 15 15:21:56.407 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:56.407 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, ktree does not have enough room
    [Jun 15 15:21:56.407 LOG: Err] <163>RT-HAL,rt_entry_add_msg_proc,2366: rt_halp_vectors->rt_create failed
    [Jun 15 15:21:56.407 LOG: Err] <163>RT-HAL,rt_entry_add_msg_proc,2416: proto ipv4,len 64 prefix 232.192.0.0.96.228.255.19/64 nh 1049690
    [Jun 15 15:21:56.498 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:56.643 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:56.826 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:56.885 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:57.040 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:57.268 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:57.268 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:57.397 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:57.495 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:57.725 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:57.784 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:57.893 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:58.112 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:58.112 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:58.281 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:58.447 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:58.522 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:58.786 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:58.786 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:59.040 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.040 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:21:59.140 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:59.269 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.426 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.526 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.640 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:59.809 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:21:59.914 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:21:59.974 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:00.167 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:00.240 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:00.381 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:00.536 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:00.851 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:00.851 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:00.902 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:01.020 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:01.146 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:01.285 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:01.413 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:01.525 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:01.676 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:01.813 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:01.912 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:02.216 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:02.269 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:02.269 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, ktree does not have enough room
    [Jun 15 15:22:02.413 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:02.527 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:02.655 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:02.942 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:02.942 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:03.183 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:03.183 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:03.457 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:03.457 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:03.593 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:03.715 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:03.857 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:03.983 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:04.088 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:04.181 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:04.627 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:04.627 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:04.627 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x5fb add_prefix_tbl failed, status 8
    [Jun 15 15:22:05.102 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:05.102 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:05.102 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x6cb add_prefix_tbl failed, status 8
    [Jun 15 15:22:05.161 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:05.193 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:05.453 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:05.513 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:05.592 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:05.726 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:05.859 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:06.014 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:06.253 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:06.253 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:06.476 LOG: Err] <163>RT-HAL,rt_msg_handler,565: route check failed
    [Jun 15 15:22:06.591 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:06.654 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:06.765 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:06.911 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:07.046 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:07.183 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:07.656 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:07.656 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:07.656 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x6b4 add_prefix_tbl failed, status 8
    [Jun 15 15:22:07.715 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:07.838 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:07.932 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:08.435 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:08.435 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:08.435 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x78b add_prefix_tbl failed, status 8
    [Jun 15 15:22:08.498 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:08.825 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:08.825 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:08.884 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:09.012 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:09.120 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:09.245 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:09.401 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:09.813 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:09.813 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:09.813 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x3248 add_prefix_tbl failed, status 8
    [Jun 15 15:22:09.858 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:10.049 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:10.449 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:10.449 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:10.449 LOG: Err] <163>jnh_vc_mtoken_add(741): pfe 1: token 0x7b4 add_prefix_tbl failed, status 8
    [Jun 15 15:22:10.508 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:10.644 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:10.884 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:10.884 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:11.057 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:11.268 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:11.268 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:11.623 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288
    [Jun 15 15:22:11.623 LOG: Err] <163>jnh_add_prefix_table(302): Table Partition, fast-memory does not have enough room
    [Jun 15 15:22:11.685 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app ktree, dwords 524288
    [Jun 15 15:22:11.850 LOG: Err] <163>jnh_call_init(1859): Failed to allocate 2 entries
    [Jun 15 15:22:11.909 LOG: Err] <163>jnh_ptable_init(105): Failed to allocate DMEM
    [LOG] -----------------------------------------------------
          PANIC PANIC PANIC PANIC PANIC PANIC PANIC PANIC PANIC
          (caller pc: 0x402e09f4)

    [Jun 15 15:21:07.167 LOG: Err] <163>jnh_partition_ok(7337): jnh_expand_partition failed, inst 1, jnh_app fast-memory, dwords 524288

    System Exception: Vector/Code 0x00900, Signal -1
    Event occurred at: Jun 15 15:23:24.900744 

    Juniper Embedded Microkernel Version 11.2S7.4
    Built by builder on 2013-01-09 22:37:02 UTC
    Copyright (C) 1998-2013, Juniper Networks, Inc.
    All rights reserved.
    Reason string: "Panic"
    Context: Thread (PFE Manager)

    Registers:
    R00: 0x4003f1cc R01: 0x4384a610 R02: 0x43846da0 R03: 0x0000005d 
    R04: 0x00000000 R05: 0x4384a618 R06: 0x00000000 R07: 0x20000000 
    R08: 0x4384a543 R09: 0x0000005d R10: 0x4384ae00 R11: 0x41240000 
    R12: 0x44022022 R13: 0xee5ff013 R14: 0x4165efc0 R15: 0x4165efc0 
    R16: 0x4165efc0 R17: 0x410d8de0 R18: 0x4384a6c0 R19: 0x40fa0000 
    R20: 0x40cd0000 R21: 0x00000000 R22: 0x00000001 R23: 0x4384a6c8 
    R24: 0x00000001 R25: 0x27fffff8 R26: 0x0000000c R27: 0x5526bd58 
    R28: 0x00000001 R29: 0x00000000 R30: 0x402e09f4 R31: 0x40e50c5c 
    MSR: 0x00029200 CTR: 0x000ef2ab Link: 0x4003f1cc SP: 0x4384a610
     CR: 0x44022082 XER: 0x20000000 DEAR: 0x00000000 PC: 0x4003f1d0
    ESR: 0x00000000 K_MSR: 0x00021200

    Stack Traceback:
    Frame 01: sp = 0x4384a610, pc = 0x4003f1cc
    Frame 02: sp = 0x4384a658, pc = 0x402e09f4
    Frame 03: sp = 0x4384a6a8, pc = 0x4082de08
    Frame 04: sp = 0x4384a840, pc = 0x4082f120
    Frame 05: sp = 0x4384a898, pc = 0x40830084
    Frame 06: sp = 0x4384a8d8, pc = 0x408305e8
    Frame 07: sp = 0x4384a930, pc = 0x4081f864
    Frame 08: sp = 0x4384a988, pc = 0x407f5b84
    Frame 09: sp = 0x4384ab78, pc = 0x407da0c0
    Frame 10: sp = 0x4384acc0, pc = 0x406e2220
    Frame 11: sp = 0x4384ace0, pc = 0x406e5e24
    Frame 12: sp = 0x4384ad98, pc = 0x4002e2ac

    [LOG] syslog called with interrupts off (caller pc:0x4005cd84)
    [LOG] Registered network packet handlers
    [LOG] syslog called with interrupts off (caller pc:0x40a47018)
    [LOG] Dumping core-NPC1 to 1
    [LOG] syslog called with interrupts off (caller pc:0x40a45d6c)
    [LOG] Coredump finished[LOG] chassis_db_set_dpc_simulation: options = 0!!
    [LOG] Set the IP IRI for table #1 to 0x80000011
    [LOG] IPV4 Init: Set the IP IRI to 0x80000011
    [LOG] if_notify_init: IF notify list already initialized 

    MPC: Reset reason (0x0): No reason?


    ROM NVRAM:
     0 available bytes, 0 used, 0 free

    NPC1(LSANCA-VFTTP-301_RE0 vty)# 
    NPC1(LSANCA-VFTTP-301_RE0 vty)# 
    NPC1(LSANCA-VFTTP-301_RE0 vty)# exit

## show syslog messages (FPC10)

    SDPC10(LSANCA-VFTTP-301_RE0 vty)# show syslog messages
    [May 18 09:22:37.852 LOG: Info] Reconnect: Established connection to Master
    [May 18 09:22:37.852 LOG: Info] Reconnect: pic attach sent for pic 10/0
    [May 18 09:22:37.852 LOG: Info] Reconnect: port info sent for pic 10/0
    [May 18 09:22:37.852 LOG: Info] CMS: Sent CM reconnect
    [May 18 09:22:37.942 LOG: Debug] UPDN msg to kernel for ifd:cms-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:22:37.942 LOG: Debug] UPDN msg to kernel for ifd:gr-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:22:37.942 LOG: Debug] UPDN msg to kernel for ifd:ip-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:22:37.942 LOG: Debug] UPDN msg to kernel for ifd:ms-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:22:37.942 LOG: Debug] UPDN msg to kernel for ifd:mt-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:22:37.942 LOG: Debug] UPDN msg to kernel for ifd:pc-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:22:37.942 LOG: Debug] UPDN msg to kernel for ifd:pd-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:22:37.942 LOG: Debug] UPDN msg to kernel for ifd:pe-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:22:37.942 LOG: Debug] UPDN msg to kernel for ifd:vt-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:22:49.938 LOG: Debug] service_update_services_params: chassis db services exists
    [May 18 09:22:50.135 LOG: Info] receive cm setting 21 with value 0x00
    [May 18 09:22:50.135 LOG: Info] receive cm setting 4 with value 0x01
    [May 18 09:22:50.136 LOG: Info] receive cm setting 35 with value 0x01
    [May 18 09:22:50.136 LOG: Info] receive cm setting 11 with value 0x00
    [May 18 09:22:50.136 LOG: Info] receive cm setting 25 with value 0x00
    [May 18 09:22:50.136 LOG: Info] receive cm setting 4 with value 0x01
    [May 18 09:22:50.136 LOG: Info] receive cm setting 25 with value 0x00
    [May 18 09:22:50.137 LOG: Info] receive cm setting 35 with value 0x01
    [May 18 09:22:50.137 LOG: Info] receive cm setting 11 with value 0x00
    [May 18 09:22:50.137 LOG: Info] receive cm setting 26 with value 0x00
    [May 18 09:24:29.134 LOG: Err] NH: NH add received for an already existing non-discard nh, nh_id=356
    , old type = Local new type = Local
    [May 18 09:29:48.513 LOG: Err] PFEMAN: Master socket closed
    [May 18 09:29:48.513 LOG: Err] PFEMAN disconnected; PFEMAN socket closed abruptly
    [May 18 09:29:48.513 LOG: Debug] sending disconnect msg for PIC slot 0
    [May 18 09:29:48.582 LOG: Err] CMLC: Master closed connection
    [May 18 09:29:48.583 LOG: Emergency] CMLC: Going disconnected; Routing engine chassis socket closed abruptly
    [May 18 09:29:48.643 LOG: Notice] Routing engine PFEMAN reconnection succeeded after 1 tries
    [May 18 09:29:48.643 LOG: Info] PFEMAN: Session manager active
    [May 18 09:29:48.643 LOG: Notice] PFEMAN master RE reconnection made
    [May 18 09:29:48.644 LOG: Info] PFEMAN: received Resync complete.
    [May 18 09:29:48.644 LOG: Info] PFEMAN session: master is in switchover transition
    [May 18 09:29:48.680 LOG: Debug] CMLC: Using IDR encoding
    [May 18 09:29:48.680 LOG: Err] CMLC: Clearing disconnected; RE connection re-established
    [May 18 09:29:48.680 LOG: Debug] CMLC: Completed Re-connecting to Master
    [May 18 09:29:48.680 LOG: Info] CMLC: Master RE reconnection made
    [May 18 09:29:48.730 LOG: Err] RT-HAL,rt_msg_handler,565: route check failed
    [May 18 09:29:48.730 LOG: Err] NH: Failed to find nh (361) for deletion
    [May 18 09:29:48.730 LOG: Err] NH: NH add received for an already existing non-discard nh, nh_id=372
    , old type = Local new type = Local
    [May 18 09:29:48.765 LOG: Info] cmsfpc_ready: Sending FPC ready mesg to master
    [May 18 09:29:48.765 LOG: Info] Reconnect: Established connection to Master
    [May 18 09:29:48.766 LOG: Info] Reconnect: pic attach sent for pic 10/0
    [May 18 09:29:48.766 LOG: Info] Reconnect: port info sent for pic 10/0
    [May 18 09:29:48.766 LOG: Info] CMS: Sent CM reconnect
    [May 18 09:29:48.943 LOG: Info] PFEMAN session: master is out of switchover transition
    [May 18 09:29:49.229 LOG: Debug] UPDN msg to kernel for ifd:cms-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:29:49.229 LOG: Debug] UPDN msg to kernel for ifd:gr-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:29:49.229 LOG: Debug] UPDN msg to kernel for ifd:ip-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:29:49.229 LOG: Debug] UPDN msg to kernel for ifd:ms-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:29:49.229 LOG: Debug] UPDN msg to kernel for ifd:mt-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:29:49.229 LOG: Debug] UPDN msg to kernel for ifd:pc-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:29:49.229 LOG: Debug] UPDN msg to kernel for ifd:pd-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:29:49.229 LOG: Debug] UPDN msg to kernel for ifd:pe-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:29:49.229 LOG: Debug] UPDN msg to kernel for ifd:vt-10/0/0, flag:1, speed: 0, duplex:0
    [May 18 09:30:02.704 LOG: Debug] service_update_services_params: chassis db services exists
    [May 18 09:30:02.918 LOG: Info] receive cm setting 21 with value 0x00
    [May 18 09:30:02.918 LOG: Info] receive cm setting 4 with value 0x01
    [May 18 09:30:02.919 LOG: Info] receive cm setting 35 with value 0x01
    [May 18 09:30:02.919 LOG: Info] receive cm setting 11 with value 0x00
    [May 18 09:30:02.919 LOG: Info] receive cm setting 25 with value 0x00
    [May 18 09:30:02.920 LOG: Info] receive cm setting 4 with value 0x01
    [May 18 09:30:02.920 LOG: Info] receive cm setting 25 with value 0x00
    [May 18 09:30:02.921 LOG: Info] receive cm setting 35 with value 0x01
    [May 18 09:30:02.921 LOG: Info] receive cm setting 11 with value 0x00
    [May 18 09:30:02.921 LOG: Info] receive cm setting 26 with value 0x00
    [May 18 09:31:48.471 LOG: Err] NH: NH add received for an already existing non-discard nh, nh_id=359
    , old type = Local new type = Local
    [May 24 12:11:27.871 LOG: Debug] asp_pfe_gencfg_handler: Received gencfg msg:minor type=ssr_blob for pfe, op=add
    [May 24 12:11:27.871 LOG: Debug] asp_pfe_gencfg_handler: data for ssr_blob for pfe : set name(SSET-REDIRECT-CIL4-DEMUX0-31770017) bypass(0) [May 27 12:16:09.812 LOG: Debug] asp_pfe_gencfg_handler: Received gencfg msg:minor type=ssr_blob for pfe, op=add
    [May 27 12:16:09.812 LOG: Debug] asp_pfe_gencfg_handler: data for ssr_blob for pfe : set name(SSET-REDIRECT-CIL3-DEMUX0-31610019) bypass(0) [May 28 12:21:46.988 LOG: Debug] asp_pfe_gencfg_handler: Received gencfg msg:minor type=ssr_blob for pfe, op=add
    [May 28 12:21:46.988 LOG: Debug] asp_pfe_gencfg_handler: data for ssr_blob for pfe : set name(SSET-REDIRECT-CIL3-DEMUX0-11150037) bypass(0) [May 30 22:27:16.598 LOG: Debug] asp_pfe_gencfg_handler: Received gencfg msg:minor type=ssr_blob for pfe, op=delete
    [May 30 22:27:16.598 LOG: Debug] asp_pfe_gencfg_handler: data for ssr_blob for pfe : set name(SSET-REDIRECT-CIL3-DEMUX0-11930025) bypass(0) [Jun  5 19:25:22.324 LOG: Debug] asp_pfe_gencfg_handler: Received gencfg msg:minor type=ssr_blob for pfe, op=delete
    [Jun  5 19:25:22.324 LOG: Debug] asp_pfe_gencfg_handler: data for ssr_blob for pfe : set name(SSET-REDIRECT-CIL3-DEMUX0-31610019) bypass(0) [Jun  7 22:41:48.150 LOG: Debug] asp_pfe_gencfg_handler: Received gencfg msg:minor type=ssr_blob for pfe, op=delete
    [Jun  7 22:41:48.150 LOG: Debug] asp_pfe_gencfg_handler: data for ssr_blob for pfe : set name(SSET-REDIRECT-CIL4-DEMUX0-31770017) bypass(0) [Jun 15 15:22:24.460 LOG: Debug] CMXDPC: Received spare plane mask: 30
    [Jun 15 15:22:24.460 LOG: Debug] CMXDPC: Current plane state on DPC(online mask): f
    [Jun 15 15:22:24.899 LOG: Debug] CMXDPC: Received spare plane mask: 30
    [Jun 15 15:22:24.899 LOG: Debug] CMXDPC: Current plane state on DPC(online mask): f
    [Jun 15 15:22:55.105 LOG: Err] NH: Failed to find nh (21285) for deletion
    [Jun 15 15:26:30.015 LOG: Err] NH: Non-existent NH (1573:Unicast, 2) 
    [Jun 15 15:26:30.676 LOG: Debug] CMXDPC: Received spare plane mask: 30
    [Jun 15 15:26:30.676 LOG: Debug] CMXDPC: Current plane state on DPC(online mask): f
    [Jun 15 15:26:31.334 LOG: Err] NH: Non-existent NH (4172:Unicast, 2) 
    [Jun 15 15:26:31.625 LOG: Debug] CMXDPC: Received spare plane mask: 30
    [Jun 15 15:26:31.625 LOG: Debug] CMXDPC: Current plane state on DPC(online mask): f
    [Jun 15 15:26:31.724 LOG: Err] NH: Non-existent NH (3635:Unicast, 2) 
    [Jun 15 15:26:35.405 LOG: Err] NH: Non-existent NH (42608:Unicast, 2) 
    [Jun 15 15:27:14.177 LOG: Err] NH: Non-existent NH (1414:Unicast, 2) 
    [Jun 15 15:27:28.241 LOG: Err] NH: Non-existent NH (1573:Unicast, 2) 
    [Jun 15 15:27:28.750 LOG: Err] NH: Non-existent NH (4172:Unicast, 2) 
    [Jun 15 15:27:28.789 LOG: Err] NH: Non-existent NH (3635:Unicast, 2) 
    [Jun 15 15:27:37.181 LOG: Err] NH: Non-existent NH (42608:Unicast, 2) 
    [Jun 15 15:28:22.977 LOG: Err] NH: Non-existent NH (1414:Unicast, 2) 

    SDPC10(LSANCA-VFTTP-301_RE0 vty)# show nvram SDPC10(LSANCA-VFTTP-301_RE0 vty)# show nvram    
    System NVRAM :
     32751 available bytes, 2182 used, 30569 free
     Contents:
    [Jan  1 00:07:20.565 LOG: Emergency] <160>CMLC: Chassis Manager terminated
    [LOG] IPV4 Init: Set the IP IRI to 0x80000012
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [Mar 15 01:45:57.570 LOG: Emergency] <160>CMLC: Chassis Manager terminated
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [Jan 24 00:25:13.570 LOG: Emergency] <160>CMLC: Chassis Manager terminated
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x8000001a
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] Set the IP IRI for table #1 to 0x8000001a
    [LOG] IPV4 Init: Set the IP IRI to 0x8000001a
    [LOG] Registered network packet handlers
    [LOG] if_notify_init: IF notify list already initialized 
    [Feb 26 10:29:14.284 LOG: Emergency] <160>CMLC: Chassis Manager terminated
    [LOG] Set the IP IRI for table #1 to 0x8000001a
    [LOG] IPV4 Init: Set the IP IRI to 0x8000001a
    [LOG] Registered network packet handlers
    [LOG] if_notify_init: IF notify list already initialized 
    [May 18 08:38:08.506 LOG: Emergency] <160>CMLC: Going disconnected; Routing engine chassis socket closed abruptly
    [May 18 09:02:32.922 LOG: Emergency] <160>CMLC: Going disconnected; Routing engine chassis socket closed abruptly
    [May 18 09:22:37.669 LOG: Emergency] <160>CMLC: Going disconnected; Routing engine chassis socket closed abruptly
    [May 18 09:29:48.583 LOG: Emergency] <160>CMLC: Going disconnected; Routing engine chassis socket closed abruptly

    ROM NVRAM:
     0 available bytes, 0 used, 0 free

    SDPC10(LSANCA-VFTTP-301_RE0 vty)# e   exit



## show nvram (FPC10)
    SDPC10(LSANCA-VFTTP-301_RE0 vty)# show nvram
    System NVRAM :
     32751 available bytes, 2182 used, 30569 free
     Contents:
    [Jan  1 00:07:20.565 LOG: Emergency] <160>CMLC: Chassis Manager terminated
    [LOG] IPV4 Init: Set the IP IRI to 0x80000012
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [Mar 15 01:45:57.570 LOG: Emergency] <160>CMLC: Chassis Manager terminated
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [Jan 24 00:25:13.570 LOG: Emergency] <160>CMLC: Chassis Manager terminated
    [LOG] IPV4 Init: Set the IP IRI to 0x80000013
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] IPV4 Init: Set the IP IRI to 0x8000001a
    [LOG] if_notify_init: IF notify list already initialized 
    [LOG] Set the IP IRI for table #1 to 0x8000001a
    [LOG] IPV4 Init: Set the IP IRI to 0x8000001a
    [LOG] Registered network packet handlers
    [LOG] if_notify_init: IF notify list already initialized 
    [Feb 26 10:29:14.284 LOG: Emergency] <160>CMLC: Chassis Manager terminated
    [LOG] Set the IP IRI for table #1 to 0x8000001a
    [LOG] IPV4 Init: Set the IP IRI to 0x8000001a
    [LOG] Registered network packet handlers
    [LOG] if_notify_init: IF notify list already initialized 
    [May 18 08:38:08.506 LOG: Emergency] <160>CMLC: Going disconnected; Routing engine chassis socket closed abruptly
    [May 18 09:02:32.922 LOG: Emergency] <160>CMLC: Going disconnected; Routing engine chassis socket closed abruptly
    [May 18 09:22:37.669 LOG: Emergency] <160>CMLC: Going disconnected; Routing engine chassis socket closed abruptly
    [May 18 09:29:48.583 LOG: Emergency] <160>CMLC: Going disconnected; Routing engine chassis socket closed abruptly

    ROM NVRAM:
     0 available bytes, 0 used, 0 free

    SDPC10(LSANCA-VFTTP-301_RE0 vty)# e   exit

    z427047@LSANCA-VFTTP-301_RE0> show interfaces ge-0/0/0
    Physical interface: ge-0/0/0, Enabled, Physical link is Up
      Interface index: 412, SNMP ifIndex: 6155
      Description: NON_PROD ACCESS:HMLDCAXFOL4_10/1:101/GE1/HMLDCAXFOL4/HMLDCAXF05W
      Link-level type: Ethernet, MTU: 1522, Speed: 1000mbps, BPDU Error: None, MAC-REWRITE Error: None, Loopback: Disabled, Source filtering: Disabled, Flow control: Disabled, Auto-negotiation: Disabled, Remote fault: Online
      Device flags   : Present Running
      Interface flags: SNMP-Traps Internal: 0x4000
      CoS queues     : 8 supported, 8 maximum usable queues
      Schedulers     : 0
      Current address: 78:19:f7:37:5f:c1, Hardware address: 78:19:f7:37:58:00
      Last flapped   : 2013-06-15 15:27:29 UTC (04:17:31 ago)
      Input rate     : 68851704 bps (13904 pps)
      Output rate    : 61480288 bps (6283 pps)
      Active alarms  : None
      Active defects : None
      Interface transmit statistics: Disabled

      Logical interface ge-0/0/0.32767 (Index 7551) (SNMP ifIndex 6158) 
        Flags: SNMP-Traps 0x4000 VLAN-Tag [ 0x0000.0 ]  Encapsulation: ENET2
        Input packets : 174650284 
        Output packets: 110793703                       <------
        Protocol aenet, AE bundle: ae1.32767

    z427047@LSANCA-VFTTP-301_RE0> show interfaces ge-1/0/0
    Physical interface: ge-1/0/0, Enabled, Physical link is Up
      Interface index: 402, SNMP ifIndex: 6221
      Description: ACCESS:HMLDCAXFOL40110311A_12/1:102/GE1/HMLDCAXFOL4/HMLDCAXF05W
      Link-level type: Ethernet, MTU: 1522, Speed: 1000mbps, BPDU Error: None, MAC-REWRITE Error: None, Loopback: Disabled, Source filtering: Disabled, Flow control: Disabled, Auto-negotiation: Disabled, Remote fault: Online
      Device flags   : Present Running
      Interface flags: SNMP-Traps Internal: 0x4000
      CoS queues     : 8 supported, 8 maximum usable queues
      Schedulers     : 0
      Current address: 78:19:f7:37:5f:c1, Hardware address: 78:19:f7:37:58:a5
      Last flapped   : 2013-06-15 15:26:41 UTC (04:18:27 ago)
      Input rate     : 16628912 bps (7325 pps)
      Output rate    : 293511320 bps (33077 pps)        <------
      Active alarms  : None
      Active defects : None
      Interface transmit statistics: Disabled

      Logical interface ge-1/0/0.32767 (Index 7546) (SNMP ifIndex 6222) 
        Flags: SNMP-Traps 0x4000 VLAN-Tag [ 0x0000.0 ]  Encapsulation: ENET2
        Input packets : 105423872 
        Output packets: 702267786
        Protocol aenet, AE bundle: ae1.32767

## show jnh 0/1 pool detail

    {master}
    z427047@LSANCA-VFTTP-301_RE0> request pfe execute target fpc0 command [ "show jnh 0 pool detail" "show jnh 1 pool detail" ] | no-more  

    SENT: Ukern command: show jnh 0 pool detail
    GOT:
    GOT:                 Name     PhysAddr           Size by Type                                   Used       (%)    Free       (%)
    GOT:                                             Private    Shared     Reserved   Expansion
    GOT:
    GOT:             Next Hop     0x00000000         2097152    0          2097152    7072768       2085626    99%    11526      1%
    GOT:                          0xc0000000         40960      258048     0          0             223377     74%    75631      26%
    GOT:
    GOT:             Firewall     0x00400000         2097152    0          2097152    7072768       36428      1%     2060724    99%
    GOT:                          0xc0000000         16384      258048     0          0             182633     66%    91799      34%
    GOT:
    GOT:             Counters     0x00900000         1048576    0          0          0             50588      4%     997988     96%
    GOT:                          0x00800000         1048576    0          0          0             129210     12%    919366     88%
    GOT:                          0x00a00000         3145728    0          0          0             558438     17%    2587290    83%
    GOT:                          0xc0000000         8192       0          0          0             3012       36%    5180       64%
    GOT:
    GOT:                 HASH     0x00000000         8590336    0          0          11267072      8590336    100%   0          0%
    GOT:
    GOT:               ENCAPS     0x00000000         4259840    0          0          11267072      4259840    100%   0          0%
    GOT:
    GOT:                 LMEM     0x00001000         512        0          0          0             52         10%    460        90%
    GOT:
    GOT:                 OMEM     0x00000000         33079304   0          0          475128        33079304   100%   0          0%
    GOT:
    GOT:           UEID_SPACE     0x01c00000         1048576    Phys size (DWORDS):   2097152       8227       < 1%   1040349    >99%
    GOT:
    GOT:    UEID_SHARED_SPACE     0x01bf0000         65536      Phys size (DWORDS):   65536         7          < 1%   65529      >99%

    SENT: Ukern command: show jnh 1 pool detail
    GOT:
     
    GOT:                 Name     PhysAddr           Size by Type                                   Used       (%)    Free       (%)
    GOT:                                             Private    Shared     Reserved   Expansion
    GOT:
    GOT:             Next Hop     0x00000000         4194304    0          0          7072768       3990273    95%    204031     5%
    GOT:                          0xc0000000         40960      258048     0          0             298602     99%    406        1%
    GOT:
    GOT:             Firewall     0x00400000         2097152    0          2097152    7072768       36428      1%     2060724    99%
    GOT:                          0xc0000000         16384      258048     0          0             257914     93%    16518      7%
    GOT:
    GOT:             Counters     0x00900000         1048576    0          0          0             50588      4%     997988     96%
    GOT:                          0x00800000         1048576    0          0          0             129210     12%    919366     88%
    GOT:                          0x00a00000         3145728    0          0          0             930        < 1%   3144798    >99%
    GOT:                          0xc0000000         8192       0          0          0             2330       28%    5862       72%
    GOT:
    GOT:                 HASH     0x00000000         8590336    0          0          9169920       8590336    100%   0          0%
    GOT:
    GOT:               ENCAPS     0x00000000         4259840    0          0          9169920       4259840    100%   0          0%
    GOT:
    GOT:                 LMEM     0x00001000         512        0          0          0             52         10%    460        90%
    GOT:
    GOT:                 OMEM     0x00000000         33079304   0          0          475128        33079304   100%   0          0%
    GOT:
    GOT:           UEID_SPACE     0x01c00000         1048576    Phys size (DWORDS):   2097152       133        < 1%   1048443    >99%
    GOT:
    GOT:    UEID_SHARED_SPACE     0x01bf0000         65536      Phys size (DWORDS):   65536         5          < 1%   65531      >99%
    LOCAL: End of file

    {master}
    z427047@LSANCA-VFTTP-301_RE0> 

    {master}
    z427047@LSANCA-VFTTP-301_RE0> request pfe execute target fpc1 command [ "show jnh 0 pool detail" "show jnh 1 pool detail" ] | no-more    

    SENT: Ukern command: show jnh 0 pool detail
    GOT:
    GOT:                 Name     PhysAddr           Size by Type                                   Used       (%)    Free       (%)
    GOT:                                             Private    Shared     Reserved   Expansion
    GOT:
    GOT:             Next Hop     0x00000000         2097152    0          2097152    7072768       2085765    99%    11387      1%
    GOT:                          0xc0000000         40960      258048     0          0             223348     74%    75660      26%
    GOT:
    GOT:             Firewall     0x00400000         2097152    0          2097152    7072768       36428      1%     2060724    99%
    GOT:                          0xc0000000         16384      258048     0          0             182610     66%    91822      34%
    GOT:
    GOT:             Counters     0x00900000         1048576    0          0          0             50586      4%     997990     96%
    GOT:                          0x00800000         1048576    0          0          0             129210     12%    919366     88%
    GOT:                          0x00a00000         3145728    0          0          0             558416     17%    2587312    83%
    GOT:                          0xc0000000         8192       0          0          0             3012       36%    5180       64%
    GOT:
    GOT:                 HASH     0x00000000         8590336    0          0          11267072      8590336    100%   0          0%
    GOT:
    GOT:               ENCAPS     0x00000000         4259840    0          0          11267072      4259840    100%   0          0%
    GOT:
    GOT:                 LMEM     0x00001000         512        0          0          0             52         10%    460        90%
    GOT:
    GOT:                 OMEM     0x00000000         33079304   0          0          475128        33079304   100%   0          0%
    GOT:
    GOT:           UEID_SPACE     0x01c00000         1048576    Phys size (DWORDS):   2097152       8224       < 1%   1040352    >99%
    GOT:
    GOT:    UEID_SHARED_SPACE     0x01bf0000         65536      Phys size (DWORDS):   65536         7          < 1%   65529      >99%

    SENT: Ukern command: show jnh 1 pool detail
    GOT:
    GOT:                 Name     PhysAddr           Size by Type                                   Used       (%)    Free       (%)
    GOT:                                             Private    Shared     Reserved   Expansion
    GOT:
    GOT:             Next Hop     0x00000000         4194304    0          0          7072768       3990313    95%    203991     5%
    GOT:                          0xc0000000         40960      258048     0          0             298599     99%    409        1%
    GOT:
    GOT:             Firewall     0x00400000         2097152    0          2097152    7072768       36428      1%     2060724    99%
    GOT:                          0xc0000000         16384      258048     0          0             257913     93%    16519      7%
    GOT:
    GOT:             Counters     0x00900000         1048576    0          0          0             50586      4%     997990     96%
    GOT:                          0x00800000         1048576    0          0          0             129210     12%    919366     88%
    GOT:                          0x00a00000         3145728    0          0          0             930        < 1%   3144798    >99%
    GOT:                          0xc0000000         8192       0          0          0             2330       28%    5862       72%
    GOT:
    GOT:                 HASH     0x00000000         8590336    0          0          9169920       8590336    100%   0          0%
    GOT:
    GOT:               ENCAPS     0x00000000         4259840    0          0          9169920       4259840    100%   0          0%
    GOT:
    GOT:                 LMEM     0x00001000         512        0          0          0             52         10%    460        90%
    GOT:
    GOT:                 OMEM     0x00000000         33079304   0          0          475128        33079304   100%   0          0%
    GOT:
    GOT:           UEID_SPACE     0x01c00000         1048576    Phys size (DWORDS):   2097152       130        < 1%   1048446    >99%
    GOT:
    GOT:    UEID_SHARED_SPACE     0x01bf0000         65536      Phys size (DWORDS):   65536         5          < 1%   65531      >99%
    LOCAL: End of file

    {master}
    z427047@LSANCA-VFTTP-301_RE0>  

## show jnh 0/1 pool composition

    {master}
    z427047@LSANCA-VFTTP-301_RE0> request pfe execute target fpc0 command [ "show jnh 0 pool composition" "show jnh 1 pool composition" ] | no-more   
    SENT: Ukern command: show jnh 0 pool composition
    GOT:
    GOT: Partition Next Hop:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                                 DV             0             0             0
    GOT:                              PPPOE            15             2             0
    GOT:                              ktree         58967       1818475       1799514
    GOT:                        ktree-nodes             0             0             0
    GOT:                                 NH        504594       1320628       1237414
    GOT:                         NH Ingress             0             0             0
    GOT:                           NH Multi             0             0             0
    GOT:                      NH Mcast List             4       1062223       1062220
    GOT:                      NH replicated          8691       1071382       1062691
    GOT:                             stream          4272            61             0
    GOT:                                iif        706147         25800         17162
    GOT:                                oif        287475         16999          8389
    GOT:                             iproto         77481          8663            54
    GOT:                             oproto        143018          8664            54
    GOT:                                iff         59646         48568         31405
    GOT:                                off           278           367           278
    GOT:                       iff-services           486           244            82
    GOT:                       off-services             0             0             0
    GOT:                    bridge-domain-i         65668             4             0
    GOT:                    bridge-domain-e        196630             5             0
    GOT:                         bridge-stp         16384             1             0
    GOT:                              l2dst             0             0             0
    GOT:                          ktree-iif         57713         45395          7467
    GOT:                   unilist-selector           672           168           147
    GOT:                        fast-memory         15834       3587682       3587216
    GOT:                           iif-list         16186        785948        777855
    GOT:        sib (sample inf base) entry           180            27             0
    GOT:                        ba_classify            42             7             0
    GOT:                          exception           781           148             0
    GOT:                        cos-rewrite          8192             1             0
    GOT:                     lifetime-table         37296             2             0
    GOT:                         rate-limit          4096             1             0
    GOT:                         IFBD IDMEM             0             0             0
    GOT:                         IFBD EDMEM             0             0             0
    GOT:                      packet-inject             0             0             0
    GOT:                    Virtual Chassis           484             1             0
    GOT:                         diag-table             0             0             0
    GOT:                               ddos             0             0             0
    GOT:                    Inline services          4096             1             0
    GOT:                          inline KA             0             0             0
    GOT:                       inline KA PT             0             0             0
    GOT:                         inline ppm             0             0             0
    GOT: Partition Firewall:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                                 FW          3589          1505           600
    GOT: Partition Counters:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                         FW Counter         34292         10650          2498
    GOT:                         FW Policer         88221         10584          2496
    GOT:                         NH Policer             0             0             0
    GOT:                     IFD Error Cntr          1088            32             0
    GOT:                    Per Stream Cntr             0             0             0
    GOT:                            NH Cntr          8662          4775           444
    GOT:                           IFL Cntr            12             6             0
    GOT:                           IFF Cntr        378256          8657            54
    GOT:                           RPF Cntr         17140         37288         28718
    GOT:                         Class Cntr             0             0             0
    GOT:                            RT Cntr             8        777701        777697
    GOT:                 bridge-domain-cntr             2             1             0
    GOT:               sample-inline-params           384             1             0
    GOT:            sample-collector-params           256             1             0
    GOT:                  services-counters            26             1             0
    GOT:                  exception-counter          1488            66             0
    GOT:                       ISSU Policer            54            54             0
    GOT:                  inline KA Counter             0             0             0
    GOT: Partition HASH:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                        bridge-hash             0             0             0
    GOT:              bridge-domain-counter       2202008             1             0
    GOT:                 HASH EDMEM Bkt/Rec       5010822             8             0
    GOT:                HASH EDMEM Sideband       1113294             2             0
    GOT:                 HASH IDMEM Bkt/Rec             0             0             0
    GOT:                HASH IDMEM Sideband             0             0             0
    GOT:               services-ring-buffer        262144             1             0
    GOT: Partition ENCAPS:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                               ueid       2097152             1             0
    GOT:                        ueid-shared         65536             1             0
    GOT:                             fabric       2097152             2             0
    GOT: Partition LMEM:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                             Master             0             0             0
    GOT: Partition OMEM:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                      HASH OMEM Rec      33079304             2             0
    SENT: Ukern command: show jnh 1 pool composition
    GOT:
    GOT: Partition Next Hop:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                                 DV             0             0             0
    GOT:                              PPPOE            15             2             0
    GOT:                              ktree         58967       1818475       1799514
    GOT:                        ktree-nodes             0             0             0
    GOT:                                 NH        488460       1311738       1236554
    GOT:                         NH Ingress             0             0             0
    GOT:                           NH Multi             0             0             0
    GOT:                      NH Mcast List             4       1062223       1062220
    GOT:                      NH replicated          8691       1071382       1062691
    GOT:                             stream          4176            29             0
    GOT:                                iif        640569         25766         17156
    GOT:                                oif        287449         16985          8387
    GOT:                             iproto         77373          8651            54
    GOT:                             oproto        142910          8652            54
    GOT:                                iff         59623         48554         31400
    GOT:                                off           274           365           278
    GOT:                       iff-services           486           244            82 
    GOT:                       off-services             0             0             0
    GOT:                    bridge-domain-i         65668             4             0
    GOT:                    bridge-domain-e        196630             5             0
    GOT:                         bridge-stp         16384             1             0
    GOT:                              l2dst             0             0             0
    GOT:                          ktree-iif          8626          8652            54
    GOT:                   unilist-selector           672           168           147
    GOT:                        fast-memory       2135774       3587253       2524979
    GOT:                           iif-list         16186        785948        777855
    GOT:        sib (sample inf base) entry           180            27             0
    GOT:                        ba_classify            42             7             0
    GOT:                          exception           781           148             0
    GOT:                        cos-rewrite          8192             1             0
    GOT:                     lifetime-table         37296             2             0
    GOT:                         rate-limit          4096             1             0
    GOT:                         IFBD IDMEM             0             0             0
    GOT:                         IFBD EDMEM             0             0             0
    GOT:                      packet-inject             0             0             0
    GOT:                    Virtual Chassis           484             1             0
    GOT:                         diag-table             0             0             0
    GOT:                               ddos             0             0             0
    GOT:                    Inline services          4096             1             0
    GOT:                          inline KA             0             0             0
    GOT:                       inline KA PT             0             0             0
    GOT:                         inline ppm             0             0             0
    GOT: Partition Firewall:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                                 FW          3589          1505           600
    GOT: Partition Counters:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                         FW Counter         34292         10650          2498
    GOT:                         FW Policer         88221         10584          2496
    GOT:                         NH Policer             0             0             0
    GOT:                     IFD Error Cntr           544            16             0
    GOT:                    Per Stream Cntr             0             0             0
    GOT:                            NH Cntr            26            13             0
    GOT:                           IFL Cntr            12             6             0
    GOT:                           IFF Cntr           744            21             0
    GOT:                           RPF Cntr         17140         37288         28718
    GOT:                         Class Cntr             0             0             0
    GOT:                            RT Cntr             8        777701        777697
    GOT:                 bridge-domain-cntr             2             1             0
    GOT:               sample-inline-params           384             1             0
    GOT:            sample-collector-params           256             1             0
    GOT:                  services-counters            26             1             0
    GOT:                  exception-counter          1488            66             0
    GOT:                       ISSU Policer            54            54             0
    GOT:                  inline KA Counter             0             0             0
    GOT: Partition HASH:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                        bridge-hash             0             0             0
    GOT:              bridge-domain-counter       2202008             1             0
    GOT:                 HASH EDMEM Bkt/Rec       5010822             8             0
    GOT:                HASH EDMEM Sideband       1113294             2             0
    GOT:                 HASH IDMEM Bkt/Rec             0             0             0
    GOT:                HASH IDMEM Sideband             0             0             0
    GOT:               services-ring-buffer        262144             1             0
    GOT: Partition ENCAPS:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                               ueid       2097152             1             0
    GOT:                        ueid-shared         65536             1             0
    GOT:                             fabric       2097152             2             0
    GOT: Partition LMEM:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                             Master             0             0             0
    GOT: Partition OMEM:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                      HASH OMEM Rec      33079304             2             0
    LOCAL: End of file

    {master}
    z427047@LSANCA-VFTTP-301_RE0> request pfe execute target fpc1 command [ "show jnh 0 pool composition" "show jnh 1 pool composition" ] | no-more    
    SENT: Ukern command: show jnh 0 pool composition
    GOT:
    GOT: Partition Next Hop:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                                 DV             0             0             0
    GOT:                              PPPOE            15             2             0
    GOT:                              ktree         58951       1818571       1799615
    GOT:                        ktree-nodes             0             0             0
    GOT:                                 NH        504812       1315620       1232296
    GOT:                         NH Ingress             0             0             0
    GOT:                           NH Multi             0             0             0
    GOT:                      NH Mcast List             4       1062279       1062276
    GOT:                      NH replicated          8691       1071438       1062747
    GOT:                             stream          4272            61             0
    GOT:                                iif        706138         25797         17162
    GOT:                                oif        287469         16996          8389
    GOT:                             iproto         77454          8660            54
    GOT:                             oproto        142991          8661            54
    GOT:                                iff         59631         45675         28518
    GOT:                                off           278           359           270
    GOT:                       iff-services           486           244            82
    GOT:                       off-services             0             0             0
    GOT:                    bridge-domain-i         65668             4             0
    GOT:                    bridge-domain-e        196630             5             0
    GOT:                         bridge-stp         16384             1             0
    GOT:                              l2dst             0             0             0
    GOT:                          ktree-iif         57703         45345          7420
    GOT:                   unilist-selector           672           168           147
    GOT:                        fast-memory         15834       3587886       3587420
    GOT:                           iif-list         16184        785987        777895
    GOT:        sib (sample inf base) entry           180            27             0
    GOT:                        ba_classify            42             7             0
    GOT:                          exception           781           148             0
    GOT:                        cos-rewrite          8192             1             0
    GOT:                     lifetime-table         37296             2             0
    GOT:                         rate-limit          4096             1             0
    GOT:                         IFBD IDMEM             0             0             0
    GOT:                         IFBD EDMEM             0             0             0
    GOT:                      packet-inject             0             0             0
    GOT:                    Virtual Chassis           484             1             0
    GOT:                         diag-table             0             0             0
    GOT:                               ddos             0             0             0
    GOT:                    Inline services          4096             1             0
    GOT:                          inline KA             0             0             0
    GOT:                       inline KA PT             0             0             0
    GOT:                         inline ppm             0             0             0
    GOT: Partition Firewall:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                                 FW          3589          1505           600
    GOT: Partition Counters:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                         FW Counter         34292          9211          1059
    GOT:                         FW Policer         88221          9145          1057
    GOT:                         NH Policer             0             0             0
    GOT:                     IFD Error Cntr          1088            32             0
    GOT:                    Per Stream Cntr             0             0             0
    GOT:                            NH Cntr          8772         10769          6383
    GOT:                           IFL Cntr            12             6             0
    GOT:                           IFF Cntr        378148          8654            54
    GOT:                           RPF Cntr         17140         35846         27276
    GOT:                         Class Cntr             0             0             0
    GOT:                            RT Cntr             6        777740        777737
    GOT:                 bridge-domain-cntr             2             1             0
    GOT:               sample-inline-params           384             1             0
    GOT:            sample-collector-params           256             1             0
    GOT:                  services-counters            26             1             0
    GOT:                  exception-counter          1488            66             0
    GOT:                       ISSU Policer            54            54             0
    GOT:                  inline KA Counter             0             0             0
    GOT: Partition HASH:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                        bridge-hash             0             0             0
    GOT:              bridge-domain-counter       2202008             1             0
    GOT:                 HASH EDMEM Bkt/Rec       5010822             8             0
    GOT:                HASH EDMEM Sideband       1113294             2             0
    GOT:                 HASH IDMEM Bkt/Rec             0             0             0
    GOT:                HASH IDMEM Sideband             0             0             0
    GOT:               services-ring-buffer        262144             1             0
    GOT: Partition ENCAPS:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                               ueid       2097152             1             0
    GOT:                        ueid-shared         65536             1             0
    GOT:                             fabric       2097152             2             0
    GOT: Partition LMEM:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                             Master             0             0             0
    GOT: Partition OMEM:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                      HASH OMEM Rec      33079304             2             0
    SENT: Ukern command: show jnh 1 pool composition
    GOT:
    GOT: Partition Next Hop:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                                 DV             0             0             0
    GOT:                              PPPOE            15             2             0
    GOT:                              ktree         58951       1818571       1799615
    GOT:                        ktree-nodes             0             0             0
    GOT:                                 NH        488460       1294765       1219581
    GOT:                         NH Ingress             0             0             0
    GOT:                           NH Multi             0             0             0
    GOT:                      NH Mcast List             4       1062279       1062276
    GOT:                      NH replicated          8691       1071438       1062747
    GOT:                             stream          4176            29             0
    GOT:                                iif        640569         25766         17156
    GOT:                                oif        287449         16985          8387
    GOT:                             iproto         77373          8651            54
    GOT:                             oproto        142910          8652            54
    GOT:                                iff         59623         45670         28516
    GOT:                                off           274           357           270
    GOT:                       iff-services           486           244            82
    GOT:                       off-services             0             0             0
    GOT:                    bridge-domain-i         65668             4             0
    GOT:                    bridge-domain-e        196630             5             0
    GOT:                         bridge-stp         16384             1             0
    GOT:                              l2dst             0             0             0
    GOT:                          ktree-iif          8626          8652            54
    GOT:                   unilist-selector           672           168           147
    GOT:                        fast-memory       2135886       3587440       2525110
    GOT:                           iif-list         16184        785987        777895
    GOT:        sib (sample inf base) entry           180            27             0
    GOT:                        ba_classify            42             7             0
    GOT:                          exception           781           148             0
    GOT:                        cos-rewrite          8192             1             0
    GOT:                     lifetime-table         37296             2             0
    GOT:                         rate-limit          4096             1             0
    GOT:                         IFBD IDMEM             0             0             0
    GOT:                         IFBD EDMEM             0             0             0
    GOT:                      packet-inject             0             0             0
    GOT:                    Virtual Chassis           484             1             0
    GOT:                         diag-table             0             0             0
    GOT:                               ddos             0             0             0
    GOT:                    Inline services          4096             1             0
    GOT:                          inline KA             0             0             0
    GOT:                       inline KA PT             0             0             0
    GOT:                         inline ppm             0             0             0
    GOT: Partition Firewall:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                                 FW          3589          1505           600
    GOT: Partition Counters:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                         FW Counter         34292          9211          1059
    GOT:                         FW Policer         88221          9145          1057
    GOT:                         NH Policer             0             0             0
    GOT:                     IFD Error Cntr           544            16             0
    GOT:                    Per Stream Cntr             0             0             0
    GOT:                            NH Cntr            26            13             0
    GOT:                           IFL Cntr            12             6             0
    GOT:                           IFF Cntr           744            21             0
    GOT:                           RPF Cntr         17140         35846         27276
    GOT:                         Class Cntr             0             0             0
    GOT:                            RT Cntr             6        777740        777737
    GOT:                 bridge-domain-cntr             2             1             0
    GOT:               sample-inline-params           384             1             0
    GOT:            sample-collector-params           256             1             0
    GOT:                  services-counters            26             1             0
    GOT:                  exception-counter          1488            66             0
    GOT:                       ISSU Policer            54            54             0
    GOT:                  inline KA Counter             0             0             0
    GOT: Partition HASH:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                        bridge-hash             0             0             0
    GOT:              bridge-domain-counter       2202008             1             0
    GOT:                 HASH EDMEM Bkt/Rec       5010822             8             0
    GOT:                HASH EDMEM Sideband       1113294             2             0
    GOT:                 HASH IDMEM Bkt/Rec             0             0             0
    GOT:                HASH IDMEM Sideband             0             0             0
    GOT:               services-ring-buffer        262144             1             0
    GOT: Partition ENCAPS:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                               ueid       2097152             1             0
    GOT:                        ueid-shared         65536             1             0
    GOT:                             fabric       2097152             2             0
    GOT: Partition LMEM:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                             Master             0             0             0
    GOT: Partition OMEM:
    GOT:                    JNH Application        DWORDS        ALLOCS         FREES
    GOT:                      HASH OMEM Rec      33079304             2             0
    LOCAL: End of file

    {master}
    z427047@LSANCA-VFTTP-301_RE0>  

## show heap

    {master}
    z427047@LSANCA-VFTTP-301_RE0> request pfe execute target fpc0 command [ "show heap" ] | no-more                                          
    SENT: Ukern command: show heap
    GOT:
    GOT: ID      Base    Total(b)     Free(b)     Used(b)   %   Name
    GOT: --  --------   ---------   ---------   ---------  ---   -----------
    GOT:  0  41774ec0  1968573712  1571350416   397223296   20  Kernel
    GOT:  1  b6cd5bd0    67108864    55857512    11251352   16  LAN buffer
    GOT:  2  bcdfffe0    52428784    52428784           0    0  Blob
    GOT:  3  bacd5bd0    34775176    34775176           0    0  ISSU scratch
    LOCAL: End of file

    {master}
    z427047@LSANCA-VFTTP-301_RE0> request pfe execute target fpc1 command [ "show heap" ] | no-more    
    SENT: Ukern command: show heap
    GOT:
    GOT: ID      Base    Total(b)     Free(b)     Used(b)   %   Name
    GOT: --  --------   ---------   ---------   ---------  ---   -----------
    GOT:  0  41774ec0  1968573712  1570698216   397875496   20  Kernel
    GOT:  1  b6cd5bd0    67108864    55841368    11267496   16  LAN buffer
    GOT:  2  bcdfffe0    52428784    52428784           0    0  Blob
    GOT:  3  bacd5bd0    34775176    34775176           0    0  ISSU scratch
    LOCAL: End of file

# gdb

    -bash-2.05b$ jdebug core-NPC0.gz.core.1
    [File is compressed. This may take a moment...]
    File type: executable core pfe.
    GNU gdb 6.5 juniper_2006a_411
    Copyright (C) 2006 Free Software Foundation, Inc.
    GDB is free software, covered by the GNU General Public License, and you are
    welcome to change it and/or distribute copies of it under certain conditions.
    Type "show copying" to see the conditions.
    There is absolutely no warranty for GDB.  Type "show warranty" for details.
    This GDB was configured as "--host=i386-unknown-freebsd6.2 --target=powerpc64-juniper-junos".
    #0  panic (format_string=0x40e50c5c "Assertion failed:../../../src/pfe/common/pfe-arch/trinity/toolkits/jnh/jnh_rpf.c:566: %s\n") at ../../../src/pfe/ukern/cpu-ppc/ppc603e_panic.c:68
    68          kprintf("\n\nRecursive PANIC detected, returning to ROM Monitor\n"
    (gdb) bt
    #0  panic (format_string=0x40e50c5c "Assertion failed:../../../src/pfe/common/pfe-arch/trinity/toolkits/jnh/jnh_rpf.c:566: %s\n") at ../../../src/pfe/ukern/cpu-ppc/ppc603e_panic.c:68
    #1  0x402e09f4 in jnh_rpf_nh_create (inst=1, ifl_index=<value optimized out>, count=2, pop_on_match=FALSE, discard_failure=TRUE, match_nh=2882303727157379084, jnhp=0x4384a6c8)
        at ../../../src/pfe/common/pfe-arch/trinity/toolkits/jnh/jnh_rpf.c:566
    #2  0x4082de08 in rt_nh_build_features (rnh=0x58770ef0, update=<value optimized out>) at ../../../src/pfe/common/pfe-arch/trinity/applications/route/rt_nh.c:703
    #3  0x4082f120 in rt_nh_install (rnh=0x58770ef0, rt=0x57cf4510, p_rtt=0x4e5bc854) at ../../../src/pfe/common/pfe-arch/trinity/applications/route/rt_nh.c:458
    #4  0x40830084 in rt_nh_alloc (p_rtt=0x4e5bc854, rt=0x57cf4510, nh=<value optimized out>, rt_rpf=0x0, rt_cos=0x0, rt_app=1) at ../../../src/pfe/common/pfe-arch/trinity/applications/route/rt_nh.c:254
    #5  0x408305e8 in rt_nh_add (rt=0x57cf4510, p_rtt=0x4e5bc854, rt_rpf=0x0, rt_cos=0x0, rt_app=1, rnhpp=0x4384a940) at ../../../src/pfe/common/pfe-arch/trinity/applications/route/rt_nh.c:166
    #6  0x4081f864 in trinity_rt_create (args=0x4384a9f4) at ../../../src/pfe/common/pfe-arch/trinity/applications/route/rt.c:80
    #7  0x407f5b84 in rt_entry_add_msg_proc (rt_params=<value optimized out>) at ../../../src/pfe/common/applications/route/hal/rt_entry.c:2364
    #8  0x407da0c0 in rt_msg_handler (pipe=0x57ba2cf0, msg=0xb74dfb10) at ../../../src/pfe/common/applications/route/hal/rt_msg.c:576
    #9  0x406e2220 in pfeman_session_manager (pipe=0x57ba2cf0, msg=0xb74dfb10) at ../../../src/pfe/common/applications/pfeman/pfeman_session.c:567
    #10 0x406e5e24 in pfeman_rt_thread () at ../../../src/pfe/common/applications/pfeman/pfeman_rt_xdpc.c:333
    #11 0x4002e2ac in thread_check_interrupt_state (action=0x4384ae00 "") at ../../../src/pfe/ukern/common/thread.c:458
        (gdb) list
        63               * We jump into the exception handler using a system call
        64               */
        65              asm volatile ("sc");
        66          }
        67
        68          kprintf("\n\nRecursive PANIC detected, returning to ROM Monitor\n"
        69                  "(caller pc: 0x%x)\n", (u_int32_t)cpu_callers_pc());
        70          hardware_reset(ROM_RETURN_SWERROR, NULL);
        71      }
        72
        (gdb)

# misc

<!--
## about request interface rebalance
MPC2 linecards in slot 0 and 1
The MS-DPC linecards in slots 10 and 11 


    z555333@NYCMNY-VFTTP-312_RE0> show interfaces targeting 
    Aggregated interface: ae1  
      Redundancy mode: FPC Level Redundancy
      Total number of distributed interfaces: 3461    
    Physical interface: ge-0/0/0, Link status: Up  
      Number of primary distributions: 3409 
      Number of backup  distributions: 52   
    Physical interface: ge-1/0/0, Link status: Up  
      Number of primary distributions: 52   
      Number of backup  distributions: 3409

This shows that AE1 is imbalanced because there are 3409 subscribers that have
chosen ge-0/0/0 as their primary interface, and only 52 that have selected
ge-1/0/0. Since this is skewed, you would run ‘request interface rebalance ae1’
to redistribute demux IFLs across both AE child links, for a more even balance


-->

## about show jnh x

Just a correction about the expansion memory I just learnt from Vibhu on this,

In these 3 cases, since memory left in the expansion memory is still huge
(~5-6M), so it means about 50% of memory is still left.  The case where the
routers crash had no expansion memory left at all.


    BAD case->
                Next Hop     0x00000000         4194304    0          0          27648         4194050    99%    254        1%  
                             0x00d00000         0          4194304    0          0             4194244    99%    60         1%  
                             0x01100000         0          2850816    0          0             2850611    99%    205        1%  
                             0xc0000000         40960      258048     0          0             298669     99%    339        1%  

    Not-so-BAD case->

    nycmny-vfttp-301: 1255 subscribers
    SENT: Ukern command: show jnh 1 pool detail
    GOT:
    GOT:                 Name     PhysAddr           Size by Type                                   Used       (%)    Free       (%)
    GOT:                                             Private    Shared     Reserved   Expansion
    GOT:
    GOT:             Next Hop     0x00000000         4194304    0          0          6024192       4194111    99%    193        1%
    GOT:                          0x00d00000         0          1048576    0          0             535304     51%    513272     49%
    GOT:                          0xc0000000         40960      258048     0          0             298687     99%    321        1%


## slax (by Anurag)

I am attaching an event script that will periodically monitor PFE memory
utilization. I currently have it set to run every hour. A syslog message is
generated to log the current utilization, as well as note about whether the
utilization is concerning. Here is an example of safe utilization:

    Jun 18 22:19:27  TMTRFLF1LAB01010100B-RE1 cscript: PFE next-hop memory utilization: FPC0 PFE0: 7072768 bytes. Safely within threshold.
    Jun 18 22:19:27  TMTRFLF1LAB01010100B-RE1 cscript: PFE next-hop memory utilization: FPC0 PFE1: 7072768 bytes. Safely within threshold.
    Jun 18 22:19:37  TMTRFLF1LAB01010100B-RE1 cscript: PFE next-hop memory utilization: FPC1 PFE0: 7072768 bytes. Safely within threshold.
    Jun 18 22:19:37  TMTRFLF1LAB01010100B-RE1 cscript: PFE next-hop memory utilization: FPC1 PFE1: 7072768 bytes. Safely within threshold.

When the utilization drops below 1.5MB remaining, the last sentence will
instead state, ‘Dangerously above threshold.’ Please schedule a linecard reboot
for the next available maintenance window if that messages is seen. As below,
please ensure that the linecards are rebooted one at a time, waiting for the
first to completely come back online before proceeding to reboot the next
linecard. Also as mentioned below, please do rebalance all AE interfaces that
host subscribers, using the instructions provided earlier.

We continue to try to reproduce this in-house, in order to provide engineering
a controlled environment to debug. Your patience is greatly appreciated.

Event Script Deployment on NG-GWRs
In order to provision the script on the router, copy it to
/var/db/scripts/event/ on both routing engines. Then configure on the master RE
and commit sync:

    u@r> show configuration event-options
    event-script {
        file check_pfe_nhop_mem.slax;
    }

You can confirm the script is provisioned by running:

    u@r> show event-options event-scripts policies 
    ## Last changed: 2013-06-18 22:30:33 EDT
    event-options {
        generate-event {
            EVERY-HOUR time-interval 3600;
        }
        policy VERIFY-PFE-MEMORY {
            events EVERY-HOUR;
            then {
                event-script check_pfe_nhop_mem.slax;
            }
        }
    }

If you need any aspect of the script modified, or have any questions, please let me know.

    /* ----------------------------------------------------------------------------
     * Author        : Anurag Khare
     * Version       : 1.0
     * Last Modified : 20:37 PM 6/18/2013
     * Platform      : MX
     * Release       : 11.2S7.4
     *
     * Copyright (c) 2011-2013  Juniper Networks. All Rights Reserved.
     *
     * YOU MUST ACCEPT THE TERMS OF THIS DISCLAIMER TO USE THIS SOFTWARE
     * 
     * JUNIPER IS WILLING TO MAKE THE INCLUDED SCRIPTING SOFTWARE AVAILABLE TO YOU
     * ONLY UPON THE CONDITION THAT YOU ACCEPT ALL OF THE TERMS CONTAINED IN THIS
     * DISCLAIMER. PLEASE READ THE TERMS AND CONDITIONS OF THIS DISCLAIMER
     * CAREFULLY.
     *
     * THE SOFTWARE CONTAINED IN THIS FILE IS PROVIDED "AS IS." JUNIPER MAKES NO
     * WARRANTIES OF ANY KIND WHATSOEVER WITH RESPECT TO SOFTWARE. ALL EXPRESS OR
     * IMPLIED CONDITIONS, REPRESENTATIONS AND WARRANTIES, INCLUDING ANY WARRANTY
     * OF NON-INFRINGEMENT OR WARRANTY OF MERCHANTABILITY OR FITNESS FOR A
     * PARTICULAR PURPOSE, ARE HEREBY DISCLAIMED AND EXCLUDED TO THE EXTENT
     * ALLOWED BY APPLICABLE LAW.
     *
     * IN NO EVENT WILL JUNIPER BE LIABLE FOR ANY LOST REVENUE, PROFIT OR DATA, OR
     * FOR DIRECT, SPECIAL, INDIRECT, CONSEQUENTIAL, INCIDENTAL OR PUNITIVE DAMAGES
     * HOWEVER CAUSED AND REGARDLESS OF THE THEORY OF LIABILITY ARISING OUT OF THE 
     * USE OF OR INABILITY TO USE THE SOFTWARE, EVEN IF JUNIPER HAS BEEN ADVISED OF 
     * THE POSSIBILITY OF SUCH DAMAGES.
     *
     */

    version 1.1;

    ns junos = "http://xml.juniper.net/junos/*/junos";
    ns xnm = "http://xml.juniper.net/xnm/1.1/xnm";
    ns jcs = "http://xml.juniper.net/junos/commit-scripts/1.0";
    ns ext = "http://xmlsoft.org/XSLT/namespace";
    ns exsl extension = "http://exslt.org/common";
    ns func extension = "http://exslt.org/functions";
    ns vzt = "http://xml.juniper.net/junos/vzt";

    import "../import/junos.xsl";

    /* Embedded event policy */
    var $event-definition = {
      <event-options> {
        <generate-event> {
          <name> "EVERY-HOUR";
          <time-interval> "3600";
        }
        <policy> {
          <name> "VERIFY-PFE-MEMORY";
          <events> "EVERY-HOUR";
            <then> {
              <event-script> {
                <name> "check_pfe_nhop_mem.slax";
              }
            }
         }
      }
    }

    var $conn-handle = jcs:open();

    match / {
      <event-script-results> {
        if (not($conn-handle)) {
          <xsl:message terminate="yes"> "Catastrophic error. Cannot establish MGD connectivity. Aborting script.";
        }
        <out> {
          call vzt:main;
        }
      }
    }

    template vzt:main {
      call vzt:iterate-slots;
    }

    template vzt:iterate-slots ($current-slot = 0, $max-slot = 1) {
      expr jcs:progress("Capturing output from slot ", $current-slot);
      var $pfes := { call vzt:show-jnh($current-slot); }
      call vzt:check-available-memory($slot = $current-slot, $pfes = $pfes);
      if ($current-slot < $max-slot) {
        call vzt:iterate-slots($current-slot = $current-slot + 1);
      }
    }

    template vzt:show-jnh ($slot = 0) {
      var $pfe0_rpc = <request-pfe-execute> {
        <command> "show jnh 0 pool detail";
        <target> "fpc" _ $slot;
      }
      var $pfe1_rpc = <request-pfe-execute> {
        <command> "show jnh 1 pool detail";
        <target> "fpc" _ $slot;
      }
      var $pfe0_results = jcs:execute($conn-handle, $pfe0_rpc);
      var $pfe1_results = jcs:execute($conn-handle, $pfe1_rpc);
      var $pfes := { 
        <pfe> {
          call vzt:extract-expansion-memory($pfe = $pfe0_results);
        }
        <pfe> {
          call vzt:extract-expansion-memory($pfe = $pfe1_results);
        }
      }
      copy-of $pfes;
    }

    template vzt:check-available-memory ($slot = 0, $pfes) {
      for-each($pfes/pfe) {
        var $available_memory = "FPC" _ $slot _ " PFE" _ (position() - 1) _ ": " _ . _ " bytes";
        expr jcs:progress(.);
        if(number(.) < 1500000) {
          call vzt:syslog($message = $available_memory _ ". Dangerously above threshold.", $priority = "external.warning");
        } else {
          call vzt:syslog($message = $available_memory _ ". Safely within threshold.");
        }
      }
    }

    template vzt:extract-expansion-memory ($pfe) {
      var $lines = jcs:break-lines($pfe);
      for-each ($lines[contains(., "Next Hop")]) {
        var $expansion_mem = ((jcs:regex("([[:digit:]]+) +[[:digit:]]+ +[[:digit:]]+%", .))[2]);
        copy-of $expansion_mem;
      }
    }

    template vzt:syslog( $message, $priority = "external.notice" ) {
      var $syslog_tag = "PFE next-hop memory utilization: ";
      expr jcs:syslog( $priority, $syslog_tag, $message );
    }

## PR query

    pings@svl-jtac-tool01:~/public_html/casedata/2013-0615-0089$ query-pr -m jnh_if_aggregate_init -m trinity_mcast_sel_update_orig_weights --summ |grep "\-1"
    663036-1 dhegde   sw-trini closed    major     4-IL2  developmen CE-Scaling:Multiple NPC cores while trying to scale 128K DHCP Dynamic AE-VLAN-DEMUX P and S smoke
    777765-1 jonas    sw-pfe-m closed    major     2-CL2  field      NPC Core due to failed assert(ifp) in jnh_if_aggregate_init
    808235-1 tpatrick sw-trini closed    major     5-IL3  systest    NPC cores at  panic (format_string=0x41bf0cbc "Assertion failed:../../../../../../../../src/pfe/common/pfe-arch/trinity/toolkits/jnh/jnh_if.c:4143: %s\n") in scaled l3vpn test setup
    867717-1 jitendra sw-trini closed    critical  3-IL1  developmen CE-SMOKE-BRAS-AE:multiple NPC cores running BRAS-AE smoke failing to bind PPPOE client with vlan demux using LACP

    pings@svl-jtac-tool01:~/public_html/casedata/2013-0615-0089$ query-pr -m jnh_if_aggregate_init -m trinity_mcast_sel_update_orig_weights --summ |grep "\-1"
    663036-1 dhegde   sw-trini closed    major     4-IL2  developmen CE-Scaling:Multiple NPC cores while trying to scale 128K DHCP Dynamic AE-VLAN-DEMUX P and S smoke
    777765-1 jonas    sw-pfe-m closed    major     2-CL2  field      NPC Core due to failed assert(ifp) in jnh_if_aggregate_init
    808235-1 tpatrick sw-trini closed    major     5-IL3  systest    NPC cores at  panic (format_string=0x41bf0cbc "Assertion failed:../../../../../../../../src/pfe/common/pfe-arch/trinity/toolkits/jnh/jnh_if.c:4143: %s\n") in scaled l3vpn test setup
    867717-1 jitendra sw-trini closed    critical  3-IL1  developmen CE-SMOKE-BRAS-AE:multiple NPC cores running BRAS-AE smoke failing to bind PPPOE client with vlan demux using LACP



    [--synopsis synopsis | -y synopsis]
    [--multitext multitext | -m multitext]

# expansion memory and subs base

LSANCA-VFTTP-301 (8042 subs) and 
NYCMNY-VFTTP-312 (4664 subs) have both crashed. 
NYCMNY-VFTTP-303 (6678 subs) drops

PRVDRI-VFTTP-303 - 4897
PRVDRI-VFTTP-302 - 2660
PRVDRI-VFTTP-304 – 2342

    NYCMNY-VFTTP-315                                                                     1747 subs

    GOT:             Next Hop     5499904       4194179    99%    125        1%
    GOT:             Next Hop     5499904       4194179    99%    125        1%

    NYCMNY-VFTTP-301                                                                     1271 subs
    GOT:             Next Hop     6024192       4193389    99%    915        1%
    GOT:             Next Hop     6024192       4193460    99%    844        1%

    NYCMNY-VFTTP-303                                                                     6678 subs
    GOT:             Next Hop     6024192       4194103    99%    201        1%         
    GOT:             Next Hop     6024192       4194107    99%    197        1%


NYCMNY-VFTTP-303 mem drop
=========================

    Jun 20 14:48:12  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC0 PFE0: 7072768 bytes. Safely above threshold.
    Jun 20 14:48:12  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC0 PFE1: 5499904 bytes. Safely above threshold.
    Jun 20 14:48:22  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC1 PFE0: 7072768 bytes. Safely above threshold.
    Jun 20 14:48:22  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC1 PFE1: 5499904 bytes. Safely above threshold.
    …
    Jun 20 15:48:12  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC0 PFE0: 7072768 bytes. Safely above threshold.
    Jun 20 15:48:12  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC0 PFE1: 4975616 bytes. Safely above threshold.
    Jun 20 15:48:22  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC1 PFE0: 7072768 bytes. Safely above threshold.
    Jun 20 15:48:22  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC1 PFE1: 4975616 bytes. Safely above threshold.

    Jun 20 15:05:30  NYCMNY-VFTTP-303_RE0 mgd[90221]: UI_CMDLINE_READ_LINE: User 'vnm108erx', command 'delete interfaces demux0 unit 22280051 '
    Jun 20 15:05:30  NYCMNY-VFTTP-303_RE0 mgd[90221]: UI_CMDLINE_READ_LINE: User 'vnm108erx', command 'delete system services dhcp-local-server group vol interface demux0.22280051 '
    Jun 20 15:05:30  NYCMNY-VFTTP-303_RE0 mgd[90221]: UI_CMDLINE_READ_LINE: User 'vnm108erx', command 'commit and-quit '


    Jun 21 15:02:59  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC0 PFE0: 7072768 bytes. Safely above threshold.
    Jun 21 15:02:59  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC0 PFE1: 4975616 bytes. Safely above threshold.
    …
    Jun 21 15:08:00  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC0 PFE0: 7072768 bytes. Safely above threshold.
    Jun 21 15:08:00  NYCMNY-VFTTP-303_RE0 cscript: PFE next-hop memory utilization: FPC0 PFE1: 4451328 bytes. Safely above threshold.

compare work
============

compared:
* config file           (2013-0619)
* config changes        (2013-0614 Jun 14 12:30)

## config file

NYCMNY-VFTTP-303 router has more subs/demux0 sub-i/f, some more multicast subs

    NYCMNY-VFTTP-303 - 6678SUBS     PRVDRI-VFTTP-303 - 4897SUBS

    +-----14219 lines: group vol    +-----10170 lines: group vol
    +--58532 lines: interfaces      +--41720 lines: interfaces
    +---3494 lines: vol-voip        +---2538 lines: vol-voip

    multicast {
        interface demux0.20190029 apply-groups COS-SUB-MCAST-01;
        interface demux0.20510067 apply-groups COS-SUB-MCAST-01;
        interface demux0.22100016 apply-groups COS-SUB-MCAST-01;
        interface demux0.22420056 apply-groups COS-SUB-MCAST-01;
        interface demux0.22250042 apply-groups COS-SUB-MCAST-01;
        interface demux0.22600020 apply-groups COS-SUB-MCAST-01;
        interface demux0.22110031 apply-groups COS-SUB-MCAST-01;
        interface demux0.20990046 apply-groups COS-SUB-MCAST-01;
        interface demux0.22270032 apply-groups COS-SUB-MCAST-01;
        interface demux0.22590021 apply-groups COS-SUB-MCAST-01;
        interface demux0.21320059 apply-groups COS-SUB-MCAST-01;
        interface demux0.21940054 apply-groups COS-SUB-MCAST-01;
        interface demux0.21000067 apply-groups COS-SUB-MCAST-01;
        interface demux0.21320063 apply-groups COS-SUB-MCAST-01;

    multicast {
        interface demux0.12410016 apply-groups COS-SUB-MCAST-01;

    z427047@NYCMNY-VFTTP-303_RE0> show conf    z427047@PRVDRI-VFTTP-303_RE0> show confi
    ## Last commit: 2013-06-19 15:35:44 UTC by ## Last commit: 2013-06-19 23:32:49 UTC 
    version 11.2S7.4;                          version 11.2S7.4;
    +--1537 lines: groups                      +--1522 lines: groups
    apply-groups [ re0 re1 ALL-GE-INTERFACES-TRapply-groups [ re0 re1 ALL-GE-INTERFACES
    +--1648 lines: dynamic-profiles            +--1648 lines: dynamic-profiles
    +--14502 lines: system                     +--10408 lines: system
    +-- 69 lines: chassis                      +-- 71 lines: chassis
    +--58532 lines: interfaces                 +--41720 lines: interfaces
    +--  7 lines: forwarding-options           +-- 31 lines: forwarding-options
    +-- 10 lines: event-options                +-- 10 lines: event-options
    +--  3 lines: event-script                 +--  3 lines: event-script
    }                                          }
    +--143 lines: snmp                         +--142 lines: snmp
    +--  3 lines: accounting-options           +--  3 lines: accounting-options
    +--508 lines: routing-options              +--227 lines: routing-options
    +--312 lines: protocols                    +--273 lines: protocols
    +--1036 lines: policy-options              +--1004 lines: policy-options
    +--1042 lines: class-of-service            +--922 lines: class-of-service
    +--4860 lines: firewall                    +--4908 lines: firewall
    +--323 lines: access                       +--272 lines: access
    +--3496 lines: routing-instances           +--2540 lines: routing-instances
    +-- 45 lines: services                     +-- 53 lines: services
    access-profile ACCESS_PROFILE-VZ_DHCPUSER; access-profile ACCESS_PROFILE-VZ_DHCPUSER
    +-- 26 lines: diameter                     +-- 26 lines: diameter

complete/detail config diff:

[config diff(big +50M!,download and open locally)](http://www-in.juniper.net/~pings/casedata/2013-0615-0089/diff-config-20130619-NYCMNY-VFTTP-303-vs-PRVDRI-VFTTP-303.html)

## config change

                            NYCMNY          PRVDRI
    all command lines       5773            2605
    all config change       2381            1058
    all submitted commit    285             114

