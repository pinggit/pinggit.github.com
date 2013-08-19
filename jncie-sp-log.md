<p>TABLE OF CONTENT</p>
<hr />
<div class="toc">
<ul>
<li><a href="#jncie-logs">JNCIE logs</a><ul>
<li><a href="#troubleshooting-pre-config">troubleshooting pre-config</a></li>
<li><a href="#device">Device</a><ul>
<li><a href="#device-task">Device Task</a></li>
<li><a href="#configtransfer-on-commit">config:transfer-on-commit</a></li>
<li><a href="#configfirewall-filter-on-r23">config:firewall filter on R2/3</a></li>
<li><a href="#config-lag">config LAG</a></li>
<li><a href="#config-graceful-restart">config graceful restart</a></li>
<li><a href="#config-bfd">config BFD</a></li>
<li><a href="#verifytransfer-on-commit">verify:transfer-on-commit</a></li>
<li><a href="#tips-firewall-filter-dont-forget-the-last-term-of-then-accept">TIPS: firewall filter: don't forget the last term of then accept</a></li>
<li><a href="#verify-gr">verify: GR</a></li>
<li><a href="#question-gres-nsr-gr">QUESTION: GRES, NSR, GR</a></li>
<li><a href="#verify-bfd">verify BFD</a></li>
<li><a href="#tip-detect-bfd-interval">TIP: detect BFD interval</a></li>
<li><a href="#tips-about-apply-groups">TIPS: about apply-groups</a></li>
<li><a href="#question-important-scp-doesnt-work">QUESTION: IMPORTANT: scp doesn't work</a></li>
<li><a href="#questionresolved-about-apply-group-except">QUESTION(resolved): about apply-group-except</a></li>
</ul>
</li>
<li><a href="#igp">IGP</a><ul>
<li><a href="#igp-task">IGP task</a></li>
<li><a href="#configigp-policy">config:IGP policy</a></li>
<li><a href="#configno-ipv6-routes-allowed-in-isis">config:no IPv6 routes allowed in ISIS</a></li>
<li><a href="#config-isis-metric">config: isis metric</a></li>
<li><a href="#verify-igp-policy">verify IGP policy</a><ul>
<li><a href="#dc-r2-all-rs">DC =&gt; R2 =&gt; all Rs</a></li>
<li><a href="#r2-dc-summarization">R2 =&gt; DC: summarization</a></li>
<li><a href="#r2-dc-conditional-default-routes">R2 =&gt; DC: conditional default routes</a></li>
</ul>
</li>
<li><a href="#verifyigp-policy">verify:IGP policy</a></li>
<li><a href="#verifyisis-metric">verify:isis metric</a></li>
<li><a href="#tips-conditional-routes">TIPS: conditional routes</a></li>
</ul>
</li>
<li><a href="#mpls">MPLS</a><ul>
<li><a href="#mpls-task">MPLS task</a></li>
<li><a href="#configmpls-interfaces">config:MPLS interfaces</a></li>
<li><a href="#tip-interface-family-mpls-vs-protocol-mpls-interface">TIP: interface family mpls vs. protocol mpls interface</a></li>
<li><a href="#configicmp-tunneling-not-required">config:icmp-tunneling (not required)</a></li>
<li><a href="#configrsvp">config:RSVP</a></li>
<li><a href="#configldp">config:LDP</a></li>
<li><a href="#verify-ldp">verify LDP</a></li>
<li><a href="#configr2ero">config:R2:ERO</a></li>
<li><a href="#verifyero">verify:ERO</a></li>
<li><a href="#configr2link-protection">config:R2:link-protection</a></li>
<li><a href="#verifylink-protection">verify:link-protection</a></li>
<li><a href="#configr4secondary-path">config:R4:secondary path</a></li>
<li><a href="#verifyr4secondary-path">verify:R4:secondary path</a></li>
<li><a href="#configr3-link-coloring">config:R3: link coloring</a></li>
<li><a href="#verify-link-coloring">verify: link coloring</a></li>
<li><a href="#question-link-color-need-on-both-side">QUESTION: link color need on both side?</a></li>
<li><a href="#configlsp-preemption">config:LSP preemption</a></li>
<li><a href="#verify-preemption">verify: preemption</a></li>
<li><a href="#config-ipv6-tunnel">config: Ipv6 tunnel</a></li>
<li><a href="#config-r5-no-label-0">config: R5: no label 0</a></li>
<li><a href="#configlsp-policer">config:LSP policer</a></li>
<li><a href="#tip-rsvp-resv-style-ff-vs-seadaptive">TIP: RSVP resv style: FF vs. SE(adaptive)</a></li>
<li><a href="#question-how-to-verify-it-works-or-not">QUESTION: how to verify it works or not?</a></li>
<li><a href="#question-how-to-config-lsp-lb-in-123">QUESTION: how to config LSP LB in 12.3</a></li>
</ul>
</li>
<li><a href="#bgp">BGP</a><ul>
<li><a href="#bgp-task">BGP task</a></li>
<li><a href="#ipv4-task">IPv4 task</a></li>
<li><a href="#pre-configbasic-bgp-rr-vpn">pre-config:basic BGP RR VPN</a><ul>
<li><a href="#r148-vpn-part-b">R1/4/8 VPN (Part B)</a></li>
<li><a href="#r7-vpn-part-a">R7 VPN: (PART A)</a></li>
<li><a href="#r23-vpn-rr">R2/3 VPN RR:</a></li>
<li><a href="#r2-r3">R2-R3</a></li>
<li><a href="#inet-rr">inet RR</a></li>
<li><a href="#r5-r6">R5-R6</a></li>
<li><a href="#ptc">P/T/C</a></li>
</ul>
</li>
<li><a href="#verifypreconfig">verify:preconfig</a></li>
<li><a href="#tip-policy-internalexteral-vs-route-type-internalexternal">TIP: policy "internal/exteral" vs. "route-type internal/external"</a></li>
<li><a href="#configas-migration">config:AS migration</a></li>
<li><a href="#verify-as-migrationhide">verify: AS migration/hide</a></li>
<li><a href="#configipv4-ipv6-rr-r5r6">config:IPv4 IPv6 RR: R5/R6</a></li>
<li><a href="#config-troubleshooting-pre-config">config: troubleshooting pre-config</a></li>
<li><a href="#config-1-all-cpt-facing-r-import-tag-routes">config 1: all C/P/T facing R: import : tag routes</a></li>
<li><a href="#verify-route-tagging">verify: route tagging</a></li>
<li><a href="#config-2-all-pt-facing-r-export-reject-pt-routes">config 2: all P/T facing R: export: reject P(T) routes</a></li>
<li><a href="#verify-route-rejection">verify: route rejection</a></li>
<li><a href="#tip-6pe">TIP: 6PE</a><ul>
<li><a href="#6pe-all-4-solutions">6PE all 4 solutions</a></li>
<li><a href="#routing">routing:</a></li>
<li><a href="#in-lab">in lab</a></li>
<li><a href="#pe-to-ce">PE to CE</a></li>
<li><a href="#pe-to-pe">PE to PE</a></li>
<li><a href="#1">场景1:</a></li>
<li><a href="#2">场景2:</a></li>
<li><a href="#">规范规则</a></li>
</ul>
</li>
<li><a href="#config6pepe-ce">config:6PE:PE-CE</a></li>
<li><a href="#verify-pe-ce">verify: PE-CE</a><ul>
<li><a href="#without-accept-remote-nexthop-and-nh-changing-policy">without accept-remote-nexthop and nh changing policy</a></li>
<li><a href="#with-accept-remote-nexthop">with accept-remote-nexthop</a></li>
<li><a href="#fix-incoming-nh-with-import-policy">fix incoming NH with import policy</a></li>
</ul>
</li>
<li><a href="#config6pepe-pe">config:6PE:PE-PE</a></li>
<li><a href="#verify-pe-pe">verify: PE-PE</a></li>
<li><a href="#verify6pe-label-pathc3-c4">verify:6PE label path:C3-C4</a></li>
<li><a href="#config-rtbh">config: RTBH</a></li>
<li><a href="#verify-rtbh">verify: RTBH</a></li>
<li><a href="#config-ipv6-routes-aggregation">config: IPv6 routes aggregation</a></li>
<li><a href="#tip-r2-policy-term4-is-a-must">TIP: R2 policy term4 is a must</a></li>
<li><a href="#note-suppress-specific-route-including-c-or-not">NOTE: suppress specific route , including C or not</a></li>
<li><a href="#verify-ipv6-aggr">verify IPv6 aggr</a></li>
<li><a href="#tip-unverified-route">TIP: unverified route</a></li>
<li><a href="#tip-missing-rid-on-a-pure-ipv6-router">TIP: missing RID on a pure IPv6 router</a></li>
</ul>
</li>
<li><a href="#interas-vpn-part-a">InterAS VPN (PART A)</a><ul>
<li><a href="#config-interas-vpn">config: InterAS VPN</a></li>
<li><a href="#config-r1-vrf-to-local-ce">config: R1 VRF to local CE</a></li>
<li><a href="#verify-e2e-pingtraceroute">verify: e2e ping/traceroute</a></li>
<li><a href="#tip-inet-labeled-unicast-resolve-vpn">TIP: inet labeled-unicast resolve-vpn</a></li>
<li><a href="#tip-find-out-communities">TIP: find out communities</a></li>
<li><a href="#tip-policy-from-rib-inet3">TIP: policy "from rib inet.3"</a></li>
<li><a href="#tip-interas-vpn-options">TIP: interAS VPN options</a></li>
<li><a href="#tip-family-in-diff-levels">TIP: family in diff levels</a></li>
<li><a href="#tip-bgp-keep-all">TIP: bgp keep-all</a></li>
<li><a href="#questionresolved-bgp-flaps-duing-config">QUESTION(resolved): bgp flaps duing config</a></li>
<li><a href="#toggle-traffic-engineering-mpls-forwarding">toggle traffic-engineering mpls-forwarding</a></li>
<li><a href="#config-solution1old">config solution1(old):</a></li>
<li><a href="#solution2-inet-resolved-vpn">solution2: inet resolved-vpn</a></li>
</ul>
</li>
<li><a href="#vpls-part-a">VPLS (PART A)</a><ul>
<li><a href="#prepareborrow-ae-ports-to-be-used-as-vpls-ports">prepare:borrow ae ports to be used as vpls ports</a></li>
<li><a href="#config-vpls">config vpls</a></li>
<li><a href="#verify-vpls">verify vpls</a><ul>
<li><a href="#r1-vpls-connection">R1 vpls connection</a></li>
<li><a href="#r7-vpls-connection">R7 vpls connection</a></li>
<li><a href="#r8-vpls-connection">R8 vpls connection</a></li>
<li><a href="#vpls-forwarding-table-no-traffic">vpls forwarding-table (no traffic)</a></li>
<li><a href="#vpls-forwarding-table-with-traffic">vpls forwarding table (with traffic)</a></li>
<li><a href="#bridge-bridge-domain-per-instance">bridge bridge domain (per-instance)</a></li>
<li><a href="#bridge-interface-statistics">bridge interface statistics</a></li>
</ul>
</li>
<li><a href="#config-vpls-firewall-policer">config: vpls firewall policer</a></li>
<li><a href="#tip-vpls-link-redundency-issue">TIP: vpls link redundency issue</a></li>
<li><a href="#tip-encapsulation-extended-vlan-vpls-and-flexible-ethernet-services">TIP: encapsulation extended-vlan-vpls and flexible-ethernet-services</a></li>
<li><a href="#2-commit-errors">2 commit errors</a></li>
</ul>
</li>
<li><a href="#vpn-part-b">VPN (PART B)</a><ul>
<li><a href="#vpn-internet-access-task">VPN internet access task</a></li>
<li><a href="#config-basic-vpn">config: basic VPN</a><ul>
<li><a href="#r1">R1:</a></li>
<li><a href="#r4">R4:</a></li>
<li><a href="#r8">R8:</a></li>
</ul>
</li>
<li><a href="#config-vpn-policy">config: VPN policy</a></li>
<li><a href="#verify-bgpospf-connections">verify bgp/ospf connections</a></li>
<li><a href="#verify-vpn-table">verify: VPN table</a><ul>
<li><a href="#vrf-r1">VRF: R1</a></li>
<li><a href="#vrf-r4">VRF: R4</a></li>
</ul>
</li>
<li><a href="#verify-solution1-data-plane-e2e-pingtraceroute">verify solution1 data plane: e2e ping/traceroute</a></li>
<li><a href="#config-shamlink">config: shamlink</a></li>
<li><a href="#verify1-shamlink">verify1: shamlink</a></li>
<li><a href="#verify2-shamlink">verify2: shamlink</a></li>
<li><a href="#config-vpn-inetaccess-1">config: VPN InetAccess 1</a></li>
<li><a href="#verify-solution-1-e2e-pingtrace">verify solution 1 e2e ping/trace</a></li>
<li><a href="#config-vpn-inetaccess-2">config: VPN InetAccess 2</a></li>
<li><a href="#verify-solution-2-pingtraceroute">verify : solution 2 ping/traceroute</a></li>
<li><a href="#config-vpn-lsp-map">config vpn LSP map</a></li>
<li><a href="#verify-vpn-lsp-map">verify vpn LSP map</a></li>
<li><a href="#tip-sham-link">TIP: sham-link</a></li>
<li><a href="#tip-domain-id">TIP: domain-id</a></li>
<li><a href="#tip-traceroute-under-mpls-vpn">TIP: traceroute under mpls vpn</a></li>
<li><a href="#tip-vrf-table-lable-vs-tunneled-interface">TIP: vrf-table-lable vs. tunneled-interface</a></li>
<li><a href="#tip-about-next-hop-next-table-greeninet0">TIP: about next-hop next-table GREEN.inet.0</a></li>
<li><a href="#tip-icmp-tunneling">TIP: icmp-tunneling</a></li>
<li><a href="#tip-about-local-as">TIP: about local-as</a></li>
<li><a href="#tip-import-rib-and-export-rib">TIP: import-rib and export-rib</a></li>
<li><a href="#solution-1-old-notes">solution 1 old notes</a><ul>
<li><a href="#source-internet-r1-adv-aggr-vpn-routes-from-r1">source Internet =&gt; R1 : adv aggr. vpn routes from R1</a></li>
<li><a href="#r1-r1vrf-r1-static-route-with-next-table">R1 =&gt; R1:vrf : R1: static route with next table</a><ul>
<li><a href="#other-r-got-aggr-vpn-routes-from-r1">other R got aggr. vpn routes from R1</a></li>
</ul>
</li>
<li><a href="#r1vrf-dest-ce-current-behavior-no-need-extra-config">R1:vrf =&gt; dest CE : current behavior, no need extra config</a></li>
<li><a href="#source-ce-r1vrf-r1vrf-adv-a-default-to-ce-via-ospf">source CE -&gt; R1:vrf : R1:vrf adv a default to CE via ospf</a><ul>
<li><a href="#ce1-routes-after-r1green-exp-default-to-ce1-via-ospf">ce1 routes after R1:GREEN exp default to ce1 via ospf</a></li>
</ul>
</li>
<li><a href="#same-for-other-ce-adjacent-rvrf-r1vrf-export-the-default-route-to-all-sites">same for other CE -&gt; adjacent R:VRF : R1:vrf export the default route to all sites</a></li>
<li><a href="#r1vrf-r1-internet-r1-leak-internet-means-bgp-table-into-r1-vrf">R1:vrf -&gt; R1 -&gt; Internet : R1 leak Internet (means bgp) table into R1 vrf</a><ul>
<li><a href="#original-r1vrfgreeninet0-table">original R1:vrf(GREEN.inet.0) table</a></li>
<li><a href="#r1greeninet0-after-rib-group-r1inet0-r1greeninet0">R1:GREEN.inet.0 , after rib-group: R1:inet.0 -&gt; R1:GREEN.inet.0</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#solution-2-old-notes">solution 2 old notes</a><ul>
<li><a href="#remove-solution1">remove solution1</a></li>
<li><a href="#solution2-config">solution2 config</a></li>
<li><a href="#r1-internet-r1-static-to-r23">R1 =&gt; Internet : R1 : static to R2/3</a></li>
<li><a href="#r1vrf-r1-internet-r1-copy-route-into-vrf">R1:vrf =&gt; R1 =&gt; Internet : R1 copy route into vrf</a></li>
<li><a href="#other-rvrf-r1vrf-internet-adv-default-to-other-site">other R:vrf =&gt; R1:vrf (=&gt; Internet) : adv default to other site</a></li>
<li><a href="#internet-r1-r1-adv-an-aggr-route-out">Internet =&gt; R1 : R1: adv an aggr route out</a></li>
<li><a href="#r1-vrf-look-up-vpn-aggr-routes-of-r1-inet0-also-in-vrf-table">R1 =&gt; vrf : look up vpn aggr routes (of R1 inet.0) also in vrf table</a></li>
<li><a href="#ping-test">ping test</a></li>
<li><a href="#remove-solution-2">remove solution 2</a></li>
</ul>
</li>
<li><a href="#config-vpn-lsp-map-old">config vpn lsp map (old)</a><ul>
<li><a href="#verify">verify</a></li>
</ul>
</li>
<li><a href="#config-vpn-inetaccess-3-tbc">config: VPN InetAccess 3 (t.b.c)</a><ul>
<li><a href="#remove-sol3">remove sol3</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#cos">COS</a><ul>
<li><a href="#config-cos">config COS</a></li>
<li><a href="#verify-cos">verify cos</a></li>
<li><a href="#tip-qoscos">TIP: QoS/CoS</a><ul>
<li><a href="#key-concepts">key concepts</a></li>
<li><a href="#ip-tosrfc791">IP TOS(RFC791)</a></li>
<li><a href="#dscp">DSCP</a><ul>
<li><a href="#diffserv-field">DiffServ field</a></li>
<li><a href="#behavior-aggregate-ba-forwarding-class">Behavior aggregate (BA): forwarding class</a></li>
<li><a href="#per-hop-behavior-phb-scheduling-algorithm-based-on-fwd-class">Per-hop behavior (PHB): scheduling algorithm based on fwd class</a><ul>
<li><a href="#efexpedited-forwarding-101110">EF(Expedited Forwarding): 101110</a></li>
<li><a href="#afassured-forwarding-001010011100bb0">AF(Assured Forwarding): (001/010/011/100)BB0</a></li>
<li><a href="#nc-or-cscode-selector-aaa000001000-111000">NC or CS(Code Selector): AAA000(001000-111000)</a></li>
<li><a href="#bebest-effort-000000">BE(Best Effort): 000000</a></li>
<li><a href="#redback-device-table">redback device table:</a></li>
<li><a href="#junos-default-forwarding-class">JUNOS default forwarding-class</a></li>
</ul>
</li>
<li><a href="#junos-default-code-point-aliases">JUNOS default code-point-aliases</a></li>
</ul>
</li>
<li><a href="#ipv6-rfc2460-tctraffic-class-8b">IPv6: RFC2460 TC(Traffic Class) 8b</a></li>
<li><a href="#ethernet-8021p-pcppriority-code-point-3b">Ethernet: 802.1p PCP(Priority Code Point) 3b</a></li>
<li><a href="#mpls-tctraffic-class-or-exp-3b">MPLS: TC(Traffic Class) or EXP 3b</a></li>
<li><a href="#junos-tool-chains">JUNOS tool chains</a><ul>
<li><a href="#classifier-ingress-traffic-q-forwarding-class">classifier: ingress traffic ==&gt; Q (forwarding class)</a></li>
<li><a href="#policer-traffic-limit">policer: traffic limit</a></li>
<li><a href="#policy-cos-based-forwarding">policy: Cos Based Forwarding</a></li>
<li><a href="#scheduler-redwredpwfqetc">scheduler: RED/WRED/PWFQ/etc</a></li>
<li><a href="#rewrite-marker">rewrite marker</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#config-cos-old">config COS (old)</a></li>
</ul>
</li>
<li><a href="#misc-notestips">misc notes/tips</a><ul>
<li><a href="#clear-commit-history">clear commit history</a></li>
<li><a href="#ipv6">ipv6</a><ul>
<li><a href="#p1p3-got-all-ipv6-routes">p1/p3 got all ipv6 routes</a></li>
<li><a href="#p2-is-missing-some-ipv6-routes">p2 is missing some IPv6 routes</a></li>
<li><a href="#r2r3-routes">R2/R3 routes</a></li>
<li><a href="#r2r3-routes-from-r5r6-are-hidden">R2/R3 routes from R5/R6 are hidden</a></li>
<li><a href="#r2r3-inet63-missing-r7r8">R2/R3 inet6.3: missing R7/R8</a></li>
<li><a href="#question-r2-hidden-p1p3-route-from-r5">QUESTION: R2 hidden P1/P3 route , from R5?</a></li>
<li><a href="#nh-self-on-rr-r5r6-when-reflecting-between-r2r3-and-r7">NH self on RR (R5/R6) when reflecting between R2/R3 and R7</a></li>
</ul>
</li>
<li><a href="#6pe-more-misc-tips">6PE more misc tips</a><ul>
<li><a href="#tip-ipv6-tunneling-vs-rib-group">TIP: ipv6-tunneling vs rib-group</a></li>
<li><a href="#tip-inet-labeled-unicast-rib-inet3">TIP: inet labeled-unicast rib inet.3</a></li>
<li><a href="#tip-configuring-ipv6-bgp-routes-over-ipv4-transport">TIP: Configuring IPv6 BGP Routes over IPv4 Transport</a><ul>
<li><a href="#accept-remote-nexthop">accept-remote-nexthop</a></li>
</ul>
</li>
<li><a href="#accept-remote-nexthop_1">accept-remote-nexthop</a></li>
<li><a href="#policy-set-next-hop-with-next-hop-peer-address">policy: set next-hop with "next-hop peer-address"</a><ul>
<li><a href="#questionsolved-next-hop-peer-address-didnt-really-change-the-nexthop">QUESTION(solved): next-hop peer-address didn't really change the nexthop?</a></li>
<li><a href="#tips-rib-in-rib-rib-out">TIPS: rib-in, rib, rib-out</a></li>
</ul>
</li>
<li><a href="#questionresolvedhow-c-routers-got-the-ipv6-routes">QUESTION(resolved):how C routers got the IPv6 routes?</a><ul>
<li><a href="#change-next-hop-to-local-ipv6-address-of-export-policy-in-lr">change next-hop to local IPv6 address of export policy in LR</a></li>
</ul>
</li>
<li><a href="#solution-1-installr23-adv-addrr56">solution 1: install@R2/3 + adv addr@R5/6</a><ul>
<li><a href="#install-r7r8-host-into-r23-inet63">install R7/R8 host into R2/3 inet6.3</a></li>
<li><a href="#make-r23-inet63-reachable-from-r7">make R2/3 inet6.3 reachable from R7</a><ul>
<li><a href="#r7-inet63">R7 inet6.3</a></li>
<li><a href="#config-adv-r2r3-from-r5r6">config: adv R2/R3 from R5/R6</a></li>
<li><a href="#r7-iet63-after-policy">R7 iet6.3 after policy</a></li>
<li><a href="#question-do-we-need-do-the-same-on-r6">QUESTION: do we need do the same on R6?</a></li>
</ul>
</li>
<li><a href="#install-both-host-routes-in-both-lsps-in-both-router-r23">install both host routes in both LSPs in both router R2/3</a></li>
</ul>
</li>
<li><a href="#question-ipv6-not-end2end-pingable">QUESTION: ipv6 not end2end pingable</a></li>
<li><a href="#solution2-change-next-hop-at-rr-no-install">solution2 : change next-hop at RR ("no install")</a><ul>
<li><a href="#remove-solution1_1">remove solution1</a></li>
<li><a href="#add-solution-2">add solution 2</a></li>
</ul>
</li>
<li><a href="#solution-3-mixed-solution12">solution 3: mixed solution1&amp;2</a><ul>
<li><a href="#remove-solution-2_1">remove solution 2:</a></li>
</ul>
</li>
<li><a href="#solution-4-rib-rib-group">solution 4: rib + rib-group</a><ul>
<li><a href="#config">config</a></li>
<li><a href="#before">before</a></li>
<li><a href="#after">after</a></li>
<li><a href="#verification-of-rib-group">verification of rib-group</a></li>
<li><a href="#tips-about-ribrib-groupinet3inet63">TIPS: about rib/rib-group/inet.3/inet6.3</a></li>
</ul>
</li>
<li><a href="#question-family-inet-unicast-vs-family-inet-labeled-unicast">QUESTION: family inet unicast vs. family inet labeled-unicast</a></li>
<li><a href="#question-why-family-inet-labeled-unicast-in-this-solution">QUESTION: why family inet labeled-unicast in this solution?</a></li>
<li><a href="#simple-topo-and-config">simple topo and config</a><ul>
<li><a href="#pe1-config">PE1 config</a></li>
<li><a href="#pe2-config">PE2 config</a></li>
<li><a href="#resources">resources</a></li>
<li><a href="#family-inet6-labeled-unicast-vs-unicast">family inet6 labeled-unicast vs unicast</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#rtbh-verify">RTBH verify</a><ul>
<li><a href="#initial-routes">initial routes</a></li>
<li><a href="#config_1">config</a></li>
<li><a href="#result">result</a></li>
</ul>
</li>
<li><a href="#basic-interconnections">basic interconnections</a><ul>
<li><a href="#results">results</a></li>
<li><a href="#issue-no-ce45-routes">issue: no CE4/5 routes</a></li>
<li><a href="#check-routes-in-rr">check routes in RR</a></li>
<li><a href="#solution-non-workadv-inactive-in-rr">solution (non-work):adv-inactive in RR</a></li>
<li><a href="#solution-install-r8-in-r2r3-lsp">solution: install R8 in R2/R3 lsp</a></li>
</ul>
</li>
<li><a href="#backdoor-routes-and-sham-link">backdoor routes and sham-link</a><ul>
<li><a href="#solutionsham-link">solution:sham-link</a></li>
</ul>
</li>
<li><a href="#vpls-old">VPLS (old)</a><ul>
<li><a href="#config_2">config</a></li>
<li><a href="#show-vpls-connection">show vpls connection</a></li>
<li><a href="#show-route-forwarding-table">show route forwarding-table</a><ul>
<li><a href="#with-tunne-service">with tunne-service</a></li>
<li><a href="#without-tunnel-service">without tunnel service</a></li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</div>
<hr />
<h1 id="jncie-logs">JNCIE logs</h1>
<h2 id="troubleshooting-pre-config">troubleshooting pre-config</h2>
<p>IGP：</p>
<ol>
<li>检查每台路由器的 router‐id，确保每台路由器的的 router‐id
   都正确。预配置里面可能有 router‐id 乱配，漏配的现象</li>
<li>检查所有路由器 loopback 0 接口是否都配置了 ISO 地址，地址是否正确</li>
<li>R5 或 R6 的 ISIS 认证密码不正确，造成 ISIS 邻接关系建立不起来</li>
<li>检查所有路由器的 group interface，是否包含了 family iso 和 family mpls，R5
   的预配置只 包含了 family mpls</li>
<li>检查所有的 ISIS 邻接关系都是 level 2</li>
<li>汇聚端口需要手动打上 family iso，family mpls，family inet6</li>
<li>
<p>汇聚端口的物理接口下因为也配置 apply‐group interface，所有我们需要打上
   apply‐groups‐except interface，不然的话，commit 会报错
  
  
BGP：</p>
</li>
<li>
<p>R2 的 BGP 配置有三个 P 邻居和两个 T 邻居，预配置中故意将一个 P 邻居移至
   T group 下，我们需要把它移到 P group 下</p>
</li>
<li>R2 中 BGP group 里面配置了 passive，如果对端路由器也配置了 passive 的话，BGP
   邻居无 法建立</li>
<li>R3 上的 BGP group 下有个 remove‐private‐as ，需要去掉</li>
<li>R5 或者 R6 上有 no‐client‐reflect，去掉，否则路由无法映射</li>
<li>查看各个 RR 的 cluster 是否配置，是否正确配置</li>
<li>R2/R3 全局下应用 apply‐group reject，去掉；有些时候 R2/R3 的 BGP
   下也发现了直接调用 reject 的情况</li>
<li>R5/R6 必须增加 route‐type external</li>
<li>R2 的入方向增加了 65535:65282 即 no‐advertise，R1 的 C3 import 加入
   65535:65281 即 no‐export，有的在 NHS
   策略里面增加了，我们需要把这些改为其它的 community 值</li>
</ol>
<h2 id="device">Device</h2>
<h3 id="device-task">Device Task</h3>
<ol>
<li>bind GE interface between R3 and R6,if any physical link down, the AE
   interface must go down either.</li>
<li>Enable Graceful restart on each core devices R1-R8</li>
<li>R2 and DC are running ospf ,achieve sub-second convergence between them.(
   enable BFD on ospf )</li>
</ol>
<p>NOTE: check the group ‘interface”’s configuration, make sure enable” mpls/iso/inet6” on the AE interface also.</p>
<ol>
<li>
<p>Task 1: 3 points Interfaces facing T routers must discard and log to syslog
   all traffic that comes from the T routers when the incoming packet has an
   IPv4 or IPv6 source address of 10.200.0.0/16 or 2011:0301::/32 respectively,
   which are the ranges used internally.</p>
</li>
<li>
<p>Task 2: 3 points Ensure that all configuration changes on R1 are backed up
   to a server when you commit the changes. The server’s details are shown in
   this section's exhibit.</p>
</li>
</ol>
<h3 id="configtransfer-on-commit">config:transfer-on-commit</h3>
<pre><code>set system archival configuration transfer-on-commit
set system archival configuration archive-sites "ftp://test:test@172.25.84.169/transfer-on-commit/";
#only work for junos, not for linux, don't know why yet
set system archival configuration archive-sites "scp://test:test123@172.25.88.12/var/home/test/"
        #doesn't work on a cygwin/linux server
        "scp://Ping:Juniper1%40@172.25.84.169/transfer-on-commit/";
</code></pre>
<h3 id="configfirewall-filter-on-r23">config:firewall filter on R2/3</h3>
<p>the target should be: block traffic coming from outside AS(like T/P), but
sourcing from IP that is same as internal networks (10.100.x).</p>
<pre><code>set logical-systems r2 firewall family inet filter filter-block-ipv4 term 1 from destination-address 192.168.100.0/24
set logical-systems r2 firewall family inet filter filter-block-ipv4 term 1 then log
set logical-systems r2 firewall family inet filter filter-block-ipv4 term 1 then discard
set logical-systems r2 firewall family inet filter filter-block-ipv4 term 2 then accept
set logical-systems r2 firewall family inet6 filter filter-block-ipv6 term 1 from destination-address 8000::/16
set logical-systems r2 firewall family inet6 filter filter-block-ipv6 term 1 then log
set logical-systems r2 firewall family inet6 filter filter-block-ipv6 term 1 then discard
set logical-systems r2 firewall family inet6 filter filter-block-ipv6 term 2 then accept

set logical-systems r2 interfaces ge-1/2/1 unit 210 family inet filter input filter-block-ipv4
set logical-systems r2 interfaces ge-1/2/1 unit 210 family inet6 filter input filter-block-ipv6
</code></pre>
<h3 id="config-lag">config LAG</h3>
<pre><code>set interfaces ge-1/2/3 apply-groups interface-group
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
</code></pre>
<h3 id="config-graceful-restart">config graceful restart</h3>
<pre><code>set logical-systems r1 routing-options graceful-restart    
set logical-systems r2 routing-options graceful-restart    
set logical-systems r3 routing-options graceful-restart    
set logical-systems r4 routing-options graceful-restart    
set logical-systems r5 routing-options graceful-restart    
set logical-systems r6 routing-options graceful-restart    
set logical-systems r7 routing-options graceful-restart    
set logical-systems r8 routing-options graceful-restart
</code></pre>
<h3 id="config-bfd">config BFD</h3>
<pre><code>set logical-systems r3 protocols isis interface ae10.0 bfd-liveness-detection minimum-interval 300 
set logical-systems r6 protocols isis interface ae11.0 bfd-liveness-detection minimum-interval 300 
set logical-systems r2 protocols ospf area 0 interface ge-1/2/1.210 bfd-liveness-detection minimum-interval 300
</code></pre>
<h3 id="verifytransfer-on-commit">verify:transfer-on-commit</h3>
<pre><code>lab@MX80-NGGWR-02# run show log messages | match transfer 
Aug 11 15:26:03  MX80-NGGWR-02 logger: transfer-file: Transferred /var/transfer/config/MX80-NGGWR-02_juniper.conf.gz_20130811_152551

[edit]
lab@abc# run show system configuration archival

/var/transfer/config/:
total blocks: 8
total files: 0
</code></pre>
<h3 id="tips-firewall-filter-dont-forget-the-last-term-of-then-accept">TIPS: firewall filter: don't forget the last term of <code>then accept</code></h3>
<p>sam "deny all" rule as cisco</p>
<h3 id="verify-gr">verify: GR</h3>
<pre><code>lab@MX80-NGGWR-02# run show route summary logical-system r3 
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
</code></pre>
<h3 id="question-gres-nsr-gr">QUESTION: GRES, NSR, GR</h3>
<p>conceptual difference. need read more.</p>
<h3 id="verify-bfd">verify BFD</h3>
<pre><code>lab@MX80-NGGWR-02# run show bfd session  
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
</code></pre>
<h3 id="tip-detect-bfd-interval">TIP: detect BFD interval</h3>
<p>first config a whatever interval, then check session to read the RX interval
from peer. then change accordingly , if required.</p>
<pre><code>[edit]
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
</code></pre>
<h3 id="tips-about-apply-groups">TIPS: about apply-groups</h3>
<p>it looks <code>apply-groups</code> doesn't necesarily save time/config work, and causing
inheritance to unintented interfaces. but if preconfig already have it, removing
them and reconfig bring more works.</p>
<p>check with: <code>show int routing</code></p>
<pre><code>lab@MX80-NGGWR-01# run show interfaces routing logical-system lr2 
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
</code></pre>
<p>so using <code>apply-group</code> or not, it's sufficient as long as core facing i/f (and
lo0) has the required family:</p>
<pre><code>inet6
iso
mpls
</code></pre>
<h3 id="question-important-scp-doesnt-work">QUESTION: IMPORTANT: scp doesn't work</h3>
<p>this looks succeed, but actually not working (no file a/v in the server)</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# save scp://Ping@172.25.84.169:transfer-on-commit/abc.txt    
Ping@172.25.84.169's password:  
tempfile 0%    0 tempfile     100%  163KB 162.7KB/s   00:00    
Wrote 5444 lines of configuration to 'scp://Ping@172.25.84.169:transfer-on-commit/abc.txt'
</code></pre>
<h3 id="questionresolved-about-apply-group-except">QUESTION(resolved): about <code>apply-group-except</code></h3>
<p>in this lab, under which condition this is required?</p>
<p>A: like in vpls part, need this to exclude other family and only keep vpls
   (otherwise commit check fail)</p>
<pre><code>lab@MX80-NGGWR-01# show logical-systems lr3 interfaces                               
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
</code></pre>
<p>have to config inet6 manually on ae bundle, to make it support an address
family?</p>
<pre><code>lab@MX80-NGGWR-01# show logical-systems lr3 interfaces ae12  
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
</code></pre>
<h2 id="igp">IGP</h2>
<h3 id="igp-task">IGP task</h3>
<ol>
<li>check isis adjacency, only level 2 neighbor will be allowed</li>
<li>R2 and DC are running ospf, on R2, </li>
<li>reject prefix: 172.16.0.0/24~172.16.7.0/24 which learned from DC ,and </li>
<li>redistribute Ospf routes into ISIS with only 2 routes </li>
<li>R2 will send 10.200/16 to DC and </li>
<li>send an default route only when R2 has active BGP routes. </li>
<li>disable ipv6 routing on ISIS</li>
<li>
<p>adjust the GE’s metric to 5 </p>
</li>
<li>
<p>Task 1: 6 points Ensure that all internal IPv4 networks are reachable and
   are visible as IS-IS routes on every internal router. Ensure that all
   internal links participate in IS-IS at Level 2 only. This task will require
   IS-IS troubleshooting. You can assume that interface IP addresses are
   correct and that physical connectivity is established.
   (make basic isis l2 work)</p>
</li>
<li>Task 2: 4 points The routes in this section’s exhibit are being received
   from the data center via OSPF. Ensure that unacceptable prefixes do not
   appear in the routing table of any internal router.
   Ensure that R2 announces the acceptable range of prefixes using IS-IS to all
   internal routers. Advertise the two best summary routes possible and
   suppress the announcement of the more specific routes.
   (R2:ospf import: suppress some routes)
   (R2:isis export: summarize with 2 and adv)</li>
<li>Task 3: 2 points Announce the 10.200.0.0/16 prefix to the data center. Also
   announce a default route to the data center only when BGP routes are present
   on R2.
   (R2:ospf exp: adv only summariazed)
   (R2:ospf exp: adv conditional def)</li>
<li>Task 4: 1 point Ensure that IS-IS link metrics are automatically calculated
   so that a 1-Gbps interface has a metric of 5.
   (isis:ref-bw)</li>
<li>
<p>Task 5: 1 point Ensure that no IPv6 addresses can appear as IS-IS routes.
   (isis: no-ipv6)</p>
<pre><code>.ACCEPTABLE PREFIXES
|=============================================================
|172.16.8/24    |172.16.11/24   |172.16.14/24   |172.16.17/24
|172.16.9/24    |172.16.12/24   |172.16.15/24   |172.16.18/24
|172.16.10/24   |172.16.13/24   |172.16.16/24   |172.16.19/24
|=============================================================

.UNACCEPTABLE PREFIXES
|=================================================
|172.16.0/24    |172.16.3/24    |172.16.6/24
|172.16.1/24    |172.16.4/24    |172.16.7/24
|172.16.2/24    |172.16.5/24    |
|=================================================
</code></pre>
</li>
</ol>
<h3 id="configigp-policy">config:IGP policy</h3>
<p>#ospf import policy: reject some type5 : routes like 172.16.0/24~172.16.7/24 or longer prefix
    set logical-systems r2 policy-options policy-statement imp-ospf-rej-longer term 1 from protocol ospf
    set logical-systems r2 policy-options policy-statement imp-ospf-rej-longer term 1 from route-filter 172.16.0.0/21 orlonger
    set logical-systems r2 policy-options policy-statement imp-ospf-rej-longer term 1 then reject
    set logical-systems r2 policy-options policy-statement imp-ospf-rej-longer term 2 then accept
    set logical-systems r2 protocols ospf import imp-ospf-rej-longer</p>
<p>#isis export policy: summarize 172.16.8~19/24
    set logical-systems r2 routing-options aggregate route 172.16.8.0/21
    set logical-systems r2 routing-options aggregate route 172.16.16.0/22
    set logical-systems r2 policy-options policy-statement exp-isis-from-ospf term 1 from protocol aggregate
    set logical-systems r2 policy-options policy-statement exp-isis-from-ospf term 1 from route-filter 172.16.8.0/21 exact
    set logical-systems r2 policy-options policy-statement exp-isis-from-ospf term 1 from route-filter 172.16.16.0/22 exact
    set logical-systems r2 policy-options policy-statement exp-isis-from-ospf term 1 then accept
    set logical-systems r2 protocols isis export exp-isis-from-ospf</p>
<p>#ospf exprt policy: summarize internal as 10.200/16 and adv a default route to DC
    set logical-systems r2 routing-options aggregate route 10.200.0.0/16</p>
<pre><code>set logical-systems r2 policy-options policy-statement only-if-from-bgp term 1 from protocol bgp
set logical-systems r2 policy-options policy-statement only-if-from-bgp term 1 from route-filter 0.0.0.0/0 prefix-length-range /0-/32
set logical-systems r2 policy-options policy-statement only-if-from-bgp term 1 then accept
set logical-systems r2 policy-options policy-statement only-if-from-bgp term 2 then reject  #&lt;------
set logical-systems r2 routing-options generate route 0.0.0.0/0 policy only-if-from-bgp

set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 1 from protocol aggregate
set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 1 from route-filter 10.200.0.0/16 exact
set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 1 then accept

set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 2 from protocol aggregate
set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 2 from route-filter 0.0.0.0/0 exact
set logical-systems r2 policy-options policy-statement exp-ospf-from-isis term 2 then accept

set logical-systems r2 protocols ospf export exp-ospf-from-isis
</code></pre>
<h3 id="configno-ipv6-routes-allowed-in-isis">config:no IPv6 routes allowed in ISIS</h3>
<pre><code>set logical-systems r1 protocols isis no-ipv6-routing  
set logical-systems r2 protocols isis no-ipv6-routing  
set logical-systems r3 protocols isis no-ipv6-routing  
set logical-systems r4 protocols isis no-ipv6-routing  
set logical-systems r5 protocols isis no-ipv6-routing  
set logical-systems r6 protocols isis no-ipv6-routing  
set logical-systems r7 protocols isis no-ipv6-routing  
set logical-systems r8 protocols isis no-ipv6-routing
</code></pre>
<h3 id="config-isis-metric">config: isis metric</h3>
<pre><code>set logical-systems r1 protocols isis reference-bandwidth 5g
set logical-systems r2 protocols isis reference-bandwidth 5g
set logical-systems r3 protocols isis reference-bandwidth 5g
set logical-systems r4 protocols isis reference-bandwidth 5g
set logical-systems r5 protocols isis reference-bandwidth 5g
set logical-systems r6 protocols isis reference-bandwidth 5g
set logical-systems r7 protocols isis reference-bandwidth 5g
set logical-systems r8 protocols isis reference-bandwidth 5g
</code></pre>
<h3 id="verify-igp-policy">verify IGP policy</h3>
<h4 id="dc-r2-all-rs">DC =&gt; R2 =&gt; all Rs</h4>
<p>R2 received all routes in LSAs</p>
<pre><code>lab@MX80-NGGWR-02# run show ospf database logical-system r2

Area 0.0.0.0
 Type       ID               Adv Rtr           Seq      Age  Opt  Cksum  Len 
Router  *10.200.1.2       10.200.1.2       0x8000000c  1307  0x22 0x6c9c  36
Router   100.0.210.2      100.0.210.2      0x8000000b  1471  0x22 0xa79a  36
Network  100.0.210.2      100.0.210.2      0x80000002  1328  0x22 0x4770  32
    OSPF AS SCOPE link state database
 Type       ID               Adv Rtr           Seq      Age  Opt  Cksum  Len 
Extern  *0.0.0.0          10.200.1.2       0x80000006   300  0x22 0x4394  36        #&lt;------
Extern  *10.200.0.0       10.200.1.2       0x80000008  2293  0x22 0x53af  36        #&lt;------
Extern   172.16.1.0       100.0.210.2      0x80000008  2756  0x22 0xba9   36        #&lt;------
Extern   172.16.2.0       100.0.210.2      0x80000008  2613  0x22 0xffb3  36        #&lt;------
Extern   172.16.3.0       100.0.210.2      0x80000008  2471  0x22 0xf4bd  36        #&lt;------
Extern   172.16.4.0       100.0.210.2      0x80000008  2328  0x22 0xe9c7  36        #&lt;------
Extern   172.16.5.0       100.0.210.2      0x80000008  2185  0x22 0xded1  36        #&lt;------
Extern   172.16.6.0       100.0.210.2      0x80000008  2042  0x22 0xd3db  36        #&lt;------
Extern   172.16.7.0       100.0.210.2      0x80000008  1899  0x22 0xc8e5  36        #&lt;------
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
</code></pre>
<p>R2 rejected 172.16.0-7/24 routes from DC</p>
<pre><code>[edit]
test@MX80-NGGWR-02# run show route logical-system lr2 protocol ospf

inet.0: 57 destinations, 59 routes (56 active, 0 holddown, 1 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

172.16.8.0/24      *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.9.0/24      *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.10.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.11.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.12.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.13.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.14.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.15.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.16.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.17.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.18.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
172.16.19.0/24     *[OSPF/150] 09:53:41, metric 0, tag 0
                    &gt; to 192.168.100.2 via ge-1/3/0.1000
224.0.0.5/32       *[OSPF/10] 10:08:17, metric 1
                      MultiRecv
</code></pre>
<p>.R2 then adv via ISIS to all internal Rs, but as 2 summarized routes</p>
<pre><code>test@MX80-NGGWR-02# run show isis database logical-system lr2 MX80-NGGWR-02-lr2.00 detail  
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
   IP prefix: 172.16.8.0/21                   Metric:       10 External Up  #&lt;------
   IP prefix: 172.16.16.0/22                  Metric:       10 External Up  #&lt;------

lab@MX80-NGGWR-02# run show route protocol isis logical-system r3 172.16/16

inet.0: 52 destinations, 71 routes (52 active, 0 holddown, 2 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

172.16.8.0/21      *[IS-IS/165] 00:55:26, metric 15
                    &gt; to 100.0.23.1 via ge-1/2/2.203
172.16.16.0/22     *[IS-IS/165] 00:55:26, metric 15
                    &gt; to 100.0.23.1 via ge-1/2/2.203
</code></pre>
<h4 id="r2-dc-summarization">R2 =&gt; DC: summarization</h4>
<pre><code>lab@MX80-NGGWR-02# run show ospf database logical-system r2 
Extern  *0.0.0.0          10.200.1.2       0x80000006   300  0x22 0x4394  36        #&lt;------
Extern  *10.200.0.0       10.200.1.2       0x80000008  2293  0x22 0x53af  36        #&lt;------

lab@MX80-NGGWR-02# run show route protocol ospf logical-system r0 table dc.inet.0

dc.inet.0: 24 destinations, 24 routes (24 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

0.0.0.0/0          *[OSPF/150] 01:15:12, metric 0, tag 0
                    &gt; to 100.0.210.1 via ge-1/2/2.210
10.200.0.0/16      *[OSPF/150] 01:15:12, metric 0, tag 0
                    &gt; to 100.0.210.1 via ge-1/2/2.210
224.0.0.5/32       *[OSPF/10] 05:44:28, metric 1
                      MultiRecv
</code></pre>
<h4 id="r2-dc-conditional-default-routes">R2 =&gt; DC: conditional default routes</h4>
<p>DC got sum route of internal addr, but no default since not in R2's bgp route</p>
<pre><code>test@MX80-NGGWR-02# run show ospf route logical-system ldc 
Topology default Route Table:

Prefix             Path  Route      NH       Metric NextHop       Nexthop      
                   Type  Type       Type            Interface     Address/LSP
10.10.1.2          Intra AS BR      IP            1 ge-1/3/1.1000 192.168.100.1
10.10.0.0/16       Ext2  Network    IP            0 ge-1/3/1.1000 192.168.100.1     &lt;------
192.168.100.0/24   Intra Network    IP            1 ge-1/3/1.1000

test@MX80-NGGWR-02# run show route logical-system lr2 0.0.0.0/0 exact

inet.0: 57 destinations, 59 routes (56 active, 0 holddown, 1 hidden)
Restart Complete
</code></pre>
<h3 id="verifyigp-policy">verify:IGP policy</h3>
<pre><code>lab@MX80-NGGWR-02# run show isis route logical-system r1         
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
</code></pre>
<h3 id="verifyisis-metric">verify:isis metric</h3>
<pre><code>lab@MX80-NGGWR-02# run show isis interface logical-system r1 
IS-IS interface database:
Interface             L CirID Level 1 DR        Level 2 DR        L1/L2 Metric
ge-1/2/1.102          2   0x1 Disabled          MX80-NGGWR-02-r2.02      5/5
ge-1/2/1.103          2   0x1 Disabled          MX80-NGGWR-02-r3.03      5/5
lo0.1                 0   0x1 Passive           Passive                 0/0
</code></pre>
<h3 id="tips-conditional-routes">TIPS: conditional routes</h3>
<p>which is right in this case? I think <code>generate route</code></p>
<p>manual:</p>
<p>Generated routes are used as the route of last resort. A packet is forwarded to
the route of last resort when the routing tables have no information about how
to reach that packet’s destination. One use of route generation is to generate
a default route to use if the routing table contains a route from a peer on a
neighboring backbone.</p>
<p>some web research:</p>
<ul>
<li>A <code>static route</code> is the most obvious. You need to be able to reach a certain
  prefix and you specify the next-hop. This is useful when you are not running
  dynamic routing protocols and/or when you want to override what a dynamic
  protocol dictates (since the protocol-preference for a static-route is lower
  -preferred- than that of any dynamic RP).</li>
<li>An <code>aggregate route</code> is a route you define but which is not used for forwarding
  traffic (next-hop is discard or reject). It is purely used to advertise this
  router's connectivity which is why it needs at least one contributing route
  (a route which belongs to the advertised subnet but with a longer mask -
  these are the ones used to forward the traffic). Typically, the aggregate
  route would be advertised into BGP (if it is active thanks to contributing
  routes) - BGP does not like dealing with routes which are too specific - it
  prefers aggregates.</li>
<li>A <code>generated route</code> is technically an aggregate route but which can be used to
  forward traffic. Traffic which matches the generated route (and not more
  specific routes) will be forwarded using the same next-hop as the first
  contributing route. A generated-route is typically combined with a policy to
  match which routes we want to be contributing and thus used as NHs. The
  generated-route is typically the default 0/0 with a policy matching to
  upstream routes - ie: provide connectivity if certain upstream routes exist.</li>
</ul>
<h2 id="mpls">MPLS</h2>
<h3 id="mpls-task">MPLS task</h3>
<ol>
<li>check each router’s LSP, make sure ALL-LSP are up .</li>
<li>you can’t enable LDP on R2/R3, can’t enable RSVP on R7/R8, find a way to
   exchange label between R1/R4and R7/R8.</li>
<li>the LSP r2-r5 must transit on two paths, the primary path transit r4 and r6,
   the secondary path transit r3, both paths must be UP simultaneously.</li>
<li>set up the secondary path for lsp r4-r3,2nd path must remain up and the
   reservation bandwidth is 600m, 2 paths’s first hop must be R2.</li>
<li>LSP r3-r5 can’t pass through the link between r3-r5, achieve this without
   using ERO.</li>
<li>LSP r1-r6 shall be preempted by other LSP</li>
<li>IPV6’s traffic must be tunneled in MPLS </li>
<li>R5/R6 shall not has label “0”</li>
<li>configure LSP r3-r4 , the reservation bandwidth will be 600m and ensure the
   traffics will not exceed 600m either, r3-r4 will not use r3-r2’s link , ERO
   was forbidden</li>
<li>
<p>on R6, configure the load balance based on the ip layer 3 AND MPLS
    first-label information</p>
</li>
<li>
<p>Task 1: 2 points Ensure that R2 and R3 do not use LDP for performing MPLS
   functions.
   (R2/3 RSVP only)</p>
</li>
<li>Task 2: 3 points Ensure that R7 and R8 do not use RSVP for signaling LSPs in
   the network.  Ensure that R1 can exchange label information with both R7 and
   R8. Ensure that the failure of any single router does not prevent this
   communication.
   (R7/8: LDP only)
   (R1 LDPoRSVP to R7/8, no single link failure)</li>
<li>
<p>Task 3: 3 points LSPs have been preconfigured, as shown in this section’s
   exhibit, and are currently operational in the network. (Functionality of
   these LSPs is dependent on completion of previous sections.) Ensure that the
   r2-to-r5 LSP follows the paths as specified in this section’s exhibit.
   Ensure that the r5-to-r2 LSP follows the path as specified in this section’s
   exhibit.</p>
</li>
<li>
<p>Task 4: 2 points Using the existing admin groups, ensure that the r2-to-r5
   LSP avoids the R2–R3 link.</p>
</li>
<li>Task 5: 3 points Configure the r3-to-r4 LSP to reserve 600Mbps of bandwidth
   across the network. Ensure this LSP can be preempted by all other
   RSVP-signaled LSPs in the network.</li>
<li>Task 6: 3 points Use a bypass LSP to improve convergence time for the
   r2-to-r5 LSP in the event of an R6-R5 link failure.</li>
<li>Task 7: 3 points Configure the network so that all IPv6 traffic will be
   tunneled through MPLS LSPs.</li>
<li>Task 8: 1 point Ensure that R5 does not allocate a label value of 0 to any
   IBGP, RSVP or LDP neighbors.</li>
</ol>
<h3 id="configmpls-interfaces">config:MPLS interfaces</h3>
<pre><code>set logical-systems r1 protocols mpls interface ge-1/2/1.102
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
</code></pre>
<h3 id="tip-interface-family-mpls-vs-protocol-mpls-interface">TIP: <code>interface family mpls</code> vs. <code>protocol mpls interface</code></h3>
<p>both is about data plane, one from <code>interface</code> standpoint and the other from
<code>prototol</code> standpoint</p>
<h3 id="configicmp-tunneling-not-required">config:icmp-tunneling (not required)</h3>
<pre><code>set logical-systems r1 protocols mpls icmp-tunneling
set logical-systems r2 protocols mpls icmp-tunneling
set logical-systems r3 protocols mpls icmp-tunneling
set logical-systems r4 protocols mpls icmp-tunneling
set logical-systems r5 protocols mpls icmp-tunneling
set logical-systems r6 protocols mpls icmp-tunneling
set logical-systems r7 protocols mpls icmp-tunneling
set logical-systems r8 protocols mpls icmp-tunneling
</code></pre>
<h3 id="configrsvp">config:RSVP</h3>
<pre><code>set logical-systems r1 protocols rsvp interface ge-1/2/1.102
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
</code></pre>
<h3 id="configldp">config:LDP</h3>
<pre><code>set logical-systems r1 protocols ldp interface lo0.1
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

set logical-systems r1 protocols mpls label-switched-path r1-r5 to 10.200.1.5
set logical-systems r1 protocols mpls label-switched-path r1-r5 ldp-tunneling
set logical-systems r1 protocols mpls label-switched-path r1-r6 to 10.200.1.6
set logical-systems r1 protocols mpls label-switched-path r1-r6 ldp-tunneling

set logical-systems r4 protocols mpls label-switched-path r4-r5 to 10.200.1.5
set logical-systems r4 protocols mpls label-switched-path r4-r5 ldp-tunneling
set logical-systems r4 protocols mpls label-switched-path r4-r6 to 10.200.1.6
set logical-systems r4 protocols mpls label-switched-path r4-r6 ldp-tunneling
</code></pre>
<h3 id="verify-ldp">verify LDP</h3>
<p>LDP sessions: Link LDP &amp; Target LDP</p>
<pre><code>          TLDPoRSVP            LLDP
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
</code></pre>
<h3 id="configr2ero">config:R2:ERO</h3>
<pre><code>set logical-systems r2 protocols mpls label-switched-path r2-r5 to 10.200.1.5
set logical-systems r2 protocols mpls label-switched-path r2-r5 primary via-r4-r6
set logical-systems r2 protocols mpls path via-r4-r6 10.200.1.4 loose
set logical-systems r2 protocols mpls path via-r4-r6 10.200.1.6 loose
</code></pre>
<h3 id="verifyero">verify:ERO</h3>
<pre><code>lab@MX80-NGGWR-02# run show mpls lsp logical-system r2 name r2-r5 ingress extensive  
Ingress LSP: 5 sessions

10.200.1.5
  From: 10.200.1.2, State: Up, ActiveRoute: 0, LSPname: r2-r5
  ActivePath: via-r4-r6 (primary)   #&lt;------
  LSPtype: Static Configured, Penultimate hop popping
  LoadBalance: Random
  Encoding type: Packet, Switching type: Packet, GPID: IPv4
 *Primary   via-r4-r6        State: Up
    Priorities: 7 0
    SmartOptimizeTimer: 180
    Computed ERO (S [L] denotes strict [loose] hops): (CSPF metric: 15)
 100.0.24.2 S 100.0.46.2 S 100.0.56.1 S     #&lt;------
    Received RRO (ProtectionFlag 1=Available 2=InUse 4=B/W 8=Node 10=SoftPreempt 20=Node-ID):
          100.0.24.2 100.0.46.2 100.0.56.1  #&lt;------
    6 Aug 11 15:01:43.138 Selected as active path
    5 Aug 11 15:01:43.137 Record Route:  100.0.24.2 100.0.46.2 100.0.56.1
    4 Aug 11 15:01:43.137 Up
    3 Aug 11 15:01:43.043 Originate Call
    2 Aug 11 15:01:43.043 CSPF: computation result accepted  100.0.24.2 100.0.46.2 100.0.56.1
    1 Aug 11 15:01:13.569 CSPF failed: no route toward 10.200.1.4
  Created: Sun Aug 11 15:00:14 2013
Total 1 displayed, Up 1, Down 0
</code></pre>
<h3 id="configr2link-protection">config:R2:link-protection</h3>
<pre><code>set logical-systems r2 protocols mpls label-switched-path r2-r6 to 10.200.1.6
set logical-systems r2 protocols mpls label-switched-path r2-r6 link-protection
set logical-systems r2 protocols rsvp interface ge-1/2/1.206 link-protection
set logical-systems r6 protocols rsvp interface ge-1/2/2.206 link-protection
</code></pre>
<h3 id="verifylink-protection">verify:link-protection</h3>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show rsvp session logical-system r2 ingress                         
Ingress RSVP: 6 sessions
To              From            State   Rt Style Labelin Labelout LSPname 
10.200.1.1      10.200.1.2      Up       0  1 FF       -        3 r2-r1
10.200.1.3      10.200.1.2      Up       0  1 FF       -        3 r2-r3
10.200.1.4      10.200.1.2      Up       0  1 FF       -        3 r2-r4
10.200.1.5      10.200.1.2      Up       0  1 FF       -   299776 r2-r5
10.200.1.6      10.200.1.2      Up       0  1 SE       -        3 r2-r6
10.200.1.6      10.200.1.2      Up       0  1 SE       -   299920 Bypass-&gt;100.0.26.2        #&lt;------
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
  Record route: &lt;self&gt; 100.0.24.2 100.0.46.2 100.0.56.1  
Total 1 displayed, Up 1, Down 0

[edit]
lab@MX80-NGGWR-02# run show rsvp session logical-system r2 ingress name Bypas-&gt;100.0.26.2 extensive  
Ingress RSVP: 6 sessions
Total 0 displayed, Up 0, Down 0
</code></pre>
<h3 id="configr4secondary-path">config:R4:secondary path</h3>
<blockquote>
<p>set up the secondary path for lsp r4-r3,2nd path must remain up and the
reservation bandwidth is 600m, 2 paths’s first hop must be R2.</p>
</blockquote>
<pre><code>set logical-systems r4 protocols mpls label-switched-path r4-r3 to 10.200.1.3
set logical-systems r4 protocols mpls label-switched-path r4-r3 bandwidth 600m
set logical-systems r4 protocols mpls label-switched-path r4-r3 adaptive    #&lt;--SE
set logical-systems r4 protocols mpls label-switched-path r4-r3 primary via-r2
set logical-systems r4 protocols mpls label-switched-path r4-r3 secondary via-r2-r5 standby #&lt;-- always "up", pre-established

set logical-systems r4 protocols mpls path via-r2 10.200.1.2 strict
set logical-systems r4 protocols mpls path via-r2-r5 10.200.1.2 strict      #&lt;--1st hop must be R2
set logical-systems r4 protocols mpls path via-r2-r5 10.200.1.5 loose
</code></pre>
<h3 id="verifyr4secondary-path">verify:R4:secondary path</h3>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show mpls lsp logical-system r4 name r4-r3 ingress extensive  
Ingress LSP: 5 sessions

10.200.1.3
  From: 10.200.1.4, State: Up, ActiveRoute: 0, LSPname: r4-r3
  ActivePath: via-r2 (primary)
  LSPtype: Static Configured, Penultimate hop popping
  LoadBalance: Random
  Encoding type: Packet, Switching type: Packet, GPID: IPv4
 *Primary   via-r2           State: Up      #&lt;------
    Priorities: 7 0
    Bandwidth: 600Mbps      #&lt;------
    SmartOptimizeTimer: 180
    Computed ERO (S [L] denotes strict [loose] hops): (CSPF metric: 10)
 100.0.24.1 S 100.0.23.2 S          #&lt;------
    Received RRO (ProtectionFlag 1=Available 2=InUse 4=B/W 8=Node 10=SoftPreempt 20=Node-ID):
          100.0.24.1 100.0.23.2
    5 Aug 13 04:04:47.691 Selected as active path
    4 Aug 13 04:04:47.691 Record Route:  100.0.24.1 100.0.23.2
    3 Aug 13 04:04:47.690 Up
    2 Aug 13 04:04:47.590 Originate Call
    1 Aug 13 04:04:47.590 CSPF: computation result accepted  100.0.24.1 100.0.23.2
  Standby   via-r2-r5        State: Up      #&lt;------
    Priorities: 7 0                 ^^
    Bandwidth: 600Mbps
    SmartOptimizeTimer: 180
    Computed ERO (S [L] denotes strict [loose] hops): (CSPF metric: 15)
 100.0.24.1 S 100.0.25.2 S 100.0.35.1 S 
    Received RRO (ProtectionFlag 1=Available 2=InUse 4=B/W 8=Node 10=SoftPreempt 20=Node-ID):
          100.0.24.1 100.0.25.2 100.0.35.1
    4 Aug 13 04:05:16.588 Record Route:  100.0.24.1 100.0.25.2 100.0.35.1
    3 Aug 13 04:05:16.587 Up
    2 Aug 13 04:05:16.560 Originate Call
    1 Aug 13 04:05:16.560 CSPF: computation result accepted  100.0.24.1 100.0.25.2 100.0.35.1
  Created: Tue Aug 13 04:04:07 2013
Total 1 displayed, Up 1, Down 0

[edit]
lab@MX80-NGGWR-02# run show rsvp interface logical-system r4    
RSVP interface: 6 active
                  Active Subscr- Static      Available   Reserved    Highwater
Interface   State resv   iption  BW          BW          BW          mark
ge-1/2/1.406Up         3   100%  1000Mbps    1000Mbps    0bps        0bps       
ge-1/2/2.204Up         4   100%  1000Mbps    400Mbps     600Mbps     600Mbps        #&lt;------
vt-0/0/0.119537667
            Up         0   100%  10Gbps      10Gbps      0bps        0bps       
vt-1/0/0.119537666
            Up         0   100%  10Gbps      10Gbps      0bps        0bps       
vt-1/1/0.119537665
            Up         0   100%  10Gbps      10Gbps      0bps        0bps       
vt-1/2/0.119537664
            Up         0   100%  10Gbps      10Gbps      0bps        0bps
</code></pre>
<h3 id="configr3-link-coloring">config:R3: link coloring</h3>
<blockquote>
<p>LSP r3-r5 can’t pass through the link between r3-r5, achieve this without
using ERO</p>
</blockquote>
<pre><code>set logical-systems r3 protocols mpls admin-groups blue 4

set logical-systems r3 protocols mpls interface ge-1/2/1.305 admin-group blue

set logical-systems r3 protocols mpls label-switched-path r3-r5 to 10.200.1.5
set logical-systems r3 protocols mpls label-switched-path r3-r5 admin-group exclude blue

set logical-systems r5 protocols mpls admin-groups blue 4
set logical-systems r5 protocols mpls interface ge-1/2/2.305 admin-group blue
set logical-systems r5 protocols mpls label-switched-path r5-r3 to 10.200.1.3
</code></pre>
<h3 id="verify-link-coloring">verify: link coloring</h3>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show mpls lsp logical-system r3 ingress name r3-r5 extensive    
Ingress LSP: 5 sessions

10.200.1.5
  From: 10.200.1.3, State: Up, ActiveRoute: 0, LSPname: r3-r5
  ActivePath:  (primary)
  LSPtype: Static Configured, Penultimate hop popping
  LoadBalance: Random
  Encoding type: Packet, Switching type: Packet, GPID: IPv4
 *Primary                    State: Up
    Priorities: 7 0
    SmartOptimizeTimer: 180
          Exclude: blue     #&lt;------
    Computed ERO (S [L] denotes strict [loose] hops): (CSPF metric: 10)
 100.0.23.1 S 100.0.25.2 S          #&lt;------
    Received RRO (ProtectionFlag 1=Available 2=InUse 4=B/W 8=Node 10=SoftPreempt 20=Node-ID):
          100.0.23.1 100.0.25.2
    5 Aug 13 04:04:47.648 Selected as active path
    4 Aug 13 04:04:47.648 Record Route:  100.0.23.1 100.0.25.2
    3 Aug 13 04:04:47.647 Up
    2 Aug 13 04:04:47.508 Originate Call
    1 Aug 13 04:04:47.508 CSPF: computation result accepted  100.0.23.1 100.0.25.2
  Created: Tue Aug 13 04:04:07 2013
Total 1 displayed, Up 1, Down 0
</code></pre>
<h3 id="question-link-color-need-on-both-side">QUESTION: link color need on both side?</h3>
<pre><code>seems no need to config on both side?
</code></pre>
<h3 id="configlsp-preemption">config:LSP preemption</h3>
<blockquote>
<p>LSP r1-r6 shall be preempted by other LSP</p>
</blockquote>
<pre><code>set logical-systems r1 protocols mpls label-switched-path r1-r6 to 10.200.1.6
set logical-systems r1 protocols mpls label-switched-path r1-r6 priority 7 7
</code></pre>
<h3 id="verify-preemption">verify: preemption</h3>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show mpls lsp logical-system r1 ingress name r1-r6 extensive    
Ingress LSP: 7 sessions

10.200.1.6
  From: 10.200.1.1, State: Up, ActiveRoute: 0, LSPname: r1-r6
  ActivePath:  (primary)
  LSPtype: Static Configured, Penultimate hop popping
  LoadBalance: Random
  Encoding type: Packet, Switching type: Packet, GPID: IPv4
 *Primary                    State: Up
    Priorities: 7 7         #&lt;------
    SmartOptimizeTimer: 180
    Computed ERO (S [L] denotes strict [loose] hops): (CSPF metric: 10)
 100.0.12.2 S 100.0.26.2 S 
    Received RRO (ProtectionFlag 1=Available 2=InUse 4=B/W 8=Node 10=SoftPreempt 20=Node-ID):
          100.0.12.2 100.0.26.2
    5 Aug 13 04:04:46.975 Selected as active path
    4 Aug 13 04:04:46.975 Record Route:  100.0.12.2 100.0.26.2
    3 Aug 13 04:04:46.974 Up
    2 Aug 13 04:04:46.948 Originate Call
    1 Aug 13 04:04:46.948 CSPF: computation result accepted  100.0.12.2 100.0.26.2
  Created: Tue Aug 13 04:04:07 2013
Total 1 displayed, Up 1, Down 0
</code></pre>
<h3 id="config-ipv6-tunnel">config: Ipv6 tunnel</h3>
<pre><code>set logical-systems r1 protocols mpls ipv6-tunneling
set logical-systems r2 protocols mpls ipv6-tunneling
set logical-systems r3 protocols mpls ipv6-tunneling
set logical-systems r4 protocols mpls ipv6-tunneling
set logical-systems r5 protocols mpls ipv6-tunneling
set logical-systems r6 protocols mpls ipv6-tunneling
set logical-systems r7 protocols mpls ipv6-tunneling
set logical-systems r8 protocols mpls ipv6-tunneling
</code></pre>
<h3 id="config-r5-no-label-0">config: R5: no label 0</h3>
<p>check and delete "explicit-null"</p>
<h3 id="configlsp-policer">config:LSP policer</h3>
<pre><code>set logical-systems r3 protocols mpls label-switched-path r3-r6 to 10.200.1.6
set logical-systems r3 protocols mpls label-switched-path r3-r6 policing filter lsp-60m

set logical-systems r3 firewall policer 60m if-exceeding bandwidth-limit 60m
set logical-systems r3 firewall policer 60m if-exceeding burst-size-limit 15k
set logical-systems r3 firewall policer 60m then discard

set logical-systems r3 firewall family any filter lsp-60m term 1 then policer 60m
set logical-systems r3 firewall family any filter lsp-60m term 1 then count 60m
set logical-systems r3 firewall policer 60m if-exceeding bandwidth-limit 60m
set logical-systems r3 firewall policer 60m if-exceeding burst-size-limit 15k
set logical-systems r3 firewall policer 60m then discard
</code></pre>
<p>or use auto-policing:</p>
<pre><code>set logical-systems r3 protocols mpls auto-policing class all drop
</code></pre>
<h3 id="tip-rsvp-resv-style-ff-vs-seadaptive">TIP: RSVP resv style: FF vs. SE(adaptive)</h3>
<p>default is Fixed Filter (FF)</p>
<p>keyword: "adaptive": change that to a Shared Explicit (SE) style;</p>
<p>SE style reservations allow resources to be shared among multiple LSPs that
share a common Session Object parameter.</p>
<h3 id="question-how-to-verify-it-works-or-not">QUESTION: how to verify it works or not?</h3>
<h3 id="question-how-to-config-lsp-lb-in-123">QUESTION: how to config LSP LB in 12.3</h3>
<p>http://www.juniper.net/techpubs/en_US/junos12.3/information-products/pathway-pages/config-guide-policy/config-guide-policy.pdf</p>
<p>it looks, these are not supported in MX80</p>
<pre><code>set logical-systems r3 policy-options policy-statement load-balance then load-balance per-packet
set logical-systems r3 policy-options policy-statement load-balance then accept
set logical-systems r3 routing-options forwarding-table export load-balance

set forwarding-options hash-key family inet layer-3
set forwarding-options hash-key family inet layer-4
set forwarding-options hash-key family mpls label-1
set forwarding-options hash-key family mpls label-2
set forwarding-options hash-key family mpls payload ip layer-3-only
</code></pre>
<h2 id="bgp">BGP</h2>
<h3 id="bgp-task">BGP task</h3>
<ol>
<li>R5/R6 will be global RR, R1,R2,R3,R4,R7,R8 will be GRR’s clients </li>
<li>R2/R3 will be VPN RR, R1,R4,R7,R8 will be VRR’s clients</li>
<li>R5/R6 , R2/R3 will set up normal IBGP peer relationship.</li>
<li>Migrate all the core router from AS:65513 to AS:4012345678,but C3 still peer
   with 65513, set up the bgp peer relationship on R1 and hide the 65513 from
   the Core.</li>
<li>all the C devices will receive C/P/T routes, P devices will receive P/C
   routes, T devices will receive T/C routes.</li>
<li>
<p>You can’t change the interface’s address setting on R1/R4/R7, only one NLRI
   are allowed under BGP family stanza ,connect all the IPV6 traffic between
   C/P/T devices according to following rules:</p>
<ul>
<li>C3 and R1 only running IPV4</li>
<li>C4and R7 running IPV4/IPV6 Dual Stack</li>
<li>C5 and R4 only running IPV6</li>
</ul>
</li>
</ol>
<p>Every Core Router has an IPV6 loopback address, the requirements as follows: </p>
<pre><code>* C3/C4 can reach every IPV4 address in the testing topology
* C4/C5 can reach every IPV6 address in the testing topology
</code></pre>
<p>6,Advertising 10.200/16 and 2011:0310::/32 to C/P/T devices, P device can only receive IPV4 prefix less and equal than /20, IPV6 prefix less and equal than /48</p>
<p>lr5/lr6 &lt;==inet/inet6 RR==&gt; lr1/2/3/4/7/8</p>
<pre><code>test@MX80-NGGWR-02# run show bgp summary logical-system lr5    
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
</code></pre>
<p>lr2/lr3 &lt;==inet-vpn RR==&gt; all PE:lr1/4/8</p>
<pre><code>test@MX80-NGGWR-02# run show bgp summary logical-system lr2    
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
</code></pre>
<h3 id="ipv4-task">IPv4 task</h3>
<blockquote>
<p>C 可以达到 C,P,T。P 之间可以互访，T 之间可以互访，P 与 T 之间不能互
访。C3，C4，C5 的路由发给 P 和 T。T 和 P 的也需要发给 C。P 和 T
不能相互发送。不能有次优路径 
      =&gt; block P/T</p>
<p>5,all the C devices will receive C/P/T routes, P devices will receive P/C
routes, T devices will receive T/C routes.
      =&gt; block P/T</p>
<p>6,Advertising 10.200/16 and 2011:0310::/32 to C/P/T devices, P device can only
receive IPV4 prefix less and equal than /20, IPV6 prefix less and equal than
/48
      =&gt; to C/T:
              adv IPv4/IPv6 agg routes
      =&gt; to P:
              adv IPv4/IPv6 agg routes
              block longer IPv4/IPv6 prefix to P</p>
</blockquote>
<h3 id="pre-configbasic-bgp-rr-vpn">pre-config:basic BGP RR VPN</h3>
<h4 id="r148-vpn-part-b">R1/4/8 VPN (Part B)</h4>
<pre><code>set logical-systems r1 protocols bgp group to-vpn-rr type internal
set logical-systems r1 protocols bgp group to-vpn-rr local-address 10.200.1.1
set logical-systems r1 protocols bgp group to-vpn-rr family inet-vpn unicast
set logical-systems r1 protocols bgp group to-vpn-rr neighbor 10.200.1.2
set logical-systems r1 protocols bgp group to-vpn-rr neighbor 10.200.1.3

set logical-systems r8 protocols bgp group to-vpn-rr type internal
set logical-systems r8 protocols bgp group to-vpn-rr local-address 10.200.1.8
set logical-systems r8 protocols bgp group to-vpn-rr family inet-vpn unicast
set logical-systems r8 protocols bgp group to-vpn-rr neighbor 10.200.1.3
set logical-systems r8 protocols bgp group to-vpn-rr neighbor 10.200.1.2

set logical-systems r4 protocols bgp group to-vpn-rr type internal
set logical-systems r4 protocols bgp group to-vpn-rr local-address 10.200.1.4
set logical-systems r4 protocols bgp group to-vpn-rr family inet-vpn unicast
set logical-systems r4 protocols bgp group to-vpn-rr neighbor 10.200.1.2
set logical-systems r4 protocols bgp group to-vpn-rr neighbor 10.200.1.3
</code></pre>
<h4 id="r7-vpn-part-a">R7 VPN: (PART A)</h4>
<pre><code>set logical-systems r1 protocols bgp group to-vpn-rr type internal
set logical-systems r1 protocols bgp group to-vpn-rr local-address 10.200.1.1
set logical-systems r1 protocols bgp group to-vpn-rr family inet-vpn unicast
set logical-systems r1 protocols bgp group to-vpn-rr neighbor 10.200.1.2
set logical-systems r1 protocols bgp group to-vpn-rr neighbor 10.200.1.3

set logical-systems r8 protocols bgp group to-vpn-rr type internal
set logical-systems r8 protocols bgp group to-vpn-rr local-address 10.200.1.8
set logical-systems r8 protocols bgp group to-vpn-rr family inet-vpn unicast
set logical-systems r8 protocols bgp group to-vpn-rr neighbor 10.200.1.3
set logical-systems r8 protocols bgp group to-vpn-rr neighbor 10.200.1.2

set logical-systems r7 protocols bgp group to-vpn-rr type internal
set logical-systems r7 protocols bgp group to-vpn-rr local-address 10.200.1.7
set logical-systems r7 protocols bgp group to-vpn-rr family inet-vpn unicast
set logical-systems r7 protocols bgp group to-vpn-rr neighbor 10.200.1.2
set logical-systems r7 protocols bgp group to-vpn-rr neighbor 10.200.1.3
</code></pre>
<h4 id="r23-vpn-rr">R2/3 VPN RR:</h4>
<pre><code>set logical-systems r2 protocols bgp group vpn-rr type internal
set logical-systems r2 protocols bgp group vpn-rr local-address 10.200.1.2
set logical-systems r2 protocols bgp group vpn-rr family inet-vpn unicast
set logical-systems r2 protocols bgp group vpn-rr cluster 2.2.2.2
set logical-systems r2 protocols bgp group vpn-rr neighbor 10.200.1.1
set logical-systems r2 protocols bgp group vpn-rr neighbor 10.200.1.7
set logical-systems r2 protocols bgp group vpn-rr neighbor 10.200.1.8
set logical-systems r2 protocols bgp group vpn-rr neighbor 10.200.1.4

set logical-systems r3 protocols bgp group vpn-rr type internal
set logical-systems r3 protocols bgp group vpn-rr local-address 10.200.1.3
set logical-systems r3 protocols bgp group vpn-rr family inet-vpn unicast
set logical-systems r3 protocols bgp group vpn-rr cluster 3.3.3.3
set logical-systems r3 protocols bgp group vpn-rr neighbor 10.200.1.1
set logical-systems r3 protocols bgp group vpn-rr neighbor 10.200.1.7
set logical-systems r3 protocols bgp group vpn-rr neighbor 10.200.1.8
set logical-systems r3 protocols bgp group vpn-rr neighbor 10.200.1.4
</code></pre>
<h4 id="r2-r3">R2-R3</h4>
<pre><code>set logical-systems r2 protocols bgp group to-r3 type internal
set logical-systems r2 protocols bgp group to-r3 local-address 10.200.1.2
set logical-systems r2 protocols bgp group to-r3 neighbor 10.200.1.3

set logical-systems r3 protocols bgp group to-r2 type internal
set logical-systems r3 protocols bgp group to-r2 local-address 10.200.1.3
set logical-systems r3 protocols bgp group to-r2 neighbor 10.200.1.2
</code></pre>
<h4 id="inet-rr">inet RR</h4>
<pre><code>set logical-systems r1 protocols bgp group to-v4v6-rr type internal
set logical-systems r1 protocols bgp group to-v4v6-rr local-address 10.200.1.1
set logical-systems r1 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r1 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r1 protocols bgp group to-v4v6-rr neighbor 10.200.1.6

set logical-systems r2 protocols bgp group to-v4v6-rr type internal
set logical-systems r2 protocols bgp group to-v4v6-rr local-address 10.200.1.2
set logical-systems r2 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r2 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r2 protocols bgp group to-v4v6-rr neighbor 10.200.1.6

set logical-systems r3 protocols bgp group to-v4v6-rr type internal
set logical-systems r3 protocols bgp group to-v4v6-rr local-address 10.200.1.3
set logical-systems r3 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r3 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r3 protocols bgp group to-v4v6-rr neighbor 10.200.1.6

set logical-systems r4 protocols bgp group to-v4v6-rr type internal
set logical-systems r4 protocols bgp group to-v4v6-rr local-address 10.200.1.4
set logical-systems r4 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r4 protocols bgp group to-v4v6-rr neighbor 10.200.1.6
set logical-systems r4 protocols bgp group to-v4v6-rr neighbor 10.200.1.5

set logical-systems r7 protocols bgp group to-v4v6-rr type internal
set logical-systems r7 protocols bgp group to-v4v6-rr local-address 10.200.1.7
set logical-systems r7 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r7 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r7 protocols bgp group to-v4v6-rr neighbor 10.200.1.6

set logical-systems r8 protocols bgp group to-v4v6-rr type internal
set logical-systems r8 protocols bgp group to-v4v6-rr local-address 10.200.1.8
set logical-systems r8 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r8 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r8 protocols bgp group to-v4v6-rr neighbor 10.200.1.6

set logical-systems r5 protocols bgp group v4v6-rr type internal
set logical-systems r5 protocols bgp group v4v6-rr local-address 10.200.1.5
set logical-systems r5 protocols bgp group v4v6-rr family inet unicast
set logical-systems r5 protocols bgp group v4v6-rr cluster 5.5.5.5
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.1
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.2
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.3
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.4
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.7
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.8

set logical-systems r6 protocols bgp group v4v6-rr type internal
set logical-systems r6 protocols bgp group v4v6-rr local-address 10.200.1.6
set logical-systems r6 protocols bgp group v4v6-rr family inet unicast
set logical-systems r6 protocols bgp group v4v6-rr cluster 6.6.6.6
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.1
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.2
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.3
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.4
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.8
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.7
</code></pre>
<h4 id="r5-r6">R5-R6</h4>
<pre><code>set logical-systems r5 protocols bgp group to-r6 type internal
set logical-systems r5 protocols bgp group to-r6 local-address 10.200.1.5
set logical-systems r5 protocols bgp group to-r6 family inet unicast
set logical-systems r5 protocols bgp group to-r6 neighbor 10.200.1.6

set logical-systems r6 protocols bgp group to-r5 type internal
set logical-systems r6 protocols bgp group to-r5 local-address 10.200.1.6
set logical-systems r6 protocols bgp group to-r5 family inet unicast
set logical-systems r6 protocols bgp group to-r5 neighbor 10.200.1.5
</code></pre>
<h4 id="ptc">P/T/C</h4>
<pre><code>set logical-systems r1 protocols bgp group to-c3 type external
set logical-systems r1 protocols bgp group to-c3 family inet unicast
set logical-systems r1 protocols bgp group to-c3 family inet6 unicast
set logical-systems r1 protocols bgp group to-c3 neighbor 100.1.33.2 peer-as 300

set logical-systems r4 protocols bgp group to-c5 type external
set logical-systems r4 protocols bgp group to-c5 family inet6 unicast
set logical-systems r4 protocols bgp group to-c5 neighbor ::100.4.35.2 peer-as 500

set logical-systems r7 protocols bgp group to-c4 type external
set logical-systems r7 protocols bgp group to-c4 family inet unicast
set logical-systems r7 protocols bgp group to-c4 family inet6 unicast
set logical-systems r7 protocols bgp group to-c4 neighbor 100.7.34.2 peer-as 400

set logical-systems r2 protocols bgp group to-p-v4 type external
set logical-systems r2 protocols bgp group to-p-v4 family inet unicast
set logical-systems r2 protocols bgp group to-p-v4 neighbor 100.2.11.2 peer-as 1000
set logical-systems r2 protocols bgp group to-p-v4 neighbor 100.2.12.2 peer-as 2000
set logical-systems r2 protocols bgp group to-p-v4 neighbor 100.2.13.2 peer-as 3000
set logical-systems r2 protocols bgp group to-t-v4 type external
set logical-systems r2 protocols bgp group to-t-v4 family inet unicast
set logical-systems r2 protocols bgp group to-t-v4 neighbor 100.2.22.2 peer-as 1200
set logical-systems r2 protocols bgp group to-t-v4 neighbor 100.2.21.2 peer-as 1100
set logical-systems r2 protocols bgp group to-p-v6 type external
set logical-systems r2 protocols bgp group to-p-v6 family inet6 unicast
set logical-systems r2 protocols bgp group to-p-v6 neighbor ::100.2.11.2 peer-as 1000
set logical-systems r2 protocols bgp group to-p-v6 neighbor ::100.2.12.2 peer-as 2000
set logical-systems r2 protocols bgp group to-p-v6 neighbor ::100.2.13.2 peer-as 3000
set logical-systems r2 protocols bgp group to-t-v6 type external
set logical-systems r2 protocols bgp group to-t-v6 family inet6 unicast
set logical-systems r2 protocols bgp group to-t-v6 neighbor ::100.2.21.2 peer-as 1100
set logical-systems r2 protocols bgp group to-t-v6 neighbor ::100.2.22.2 peer-as 1200

set logical-systems r3 protocols bgp group to-p-v4 type external
set logical-systems r3 protocols bgp group to-p-v4 family inet unicast
set logical-systems r3 protocols bgp group to-p-v4 neighbor 100.3.11.2 peer-as 1000
set logical-systems r3 protocols bgp group to-p-v4 neighbor 100.3.12.2 peer-as 2000
set logical-systems r3 protocols bgp group to-t-v4 type external
set logical-systems r3 protocols bgp group to-t-v4 family inet unicast
set logical-systems r3 protocols bgp group to-t-v4 neighbor 100.3.21.2 peer-as 1100
set logical-systems r3 protocols bgp group to-t-v4 neighbor 100.3.22.2 peer-as 1200
set logical-systems r3 protocols bgp group to-p-v6 type external
set logical-systems r3 protocols bgp group to-p-v6 family inet6 unicast
set logical-systems r3 protocols bgp group to-p-v6 neighbor ::100.3.11.2 peer-as 1000
set logical-systems r3 protocols bgp group to-p-v6 neighbor ::100.3.12.2 peer-as 2000
set logical-systems r3 protocols bgp group to-t-v6 type external
set logical-systems r3 protocols bgp group to-t-v6 family inet6 unicast
set logical-systems r3 protocols bgp group to-t-v6 neighbor ::100.3.21.2 peer-as 1100
set logical-systems r3 protocols bgp group to-t-v6 neighbor ::100.3.22.2 peer-as 1200

set logical-systems r5 protocols bgp group to-p-v4 type external
set logical-systems r5 protocols bgp group to-p-v4 family inet unicast
set logical-systems r5 protocols bgp group to-p-v4 neighbor 100.5.12.2 peer-as 2000
set logical-systems r5 protocols bgp group to-p-v4 neighbor 100.5.13.2 peer-as 3000
set logical-systems r5 protocols bgp group to-p-v6 type external
set logical-systems r5 protocols bgp group to-p-v6 family inet6 unicast
set logical-systems r5 protocols bgp group to-p-v6 neighbor ::100.5.12.2 peer-as 2000
set logical-systems r5 protocols bgp group to-p-v6 neighbor ::100.5.13.2 peer-as 3000
</code></pre>
<h3 id="verifypreconfig">verify:preconfig</h3>
<pre><code>lab@MX80-NGGWR-02# run show bgp summary logical-system r2                 
Groups: 7 Peers: 17 Down peers: 0
Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
inet.0               
                      33         15          0          0          0          0
inet.3               
                       8          3          0          0          0          0
inet6.0              
                      43         24          0          0          0          0
bgp.l3vpn.0          
                      16         16          0          0          0          0
bgp.l2vpn.0          
                       0          0          0          0          0          0
Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
10.200.1.1       4012345678        157        160       0       0     1:09:57 Establ
  bgp.l3vpn.0: 5/5/5/0
10.200.1.3       4012345678        152        151       0       0     1:09:28 Establ
  bgp.l2vpn.0: 0/0/0/0
10.200.1.4       4012345678        158        157       0       0     1:09:42 Establ
  bgp.l3vpn.0: 6/6/6/0
10.200.1.5       4012345678        191        164       0       0     1:09:59 Establ
  inet.0: 10/15/14/0
  inet.3: 3/4/4/0
  inet6.0: 18/19/19/0
10.200.1.6       4012345678        202        163       0       0     1:09:57 Establ
  inet.0: 0/13/12/0
  inet.3: 0/4/4/0
  inet6.0: 1/19/19/0
10.200.1.7       4012345678        155        162       0       0     1:09:50 Establ
  bgp.l3vpn.0: 0/0/0/0
10.200.1.8       4012345678        156        160       0       0     1:09:46 Establ
  bgp.l3vpn.0: 5/5/5/0
100.2.11.2             1000        152        162       0       0     1:09:58 Establ
  inet.0: 1/1/1/0
100.2.12.2             2000        151        159       0       0     1:09:54 Establ
  inet.0: 1/1/1/0
100.2.13.2             3000        152        159       0       0     1:09:51 Establ
  inet.0: 1/1/1/0
100.2.21.2             1100        152        164       0       0     1:09:43 Establ
  inet.0: 1/1/1/0
100.2.22.2             1200        151        166       0       0     1:09:46 Establ
  inet.0: 1/1/1/0
::100.2.11.2           1000        151        160       0       0     1:09:41 Establ
  inet6.0: 1/1/1/0
::100.2.12.2           2000        152        160       0       0     1:09:45 Establ
  inet6.0: 1/1/1/0
::100.2.13.2           3000        152        159       0       0     1:09:34 Establ
  inet6.0: 1/1/1/0
::100.2.21.2           1100        150        158       0       0     1:09:17 Establ
  inet6.0: 1/1/1/0
::100.2.22.2           1200        151        165       0       0     1:09:47 Establ
  inet6.0: 1/1/1/0

[edit]
lab@MX80-NGGWR-02# run show bgp summary logical-system r3    
Groups: 7 Peers: 15 Down peers: 0
Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
inet.0               
                      35         16          0          0          0          0
inet.3               
                       8          3          0          0          0          0
inet6.0              
                      44         24          0          0          0          0
bgp.l3vpn.0          
                      16         16          0          0          0          0
bgp.l2vpn.0          
                       0          0          0          0          0          0
Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
10.200.1.1       4012345678        157        162       0       0     1:10:05 Establ
  bgp.l3vpn.0: 5/5/5/0
10.200.1.2       4012345678        151        152       0       0     1:09:34 Establ
  bgp.l2vpn.0: 0/0/0/0
10.200.1.4       4012345678        160        160       0       0     1:09:56 Establ
  bgp.l3vpn.0: 6/6/6/0
10.200.1.5       4012345678        194        161       0       0     1:10:01 Establ
  inet.0: 12/17/16/0
  inet.3: 0/4/4/0
  inet6.0: 18/20/20/0
10.200.1.6       4012345678        205        160       0       0     1:09:59 Establ
  inet.0: 1/15/14/0
  inet.3: 3/4/4/0
  inet6.0: 2/20/20/0
10.200.1.7       4012345678        156        166       0       0     1:10:03 Establ
  bgp.l3vpn.0: 0/0/0/0
10.200.1.8       4012345678        157        163       0       0     1:10:00 Establ
  bgp.l3vpn.0: 5/5/5/0
100.3.11.2             1000        152        162       0       0     1:10:04 Establ
  inet.0: 1/1/1/0
100.3.12.2             2000        152        162       0       0     1:10:05 Establ
  inet.0: 1/1/1/0
100.3.21.2             1100        152        170       0       0     1:10:04 Establ
  inet.0: 1/1/1/0
100.3.22.2             1200        151        168       0       0     1:10:01 Establ
  inet.0: 0/0/0/0
::100.3.11.2           1000        151        163       0       0     1:09:53 Establ
  inet6.0: 1/1/1/0
::100.3.12.2           2000        151        160       0       0     1:09:53 Establ
  inet6.0: 1/1/1/0
::100.3.21.2           1100        151        167       0       0     1:09:53 Establ
  inet6.0: 1/1/1/0
::100.3.22.2           1200        152        159       0       0     1:09:44 Establ
  inet6.0: 1/1/1/0

[edit]
lab@MX80-NGGWR-02# run show bgp summary logical-system r5    
Groups: 4 Peers: 11 Down peers: 0
Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
inet.0               
                      29         15          0          0          0          0
inet.3               
                       0          0          0          0          0          0
inet6.0              
                      44         23          0          0          0          0
Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
10.200.1.1       4012345678        161        196       0       0     1:10:09 Establ
  inet.0: 4/4/4/0
  inet.3: 0/0/0/0
  inet6.0: 4/4/4/0
10.200.1.2       4012345678        165        190       0       0     1:10:08 Establ
  inet.0: 5/5/5/0
  inet.3: 0/0/0/0
  inet6.0: 6/6/6/0
10.200.1.3       4012345678        162        192       0       0     1:10:04 Establ
  inet.0: 3/3/3/0
  inet.3: 0/0/0/0
  inet6.0: 5/5/5/0
10.200.1.4       4012345678        158        194       0       0     1:10:00 Establ
  inet.0: 0/0/0/0
  inet6.0: 2/2/2/0
10.200.1.6       4012345678        189        193       0       0     1:10:06 Establ
  inet.0: 0/14/14/0
  inet.3: 0/0/0/0
  inet6.0: 1/22/22/0
10.200.1.7       4012345678        160        197       0       0     1:09:56 Establ
  inet.0: 1/1/1/0
  inet.3: 0/0/0/0
  inet6.0: 2/2/2/0
10.200.1.8       4012345678        158        199       0       0     1:10:03 Establ
  inet.0: 0/0/0/0
  inet.3: 0/0/0/0
  inet6.0: 1/1/1/0
100.5.12.2             2000        153        160       0       0     1:10:04 Establ
  inet.0: 1/1/1/0
100.5.13.2             3000        152        163       0       0     1:10:04 Establ
  inet.0: 1/1/1/0
::100.5.12.2           2000        151        160       0       0     1:09:48 Establ
  inet6.0: 1/1/1/0
::100.5.13.2           3000        151        163       0       0     1:09:54 Establ
  inet6.0: 1/1/1/0

[edit]
lab@MX80-NGGWR-02# run show bgp summary logical-system r6    
Groups: 2 Peers: 7 Down peers: 0
Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
inet.0               
                      29         13          0          0          0          0
inet.3               
                       0          0          0          0          0          0
inet6.0              
                      44         23          0          0          0          0
Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
10.200.1.1       4012345678        159        192       0       0     1:09:41 Establ
  inet.0: 4/4/4/0
  inet.3: 0/0/0/0
  inet6.0: 4/4/4/0
10.200.1.2       4012345678        164        201       0       0     1:10:09 Establ
  inet.0: 5/5/5/0
  inet.3: 0/0/0/0
  inet6.0: 6/6/6/0
10.200.1.3       4012345678        161        204       0       0     1:10:05 Establ
  inet.0: 3/3/3/0
  inet.3: 0/0/0/0
  inet6.0: 5/5/5/0
10.200.1.4       4012345678        156        201       0       0     1:10:01 Establ
  inet.0: 0/0/0/0
  inet6.0: 2/2/2/0
10.200.1.5       4012345678        195        188       0       0     1:10:09 Establ
  inet.0: 0/16/16/0
  inet.3: 0/0/0/0
  inet6.0: 3/24/24/0
10.200.1.7       4012345678        158        205       0       0     1:09:53 Establ
  inet.0: 1/1/1/0
  inet.3: 0/0/0/0
  inet6.0: 2/2/2/0
10.200.1.8       4012345678        157        208       0       0     1:10:02 Establ
  inet.0: 0/0/0/0
  inet.3: 0/0/0/0
  inet6.0: 1/1/1/0
</code></pre>
<h3 id="tip-policy-internalexteral-vs-route-type-internalexternal">TIP: policy "internal/exteral" vs. "route-type internal/external"</h3>
<p><a href="http://www.juniper.net/techpubs/en_US/junos/topics/usage-guidelines/policy-configuring-match-conditions-in-routing-policy-terms.html">http://www.juniper.net/techpubs/en_US/junos/topics/usage-guidelines/policy-configuring-match-conditions-in-routing-policy-terms.html</a></p>
<pre><code>external [ type metric-type ]   
Standard        
(OSPF and IS-IS only) Match IGP external routes. For IS-IS routes, the external
condition also matches routes that are exported from one IS-IS level to
another. The type keyword is optional and is applicable only to OSPF external
routes. When you do not specify type, the external condition matches all IGP
external (OSPF and IS-IS) routes. When you specify type, the external condition
matches only OSPF external routes with the specified OSPF metric type. The
metric type can either be 1 or 2.
</code></pre>
<p>To match BGP external routes, use the route-type match condition.</p>
<pre><code>route-type value        
Standard        
Type of BGP route. The value can be one of the following:
external—External route.
internal—Internal route.
</code></pre>
<p>To match IGP external routes, use the external match condition.</p>
<h3 id="configas-migration">config:AS migration</h3>
<blockquote>
<p>r1-r8 use AS 4012345678, but appears 65513 to C3, hide 65513 to the core</p>
</blockquote>
<pre><code>set logical-systems r1 protocols bgp group to-c3 neighbor 100.1.33.2 local-as 65513
set logical-systems r1 protocols bgp group to-c3 neighbor 100.1.33.2 local-as private
</code></pre>
<p>initial config is all 65513 in core, need to change to 4012345678 in all R</p>
<h3 id="verify-as-migrationhide">verify: AS migration/hide</h3>
<p>with <code>local-as private</code></p>
<pre><code>[edit]
lab@MX80-NGGWR-02# show | compare  
[edit logical-systems r1 protocols bgp group to-c3 neighbor 100.1.33.2 local-as]
-       private;
</code></pre>
<p>simplest way to verify:</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp 10.200.1.5 logical-system r1

inet.0: 49 destinations, 67 routes (46 active, 0 holddown, 3 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* 3.3.3.0/24              Self                         100        65513 300 I
* 20.20.0.0/16            Self                         100        I
* 33.33.0.0/16            Self                         100        65513 300 I
* 33.33.33.33/32          Self                         100        65513 300 I

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* ::3.3.3.0/120           Self                         100        65513 300 I
* ::33.33.33.33/128       Self                         100        65513 300 I
  2011:310:1020::1/128
*                         Self                         100        I
* 3333:3333:3333::/48     Self                         100        65513 300 I
</code></pre>
<p>use <code>detail | match</code>:</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp 10.200.1.5 logical-system r1 detail | match 65513    
     AS path: 65513 300 I
     Communities: 65412:100 65513:100 target:4012345678L:2000
     AS path: 65513 300 I
     Communities: 65412:100 65513:100 target:4012345678L:2000
     AS path: 65513 300 I
     Communities: 65412:100 65513:100 target:4012345678L:2000
     AS path: 65513 300 I
     Communities: 65412:100 65513:100 target:4012345678L:2000
     AS path: 65513 300 I
     Communities: 65412:100 65513:100 target:4012345678L:2000
     AS path: 65513 300 I
     Communities: 65412:100 65513:100 target:4012345678L:2000
</code></pre>
<p>use as-path regex:</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp 10.200.1.5 logical-system r1 aspath-regex ".* 65513 .*"

inet.0: 49 destinations, 67 routes (46 active, 0 holddown, 3 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* 3.3.3.0/24              Self                         100        65513 300 I
* 33.33.0.0/16            Self                         100        65513 300 I
* 33.33.33.33/32          Self                         100        65513 300 I

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* ::3.3.3.0/120           Self                         100        65513 300 I
* ::33.33.33.33/128       Self                         100        65513 300 I
* 3333:3333:3333::/48     Self                         100        65513 300 I
</code></pre>
<p>with <code>local-as private</code>:</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp 10.200.1.5 logical-system r1

inet.0: 49 destinations, 67 routes (46 active, 0 holddown, 3 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* 3.3.3.0/24              Self                         100        300 I
* 20.20.0.0/16            Self                         100        I
* 33.33.0.0/16            Self                         100        300 I
* 33.33.33.33/32          Self                         100        300 I

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* ::3.3.3.0/120           Self                         100        300 I
* ::33.33.33.33/128       Self                         100        300 I
  2011:310:1020::1/128
*                         Self                         100        I
* 3333:3333:3333::/48     Self                         100        300 I

[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp 10.200.1.5 logical-system r1 aspath-regex ".* 65513 .*"

inet.0: 49 destinations, 67 routes (46 active, 0 holddown, 3 hidden)
Restart Complete

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete

[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp 10.200.1.5 logical-system r1 detail | match 65513          
     Communities: 65412:100 65513:100 target:4012345678L:2000
     Communities: 65412:100 65513:100 target:4012345678L:2000
     Communities: 65412:100 65513:100 target:4012345678L:2000
     Communities: 65412:100 65513:100 target:4012345678L:2000
     Communities: 65412:100 65513:100 target:4012345678L:2000
     Communities: 65412:100 65513:100 target:4012345678L:2000
</code></pre>
<h3 id="configipv4-ipv6-rr-r5r6">config:IPv4 IPv6 RR: R5/R6</h3>
<pre><code>set logical-systems r1 protocols bgp group to-v4v6-rr type internal
set logical-systems r1 protocols bgp group to-v4v6-rr local-address 10.200.1.1
set logical-systems r1 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r1 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r1 protocols bgp group to-v4v6-rr neighbor 10.200.1.6
set logical-systems r1 protocols bgp group to-v4v6-rr family inet6

set logical-systems r2 protocols bgp group to-v4v6-rr type internal
set logical-systems r2 protocols bgp group to-v4v6-rr local-address 10.200.1.2
set logical-systems r2 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r2 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r2 protocols bgp group to-v4v6-rr neighbor 10.200.1.6
set logical-systems r2 protocols bgp group to-v4v6-rr family inet6

set logical-systems r3 protocols bgp group to-v4v6-rr type internal
set logical-systems r3 protocols bgp group to-v4v6-rr local-address 10.200.1.3
set logical-systems r3 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r3 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r3 protocols bgp group to-v4v6-rr neighbor 10.200.1.6
set logical-systems r3 protocols bgp group to-v4v6-rr family inet6

set logical-systems r4 protocols bgp group to-v4v6-rr type internal
set logical-systems r4 protocols bgp group to-v4v6-rr local-address 10.200.1.4
set logical-systems r4 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r4 protocols bgp group to-v4v6-rr neighbor 10.200.1.6
set logical-systems r4 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r4 protocols bgp group to-v4v6-rr family inet6

set logical-systems r7 protocols bgp group to-v4v6-rr type internal
set logical-systems r7 protocols bgp group to-v4v6-rr local-address 10.200.1.7
set logical-systems r7 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r7 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r7 protocols bgp group to-v4v6-rr neighbor 10.200.1.6
set logical-systems r7 protocols bgp group to-v4v6-rr family inet6

set logical-systems r8 protocols bgp group to-v4v6-rr type internal
set logical-systems r8 protocols bgp group to-v4v6-rr local-address 10.200.1.8
set logical-systems r8 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r8 protocols bgp group to-v4v6-rr neighbor 10.200.1.5
set logical-systems r8 protocols bgp group to-v4v6-rr neighbor 10.200.1.6
set logical-systems r8 protocols bgp group to-v4v6-rr family inet6

set logical-systems r5 protocols bgp group v4v6-rr type internal
set logical-systems r5 protocols bgp group v4v6-rr local-address 10.200.1.5
set logical-systems r5 protocols bgp group v4v6-rr family inet unicast
set logical-systems r5 protocols bgp group v4v6-rr cluster 5.5.5.5  #&lt;------
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.1
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.2
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.3
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.4
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.7
set logical-systems r5 protocols bgp group v4v6-rr neighbor 10.200.1.8
set logical-systems r5 protocols bgp group to-v4v6-rr family inet6

set logical-systems r6 protocols bgp group v4v6-rr type internal
set logical-systems r6 protocols bgp group v4v6-rr local-address 10.200.1.6
set logical-systems r6 protocols bgp group v4v6-rr family inet unicast
set logical-systems r6 protocols bgp group v4v6-rr cluster 6.6.6.6  #&lt;------
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.1
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.2
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.3
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.4
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.8
set logical-systems r6 protocols bgp group v4v6-rr neighbor 10.200.1.7
set logical-systems r6 protocols bgp group to-v4v6-rr family inet6
</code></pre>
<h3 id="config-troubleshooting-pre-config">config: troubleshooting pre-config</h3>
<pre><code>#correct NHS policy in all R
set logical-systems r1 policy-options policy-statement exp-bgp-nhs term 1 from protocol bgp
set logical-systems r1 policy-options policy-statement exp-bgp-nhs term 1 from route-type external  #&lt;------(not `external`)
set logical-systems r1 policy-options policy-statement exp-bgp-nhs term 1 then next-hop self

#delete existing `reject` group
delete logical-systems r2 apply-groups reject
delete logical-systems r3 apply-groups reject
</code></pre>
<h3 id="config-1-all-cpt-facing-r-import-tag-routes">config 1: all C/P/T facing R: import : tag routes</h3>
<pre><code>set logical-systems r1 policy-options policy-statement imp-bgp-tag-c term 1 from protocol bgp
set logical-systems r1 policy-options policy-statement imp-bgp-tag-c term 1 then community add c-route
set logical-systems r1 policy-options community c-route members 65513:100
set logical-systems r1 policy-options community p-route members 65513:200
set logical-systems r1 policy-options community t-route members 65513:300

set logical-systems r2 policy-options policy-statement imp-bgp-tag-p term 1 from protocol bgp
set logical-systems r2 policy-options policy-statement imp-bgp-tag-p term 1 then community add p-route
set logical-systems r2 policy-options policy-statement imp-bgp-tag-t term 1 from protocol bgp
set logical-systems r2 policy-options policy-statement imp-bgp-tag-t term 1 then community add t-route
set logical-systems r2 policy-options community c-route members 65513:100
set logical-systems r2 policy-options community p-route members 65513:200
set logical-systems r2 policy-options community t-route members 65513:300

set logical-systems r3 policy-options policy-statement imp-bgp-tag-p term 1 from protocol bgp
set logical-systems r3 policy-options policy-statement imp-bgp-tag-p term 1 then community add p-route
set logical-systems r3 policy-options policy-statement imp-bgp-tag-t term 1 from protocol bgp
set logical-systems r3 policy-options policy-statement imp-bgp-tag-t term 1 then community add t-route
set logical-systems r3 policy-options community c-route members 65513:100
set logical-systems r3 policy-options community p-route members 65513:200
set logical-systems r3 policy-options community t-route members 65513:300

set logical-systems r4 policy-options policy-statement imp-bgp-tag-c term 1 from protocol bgp
set logical-systems r4 policy-options policy-statement imp-bgp-tag-c term 1 then community add c-route
set logical-systems r4 policy-options community c-route members 65513:100
set logical-systems r4 policy-options community p-route members 65513:200
set logical-systems r4 policy-options community t-route members 65513:300

set logical-systems r5 policy-options policy-statement imp-bgp-tag-p term 1 from protocol bgp
set logical-systems r5 policy-options policy-statement imp-bgp-tag-p term 1 then community add p-route
set logical-systems r5 policy-options community c-route members 65513:100
set logical-systems r5 policy-options community p-route members 65513:200
set logical-systems r5 policy-options community t-route members 65513:300

set logical-systems r7 policy-options policy-statement imp-bgp-tag-c term 1 from protocol bgp
set logical-systems r7 policy-options policy-statement imp-bgp-tag-c term 1 then community add c-route
set logical-systems r7 policy-options community c-route members 65513:100
set logical-systems r7 policy-options community p-route members 65513:200
set logical-systems r7 policy-options community t-route members 65513:300

set logical-systems r1 protocols bgp group to-c3 import imp-bgp-tag-c
set logical-systems r2 protocols bgp group to-p import imp-bgp-tag-p
set logical-systems r2 protocols bgp group to-t import imp-bgp-tag-t
set logical-systems r3 protocols bgp group to-p import imp-bgp-tag-p
set logical-systems r3 protocols bgp group to-t import imp-bgp-tag-t
set logical-systems r4 protocols bgp group to-c5 import imp-bgp-tag-c
set logical-systems r5 protocols bgp group to-p import imp-bgp-tag-p
set logical-systems r7 protocols bgp group to-c4 import imp-bgp-tag-c
</code></pre>
<h3 id="verify-route-tagging">verify: route tagging</h3>
<pre><code>#tag C route
lab@MX80-NGGWR-02# run show route protocol bgp logical-system r1 3.3.3/24 extensive | match comm  
    Communities: 65412:100 65513:100 target:4012345678L:2000
    Communities: 65412:100 65513:100 target:4012345678L:2000
                Communities: 65412:100 65513:100 target:4012345678L:2000

#tag P route
lab@MX80-NGGWR-02# run show route protocol bgp logical-system r2 211.1/16 extensive | match comm        
    Communities: 65513:200
    Communities: 65513:200
                Communities: 65513:200

#tag T route
lab@MX80-NGGWR-02# run show route protocol bgp logical-system r2 222.1/16 extensive | match comm 
    Communities: 65513:300
    Communities: 65513:300
                Communities: 65513:300
</code></pre>
<h3 id="config-2-all-pt-facing-r-export-reject-pt-routes">config 2: all P/T facing R: export: reject P(T) routes</h3>
<pre><code>set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 1 from protocol bgp
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 1 from community t-route
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 1 then reject

set logical-systems r2 policy-options policy-statement exp-bgp-t-out term 1 from protocol bgp
set logical-systems r2 policy-options policy-statement exp-bgp-t-out term 1 from community p-route
set logical-systems r2 policy-options policy-statement exp-bgp-t-out term 1 then reject

set logical-systems r3 policy-options policy-statement exp-bgp-p-out term 1 from protocol bgp
set logical-systems r3 policy-options policy-statement exp-bgp-p-out term 1 from community t-route
set logical-systems r3 policy-options policy-statement exp-bgp-p-out term 1 then reject

set logical-systems r3 policy-options policy-statement exp-bgp-t-out term 1 from protocol bgp
set logical-systems r3 policy-options policy-statement exp-bgp-t-out term 1 from community p-route
set logical-systems r3 policy-options policy-statement exp-bgp-t-out term 1 then reject

set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 1 from protocol bgp
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 1 from community t-route
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 1 then reject
</code></pre>
<h3 id="verify-route-rejection">verify: route rejection</h3>
<p>R1 -&gt; C3:</p>
<pre><code>lab@MX80-NGGWR-02# run show route advertising-protocol bgp 100.1.33.2 logical-system r1

inet.0: 45 destinations, 63 routes (43 active, 0 holddown, 2 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* 3.3.3.0/24              100.1.33.2                              4012345678 300 I
* 10.200.0.0/16           Self                                    4012345678 I      #&lt;------aggr. internal
* 20.20.0.0/16            Self                                    I
* 33.33.0.0/16            100.1.33.2                              4012345678 300 I
* 33.33.33.33/32          100.1.33.2                              4012345678 300 I
* 44.44.0.0/16            Self                                    4012345678 400 I  #&lt;------C4 routes
* 211.1.0.0/16            Self                                    4012345678 1000 I #&lt;------all P routes
* 211.2.0.0/16            Self                                    4012345678 2000 I
* 211.3.0.0/16            Self                                    4012345678 3000 I
* 211.4.0.0/16            Self                                    4012345678 1000 I
* 211.5.0.0/16            Self                                    4012345678 2000 I
* 211.6.0.0/16            Self                                    4012345678 2000 I
* 211.7.0.0/16            Self                                    4012345678 3000 I
* 222.1.0.0/16            Self                                    4012345678 1100 I #&lt;------all T routes
* 222.2.0.0/16            Self                                    4012345678 1200 I
* 222.3.0.0/16            Self                                    4012345678 1100 I

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* ::3.3.3.0/120           ::100.1.33.1                            4012345678 300 I
* ::33.33.33.33/128       ::100.1.33.1                            4012345678 300 I
* 2000:1000::/32          ::100.1.33.1                            4012345678 1000 I         #&lt;------P routes
* 2000:2000::/32          ::100.1.33.1                            4012345678 2000 I
* 2000:3000::/32          ::100.1.33.1                            4012345678 3000 I
* 2000:4000::/32          ::100.1.33.1                            4012345678 1000 I
* 2000:5000::/32          ::100.1.33.1                            4012345678 2000 I
* 2000:6000::/32          ::100.1.33.1                            4012345678 2000 I
* 2000:7000::/32          ::100.1.33.1                            4012345678 3000 I
* 2011:310::/32           ::100.1.33.1                            4012345678 I      #&lt;------core IPv6 aggr
  2011:310:1020::2/128                                                              #&lt;------core IPv6 lo0
*                         ::100.1.33.1                            4012345678 I
  2011:310:1020::3/128
*                         ::100.1.33.1                            4012345678 I
  2011:310:1020::4/128
*                         ::100.1.33.1                            4012345678 I
  2011:310:1020::5/128
*                         ::100.1.33.1                            4012345678 I
  2011:310:1020::6/128
*                         ::100.1.33.1                            4012345678 I
  2011:310:1020::7/128
*                         ::100.1.33.1                            4012345678 I
  2011:310:1020::8/128
*                         ::100.1.33.1                            4012345678 I
* 3000:1000::/32          ::100.1.33.1                            4012345678 1100 I #&lt;------T route
* 3000:2000::/32          ::100.1.33.1                            4012345678 1200 I
* 3000:3000::/32          ::100.1.33.1                            4012345678 1100 I
* 3000:4000::/32          ::100.1.33.1                            4012345678 1200 I
* 3333:3333:3333::/48     ::100.1.33.1                            4012345678 300 I  #&lt;------C routes
* 4444:4444:4444::/48     ::100.1.33.1                            4012345678 400 I
* 5555:5555:5555::/48     ::100.1.33.1                            4012345678 500 I
</code></pre>
<p>R2 -&gt; P1: V4</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp 100.2.11.2 logical-system r2

inet.0: 72 destinations, 90 routes (71 active, 0 holddown, 3 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* 10.200.0.0/16           Self                                    I         #&lt;------aggr
* 20.20.0.0/16            Self                                    I         #&lt;------aggr
* 33.33.0.0/16            Self                                    300 I     #&lt;------C3
* 44.44.0.0/16            Self                                    400 I     #&lt;------C4
* 211.2.0.0/16            Self                                    2000 I    #&lt;------all P
* 211.3.0.0/16            Self                                    3000 I
* 211.5.0.0/16            Self                                    2000 I
* 211.6.0.0/16            Self                                    2000 I
* 211.7.0.0/16            Self                                    3000 I
</code></pre>
<p>R2 -&gt; P1: V6</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp ::100.2.11.2 logical-system r2

inet6.0: 48 destinations, 77 routes (48 active, 0 holddown, 0 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* 2000:2000::/32          Self                                    2000 I    #&lt;------all P V6 routes
* 2000:3000::/32          Self                                    3000 I
* 2000:5000::/32          Self                                    2000 I
* 2000:6000::/32          Self                                    2000 I
* 2000:7000::/32          Self                                    3000 I
* 2011:310::/32           Self                                    I         #&lt;------V6 aggr
* 3333:3333:3333::/48     Self                                    300 I     #&lt;------all C V6 routes
* 4444:4444:4444::/48     Self                                    400 I
* 5555:5555:5555::/48     Self                                    500 I
</code></pre>
<h3 id="tip-6pe">TIP: 6PE</h3>
<ul>
<li>like MPLS/VPN. but no vrf, </li>
<li>bgp assign either reserved label 2(ipv6 explicit) or any lable as inner
  label(like vpn label).</li>
<li>running on top of LSP (ldp or rsvp based)   <br />
</li>
<li>Juniper PE core facing i/f <code>must</code> enable ipv6 =&gt; troubleshooting tip.
  (seems only if use label 2). otherwise forwarding will have issue.</li>
</ul>
<h4 id="6pe-all-4-solutions">6PE all 4 solutions</h4>
<p>the issue: 
    no consistent LDP/RSVP (R2/3 run RSVP vs. R7/8 run LDP)     =&gt; 
    R2/3 , R7/8 are missing each other in inet.3                =&gt;
    R2/3 , R7/8 are missing each other in inet6.3               =&gt;
    R2/3 &lt;--&gt; R7/8 can't resolve each other as BGP NH           =&gt;
    R2/3 , R7/8: routes learned from each other show as hidden</p>
<p>the solutions:</p>
<ol>
<li>RSVP install R7/8 @ R2/3 + 
   LDP adv host @ R5/6 for R7/8(no RSVP)</li>
<li>change NH @ RR(R5/6): because both R1/2 and R7/8 can resolve RR as NH</li>
<li>mix 1/2</li>
<li>RRs (R5/6) BGP: adv R2/3/7/8 , so all R has each other's lo0 in BGP
   all Rs(R2/3/5/6/7/8) BGP: 
       inet labeld-unicast rib inet.3 =&gt; put learned labeled lo0 into inet.3
   R2/3,R7/8 BGP:
       inet labeld-unicast rib-group 6pe =&gt; copy inet.3 into inet6.3</li>
</ol>
<p>notes:
R8 is not involved here (no C/P/T router attached, only for MPLS/VPN)</p>
<h4 id="routing">routing:</h4>
<ul>
<li>CE2 adv IPv6 routes to PE2, via IPv6 protocols (BGP, ISIS, OSPFv3, RIPng, etc)</li>
<li>PE2 get CE2 IPv6 routes, with NH as CE2 IPv6 address</li>
<li><code>family inet6 labeled-unicast</code> =&gt; </li>
<li>PE2 adv labeled(<code>explicit-null</code> =&gt; label 2) IPv6 routes to PE1, via MP-BGP</li>
<li><code>protocol mpls ipv6-tunneling</code> =&gt; </li>
<li>PE1 check inet3.0 (table of map: IPv4 &lt;=&gt; LSP )</li>
<li>PE1 convert all IPv4 in inet.3 to IPv6, in a form of "IPv4 mapped IPv6 address"</li>
<li>PE1 put all IPv4-m-IPv6 into inet6.3 (a table of map: IPv6 &lt;=&gt; LSP)</li>
<li>
<p>PE1 BGP now can: </p>
<pre><code>              (auto-convert based on IPv4 NH)
    resolve IPv6 routes ===&gt; NH IPv4-m-IPv6
                    (inet6.3)
    resolve IPv4-m-IPv6 ===&gt; LSP
</code></pre>
</li>
<li>
<p>PE1 adv IPv6 routes to CE1, NH to PE1 IPv6</p>
<pre><code>                      &lt; ----MPLS---------&gt; 
    CE1-----------PE1==========/P/==========PE2-------------CE2
 (pure IPv6)   (dual)                       (dual)                (dual stack)

                                                        (routing:)
                                              &lt;===IPv6 protocol=
                    &lt;==MP-BGP:labeled IPv6===
    &lt;==IPv6 protocol=

    (forwarding:)
    ===IPv6 packet=&gt;
                    =&gt;IPv6/IL:2/OL (PHP)
                                ==IPv6/IL:2=&gt;               
                                              ===&gt;IPv6 packet=&gt;
</code></pre>
</li>
</ul>
<h4 id="in-lab">in lab</h4>
<pre><code>                          &lt; ----MPLS---------&gt; 
        CE1-----------PE2==========/P/==========PE8-------------CE2
        CE1-----------R1===========R3===========R5==========R7--------------CE2
     (pure IPv6)   (dual)                       (dual)      |         (dual stack)
                      |                                     |                  |
                      |                                     | (routing:)       |
                      |                                     | &lt;===IPv6 protocol|
                      |                                     |   NH:v4-m-v6 CE2 i/f (need 'accept-remote-nexthop`)           a)
                      |                                     |   NH:v4-c-v6 CE2 i/f (need imp: change NH)
                      |                                     |
                      |               &lt;==MP-BGP:labeled IPv6|
                      |                 1. NH:v4-m-v6 PE2 lo0, 
                      |                 2. NH resolve: need inet6.3 (v4-m-v6 lo0 -&gt; LSP)
                      |                   PE1 learn PE2 (labeled)v4 lo0 via :
                      |                     1) LDP/RSVP (R1) -&gt; generate inet.3 (v4 lo0 -&gt; LSP)
                      |                        `mpls ipv6-tunneling` -&gt; generate inet.6 from inet.3
                      |                     2) BGP `inet labeled-unicast rib inet.3` (R2/3/7/8) -&gt; generate inet.3
                      |                        `inet labeled-unicast rib-group` -&gt; generate inet.3 -&gt; inet.6
                      | 
      &lt;==IPv6 protocol|
      NH:v4-m-v6 CE2 i/f ('accept-remote-nexthop`)
      NH:v4-c-v6 CE2 i/f (imp: change NH)

      (forwarding:)
      ===IPv6 packet=&gt;
                      =&gt;IPv6/IL:2/L:LDP/OL:RSVP 
                                  (PHP RSVP)
                                  ==IPv6/IL:2:=&gt;               
                                                ===&gt;IPv6 packet=&gt;
</code></pre>
<h4 id="pe-to-ce">PE to CE</h4>
<p>lab中：
1. 只允许使用IPv4 BGP session
2. PE CE都使用了IPv4-c-IPv6 地址，不允许更改（为IPv4-m-IPv6)</p>
<p>因为1, 所以只能用V4的BGP session,配置family inet6 传递V6 路由信息
但（V6规范或者JUNOS规则要求），V6路由信息只能用以下V6 地址做NH:
<em> 明确配置的远端V6 lo0
</em> 系统根据V4 lo0 生成的IPv4-m-IPv6 地址</p>
<p>根据（JUNOS) EBGP规则，从single-hop的EBGP
session收到的路由的NH,必须跟本地地址共享一个网段，否则丢弃路由信息。
"the default behavior is for any next-hop address received from a single-hop
EBGP peer that is not recognized as sharing a common subnet to be discarded."
但目前是V4 session, V6路由信息的NH经自动转换也只能是V6形式(V4-m-V6), 所以会丢弃。
解决方法是配置“accept-remote-nexthop”</p>
<p>现在路由是显现了，但缺省规则也只是以V4-m-V6做NH,但lab中本地配置的是V4-c-V6,因此需要改变NH</p>
<h4 id="pe-to-pe">PE to PE</h4>
<ol>
<li>PE之间建立bgp IPv4 session, 彼此双方PE的inet6
   路由(此处称为6PE路由，相对于MPLSVPN中的vpn路由)以labeled inet6 NLRI形式传递,
   (使用explicit-null 则用 label 2 -- 这是junos 6PE “标准”label);
   决定这个的配置是<code>family inet6 labeled-unicast explicit-null</code></li>
<li>因为有了可携带inet6 NLRI的BGP session,中间怎么乱都没所谓，路由信息都可以通过去</li>
<li>
<p>因为是inet6 的NLRI ，所以NH就自动使用v4-m-v6 (疑为IPv6规范)</p>
<pre><code>Source: 10.200.1.5
Protocol next hop: ::ffff:10.200.1.7
</code></pre>
</li>
<li>
<p>现在需要resolved 这个形式为v4-m-v6 的NH(解析为LSP),
   JUNOS的实现规则，需要查找inet6.3</p>
</li>
<li>一切复杂性开始了，都是关于如何生成inet6.3. lab中有两个场景。</li>
</ol>
<h4 id="1">场景1:</h4>
<ol>
<li>R1有点特殊。它恰好已从RSVP(R2/3/4), 和LDPoRSVP(R5/6/7/8)学到了所有的IPv4 lo0.</li>
<li>junos缺省规则：为ldp/rsvp路由缺省生成inet.3</li>
<li>R1的配置"mpls ipv6-tunnel", 使得inet.6 可以根据inet.3做自动转换而生成，
   “转换”基本就是把prefix 从IPv4 换为v4-m-v6</li>
<li>R1 问题解决了。</li>
</ol>
<h4 id="2">场景2:</h4>
<ol>
<li>复杂问题在于R2/3/7/8. 因为R5/6分割了ldp/rsvp的连通性。所以R2/3
   和R7/8之间互相通过LDP或者RSVP学到对方的IPv4 lo0, 也就是说，inet.3中缺这些东西</li>
<li>解决的方法，按照solution 4, 就用连贯的bgp 取代不连贯的ldp/rsvp，
   充当一个新的label 分配协议。也就是<code>inet labeled-unicast</code>;</li>
<li>但如果不配置<code>rib inet.3</code>的话， 这个新的inet labeled-unicast和原来的inet
   unicast, 因为承担了相同的prefix,
   所以在路由信息放置在哪个表里的时候，冲突了。因此配置不允许并存，只能选择其一。
   就是说如果用labled-unicast，则需要把unicast 删掉，而labeled
   prefix则依然放在inet.0中，不会因为BGP充当了“LDP” 就放在inet.3
   中，这是JUNOS bgp的缺省行为</li>
<li>解决方法是使用<code>rib inet.3</code>配置，<code>inet labeled-unicast rib inet.3</code>， 这个配置
   干了两个事情: 
   现在inet labeled unicast不与inet unicast冲突: 
   inet.0没有影响
   RR上通告的labeled-unicast 的v4 lo0 则另外放在inet.3，这样就有了v4 NH 的inet.3</li>
<li>此时细看r1的inet.3， 必定既有ldp/rsvp的，也有bgp来的；
   但根据preference，选择ldp/rsvp的。只有新生成的r7/8的lo0
   用了bgp的。这些细节都不重要了。</li>
<li>只是这时候仍然没有inet.6， 但根据前面的原则， ipv6的NLRI硬性要求ipv4-m-v6
   为NH，要解析的也是v6 NH. 也就是说必须要有inet.6， 但JUNOS规则，“mpls
   ipv6-tunneling” ， 不会对BGP生成的inet.3 生成inet6.3 ， 因此手工用rib-group
   生成。</li>
</ol>
<h4 id="">规范规则</h4>
<p>这个过程中涉及到不少潜在的规则或者规范，（也是考试设置的环境特意要考察的知识点）：
1. <code>family inet6 labeled-unicast explicit-null</code> =&gt; 为6PE路由分配“VPN” label 2
1. inet6的BGP prefix，要求NH必须为V6, 因此系统自动根据IPv4 lo0生成IPv4-m-IPv6 作为NH
1. LDP/RSVP学习到的lo0 自动放置在inet.3 ，BGP不会。除非配置<code>inet labeled-unicast rib inet.3</code>
1. <code>mpls ipv6-tunnel</code>为LDP/RSVP的inet.3生成inet6.3, 不会为BGP的inet.3生成。使用rib-group 手工解决</p>
<h3 id="config6pepe-ce">config:6PE:PE-CE</h3>
<p>R1:</p>
<pre><code>#`accept-remote-nexthop`, otherwise not accept
set logical-systems r1 protocols bgp group to-c3 accept-remote-nexthop
set logical-systems r1 protocols bgp group to-c3 family inet unicast
set logical-systems r1 protocols bgp group to-c3 family inet6 unicast
set logical-systems r1 protocols bgp group to-c3 import imp-bgp-fix-nh
set logical-systems r1 protocols bgp group to-c3 export exp-bgp-fix-nh

#change NH of received C routes ,from (system default generated) IPv4-mapped-IPv6 addr
#  to IPv4-compatible-IPv6, otherwise appears in local table as `hidden`
set logical-systems r1 policy-options policy-statement imp-bgp-fix-nh term 1 from protocol bgp
set logical-systems r1 policy-options policy-statement imp-bgp-fix-nh term 1 from route-filter ::0/0 prefix-length-range /0-/128    #&lt;------just for IPv6
set logical-systems r1 policy-options policy-statement imp-bgp-fix-nh term 1 then next-hop ::100.1.33.2

#change NH of advertised routes, from (system default generated) IPv4-mapped-IPv6 addr
#  to IPv4-compatible-IPv6, otherwise appears as `hidden` in C router
set logical-systems r1 policy-options policy-statement exp-bgp-fix-nh term 1 from protocol bgp
set logical-systems r1 policy-options policy-statement exp-bgp-fix-nh term 1 from route-filter ::/0 prefix-length-range /0-/128     #&lt;------just for IPv6
set logical-systems r1 policy-options policy-statement exp-bgp-fix-nh term 1 then next-hop ::100.1.33.1
</code></pre>
<p>R7:</p>
<pre><code>set logical-systems r7 protocols bgp group to-c4 accept-remote-nexthop
set logical-systems r7 protocols bgp group to-c4 family inet unicast
set logical-systems r7 protocols bgp group to-c4 family inet6 unicast
set logical-systems r7 protocols bgp group to-c4 import imp-bgp-fix-nh
set logical-systems r7 protocols bgp group to-c4 export exp-bgp-fix-nh

set logical-systems r7 policy-options policy-statement imp-bgp-fix-nh term 1 from protocol bgp
set logical-systems r7 policy-options policy-statement imp-bgp-fix-nh term 1 from route-filter ::/0 prefix-length-range /0-/128     #&lt;------just for IPv6
set logical-systems r7 policy-options policy-statement imp-bgp-fix-nh term 1 then next-hop ::100.7.34.2

set logical-systems r7 policy-options policy-statement exp-bgp-fix-nh term 1 from protocol bgp
set logical-systems r7 policy-options policy-statement exp-bgp-fix-nh term 1 from route-filter ::/0 prefix-length-range /0-/128     #&lt;------just for IPv6
set logical-systems r7 policy-options policy-statement exp-bgp-fix-nh term 1 then next-hop ::100.7.34.1
</code></pre>
<h3 id="verify-pe-ce">verify: PE-CE</h3>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route logical-system r1 table inet6.0 receive-protocol bgp 100.1.33.2

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* ::3.3.3.0/120           ::ffff:100.1.33.2                       300 I
* ::33.33.33.33/128       ::ffff:100.1.33.2                       300 I
* 3333:3333:3333::/48     ::ffff:100.1.33.2                       300 I
</code></pre>
<h4 id="without-accept-remote-nexthop-and-nh-changing-policy">without <code>accept-remote-nexthop</code> and nh changing policy</h4>
<p>not accept any route at all, not even in hidden</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route receive-protocol bgp 100.1.33.2 logical-system r1 table inet6.0

inet6.0: 29 destinations, 52 routes (29 active, 0 holddown, 0 hidden)
Restart Complete
</code></pre>
<h4 id="with-accept-remote-nexthop">with <code>accept-remote-nexthop</code></h4>
<p>accept route as <code>hidden</code>:</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# set logical-systems r1 protocols bgp group to-c3 accept-remote-nexthop

[edit]
lab@MX80-NGGWR-02# commit  
commit complete

[edit]
lab@MX80-NGGWR-02# run show route receive-protocol bgp 100.1.33.2 logical-system r1 table inet6.0 hidden

inet6.0: 32 destinations, 55 routes (29 active, 0 holddown, 3 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
  ::3.3.3.0/120           ::ffff:100.1.33.2                       300 I     #&lt;------
  ::33.33.33.33/128       ::ffff:100.1.33.2                       300 I     #&lt;------
  3333:3333:3333::/48     ::ffff:100.1.33.2                       300 I     #&lt;------
</code></pre>
<h4 id="fix-incoming-nh-with-import-policy">fix incoming NH with import policy</h4>
<p>rib-in still unchanged:</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route receive-protocol bgp 100.1.33.2 logical-system r1 table inet6.0

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* ::3.3.3.0/120           ::ffff:100.1.33.2                       300 I
                          ^^^^^^^^^^^^^^^^^
* ::33.33.33.33/128       ::ffff:100.1.33.2                       300 I
* 3333:3333:3333::/48     ::ffff:100.1.33.2                       300 I
</code></pre>
<p>routes in <code>rib</code> is changed, with new NH:</p>
<pre><code>(IPv4-mapped-IPv6)          (IPv4-compatible-IPv6)
::ffff:100.1.33.2   ==&gt;     ::100.1.33.2

[edit]
lab@MX80-NGGWR-02# run show route protocol bgp logical-system r1 table inet6.0 ::3.3.3.0/120 extensive

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete
::3.3.3.0/120 (1 entry, 1 announced)
TSI:
KRT in-kernel ::3.3.3.0/120 -&gt; {::100.1.33.2}
Page 0 idx 0 Type 1 val 26e2824
    Nexthop: ::100.1.33.2                                   #&lt;------
    AS path: 4012345678 300 I
    Communities: 65412:100 65513:100 target:4012345678L:2000
Page 0 idx 1 Type 1 val 26e262c
    Flags: Nexthop Change
    Nexthop: Self
    Localpref: 100
    AS path: [4012345678] 300 I
    Communities: 65412:100 65513:100 target:4012345678L:2000
Path ::3.3.3.0 from 100.1.33.2 Vector len 4.  Val: 0 1
        *BGP    Preference: 170/-101
                Next hop type: Router, Next hop index: 2320
                Address: 0x26e8698
                Next-hop reference count: 9
                Source: 100.1.33.2
                Next hop: ::100.1.33.2 via ge-1/2/1.133, selected
                Session Id: 0x500003
                State: &lt;Active Ext&gt;
                Local AS: 4012345678 Peer AS:   300
                Age: 8:07 
                Validation State: unverified 
                Task: BGP_300_65513.100.1.33.2+179
                Announcement bits (3): 0-KRT 3-BGP_RT_Background 4-Resolve tree 5 
                AS path: 300 I
                Communities: 65412:100 65513:100 target:4012345678L:2000
                Accepted
                Localpref: 100
                Router ID: 3.3.3.1
</code></pre>
<h3 id="config6pepe-pe">config:6PE:PE-PE</h3>
<p>R1:
    #accept all lo0 via BGP labeled route, then put into inet.3
    set logical-systems r1 protocols bgp group to-v4v6-rr family inet labeled-unicast rib inet.3
    #assign 6PE label (like vpn label)
    set logical-systems r1 protocols bgp group to-v4v6-rr family inet6 labeled-unicast explicit-null</p>
<p>R2,R3,R7,R8:</p>
<pre><code>set logical-systems r2 protocols bgp group to-v4v6-rr family inet6 labeled-unicast explicit-null
set logical-systems r2 protocols bgp group to-v4v6-rr family inet labeled-unicast rib inet.3
#"manually" copy inet.3 into inet6.3
set logical-systems r2 protocols bgp group to-v4v6-rr family inet labeled-unicast rib-group copy-inet.3-to-inet6.3

set logical-systems r3 protocols bgp group to-v4v6-rr family inet labeled-unicast rib-group copy-inet.3-to-inet6.3
set logical-systems r3 protocols bgp group to-v4v6-rr family inet labeled-unicast rib inet.3
set logical-systems r3 protocols bgp group to-v4v6-rr family inet6 labeled-unicast explicit-null

set logical-systems r7 protocols bgp group to-v4v6-rr family inet labeled-unicast rib-group copy-inet.3-to-inet6.3
set logical-systems r7 protocols bgp group to-v4v6-rr family inet labeled-unicast rib inet.3
set logical-systems r7 protocols bgp group to-v4v6-rr family inet6 labeled-unicast explicit-null

set logical-systems r8 protocols bgp group to-v4v6-rr family inet labeled-unicast rib-group copy-inet.3-to-inet6.3
set logical-systems r8 protocols bgp group to-v4v6-rr family inet labeled-unicast rib inet.3
set logical-systems r8 protocols bgp group to-v4v6-rr family inet6 labeled-unicast explicit-null
</code></pre>
<h3 id="verify-pe-pe">verify: PE-PE</h3>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route protocol bgp logical-system r1 table inet6.0

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::3.3.3.0/120      *[BGP/170] 01:24:15, localpref 100, from 100.1.33.2      #&lt;------C3 IPv6 routes
                      AS path: 300 I, validation-state: unverified
                    &gt; to ::100.1.33.2 via ge-1/2/1.133
::33.33.33.33/128  *[BGP/170] 01:24:15, localpref 100, from 100.1.33.2
                      AS path: 300 I, validation-state: unverified
                    &gt; to ::100.1.33.2 via ge-1/2/1.133
2000:1000::/32     *[BGP/170] 01:24:09, localpref 100, from 10.200.1.5      #&lt;------all P IPv6 routes
                      AS path: 1000 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
                    [BGP/170] 01:24:09, localpref 100, from 10.200.1.6
                      AS path: 1000 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
2000:2000::/32     *[BGP/170] 01:24:16, localpref 100, from 10.200.1.5
                      AS path: 2000 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
                    [BGP/170] 01:24:17, localpref 100, from 10.200.1.6
                      AS path: 2000 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
2000:3000::/32     *[BGP/170] 01:24:16, localpref 100, from 10.200.1.5
                      AS path: 3000 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
                    [BGP/170] 01:24:20, localpref 100, from 10.200.1.6
                      AS path: 3000 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
2000:4000::/32     *[BGP/170] 01:24:12, localpref 100, from 10.200.1.5
                      AS path: 1000 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
                    [BGP/170] 01:24:13, localpref 100, from 10.200.1.6
                      AS path: 1000 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
2000:5000::/32     *[BGP/170] 01:24:12, localpref 100, from 10.200.1.5
                      AS path: 2000 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
                    [BGP/170] 01:24:20, localpref 100, from 10.200.1.6
                      AS path: 2000 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
2000:6000::/32     *[BGP/170] 01:24:15, localpref 100, from 10.200.1.5
                      AS path: 2000 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
                    [BGP/170] 01:24:15, localpref 100, from 10.200.1.6
                      AS path: 2000 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
2000:7000::/32     *[BGP/170] 01:24:13, localpref 100, from 10.200.1.5
                      AS path: 3000 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
                    [BGP/170] 01:24:13, localpref 100, from 10.200.1.6
                      AS path: 3000 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
2011:310::/32      *[BGP/170] 01:24:24, localpref 100, from 10.200.1.6      #&lt;------core aggr IPv6 route
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 01:24:20, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
2011:310:1020::2/128                                                        #&lt;------core all IPv6 lo0
                   *[BGP/170] 01:24:16, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
                    [BGP/170] 01:24:20, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
2011:310:1020::3/128
                   *[BGP/170] 01:24:12, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
                    [BGP/170] 01:24:20, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
2011:310:1020::4/128
                   *[BGP/170] 01:24:08, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
                    [BGP/170] 01:24:18, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
2011:310:1020::5/128
                   *[BGP/170] 01:24:20, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
                    [BGP/170] 01:24:20, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
2011:310:1020::6/128
                   *[BGP/170] 01:24:24, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 01:24:20, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
2011:310:1020::7/128
                   *[BGP/170] 01:24:20, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
                    [BGP/170] 01:24:10, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
2011:310:1020::8/128
                   *[BGP/170] 01:24:20, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 01:24:14, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
3000:1000::/32     *[BGP/170] 01:24:16, localpref 100, from 10.200.1.5      #&lt;------ all T IPv6 routes
                      AS path: 1100 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
                    [BGP/170] 01:24:20, localpref 100, from 10.200.1.6
                      AS path: 1100 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
3000:2000::/32     *[BGP/170] 01:24:16, localpref 100, from 10.200.1.5
                      AS path: 1200 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
                    [BGP/170] 01:24:20, localpref 100, from 10.200.1.6
                      AS path: 1200 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
3000:3000::/32     *[BGP/170] 01:24:09, localpref 100, from 10.200.1.5
                      AS path: 1100 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
                    [BGP/170] 01:24:09, localpref 100, from 10.200.1.6
                      AS path: 1100 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
3000:4000::/32     *[BGP/170] 01:24:12, localpref 100, from 10.200.1.5
                      AS path: 1200 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
                    [BGP/170] 01:24:17, localpref 100, from 10.200.1.6
                      AS path: 1200 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
3333:3333:3333::/48*[BGP/170] 01:24:15, localpref 100, from 100.1.33.2      #&lt;------C3 IPv6 route
                      AS path: 300 I, validation-state: unverified
                    &gt; to ::100.1.33.2 via ge-1/2/1.133
4444:4444:4444::/48*[BGP/170] 01:24:20, localpref 100, from 10.200.1.5      #&lt;------C4 IPv6 route
                      AS path: 400 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
                    [BGP/170] 01:24:10, localpref 100, from 10.200.1.6
                      AS path: 400 I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
5555:5555:5555::/48*[BGP/170] 01:24:08, localpref 100, from 10.200.1.5      #&lt;------C5 IPv6 route
                      AS path: 500 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
                    [BGP/170] 01:24:18, localpref 100, from 10.200.1.6
                      AS path: 500 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
</code></pre>
<h3 id="verify6pe-label-pathc3-c4">verify:6PE label path:C3-C4</h3>
<p>R1-&gt;R2: label 299904</p>
<pre><code>lab@MX80-NGGWR-02# run show route forwarding-table matching 4444:4444:4444::/48 | find r1 
Logical system: r1
Routing table: default.inet6
Internet6:
Destination        Type RtRef Next hop           Type Index NhRef Netif
4444:4444:4444::/48 user     0                   indr 1048676     3
                              100.0.12.2        Push 2, Push 299808, Push 299904(top)  2561     2 ge-1/2/1.102

[edit]
lab@MX80-NGGWR-02# run show route 4444:4444:4444::/48 logical-system r1

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

4444:4444:4444::/48*[BGP/170] 03:22:48, localpref 100, from 10.200.1.5
                      AS path: 400 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r5     #&lt;------
                    [BGP/170] 03:22:48, localpref 100, from 10.200.1.6
                      AS path: 400 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r5

lab@MX80-NGGWR-02# run show route 4444:4444:4444::/48 logical-system r1 detail | match label          
                Label-switched-path r1-r5
                Label operation: Push 2, Push 299808, Push 299904(top)
                Label TTL action: prop-ttl, prop-ttl, prop-ttl(top)
                Route Label: 2
                Label-switched-path r1-r5
                Label operation: Push 2, Push 299808, Push 299904(top)
                Label TTL action: prop-ttl, prop-ttl, prop-ttl(top)
                Route Label: 2
</code></pre>
<p>R2-&gt;R5: 299904 -&gt; pop                            <br />
</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route table mpls.0 logical-system r2 label 299904

mpls.0: 29 destinations, 29 routes (29 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

299904             *[RSVP/7/1] 03:17:04, metric 1
                    &gt; to 100.0.25.2 via ge-1/2/1.205, label-switched-path r1-r5
299904(S=0)        *[RSVP/7/1] 03:17:04, metric 1
                    &gt; to 100.0.25.2 via ge-1/2/1.205, label-switched-path r1-r5

[edit]
lab@MX80-NGGWR-02# run show route table mpls.0 logical-system r2 label 299904 detail

mpls.0: 29 destinations, 29 routes (29 active, 0 holddown, 0 hidden)
Restart Complete
299904 (1 entry, 1 announced)
        *RSVP   Preference: 7/1
                Next hop type: Router, Next hop index: 2485
                Address: 0x2a8051c
                Next-hop reference count: 3
                Next hop: 100.0.25.2 via ge-1/2/1.205 weight 0x1, selected
                Label-switched-path r1-r5
                Label operation: Pop      
                Session Id: 0x600002
                State: &lt;Active Int AckRequest Accounting&gt;
                Local AS: 4012345678 
                Age: 3:18:10    Metric: 1 
                Validation State: unverified 
                Task: RSVP
                Announcement bits (1): 1-KRT 
                AS path: I

299904(S=0) (1 entry, 1 announced)
        *RSVP   Preference: 7/1
                Next hop type: Router, Next hop index: 2486
                Address: 0x2a80568
                Next-hop reference count: 2
                Next hop: 100.0.25.2 via ge-1/2/1.205 weight 0x1, selected
                Label-switched-path r1-r5
                Label operation: Pop      
                Session Id: 0x600002
                State: &lt;Active Int AckRequest Accounting&gt;
                Local AS: 4012345678 
                Age: 3:18:10    Metric: 1 
                Validation State: unverified 
                Task: RSVP
                Announcement bits (1): 1-KRT 
                AS path: I
</code></pre>
<p>R5-&gt;R7:</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route table mpls.0 logical-system r5 label 299808

mpls.0: 24 destinations, 24 routes (24 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

299808             *[LDP/9] 03:19:58, metric 1
                    &gt; to 100.0.57.2 via ge-1/2/1.507, Pop      
299808(S=0)        *[LDP/9] 03:19:58, metric 1
                    &gt; to 100.0.57.2 via ge-1/2/1.507, Pop

[edit]
lab@MX80-NGGWR-02# run show route table mpls.0 logical-system r5 label 299808 detail

mpls.0: 24 destinations, 24 routes (24 active, 0 holddown, 0 hidden)
Restart Complete
299808 (1 entry, 1 announced)
        *LDP    Preference: 9
                Next hop type: Router, Next hop index: 2401
                Address: 0x26e6d7c
                Next-hop reference count: 2
                Next hop: 100.0.57.2 via ge-1/2/1.507, selected
                Label operation: Pop      
                Session Id: 0x48000b
                State: &lt;Active Int&gt;
                Local AS: 4012345678 
                Age: 3:20:03    Metric: 1 
                Validation State: unverified 
                Task: LDP
                Announcement bits (1): 1-KRT 
                AS path: I
                Prefixes bound to route: 10.200.1.7/32

299808(S=0) (1 entry, 1 announced)
        *LDP    Preference: 9
                Next hop type: Router, Next hop index: 2402
                Address: 0x26e6dc8
                Next-hop reference count: 2
                Next hop: 100.0.57.2 via ge-1/2/1.507, selected
                Label operation: Pop      
                Session Id: 0x48000b
                State: &lt;Active Int&gt;
                Local AS: 4012345678 
                Age: 3:20:03    Metric: 1 
                Validation State: unverified 
                Task: LDP
                Announcement bits (1): 1-KRT 
                AS path: I
</code></pre>
<p>R7: receive</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route table mpls.0 logical-system r7 label 2

mpls.0: 11 destinations, 11 routes (11 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

2                  *[MPLS/0] 03:21:53, metric 1
                      Receive
</code></pre>
<h3 id="config-rtbh">config: RTBH</h3>
<pre><code>set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 1 from protocol bgp
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 1 from community rtbh
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 1 from route-filter 0.0.0.0/0 prefix-length-range /32-/32
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 1 then next-hop discard
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 1 then accept
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 2 from protocol bgp
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 2 from community rtbh
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 2 from route-filter ::/0 prefix-length-range /128-/128
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 2 then next-hop discard
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 2 then accept
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 3 from protocol bgp
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 3 from community rtbh
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 3 then community delete rtbh
set logical-systems r2 policy-options policy-statement imp-bgp-rtbh term 3 then accept
set logical-systems r2 policy-options community rtbh members 65412:100
set logical-systems r2 policy-options community rtbh members target:4012345678L:2000
set logical-systems r2 protocols bgp group to-v4v6-rr import imp-bgp-rtbh

set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 1 from protocol bgp
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 1 from community rtbh
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 1 from route-filter 0.0.0.0/0 prefix-length-range /32-/32
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 1 then next-hop discard
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 1 then accept
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 2 from protocol bgp
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 2 from community rtbh
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 2 from route-filter ::/0 prefix-length-range /128-/128
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 2 then next-hop discard
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 2 then accept
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 3 from protocol bgp
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 3 from community rtbh
set logical-systems r3 policy-options policy-statement imp-bgp-rtbh term 3 then community delete rtbh
set logical-systems r3 policy-options community rtbh members 65412:100
set logical-systems r3 policy-options community rtbh members target:4012345678L:2000
set logical-systems r2 protocols bgp group to-v4v6-rr import imp-bgp-rtbh

set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 1 from protocol bgp
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 1 from community rtbh
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 1 from route-filter 0.0.0.0/0 prefix-length-range /32-/32
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 1 then next-hop discard
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 1 then accept
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 2 from protocol bgp
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 2 from community rtbh
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 2 from route-filter ::/0 prefix-length-range /128-/128
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 2 then next-hop discard
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 2 then accept
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 3 from protocol bgp
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 3 from community rtbh
set logical-systems r5 policy-options policy-statement imp-bgp-rtbh term 3 then community delete rtbh
set logical-systems r5 policy-options community rtbh members 65412:100
set logical-systems r5 policy-options community rtbh members target:4012345678L:2000
set logical-systems r5 protocols bgp group v4v6-rr import imp-bgp-rtbh
</code></pre>
<h3 id="verify-rtbh">verify: RTBH</h3>
<p>R5 rib-in (before imp policy): 
initial C3 routes from R1</p>
<ul>
<li>
<p>non-host routes also with 2 communities, need to delete</p>
<p>[edit]
lab@MX80-NGGWR-02# run show route protocol bgp logical-system r5 receive-protocol bgp 10.200.1.1 table inet.0 detail<br />
</p>
<p>inet.0: 50 destinations, 64 routes (50 active, 0 holddown, 0 hidden)
Restart Complete
* 3.3.3.0/24 (2 entries, 1 announced)
     Accepted
     Nexthop: 10.200.1.1    #&lt;------
     Localpref: 100
     AS path: 300 I
     Communities: 65412:100 65513:100 target:4012345678L:2000       #&lt;------</p>
<ul>
<li>
<p>20.20.0.0/16 (2 entries, 1 announced)
     Accepted
     Nexthop: 10.200.1.1
     Localpref: 100
     AS path: I
     Aggregator: 4012345678 10.200.1.1</p>
</li>
<li>
<p>33.33.0.0/16 (2 entries, 1 announced)
     Accepted
     Nexthop: 10.200.1.1    #&lt;------
     Localpref: 100
     AS path: 300 I
     Communities: 65412:100 65513:100 target:4012345678L:2000       #&lt;------</p>
</li>
<li>
<p>33.33.33.33/32 (2 entries, 1 announced)
     Accepted
     Nexthop: 10.200.1.1    #&lt;------
     Localpref: 100
     AS path: 300 I
     Communities: 65412:100 65513:100 target:4012345678L:2000       #&lt;------</p>
</li>
</ul>
</li>
</ul>
<p>R5 rib(after imp policy)</p>
<ul>
<li>the non-host routes: removed the 2 communities</li>
<li>the non-host routes: don't change next-hop</li>
<li>host routes: keep the 2 communities</li>
<li>
<p>host routes: next-hop set to discard</p>
<p>[edit]
lab@MX80-NGGWR-02# run show route protocol bgp logical-system r5 3.3.3.0/24 detail<br />
</p>
<p>inet.0: 50 destinations, 64 routes (50 active, 0 holddown, 0 hidden)
Restart Complete
3.3.3.0/24 (2 entries, 1 announced)
        *BGP    Preference: 170/-101
                Next hop type: Indirect
                Address: 0x26e7664
                Next-hop reference count: 12
                Source: 10.200.1.1
                Next hop type: Router, Next hop index: 2539
                Next hop: 100.0.25.1 via ge-1/2/2.205 weight 0x1, selected  #&lt;------
                Label-switched-path r5-r1
                Label operation: Push 299936
                Label TTL action: prop-ttl
                Session Id: 0x80008
                Protocol next hop: 10.200.1.1
                Indirect next hop: 297c760 1048668 INH Session ID: 0x80012
                State: <Active Int Ext>
                Local AS: 4012345678 Peer AS: 4012345678
                Age: 2:26:58    Metric2: 10 
                Validation State: unverified 
                Task: BGP_4012345678.10.200.1.1+179
                Announcement bits (3): 1-KRT 5-BGP_RT_Background 6-Resolve tree 4 
                AS path: 300 I
                Communities: 65513:100      #&lt;------
                Accepted
                Localpref: 100
                Router ID: 10.200.1.1
         BGP    Preference: 170/-101
                Next hop type: Indirect
                Address: 0x26e7664
                Next-hop reference count: 12
                Source: 10.200.1.6
                Next hop type: Router, Next hop index: 2539
                Next hop: 100.0.25.1 via ge-1/2/2.205 weight 0x1, selected  #&lt;------
                Label-switched-path r5-r1
                Label operation: Push 299936
                Label TTL action: prop-ttl
                Session Id: 0x80008
                Protocol next hop: 10.200.1.1
                Indirect next hop: 297c760 1048668 INH Session ID: 0x80012
                State: <NotBest Int Ext>
                Inactive reason: Not Best in its group - Cluster list length
                Local AS: 4012345678 Peer AS: 4012345678
                Age: 2:26:58    Metric2: 10 
                Validation State: unverified 
                Task: BGP_4012345678.10.200.1.6+179
                AS path: 300 I (Originator)
                Cluster list:  6.6.6.6
                Originator ID: 10.200.1.1
                Communities: 65513:100      #&lt;------
                Accepted
                Localpref: 100
                Router ID: 10.200.1.6 <br />
</p>
<p>[edit]
lab@MX80-NGGWR-02# run show route protocol bgp logical-system r5 33.33.33.33/32 detail<br />
</p>
<p>inet.0: 50 destinations, 64 routes (50 active, 0 holddown, 0 hidden)
Restart Complete
33.33.33.33/32 (2 entries, 1 announced)
        *BGP    Preference: 170/-101
                Next hop type: Discard      #&lt;------
                Address: 0x24cf08c
                Next-hop reference count: 8
                State: <Active Int Ext>
                Local AS: 4012345678 Peer AS: 4012345678
                Age: 2:31:29 
                Validation State: unverified 
                Task: BGP_4012345678.10.200.1.1+179
                Announcement bits (3): 1-KRT 5-BGP_RT_Background 6-Resolve tree 4 
                AS path: 300 I
                Communities: 65412:100 65513:100 target:4012345678L:2000    #&lt;------
                Accepted
                Localpref: 100
                Router ID: 10.200.1.1
         BGP    Preference: 170/-101
                Next hop type: Discard      #&lt;------
                Address: 0x24cf08c
                Next-hop reference count: 8
                State: <NotBest Int Ext>
                Inactive reason: Not Best in its group - Cluster list length
                Local AS: 4012345678 Peer AS: 4012345678
                Age: 2:31:29 
                Validation State: unverified 
                Task: BGP_4012345678.10.200.1.6+179
                AS path: 300 I (Originator)
                Cluster list:  6.6.6.6
                Originator ID: 10.200.1.1
                Communities: 65412:100 65513:100 target:4012345678L:2000    #&lt;------
                Accepted
                Localpref: 100
                Router ID: 10.200.1.6</p>
</li>
</ul>
<h3 id="config-ipv6-routes-aggregation">config: IPv6 routes aggregation</h3>
<p>R1-R8: adv IPv6 lo0</p>
<p>R5-R6: adv aggr.ed IPv4&amp;IPv6 routes</p>
<pre><code>set logical-systems r1 policy-options policy-statement exp-bgp-lo0-v6 term 1 from route-filter 2011:0310:1020::1/128 exact
set logical-systems r1 policy-options policy-statement exp-bgp-lo0-v6 term 1 then accept
set logical-systems r1 protocols bgp group to-v4v6-rr export exp-bgp-lo0-v6

set logical-systems r2 policy-options policy-statement exp-bgp-lo0-v6 term 1 from route-filter 2011:0310:1020::2/128 exact
set logical-systems r2 policy-options policy-statement exp-bgp-lo0-v6 term 1 then accept
set logical-systems r2 protocols bgp group to-v4v6-rr export exp-bgp-lo0-v6

set logical-systems r3 policy-options policy-statement exp-bgp-lo0-v6 term 1 from route-filter 2011:0310:1020::3/128 exact
set logical-systems r3 policy-options policy-statement exp-bgp-lo0-v6 term 1 then accept
set logical-systems r3 protocols bgp group to-v4v6-rr export exp-bgp-lo0-v6

set logical-systems r4 policy-options policy-statement exp-bgp-lo0-v6 term 1 from route-filter 2011:0310:1020::4/128 exact
set logical-systems r4 policy-options policy-statement exp-bgp-lo0-v6 term 1 then accept
set logical-systems r4 protocols bgp group to-v4v6-rr export exp-bgp-lo0-v6

set logical-systems r5 routing-options aggregate route 10.200.0.0/16
set logical-systems r5 routing-options rib inet6.0 aggregate route 2011:0310::/32
set logical-systems r5 policy-options policy-statement exp-bgp-lo0-v6 term 1 from route-filter 10.200.0.0/16 exact
set logical-systems r5 policy-options policy-statement exp-bgp-lo0-v6 term 1 then accept
set logical-systems r5 policy-options policy-statement exp-bgp-lo0-v6 term 2 from route-filter 2011:0310::/32 exact
set logical-systems r5 policy-options policy-statement exp-bgp-lo0-v6 term 2 then accept
set logical-systems r5 policy-options policy-statement exp-bgp-lo0-v6 term 3 from route-filter 2011:0310:1020::5/128 exact
set logical-systems r5 policy-options policy-statement exp-bgp-lo0-v6 term 3 then accept
set logical-systems r5 protocols bgp group to-v4v6-rr export exp-bgp-lo0-v6
set logical-systems r5 protocols bgp group to-r6 export exp-bgp-lo0-v6

set logical-systems r6 routing-options aggregate route 10.200.0.0/16
set logical-systems r6 routing-options rib inet6.0 aggregate route 2011:0310::/32
set logical-systems r6 policy-options policy-statement exp-bgp-lo0-v6 term 1 from route-filter 10.200.0.0/16 exact
set logical-systems r6 policy-options policy-statement exp-bgp-lo0-v6 term 1 then accept
set logical-systems r6 policy-options policy-statement exp-bgp-lo0-v6 term 2 from route-filter 2011:0310::/32 exact
set logical-systems r6 policy-options policy-statement exp-bgp-lo0-v6 term 2 then accept
set logical-systems r6 policy-options policy-statement exp-bgp-lo0-v6 term 3 from route-filter 2011:0310:1020::6/128 exact
set logical-systems r6 policy-options policy-statement exp-bgp-lo0-v6 term 3 then accept
set logical-systems r6 protocols bgp group to-v4v6-rr export exp-bgp-lo0-v6
set logical-systems r6 protocols bgp group to-r5 export exp-bgp-lo0-v6

set logical-systems r7 policy-options policy-statement exp-bgp-lo0-v6 term 1 from route-filter 2011:0310:1020::7/128 exact
set logical-systems r7 policy-options policy-statement exp-bgp-lo0-v6 term 1 then accept
set logical-systems r7 protocols bgp group to-v4v6-rr export exp-bgp-lo0-v6

set logical-systems r8 policy-options policy-statement exp-bgp-lo0-v6 term 1 from route-filter 2011:0310:1020::8/128 exact
set logical-systems r8 policy-options policy-statement exp-bgp-lo0-v6 term 1 then accept
set logical-systems r8 protocols bgp group to-v4v6-rr export exp-bgp-lo0-v6
</code></pre>
<p>to P: reject some too pecific routes</p>
<pre><code>set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 1 from protocol bgp
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 1 from community t-route
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 1 then reject
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 2 from route-filter 0.0.0.0/0 prefix-length-range /21-/32         #&lt;------
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 2 then reject     #&lt;------
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 3 from route-filter ::/0 prefix-length-range /49-/128     #&lt;------
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 3 then reject     #&lt;------
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 4 from route-filter 10.200.0.0/16 exact   #&lt;------MUST
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 4 then accept                             #&lt;------MUST
set logical-systems r2 protocols bgp group to-p-v4 export exp-bgp-p-out
set logical-systems r2 protocols bgp group to-p-v6 export exp-bgp-p-out

set logical-systems r3 policy-options policy-statement exp-bgp-p-out term 1 from protocol bgp
set logical-systems r3 policy-options policy-statement exp-bgp-p-out term 1 from community t-route
set logical-systems r3 policy-options policy-statement exp-bgp-p-out term 1 then reject
set logical-systems r3 policy-options policy-statement exp-bgp-p-out term 2 from route-filter 0.0.0.0/0 prefix-length-range /21-/32         #&lt;------
set logical-systems r3 policy-options policy-statement exp-bgp-p-out term 2 then reject     #&lt;------
set logical-systems r3 policy-options policy-statement exp-bgp-p-out term 3 from route-filter ::/0 prefix-length-range /49-/128     #&lt;------
set logical-systems r3 policy-options policy-statement exp-bgp-p-out term 3 then reject     #&lt;------
set logical-systems r3 protocols bgp group to-p-v4 export exp-bgp-p-out
set logical-systems r3 protocols bgp group to-p-v6 export exp-bgp-p-out

set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 1 from protocol bgp
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 1 from community t-route
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 1 then reject
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 2 from route-filter 0.0.0.0/0 prefix-length-range /21-/32         #&lt;------
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 2 then reject     #&lt;------
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 3 from route-filter ::/0 prefix-length-range /49-/128     #&lt;------
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 3 then reject     #&lt;------
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 4 from protocol aggregate
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 4 from route-filter 10.200.0.0/16 exact   #&lt;------
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 4 then accept     #&lt;------
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 5 from protocol aggregate         #&lt;------
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 5 from route-filter 2011:310::/32 exact   #&lt;------
set logical-systems r5 policy-options policy-statement exp-bgp-p-out term 5 then accept
set logical-systems r5 protocols bgp group to-p-v4 export exp-bgp-p-out
set logical-systems r5 protocols bgp group to-p-v6 export exp-bgp-p-out
</code></pre>
<h3 id="tip-r2-policy-term4-is-a-must">TIP: R2 policy term4 is a must</h3>
<pre><code>lab@MX80-NGGWR-02# run show route logical-system r2 10.200/16

inet.0: 72 destinations, 90 routes (71 active, 0 holddown, 3 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

10.200.0.0/16      *[Aggregate/130] 03:34:02
                      Reject
                    [BGP/170] 03:33:26, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.2 via ge-1/2/1.204, label-switched-path r2-r5
                    [BGP/170] 03:33:36, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.26.2 via ge-1/2/1.206, label-switched-path r2-r6
                      to 100.0.25.2 via ge-1/2/1.205, label-switched-path Bypass-&gt;100.0.26.2
</code></pre>
<h3 id="note-suppress-specific-route-including-c-or-not">NOTE: suppress specific route , including C or not</h3>
<p>currently suppress all specific routes.
if the target is meant to suppress specific routes from core, but not to
specific routes from C, then insert another term before term 2, </p>
<pre><code>from community c-route
then accept

[edit]
lab@MX80-NGGWR-02# show logical-systems r2 policy-options policy-statement exp-bgp-p-out | display set 
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 1 from protocol bgp
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 1 from community t-route
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 1 then reject
#optional, depending on whether specific routes from C is allowed or not
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 2-b1 from community c-route       #&lt;---
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 2-b1 then accept                  #&lt;---
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 2 from route-filter 0.0.0.0/0 prefix-length-range /21-/32
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 2 then reject
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 3 from route-filter ::/0 prefix-length-range /49-/128
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 3 then reject
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 4 from route-filter 10.200.0.0/16 exact
set logical-systems r2 policy-options policy-statement exp-bgp-p-out term 4 then accept

[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp 100.2.11.2 logical-system r2

inet.0: 72 destinations, 90 routes (71 active, 0 holddown, 3 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* 3.3.3.0/24              Self                                    300 I
* 10.200.0.0/16           Self                                    I
* 20.20.0.0/16            Self                                    I
* 33.33.0.0/16            Self                                    300 I
* 33.33.33.33/32          Self                                    300 I
* 44.44.0.0/16            Self                                    400 I
* 211.2.0.0/16            Self                                    2000 I
* 211.3.0.0/16            Self                                    3000 I
* 211.5.0.0/16            Self                                    2000 I
* 211.6.0.0/16            Self                                    2000 I
* 211.7.0.0/16            Self                                    3000 I

[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp ::100.2.11.2 logical-system r2

inet6.0: 48 destinations, 77 routes (48 active, 0 holddown, 0 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* ::3.3.3.0/120           Self                                    300 I
* ::33.33.33.33/128       Self                                    300 I
* 2000:2000::/32          Self                                    2000 I
* 2000:3000::/32          Self                                    3000 I
* 2000:5000::/32          Self                                    2000 I
* 2000:6000::/32          Self                                    2000 I
* 2000:7000::/32          Self                                    3000 I
* 2011:310::/32           Self                                    I
* 3333:3333:3333::/48     Self                                    300 I
* 4444:4444:4444::/48     Self                                    400 I
* 5555:5555:5555::/48     Self                                    500 I
</code></pre>
<h3 id="verify-ipv6-aggr">verify IPv6 aggr</h3>
<p>R1-R8 has : aggr. V4 &amp; V6 routes, all IPv6 lo0</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route logical-system r1 10.200/16 exact table inet.0

inet.0: 49 destinations, 67 routes (46 active, 0 holddown, 3 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

10.200.0.0/16      *[BGP/170] 03:25:58, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 03:25:54, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5

[edit]
lab@MX80-NGGWR-02# run show route logical-system r1 2011:310::/32

inet6.0: 32 destinations, 55 routes (32 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

2011:310::/32      *[BGP/170] 03:26:49, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 03:26:45, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
2011:310:1020::1/128
                   *[Direct/0] 03:27:06
                    &gt; via lo0.1
2011:310:1020::2/128
                   *[BGP/170] 03:26:41, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
                    [BGP/170] 03:26:45, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r2
2011:310:1020::3/128
                   *[BGP/170] 03:26:37, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
                    [BGP/170] 03:26:45, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r3
2011:310:1020::4/128
                   *[BGP/170] 03:26:33, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
                    [BGP/170] 03:26:43, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
2011:310:1020::5/128
                   *[BGP/170] 03:26:45, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
                    [BGP/170] 03:26:45, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
2011:310:1020::6/128
                   *[BGP/170] 03:26:49, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 03:26:45, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
2011:310:1020::7/128                    
                   *[BGP/170] 03:26:45, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
                    [BGP/170] 03:26:35, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.13.2 via ge-1/2/1.103, label-switched-path r1-r5
2011:310:1020::8/128
                   *[BGP/170] 03:26:45, localpref 100, from 10.200.1.5
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 03:26:39, localpref 100, from 10.200.1.6
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
</code></pre>
<p>R2 to P:  aggr V4&amp;V6, no too specific routes</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp 100.2.11.2 logical-system r2

inet.0: 72 destinations, 90 routes (71 active, 0 holddown, 3 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* 10.200.0.0/16           Self                                    I         #&lt;------
* 20.20.0.0/16            Self                                    I
* 33.33.0.0/16            Self                                    300 I
* 44.44.0.0/16            Self                                    400 I
* 211.2.0.0/16            Self                                    2000 I
* 211.3.0.0/16            Self                                    3000 I
* 211.5.0.0/16            Self                                    2000 I
* 211.6.0.0/16            Self                                    2000 I
* 211.7.0.0/16            Self                                    3000 I

[edit]
lab@MX80-NGGWR-02# run show route advertising-protocol bgp ::100.2.11.2 logical-system r2

inet6.0: 48 destinations, 77 routes (48 active, 0 holddown, 0 hidden)
Restart Complete
  Prefix                  Nexthop              MED     Lclpref    AS path
* 2000:2000::/32          Self                                    2000 I
* 2000:3000::/32          Self                                    3000 I
* 2000:5000::/32          Self                                    2000 I
* 2000:6000::/32          Self                                    2000 I
* 2000:7000::/32          Self                                    3000 I
* 2011:310::/32           Self                                    I         #&lt;------
* 3333:3333:3333::/48     Self                                    300 I
* 4444:4444:4444::/48     Self                                    400 I
* 5555:5555:5555::/48     Self                                    500 I
</code></pre>
<h3 id="tip-unverified-route">TIP: unverified route</h3>
<p><a href="http://www.juniper.net/techpubs/en_US/junos12.2/topics/topic-map/bgp-origin-as-validation.html">http://www.juniper.net/techpubs/en_US/junos12.2/topics/topic-map/bgp-origin-as-validation.html</a></p>
<h3 id="tip-missing-rid-on-a-pure-ipv6-router">TIP: missing RID on a pure IPv6 router</h3>
<p>in the IPv6 network (only IPv6), BGP router id need to be specified 32 bit. OPEN message  need to be add on both CEs router.</p>
<p>Quote from RFC 2544:
  "Note that the information referred above is distinct from the BGP
   Identifier used in the BGP-4 tie breaking procedure. The BGP
   Identifier is a 32 bit unsigned integer exchanged between two peers
   at session establishment time, within an OPEN message. This is a
   system wide value determined at startup which must be unique in the
   network and should be derived from an IPv4 address regardless of the
   network protocol(s) a particular BGP-4 instance is configured to
   convey at a given moment."</p>
<p>If you are not configure router ID on CE router, OPEN message will fail.  BGP session cannot established. Debug will show why IPv6 BGP session failed when CE router have no router id.</p>
<pre><code>Mar  1 08:57:35  prime pe2: rpd[3251]: bgp_get_open: NOTIFICATION sent to 11::2+4597 (proto): 
code 2 (Open Message Error) subcode 3 (bad BGP ID), Reason: peer 11::2+4597 (proto): 
invalid BGP identifier 0x0
</code></pre>
<h2 id="interas-vpn-part-a">InterAS VPN (PART A)</h2>
<h3 id="config-interas-vpn">config: InterAS VPN</h3>
<p>R5: 
    #to both RR and ASBR, config: family inet unicast+labeled unicast rib inet.3 
    set logical-systems r5 protocols bgp group to-asbr neighbor 100.5.22.2 family inet unicast
    set logical-systems r5 protocols bgp group to-asbr neighbor 100.5.22.2 family inet labeled-unicast rib inet.3
    set logical-systems r5 protocols bgp group to-asbr neighbor 100.5.22.2 peer-as 2</p>
<pre><code>set logical-systems r5 protocols bgp group v4v6-rr family inet unicast
set logical-systems r5 protocols bgp group v4v6-rr family inet labeled-unicast rib inet.3

#adv. R1 lo0 both as inet (from def rib.0), and labeled-inet (from rib inet.3)
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 1 from protocol isis
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 1 from route-filter 10.200.1.1/32 exact
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 1 then accept
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 2 from rib inet.3
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 2 from route-filter 10.200.1.1/32 exact
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 2 then accept

set logical-systems r5 protocols bgp group to-asbr neighbor 100.5.22.2 export exp-bgp-adv-1
</code></pre>
<p>R1:</p>
<pre><code>#config MH-MP-EBGP to remote PE; 
#to both end enable inet unicast+labeled-unicast; to remote PE also enable inet-vpn
set logical-systems r1 protocols bgp group to-v4v6-rr family inet unicast
set logical-systems r1 protocols bgp group to-v4v6-rr family inet labeled-unicast rib inet.3
set logical-systems r1 protocols bgp group to-pe multihop
set logical-systems r1 protocols bgp group to-pe neighbor 10.10.10.10 family inet unicast
set logical-systems r1 protocols bgp group to-pe neighbor 10.10.10.10 family inet labeled-unicast rib inet.3
set logical-systems r1 protocols bgp group to-pe neighbor 10.10.10.10 family inet-vpn unicast
set logical-systems r1 protocols bgp group to-pe neighbor 10.10.10.10 peer-as 2
</code></pre>
<h3 id="config-r1-vrf-to-local-ce">config: R1 VRF to local CE</h3>
<p>R1 VRF:</p>
<pre><code>set logical-systems r1 routing-instances PINK instance-type vrf
set logical-systems r1 routing-instances PINK interface ge-1/2/1.611
set logical-systems r1 routing-instances PINK interface lo0.111
set logical-systems r1 routing-instances PINK route-distinguisher 10.200.1.1:1
set logical-systems r1 routing-instances PINK vrf-import vrf-imp
set logical-systems r1 routing-instances PINK vrf-export vrf-exp
set logical-systems r1 routing-instances PINK vrf-table-label
set logical-systems r1 routing-instances PINK protocols bgp group to-ce1 neighbor 200.6.11.2 family inet unicast
set logical-systems r1 routing-instances PINK protocols bgp group to-ce1 neighbor 200.6.11.2 peer-as 1111

set logical-systems r1 policy-options policy-statement vrf-exp term 1 from protocol bgp
set logical-systems r1 policy-options policy-statement vrf-exp term 1 then community add GREEN
set logical-systems r1 policy-options policy-statement vrf-exp term 1 then accept
set logical-systems r1 policy-options policy-statement vrf-exp term 2 from protocol direct
set logical-systems r1 policy-options policy-statement vrf-exp term 2 then community add GREEN
set logical-systems r1 policy-options policy-statement vrf-exp term 2 then accept

set logical-systems r1 policy-options policy-statement vrf-imp term 1 from protocol bgp
set logical-systems r1 policy-options policy-statement vrf-imp term 1 from community GREEN
set logical-systems r1 policy-options policy-statement vrf-imp term 1 then accept
</code></pre>
<h3 id="verify-e2e-pingtraceroute">verify: e2e ping/traceroute</h3>
<pre><code>[edit]
lab@MX80-NGGWR-02# run ping 20.20.2.11 logical-system r0 routing-instance vpn1 source 20.20.1.11 
PING 20.20.2.11 (20.20.2.11): 56 data bytes
64 bytes from 20.20.2.11: icmp_seq=0 ttl=60 time=0.929 ms
^C
--- 20.20.2.11 ping statistics ---
1 packets transmitted, 1 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.929/0.929/0.929/0.000 ms

[edit]
lab@MX80-NGGWR-02# run traceroute 20.20.2.11 logical-system r0 routing-instance vpn1 source 20.20.1.11 
traceroute to 20.20.2.11 (20.20.2.11) from 20.20.1.11, 30 hops max, 40 byte packets
 1  200.6.11.1 (200.6.11.1)  0.594 ms  0.495 ms  0.552 ms
 2  100.0.13.2 (100.0.13.2)  0.886 ms  0.876 ms  0.594 ms
     MPLS Label=299776 CoS=0 TTL=1 S=0
     MPLS Label=299984 CoS=0 TTL=1 S=0
     MPLS Label=16 CoS=0 TTL=1 S=1
 3  100.0.35.2 (100.0.35.2)  0.609 ms  0.722 ms  0.579 ms
     MPLS Label=299984 CoS=0 TTL=1 S=0
     MPLS Label=16 CoS=0 TTL=2 S=1
 4  100.5.22.2 (100.5.22.2)  0.600 ms  0.610 ms  0.583 ms
     MPLS Label=299776 CoS=0 TTL=1 S=0
     MPLS Label=16 CoS=0 TTL=3 S=1
 5  20.20.2.11 (20.20.2.11)  0.637 ms  0.614 ms  0.576 ms
</code></pre>
<h3 id="tip-inet-labeled-unicast-resolve-vpn">TIP: <code>inet labeled-unicast resolve-vpn</code></h3>
<p>Allow labeled routes to be placed in the inet.3 routing table for route
resolution. These routes are then resolved for PE router connections where the
remote PE is located across another AS. For a PE router to install a route in
the VRF, the next hop must resolve to a route stored within the inet.3 table</p>
<h3 id="tip-find-out-communities">TIP: find out communities</h3>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route receive-protocol bgp 10.10.10.10 logical-system r1 table bgp.l3vpn.0 detail

bgp.l3vpn.0: 3 destinations, 3 routes (3 active, 0 holddown, 0 hidden)
Restart Complete
* 10.10.10.10:1:20.20.2.11/32 (1 entry, 1 announced)
     Import Accepted
     Route Distinguisher: 10.10.10.10:1
     VPN Label: 16
     Nexthop: 10.10.10.10
     AS path: 2 I
     Communities: target:2:65000
</code></pre>
<h3 id="tip-policy-from-rib-inet3">TIP: policy "from rib inet.3"</h3>
<pre><code>R1             (BGP route NLRI addr family)         R5
   ============================================&gt;
inet.0          inet unicast                        inet.0
inet.3          inet labeled-unicast                inet.3

inet unicast: 传递unicast的路由，放入inet.0
labeled-unicast：传递unciast路由，放入inet.0
labeld-unicast rib inet.3: 传递inet.3的路由，放入inet.3
inet unicast+rib inet.3：传递inet.0和inet.3的路由，unicast的放入inet.0, rib inet.3的放入inet.3
</code></pre>
<p>这就是为什么无法同时配置inet uncast 和labeled-unicast，而可以同时配置inet unicast和rib inet.3 </p>
<pre><code>lab@MX80-NGGWR-01# show logical-systems r5 policy-options policy-statement exp-bgp-adv-1    
term 1 {
    from {
        protocol isis;                      #&lt;------taken from inet.0
        route-filter 10.10.1.1/32 exact;    #&lt;--will be adv. as `inet-unicast`
    }
    then accept;

}
term 2 {
    from {
        rib inet.3;                         #&lt;------taken from inet.0
        route-filter 10.10.1.1/32 exact;    #&lt;--will be adv. as `inet-labeled-unicast`
    }
    then accept;
}
</code></pre>
<h3 id="tip-interas-vpn-options">TIP: interAS VPN options</h3>
<p>Option A: Unlabeled VPN-IPv4 (b2b vrf)</p>
<pre><code>vrf1                              vrf1                                 vrf1
    PE1---------------------ASBR1-------ASBR2-----------------------PE2
vrf2                              vrf2                                 vrf2
</code></pre>
<ul>
<li>ASBR:<ul>
<li>carry all routes in: bgp.v3vpn.0, and each VRFs</li>
</ul>
</li>
<li>least scale, not good</li>
</ul>
<p>Option B: Labeled VPN-IPv4</p>
<ul>
<li>
<p>ASBR:</p>
<ul>
<li>retain all VPN routes , in bgp.l3vpn.0</li>
<li>labeled-unicast to assign label(stitching e2e LSP)</li>
</ul>
<p>vrf1                                                                   vrf1
    PE1---------------------ASBR1-------ASBR2-----------------------PE2
vrf2                                                                   vrf2</p>
<pre><code>    &lt;....(ldp label).......(BGP label).....(ldp label)......&gt;
</code></pre>
</li>
</ul>
<p>Option C: Multihop MP-BGP</p>
<pre><code>vrf1                                                                   vrf1
    PE1---------------------ASBR1-------ASBR2-----------------------PE2
vrf2                                                                   vrf2

        &lt;....(ldp label).......(BGP label).....(ldp label)......&gt;
</code></pre>
<ul>
<li>PE:<ul>
<li>multi-hop MP-EBGP betw PE</li>
</ul>
</li>
<li>ASBR: <ul>
<li>no need to maintain VPN routes</li>
<li>leak PE1 lo0 into peer AS</li>
<li>labeled-unicast to assign label</li>
</ul>
</li>
</ul>
<h3 id="tip-family-in-diff-levels">TIP: family in diff levels</h3>
<ul>
<li>without configs in more specific level, it "inherit" from upper level</li>
<li>once configured in more specific level, it "overide", no more inheritence</li>
</ul>
<p>same as policys, anything else in JUNOS</p>
<h3 id="tip-bgp-keep-all">TIP: bgp keep-all</h3>
<p>keep all bgp.l3vpn.0 regardless of RT</p>
<h3 id="questionresolved-bgp-flaps-duing-config">QUESTION(resolved): bgp flaps duing config</h3>
<p>noticed bgp flaps during inter-AS vpn configs,might be normal</p>
<pre><code>Aug  4 04:39:35  MX80-NGGWR-01 r1:rpd[1401]: RPD_OSPF_NBRDOWN: OSPF neighbor 4.4.4.4 (realm ospf-v2 shamlink.0 area 0.0.0.0) state changed f
rom Full to Down due to KillNbr (event reason: interface went down)
Aug  4 04:39:34  MX80-NGGWR-01 r1: rpd[1401]: bgp_adv_main_update:7762: NOTIFICATION sent to 10.10.1.2 (Internal AS 4012345678): code 6 (Cea
se) subcode 6 (Other Configuration Change), Reason: Configuration change - VPN table advertise
Aug  4 04:39:34  MX80-NGGWR-01 r1: rpd[1401]: bgp_adv_main_update:7762: NOTIFICATION sent to 10.10.1.3 (Internal AS 4012345678): code 6 (Cea
se) subcode 6 (Other Configuration Change), Reason: Configuration change - VPN table advertise
</code></pre>
<p>normal, capability re-negotiation</p>
<h3 id="toggle-traffic-engineering-mpls-forwarding">toggle <code>traffic-engineering mpls-forwarding</code></h3>
<pre><code>delete logical-systems r1 protocols mpls traffic-engineering  
delete logical-systems r5 protocols mpls traffic-engineering     
delete logical-systems r9 protocols mpls traffic-engineering

set logical-systems r1 protocols mpls traffic-engineering  
set logical-systems r5 protocols mpls traffic-engineering     
set logical-systems r9 protocols mpls traffic-engineering
</code></pre>
<h3 id="config-solution1old">config solution1(old):</h3>
<p><code>inet (uncast+labeled-unicast rib inet.3)</code></p>
<pre><code>###R5: adv R1 lo0 to peer ASBR via policy, as inet-unicast&amp;labeled-unicast
###    so peer ASBR can install R1 lo0 in both inet.0 &amp; inet.3
#match r1 lo0 from inet.0 (serving `inet-unicast` bgp family only)
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 1 from protocol isis
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 1 from route-filter 10.10.1.1/32 exact
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 1 then accept
#match r1 lo0 from inet.3 (serving `inet-labeled-unicast` family only)
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 2 from rib inet.3
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 2 from route-filter 10.10.1.1/32 exact
set logical-systems r5 policy-options policy-statement exp-bgp-adv-1 term 2 then accept

#`family inet unicast` =&gt;                    r1 lo0 from inet.0 will be adv.ed as `inet-unicast` bgp routes
#`family inet labeled-unicast rib inet.3` =&gt; r1 lo0 from inet.3 will be adv.ed as `inet-labeled-unicast` routes
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
</code></pre>
<h3 id="solution2-inet-resolved-vpn">solution2: <code>inet resolved-vpn</code></h3>
<pre><code>set logical-systems r1 protocols bgp group to-rr family inet labeled-unicast resolve-vpn    
set logical-systems r5 protocols bgp group l3vpn family inet labeled-unicast
set logical-systems r9 protocols bgp group to-r5 family inet labeled-unicast
</code></pre>
<h2 id="vpls-part-a">VPLS (PART A)</h2>
<h3 id="prepareborrow-ae-ports-to-be-used-as-vpls-ports">prepare:borrow ae ports to be used as vpls ports</h3>
<pre><code>deactivate interfaces ge-1/2/3 gigether-options 802.3ad    
deactivate interfaces ge-1/2/4 gigether-options 802.3ad    
deactivate interfaces ge-1/2/5 gigether-options 802.3ad    
deactivate interfaces ge-1/2/6 gigether-options 802.3ad    
deactivate logical-systems r3 interfaces ae10              
deactivate logical-systems r6 interfaces ae11

deactivate logical-systems r3 protocols isis interface ae10.0 
deactivate logical-systems r6 protocols isis interface ae11.0

activate logical-systems r3 interfaces ge-1/2/1 unit 306     
activate logical-systems r6 interfaces ge-1/2/2 unit 306 
activate logical-systems r3 protocols isis interface ge-1/2/1.306
activate logical-systems r6 protocols isis interface ge-1/2/2.306
</code></pre>
<h3 id="config-vpls">config vpls</h3>
<p>R1/7/8: vpls inteface</p>
<pre><code>set logical-systems r1 interfaces ge-1/2/3 unit 100 vlan-id 100 encapsulation vlan-vpls apply-groups-except interface
set logical-systems r1 interfaces ge-1/2/5 unit 100 vlan-id 100 encapsulation vlan-vpls apply-groups-except interface
set logical-systems r7 interfaces ge-1/3/0 unit 100 vlan-id 100 encapsulation vlan-vpls apply-groups-except interface
set logical-systems r8 interfaces ge-1/3/2 unit 100 vlan-id 100 encapsulation vlan-vpls apply-groups-except interface

set interfaces ge-1/2/3 vlan-tagging encapsulation flexible-ethernet-services
set interfaces ge-1/2/5 vlan-tagging encapsulation flexible-ethernet-services
set interfaces ge-1/3/0 vlan-tagging encapsulation flexible-ethernet-services
set interfaces ge-1/3/2 vlan-tagging encapsulation flexible-ethernet-services
</code></pre>
<p>R1/7/8/2/3 BGP family L2vpn signaling:</p>
<pre><code>set logical-systems r1 protocols bgp group to-vpn-rr family l2vpn signaling
set logical-systems r7 protocols bgp group to-vpn-rr family l2vpn signaling
set logical-systems r8 protocols bgp group to-vpn-rr family l2vpn signaling
</code></pre>
<p>VPLS RI: R1/7/8:</p>
<pre><code>set logical-systems r1 routing-instances GOLD instance-type vpls
set logical-systems r1 routing-instances GOLD interface ge-1/2/3.100
set logical-systems r1 routing-instances GOLD interface ge-1/2/5.100
set logical-systems r1 routing-instances GOLD route-distinguisher 1.1.1.1:1
set logical-systems r1 routing-instances GOLD vrf-target target:6500:1
set logical-systems r1 routing-instances GOLD protocols vpls site-range 10
set logical-systems r1 routing-instances GOLD protocols vpls interface-mac-limit 500
set logical-systems r1 routing-instances GOLD protocols vpls no-tunnel-services
set logical-systems r1 routing-instances GOLD protocols vpls site 1 site-identifier 1
set logical-systems r1 routing-instances GOLD protocols vpls site 1 active-interface any
#just for ping test purpose
#set logical-systems r1 routing-instances GOLD protocols vpls site 1 active-interface primary ge-1/2/5.100   
set logical-systems r1 routing-instances GOLD protocols vpls site 1 interface ge-1/2/3.100
set logical-systems r1 routing-instances GOLD protocols vpls site 1 interface ge-1/2/5.100

set logical-systems r7 routing-instances GOLD instance-type vpls
set logical-systems r7 routing-instances GOLD interface ge-1/3/0.100
set logical-systems r7 routing-instances GOLD route-distinguisher 7.7.7.7:1
set logical-systems r7 routing-instances GOLD vrf-target target:6500:1
set logical-systems r7 routing-instances GOLD protocols vpls site-range 10
set logical-systems r7 routing-instances GOLD protocols vpls no-tunnel-services
set logical-systems r7 routing-instances GOLD protocols vpls site 7 site-identifier 2
set logical-systems r7 routing-instances GOLD protocols vpls site 7 multi-homing
set logical-systems r7 routing-instances GOLD protocols vpls site 7 site-preference 150
set logical-systems r7 routing-instances GOLD protocols vpls site 7 interface ge-1/3/0.100

set logical-systems r8 routing-instances GOLD instance-type vpls
set logical-systems r8 routing-instances GOLD interface ge-1/3/2.100
set logical-systems r8 routing-instances GOLD route-distinguisher 8.8.8.8:1
set logical-systems r8 routing-instances GOLD vrf-target target:6500:1
set logical-systems r8 routing-instances GOLD protocols vpls site-range 10
set logical-systems r8 routing-instances GOLD protocols vpls no-tunnel-services
set logical-systems r8 routing-instances GOLD protocols vpls site 8 site-identifier 2
set logical-systems r8 routing-instances GOLD protocols vpls site 8 multi-homing
#"preference": the higher the better, not like "priority"
set logical-systems r8 routing-instances GOLD protocols vpls site 8 site-preference 200 
set logical-systems r8 routing-instances GOLD protocols vpls site 8 interface ge-1/3/2.100
</code></pre>
<p>optional: tunnel-service</p>
<h3 id="verify-vpls">verify vpls</h3>
<h4 id="r1-vpls-connection">R1 vpls connection</h4>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show vpls connections logical-system r1 
Layer-2 VPN connections:

Legend for connection status (St)   
EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
EM -- encapsulation mismatch     WE -- interface and instance encaps not same
VC-Dn -- Virtual circuit down    NP -- interface hardware not present 
CM -- control-word mismatch      -&gt; -- only outbound connection is up
CN -- circuit not provisioned    &lt;- -- only inbound connection is up
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
LB -- Local site not best-site   RB -- Remote site not best-site
VM -- VLAN ID mismatch

Legend for interface status 
Up -- operational           
Dn -- down

Instance: GOLD
  Local site: 1 (1)
    connection-site           Type  St     Time last up          # Up trans
    2                         rmt   Up     Aug 19 00:55:44 2013           1
    ^
      Remote PE: 10.200.1.8, Negotiated control-word: No
      ^^^^^^^^^^^^^^^^^^^^^
      Incoming label: 262154, Outgoing label: 262145
      Local interface: lsi.152043520, Status: Up, Encapsulation: VPLS
                       ^^^^^^^^^^^^^
        Description: Intf - vpls GOLD local site 1 remote site 2
                                      ^^^^^^^^^^^^^^^^^^^^^^^^^^

[edit]
lab@MX80-NGGWR-02# run show vpls connections logical-system r1 extensive  
Layer-2 VPN connections:

Legend for connection status (St)   
EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
EM -- encapsulation mismatch     WE -- interface and instance encaps not same
VC-Dn -- Virtual circuit down    NP -- interface hardware not present 
CM -- control-word mismatch      -&gt; -- only outbound connection is up
CN -- circuit not provisioned    &lt;- -- only inbound connection is up
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
LB -- Local site not best-site   RB -- Remote site not best-site
VM -- VLAN ID mismatch

Legend for interface status 
Up -- operational           
Dn -- down

Instance: GOLD
  Local site: 1 (1)
    Number of local interfaces: 2
    Number of local interfaces up: 2
    IRB interface present: no
    ge-1/2/3.100       
        Interface flags: VC-Down    #&lt;------("active-interface primary ge-1/2/5.100")
    ge-1/2/5.100       
    lsi.152043520       2         Intf - vpls GOLD local site 1 remote site 2
    Label-base        Offset     Size  Range     Preference
    262153            1          8      8         100   
    connection-site           Type  St     Time last up          # Up trans
    2                         rmt   Up     Aug 19 00:55:44 2013           1
      Remote PE: 10.200.1.8, Negotiated control-word: No
      Incoming label: 262154, Outgoing label: 262145
      Local interface: lsi.152043520, Status: Up, Encapsulation: VPLS
        Description: Intf - vpls GOLD local site 1 remote site 2
    Connection History:
        Aug 19 00:55:44 2013  status update timer  
        Aug 19 00:55:44 2013  loc intf up                lsi.152043520
        Aug 19 00:55:44 2013  PE route changed     
        Aug 19 00:55:44 2013  Out lbl Update                    262145
        Aug 19 00:55:44 2013  In lbl Update                     262154
        Aug 19 00:55:44 2013  loc intf down
</code></pre>
<h4 id="r7-vpls-connection">R7 vpls connection</h4>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show vpls connections logical-system r7              
Layer-2 VPN connections:

Legend for connection status (St)   
EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
EM -- encapsulation mismatch     WE -- interface and instance encaps not same
VC-Dn -- Virtual circuit down    NP -- interface hardware not present 
CM -- control-word mismatch      -&gt; -- only outbound connection is up
CN -- circuit not provisioned    &lt;- -- only inbound connection is up
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
LB -- Local site not best-site   RB -- Remote site not best-site
VM -- VLAN ID mismatch

Legend for interface status 
Up -- operational           
Dn -- down

Instance: GOLD
  Local site: 7 (2)
    connection-site           Type  St     Time last up          # Up trans
    1                         rmt   LN   
    2                         rmt   LN

[edit]
lab@MX80-NGGWR-02# run show vpls connections logical-system r7 extensive  
Layer-2 VPN connections:

Legend for connection status (St)   
EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
EM -- encapsulation mismatch     WE -- interface and instance encaps not same
VC-Dn -- Virtual circuit down    NP -- interface hardware not present 
CM -- control-word mismatch      -&gt; -- only outbound connection is up
CN -- circuit not provisioned    &lt;- -- only inbound connection is up
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
LB -- Local site not best-site   RB -- Remote site not best-site
VM -- VLAN ID mismatch

Legend for interface status 
Up -- operational           
Dn -- down

Instance: GOLD
  Local site: 7 (2)
    Number of local interfaces: 1
    Number of local interfaces up: 0
    IRB interface present: no
    ge-1/3/0.100       
        Interface flags: VC-Down
    Label-base        Offset     Size  Range     Preference
    262145            1          8      8         0     
    connection-site           Type  St     Time last up          # Up trans
    1                         rmt   LN   
    2                         rmt   LN
</code></pre>
<h4 id="r8-vpls-connection">R8 vpls connection</h4>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show vpls connections logical-system r8              
Layer-2 VPN connections:

Legend for connection status (St)   
EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
EM -- encapsulation mismatch     WE -- interface and instance encaps not same
VC-Dn -- Virtual circuit down    NP -- interface hardware not present 
CM -- control-word mismatch      -&gt; -- only outbound connection is up
CN -- circuit not provisioned    &lt;- -- only inbound connection is up
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
LB -- Local site not best-site   RB -- Remote site not best-site
VM -- VLAN ID mismatch

Legend for interface status 
Up -- operational           
Dn -- down

Instance: GOLD
  Local site: 8 (2)
    connection-site           Type  St     Time last up          # Up trans
    1                         rmt   Up     Aug 19 00:55:44 2013           1
      Remote PE: 10.200.1.1, Negotiated control-word: No
      Incoming label: 262145, Outgoing label: 262154
      Local interface: lsi.168820736, Status: Up, Encapsulation: VPLS
        Description: Intf - vpls GOLD local site 2 remote site 1
    2                         rmt   RN

[edit]
lab@MX80-NGGWR-02# run show vpls connections logical-system r8 extensive  
Layer-2 VPN connections:

Legend for connection status (St)   
EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
EM -- encapsulation mismatch     WE -- interface and instance encaps not same
VC-Dn -- Virtual circuit down    NP -- interface hardware not present 
CM -- control-word mismatch      -&gt; -- only outbound connection is up
CN -- circuit not provisioned    &lt;- -- only inbound connection is up
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
LB -- Local site not best-site   RB -- Remote site not best-site
VM -- VLAN ID mismatch

Legend for interface status 
Up -- operational           
Dn -- down

Instance: GOLD
  Local site: 8 (2)
    Number of local interfaces: 1
    Number of local interfaces up: 1
    IRB interface present: no
    ge-1/3/2.100       
    lsi.168820736       1         Intf - vpls GOLD local site 2 remote site 1
    Label-base        Offset     Size  Range     Preference
    262145            1          8      8         200   
    connection-site           Type  St     Time last up          # Up trans
    1                         rmt   Up     Aug 19 00:55:44 2013           1
      Remote PE: 10.200.1.1, Negotiated control-word: No
      Incoming label: 262145, Outgoing label: 262154
      Local interface: lsi.168820736, Status: Up, Encapsulation: VPLS
        Description: Intf - vpls GOLD local site 2 remote site 1
    Connection History:
        Aug 19 00:55:44 2013  status update timer  
        Aug 19 00:55:44 2013  loc intf up                lsi.168820736
        Aug 19 00:55:44 2013  PE route changed     
        Aug 19 00:55:44 2013  Out lbl Update                    262154
        Aug 19 00:55:44 2013  In lbl Update                     262145
        Aug 19 00:55:44 2013  loc intf down        
    2                         rmt   RN
</code></pre>
<h4 id="vpls-forwarding-table-no-traffic">vpls forwarding-table (no traffic)</h4>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route forwarding-table family vpls  
Logical system: r8
Routing table: GOLD.vpls
VPLS:
Destination        Type RtRef Next hop           Type Index NhRef Netif
default            perm     0                    dscd  1829     1
lsi.168820736      intf     0                    indr 1048689     4
                              100.0.68.1        Push 262154, Push 299888(top)  1640     2 ge-1/2/2.608
0x3000d/51         user     0                    comp  2582     2
ge-1/3/2.100       intf     0                    ucst  1643     4 ge-1/3/2.100
0x3000b/51         user     0                    comp  1906     2
0x3000a/51         user     0                    comp  1901     2

Logical system: r7
Routing table: GOLD.vpls
VPLS:
Destination        Type RtRef Next hop           Type Index NhRef Netif
default            perm     0                    dscd  1644     1
ge-1/3/0.100       intf     0                    ucst  2496     4 ge-1/3/0.100
0x30008/51         user     0                    comp  2511     2
0x30009/51         user     0                    comp  2500     2

Logical system: r1
Routing table: GOLD.vpls
VPLS:
Destination        Type RtRef Next hop           Type Index NhRef Netif
default            perm     0                    dscd  1215     1
lsi.152043520      intf     0                    indr 1048688     4
                              100.0.12.2        Push 262145, Push 299808, Push 299872(top)  1637     2 ge-1/2/1.102
0x3000c/51         user     0                    comp  2552     2
ge-1/2/5.100       intf     0                    ucst  1636     4 ge-1/2/5.100
0x30007/51         user     0                    comp  2569     2
0x30006/51         user     0                    comp  2536     2
</code></pre>
<h4 id="vpls-forwarding-table-with-traffic">vpls forwarding table (with traffic)</h4>
<pre><code>[edit]
lab@MX80-NGGWR-02# run ping 100.100.1.2 logical-system r0 routing-instance vce1 source 100.100.1.1             
PING 100.100.1.2 (100.100.1.2): 56 data bytes
^C
--- 100.100.1.2 ping statistics ---
2 packets transmitted, 0 packets received, 100% packet loss

[edit]
lab@MX80-NGGWR-02# run ping 100.100.2.2 logical-system r0 routing-instance vce1 source 100.100.2.1                        
PING 100.100.2.2 (100.100.2.2): 56 data bytes
64 bytes from 100.100.2.2: icmp_seq=0 ttl=64 time=1.246 ms
64 bytes from 100.100.2.2: icmp_seq=1 ttl=64 time=0.644 ms
64 bytes from 100.100.2.2: icmp_seq=2 ttl=64 time=0.651 ms
^C
--- 100.100.2.2 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.644/0.847/1.246/0.282 ms

[edit]
lab@MX80-NGGWR-02# run show route forwarding-table family vpls                                        
Logical system: r8
Routing table: GOLD.vpls
VPLS:
Destination        Type RtRef Next hop           Type Index NhRef Netif
default            perm     0                    dscd  1829     1
lsi.168820736      intf     0                    indr 1048689     5
                              100.0.68.1        Push 262154, Push 299888(top)  1640     2 ge-1/2/2.608
0x3000d/51         user     0                    comp  2582     2
f8:c0:01:18:91:96/48 user     0                  indr 1048689     5         #&lt;------
                              100.0.68.1        Push 262154, Push 299888(top)  1640     2 ge-1/2/2.608
f8:c0:01:18:91:ab/48 user     0                  ucst  1643     5 ge-1/3/2.100      #&lt;------
ge-1/3/2.100       intf     0                    ucst  1643     5 ge-1/3/2.100
0x3000b/51         user     0                    comp  1906     2
0x3000a/51         user     0                    comp  1901     2

Logical system: r7
Routing table: GOLD.vpls
VPLS:
Destination        Type RtRef Next hop           Type Index NhRef Netif
default            perm     0                    dscd  1644     1
ge-1/3/0.100       intf     0                    ucst  2496     4 ge-1/3/0.100
0x30008/51         user     0                    comp  2511     2
0x30009/51         user     0                    comp  2500     2

Logical system: r1
Routing table: GOLD.vpls
VPLS:
Destination        Type RtRef Next hop           Type Index NhRef Netif
default            perm     0                    dscd  1215     1
lsi.152043520      intf     0                    indr 1048688     5
                              100.0.12.2        Push 262145, Push 299808, Push 299872(top)  1637     2 ge-1/2/1.102
0x3000c/51         user     0                    comp  2552     2
f8:c0:01:18:91:96/48 user     0                  ucst  1636     5 ge-1/2/5.100      #&lt;------
f8:c0:01:18:91:ab/48 user     0                  indr 1048688     5         #&lt;------
                              100.0.12.2        Push 262145, Push 299808, Push 299872(top)  1637     2 ge-1/2/1.102
ge-1/2/5.100       intf     0                    ucst  1636     5 ge-1/2/5.100
0x30007/51         user     0                    comp  2569     2
0x30006/51         user     0                    comp  2536     2
</code></pre>
<h4 id="bridge-bridge-domain-per-instance">bridge bridge domain (per-instance)</h4>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show bridge domain instance GOLD

Routing instance        Bridge domain            VLAN ID     Interfaces
GOLD                    __GOLD__                 NA       
                                                     ge-1/2/3.100
                                                     ge-1/2/5.100
                                                     lsi.152043520
GOLD                    __GOLD__                 NA       
                                                     ge-1/3/0.100
GOLD                    __GOLD__                 NA       
                                                     ge-1/3/2.100
                                                     lsi.168820736
</code></pre>
<h4 id="bridge-interface-statistics">bridge interface statistics</h4>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show bridge statistics logical-system r1 
   Local interface: lsi.152043520, Index: 512
     Current MAC count:                     1
   Local interface: ge-1/2/5.100, Index: 335
     Broadcast packets:                     4
     Broadcast bytes  :                   240
     Multicast packets:                     0
     Multicast bytes  :                     0
     Flooded packets  :                     1
     Flooded bytes    :                   102
     Unicast packets  :                    13
     Unicast bytes    :                  1284
     Current MAC count:                     1 (Limit 500)
   Local interface: ge-1/2/3.100, Index: 465
     Broadcast packets:                     0
     Broadcast bytes  :                     0
     Multicast packets:                     0
     Multicast bytes  :                     0
     Flooded packets  :                     0
     Flooded bytes    :                     0
     Unicast packets  :                     0
     Unicast bytes    :                     0
     Current MAC count:                     0 (Limit 500)

[edit]
lab@MX80-NGGWR-02# run show bridge statistics logical-system r7    
   Local interface: ge-1/3/0.100, Index: 498
     Broadcast packets:                     5
     Broadcast bytes  :                   300
     Multicast packets:                     0
     Multicast bytes  :                     0
     Flooded packets  :                     0
     Flooded bytes    :                     0
     Unicast packets  :                     0
     Unicast bytes    :                     0
     Current MAC count:                     0 (Limit 1024)

[edit]
lab@MX80-NGGWR-02# run show bridge statistics logical-system r8    
   Local interface: lsi.168820736, Index: 535
     Current MAC count:                     1
   Local interface: ge-1/3/2.100, Index: 500
     Broadcast packets:                     1
     Broadcast bytes  :                    60
     Multicast packets:                     0
     Multicast bytes  :                     0
     Flooded packets  :                     0
     Flooded bytes    :                     0
     Unicast packets  :                    13
     Unicast bytes    :                  1158
     Current MAC count:                     1 (Limit 1024)
</code></pre>
<h3 id="config-vpls-firewall-policer">config: vpls firewall policer</h3>
<pre><code>set logical-systems r1 firewall policer 5m if-exceeding bandwidth-limit 5m
set logical-systems r1 firewall policer 5m if-exceeding burst-size-limit 15k
set logical-systems r1 firewall policer 5m then discard

set logical-systems r1 firewall family vpls filter vpls term 1 from traffic-type broadcast
set logical-systems r1 firewall family vpls filter vpls term 1 from traffic-type multicast
set logical-systems r1 firewall family vpls filter vpls term 1 then policer 5m
set logical-systems r1 firewall family vpls filter vpls term 2 then accept

set logical-systems r1 interfaces ge-1/2/3 unit 100 encapsulation vlan-vpls
set logical-systems r1 interfaces ge-1/2/3 unit 100 family vpls filter input vpls
set logical-systems r1 interfaces ge-1/2/5 unit 100 encapsulation vlan-vpls
set logical-systems r1 interfaces ge-1/2/5 unit 100 family vpls filter input vpls
</code></pre>
<h3 id="tip-vpls-link-redundency-issue">TIP: vpls link redundency issue</h3>
<p>by default system will disable one link. if the test ping happens to arrive
from the disabled link, ping won't succeed </p>
<h3 id="tip-encapsulation-extended-vlan-vpls-and-flexible-ethernet-services">TIP: <code>encapsulation extended-vlan-vpls</code> and <code>flexible-ethernet-services</code></h3>
<p>Gigabit Ethernet, 4-port Fast Ethernet, MX Series router Gigabit Ethernet,
Tri-Rate Ethernet copper, 10-Gigabit Ethernet, and aggregated Ethernet
interfaces with VLAN tagging enabled can use extended VLAN CCC or VLAN VPLS,
which allow 802.1Q tagging.</p>
<p>flexible-ethernet-services—For Gigabit Ethernet IQ interfaces and Gigabit
Ethernet PICs with small form-factor pluggable transceivers (SFPs) (except the
10-port Gigabit Ethernet PIC and the built-in Gigabit Ethernet port on the M7i
router), use flexible Ethernet services encapsulation when you want to
configure multiple per-unit Ethernet encapsulations. Aggregated Ethernet
bundles can use this encapsulation type. This encapsulation type allows you to
configure any combination of route, TCC, CCC, Layer 2 virtual private networks
(VPNs), and VPLS encapsulations on a single physical port. If you configure
flexible Ethernet services encapsulation on the physical interface, VLAN IDs
from 1 through 511 are no longer reserved for normal VLANs.</p>
<h3 id="2-commit-errors">2 commit errors</h3>
<pre><code>[edit logical-systems r1 interfaces ge-1/2/3]
  'unit 100'
     Link encapsulation type is not valid for device type
error: configuration check-out failed
</code></pre>
<p>config encap flexible-ethernet-service resolve it</p>
<pre><code>lab@MX80-NGGWR-02# set interfaces ge-1/2/3 encapsulation flexible-ethernet-services

[edit logical-systems r1 interfaces ge-1/2/3 unit 100]
  'family'
     Only the VPLS family is allowed on VPLS interfaces
error: configuration check-out failed
</code></pre>
<h2 id="vpn-part-b">VPN (PART B)</h2>
<h3 id="vpn-internet-access-task">VPN internet access task</h3>
<p>VPN must have internet access, and 
<em> the internet gateway is R1, 
</em> you can’t define any static route in VRF instance, 
<em> you can only define 1 static route on PE，
</em> rib-group not allowed under VRF.</p>
<p>solution 1:</p>
<ul>
<li>
<p>R1-global: suck all downward (from Internet to VPN) traffic to R1-global</p>
<ul>
<li>aggr. VPN routes</li>
<li>adv aggr.ed VPN routes via BGP</li>
</ul>
</li>
<li>
<p>R1-global: direct sucked traffic into VRF, who already knows how to reach all VPN site. downward done.</p>
<ul>
<li>static route to VPN aggr. routes via next-table GREEN.inet.0</li>
</ul>
</li>
<li>
<p>R1-vrf: suck all upward (to Internet) traffic to local R1-VRF</p>
<ul>
<li>vrf adv default routes to all VPN sites</li>
</ul>
</li>
<li>
<p>R1-global: leak full Internet table into R1-vrf, making R1-VRF knows how to reach Internet, upward done.</p>
<ul>
<li>rib-group, copy inet.0 into GREEN.inet.0</li>
</ul>
</li>
</ul>
<h3 id="config-basic-vpn">config: basic VPN</h3>
<h4 id="r1">R1:</h4>
<pre><code>set logical-systems r1 routing-instances GREEN instance-type vrf
set logical-systems r1 routing-instances GREEN interface ge-1/2/1.611
set logical-systems r1 routing-instances GREEN interface lo0.111
set logical-systems r1 routing-instances GREEN route-distinguisher 10.200.1.1:1
set logical-systems r1 routing-instances GREEN vrf-import vrf-imp
set logical-systems r1 routing-instances GREEN vrf-export vrf-exp
set logical-systems r1 routing-instances GREEN vrf-table-label
set logical-systems r1 routing-instances GREEN protocols ospf area 0.0.0.0 interface ge-1/2/1.611

set logical-systems r1 policy-options policy-statement vrf-imp term 1 from protocol bgp
set logical-systems r1 policy-options policy-statement vrf-imp term 1 from community GREEN
set logical-systems r1 policy-options policy-statement vrf-imp term 1 then accept

set logical-systems r1 policy-options policy-statement vrf-exp term 1 from protocol ospf    #&lt;------OSPF
set logical-systems r1 policy-options policy-statement vrf-exp term 1 then community add GREEN
set logical-systems r1 policy-options policy-statement vrf-exp term 1 then accept
set logical-systems r1 policy-options policy-statement vrf-exp term 2 from protocol direct  #&lt;------direct
set logical-systems r1 policy-options policy-statement vrf-exp term 2 then community add GREEN
set logical-systems r1 policy-options policy-statement vrf-exp term 2 then accept
set logical-systems r1 policy-options community GREEN members target:2:65000
</code></pre>
<h4 id="r4">R4:</h4>
<pre><code>set logical-systems r4 routing-instances GREEN instance-type vrf
set logical-systems r4 routing-instances GREEN interface ge-1/2/1.642
set logical-systems r4 routing-instances GREEN interface ge-1/2/1.643
set logical-systems r4 routing-instances GREEN interface lo0.444
set logical-systems r4 routing-instances GREEN route-distinguisher 10.200.1.4:1
set logical-systems r4 routing-instances GREEN vrf-import vrf-imp
set logical-systems r4 routing-instances GREEN vrf-export vrf-exp
set logical-systems r4 routing-instances GREEN vrf-table-label
set logical-systems r4 routing-instances GREEN protocols bgp group to-ce3 neighbor 200.6.43.2 family inet unicast
set logical-systems r4 routing-instances GREEN protocols bgp group to-ce3 neighbor 200.6.43.2 peer-as 65000
set logical-systems r4 routing-instances GREEN protocols bgp group to-ce3 neighbor 200.6.43.2 as-override
set logical-systems r4 routing-instances GREEN protocols ospf area 0.0.0.0 interface ge-1/2/1.642

set logical-systems r4 policy-options policy-statement vrf-imp term 1 from protocol bgp
set logical-systems r4 policy-options policy-statement vrf-imp term 1 from community GREEN
set logical-systems r4 policy-options policy-statement vrf-imp term 1 then accept

set logical-systems r4 policy-options policy-statement vrf-exp term 1 from protocol ospf    #&lt;------OSPF
set logical-systems r4 policy-options policy-statement vrf-exp term 1 then community add GREEN
set logical-systems r4 policy-options policy-statement vrf-exp term 1 then community add ce2
set logical-systems r4 policy-options policy-statement vrf-exp term 1 then accept
set logical-systems r4 policy-options policy-statement vrf-exp term 2 from protocol direct  #&lt;------direct link1
set logical-systems r4 policy-options policy-statement vrf-exp term 2 from route-filter 200.6.42.0/24 exact
set logical-systems r4 policy-options policy-statement vrf-exp term 2 then community add GREEN
set logical-systems r4 policy-options policy-statement vrf-exp term 2 then community add ce2
set logical-systems r4 policy-options policy-statement vrf-exp term 2 then accept
set logical-systems r4 policy-options policy-statement vrf-exp term 3 from protocol bgp     #&lt;------BGP
set logical-systems r4 policy-options policy-statement vrf-exp term 3 then community add GREEN
set logical-systems r4 policy-options policy-statement vrf-exp term 3 then community add ce3
set logical-systems r4 policy-options policy-statement vrf-exp term 3 then accept
set logical-systems r4 policy-options policy-statement vrf-exp term 4 from protocol direct  #&lt;------direct link2
set logical-systems r4 policy-options policy-statement vrf-exp term 4 from route-filter 200.6.43.0/24 exact
set logical-systems r4 policy-options policy-statement vrf-exp term 4 then community add GREEN
set logical-systems r4 policy-options policy-statement vrf-exp term 4 then community add ce3
set logical-systems r4 policy-options policy-statement vrf-exp term 4 then accept
set logical-systems r4 policy-options policy-statement vrf-exp term 5 from protocol direct  #&lt;------optional(no need in exam)
set logical-systems r4 policy-options policy-statement vrf-exp term 5 from route-filter 4.4.4.4/32 exact
set logical-systems r4 policy-options policy-statement vrf-exp term 5 then community add GREEN
set logical-systems r4 policy-options policy-statement vrf-exp term 5 then community add ce2
set logical-systems r4 policy-options policy-statement vrf-exp term 5 then accept
set logical-systems r4 policy-options community GREEN members target:2:65000
</code></pre>
<h4 id="r8">R8:</h4>
<pre><code>set logical-systems r8 routing-instances GREEN instance-type vrf
set logical-systems r8 routing-instances GREEN interface ge-1/2/1.684
set logical-systems r8 routing-instances GREEN interface ge-1/2/1.685
set logical-systems r8 routing-instances GREEN interface lo0.888
set logical-systems r8 routing-instances GREEN route-distinguisher 10.200.1.8:1
set logical-systems r8 routing-instances GREEN vrf-import vrf-imp
set logical-systems r8 routing-instances GREEN vrf-export vrf-exp
set logical-systems r8 routing-instances GREEN vrf-table-label
set logical-systems r8 routing-instances GREEN protocols bgp group to-ce4-ce5 type external
set logical-systems r8 routing-instances GREEN protocols bgp group to-ce4-ce5 family inet unicast
set logical-systems r8 routing-instances GREEN protocols bgp group to-ce4-ce5 peer-as 65000
set logical-systems r8 routing-instances GREEN protocols bgp group to-ce4-ce5 as-override

set logical-systems r8 policy-options policy-statement vrf-imp term 1 from protocol bgp
set logical-systems r8 policy-options policy-statement vrf-imp term 1 from community GREEN
set logical-systems r8 policy-options policy-statement vrf-imp term 1 then accept

set logical-systems r8 policy-options policy-statement vrf-exp term 1 from protocol bgp     #&lt;------BGP
set logical-systems r8 policy-options policy-statement vrf-exp term 1 then community add GREEN
set logical-systems r8 policy-options policy-statement vrf-exp term 1 then accept
set logical-systems r8 policy-options policy-statement vrf-exp term 2 from protocol direct  #&lt;------direct
set logical-systems r8 policy-options policy-statement vrf-exp term 2 then community add GREEN
set logical-systems r8 policy-options policy-statement vrf-exp term 2 then accept
set logical-systems r8 policy-options community GREEN members target:2:65000
</code></pre>
<h3 id="config-vpn-policy">config: VPN policy</h3>
<pre><code>set logical-systems r1 policy-options policy-statement vrf-exp-ospf-from-bgp term 1 from protocol bgp
set logical-systems r1 policy-options policy-statement vrf-exp-ospf-from-bgp term 1 from community GREEN    #&lt;------optional
set logical-systems r1 policy-options policy-statement vrf-exp-ospf-from-bgp term 1 then accept
set logical-systems r1 routing-instances GREEN protocols ospf export vrf-exp-ospf-from-bgp

set logical-systems r4 policy-options policy-statement vrf-exp-bgp-from-ospf term 1 from protocol ospf
set logical-systems r4 policy-options policy-statement vrf-exp-bgp-from-ospf term 1 then accept
set logical-systems r4 policy-options policy-statement vrf-exp-bgp-from-ospf term 2 from protocol direct
set logical-systems r4 policy-options policy-statement vrf-exp-bgp-from-ospf term 2 from route-filter 200.6.42.0/24 exact
set logical-systems r4 policy-options policy-statement vrf-exp-bgp-from-ospf term 2 then accept

set logical-systems r4 policy-options policy-statement vrf-exp-ospf-from-bgp term 1 from protocol bgp
set logical-systems r4 policy-options policy-statement vrf-exp-ospf-from-bgp term 1 from community GREEN    #&lt;------optional
set logical-systems r4 policy-options policy-statement vrf-exp-ospf-from-bgp term 1 then accept     
set logical-systems r4 policy-options policy-statement vrf-exp-ospf-from-bgp term 2 then reject

set logical-systems r4 routing-instances GREEN protocols bgp export vrf-exp-bgp-from-ospf
set logical-systems r4 routing-instances GREEN protocols ospf export vrf-exp-ospf-from-bgp
</code></pre>
<h3 id="verify-bgpospf-connections">verify bgp/ospf connections</h3>
<p>core MP-BGP: from RR: R2/3: all neighbor established, with correct family</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show bgp summary logical-system r2 
Groups: 7 Peers: 17 Down peers: 0
Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
inet.0               
                      33         15          0          0          0          0
inet.3               
                       8          3          0          0          0          0
inet6.0              
                      43         24          0          0          0          0
bgp.l3vpn.0          
                      16         16          0          0          0          0
bgp.l2vpn.0          
                       0          0          0          0          0          0
Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
10.200.1.1       4012345678       2803       2753       0       0    21:15:05 Establ        #&lt;------
  bgp.l3vpn.0: 5/5/5/0
10.200.1.3       4012345678       2748       2742       0       0    21:15:10 Establ        #&lt;------
  bgp.l2vpn.0: 0/0/0/0
10.200.1.4       4012345678       2795       2747       0       0    21:15:08 Establ        #&lt;------
  bgp.l3vpn.0: 6/6/6/0
10.200.1.5       4012345678       2821       2752       0       0    21:14:58 Establ
  inet.0: 10/15/14/0
  inet.3: 3/4/4/0
  inet6.0: 18/19/19/0
10.200.1.6       4012345678       2823       2753       0       0    21:15:08 Establ
  inet.0: 0/13/12/0
  inet.3: 0/4/4/0
  inet6.0: 1/19/19/0
10.200.1.7       4012345678       2797       2755       0       0    21:14:45 Establ        #&lt;------
  bgp.l3vpn.0: 0/0/0/0
10.200.1.8       4012345678       2790       2753       0       0    21:14:37 Establ        #&lt;------
  bgp.l3vpn.0: 5/5/5/0
100.2.11.2             1000       2715       2756       0       0    21:15:21 Establ
  inet.0: 1/1/1/0
100.2.12.2             2000       2716       2753       0       0    21:15:12 Establ
  inet.0: 1/1/1/0
100.2.13.2             3000       2715       2754       0       0    21:15:16 Establ
  inet.0: 1/1/1/0
100.2.21.2             1100       2716       2759       0       0    21:15:12 Establ
  inet.0: 1/1/1/0
100.2.22.2             1200       2715       2761       0       0    21:15:12 Establ
  inet.0: 1/1/1/0
::100.2.11.2           1000       2715       2751       0       0    21:14:51 Establ
  inet6.0: 1/1/1/0
::100.2.12.2           2000       2716       2752       0       0    21:14:59 Establ
  inet6.0: 1/1/1/0
::100.2.13.2           3000       2715       2754       0       0    21:15:04 Establ
  inet6.0: 1/1/1/0
::100.2.21.2           1100       2715       2757       0       0    21:15:04 Establ
  inet6.0: 1/1/1/0
::100.2.22.2           1200       2715       2756       0       0    21:15:04 Establ
  inet6.0: 1/1/1/0
</code></pre>
<p>VRF-CE:</p>
<pre><code>lab@MX80-NGGWR-02# run show ospf neighbor logical-system r1 instance GREEN 
Address          Interface              State     ID               Pri  Dead
200.6.11.2       ge-1/2/1.611           Full      20.20.1.11       128    39

[edit]
lab@MX80-NGGWR-02# run show ospf neighbor logical-system r4 instance GREEN 
Address          Interface              State     ID               Pri  Dead
200.6.42.2       ge-1/2/1.642           Full      20.20.1.22       128    37

[edit]
lab@MX80-NGGWR-02# run show bgp summary logical-system r4 instance GREEN 
Groups: 1 Peers: 1 Down peers: 0
Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
GREEN.inet.0         
                      21         10          0          0          0          0
GREEN.mdt.0          
                       0          0          0          0          0          0
Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
200.6.43.2            65000       2719       2804       0       0    21:17:13 Establ        #&lt;------
  GREEN.inet.0: 1/1/1/0

[edit]
lab@MX80-NGGWR-02# run show bgp summary logical-system r8 instance GREEN    
Groups: 2 Peers: 2 Down peers: 0
Table          Tot Paths  Act Paths Suppressed    History Damp State    Pending
GREEN.inet.0         
                      24         12          0          0          0          0
GREEN.mdt.0          
                       0          0          0          0          0          0
Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...
200.6.84.2            65000       2728       2814       0       0    21:20:40 Establ        #&lt;------
  GREEN.inet.0: 1/1/1/0
200.6.85.2            65000       2728       2814       0       0    21:20:38 Establ        #&lt;------
  GREEN.inet.0: 1/1/1/0
</code></pre>
<h3 id="verify-vpn-table">verify: VPN table</h3>
<h4 id="vrf-r1">VRF: R1</h4>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route logical-system r1 table GREEN.inet.0

GREEN.inet.0: 17 destinations, 32 routes (17 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

0.0.0.0/0          *[Static/5] 21:59:08
                      to table inet.0
1.1.1.1/32         *[Direct/0] 21:58:59
                    &gt; via lo0.111
4.4.4.4/32         *[BGP/170] 21:58:12, localpref 100, from 10.200.1.2      #&lt;------R4 VRF lo0
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
                    [BGP/170] 21:58:28, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
8.8.8.8/32         *[BGP/170] 21:58:12, localpref 100, from 10.200.1.2      #&lt;------R8 VRF lo0
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 21:58:26, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
11.22.0.0/24       *[OSPF/10] 21:57:57, metric 51                           #&lt;------CE1-CE2 link
                    &gt; to 200.6.11.2 via ge-1/2/1.611
                    [BGP/170] 21:58:07, MED 51, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
                    [BGP/170] 21:58:07, MED 51, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
20.20.1.11/32      *[OSPF/150] 21:57:57, metric 0, tag 0                    #&lt;------CE1-5 lo0
                    &gt; to 200.6.11.2 via ge-1/2/1.611
20.20.1.22/32      *[BGP/170] 21:58:07, MED 1, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
                    [BGP/170] 21:58:07, MED 1, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
20.20.1.33/32      *[BGP/170] 21:58:12, localpref 100, from 10.200.1.2
                      AS path: 65000 I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
                    [BGP/170] 21:58:28, localpref 100, from 10.200.1.3
                      AS path: 65000 I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
20.20.1.44/32      *[BGP/170] 21:58:12, localpref 100, from 10.200.1.2
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 21:58:26, localpref 100, from 10.200.1.3
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
20.20.1.55/32      *[BGP/170] 21:58:12, localpref 100, from 10.200.1.2
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 21:58:26, localpref 100, from 10.200.1.3
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
200.6.11.0/24      *[Direct/0] 21:58:59
                    &gt; via ge-1/2/1.611
200.6.11.1/32      *[Local/0] 21:58:59
                      Local via ge-1/2/1.611
200.6.42.0/24      *[BGP/170] 21:58:12, localpref 100, from 10.200.1.2      #&lt;------remote PE-CE links
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
                    [BGP/170] 21:58:28, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
200.6.43.0/24      *[BGP/170] 21:58:12, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
                    [BGP/170] 21:58:28, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
200.6.84.0/24      *[BGP/170] 21:58:12, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 21:58:26, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
200.6.85.0/24      *[BGP/170] 21:58:12, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
                    [BGP/170] 21:58:26, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r6
224.0.0.5/32       *[OSPF/10] 21:59:15, metric 1
                      MultiRecv
</code></pre>
<h4 id="vrf-r4">VRF: R4</h4>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route logical-system r4 table GREEN.inet.0

GREEN.inet.0: 18 destinations, 32 routes (18 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

0.0.0.0/0          *[BGP/170] 22:03:28, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.1 via ge-1/2/2.204, label-switched-path r4-r1
                    [BGP/170] 22:03:44, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.1 via ge-1/2/2.204, label-switched-path r4-r1
1.1.1.1/32         *[BGP/170] 22:03:28, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.1 via ge-1/2/2.204, label-switched-path r4-r1
                    [BGP/170] 22:03:44, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.1 via ge-1/2/2.204, label-switched-path r4-r1
4.4.4.4/32         *[Direct/0] 22:04:21
                    &gt; via lo0.444
8.8.8.8/32         *[BGP/170] 22:03:28, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.46.2 via ge-1/2/1.406, label-switched-path r4-r6
                    [BGP/170] 22:03:42, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.46.2 via ge-1/2/1.406, label-switched-path r4-r6
11.22.0.0/24       *[OSPF/10] 22:03:23, metric 51
                    &gt; to 200.6.42.2 via ge-1/2/1.642
                    [BGP/170] 22:03:13, MED 51, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.1 via ge-1/2/2.204, label-switched-path r4-r1
                    [BGP/170] 22:03:13, MED 51, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.1 via ge-1/2/2.204, label-switched-path r4-r1
20.20.1.11/32      *[BGP/170] 22:03:13, MED 0, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.1 via ge-1/2/2.204, label-switched-path r4-r1
                    [BGP/170] 22:03:13, MED 0, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.1 via ge-1/2/2.204, label-switched-path r4-r1
20.20.1.22/32      *[OSPF/10] 22:03:23, metric 1
                    &gt; to 200.6.42.2 via ge-1/2/1.642
20.20.1.33/32      *[BGP/170] 22:04:01, localpref 100
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 200.6.43.2 via ge-1/2/1.643
20.20.1.44/32      *[BGP/170] 22:03:28, localpref 100, from 10.200.1.2
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 100.0.46.2 via ge-1/2/1.406, label-switched-path r4-r6
                    [BGP/170] 22:03:42, localpref 100, from 10.200.1.3
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 100.0.46.2 via ge-1/2/1.406, label-switched-path r4-r6
20.20.1.55/32      *[BGP/170] 22:03:28, localpref 100, from 10.200.1.2
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 100.0.46.2 via ge-1/2/1.406, label-switched-path r4-r6
                    [BGP/170] 22:03:42, localpref 100, from 10.200.1.3
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 100.0.46.2 via ge-1/2/1.406, label-switched-path r4-r6
200.6.11.0/24      *[BGP/170] 22:03:28, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.1 via ge-1/2/2.204, label-switched-path r4-r1
                    [BGP/170] 22:03:44, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.24.1 via ge-1/2/2.204, label-switched-path r4-r1
200.6.42.0/24      *[Direct/0] 22:04:21
                    &gt; via ge-1/2/1.642
200.6.42.1/32      *[Local/0] 22:04:21
                      Local via ge-1/2/1.642
200.6.43.0/24      *[Direct/0] 22:04:21
                    &gt; via ge-1/2/1.643
200.6.43.1/32      *[Local/0] 22:04:21
                      Local via ge-1/2/1.643
200.6.84.0/24      *[BGP/170] 22:03:28, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.46.2 via ge-1/2/1.406, label-switched-path r4-r6
                    [BGP/170] 22:03:42, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.46.2 via ge-1/2/1.406, label-switched-path r4-r6
200.6.85.0/24      *[BGP/170] 22:03:28, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.46.2 via ge-1/2/1.406, label-switched-path r4-r6
                    [BGP/170] 22:03:42, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 100.0.46.2 via ge-1/2/1.406, label-switched-path r4-r6
224.0.0.5/32       *[OSPF/10] 22:04:31, metric 1
                      MultiRecv
</code></pre>
<h3 id="verify-solution1-data-plane-e2e-pingtraceroute">verify solution1 data plane: e2e ping/traceroute</h3>
<pre><code>run ping 20.20.1.22 logical-system r0 routing-instance vpn1 source 20.20.1.11 count 3 rapid
run ping 20.20.1.33 logical-system r0 routing-instance vpn1 source 20.20.1.11 count 3 rapid   
run ping 20.20.1.44 logical-system r0 routing-instance vpn1 source 20.20.1.11 count 3 rapid   
run ping 20.20.1.55 logical-system r0 routing-instance vpn1 source 20.20.1.11 count 3 rapid   
run ping 20.20.1.11 logical-system r0 routing-instance vpn2 source 20.20.1.22 count 3 rapid   
run ping 20.20.1.33 logical-system r0 routing-instance vpn2 source 20.20.1.22 count 3 rapid   
run ping 20.20.1.44 logical-system r0 routing-instance vpn2 source 20.20.1.22 count 3 rapid   
run ping 20.20.1.55 logical-system r0 routing-instance vpn2 source 20.20.1.22 count 3 rapid   
run ping 20.20.1.11 logical-system r0 routing-instance vpn3 source 20.20.1.33 count 3 rapid   
run ping 20.20.1.22 logical-system r0 routing-instance vpn3 source 20.20.1.33 count 3 rapid   
run ping 20.20.1.44 logical-system r0 routing-instance vpn3 source 20.20.1.33 count 3 rapid   
run ping 20.20.1.55 logical-system r0 routing-instance vpn3 source 20.20.1.33 count 3 rapid

run traceroute 20.20.1.22 logical-system r0 routing-instance vpn1 source 20.20.1.11 
run traceroute 20.20.1.33 logical-system r0 routing-instance vpn1 source 20.20.1.11 
run traceroute 20.20.1.44 logical-system r0 routing-instance vpn1 source 20.20.1.11 
run traceroute 20.20.1.55 logical-system r0 routing-instance vpn1 source 20.20.1.11 
run traceroute 20.20.1.11 logical-system r0 routing-instance vpn2 source 20.20.1.22    
run traceroute 20.20.1.33 logical-system r0 routing-instance vpn2 source 20.20.1.22    
run traceroute 20.20.1.44 logical-system r0 routing-instance vpn2 source 20.20.1.22    
run traceroute 20.20.1.55 logical-system r0 routing-instance vpn2 source 20.20.1.22    
run traceroute 20.20.1.11 logical-system r0 routing-instance vpn3 source 20.20.1.33    
run traceroute 20.20.1.22 logical-system r0 routing-instance vpn3 source 20.20.1.33    
run traceroute 20.20.1.44 logical-system r0 routing-instance vpn3 source 20.20.1.33    
run traceroute 20.20.1.55 logical-system r0 routing-instance vpn3 source 20.20.1.33

[edit]
lab@MX80-NGGWR-02# run ping 20.20.1.22 logical-system r0 routing-instance vpn1 source 20.20.1.11  
PING 20.20.1.22 (20.20.1.22): 56 data bytes
64 bytes from 20.20.1.22: icmp_seq=0 ttl=61 time=0.686 ms
64 bytes from 20.20.1.22: icmp_seq=1 ttl=61 time=0.599 ms
^C
--- 20.20.1.22 ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.599/0.643/0.686/0.043 ms

[edit]
lab@MX80-NGGWR-02# run ping 20.20.1.33 logical-system r0 routing-instance vpn1 source 20.20.1.11 
PING 20.20.1.33 (20.20.1.33): 56 data bytes
64 bytes from 20.20.1.33: icmp_seq=0 ttl=61 time=0.758 ms
64 bytes from 20.20.1.33: icmp_seq=1 ttl=61 time=0.604 ms
^C
--- 20.20.1.33 ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.604/0.681/0.758/0.077 ms

[edit]
lab@MX80-NGGWR-02# run ping 20.20.1.44 logical-system r0 routing-instance vpn1 source 20.20.1.11 
PING 20.20.1.44 (20.20.1.44): 56 data bytes
64 bytes from 20.20.1.44: icmp_seq=0 ttl=60 time=0.727 ms
^C
--- 20.20.1.44 ping statistics ---
1 packets transmitted, 1 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.727/0.727/0.727/0.000 ms

[edit]
lab@MX80-NGGWR-02# run ping 20.20.1.55 logical-system r0 routing-instance vpn1 source 20.20.1.11 
PING 20.20.1.55 (20.20.1.55): 56 data bytes
64 bytes from 20.20.1.55: icmp_seq=0 ttl=60 time=0.753 ms
^C
--- 20.20.1.55 ping statistics ---
1 packets transmitted, 1 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.753/0.753/0.753/0.000 ms

[edit]
lab@MX80-NGGWR-02# run traceroute 20.20.1.22 logical-system r0 routing-instance vpn1 source 20.20.1.11 
traceroute to 20.20.1.22 (20.20.1.22) from 20.20.1.11, 30 hops max, 40 byte packets
 1  200.6.11.1 (200.6.11.1)  0.560 ms  0.399 ms  0.369 ms
 2  100.0.12.2 (100.0.12.2)  1.820 ms  0.551 ms  0.555 ms
     MPLS Label=299904 CoS=0 TTL=1 S=0
     MPLS Label=16 CoS=0 TTL=1 S=1
 3  4.4.4.4 (4.4.4.4)  0.544 ms  0.549 ms  0.518 ms
 4  20.20.1.22 (20.20.1.22)  0.604 ms  0.578 ms  0.556 ms

[edit]
lab@MX80-NGGWR-02# run traceroute 20.20.1.33 logical-system r0 routing-instance vpn1 source 20.20.1.11 
traceroute to 20.20.1.33 (20.20.1.33) from 20.20.1.11, 30 hops max, 40 byte packets
 1  200.6.11.1 (200.6.11.1)  0.526 ms  0.427 ms  0.366 ms
 2  100.0.12.2 (100.0.12.2)  0.547 ms  0.522 ms  0.502 ms
     MPLS Label=299808 CoS=0 TTL=1 S=0
     MPLS Label=16 CoS=0 TTL=1 S=1
 3  4.4.4.4 (4.4.4.4)  0.601 ms  0.550 ms  0.521 ms
 4  20.20.1.33 (20.20.1.33)  0.571 ms  0.569 ms  0.553 ms

[edit]
lab@MX80-NGGWR-02# run traceroute 20.20.1.44 logical-system r0 routing-instance vpn1 source 20.20.1.11 
traceroute to 20.20.1.44 (20.20.1.44) from 20.20.1.11, 30 hops max, 40 byte packets
 1  200.6.11.1 (200.6.11.1)  0.527 ms  0.417 ms  0.372 ms
 2  100.0.12.2 (100.0.12.2)  0.531 ms  0.531 ms  0.510 ms
     MPLS Label=299872 CoS=0 TTL=1 S=0
     MPLS Label=299808 CoS=0 TTL=1 S=0
     MPLS Label=16 CoS=0 TTL=1 S=1
 3  100.0.26.2 (100.0.26.2)  0.556 ms  0.592 ms  0.545 ms
     MPLS Label=299808 CoS=0 TTL=1 S=0
     MPLS Label=16 CoS=0 TTL=2 S=1
 4  8.8.8.8 (8.8.8.8)  0.561 ms  0.596 ms  0.544 ms
 5  20.20.1.44 (20.20.1.44)  0.583 ms  0.592 ms  0.566 ms

[edit]
lab@MX80-NGGWR-02# run traceroute 20.20.1.55 logical-system r0 routing-instance vpn1 source 20.20.1.11 
traceroute to 20.20.1.55 (20.20.1.55) from 20.20.1.11, 30 hops max, 40 byte packets
 1  200.6.11.1 (200.6.11.1)  0.493 ms  0.398 ms  0.361 ms
 2  100.0.12.2 (100.0.12.2)  0.539 ms  0.531 ms  0.508 ms
     MPLS Label=299872 CoS=0 TTL=1 S=0
     MPLS Label=299808 CoS=0 TTL=1 S=0
     MPLS Label=16 CoS=0 TTL=1 S=1
 3  100.0.26.2 (100.0.26.2)  0.562 ms  0.545 ms  0.523 ms
     MPLS Label=299808 CoS=0 TTL=1 S=0
     MPLS Label=16 CoS=0 TTL=2 S=1
 4  8.8.8.8 (8.8.8.8)  0.566 ms  0.566 ms  2.423 ms
 5  20.20.1.55 (20.20.1.55)  0.593 ms  0.590 ms  0.613 ms
</code></pre>
<h3 id="config-shamlink">config: shamlink</h3>
<pre><code>set logical-systems r1 routing-instances GREEN protocols ospf sham-link local 1.1.1.1
set logical-systems r1 routing-instances GREEN protocols ospf area 0.0.0.0 sham-link-remote 4.4.4.4

set logical-systems r4 routing-instances GREEN protocols ospf sham-link local 4.4.4.4
set logical-systems r4 routing-instances GREEN protocols ospf area 0.0.0.0 sham-link-remote 1.1.1.1
</code></pre>
<h3 id="verify1-shamlink">verify1: shamlink</h3>
<p>essential of shamlink:</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show ospf route logical-system r0 instance vpn1                                   
Topology default Route Table:

Prefix             Path  Route      NH       Metric NextHop       Nexthop      
                   Type  Type       Type            Interface     Address/LSP
1.1.1.1            Intra Area/AS BR IP            1 ge-1/2/2.611  200.6.11.1
4.4.4.4            Intra Area/AS BR IP            2 ge-1/2/2.611  200.6.11.1        #&lt;------shamlink!!!
20.20.1.22         Intra Router     IP            3 ge-1/2/2.611  200.6.11.1
0.0.0.0/0          Ext2  Network    IP            0 ge-1/2/2.611  200.6.11.1
1.1.1.1/32         Ext2  Network    IP            0 ge-1/2/2.611  200.6.11.1
4.4.4.4/32         Ext2  Network    IP            0 ge-1/2/2.611  200.6.11.1
8.8.8.8/32         Ext2  Network    IP            0 ge-1/2/2.611  200.6.11.1
11.22.0.0/24       Intra Network    IP           50 ge-1/2/1.1122
20.20.1.22/32      Intra Network    IP            3 ge-1/2/2.611  200.6.11.1
20.20.1.33/32      Ext2  Network    IP            0 ge-1/2/2.611  200.6.11.1
20.20.1.44/32      Ext2  Network    IP            0 ge-1/2/2.611  200.6.11.1
20.20.1.55/32      Ext2  Network    IP            0 ge-1/2/2.611  200.6.11.1
200.6.11.0/24      Intra Network    IP            1 ge-1/2/2.611
200.6.42.0/24      Intra Network    IP            3 ge-1/2/2.611  200.6.11.1
200.6.43.0/24      Ext2  Network    IP            0 ge-1/2/2.611  200.6.11.1
200.6.84.0/24      Ext2  Network    IP            0 ge-1/2/2.611  200.6.11.1
200.6.85.0/24      Ext2  Network    IP            0 ge-1/2/2.611  200.6.11.1
</code></pre>
<h3 id="verify2-shamlink">verify2: shamlink</h3>
<pre><code>lab@MX80-NGGWR-02# run show route logical-system r0 table vpn1.inet.0 protocol ospf

vpn1.inet.0: 18 destinations, 18 routes (18 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

0.0.0.0/0          *[OSPF/150] 00:23:19, metric 0, tag 0
                    &gt; to 200.6.11.1 via ge-1/2/2.611
1.1.1.1/32         *[OSPF/150] 00:23:19, metric 0, tag 3489696078
                    &gt; to 200.6.11.1 via ge-1/2/2.611
4.4.4.4/32         *[OSPF/150] 00:15:31, metric 0, tag 3489696078
                    &gt; to 200.6.11.1 via ge-1/2/2.611
8.8.8.8/32         *[OSPF/150] 00:23:19, metric 0, tag 3489696078
                    &gt; to 200.6.11.1 via ge-1/2/2.611
20.20.1.22/32      *[OSPF/10] 00:23:19, metric 3
                    &gt; to 200.6.11.1 via ge-1/2/2.611
20.20.1.33/32      *[OSPF/150] 00:23:19, metric 0, tag 0    #&lt;------learned from type5(150)
                    &gt; to 200.6.11.1 via ge-1/2/2.611
20.20.1.44/32      *[OSPF/150] 00:23:19, metric 0, tag 3489696078
                    &gt; to 200.6.11.1 via ge-1/2/2.611
20.20.1.55/32      *[OSPF/150] 00:23:19, metric 0, tag 3489696078
                    &gt; to 200.6.11.1 via ge-1/2/2.611
200.6.42.0/24      *[OSPF/10] 00:23:19, metric 3
                    &gt; to 200.6.11.1 via ge-1/2/2.611
200.6.43.0/24      *[OSPF/150] 00:15:31, metric 0, tag 3489696078
                    &gt; to 200.6.11.1 via ge-1/2/2.611
200.6.84.0/24      *[OSPF/150] 00:23:19, metric 0, tag 3489696078
                    &gt; to 200.6.11.1 via ge-1/2/2.611
200.6.85.0/24      *[OSPF/150] 00:23:19, metric 0, tag 3489696078
                    &gt; to 200.6.11.1 via ge-1/2/2.611
224.0.0.5/32       *[OSPF/10] 00:24:35, metric 1
                      MultiRecv

lab@MX80-NGGWR-02# run show ospf database logical-system r0 instance vpn1

Area 0.0.0.0
 Type       ID               Adv Rtr           Seq      Age  Opt  Cksum  Len 
Router   1.1.1.1          1.1.1.1          0x80000023  1256  0x22 0x4a65  48
Router   4.4.4.4          4.4.4.4          0x80000022   757  0x22 0x273e  48
Router  *20.20.1.11       20.20.1.11       0x80000022  1257  0x22 0x6cfd  48
Router   20.20.1.22       20.20.1.22       0x80000023   161  0x22 0x4c1   60
Network  11.22.0.2        20.20.1.22       0x8000001f  1256  0x22 0x5ee7  32
Network  200.6.11.1       1.1.1.1          0x80000003   240  0x22 0x170a  32
Network  200.6.42.2       20.20.1.22       0x8000001d  1256  0x22 0x490   32
    OSPF AS SCOPE link state database
 Type       ID               Adv Rtr           Seq      Age  Opt  Cksum  Len 
Extern   0.0.0.0          1.1.1.1          0x8000001e  1256  0x22 0xa8e8  36
Extern   1.1.1.1          4.4.4.4          0x8000001f   400  0xa2 0x76e0  36
Extern   4.4.4.4          1.1.1.1          0x80000001   786  0xa2 0x82f2  36
Extern   8.8.8.8          1.1.1.1          0x80000001   786  0xa2 0xc99b  36
Extern   8.8.8.8          4.4.4.4          0x8000001e    43  0xa2 0x3507  36
Extern  *20.20.1.11       20.20.1.11       0x8000001e  1257  0x22 0xb874  36
Extern   20.20.1.33       4.4.4.4          0x8000001e  1257  0x22 0x239   36        #&lt;------
Extern   20.20.1.44       1.1.1.1          0x80000001   786  0xa2 0x80af  36
Extern   20.20.1.44       4.4.4.4          0x8000001d  1257  0xa2 0xed1a  36        #&lt;------
Extern   20.20.1.55       1.1.1.1          0x80000001   786  0xa2 0x1213  36
Extern   20.20.1.55       4.4.4.4          0x8000001d  1257  0xa2 0x7f7d  36        #&lt;------
Extern   200.6.43.0       1.1.1.1          0x80000001   786  0xa2 0xe5a5  36
Extern   200.6.84.0       1.1.1.1          0x80000001   786  0xa2 0x2141  36
Extern   200.6.84.0       4.4.4.4          0x8000001d  1257  0xa2 0x8eab  36
Extern   200.6.85.0       1.1.1.1          0x80000001   786  0xa2 0x164b  36
Extern   200.6.85.0       4.4.4.4          0x8000001d  1257  0xa2 0x83b5  36

[edit]
lab@MX80-NGGWR-02# run show ospf database logical-system r0 instance vpn1 lsa-id 20.20.1.33 detail  
    OSPF AS SCOPE link state database
 Type       ID               Adv Rtr           Seq      Age  Opt  Cksum  Len 
Extern   20.20.1.33       4.4.4.4          0x8000001f   191  0x22 0xff3a  36
  mask 255.255.255.255
  Topology default (ID 0)
    Type: 2, Metric: 0, Fwd addr: 0.0.0.0, Tag: 0.0.0.0

[edit]
lab@MX80-NGGWR-02# run show ospf database logical-system r0 instance vpn1 lsa-id 20.20.1.44 detail    
    OSPF AS SCOPE link state database
 Type       ID               Adv Rtr           Seq      Age  Opt  Cksum  Len 
Extern   20.20.1.44       1.1.1.1          0x80000001  1307  0xa2 0x80af  36
  mask 255.255.255.255
  Topology default (ID 0)
    Type: 2, Metric: 0, Fwd addr: 0.0.0.0, Tag: 208.0.137.78
Extern   20.20.1.44       4.4.4.4          0x8000001d  1778  0xa2 0xed1a  36
  mask 255.255.255.255
  Topology default (ID 0)
    Type: 2, Metric: 0, Fwd addr: 0.0.0.0, Tag: 208.0.137.78

[edit]
lab@MX80-NGGWR-02# run show route logical-system r4 table GREEN.inet.0 protocol ospf

GREEN.inet.0: 18 destinations, 32 routes (18 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

11.22.0.0/24       *[OSPF/10] 22:04:44, metric 51
                    &gt; to 200.6.42.2 via ge-1/2/1.642
20.20.1.22/32      *[OSPF/10] 22:04:44, metric 1
                    &gt; to 200.6.42.2 via ge-1/2/1.642
224.0.0.5/32       *[OSPF/10] 22:05:52, metric 1
                      MultiRecv

[edit]
lab@MX80-NGGWR-02# run show route logical-system r1 table GREEN.inet.0 protocol ospf

GREEN.inet.0: 17 destinations, 32 routes (17 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

11.22.0.0/24       *[OSPF/10] 22:04:43, metric 51
                    &gt; to 200.6.11.2 via ge-1/2/1.611
20.20.1.11/32      *[OSPF/150] 22:04:43, metric 0, tag 0
                    &gt; to 200.6.11.2 via ge-1/2/1.611
224.0.0.5/32       *[OSPF/10] 22:06:01, metric 1
                      MultiRecv

[edit]
lab@MX80-NGGWR-02# run show route logical-system r1 table GREEN.inet.0 hidden

GREEN.inet.0: 17 destinations, 32 routes (17 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

20.20.1.22/32       [OSPF] 22:05:01, metric 2
                    &gt; via shamlink.0
20.20.1.33/32       [OSPF] 22:05:11, metric 0, tag 0
                    &gt; via shamlink.0
200.6.42.0/24       [OSPF] 22:05:11, metric 2
                    &gt; via shamlink.0

[edit]
lab@MX80-NGGWR-02# run show route logical-system r4 table GREEN.inet.0 hidden

GREEN.inet.0: 18 destinations, 32 routes (18 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

0.0.0.0/0           [OSPF] 22:05:26, metric 0, tag 0
                    &gt; via shamlink.0
20.20.1.11/32       [OSPF] 22:05:01, metric 0, tag 0
                    &gt; via shamlink.0
200.6.11.0/24       [OSPF] 22:05:01, metric 2
                    &gt; via shamlink.0

[edit]
lab@MX80-NGGWR-02#
</code></pre>
<h3 id="config-vpn-inetaccess-1">config: VPN InetAccess 1</h3>
<pre><code>set logical-systems r1 routing-options static route 20.20/16 next-table GREEN.inet.0 
set logical-systems r1 policy-options policy-statement exp-bgp-vpn-routes term 1 from protocol static route-filter 20.20/16 exact  
set logical-systems r1 policy-options policy-statement exp-bgp-vpn-routes term 1 then next-hop self                                          
set logical-systems r1 policy-options policy-statement exp-bgp-vpn-routes term 1 then accept           
set logical-systems r1 protocols bgp group to-v4v6-rr export exp-bgp-vpn-routes  
set logical-systems r1 protocols bgp group to-c3 export exp-bgp-vpn-routes  
set logical-systems r1 routing-options rib-groups imp-inet.0-to-vrf import-rib [inet.0 GREEN.inet.0]  
set logical-systems r1 protocols bgp group to-v4v6-rr family inet unicast rib-group imp-inet.0-to-vrf 
set logical-systems r1 protocols bgp group to-c3 family inet unicast rib-group imp-inet.0-to-vrf 
set logical-systems r1 routing-instances GREEN routing-options aggregate route 0/0    
set logical-systems r1 policy-options policy-statement vrf-exp-ospf-default term 1 from instance GREEN protocol aggregate route-filter 0/0 exact                   
set logical-systems r1 policy-options policy-statement vrf-exp-ospf-default term 1 then accept                                                      
set logical-systems r1 routing-instances GREEN protocols ospf export vrf-exp-ospf-default  
set logical-systems r1 policy-options policy-statement vrf-exp term 3 from protocol aggregate route-filter 0/0 exact                  
set logical-systems r1 policy-options policy-statement vrf-exp term 3 then community add GREEN                          
set logical-systems r1 policy-options policy-statement vrf-exp term 3 then accept
</code></pre>
<h3 id="verify-solution-1-e2e-pingtrace">verify solution 1 e2e ping/trace</h3>
<pre><code>lab@MX80-NGGWR-02# run ping 10.200.1.8 logical-system r0 routing-instance vpn1 source 20.20.1.11 rapid              
PING 10.200.1.8 (10.200.1.8): 56 data bytes
!!!!!
--- 10.200.1.8 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.543/0.621/0.752/0.083 ms

lab@MX80-NGGWR-02# run ping 3.3.3.1 logical-system r0 routing-instance vpn1 source 20.20.1.11 rapid    
PING 3.3.3.1 (3.3.3.1): 56 data bytes
!!!!!
--- 3.3.3.1 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.505/0.775/1.632/0.435 ms
</code></pre>
<h3 id="config-vpn-inetaccess-2">config: VPN InetAccess 2</h3>
<pre><code>#R1:VRF -&gt; Internet: R1 config static def pointing to R2/3; then rib-group it to vrf
#this original solution doesn't work for c3
#set logical-systems r1 routing-options static route 0/0 next-hop [ 100.0.12.2 100.0.13.2 ]
set logical-systems r1 routing-options static route 0/0 next-hop [ 10.200.1.2 10.200.1.3 ]  #&lt;------use R2/3 lo0
set logical-systems r1 routing-options static route 0.0.0.0/0 resolve       #&lt;------and resolve, now C3 is also pingable
set logical-systems r1 routing-options rib-groups imp-inet.0-to-vrf import-rib [ inet.0 GREEN.inet.0 ] 
set logical-systems r1 routing-options static rib-group imp-inet.0-to-vrf

#VPN site-&gt;R1:VRF: R1 VRF adv static def to remote site via vrf-exp; and to local CE via export to ospf 
set logical-systems r1 policy-options policy-statement vrf-exp term 3 from protocol static route-filter 0/0 exact  
set logical-systems r1 policy-options policy-statement vrf-exp term 3 then community add GREEN
set logical-systems r1 policy-options policy-statement vrf-exp term 3 then accept

set logical-systems r1 policy-options policy-statement vrf-exp-ospf-default term 1 from protocol static route-filter 0/0 exact  
set logical-systems r1 policy-options policy-statement vrf-exp-ospf-default term 1 then accept
set logical-systems r1 routing-instances GREEN protocols ospf export vrf-exp-ospf-default

#Internet -&gt; R1: R1 
#   config aggr vpn route; 
#       rib-group some vrf routes (from vrf ospf) into R1,making aggr active
#       adv aggr vpn routes to RR and ce2 
set logical-systems r1 routing-options aggregate route 20.20/16

set logical-systems r1 routing-options rib-groups imp-vrf-to-inet.0 import-rib [ GREEN.inet.0 inet.0 ] 
set logical-systems r1 routing-instances GREEN protocols ospf rib-group imp-vrf-to-inet.0

set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 from protocol aggregate route-filter 20.20/16 exact  
set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 then accept                                      
set logical-systems r1 protocols bgp group to-v4v6-rr export exp-bgp-vpn-agg  
set logical-systems r1 protocols bgp group to-c3 export exp-bgp-vpn-agg

#R1 -&gt; VRF: use policy to change NH to next-table pointing to vrf table; 
#       and apply policy into fwd table
set logical-systems r1 policy-options policy-statement exp-fwd-fix-vpn-nh term 1 from protocol aggregate rib inet.0 route-filter 20.20/16 exact
set logical-systems r1 policy-options policy-statement exp-fwd-fix-vpn-nh term 1 then next-hop next-table GREEN.inet.0
set logical-systems r1 policy-options policy-statement exp-fwd-fix-vpn-nh term 1 then accept
set logical-systems r1 routing-options forwarding-table export exp-fwd-fix-vpn-nh
</code></pre>
<h3 id="verify-solution-2-pingtraceroute">verify : solution 2 ping/traceroute</h3>
<ul>
<li>ping to C3 doesn't work, all other OK</li>
<li>
<p>traceroute doesn't work</p>
<p>lab@MX80-NGGWR-02# run ping 10.200.1.8 logical-system r0 routing-instance vpn1 source 20.20.1.11 rapid               <br />
PING 10.200.1.8 (10.200.1.8): 56 data bytes
!!!!!
--- 10.200.1.8 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.546/0.619/0.863/0.122 ms</p>
<p>[edit]
lab@MX80-NGGWR-02# run ping 3.3.3.1 logical-system r0 routing-instance vpn1 source 20.20.1.11 rapid                <br />
PING 3.3.3.1 (3.3.3.1): 56 data bytes
....^C
--- 3.3.3.1 ping statistics ---
5 packets transmitted, 0 packets received, 100% packet loss</p>
<p>[edit]
lab@MX80-NGGWR-02# run ping 44.44.1.1 logical-system r0 routing-instance vpn1 source 20.20.1.11<br />
PING 44.44.1.1 (44.44.1.1): 56 data bytes
64 bytes from 44.44.1.1: icmp_seq=0 ttl=60 time=0.750 ms
64 bytes from 44.44.1.1: icmp_seq=1 ttl=60 time=0.634 ms
^C
--- 44.44.1.1 ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.634/0.692/0.750/0.058 ms</p>
<p>[edit]
lab@MX80-NGGWR-02# run traceroute 44.44.1.1 logical-system r0 routing-instance vpn1 source 20.20.1.11<br />
traceroute to 44.44.1.1 (44.44.1.1) from 20.20.1.11, 30 hops max, 40 byte packets
 1  200.6.11.1 (200.6.11.1)  0.527 ms  0.418 ms  0.485 ms
^C
[edit]
lab@MX80-NGGWR-02# run traceroute 10.200.0.8 logical-system r0 routing-instance vpn1 source 20.20.1.11<br />
traceroute to 10.200.0.8 (10.200.0.8) from 20.20.1.11, 30 hops max, 40 byte packets
 1  200.6.11.1 (200.6.11.1)  2.590 ms  2.478 ms  3.191 ms
^C
[edit]</p>
</li>
</ul>
<p>after workaround it works:</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run ping 3.3.3.1 logical-system r0 routing-instance vpn1 source 20.20.1.11       
PING 3.3.3.1 (3.3.3.1): 56 data bytes
64 bytes from 3.3.3.1: icmp_seq=0 ttl=63 time=0.915 ms
^C
--- 3.3.3.1 ping statistics ---
1 packets transmitted, 1 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.915/0.915/0.915/0.000 ms

[edit]
lab@MX80-NGGWR-02# run traceroute 10.200.0.8 logical-system r0 routing-instance vpn1 source 20.20.1.11            
traceroute to 10.200.0.8 (10.200.0.8) from 20.20.1.11, 30 hops max, 40 byte packets
 1  200.6.11.1 (200.6.11.1)  0.584 ms  0.450 ms  0.366 ms
 2  100.0.12.2 (100.0.12.2)  0.531 ms  0.522 ms  0.519 ms
 3  100.0.12.2 (100.0.12.2)  0.494 ms !N  0.423 ms !N  0.409 ms !N

[edit]
lab@MX80-NGGWR-02# run traceroute 10.200.1.8 logical-system r0 routing-instance vpn1 source 20.20.1.11   
traceroute to 10.200.1.8 (10.200.1.8) from 20.20.1.11, 30 hops max, 40 byte packets
 1  200.6.11.1 (200.6.11.1)  0.578 ms  0.489 ms  0.393 ms
 2  100.0.12.2 (100.0.12.2)  0.685 ms  0.943 ms  0.593 ms
 3  100.0.26.2 (100.0.26.2)  0.463 ms  0.460 ms  0.426 ms
 4  10.200.1.8 (10.200.1.8)  0.584 ms  0.586 ms  0.558 ms

[edit]
lab@MX80-NGGWR-02# run traceroute 3.3.3.1 logical-system r0 routing-instance vpn1 source 20.20.1.11 
traceroute to 3.3.3.1 (3.3.3.1) from 20.20.1.11, 30 hops max, 40 byte packets
 1  200.6.11.1 (200.6.11.1)  0.619 ms  0.427 ms  0.377 ms
 2  100.0.12.2 (100.0.12.2)  0.675 ms  0.571 ms  0.627 ms
 3  100.0.12.1 (100.0.12.1)  5.438 ms  0.432 ms  0.478 ms
 4  3.3.3.1 (3.3.3.1)  0.561 ms  0.550 ms  0.618 ms
</code></pre>
<h3 id="config-vpn-lsp-map">config vpn LSP map</h3>
<pre><code>set logical-systems r1 policy-options policy-statement exp-fwd-lsp-map term 1 from protocol bgp
set logical-systems r1 policy-options policy-statement exp-fwd-lsp-map term 1 from community ce2
set logical-systems r1 policy-options policy-statement exp-fwd-lsp-map term 1 then install-nexthop lsp r1-r4-green  #&lt;------
set logical-systems r1 policy-options policy-statement exp-fwd-lsp-map term 2 from protocol bgp
set logical-systems r1 policy-options policy-statement exp-fwd-lsp-map term 2 from community ce3
set logical-systems r1 policy-options policy-statement exp-fwd-lsp-map term 2 then install-nexthop lsp r1-r4-blue   #&lt;------

set logical-systems r1 routing-options forwarding-table export exp-fwd-lsp-map
set logical-systems r1 routing-options forwarding-table export exp-fwd-fix-vpn-nh
</code></pre>
<h3 id="verify-vpn-lsp-map">verify vpn LSP map</h3>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show route logical-system r1 table GREEN.inet.0 20.20.1.22

GREEN.inet.0: 17 destinations, 31 routes (17 active, 0 holddown, 2 hidden)
+ = Active Route, - = Last Active, * = Both

20.20.1.22/32      *[BGP/170] 1d 12:48:48, MED 1, localpref 100, from 10.200.1.2
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green
                    [BGP/170] 1d 12:48:48, MED 1, localpref 100, from 10.200.1.3
                      AS path: I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-green

[edit]
lab@MX80-NGGWR-02# run show route logical-system r1 table GREEN.inet.0 20.20.1.33

GREEN.inet.0: 17 destinations, 31 routes (17 active, 0 holddown, 2 hidden)
+ = Active Route, - = Last Active, * = Both

20.20.1.33/32      *[BGP/170] 1d 12:49:06, localpref 100, from 10.200.1.2
                      AS path: 65000 I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
                    [BGP/170] 1d 12:49:22, localpref 100, from 10.200.1.3
                      AS path: 65000 I, validation-state: unverified
                      to 100.0.12.2 via ge-1/2/1.102, label-switched-path r1-r4-blue
</code></pre>
<h3 id="tip-sham-link">TIP: sham-link</h3>
<p>by default all type5 LSA</p>
<pre><code>ce1--------vrf1:pe1-----------//-----------PE2:vrf2----------ce2
   (OSPF)          (MP-BGP)                 (OSPF)
          &lt;-------                         &lt;------
       type5
</code></pre>
<p>sham-link: (benefit over domain-id ?)</p>
<pre><code>             sham-link(unnumbered lo i/f)
            ....................&lt;.................
            .                                    .
            v                                    A
            .                                    .
ce1--------vrf1:pe1-----------//-----------PE2:vrf2----------ce2
   (OSPF)          (MP-BGP)                 (OSPF)
          &lt;-------                         &lt;------
       type5
</code></pre>
<p>routes learned via sham-link , but spf won't install them (why?)</p>
<p><a href="http://www.cisco.com/en/US/docs/ios-xml/ios/iproute_ospf/configuration/15-sy/iro-sham-link.html#GUID-45F321D9-7482-447A-B642-01ADC624A4F7">http://www.cisco.com/en/US/docs/ios-xml/ios/iproute_ospf/configuration/15-sy/iro-sham-link.html#GUID-45F321D9-7482-447A-B642-01ADC624A4F7</a></p>
<p>Before you create a sham-link between PE routers in an MPLS VPN, you must:</p>
<p>Configure a separate /32 address on the remote PE so that OSPF packets can be
sent over the VPN backbone to the remote end of the sham-link. The /32 address
must meet the following criteria:</p>
<ol>
<li>Belong to a VRF.</li>
<li>Not be advertised by OSPF.</li>
<li>Be advertised by BGP.</li>
<li>You can use the /32 address for other sham-links.</li>
</ol>
<p>Associate the sham-link with an existing OSPF area.</p>
<p>seem no need 2 in my case:</p>
<pre><code>lab@MX80-NGGWR-01# show logical-systems lr1 routing-instances GREEN            
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
            interface lo0.11;       #&lt;------
        }
    }
}
</code></pre>
<p>but, the router seems to be able to handle this automatically:</p>
<p>before sham-link up:</p>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system lr1 table GREEN 4.4.4.4/32

GREEN.inet.0: 15 destinations, 34 routes (15 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

4.4.4.4/32         *[OSPF/10] 2d 20:04:12, metric 52        #&lt;------
                    &gt; to 20.20.19.1 via ge-1/2/1.691
                    [BGP/170] 2d 20:49:02, localpref 100, from 10.10.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 2d 20:49:02, localpref 100, from 10.10.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
</code></pre>
<p>but after sham-link up:</p>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system lr1 table GREEN 4.4.4.4/32

GREEN.inet.0: 15 destinations, 29 routes (15 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

4.4.4.4/32         *[BGP/170] 2d 21:07:49, localpref 100, from 10.10.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 2d 21:07:49, localpref 100, from 10.10.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
</code></pre>
<h3 id="tip-domain-id">TIP: domain-id</h3>
<pre><code>determine type3(same) vs type5(diff)
make it unique at all PE routers to ensure that the Type 3 summary LSAs, which
advertise the CE router’s loopback address, are correctly distributed to the remote PE as an
AS external (LSA Type 5). When no domain ID is configured, or when the configured value
matches, network summary LSAs are distributed to the remote CE as a network summary
</code></pre>
<h3 id="tip-traceroute-under-mpls-vpn">TIP: traceroute under mpls vpn</h3>
<ul>
<li><a href="http://forums.juniper.net/t5/Routing/what-does-quot-icmp-tunneling-quot-mean-in-mpls-vpn/td-p/164284">how traceroute works</a></li>
<li>icmp-tunnel</li>
</ul>
<h3 id="tip-vrf-table-lable-vs-tunneled-interface">TIP: vrf-table-lable vs. tunneled-interface</h3>
<p>LSI: LSP sub i/f abstract
enable the knob =&gt; create 1 LSI for this vrf =&gt; assign lable to LSI (1024-2048)</p>
<pre><code>RE1                              PE2
                                  | VRF1                        
                     label1 ------|---- LSI1 
                                  | VRF2
                     label2 ------|---- LSI2 
                                  | VRF3     
                     label3 ------|---- LSI3 
                                  |
</code></pre>
<p>vrf-table-label:</p>
<ul>
<li>Uses LSP sub-interface abstract </li>
<li>Creates an LSI that maps to each VRF table</li>
<li>Supported core-facing interfaces map reserved MPLS labels to each VRF LSI Caveats:
    Only supported on limited interface types
    Not supported for MP-BGP-labeled routes (interprovider and carrier-of-carrier VPNs)</li>
</ul>
<p>VPN tunnel interface :</p>
<ul>
<li>Requires a tunnel services PIC</li>
<li>Causes Internet Processor II lookups on the Egress PE</li>
<li>Rather than forward the packet directly out the physical VRF interface, the
  resulting IP packet from the first lookup is sent to the tunnel service
  interface (next hop equals the vt-x/y/z interface)                      <br />
</li>
</ul>
<h3 id="tip-about-next-hop-next-table-greeninet0">TIP: about <code>next-hop next-table GREEN.inet.0</code></h3>
<ul>
<li>this only change where to "lookup" , not to change/copy any routing tables
  themselves.</li>
<li>
<p>once next-table is used, the <code>from</code> statement must exclude the table in the
  <code>next-table</code> action (meaning specifying a different table) </p>
<p>from ...</p>
<pre><code>rib inet.0      #&lt;------this can't be omitted
</code></pre>
<p>then ...</p>
<pre><code>next-hop next-table GREEN.inet.0
</code></pre>
</li>
</ul>
<h3 id="tip-icmp-tunneling">TIP: icmp-tunneling</h3>
<pre><code>set logical-systems r1 protocols mpls icmp-tunneling       
set logical-systems r2 protocols mpls icmp-tunneling       
set logical-systems r3 protocols mpls icmp-tunneling       
set logical-systems r4 protocols mpls icmp-tunneling       
set logical-systems r5 protocols mpls icmp-tunneling       
set logical-systems r6 protocols mpls icmp-tunneling       
set logical-systems r7 protocols mpls icmp-tunneling       
set logical-systems r8 protocols mpls icmp-tunneling
</code></pre>
<h3 id="tip-about-local-as">TIP: about <code>local-as</code></h3>
<p>configured local-as under RI without <code>autonomous-system</code> under routing-option,
will lead to unexpected behavior at least in the lab simulation</p>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system r0 table green-ce5.inet.0 hidden 0/0 exact extensive

green-ce5.inet.0: 14 destinations, 16 routes (13 active, 0 holddown, 2 hidden)
0.0.0.0/0 (1 entry, 0 announced)
         BGP   
                Next hop type: Router, Next hop index: 2795
                Address: 0x2be0b0c
                Next-hop reference count: 21
                Source: 20.20.150.1
                Next hop: 20.20.150.1 via ge-1/2/2.658, selected
                State: &lt;Hidden Ext&gt;
                Peer AS: 4012345678
                Age: 52 
                Task: BGP_4012345678_65000.20.20.150.1+65053
                AS path: 4012345678 {4012345678 400 1000 1001 1002 2000 3000} I (Looped: 400)  Aggregator: 4012345678 10.10.1.1
                Communities: target:2:65000
                Router ID: 20.20.150.1

same to ce3,4,5.

changing C4 as from `local-as` to `autonomous-system XX` solved the issue.

lab@MX80-NGGWR-01# run show route logical-system r0 table green-ce5.inet.0 0/0 exact extensive      #&lt;------(not hidden)

green-ce5.inet.0: 14 destinations, 16 routes (14 active, 0 holddown, 1 hidden)
0.0.0.0/0 (1 entry, 1 announced)
TSI:
KRT in-kernel 0.0.0.0/0 -&gt; {20.20.150.1}
        *BGP    Preference: 170/-101
                Next hop type: Router, Next hop index: 2795
                Address: 0x2be0b0c
                Next-hop reference count: 22
                Source: 20.20.150.1
                Next hop: 20.20.150.1 via ge-1/2/2.658, selected
                State: &lt;Active Ext&gt;
                Peer AS: 4012345678
                Age: 5 
                Task: BGP_4012345678_65000.20.20.150.1+65053
                Announcement bits (1): 0-KRT 
                AS path: 4012345678 {4012345678 400 1000 1001 1002 2000 3000} I Aggregator: 4012345678 10.10.1.1
                Communities: target:2:65000
                Accepted
                Localpref: 100
                Router ID: 20.20.150.1
</code></pre>
<h3 id="tip-import-rib-and-export-rib">TIP: import-rib and export-rib</h3>
<p>example:</p>
<pre><code>set logical-systems r1 routing-instances GREEN protocols ospf rib-group imp-vrf-to-inet.0    
set logical-systems r1 routing-options rib-groups imp-vrf-to-inet.0 import-rib [GREEN.inet.0 inet.0]
</code></pre>
<p>one common understanding is : import rib from a "source" vrf table GREEN.inet.0,
into the global routing table inet.0</p>
<p>but a more accurate understanding should be:</p>
<p>from the routing table's standspoint:
"import" routes from protocol ospf under vrf GREEN, into "primary" routing table
-- under vrf its the vrf table GREEN.inet.0 (default behavior) , and because of this
import-rib config, also import into a "backup" routing table -- inet.0 , meaning
the global routing table.</p>
<pre><code>from protocol:      ospf/static/interface/etc...                    into protocol
                           ||                           AA
                           ||                           ||
import into:        -------++---------------------------++-------   export
                   (import)||                   (export)||
                           vv                           ||
routing table:      
     default:       inet.0 (def. )              inet.0 (def. w/o export-rib)
     rib-group:     inet.0 + GREEN.inet.0       inet.3(need some test)
</code></pre>
<h3 id="solution-1-old-notes">solution 1 old notes</h3>
<pre><code>#R1 global add static route summarizing all vpn routes, pointing into vrf
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
</code></pre>
<h4 id="source-internet-r1-adv-aggr-vpn-routes-from-r1">source Internet =&gt; R1 : adv aggr. vpn routes from R1</h4>
<h4 id="r1-r1vrf-r1-static-route-with-next-table">R1 =&gt; R1:vrf : R1: static route with next table</h4>
<h5 id="other-r-got-aggr-vpn-routes-from-r1">other R got aggr. vpn routes from R1</h5>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system r5 protocol bgp 20.20/16

inet.0: 50 destinations, 56 routes (50 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

20.20.0.0/16       *[BGP/170] 00:02:33, localpref 100, from 10.10.1.1
                      AS path: I
                    &gt; to 10.10.25.1 via ge-1/2/2.25, label-switched-path r5-r1
</code></pre>
<h4 id="r1vrf-dest-ce-current-behavior-no-need-extra-config">R1:vrf =&gt; dest CE : current behavior, no need extra config</h4>
<h4 id="source-ce-r1vrf-r1vrf-adv-a-default-to-ce-via-ospf">source CE -&gt; R1:vrf : R1:vrf adv a default to CE via ospf</h4>
<h5 id="ce1-routes-after-r1green-exp-default-to-ce1-via-ospf">ce1 routes after R1:GREEN exp default to ce1 via ospf</h5>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system r0 table green-ce1.inet.0 0/0 exact

green-ce1.inet.0: 24 destinations, 25 routes (24 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

0.0.0.0/0          *[OSPF/150] 00:01:57, metric 0, tag 0
                    &gt; to 20.20.19.2 via ge-1/2/2.691
</code></pre>
<h4 id="same-for-other-ce-adjacent-rvrf-r1vrf-export-the-default-route-to-all-sites">same for other CE -&gt; adjacent R:VRF : R1:vrf export the default route to all sites</h4>
<h4 id="r1vrf-r1-internet-r1-leak-internet-means-bgp-table-into-r1-vrf">R1:vrf -&gt; R1 -&gt; Internet : R1 leak Internet (means bgp) table into R1 vrf</h4>
<h5 id="original-r1vrfgreeninet0-table">original R1:vrf(GREEN.inet.0) table</h5>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN.inet.0

GREEN.inet.0: 15 destinations, 29 routes (15 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

1.1.1.1/32         *[Direct/0] 00:17:19
                    &gt; via lo0.11
4.4.4.4/32         *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:16:58, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.1.11/32      *[OSPF/150] 00:16:23, metric 0, tag 0
                    &gt; to 20.20.19.1 via ge-1/2/1.691
20.20.1.22/32      *[BGP/170] 00:16:22, MED 0, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:16:22, MED 0, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.1.33/32      *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                      AS path: 65000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:16:58, localpref 100, from 10.10.1.3
                      AS path: 65000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.1.44/32      *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                      AS path: 65000 I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                    [BGP/170] 00:16:56, localpref 100, from 10.10.1.3
                      AS path: 65000 I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
20.20.1.55/32      *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                      AS path: 65000 I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                    [BGP/170] 00:16:56, localpref 100, from 10.10.1.3
                      AS path: 65000 I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
20.20.19.0/24      *[Direct/0] 00:17:19
                    &gt; via ge-1/2/1.691
20.20.19.2/32      *[Local/0] 00:17:19
                      Local via ge-1/2/1.691
20.20.42.0/24      *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                      AS path: I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:16:58, localpref 100, from 10.10.1.3
                      AS path: I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.100.0/31     *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:16:58, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.120.0/24     *[OSPF/10] 00:16:23, metric 51
                    &gt; to 20.20.19.1 via ge-1/2/1.691
                    [BGP/170] 00:16:22, MED 51, localpref 100, from 10.10.1.2
                      AS path: I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:16:22, MED 51, localpref 100, from 10.10.1.3
                      AS path: I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.150.0/31     *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                    [BGP/170] 00:16:56, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
20.20.200.0/31     *[BGP/170] 00:16:56, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                    [BGP/170] 00:16:56, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
224.0.0.5/32       *[OSPF/10] 00:17:44, metric 1
                      MultiRecv

[edit]
lab@MX80-NGGWR-01#
</code></pre>
<h5 id="r1greeninet0-after-rib-group-r1inet0-r1greeninet0">R1:GREEN.inet.0 , after rib-group: R1:inet.0 -&gt; R1:GREEN.inet.0</h5>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN.inet.0

GREEN.inet.0: 22 destinations, 43 routes (22 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

1.0.0.0/8          *[BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                      AS path: 1001 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
                    [BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                      AS path: 1001 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
1.1.1.1/32         *[Direct/0] 00:19:50
                    &gt; via lo0.11
4.4.4.4/32         *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:19:29, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
10.10.0.0/16       *[BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r5
                    [BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                      AS path: I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
20.20.1.11/32      *[OSPF/150] 00:18:54, metric 0, tag 0
                    &gt; to 20.20.19.1 via ge-1/2/1.691
20.20.1.22/32      *[BGP/170] 00:18:53, MED 0, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:18:53, MED 0, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.1.33/32      *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                      AS path: 65000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:19:29, localpref 100, from 10.10.1.3
                      AS path: 65000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.1.44/32      *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                      AS path: 65000 I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                    [BGP/170] 00:19:27, localpref 100, from 10.10.1.3
                      AS path: 65000 I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
20.20.1.55/32      *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                      AS path: 65000 I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                    [BGP/170] 00:19:27, localpref 100, from 10.10.1.3
                      AS path: 65000 I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
20.20.19.0/24      *[Direct/0] 00:19:50
                    &gt; via ge-1/2/1.691
20.20.19.2/32      *[Local/0] 00:19:50
                      Local via ge-1/2/1.691
20.20.42.0/24      *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                      AS path: I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:19:29, localpref 100, from 10.10.1.3
                      AS path: I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.100.0/31     *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:19:29, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.120.0/24     *[OSPF/10] 00:18:54, metric 51
                    &gt; to 20.20.19.1 via ge-1/2/1.691
                    [BGP/170] 00:18:53, MED 51, localpref 100, from 10.10.1.2
                      AS path: I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:18:53, MED 51, localpref 100, from 10.10.1.3
                      AS path: I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.150.0/31     *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                    [BGP/170] 00:19:27, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
20.20.200.0/31     *[BGP/170] 00:19:27, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
                    [BGP/170] 00:19:27, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.13.2 via ge-1/2/1.13, label-switched-path r1-r6
44.44.0.0/16       *[BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                      AS path: 400 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r5
                    [BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                      AS path: 400 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r5
212.100.0.0/16     *[BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                      AS path: 1002 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
                    [BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                      AS path: 1002 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
215.1.0.0/16       *[BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                      AS path: 1000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
                    [BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                      AS path: 1000 I
                    &gt; to 10.10.13.2 via ge-1/2/1.13
                      to 10.10.12.2 via ge-1/2/1.12
218.2.0.0/16       *[BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                      AS path: 2000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
                    [BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                      AS path: 2000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
223.3.0.0/16       *[BGP/170] 00:00:17, localpref 100, from 10.10.1.6
                      AS path: 3000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r2
                    [BGP/170] 00:00:17, localpref 100, from 10.10.1.5
                      AS path: 3000 I
                      to 10.10.13.2 via ge-1/2/1.13
                    &gt; to 10.10.12.2 via ge-1/2/1.12
224.0.0.5/32       *[OSPF/10] 00:20:15, metric 1
                      MultiRecv
</code></pre>
<h3 id="solution-2-old-notes">solution 2 old notes</h3>
<h4 id="remove-solution1">remove solution1</h4>
<pre><code>#R1 global add static route summarizing all vpn routes, pointing intoto vrf
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
</code></pre>
<h4 id="solution2-config">solution2 config</h4>
<pre><code>#config R1 static default to R2/3, then copy to vrf
set logical-systems r1 routing-options static route 0/0 next-hop [ 10.10.12.2 10.10.13.2 ] 
set logical-systems r1 routing-options rib-groups imp-inet.0-to-vrf import-rib [ inet.0 GREEN.inet.0 ] 
set logical-systems r1 routing-options static rib-group imp-inet.0-to-vrf

#R1 vrf adv this default to other VPN sites
set logical-systems r1 policy-options policy-statement vrf-exp term 3 from protocol static route-filter 0/0 exact  
set logical-systems r1 policy-options policy-statement vrf-exp term 3 then community add GREEN                       
set logical-systems r1 policy-options policy-statement vrf-exp term 3 then accept

#config an aggr route in R1 and adv to all R
set logical-systems r1 routing-options aggregate route 20.20/16      
set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 from protocol aggregate route-filter 20.20/16 exact  
set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 then accept                                            
set logical-systems r1 protocols bgp group to-rr export exp-bgp-vpn-agg

#aggr. routes need at least one contributor, import some contributing routes from vrf table
set logical-systems r1 routing-options rib-groups imp-vrf-to-inet.0 import-rib [GREEN.inet.0 inet.0]    
set logical-systems r1 routing-instances GREEN protocols ospf rib-group imp-vrf-to-inet.0

set logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg term 1 from rib inet.0 protocol aggregate route-filter 20.20/16 exact    
set logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg term 1 then next-hop next-table GREEN.inet.0 
set logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg term 1 then accept                                            
set logical-systems r1 routing-options forwarding-table export exp-fwd-vpn-agg
</code></pre>
<h4 id="r1-internet-r1-static-to-r23">R1 =&gt; Internet : R1 : static to R2/3</h4>
<pre><code>set logical-systems r1 routing-options static route 0/0 next-hop [ 10.10.12.2 10.10.13.2 ]

lab@MX80-NGGWR-01# run show route 0/0 exact logical-system r1

inet.0: 48 destinations, 55 routes (48 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

0.0.0.0/0          *[Static/5] 00:02:28
                    &gt; to 10.10.13.2 via ge-1/2/1.13
                      to 10.10.12.2 via ge-1/2/1.12
</code></pre>
<h4 id="r1vrf-r1-internet-r1-copy-route-into-vrf">R1:vrf =&gt; R1 =&gt; Internet : R1 copy route into vrf</h4>
<pre><code>set logical-systems r1 routing-options rib-groups imp-inet.0-to-vrf import-rib [ inet.0 GREEN.inet.0 ] 
set logical-systems r1 routing-options static rib-group imp-inet.0-to-vrf

lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN.inet.0 protocol static

GREEN.inet.0: 16 destinations, 30 routes (16 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

0.0.0.0/0          *[Static/5] 00:00:55
                      to 10.10.13.2 via ge-1/2/1.13
                    &gt; to 10.10.12.2 via ge-1/2/1.12
</code></pre>
<h4 id="other-rvrf-r1vrf-internet-adv-default-to-other-site">other R:vrf =&gt; R1:vrf (=&gt; Internet) : adv default to other site</h4>
<pre><code>set logical-systems r1 policy-options policy-statement vrf-exp term 3 from protocol static route-filter 0/0 exact  
set logical-systems r1 policy-options policy-statement vrf-exp term 3 then community add GREEN                       
set logical-systems r1 policy-options policy-statement vrf-exp term 3 then accept

[edit]
lab@MX80-NGGWR-01# run show route table GREEN.inet.0 logical-system r4 0/0 exact

GREEN.inet.0: 17 destinations, 29 routes (17 active, 0 holddown, 2 hidden)
+ = Active Route, - = Last Active, * = Both

0.0.0.0/0          *[BGP/170] 00:02:06, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.24.1 via ge-1/2/2.24, label-switched-path r4-r1
                    [BGP/170] 00:02:06, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.24.1 via ge-1/2/2.24, label-switched-path r4-r1

[edit]
lab@MX80-NGGWR-01# run show route table GREEN.inet.0 logical-system r8 0/0 exact

GREEN.inet.0: 16 destinations, 28 routes (16 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

0.0.0.0/0          *[BGP/170] 00:02:17, localpref 100, from 10.10.1.2
                      AS path: I
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 16, Push 300544(top)
                    [BGP/170] 00:02:17, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 16, Push 300544(top)
</code></pre>
<h4 id="internet-r1-r1-adv-an-aggr-route-out">Internet =&gt; R1 : R1: adv an aggr route out</h4>
<pre><code>#config an aggr route in R1 and adv to all R
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
                        &gt; to 20.20.19.1 via ge-1/2/1.691
    20.20.120.0/24     *[OSPF/10] 00:05:42, metric 51
                        &gt; to 20.20.19.1 via ge-1/2/1.691
    224.0.0.5/32       *[OSPF/10] 00:07:16, metric 1
                          MultiRecv

    [edit]
    lab@MX80-NGGWR-01# run show route protocol bgp logical-system r2 20.20/16 exact

    inet.0: 75 destinations, 93 routes (75 active, 0 holddown, 2 hidden)
    Restart Complete
    + = Active Route, - = Last Active, * = Both

    20.20.0.0/16       *[BGP/170] 00:00:07, localpref 100, from 10.10.1.5
                          AS path: I
                        &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                        [BGP/170] 00:00:07, localpref 100, from 10.10.1.6
                          AS path: I
                        &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
</code></pre>
<h4 id="r1-vrf-look-up-vpn-aggr-routes-of-r1-inet0-also-in-vrf-table">R1 =&gt; vrf : look up vpn aggr routes (of R1 inet.0) also in vrf table</h4>
<pre><code>set logical-systems r1 policy-options policy-statement exp-fwd-vpn-agg term 1 from rib inet.0 protocol aggregate route-filter 20.20/16 exact    
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
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 01:06:57, localpref 100, from 10.10.1.3
                      AS path: 65000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
</code></pre>
<h4 id="ping-test">ping test</h4>
<pre><code>lab@MX80-NGGWR-01# run ping 10.10.1.5 logical-system r0 routing-instance green-ce3 source 20.20.1.33              
PING 10.10.1.5 (10.10.1.5): 56 data bytes
64 bytes from 10.10.1.5: icmp_seq=0 ttl=60 time=1.432 ms
64 bytes from 10.10.1.5: icmp_seq=1 ttl=60 time=0.665 ms
^C
--- 10.10.1.5 ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.665/1.048/1.432/0.384 ms
</code></pre>
<h4 id="remove-solution-2">remove solution 2</h4>
<pre><code>delete logical-systems r1 routing-options static route 0/0
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
</code></pre>
<h3 id="config-vpn-lsp-map-old">config vpn lsp map (old)</h3>
<pre><code>set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 1 from protocol bgp community ce2
set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 1 then install-nexthop lsp r1-r4-blue
set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 1 then accept
set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 2 from protocol bgp community ce3
set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 2 then install-nexthop lsp r1-r4-green
set logical-systems r1 policy-options policy-statement exp-fwd-lspmap term 2 then accept

set logical-systems r1 routing-options forwarding-table export exp-fwd-lspmap
</code></pre>
<h4 id="verify">verify</h4>
<pre><code>[edit]
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
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #&lt;------default:all pick blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:41:23, MED 0, localpref 100, from 10.10.1.3
                      AS path: I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #&lt;------
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green

[edit]
lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN 20.20.1.33

GREEN.inet.0: 16 destinations, 30 routes (16 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

20.20.1.33/32      *[BGP/170] 00:41:33, localpref 100, from 10.10.1.2
                      AS path: 65000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #&lt;------default:all pick blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 00:41:33, localpref 100, from 10.10.1.3
                      AS path: 65000 I
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #&lt;------
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
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #&lt;------only 1 LSP (r1-r4-blue)
                    [BGP/170] 00:01:00, MED 0, localpref 100, from 10.10.1.3
                      AS path: I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue         #&lt;------was used

[edit]
lab@MX80-NGGWR-01# run show route logical-system r1 table GREEN 20.20.1.33

GREEN.inet.0: 16 destinations, 30 routes (16 active, 0 holddown, 3 hidden)
+ = Active Route, - = Last Active, * = Both

20.20.1.33/32      *[BGP/170] 00:01:05, localpref 100, from 10.10.1.2
                      AS path: 65000 I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green        #&lt;------
                    [BGP/170] 00:01:05, localpref 100, from 10.10.1.3
                      AS path: 65000 I
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green        #&lt;------

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
</code></pre>
<h3 id="config-vpn-inetaccess-3-tbc">config: VPN InetAccess 3 (t.b.c)</h3>
<pre><code>set logical-systems r1 routing-options aggregate route 20.20.0.0/16
set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 from protocol aggregate
set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 from route-filter 20.20.0.0/16 exact
set logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg term 1 then accept
set logical-systems r1 protocols bgp group to-v4v6-rr export exp-bgp-vpn-agg

set logical-systems r1 routing-options rib-groups imp-vrf-to-inet.0 import-rib GREEN.inet.0
set logical-systems r1 routing-options rib-groups imp-vrf-to-inet.0 import-rib inet.0
</code></pre>
<h4 id="remove-sol3">remove sol3</h4>
<pre><code>delete logical-systems r1 routing-instances GREEN routing-options static  
delete logical-systems r1 policy-options policy-statement vrf-exp term 3 
delete logical-systems r1 routing-instances GREEN protocols ospf export exp-defaults-to-vpn1    
delete logical-systems r1 policy-options policy-statement exp-defaults-to-vpn1                    
delete logical-systems r1 routing-options aggregate route 20.20.0.0/16       
delete logical-systems r1 routing-instances GREEN protocols ospf rib-group    
delete logical-systems r1 routing-instances GREEN routing-options interface-routes rib-group  
delete logical-systems r1 policy-options policy-statement exp-bgp-vpn-agg                     
delete logical-systems r1 protocols bgp group to-v4v6-rr export exp-bgp-vpn-agg                     
delete logical-systems r1 protocols bgp group to-c3 export exp-bgp-vpn-agg  
delete logical-systems r1 routing-options forwarding-table export exp-fwd-fix-vpn-agg-nh  
delete logical-systems r1 policy-options policy-statement exp-fwd-fix-vpn-agg-nh
</code></pre>
<h2 id="cos">COS</h2>
<h3 id="config-cos">config COS</h3>
<p>[from sp3]</p>
<pre><code>1,Provide COS service to the traffic flow from C3 to P3. 
2,on R1, for the cos 111’s input traffic, assign to EF class, cos 110 to AF, others goes into BE.
3,EF set speed limit to 5m, AF to 10m, BE to 7m
4,you can’t affect the default cos policy.
5,make sure the cos service was constant all the way from C3 to P3

IP Prec          111         110             other
fwd-class        EF          AF              BE
</code></pre>
<p>R1:</p>
<pre><code>#define policers:5m/7m/10m
set logical-systems r1 firewall policer 5m if-exceeding bandwidth-limit 5m
set logical-systems r1 firewall policer 5m if-exceeding burst-size-limit 15k
set logical-systems r1 firewall policer 5m then discard
set logical-systems r1 firewall policer 7m if-exceeding bandwidth-limit 7m
set logical-systems r1 firewall policer 7m if-exceeding burst-size-limit 15k
set logical-systems r1 firewall policer 7m then discard
set logical-systems r1 firewall policer 10m if-exceeding bandwidth-limit 10m
set logical-systems r1 firewall policer 10m if-exceeding burst-size-limit 15k
set logical-systems r1 firewall policer 10m then discard

#map: IPrec =&gt; fwd-class; 
#(router will then rewrite MPLS EXP per fwd-class =&gt; exp rewrite rule) 
#apply policers under firewall filter
set logical-systems r1 firewall filter J-Classifier term 1 from precedence 7
set logical-systems r1 firewall filter J-Classifier term 1 then policer 5m
set logical-systems r1 firewall filter J-Classifier term 1 then forwarding-class expedited-forwarding
set logical-systems r1 firewall filter J-Classifier term 1 then accept
set logical-systems r1 firewall filter J-Classifier term 2 from precedence 6
set logical-systems r1 firewall filter J-Classifier term 2 then policer 10m
set logical-systems r1 firewall filter J-Classifier term 2 then forwarding-class assured-forwarding
set logical-systems r1 firewall filter J-Classifier term 2 then accept
set logical-systems r1 firewall filter J-Classifier term 3 then policer 7m
set logical-systems r1 firewall filter J-Classifier term 3 then forwarding-class best-effort
set logical-systems r1 firewall filter J-Classifier term 3 then accept

#apply firewall filter under i/f
set logical-systems r1 interfaces ge-1/2/1 unit 133 family inet filter input J-Classifier
</code></pre>
<p>R5:</p>
<pre><code>#define map: DSCP code(IP prec) =&gt; fwd-class
set class-of-service classifiers inet-precedence class-inetprec import default  
set class-of-service classifiers inet-precedence class-inetprec forwarding-class expedited-forwarding loss-priority low code-points 111 
set class-of-service classifiers inet-precedence class-inetprec forwarding-class assured-forwarding loss-priority low code-points 110

set class-of-service interfaces ge-1/2/2 unit 35 classifiers inet-precedence class-inetprec
set class-of-service interfaces ge-1/2/2 unit 25 classifiers inet-precedence class-inetprec
set class-of-service interfaces ge-1/2/2 unit 45 classifiers inet-precedence class-inetprec
</code></pre>
<h3 id="verify-cos">verify cos</h3>
<pre><code>run show class-of-service classifier type inet-precedence
run show class-of-service rewrite-rule type exp
</code></pre>
<p>R5:</p>
<pre><code>[edit]
lab@MX80-NGGWR-02# run show class-of-service classifier type inet-precedence                 
Classifier: ipprec-default, Code point type: inet-precedence, Index: 12
  Code point         Forwarding class                    Loss priority
  000                best-effort                         low         
  001                assured-forwarding                  low         
  010                best-effort                         low         
  011                best-effort                         low         
  100                best-effort                         low         
  101                expedited-forwarding                low         
  110                network-control                     low         
  111                network-control                     high

Classifier: ipprec-compatibility, Code point type: inet-precedence, Index: 13
  Code point         Forwarding class                    Loss priority
  000                best-effort                         low         
  001                best-effort                         high        
  010                best-effort                         low         
  011                best-effort                         high        
  100                best-effort                         low         
  101                best-effort                         high        
  110                network-control                     low         
  111                network-control                     high

Classifier: class-inetprec, Code point type: inet-precedence, Index: 44252  #&lt;--my config
  Code point         Forwarding class                    Loss priority
  000                best-effort                         low   #&lt;---  
  001                assured-forwarding                  low   #  A   
  010                best-effort                         low   #  |def
  011                best-effort                         low   #  |   
  100                best-effort                         low   #  v   
  101                expedited-forwarding                low   #&lt;---- 
  110                assured-forwarding                  low   #&lt;------
  111                expedited-forwarding                low   #&lt;------
</code></pre>
<h3 id="tip-qoscos">TIP: QoS/CoS</h3>
<h4 id="key-concepts">key concepts</h4>
<p>unidirectonal</p>
<h4 id="ip-tosrfc791">IP TOS(RFC791)</h4>
<pre><code>P2      P1      P0      D      T      R      CU1     CU0
</code></pre>
<ul>
<li>
<p>IP precedence—three bits (P2 to P0)</p>
<p>network         Match packets with network control precedence (7)
internet        Match packets with internetwork control precedence (6)
critical        Match packets with critical precedence (5)
flash-override  Match packets with flash override precedence (4)
flash           Match packets with flash precedence (3)
immediate       Match packets with immediate precedence (2)
priority        Match packets with priority precedence (1)
routine         Match packets with routine precedence (0)</p>
</li>
<li>
<p>Delay, Throughput and Reliability—three bits (D T R)</p>
</li>
<li>CU (Currently Unused)—two bits(CU1-CU0)</li>
</ul>
<h4 id="dscp">DSCP</h4>
<h5 id="diffserv-field">DiffServ field</h5>
<p>Original IPv4 ToS byte (ping: just a new name in the context of diffserv)</p>
<p>RFC2474</p>
<pre><code>DS5     DS4     DS3     DS2     DS1     DS0     ECN     ECN
</code></pre>
<h5 id="behavior-aggregate-ba-forwarding-class">Behavior aggregate (BA): forwarding class</h5>
<p><strong>Classification</strong> 
based / indexed on DSCP 
Packets with a common DSCP belong to the same BA (forwarding class)</p>
<h5 id="per-hop-behavior-phb-scheduling-algorithm-based-on-fwd-class">Per-hop behavior (PHB): scheduling algorithm based on fwd class</h5>
<p>Forwarding treatment associated with a given BA
Packets with the same DSCP value have the same PHB</p>
<p>PHB group:
A set of one or more PHBs with related forwarding behavior </p>
<p>Example: 
assured forwarding (AF) is a PHB group, consisting of PHBs AF1, AF2, AF3, and
AF4</p>
<h6 id="efexpedited-forwarding-101110">EF(Expedited Forwarding): 101110</h6>
<p>RFC3246</p>
<h6 id="afassured-forwarding-001010011100bb0">AF(Assured Forwarding): (001/010/011/100)BB0</h6>
<p>RFC2597</p>
<pre><code>DSCP        AAA BB0
=====================        
AF1         001 BB0

    AF11    001 01       low
    AF11    001 10       medium
    AF11    001 11       high

AF2         010

AF3         011

AF4         100
</code></pre>
<h6 id="nc-or-cscode-selector-aaa000001000-111000">NC or CS(Code Selector): AAA000(001000-111000)</h6>
<p>RFC2474: 
defined for backward compatible with RFC791 (IP precedence)
"code selector code point"
for network control traffic</p>
<p>AAA: 001 - 111
BBB: 000        #&lt;------this is how to diff with other PHB</p>
<h6 id="bebest-effort-000000">BE(Best Effort): 000000</h6>
<p>no spec</p>
<h6 id="redback-device-table">redback device table:</h6>
<pre><code>============================================================
&lt;0-63&gt;   Differentiated services codepoint value 
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
</code></pre>
<h6 id="junos-default-forwarding-class">JUNOS default forwarding-class</h6>
<pre><code>lab@MX80-NGGWR-01# set logical-systems r1 firewall filter Jfilter term 1 then forwarding-class ?
Possible completions:
  &lt;forwarding-class&gt;   Classify packet to forwarding class
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
</code></pre>
<h5 id="junos-default-code-point-aliases">JUNOS default code-point-aliases</h5>
<pre><code>lab@rams# run show class-of-service code-point-aliases (inet-precedence|exp|dscp)

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
</code></pre>
<h4 id="ipv6-rfc2460-tctraffic-class-8b">IPv6: RFC2460 TC(Traffic Class) 8b</h4>
<h4 id="ethernet-8021p-pcppriority-code-point-3b">Ethernet: 802.1p PCP(Priority Code Point) 3b</h4>
<h4 id="mpls-tctraffic-class-or-exp-3b">MPLS: TC(Traffic Class) or EXP 3b</h4>
<h4 id="junos-tool-chains">JUNOS tool chains</h4>
<pre><code>          +-----------+     +-----------+    +-----------+    +-----------+
   Ingress|classifier |     |policer    |    |multi-field|    |policy     |
    --&gt;---+           +-----+           +----+classifier +----+           +
          +-----------+     +-----------+    +-----------+    +-----+-----+
                                                                    |
                                                                    |
                                                                    |
                                                                    |
          +-----------+     +-----------+    +-----------+    +-----+-----+
    Egress|rewrite    |     |scheduler  |    |multi-field|    |policer    |
    &lt;-----+marker     +-----+shaper/RED +----+classifier +----+           +
          +-----------+     +-----------+    +-----------+    +-----------+
</code></pre>
<h5 id="classifier-ingress-traffic-q-forwarding-class">classifier: ingress traffic ==&gt; Q (forwarding class)</h5>
<pre><code>run show class-of-service classifier
</code></pre>
<h5 id="policer-traffic-limit">policer: traffic limit</h5>
<h5 id="policy-cos-based-forwarding">policy: Cos Based Forwarding</h5>
<h5 id="scheduler-redwredpwfqetc">scheduler: RED/WRED/PWFQ/etc</h5>
<h5 id="rewrite-marker">rewrite marker</h5>
<pre><code>run show class-of-service rewrite-rule type exp
</code></pre>
<h3 id="config-cos-old">config COS (old)</h3>
<p>R1:</p>
<pre><code>#config firewall policers:5m,7m,10m
set logical-systems r1 firewall policer 5m if-exceeding bandwidth-limit 5m    
set logical-systems r1 firewall policer 5m if-exceeding burst-size-limit 15k   
set logical-systems r1 firewall policer 5m then discard

set logical-systems r1 firewall policer 7m if-exceeding bandwidth-limit 7m    
set logical-systems r1 firewall policer 7m if-exceeding burst-size-limit 15k   
set logical-systems r1 firewall policer 7m then discard

set logical-systems r1 firewall policer 10m if-exceeding bandwidth-limit 10m    
set logical-systems r1 firewall policer 10m if-exceeding burst-size-limit 15k   
set logical-systems r1 firewall policer 10m then discard

#apply policer into firewall filter: Jfilter
set logical-systems r1 firewall filter Jfilter term 1 from precedence 7                                    
set logical-systems r1 firewall filter Jfilter term 1 then forwarding-class expedited-forwarding accept policer 5m 
set logical-systems r1 firewall filter Jfilter term 2 from precedence 6                                    
set logical-systems r1 firewall filter Jfilter term 2 then forwarding-class assured-forwarding accept policer 10m 
set logical-systems r1 firewall filter Jfilter term 3 then forwarding-class best-effort accept policer 7m

#apply firewall filter on R1 ingress i/f
set logical-systems r1 interfaces ge-1/2/2 unit 133 family inet filter input Jfilter
</code></pre>
<p>R5:</p>
<pre><code>#R5: cos classifier (not supported under LR)
set class-of-service classifiers inet-precedence class-ippre import default
set class-of-service classifiers inet-precedence class-ippre forwarding-class expedited-forwarding loss-priority low code-points 111
set class-of-service classifiers inet-precedence class-ippre forwarding-class assured-forwarding loss-priority low code-points 110 
set class-of-service interfaces ge-1/2/2 unit 35 classifiers inet-precedence class-ippre
</code></pre>
<h2 id="misc-notestips">misc notes/tips</h2>
<h3 id="clear-commit-history">clear commit history</h3>
<p>echo "" &gt; /var/db/commits</p>
<h3 id="ipv6">ipv6</h3>
<h4 id="p1p3-got-all-ipv6-routes">p1/p3 got all ipv6 routes</h4>
<pre><code>lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table p1.inet6.0

p1.inet6.0: 20 destinations, 31 routes (20 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

2000:2000::/32     *[BGP/170] 00:54:04, localpref 100
                      AS path: 4012345678 2000 I
                    &gt; to ::192.168.211.1 via ge-1/2/2.211
                    [BGP/170] 00:54:04, localpref 100
                      AS path: 4012345678 2000 I
                    &gt; to ::192.168.31.1 via ge-1/2/2.311
                    [BGP/170] 00:54:04, localpref 100
                      AS path: 4012345678 2000 I
                    &gt; to ::192.168.11.1 via ge-1/2/2.511
2000:3000::/32     *[BGP/170] 00:54:04, localpref 100
                      AS path: 4012345678 3000 I
                    &gt; to ::192.168.211.1 via ge-1/2/2.211
                    [BGP/170] 00:54:04, localpref 100
                      AS path: 4012345678 3000 I
                    &gt; to ::192.168.31.1 via ge-1/2/2.311
                    [BGP/170] 00:54:04, localpref 100
                      AS path: 4012345678 3000 I
                    &gt; to ::192.168.11.1 via ge-1/2/2.511
3000:1000::/32     *[BGP/170] 00:54:08, localpref 100
                      AS path: 4012345678 1001 I
                    &gt; to ::192.168.11.1 via ge-1/2/2.511
3000:2000::/32     *[BGP/170] 00:54:08, localpref 100
                      AS path: 4012345678 1002 I
                    &gt; to ::192.168.11.1 via ge-1/2/2.511
3333:3333:3333::/48*[BGP/170] 00:54:12, localpref 100
                      AS path: 4012345678 300 I
                    &gt; to ::192.168.31.1 via ge-1/2/2.311
                    [BGP/170] 00:54:12, localpref 100
                      AS path: 4012345678 300 I
                    &gt; to ::192.168.211.1 via ge-1/2/2.211
                    [BGP/170] 00:54:08, localpref 100
                      AS path: 4012345678 300 I
                    &gt; to ::192.168.11.1 via ge-1/2/2.511
4444:4444:4444::/48*[BGP/170] 00:54:08, localpref 100
                      AS path: 4012345678 400 I
                    &gt; to ::192.168.11.1 via ge-1/2/2.511
5555:5555:5555::/48*[BGP/170] 00:54:12, localpref 100
                      AS path: 4012345678 500 I
                    &gt; to ::192.168.211.1 via ge-1/2/2.211
                    [BGP/170] 00:43:48, localpref 100
                      AS path: 4012345678 500 I
                    &gt; to ::192.168.31.1 via ge-1/2/2.311
                    [BGP/170] 00:54:08, localpref 100
                      AS path: 4012345678 500 I
                    &gt; to ::192.168.11.1 via ge-1/2/2.511
</code></pre>
<h4 id="p2-is-missing-some-ipv6-routes">p2 is missing some IPv6 routes</h4>
<pre><code>lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table p2.inet6.0

p2.inet6.0: 14 destinations, 20 routes (14 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

2000:1000::/32     *[BGP/170] 00:56:48, localpref 100
                      AS path: 4012345678 1000 I
                    &gt; to ::192.168.212.1 via ge-1/2/2.212
                    [BGP/170] 00:56:48, localpref 100
                      AS path: 4012345678 1000 I
                    &gt; to ::192.168.32.1 via ge-1/2/2.312
2000:3000::/32     *[BGP/170] 00:56:48, localpref 100
                      AS path: 4012345678 3000 I
                    &gt; to ::192.168.212.1 via ge-1/2/2.212
                    [BGP/170] 00:56:48, localpref 100
                      AS path: 4012345678 3000 I
                    &gt; to ::192.168.32.1 via ge-1/2/2.312
3333:3333:3333::/48*[BGP/170] 00:56:48, localpref 100
                      AS path: 4012345678 300 I
                    &gt; to ::192.168.212.1 via ge-1/2/2.212
                    [BGP/170] 00:56:48, localpref 100
                      AS path: 4012345678 300 I
                    &gt; to ::192.168.32.1 via ge-1/2/2.312
5555:5555:5555::/48*[BGP/170] 00:56:48, localpref 100
                      AS path: 4012345678 500 I
                    &gt; to ::192.168.212.1 via ge-1/2/2.212
                    [BGP/170] 00:46:32, localpref 100
                      AS path: 4012345678 500 I
                    &gt; to ::192.168.32.1 via ge-1/2/2.312
</code></pre>
<p>P2 is missing C4 routes, T1/T2 routes, need to check R2/R3</p>
<h4 id="r2r3-routes">R2/R3 routes</h4>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table p2.inet6.0 hidden

p2.inet6.0: 14 destinations, 20 routes (14 active, 0 holddown, 0 hidden)

[edit]
lab@MX80-NGGWR-01# run show route protocol bgp table inet6.0 logical-system lr2

inet6.0: 24 destinations, 33 routes (23 active, 0 holddown, 4 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

2000:1000::/32     *[BGP/170] 01:00:39, localpref 100
                      AS path: 1000 I
                    &gt; to ::192.168.211.0 via ge-1/2/1.211
2000:2000::/32     *[BGP/170] 01:00:31, localpref 100
                      AS path: 2000 I
                    &gt; to ::192.168.212.0 via ge-1/2/1.212
2000:3000::/32     *[BGP/170] 01:00:31, localpref 100
                      AS path: 3000 I
                    &gt; to ::192.168.213.0 via ge-1/2/1.213
3000:1000::/32     *[BGP/170] 01:00:39, localpref 100
                      AS path: 1001 I
                    &gt; to ::192.168.221.0 via ge-1/2/1.221
3000:2000::/32     *[BGP/170] 01:00:31, localpref 100
                      AS path: 1002 I
                    &gt; to ::192.168.222.0 via ge-1/2/1.222
3333:3333:3333::/48*[BGP/170] 01:00:39, localpref 100, from 10.10.1.5
                      AS path: 300 I
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                    [BGP/170] 01:00:39, localpref 100, from 10.10.1.6
                      AS path: 300 I
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
5555:5555:5555::/48*[BGP/170] 01:00:39, localpref 100, from 10.10.1.5
                      AS path: 500 I
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
                    [BGP/170] 01:00:39, localpref 100, from 10.10.1.6
                      AS path: 500 I
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4

lab@MX80-NGGWR-01# run show route protocol bgp table inet6.0 logical-system lr3

inet6.0: 21 destinations, 36 routes (20 active, 0 holddown, 4 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

2000:1000::/32     *[BGP/170] 01:01:07, localpref 100
                      AS path: 1000 I
                    &gt; to ::192.168.31.0 via ge-1/2/1.311
                    [BGP/170] 01:01:07, localpref 100, from 10.10.1.6
                      AS path: 1000 I
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
2000:2000::/32     *[BGP/170] 01:00:59, localpref 100
                      AS path: 2000 I
                    &gt; to ::192.168.32.0 via ge-1/2/1.312
                    [BGP/170] 00:50:42, localpref 100, from 10.10.1.5
                      AS path: 2000 I
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
                    [BGP/170] 01:00:59, localpref 100, from 10.10.1.6
                      AS path: 2000 I
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
2000:3000::/32     *[BGP/170] 01:00:59, localpref 100, from 10.10.1.6
                      AS path: 3000 I
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
3000:1000::/32     *[BGP/170] 01:00:59, localpref 100
                      AS path: 1001 I
                    &gt; to ::192.168.21.0 via ge-1/2/1.321
                    [BGP/170] 00:50:42, localpref 100, from 10.10.1.5
                      AS path: 1001 I
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
                    [BGP/170] 01:01:07, localpref 100, from 10.10.1.6
                      AS path: 1001 I
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
3000:2000::/32     *[BGP/170] 01:01:07, localpref 100
                      AS path: 1002 I
                    &gt; to ::192.168.22.0 via ge-1/2/1.322
                    [BGP/170] 00:50:42, localpref 100, from 10.10.1.5
                      AS path: 1002 I
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
                    [BGP/170] 01:00:59, localpref 100, from 10.10.1.6
                      AS path: 1002 I
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
3333:3333:3333::/48*[BGP/170] 01:01:07, localpref 100, from 10.10.1.5
                      AS path: 300 I
                    &gt; to 10.10.13.1 via ge-1/2/2.13, label-switched-path r3-r1
                    [BGP/170] 01:01:07, localpref 100, from 10.10.1.6
                      AS path: 300 I
                    &gt; to 10.10.13.1 via ge-1/2/2.13, label-switched-path r3-r1
5555:5555:5555::/48*[BGP/170] 01:01:07, localpref 100, from 10.10.1.5
                      AS path: 500 I
                    &gt; to 10.10.36.2 via ae12.0, label-switched-path r3-r4
                    [BGP/170] 01:01:07, localpref 100, from 10.10.1.6
                      AS path: 500 I
                    &gt; to 10.10.36.2 via ae12.0, label-switched-path r3-r4
</code></pre>
<p>problem:
<em> R2/R3 have all routes except C4 routes
</em> because of policy config, p/t won't exchange routes, so that's why lr2 won't
  export t routes to p.
* why R2/R3 don't have C4 route?</p>
<h4 id="r2r3-routes-from-r5r6-are-hidden">R2/R3 routes from R5/R6 are hidden</h4>
<pre><code>[edit]
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
                State: &lt;Hidden Int Ext&gt;
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
                State: &lt;Hidden Int Ext&gt;
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
</code></pre>
<p>next-hop is R7's "ipv4-mapped ipv6" address, need to check inet6.3 for this
address.</p>
<h4 id="r2r3-inet63-missing-r7r8">R2/R3 inet6.3: missing R7/R8</h4>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route table inet6.3 logical-system lr2

inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[RSVP/7/1] 01:18:25, metric 5
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
::ffff:10.10.1.3/128
                   *[RSVP/7/1] 01:18:25, metric 5
                    &gt; to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
::ffff:10.10.1.4/128
                   *[RSVP/7/1] 01:18:25, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
::ffff:10.10.1.5/128
                   *[RSVP/7/1] 01:18:25, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
::ffff:10.10.1.6/128
                   *[RSVP/7/1] 01:18:25, metric 5
                    &gt; to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6

[edit]
lab@MX80-NGGWR-01# run show route table inet6.3 logical-system lr3

inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[RSVP/7/1] 01:18:28, metric 5
                    &gt; to 10.10.13.1 via ge-1/2/2.13, label-switched-path r3-r1
::ffff:10.10.1.2/128
                   *[RSVP/7/1] 01:18:28, metric 5
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
::ffff:10.10.1.4/128
                   *[RSVP/7/1] 01:18:27, metric 10
                    &gt; to 10.10.36.2 via ae12.0, label-switched-path r3-r4
::ffff:10.10.1.5/128
                   *[RSVP/7/1] 01:18:28, metric 5
                    &gt; to 10.10.35.2 via ge-1/2/1.35, label-switched-path r3-r5
::ffff:10.10.1.6/128
                   *[RSVP/7/1] 01:18:27, metric 5
                    &gt; to 10.10.36.2 via ae12.0, label-switched-path r3-r6
</code></pre>
<p>R2/R3 are missing R3/R2/R7/R8 lo0 host routes in inet6.3, making all IPv6 routes
coming from them listed in "hidden".</p>
<p>solutions:
<em> "install" the missing R7 entry
</em> change NH of those hidden routes to RRs (R5/R6) instead of R7</p>
<h4 id="question-r2-hidden-p1p3-route-from-r5">QUESTION: R2 hidden P1/P3 route , from R5?</h4>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route protocol bgp table inet6.0 logical-system lr2 hidden 2000:1000::/32 extensive

inet6.0: 24 destinations, 33 routes (23 active, 0 holddown, 4 hidden)
Restart Complete
2000:1000::/32 (2 entries, 1 announced)
TSI:
KRT in-kernel 2000:1000::/32 -&gt; {::192.168.211.0}
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
                State: &lt;Hidden Int Ext&gt;
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
</code></pre>
<p>A: might need to define some dedicated VLANs in LS lptc to adv routes</p>
<h4 id="nh-self-on-rr-r5r6-when-reflecting-between-r2r3-and-r7">NH self on RR (R5/R6) when reflecting between R2/R3 and R7</h4>
<pre><code>set logical-systems lr5 policy-options policy-statement exp-nhs-from-r2-r3 term 1 from protocol bgp neighbor 10.10.1.2 
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
                    &gt; to ::192.168.212.1 via ge-1/2/2.212
                    [BGP/170] 02:13:02, localpref 100
                      AS path: 4012345678 1000 I
                    &gt; to ::192.168.32.1 via ge-1/2/2.312
2000:3000::/32     *[BGP/170] 02:13:02, localpref 100
                      AS path: 4012345678 3000 I
                    &gt; to ::192.168.212.1 via ge-1/2/2.212
                    [BGP/170] 02:13:02, localpref 100
                      AS path: 4012345678 3000 I
                    &gt; to ::192.168.32.1 via ge-1/2/2.312
3333:3333:3333::/48*[BGP/170] 02:13:02, localpref 100
                      AS path: 4012345678 300 I
                    &gt; to ::192.168.212.1 via ge-1/2/2.212
                    [BGP/170] 02:13:02, localpref 100
                      AS path: 4012345678 300 I
                    &gt; to ::192.168.32.1 via ge-1/2/2.312
4444:4444:4444::/48*[BGP/170] 00:02:43, localpref 100
                      AS path: 4012345678 400 I
                    &gt; to ::192.168.212.1 via ge-1/2/2.212
                    [BGP/170] 00:02:43, localpref 100
                      AS path: 4012345678 400 I
                    &gt; to ::192.168.32.1 via ge-1/2/2.312
5555:5555:5555::/48*[BGP/170] 02:13:02, localpref 100
                      AS path: 4012345678 500 I
                    &gt; to ::192.168.212.1 via ge-1/2/2.212
                    [BGP/170] 02:02:46, localpref 100
                      AS path: 4012345678 500 I
                    &gt; to ::192.168.32.1 via ge-1/2/2.312
</code></pre>
<h3 id="6pe-more-misc-tips">6PE more misc tips</h3>
<h4 id="tip-ipv6-tunneling-vs-rib-group">TIP: <code>ipv6-tunneling</code> vs <code>rib-group</code></h4>
<p>R1 don't need extra config to copy inet.3 into inet6.3, 
previous config: <code>ipv6-tunneling</code> under mpls will do it
while this magic is true for r1, which built inet.3 via rsvp/ldp; 
this doesn't work for other routers like R2/3/7/8. 
the way they build their inet.3 is through BGP (<code>inet labeled-unicast rib inet.3</code>)</p>
<p>如果inet.3中的路由是从ldp或者rsvp学来的，那么配置了ipv-tunneling之后，
这些路由会直接copy到inet6.3中，
如果路由是从bgp学来的，默认不会copy，需要做rib-group</p>
<h4 id="tip-inet-labeled-unicast-rib-inet3">TIP: <code>inet labeled-unicast rib inet.3</code></h4>
<p>manual about "rib inet.3":</p>
<p>You can allow both labeled and unlabeled routes to be exchanged in a single
session. The labeled routes are placed in the inet.3 routing table, and both
labeled and unlabeled unicast routes can be sent or received by the router.</p>
<p>(WRONG) this looks also inherit all behavior of <code>inet unicast</code></p>
<p>(correct):
without rib inet.3, following can't co-exist:</p>
<pre><code>inet unicast 
inet labeled-unicast
</code></pre>
<p>because both routes (by default), will be put in inet.0 -- the only diff
between these 2 types of routes are, the labeled route carries a label -- this
will lead confliction so only one address family can't be supported</p>
<p>with rib inet.3 ,these are fine:</p>
<pre><code>inet unicast
inet labeled-unicast rib inet.3
</code></pre>
<p>because labeled-route are now put in inet.3, unlabeled are in inet.0</p>
<p>now "You can allow both labeled and unlabeled routes to be exchanged in a single
session"</p>
<h4 id="tip-configuring-ipv6-bgp-routes-over-ipv4-transport">TIP: Configuring IPv6 BGP Routes over IPv4 Transport</h4>
<p><a href="http://www.juniper.net/techpubs/en_US/junos10.4/topics/usage-guidelines/routing-configuring-ipv6-bgp-routes-over-ipv4-transport.html">http://www.juniper.net/techpubs/en_US/junos10.4/topics/usage-guidelines/routing-configuring-ipv6-bgp-routes-over-ipv4-transport.html</a></p>
<h5 id="accept-remote-nexthop">accept-remote-nexthop</h5>
<p>Q: how to make C router (BGP ipv4 neighbor) accept V6 routes without 
configuring "accept-remote-nexthop" on it?                         <br />
</p>
<p>A: no way, C should have that pre-configured already.              <br />
Kevin: is it possible to use IPv4-compatible address as next-hop to carry ipv6 routes? 
http://www.juniper.net/techpubs/en_US/junos12.2/topics/example/bgp-ipv6.html</p>
<h4 id="accept-remote-nexthop_1">accept-remote-nexthop</h4>
<p>.initially got no ipv6 route from a v4 peer, not even as hidden</p>
<pre><code>lab@MX80-NGGWR-01# show logical-systems lr7 protocols bgp group c4                                                              
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
</code></pre>
<p>.add <code>accept-remote-nexthops</code>: showing as hidden</p>
<pre><code>[edit]
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
     Nexthop: ::ffff:192.168.34.0   &lt;------
     AS path: 400 I
</code></pre>
<h4 id="policy-set-next-hop-with-next-hop-peer-address">policy: set next-hop with "next-hop peer-address"</h4>
<pre><code>[edit]
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
</code></pre>
<h5 id="questionsolved-next-hop-peer-address-didnt-really-change-the-nexthop">QUESTION(solved): next-hop peer-address didn't really change the nexthop?</h5>
<p>check <code>rib</code> (after input policy applied) or <code>rib-out</code>(after input&amp;output policy
applied), not <code>rib-in</code> (before policy applied)</p>
<p>use <code>show route protocol</code>, instead of <code>show route received-protocol bgp</code></p>
<p><code>rib-in</code>:</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lr7 receive-protocol bgp 192.168.34.0 4444:4444:4444::/48 extensive

inet6.0: 24 destinations, 39 routes (22 active, 0 holddown, 9 hidden)
Restart Complete
* 4444:4444:4444::/48 (1 entry, 1 announced)
     Accepted
     Nexthop: ::ffff:192.168.34.0   #&lt;------
     AS path: 400 I
</code></pre>
<p><code>rib</code>:</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lr7 protocol bgp table inet6.0 4444:4444:4444::/48 extensive

inet6.0: 24 destinations, 39 routes (22 active, 0 holddown, 9 hidden)
Restart Complete
4444:4444:4444::/48 (1 entry, 1 announced)
TSI:
KRT in-kernel 4444:4444:4444::/48 -&gt; {192.168.34.0}
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
                Next hop: 192.168.34.0 via ge-1/2/1.734, selected   #&lt;------
                Session Id: 0x100001
                State: &lt;Active Ext&gt;
                Local AS: 4012345678 Peer AS:   400
                Age: 4d 4:12:27 
                Validation State: unverified 
                Task: BGP_400.192.168.34.0+179
                Announcement bits (3): 0-KRT 3-BGP_RT_Background 4-Resolve tree 5 
                AS path: 400 I
                Accepted
                Localpref: 100
                Router ID: 44.44.1.1
</code></pre>
<p><code>rib-out</code>:</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route advertising-protocol bgp 10.10.1.5 logical-system lr7 4444:4444:4444::/48 extensive

inet6.0: 24 destinations, 39 routes (22 active, 0 holddown, 9 hidden)
Restart Complete
* 4444:4444:4444::/48 (1 entry, 1 announced)
 BGP group to-rr type Internal
     Nexthop: Self  #&lt;------
     Flags: Nexthop Change
     Localpref: 100
     AS path: [4012345678] 400 I
</code></pre>
<h5 id="tips-rib-in-rib-rib-out">TIPS: rib-in, rib, rib-out</h5>
<p>RFC1771/4271 BGP Routing Information Base consists of three parts as explained below:</p>
<ul>
<li>
<p>The Adj-RIBs-In: BGP RIB-In stores BGP routing information received from
different peers. The stored information is used as an input to BGP decision
process. In other words this is the information received from peers before
applying any attribute modifications or route filtering to them.</p>
</li>
<li>
<p>The Local RIB: The local routing information base stores the resulted
information from processing the RIBs-In database’s information. These are the
routes that are used locally after applying BGP policies and decision process.</p>
</li>
<li>
<p>The Adj-RIBs-out: This one stores the routing information that was selected by
the local BGP router to advertise to its peers through BGP update messages. Do
not forget;  BGP only advertises best routes if they are allowed by local
outbound policies.</p>
</li>
</ul>
<h4 id="questionresolvedhow-c-routers-got-the-ipv6-routes">QUESTION(resolved):how C routers got the IPv6 routes?</h4>
<p>"accept-remote-nexthop" must have been pre-configured in C.</p>
<pre><code>[edit]
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
</code></pre>
<h5 id="change-next-hop-to-local-ipv6-address-of-export-policy-in-lr">change next-hop to local IPv6 address of export policy in LR</h5>
<pre><code>lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table c3.inet6.0 hidden 4444:4444:4444::/48 extensive

c3.inet6.0: 13 destinations, 13 routes (6 active, 0 holddown, 7 hidden)
4444:4444:4444::/48 (1 entry, 0 announced)
         BGP    Preference: 170/-101
                Next hop type: Unusable     &lt;------
                Address: 0x23f3f04
                Next-hop reference count: 10
                State: &lt;Hidden Ext&gt;
                Local AS:   300 Peer AS: 65513
                Age: 10:16 
                Task: BGP_65513_300.192.168.133.1+52133
                AS path: 65513 4012345678 400 I
                Accepted
                Localpref: 100
                Router ID: 10.10.1.1
                Indirect next hops: 1
                        Protocol next hop: ::ffff:192.168.133.1     &lt;------
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
KRT in-kernel 4444:4444:4444::/48 -&gt; {::192.168.133.1}      &lt;------
        *BGP    Preference: 170/-101
                Next hop type: Router, Next hop index: 2361
                Address: 0x282ea38
                Next-hop reference count: 21
                Source: 192.168.133.1
                Next hop: ::192.168.133.1 via ge-1/2/2.133, selected        &lt;------
                State: &lt;Active Ext&gt;
                Local AS:   300 Peer AS: 65513
                Age: 36 
                Task: BGP_65513_300.192.168.133.1+52133
                Announcement bits (2): 0-KRT 2-Resolve tree 4 
                AS path: 65513 4012345678 400 I
                Accepted
                Localpref: 100
                Router ID: 10.10.1.1
</code></pre>
<h4 id="solution-1-installr23-adv-addrr56">solution 1: install@R2/3 + adv addr@R5/6</h4>
<h5 id="install-r7r8-host-into-r23-inet63">install R7/R8 host into R2/3 inet6.3</h5>
<p>install R7/8 host in R2/R3 at LSP</p>
<pre><code>activate logical-systems lr2 protocols mpls label-switched-path r2-r5 install 10.10.1.7/32  
activate logical-systems lr2 protocols mpls label-switched-path r2-r5 install 10.10.1.8/32    
activate logical-systems lr2 protocols mpls label-switched-path r2-r6 install 10.10.1.7/32    
activate logical-systems lr2 protocols mpls label-switched-path r2-r6 install 10.10.1.8/32

activate logical-systems lr3 protocols mpls label-switched-path r3-r5 install 10.10.1.7/32  
activate logical-systems lr3 protocols mpls label-switched-path r3-r5 install 10.10.1.8/32    
activate logical-systems lr3 protocols mpls label-switched-path r3-r6 install 10.10.1.7/32    
activate logical-systems lr3 protocols mpls label-switched-path r3-r6 install 10.10.1.8/32
</code></pre>
<p>r2/r3: before install:</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lr2 table inet6.3

inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[RSVP/7/1] 3d 18:20:35, metric 5
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
::ffff:10.10.1.3/128
                   *[RSVP/7/1] 3d 18:20:36, metric 5
                    &gt; to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
::ffff:10.10.1.4/128
                   *[RSVP/7/1] 3d 18:20:36, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
::ffff:10.10.1.5/128
                   *[RSVP/7/1] 3d 18:20:35, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
::ffff:10.10.1.6/128
                   *[RSVP/7/1] 3d 18:20:36, metric 5
                    &gt; to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6

lab@MX80-NGGWR-01# run show route logical-system lr3 table inet6.3

inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[RSVP/7/1] 3d 18:52:18, metric 5
                    &gt; to 10.10.13.1 via ge-1/2/2.13, label-switched-path r3-r1
::ffff:10.10.1.2/128
                   *[RSVP/7/1] 3d 18:52:19, metric 5
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
::ffff:10.10.1.4/128
                   *[RSVP/7/1] 3d 18:52:19, metric 10
                    &gt; to 10.10.36.2 via ae12.0, label-switched-path r3-r4
::ffff:10.10.1.5/128
                   *[RSVP/7/1] 3d 18:52:19, metric 5
                    &gt; to 10.10.35.2 via ge-1/2/1.35, label-switched-path r3-r5
::ffff:10.10.1.6/128
                   *[RSVP/7/1] 3d 18:52:18, metric 5
                    &gt; to 10.10.36.2 via ae12.0, label-switched-path r3-r6
</code></pre>
<p>r2/lr3 after install:</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lr2 table inet6.3

inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[RSVP/7/1] 3d 18:58:42, metric 5
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
::ffff:10.10.1.3/128
                   *[RSVP/7/1] 3d 18:58:43, metric 5
                    &gt; to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
::ffff:10.10.1.4/128
                   *[RSVP/7/1] 3d 18:58:43, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
::ffff:10.10.1.5/128
                   *[RSVP/7/1] 3d 18:58:42, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
::ffff:10.10.1.6/128
                   *[RSVP/7/1] 00:00:21, metric 5
                    &gt; to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
::ffff:10.10.1.7/128        &lt;------
                   *[RSVP/7/1] 00:00:21, metric 5
                      to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                    &gt; to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
::ffff:10.10.1.8/128        &lt;------
                   *[RSVP/7/1] 00:00:21, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5

[edit]
lab@MX80-NGGWR-01# run show route logical-system lr3 table inet6.3

inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[RSVP/7/1] 3d 18:58:32, metric 5
                    &gt; to 10.10.13.1 via ge-1/2/2.13, label-switched-path r3-r1
::ffff:10.10.1.2/128
                   *[RSVP/7/1] 3d 18:58:33, metric 5
                    &gt; to 10.10.23.1 via ge-1/2/2.23, label-switched-path r3-r2
::ffff:10.10.1.4/128
                   *[RSVP/7/1] 3d 18:58:33, metric 10
                    &gt; to 10.10.36.2 via ae12.0, label-switched-path r3-r4
::ffff:10.10.1.5/128
                   *[RSVP/7/1] 00:00:12, metric 5
                    &gt; to 10.10.35.2 via ge-1/2/1.35, label-switched-path r3-r5
::ffff:10.10.1.6/128
                   *[RSVP/7/1] 00:00:12, metric 5
                    &gt; to 10.10.36.2 via ae12.0, label-switched-path r3-r6
::ffff:10.10.1.7/128        &lt;------
                   *[RSVP/7/1] 00:00:12, metric 5
                      to 10.10.35.2 via ge-1/2/1.35, label-switched-path r3-r5
                    &gt; to 10.10.36.2 via ae12.0, label-switched-path r3-r6
::ffff:10.10.1.8/128        &lt;------
                   *[RSVP/7/1] 00:00:12, metric 5
                    &gt; to 10.10.35.2 via ge-1/2/1.35, label-switched-path r3-r5
                      to 10.10.36.2 via ae12.0, label-switched-path r3-r6
</code></pre>
<p>lr7/lr8:</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lr7 table inet6.3

inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 3d 19:02:35, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299808
::ffff:10.10.1.4/128
                   *[LDP/9] 3d 19:02:33, metric 1
                      to 10.10.78.2 via ge-1/2/1.78, Push 299824
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299824
::ffff:10.10.1.5/128
                   *[LDP/9] 3d 19:02:48, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.6/128
                   *[LDP/9] 3d 19:02:40, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78, Push 299792
::ffff:10.10.1.8/128
                   *[LDP/9] 3d 19:02:42, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78

[edit]
lab@MX80-NGGWR-01# run show route logical-system lr8 table inet6.3

inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 3d 19:02:40, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 299856
::ffff:10.10.1.4/128
                   *[LDP/9] 3d 19:02:40, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 299872
::ffff:10.10.1.5/128
                   *[LDP/9] 3d 19:02:40, metric 1
                    &gt; to 10.10.78.1 via ge-1/2/2.78, Push 299776
::ffff:10.10.1.6/128
                   *[LDP/9] 3d 19:02:47, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68
::ffff:10.10.1.7/128
                   *[LDP/9] 3d 19:02:49, metric 1
                    &gt; to 10.10.78.1 via ge-1/2/2.78

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
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299808
::ffff:10.10.1.2/128
                   *[LDP/9] 00:16:26, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.3/128
                   *[LDP/9] 00:16:26, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.4/128
                   *[LDP/9] 3d 19:28:24, metric 1
                      to 10.10.78.2 via ge-1/2/1.78, Push 299824
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299824
::ffff:10.10.1.8/128
                   *[LDP/9] 3d 19:28:33, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78

[edit]
lab@MX80-NGGWR-01# run show route logical-system lr8 table inet6.3

inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 3d 19:12:08, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 299856
::ffff:10.10.1.2/128        &lt;------
                   *[LDP/9] 00:00:10, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68
::ffff:10.10.1.3/128        &lt;------
                   *[LDP/9] 00:00:10, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68
::ffff:10.10.1.4/128
                   *[LDP/9] 3d 19:12:08, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 299872
::ffff:10.10.1.7/128
                   *[LDP/9] 3d 19:12:17, metric 1
                    &gt; to 10.10.78.1 via ge-1/2/2.78
</code></pre>
<p>have to add lr5/6 lo0:</p>
<pre><code>set logical-systems lr5 policy-options policy-statement egr-ldp-adv-235 term 1 from route-filter 10.10.1.5/32 exact
set logical-systems lr6 policy-options policy-statement egr-ldp-adv-236 term 1 from route-filter 10.10.1.6/32 exact

[edit]
lab@MX80-NGGWR-01# run show route logical-system lr7 table inet6.3

inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 3d 20:41:40, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299808
::ffff:10.10.1.2/128
                   *[LDP/9] 01:29:40, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.3/128
                   *[LDP/9] 01:29:40, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.4/128
                   *[LDP/9] 3d 20:41:38, metric 1
                      to 10.10.78.2 via ge-1/2/1.78, Push 299824
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299824
::ffff:10.10.1.5/128
                   *[LDP/9] 00:00:22, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.6/128
                   *[LDP/9] 00:00:22, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78, Push 299792
::ffff:10.10.1.8/128
                   *[LDP/9] 3d 20:41:47, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78

[edit]
lab@MX80-NGGWR-01# run show route logical-system lr8 table inet6.3

inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 3d 20:41:52, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 299856
::ffff:10.10.1.2/128
                   *[LDP/9] 01:29:54, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68
::ffff:10.10.1.3/128
                   *[LDP/9] 01:29:54, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68
::ffff:10.10.1.4/128
                   *[LDP/9] 3d 20:41:52, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 299872
::ffff:10.10.1.5/128
                   *[LDP/9] 00:00:36, metric 1
                    &gt; to 10.10.78.1 via ge-1/2/2.78, Push 299776
::ffff:10.10.1.6/128
                   *[LDP/9] 00:00:36, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68
::ffff:10.10.1.7/128
                   *[LDP/9] 3d 20:42:01, metric 1
                    &gt; to 10.10.78.1 via ge-1/2/2.78
</code></pre>
<p>C3 inet6.0 route:</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table c3.inet6.0

c3.inet6.0: 13 destinations, 13 routes (13 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

2000:1000::/32     *[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                      AS path: 65513 4012345678 1000 I
                    &gt; to ::192.168.133.1 via ge-1/2/2.133
2000:2000::/32     *[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                      AS path: 65513 4012345678 2000 I
                    &gt; to ::192.168.133.1 via ge-1/2/2.133
2000:3000::/32     *[BGP/170] 2d 01:01:03, localpref 100, from 192.168.133.1
                      AS path: 65513 4012345678 3000 I
                    &gt; to ::192.168.133.1 via ge-1/2/2.133
3000:1000::/32     *[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                      AS path: 65513 4012345678 1001 I
                    &gt; to ::192.168.133.1 via ge-1/2/2.133
3000:2000::/32     *[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                      AS path: 65513 4012345678 1002 I
                    &gt; to ::192.168.133.1 via ge-1/2/2.133
4444:4444:4444::/48*[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                      AS path: 65513 4012345678 400 I
                    &gt; to ::192.168.133.1 via ge-1/2/2.133
5555:5555:5555::/48*[BGP/170] 2d 01:01:02, localpref 100, from 192.168.133.1
                      AS path: 65513 4012345678 500 I
                    &gt; to ::192.168.133.1 via ge-1/2/2.133

[edit]
lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table c4.inet6.0

c4.inet6.0: 13 destinations, 13 routes (13 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

2000:1000::/32     *[BGP/170] 01:39:10, localpref 100, from 192.168.34.1
                      AS path: 4012345678 1000 I
                    &gt; to ::192.168.34.1 via ge-1/2/2.734
2000:2000::/32     *[BGP/170] 01:39:10, localpref 100, from 192.168.34.1
                      AS path: 4012345678 2000 I
                    &gt; to ::192.168.34.1 via ge-1/2/2.734
2000:3000::/32     *[BGP/170] 01:39:10, localpref 100, from 192.168.34.1
                      AS path: 4012345678 3000 I
                    &gt; to ::192.168.34.1 via ge-1/2/2.734
3000:1000::/32     *[BGP/170] 01:39:10, localpref 100, from 192.168.34.1
                      AS path: 4012345678 1001 I
                    &gt; to ::192.168.34.1 via ge-1/2/2.734
3000:2000::/32     *[BGP/170] 01:39:10, localpref 100, from 192.168.34.1
                      AS path: 4012345678 1002 I
                    &gt; to ::192.168.34.1 via ge-1/2/2.734
3333:3333:3333::/48*[BGP/170] 2d 00:16:27, localpref 100, from 192.168.34.1
                      AS path: 4012345678 300 I
                    &gt; to ::192.168.34.1 via ge-1/2/2.734
5555:5555:5555::/48*[BGP/170] 2d 00:16:27, localpref 100, from 192.168.34.1
                      AS path: 4012345678 500 I
                    &gt; to ::192.168.34.1 via ge-1/2/2.734

[edit]
lab@MX80-NGGWR-01# run show route protocol bgp logical-system lptc table c5.inet6.0

c5.inet6.0: 13 destinations, 13 routes (13 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

2000:1000::/32     *[BGP/170] 2d 01:17:46, localpref 100
                      AS path: 4012345678 1000 I
                    &gt; to 33b1::1 via ge-1/2/2.435
2000:2000::/32     *[BGP/170] 2d 01:17:39, localpref 100
                      AS path: 4012345678 2000 I
                    &gt; to 33b1::1 via ge-1/2/2.435
2000:3000::/32     *[BGP/170] 2d 01:17:42, localpref 100
                      AS path: 4012345678 3000 I
                    &gt; to 33b1::1 via ge-1/2/2.435
3000:1000::/32     *[BGP/170] 2d 01:17:46, localpref 100
                      AS path: 4012345678 1001 I
                    &gt; to 33b1::1 via ge-1/2/2.435
3000:2000::/32     *[BGP/170] 2d 01:17:42, localpref 100
                      AS path: 4012345678 1002 I
                    &gt; to 33b1::1 via ge-1/2/2.435
3333:3333:3333::/48*[BGP/170] 2d 01:17:46, localpref 100
                      AS path: 4012345678 300 I
                    &gt; to 33b1::1 via ge-1/2/2.435
4444:4444:4444::/48*[BGP/170] 2d 01:17:46, localpref 100
                      AS path: 4012345678 400 I
                    &gt; to 33b1::1 via ge-1/2/2.435
</code></pre>
<h5 id="make-r23-inet63-reachable-from-r7">make R2/3 inet6.3 reachable from R7</h5>
<h6 id="r7-inet63">R7 inet6.3</h6>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system lr7 table inet6.3

inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 4d 04:38:10, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299808
::ffff:10.10.1.4/128
                   *[LDP/9] 4d 04:38:09, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299824
                      to 10.10.78.2 via ge-1/2/1.78, Push 299840
::ffff:10.10.1.5/128
                   *[LDP/9] 4d 04:38:20, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.6/128
                   *[LDP/9] 4d 04:38:20, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78, Push 299808
::ffff:10.10.1.8/128
                   *[LDP/9] 3d 17:24:26, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78
</code></pre>
<h6 id="config-adv-r2r3-from-r5r6">config: adv R2/R3 from R5/R6</h6>
<pre><code>lab@MX80-NGGWR-01# show logical-systems lr5 policy-options policy-statement egr-ldp-adv-235  
term 1 {
    from {
        route-filter 10.10.1.2/32 exact;
        route-filter 10.10.1.3/32 exact;
        route-filter 10.10.1.5/32 exact;
    }
    then accept;
}

lab@MX80-NGGWR-01# set logical-systems lr5 protocols ldp egress-policy egr-ldp-adv-235
</code></pre>
<h6 id="r7-iet63-after-policy">R7 iet6.3 after policy</h6>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lr7 table inet6.3

inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 4d 04:42:00, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299808
::ffff:10.10.1.2/128
                   *[LDP/9] 00:00:57, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.3/128
                   *[LDP/9] 00:00:46, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.4/128
                   *[LDP/9] 4d 04:41:59, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299824
                      to 10.10.78.2 via ge-1/2/1.78, Push 299840
::ffff:10.10.1.5/128
                   *[LDP/9] 4d 04:42:10, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.6/128
                   *[LDP/9] 4d 04:42:10, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78, Push 299808
::ffff:10.10.1.8/128
                   *[LDP/9] 3d 17:28:16, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78
</code></pre>
<p>R8 inet6.3 table is still missing R2/R3</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lr8 table inet6.3

inet6.3: 6 destinations, 6 routes (6 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 4d 04:50:49, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 299824
::ffff:10.10.1.3/128
                   *[LDP/9] 00:00:04, metric 1
                    &gt; to 10.10.78.1 via ge-1/2/2.78, Push 299776
::ffff:10.10.1.4/128
                   *[LDP/9] 4d 04:50:44, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 299888
::ffff:10.10.1.5/128
                   *[LDP/9] 4d 04:50:55, metric 1
                    &gt; to 10.10.78.1 via ge-1/2/2.78, Push 299776
::ffff:10.10.1.6/128
                   *[LDP/9] 4d 04:50:55, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68
::ffff:10.10.1.7/128
                   *[LDP/9] 4d 04:50:55, metric 1
                    &gt; to 10.10.78.1 via ge-1/2/2.78
</code></pre>
<p>config same on R6:</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# show | compare  
[edit logical-systems lr6 protocols ldp]
-    inactive: egress-policy egr-ldp-adv-236;
+    egress-policy egr-ldp-adv-236;

[edit]
lab@MX80-NGGWR-01# commit  
commit complete
</code></pre>
<p>R8 inet6.3 :</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lr8 table inet6.3

inet6.3: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 4d 04:56:45, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 299824
::ffff:10.10.1.2/128
                   *[LDP/9] 00:00:27, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68
::ffff:10.10.1.3/128
                   *[LDP/9] 00:00:27, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68
::ffff:10.10.1.4/128
                   *[LDP/9] 4d 04:56:40, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68, Push 299888
::ffff:10.10.1.5/128
                   *[LDP/9] 4d 04:56:51, metric 1
                    &gt; to 10.10.78.1 via ge-1/2/2.78, Push 299776
::ffff:10.10.1.6/128
                   *[LDP/9] 4d 04:56:51, metric 1
                    &gt; to 10.10.68.1 via ge-1/2/2.68
::ffff:10.10.1.7/128
                   *[LDP/9] 4d 04:56:51, metric 1
                    &gt; to 10.10.78.1 via ge-1/2/2.78
</code></pre>
<h6 id="question-do-we-need-do-the-same-on-r6">QUESTION: do we need do the same on R6?</h6>
<p>there is no C router attached in R8.
R8 has nothing to do with the IPv6 task here
so R8 don't need to reach R2/R3's lo0 in inet6.3
it looks no need to config R6 ldp also adv R2/R3 lo0</p>
<h5 id="install-both-host-routes-in-both-lsps-in-both-router-r23">install both host routes in both LSPs in both router R2/3</h5>
<p>this is just for completeness, seems not help</p>
<pre><code>lab@MX80-NGGWR-01# show | compare  
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
</code></pre>
<h4 id="question-ipv6-not-end2end-pingable">QUESTION: ipv6 not end2end pingable</h4>
<pre><code>[edit]
lab@MX80-NGGWR-01# run ping 4444:4444:4444::1 logical-system lptc routing-instance c3   
PING6(56=40+8+8 bytes) ::192.168.133.0 --&gt; 4444:4444:4444::1
^C
--- 4444:4444:4444::1 ping6 statistics ---
8 packets transmitted, 0 packets received, 100% packet loss

lab@MX80-NGGWR-01# run ping inet6 4444:4444:4444::1 logical-system lptc routing-instance c3 source 3333:3333:3333::1 
PING6(56=40+8+8 bytes) 3333:3333:3333::1 --&gt; 4444:4444:4444::1
^C
--- 4444:4444:4444::1 ping6 statistics ---
6 packets transmitted, 0 packets received, 100% packet loss

[edit]
lab@MX80-NGGWR-01# run show route logical-system lptc table c4.inet6.0 3333:3333:3333::1

c4.inet6.0: 23 destinations, 23 routes (23 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

3333:3333:3333::/48*[BGP/170] 4d 08:39:09, localpref 100, from 192.168.34.1
                      AS path: 4012345678 300 I, validation-state: unverified
                    &gt; to ::192.168.34.1 via ge-1/2/2.734

[edit]
lab@MX80-NGGWR-01# run show route logical-system lptc table c3.inet6.0 4444:4444:4444::1

c3.inet6.0: 26 destinations, 29 routes (26 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

4444:4444:4444::/48*[BGP/170] 4d 08:39:41, localpref 100, from 192.168.133.1
                      AS path: 65513 4012345678 400 I, validation-state: unverified
                    &gt; to ::192.168.133.1 via ge-1/2/2.133
</code></pre>
<h4 id="solution2-change-next-hop-at-rr-no-install">solution2 : change next-hop at RR ("no install")</h4>
<h5 id="remove-solution1_1">remove solution1</h5>
<pre><code>deactivate logical-systems r2 protocols mpls label-switched-path r2-r5 install 10.10.1.7/32  
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
</code></pre>
<h5 id="add-solution-2">add solution 2</h5>
<pre><code>change bgp nh from rr R4/5 when reflecting between R2/3 and R7

set logical-systems lr5 protocols bgp group rr neighbor 10.10.1.2 export exp-bgp-nhs-from-r7  
set logical-systems lr5 protocols bgp group rr neighbor 10.10.1.3 export exp-bgp-nhs-from-r7    
set logical-systems lr5 protocols bgp group rr neighbor 10.10.1.7 export exp-bgp-nhs-from-r2-r3                           
set logical-systems lr6 protocols bgp group rr neighbor 10.10.1.2 export exp-bgp-nhs-from-r7  
set logical-systems lr6 protocols bgp group rr neighbor 10.10.1.3 export exp-bgp-nhs-from-r7    
set logical-systems lr6 protocols bgp group rr neighbor 10.10.1.7 export exp-bgp-nhs-from-r2-r3

commit
run clear bgp neighbor soft logical-system lr5
run clear bgp neighbor soft logical-system lr6
</code></pre>
<h4 id="solution-3-mixed-solution12">solution 3: mixed solution1&amp;2</h4>
<h5 id="remove-solution-2_1">remove solution 2:</h5>
<pre><code>delete logical-systems lr5 protocols bgp group rr neighbor 10.10.1.2 export exp-bgp-nhs-from-r7  
delete logical-systems lr5 protocols bgp group rr neighbor 10.10.1.3 export exp-bgp-nhs-from-r7    
delete logical-systems lr5 protocols bgp group rr neighbor 10.10.1.7 export exp-bgp-nhs-from-r2-r3                           
delete logical-systems lr6 protocols bgp group rr neighbor 10.10.1.2 export exp-bgp-nhs-from-r7  
delete logical-systems lr6 protocols bgp group rr neighbor 10.10.1.3 export exp-bgp-nhs-from-r7    
delete logical-systems lr6 protocols bgp group rr neighbor 10.10.1.7 export exp-bgp-nhs-from-r2-r3

commit
run clear bgp neighbor soft logical-system lr5
run clear bgp neighbor soft logical-system lr6
</code></pre>
<p>this solution does not look great. no extra benefit also.</p>
<h4 id="solution-4-rib-rib-group">solution 4: rib + rib-group</h4>
<h5 id="config">config</h5>
<pre><code>#R5/6: advertise R2/3/7/8 lo0 via BGP:

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
</code></pre>
<h5 id="before">before</h5>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system r2 10.10.1.7

inet.0: 62 destinations, 62 routes (62 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

10.10.1.7/32       *[IS-IS/18] 06:13:33, metric 10
                    &gt; to 10.10.25.2 via ge-1/2/1.25

lab@MX80-NGGWR-01# run show route logical-system r2 table inet.3

inet.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

10.10.1.1/32       *[RSVP/7/1] 05:55:13, metric 5
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
10.10.1.3/32       *[RSVP/7/1] 05:55:14, metric 5
                    &gt; to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
10.10.1.4/32       *[RSVP/7/1] 05:55:13, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.5/32       *[RSVP/7/1] 05:55:13, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
10.10.1.6/32       *[RSVP/7/1] 05:55:13, metric 5
                    &gt; to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
</code></pre>
<h5 id="after">after</h5>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system r2 10.10.1.7

inet.0: 67 destinations, 83 routes (67 active, 0 holddown, 2 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

10.10.1.7/32       *[IS-IS/18] 06:13:40, metric 10
                    &gt; to 10.10.25.2 via ge-1/2/1.25
                    [BGP/170] 00:00:03, MED 5, localpref 100, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.25.2 via ge-1/2/1.25
                    [BGP/170] 00:00:05, MED 10, localpref 100, from 10.10.1.6
                      AS path: I
                    &gt; to 10.10.25.2 via ge-1/2/1.25
                      to 10.10.26.2 via ge-1/2/1.26

lab@MX80-NGGWR-01# run show route logical-system r2 table inet.3

inet.3: 8 destinations, 9 routes (8 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

10.10.1.1/32       *[RSVP/7/1] 05:55:36, metric 5
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
10.10.1.2/32       *[BGP/170] 00:00:01, MED 5, localpref 4294967294, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
10.10.1.3/32       *[RSVP/7/1] 05:55:37, metric 5
                    &gt; to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
                    [BGP/170] 00:00:01, MED 5, localpref 4294967294, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
10.10.1.4/32       *[RSVP/7/1] 05:55:36, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.5/32       *[RSVP/7/1] 05:55:36, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
10.10.1.6/32       *[RSVP/7/1] 05:55:36, metric 5
                    &gt; to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
10.10.1.7/32       *[BGP/170] 00:00:01, MED 1, localpref 100, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
10.10.1.8/32       *[BGP/170] 00:00:01, MED 1, localpref 100, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
</code></pre>
<h5 id="verification-of-rib-group">verification of rib-group</h5>
<p>before rib-group applied at R7:</p>
<pre><code>family inet labeled-uncast rib-group 6pe
</code></pre>
<p>inet.3 is good but inet6.3 are still not complete:</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route table inet.3 logical-system r7

inet.3: 8 destinations, 9 routes (8 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

10.10.1.1/32       *[LDP/9] 07:21:14, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299824
10.10.1.2/32       *[BGP/170] 00:00:20, MED 5, localpref 4294967294, from 10.10.1.5         #&lt;------
                      AS path: I
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299968
10.10.1.3/32       *[BGP/170] 00:00:20, MED 5, localpref 4294967294, from 10.10.1.5         #&lt;------
                      AS path: I
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299984
10.10.1.4/32       *[LDP/9] 07:21:15, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78, Push 299840
                      to 10.10.57.1 via ge-1/2/2.57, Push 299808
10.10.1.5/32       *[LDP/9] 07:21:44, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
10.10.1.6/32       *[LDP/9] 07:21:43, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78, Push 299776
10.10.1.7/32       *[BGP/170] 00:00:20, MED 1, localpref 100, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 300000
10.10.1.8/32       *[LDP/9] 07:21:43, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78
                    [BGP/170] 00:00:20, MED 1, localpref 100, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 300016

[edit]
lab@MX80-NGGWR-01# run show route table inet6.3 logical-system r7

inet6.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 07:21:28, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299824
::ffff:10.10.1.4/128
                   *[LDP/9] 07:21:29, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78, Push 299840
                      to 10.10.57.1 via ge-1/2/2.57, Push 299808
::ffff:10.10.1.5/128
                   *[LDP/9] 07:21:58, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.6/128
                   *[LDP/9] 07:21:57, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78, Push 299776
::ffff:10.10.1.8/128
                   *[LDP/9] 07:21:57, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78

[edit]
lab@MX80-NGGWR-01# run show route table inet6.3 logical-system r7

inet6.3: 8 destinations, 9 routes (8 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

::ffff:10.10.1.1/128
                   *[LDP/9] 07:36:12, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299824
::ffff:10.10.1.2/128        #&lt;------
                   *[BGP/170] 00:10:46, MED 5, localpref 4294967294, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299968
::ffff:10.10.1.3/128        #&lt;------
                   *[BGP/170] 00:10:46, MED 5, localpref 4294967294, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 299984
::ffff:10.10.1.4/128
                   *[LDP/9] 07:36:13, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78, Push 299840
                      to 10.10.57.1 via ge-1/2/2.57, Push 299808
::ffff:10.10.1.5/128
                   *[LDP/9] 07:36:42, metric 1
                    &gt; to 10.10.57.1 via ge-1/2/2.57
::ffff:10.10.1.6/128
                   *[LDP/9] 07:36:41, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78, Push 299776
::ffff:10.10.1.7/128        #&lt;------
                   *[BGP/170] 00:10:46, MED 1, localpref 100, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 300000
::ffff:10.10.1.8/128
                   *[LDP/9] 07:36:41, metric 1
                    &gt; to 10.10.78.2 via ge-1/2/1.78
                    [BGP/170] 00:10:46, MED 1, localpref 100, from 10.10.1.5
                      AS path: I
                    &gt; to 10.10.57.1 via ge-1/2/2.57, Push 300016
</code></pre>
<h5 id="tips-about-ribrib-groupinet3inet63">TIPS: about rib/rib-group/inet.3/inet6.3</h5>
<p>R2/3 inet.3 won't change before R5/6 and R2/3 configured:</p>
<pre><code>family inet labeled-unicast rib inet.3
</code></pre>
<p>R2/3 inet6.3 won't updated before R2/3 configured:</p>
<pre><code>family inet labeled-uncast rib-group 6pe
</code></pre>
<h4 id="question-family-inet-unicast-vs-family-inet-labeled-unicast">QUESTION: <code>family inet unicast</code> vs. <code>family inet labeled-unicast</code></h4>
<pre><code>lab@MX80-NGGWR-01# show logical-systems lr2 protocols bgp group to-rr  
type internal;
local-address 10.10.1.2;
import imp-bgp-rtbh;
family inet {
    unicast;                #&lt;------these are fine being configured 
    labeled-unicast {       #&lt;------together
        rib-group 6pe;
        rib {
            inet.3;
        }
    }
}
family inet6 {
    labeled-unicast {       #&lt;------can't co-exist with unicast.
        explicit-null;
    }
}
export [ exp-bgp-nhs exp-bgp-lo0-v6 ];
neighbor 10.10.1.5;
neighbor 10.10.1.6;
</code></pre>
<p>error message:</p>
<pre><code>lab@MX80-NGGWR-01# set logical-systems lr2 protocols bgp group to-rr family inet6 unicast

[edit]
lab@MX80-NGGWR-01# commit  
[edit logical-systems lr2 protocols]
  'bgp'
    Error in neighbor 10.10.1.5 of group to-rr:
peer cannot have both inet6 unicast and inet6 labeled-unicast nlri
error: configuration check-out failed
</code></pre>
<h4 id="question-why-family-inet-labeled-unicast-in-this-solution">QUESTION: why <code>family inet labeled-unicast</code> in this solution?</h4>
<p>according to 6PE spec, <code>family inet6 labeled-unicast explicit-null</code> is used to
assign label (2) to ipv6 prefixes at PE, why again <code>family inet
labeled-unicast</code>? </p>
<p>is it just because <code>rib</code> and <code>rib-group</code> feature only supported under
labeled-unicast by design?</p>
<p><a href="http://www.juniper.net/techpubs/software/junos/junos94/swconfig-routing/rib_2.html">http://www.juniper.net/techpubs/software/junos/junos94/swconfig-routing/rib_2.html</a>
<a href="http://www.juniper.net/techpubs/en_US/junos12.1/topics/topic-map/bgp-multiprotocol.html">http://www.juniper.net/techpubs/en_US/junos12.1/topics/topic-map/bgp-multiprotocol.html</a></p>
<p>You can allow both labeled and unlabeled routes to be exchanged in a single
session. The labeled routes are placed in the inet.3 routing table, and both
labeled and unlabeled unicast routes can be sent to or received by the routing
device. </p>
<p>To allow both labeled and unlabeled routes to be exchanged, include the rib
inet.3 statement:</p>
<pre><code>rib inet.3;
</code></pre>
<h4 id="simple-topo-and-config">simple topo and config</h4>
<pre><code>&lt;--ipv6 (AS1000)-&gt; &lt;---------ipv4 AS(3000)-------&gt; &lt;--ipv6 (AS2000)-&gt;
+-----+        +-----+         +-----+         +-----+       +-----+
| ce1 |--------| pe1 |---------|  p  |---------| pe2 |-------| ce2 |
+-+---+ V1501  +-+---+ V1503   +--+--+ V1502   +--+--+ V1504 +--+--+
  |  10::1/126   | 192.168.0.0/30 | 192.168.0.4/30|   11::0/126 |
  |              | 1.1.1.1/32     |       2.2.2.2 |             |
  |98::1/128                  10.10.10.10/32          98::1/128 |
</code></pre>
<h5 id="pe1-config">PE1 config</h5>
<pre><code>logical-routers 6pepe1 {
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
                    labeled-unicast {       #&lt;------
                        explicit-null;      #&lt;------
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
            ipv6-tunneling;         #&lt;------
            label-switched-path pe1-to-pe2 {
                to 2.2.2.2;
            }
            interface ge-1/2/1.1501;
        }
    }
}
</code></pre>
<h5 id="pe2-config">PE2 config</h5>
<pre><code>logical-systems 6pepe2 {                   
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
</code></pre>
<h5 id="resources">resources</h5>
<ul>
<li><a href="http://tools.ietf.org/html/rfc4798">6PE</a></li>
<li><a href="http://tools.ietf.org/html/rfc3032">reserved IPv6 Explicit NULL Label</a></li>
<li><a href="http://www.juniper.net/techpubs/en_US/junos13.1/topics/reference/configuration-statement/ipv6-tunneling-edit-protocols-mpls.html">ipv6-tunnel</a></li>
<li><a href="http://www.youtube.com/watch?v=zraAfs3bY5E">vedio</a></li>
<li><a href="http://www.juniper.net/techpubs/en_US//junos/topics/example/mpls-tunneling-ipv6-over-mpls-ipv4.html">example</a></li>
</ul>
<h5 id="family-inet6-labeled-unicast-vs-unicast">family inet6 <code>labeled-unicast</code> vs <code>unicast</code></h5>
<pre><code>delete logical-systems lr1 protocols bgp group to-rr family inet6 unicast
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
</code></pre>
<h3 id="rtbh-verify">RTBH verify</h3>
<h4 id="initial-routes">initial routes</h4>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet.0 33.33.33.33/32

inet.0: 67 destinations, 76 routes (67 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

33.33.33.33/32     *[BGP/170] 01:05:50, localpref 100, from 10.10.1.5
                      AS path: 300 I
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                    [BGP/170] 01:05:48, localpref 100, from 10.10.1.6
                      AS path: 300 I
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

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
                State: &lt;Active Int Ext&gt;
                Local AS: 4012345678 Peer AS: 4012345678
                Age: 1:06:28    Metric2: 5 
                Task: BGP_4012345678.10.10.1.5+179
                Announcement bits (4): 2-KRT 5-Aggregate 6-BGP_RT_Background 7-Resolve tree 4 
                AS path: 300 I (Originator) Cluster list:  1.1.1.1
                AS path:  Originator ID: 10.10.1.1
                Communities: 65412:100 target:4012345678L:2000      &lt;------
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
                State: &lt;NotBest Int Ext&gt;
                Inactive reason: Not Best in its group - Update source
                Local AS: 4012345678 Peer AS: 4012345678
                Age: 1:06:26    Metric2: 5 
                Task: BGP_4012345678.10.10.1.6+179
                AS path: 300 I (Originator) Cluster list:  1.1.1.1
                AS path:  Originator ID: 10.10.1.1
                Communities: 65412:100 target:4012345678L:2000      &lt;------
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
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                    [BGP/170] 01:07:37, localpref 100, from 10.10.1.6
                      AS path: 300 I
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

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
                State: &lt;Active Int Ext&gt;
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
                State: &lt;NotBest Int Ext&gt;
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
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                    [BGP/170] 01:08:28, localpref 100, from 10.10.1.6
                      AS path: 300 I
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

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
                State: &lt;Active Int Ext&gt;
                Local AS: 4012345678 Peer AS: 4012345678
                Age: 1:08:39    Metric2: 5 
                Task: BGP_4012345678.10.10.1.5+179
                Announcement bits (3): 0-KRT 3-BGP_RT_Background 4-Resolve tree 5 
                AS path: 300 I (Originator) Cluster list:  1.1.1.1
                AS path:  Originator ID: 10.10.1.1
                Communities: 65412:100 target:4012345678L:2000      &lt;------
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
                State: &lt;NotBest Int Ext&gt;
                Inactive reason: Not Best in its group - Update source
                Local AS: 4012345678 Peer AS: 4012345678
                Age: 1:08:35    Metric2: 5 
                Task: BGP_4012345678.10.10.1.6+179
                AS path: 300 I (Originator) Cluster list:  1.1.1.1
                AS path:  Originator ID: 10.10.1.1
                Communities: 65412:100 target:4012345678L:2000      &lt;------
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
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                    [BGP/170] 01:08:50, localpref 100, from 10.10.1.6
                      AS path: 300 I
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

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
                State: &lt;Active Int Ext&gt;
                Local AS: 4012345678 Peer AS: 4012345678
                Age: 1:09:00    Metric2: 5 
                Task: BGP_4012345678.10.10.1.5+179
                Announcement bits (3): 0-KRT 3-BGP_RT_Background 4-Resolve tree 5 
                AS path: 300 I (Originator) Cluster list:  1.1.1.1
                AS path:  Originator ID: 10.10.1.1
                Communities: 65412:100 target:4012345678L:2000      &lt;------
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
                State: &lt;NotBest Int Ext&gt;
                Inactive reason: Not Best in its group - Update source
                Local AS: 4012345678 Peer AS: 4012345678
                Age: 1:08:56    Metric2: 5 
                Task: BGP_4012345678.10.10.1.6+179
                AS path: 300 I (Originator) Cluster list:  1.1.1.1
                AS path:  Originator ID: 10.10.1.1
                Communities: 65412:100 target:4012345678L:2000      &lt;------
                Accepted
                Localpref: 100
                Router ID: 10.10.1.6
</code></pre>
<h4 id="config_1">config</h4>
<pre><code>set logical-systems lr2 policy-options community rtbh members [ 65412:100 target:4012345678L:2000 ] 
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
</code></pre>
<h4 id="result">result</h4>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route protocol bgp logical-system lr2 table inet.0 3.3.3.0/24

inet.0: 67 destinations, 76 routes (67 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

3.3.3.0/24         *[BGP/170] 01:13:15, localpref 100, from 10.10.1.5
                      AS path: 300 I
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                    [BGP/170] 01:13:13, localpref 100, from 10.10.1.6
                      AS path: 300 I
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

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
                State: &lt;Active Int Ext&gt;
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
                State: &lt;NotBest Int Ext&gt;
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
                State: &lt;Active Int Ext&gt;
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
                State: &lt;NotBest Int Ext&gt;
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
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
                    [BGP/170] 01:13:24, localpref 100, from 10.10.1.6
                      AS path: 300 I
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1

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
                State: &lt;Active Int Ext&gt;
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
                State: &lt;NotBest Int Ext&gt;
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
                State: &lt;Active Int Ext&gt;
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
                State: &lt;NotBest Int Ext&gt;
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
</code></pre>
<h3 id="basic-interconnections">basic interconnections</h3>
<h4 id="results">results</h4>
<p>R1:</p>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system lr1 table GREEN.inet.0

GREEN.inet.0: 11 destinations, 28 routes (11 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

1.1.1.1/32         *[Direct/0] 3d 13:40:48
                    &gt; via lo0.11
                    [BGP/170] 2d 19:15:40, MED 52, localpref 100, from 10.10.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 2d 19:15:40, MED 52, localpref 100, from 10.10.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
4.4.4.4/32         *[OSPF/10] 2d 19:15:40, metric 52
                    &gt; to 20.20.19.1 via ge-1/2/1.691
                    [BGP/170] 2d 20:00:30, localpref 100, from 10.10.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 2d 20:00:30, localpref 100, from 10.10.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.1.11/32      *[OSPF/150] 2d 19:15:45, metric 0, tag 0
                    &gt; to 20.20.19.1 via ge-1/2/1.691
                    [BGP/170] 2d 19:15:40, MED 0, localpref 100, from 10.10.1.2
                      AS path: I, validation-state: unverified
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 2d 19:15:40, MED 0, localpref 100, from 10.10.1.3
                      AS path: I, validation-state: unverified
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.1.22/32      *[OSPF/150] 2d 19:15:40, metric 0, tag 0
                    &gt; to 20.20.19.1 via ge-1/2/1.691
                    [BGP/170] 2d 19:15:45, MED 0, localpref 100, from 10.10.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 2d 19:15:45, MED 0, localpref 100, from 10.10.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.1.33/32      *[OSPF/150] 05:21:45, metric 0, tag 103
                    &gt; to 20.20.19.1 via ge-1/2/1.691
                    [BGP/170] 05:21:50, localpref 100, from 10.10.1.2
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 05:21:50, localpref 100, from 10.10.1.3
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.19.0/24      *[Direct/0] 3d 13:39:14
                    &gt; via ge-1/2/1.691
                    [BGP/170] 2d 19:15:40, MED 52, localpref 100, from 10.10.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 2d 19:15:40, MED 52, localpref 100, from 10.10.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.19.2/32      *[Local/0] 3d 13:39:23
                      Local via ge-1/2/1.691
20.20.42.0/24      *[OSPF/10] 2d 19:15:40, metric 52
                    &gt; to 20.20.19.1 via ge-1/2/1.691
                    [BGP/170] 3d 02:19:17, localpref 100, from 10.10.1.2
                      AS path: I, validation-state: unverified
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 3d 11:37:33, localpref 100, from 10.10.1.3
                      AS path: I, validation-state: unverified
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.100.0/31     *[BGP/170] 3d 02:19:17, localpref 100, from 10.10.1.2
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 3d 11:37:33, localpref 100, from 10.10.1.3
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
20.20.120.0/24     *[OSPF/10] 2d 19:15:45, metric 51
                    &gt; to 20.20.19.1 via ge-1/2/1.691
                    [BGP/170] 2d 19:15:45, MED 51, localpref 100, from 10.10.1.2
                      AS path: I, validation-state: unverified
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
                    [BGP/170] 2d 19:15:45, MED 51, localpref 100, from 10.10.1.3
                      AS path: I, validation-state: unverified
                      to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-blue
                    &gt; to 10.10.12.2 via ge-1/2/1.12, label-switched-path r1-r4-green
224.0.0.5/32       *[OSPF/10] 3d 13:41:03, metric 1
                      MultiRecv
</code></pre>
<h4 id="issue-no-ce45-routes">issue: no CE4/5 routes</h4>
<h4 id="check-routes-in-rr">check routes in RR</h4>
<p>no CE4/5 routes:</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lr2 table bgp.l3vpn.0

bgp.l3vpn.0: 20 destinations, 20 routes (16 active, 0 holddown, 4 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

10.10.1.1:1:1.1.1.1/32                
                   *[BGP/170] 3d 02:22:31, localpref 100, from 10.10.1.1
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
10.10.1.1:1:4.4.4.4/32                
                   *[BGP/170] 2d 19:18:54, MED 52, localpref 100, from 10.10.1.1
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
10.10.1.1:1:20.20.1.11/32                
                   *[BGP/170] 2d 19:18:59, MED 0, localpref 100, from 10.10.1.1
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
10.10.1.1:1:20.20.1.22/32                
                   *[BGP/170] 2d 19:18:54, MED 0, localpref 100, from 10.10.1.1
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
10.10.1.1:1:20.20.19.0/24                
                   *[BGP/170] 3d 02:22:31, localpref 100, from 10.10.1.1
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
10.10.1.1:1:20.20.42.0/24                
                   *[BGP/170] 2d 19:18:54, MED 52, localpref 100, from 10.10.1.1
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
10.10.1.1:1:20.20.120.0/24                
                   *[BGP/170] 2d 19:18:59, MED 51, localpref 100, from 10.10.1.1
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
10.10.1.4:1:1.1.1.1/32                
                   *[BGP/170] 2d 19:18:54, MED 52, localpref 100, from 10.10.1.4
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.4:1:4.4.4.4/32                
                   *[BGP/170] 2d 20:03:44, localpref 100, from 10.10.1.4
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.4:1:20.20.1.11/32                
                   *[BGP/170] 2d 19:18:54, MED 0, localpref 100, from 10.10.1.4
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.4:1:20.20.1.22/32                
                   *[BGP/170] 2d 19:18:59, MED 0, localpref 100, from 10.10.1.4
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.4:1:20.20.1.33/32                
                   *[BGP/170] 05:25:04, localpref 100, from 10.10.1.4
                      AS path: 65000 I, validation-state: unverified
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.4:1:20.20.19.0/24                
                   *[BGP/170] 2d 19:18:54, MED 52, localpref 100, from 10.10.1.4
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.4:1:20.20.42.0/24                
                   *[BGP/170] 3d 02:22:31, localpref 100, from 10.10.1.4
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.4:1:20.20.100.0/31                
                   *[BGP/170] 3d 02:22:31, localpref 100, from 10.10.1.4
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.4:1:20.20.120.0/24                
                   *[BGP/170] 2d 19:18:59, MED 51, localpref 100, from 10.10.1.4
                      AS path: I, validation-state: unverified
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
</code></pre>
<p>check RR bgp.l3vpn.0 =&gt;  CE4/5 route in "hidden":</p>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lr2 table bgp.l3vpn.0 all 20.20.1.44/32 extensive

bgp.l3vpn.0: 20 destinations, 20 routes (16 active, 0 holddown, 4 hidden)
Restart Complete
10.10.1.8:1:20.20.1.44/32 (1 entry, 0 announced)
         BGP    Preference: 170/-101
                Route Distinguisher: 10.10.1.8:1
                Next hop type: Unusable
                Address: 0x244ce94
                Next-hop reference count: 6
                State: &lt;Hidden Int Ext&gt;
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
</code></pre>
<p>reason is no next hop resolvation, =&gt; check inet.3. </p>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system lr2 table inet.3

inet.3: 5 destinations, 5 routes (5 active, 0 holddown, 0 hidden)
Restart Complete
+ = Active Route, - = Last Active, * = Both

10.10.1.1/32       *[RSVP/7/1] 3d 13:52:24, metric 5
                    &gt; to 10.10.12.1 via ge-1/2/2.12, label-switched-path r2-r1
10.10.1.3/32       *[RSVP/7/1] 3d 13:52:23, metric 5
                    &gt; to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r3
10.10.1.4/32       *[RSVP/7/1] 3d 13:52:22, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r4
10.10.1.5/32       *[RSVP/7/1] 3d 13:52:24, metric 5
                    &gt; to 10.10.24.2 via ge-1/2/1.24, label-switched-path r2-r5
                      to 10.10.23.2 via ge-1/2/1.23, label-switched-path r2-r5
10.10.1.6/32       *[RSVP/7/1] 3d 13:52:23, metric 5
                    &gt; to 10.10.26.2 via ge-1/2/1.26, label-switched-path r2-r6
</code></pre>
<p>no LSP to R8. that's the issue.
solution:
   1) create LSP
   2) install host routes
   3) adv inactive (inactive = hidden ?)
   4) ?</p>
<h4 id="solution-non-workadv-inactive-in-rr">solution (non-work):adv-inactive in RR</h4>
<p>doesn't work</p>
<h4 id="solution-install-r8-in-r2r3-lsp">solution: install R8 in R2/R3 lsp</h4>
<pre><code>lab@MX80-NGGWR-01# show | compare  
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
  10.10.1.8:1:20.20.1.44/32                                         #&lt;------
*                         10.10.1.8                    100        65000 I
  10.10.1.8:1:20.20.1.55/32                    
*                         10.10.1.8                    100        65000 I
  10.10.1.8:1:20.20.150.0/31                    
*                         10.10.1.8                    100        I
  10.10.1.8:1:20.20.200.0/31                    
*                         10.10.1.8                    100        I
</code></pre>
<h3 id="backdoor-routes-and-sham-link">backdoor routes and sham-link</h3>
<pre><code>[edit]
lab@MX80-NGGWR-01# run show route logical-system lce table green-ce1.inet.0

green-ce1.inet.0: 16 destinations, 17 routes (16 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

1.1.1.1/32         *[OSPF/10] 2d 19:49:33, metric 1
                    &gt; to 20.20.19.2 via ge-1/2/2.691
4.4.4.4/32         *[OSPF/10] 2d 19:49:23, metric 51
                    &gt; to 20.20.120.1 via ge-1/2/2.120
20.20.1.11/32      *[Direct/0] 2d 19:49:39
                    &gt; via ge-1/2/2.4001
                    [Local/0] 2d 19:49:39
                      Local via ge-1/2/2.4001
20.20.1.22/32      *[OSPF/150] 2d 19:49:23, metric 0, tag 0         #&lt;------
                    &gt; to 20.20.120.1 via ge-1/2/2.120
20.20.1.33/32      *[OSPF/150] 05:55:33, metric 0, tag 103          #&lt;------
                    &gt; to 20.20.120.1 via ge-1/2/2.120
20.20.1.44/32      *[OSPF/150] 00:06:30, metric 0, tag 3489696078   #&lt;------
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.1.55/32      *[OSPF/150] 00:06:30, metric 0, tag 3489696078   #&lt;------
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.19.0/24      *[Direct/0] 3d 14:13:02
                    &gt; via ge-1/2/2.691
20.20.19.1/32      *[Local/0] 3d 14:13:14
                      Local via ge-1/2/2.691
20.20.42.0/24      *[OSPF/10] 2d 19:49:23, metric 51
                    &gt; to 20.20.120.1 via ge-1/2/2.120
20.20.100.0/31     *[OSPF/150] 05:45:57, metric 0, tag 3489696078
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.120.0/24     *[Direct/0] 3d 14:13:02
                    &gt; via ge-1/2/2.120
20.20.120.2/32     *[Local/0] 3d 14:13:12
                      Local via ge-1/2/2.120
20.20.150.0/31     *[OSPF/150] 00:06:30, metric 0, tag 3489696078
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.200.0/31     *[OSPF/150] 00:06:30, metric 0, tag 3489696078
                    &gt; to 20.20.19.2 via ge-1/2/2.691
224.0.0.5/32       *[OSPF/10] 3d 14:14:52, metric 1
                      MultiRecv
</code></pre>
<p>vpn route prefer the backdoor exit, need to fix it with shamlink</p>
<h4 id="solutionsham-link">solution:sham-link</h4>
<pre><code>lab@MX80-NGGWR-01# show | compare  
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
</code></pre>
<p>now the ce1 prefer backbone instead of backdoor:</p>
<pre><code>lab@MX80-NGGWR-01# run show route logical-system lce table green-ce1.inet.0

green-ce1.inet.0: 16 destinations, 17 routes (16 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

1.1.1.1/32         *[OSPF/150] 00:06:03, metric 0, tag 3489696078
                    &gt; to 20.20.19.2 via ge-1/2/2.691
4.4.4.4/32         *[OSPF/150] 00:06:13, metric 0, tag 3489696078
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.1.11/32      *[Direct/0] 2d 20:24:38
                    &gt; via ge-1/2/2.4001
                    [Local/0] 2d 20:24:38
                      Local via ge-1/2/2.4001
20.20.1.22/32      *[OSPF/150] 00:06:03, metric 0, tag 0    #&lt;------
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.1.33/32      *[OSPF/150] 00:06:03, metric 0, tag 103  #&lt;------
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.1.44/32      *[OSPF/150] 00:41:29, metric 0, tag 3489696078
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.1.55/32      *[OSPF/150] 00:41:29, metric 0, tag 3489696078
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.19.0/24      *[Direct/0] 3d 14:48:01
                    &gt; via ge-1/2/2.691
20.20.19.1/32      *[Local/0] 3d 14:48:13
                      Local via ge-1/2/2.691
20.20.42.0/24      *[OSPF/10] 00:06:03, metric 3
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.100.0/31     *[OSPF/150] 06:20:56, metric 0, tag 3489696078
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.120.0/24     *[Direct/0] 3d 14:48:01
                    &gt; via ge-1/2/2.120
20.20.120.2/32     *[Local/0] 3d 14:48:11
                      Local via ge-1/2/2.120
20.20.150.0/31     *[OSPF/150] 00:41:29, metric 0, tag 3489696078
                    &gt; to 20.20.19.2 via ge-1/2/2.691
20.20.200.0/31     *[OSPF/150] 00:41:29, metric 0, tag 3489696078
                    &gt; to 20.20.19.2 via ge-1/2/2.691
224.0.0.5/32       *[OSPF/10] 3d 14:49:51, metric 1
                      MultiRecv
</code></pre>
<h3 id="vpls-old">VPLS (old)</h3>
<h4 id="config_2">config</h4>
<pre><code>set logical-systems r1 routing-instances vpls instance-type vpls
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
</code></pre>
<h4 id="show-vpls-connection">show vpls connection</h4>
<pre><code>lab@MX80-NGGWR-01# run show vpls connections logical-system r1 extensive          
Layer-2 VPN connections:

Legend for connection status (St)   
EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
EM -- encapsulation mismatch     WE -- interface and instance encaps not same
VC-Dn -- Virtual circuit down    NP -- interface hardware not present 
CM -- control-word mismatch      -&gt; -- only outbound connection is up
CN -- circuit not provisioned    &lt;- -- only inbound connection is up
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
</code></pre>
<h4 id="show-route-forwarding-table">show route forwarding-table</h4>
<h5 id="with-tunne-service">with tunne-service</h5>
<pre><code>lab@MX80-NGGWR-01# run show route forwarding-table | find vpls.vpls
Logical system: r1
Routing table: vpls.vpls
VPLS:
Destination        Type RtRef Next hop           Type Index NhRef Netif
default            perm     0                    dscd   728     1
vt-1/2/10.235929600 intf     0                   indr 1048693     4
                              10.10.12.2        Push 800000, Push 299808, Push 299792(top)  3007     2 ge-1/2/1.12
0x3000b/51         user     0                    comp  3016     2
f8:c0:01:18:93:92/48 user     0                  ucst  1986     5 ge-1/2/1.121      #&lt;------
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
f8:c0:01:18:93:92/48 user     0                  indr 1048659     5         #&lt;------
                              10.10.68.1        Push 800006, Push 299872(top)  3052     2 ge-1/2/2.68
ge-1/2/1.687       intf     0                    ucst  1973     4 ge-1/2/1.687
0x30009/51         user     0                    comp  1983     2
0x30006/51         user     0                    comp  1980     2
</code></pre>
<p>turn off tunnel service:</p>
<pre><code>lab@MX80-NGGWR-01# show | compare  
[edit logical-systems r1 routing-instances vpls protocols vpls]
+      no-tunnel-services;
[edit logical-systems r8 routing-instances vpls protocols vpls]
+      no-tunnel-services;
</code></pre>
<h5 id="without-tunnel-service">without tunnel service</h5>
<pre><code>Logical system: r1
Routing table: vpls.vpls
VPLS:
Destination        Type RtRef Next hop           Type Index NhRef Netif
default            perm     0                    dscd   728     1
lsi.235929600      intf     0                    indr 1048699     4
                              10.10.12.2        Push 262145, Push 299808, Push 299792(top)  3014     2 ge-1/2/1.12
0x3000a/51         user     0                    comp  3062     2
f8:c0:01:18:93:92/48 user     0                  ucst   716     5 ge-1/2/1.121      #&lt;------
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
f8:c0:01:18:93:92/48 user     0                  indr 1048698     5         #&lt;------
                              10.10.68.1        Push 262151, Push 299872(top)  3005     2 ge-1/2/2.68
ge-1/2/1.687       intf     0                    ucst  1980     4 ge-1/2/1.687
0x3000b/51         user     0                    comp  3146     2
0x30008/51         user     0                    comp  3143     2

ge-1/2/1: Current address: f8:c0:01:18:93:91, Hardware address: f8:c0:01:18:93:91
ge-1/2/2: Current address: f8:c0:01:18:93:92, Hardware address: f8:c0:01:18:93:92
</code></pre>
