---
layout: post
title: "issuechecker"
published: true
created:  2015  5月 27 05时42分25秒
tags: [issuechecker, tcl, expect, script]
categories: [tech]

---


<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="content-type" content="text/html; charset=utf-8" />
    <meta name="keywords" content="remark,remarkjs,markdown,slideshow,presentation" />
    <meta name="description" content="A simple, in-browser, markdown-driven slideshow tool." />
    <title>Tcl/Expect</title>
    <style type="text/css">
      @import url(http://fonts.googleapis.com/css?family=Droid+Serif);
      @import url(http://fonts.googleapis.com/css?family=Yanone+Kaffeesatz);

      body {
        font-family: 'Droid Serif';
        font-size: 20px;
      }
      h1, h2, h3 {
        font-family: 'Yanone Kaffeesatz';
        font-weight: 400;
        margin-bottom: 0;
      }
      h1 { font-size: 4em; }
      h2 { font-size: 2em; }
      h3 { font-size: 1.6em; }
      .footnote {
        position: absolute;
        bottom: 3em;
      }
      li p { line-height: 1.25em; }
      .red { color: #fa0000; }
      .large { font-size: 2em; }
      a, a > code {
        color: rgb(249, 38, 114);
        text-decoration: none;
      }
      code {
        -moz-border-radius: 5px;
        -web-border-radius: 5px;
        background: #e7e8e2;
        border-radius: 5px;
        font-size: 16px;
      }
      .pull-left {
        float: left;
        width: 47%;
      }
      .pull-right {
        float: right;
        width: 47%;
      }
      .pull-right ~ p {
        clear: both;
      }
      #slideshow .slide .content code {
        font-size: 0.8em;
      }
      #slideshow .slide .content pre code {
        font-size: 0.9em;
        padding: 15px;
      }
      .inverse {
        background: #272822;
        color: #777872;
        text-shadow: 0 0 20px #333;
      }
      .inverse h1, .inverse h2 {
        color: #f3f3f3;
        line-height: 0.8em;
      }

      /* Slide-specific styling */
      #slide-inverse .footnote {
        bottom: 12px;
        left: 20px;
      }
      #slide-how .slides {
        font-size: 0.9em;
        position: absolute;
        top:  151px;
        right: 140px;
      }
      #slide-how .slides h3 {
        margin-top: 0.2em;
      }
      #slide-how .slides .first, #slide-how .slides .second {
        padding: 1px 20px;
        height: 180px;
        width: 160px;
        -moz-box-shadow: 0 0 10px #777;
        -webkit-box-shadow: 0 0 10px #777;
        box-shadow: 0 0 10px #777;
      }
      #slide-how .slides .first {
        background: #fff;
        position: absolute;
        top: 20%;
        left: 20%;
        z-index: 1;
      }
      #slide-how .slides .second {
        position: relative;
        background: #fff;
        z-index: 0;
      }

      /* Two-column layout */
      .left-column {
        color: #777;
        width: 20%;
        height: 92%;
        float: left;
      }
        .left-column h2:last-of-type, .left-column h3:last-child {
          color: #000;
        }
      .right-column {
        width: 75%;
        float: right;
        padding-top: 1em;
      }
    </style>
  </head>
  <body>
    <textarea id="source">
name: inverse
layout: true
class: left, middle, inverse

---
template: inverse

class: center, middle, inverse
#issuechecker.tcl
-- a generic-purpose expect script, for issue replication and network monitoring

JTAC:Ping Song <pings@juniper.net>  2014

.footnote[Go to [my blog](http://www-in.juniper.net/~pings/myblog/tech/2014/02/11/scripts/)]
[Tcl]: http://en.wikipedia.org/wiki/Tcl
[Expect]: http://en.wikipedia.org/wiki/Expect

---

class: center, middle, inverse
template: inverse
##table of content
### basic USAGE
### USAGE cases
#### single router, info collection
#### multiple routers, info collection
#### long time networks monitor
#### issue replication
#### common configurable options
#### polling att lab routers
#### network audit

---

class: center, middle, inverse
template: inverse
##basic usage

---

layout: false
.left-column[
 # basic usage
 ## how to run
]

.right-column[
### run from my folder directly
```
bash$ ~pings/bin/issuechecker.tcl
```

### or,copy it into your own folder and run
```
cd yourfolder
cp ~pings/bin/issuechecker.tcl ./
chmod 755 issuechecker.tcl
./issuechecker.tcl
```

### ideally, put it in a place that is in the `PATH` variable, so it can be executed from anywhere
```
echo $PATH
~/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
```
]

---

layout: false

.left-column[
 # basic usage
 ## first time run
]

.right-column[
##first time run:
* just create a test folder and enter the folder
* run the script , without any parameter (config file name)
* it will print a usage message and generate some example config files, for your later reference

```
pings@svl-jtac-tool02:~$ mkdir temp1
pings@svl-jtac-tool02:~$ cd temp1
pings@svl-jtac-tool02:~/temp1$ ~pings/bin/issuechecker.tcl
usage:
  #to generate a example config files:
  issuechecker
  #to run the script with a config file:
  issuechecker [CONFIG_FILE_NAME_UNDER_CURRENT_FOLDER]
example:
  issuechecker
  issuechecker config1.conf
following example config files has been generated FYR:
 111 May  4 12:54 issuechecker_example1_single.conf
1421 May  4 12:54 issuechecker_example5_replicate_options.conf
 898 May  4 12:54 issuechecker_example4_replicate.conf
1493 May  4 12:54 issuechecker_example6_replicate_collect.conf
 158 May  4 12:54 issuechecker_example2_multi.conf
1910 May  4 12:54 issuechecker_example7_monitor_change.conf
 659 May  4 12:54 issuechecker_example8_dataexport.conf
 296 May  4 12:54 issuechecker_example3_check.conf
```
]

---

.left-column[
 # basic usage
 ## first time run
]

.right-column[
##check the generated files:
* some example configuration files were generated for your reference
* choose any of them as a template to start with
```
pings@svl-jtac-tool02:~/temp1$ ls -l
 111 May  4 17:21 issuechecker_example1_single.conf
 158 May  4 17:21 issuechecker_example2_multi.conf
 296 May  4 17:21 issuechecker_example3_check.conf
 898 May  4 17:21 issuechecker_example4_replicate.conf
1421 May  4 17:21 issuechecker_example5_replicate_options.conf
1493 May  4 17:21 issuechecker_example6_replicate_collect.conf
1910 May  4 17:21 issuechecker_example7_monitor_change.conf
 659 May  4 17:21 issuechecker_example8_dataexport.conf
```
]

---

.left-column[
 # basic usage
 ## run with config file
]

.right-column[
## run the script with config file
* select an example config file, 
* modify it (router name , commands , etc) and save as your own config file
* run the script with your config file name

```
~/temp1$ ~pings/bin/issuechecker.tcl issuechecker_example2_multi.conf
Trying 172.19.161.100...
Connected to alecto.jtac-east.jnpr.net.
Escape character is '^'.
alecto-re1 (ttyp1)
login: lab
Password: 
-- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC
{master}
lab@alecto-re1> current log file .//alecto.log
set cli screen-width 300 
Screen width set to 300
{master}
lab@alecto-re1> Trying 172.19.161.51...
Connected to hermes.jtac-east.jnpr.net.
Escape character is '^'.
hermes-re0 (ttyp1)
login: lab
Password: 
-- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC
{master}
lab@hermes-re0> current log file .//hermes.log
set cli screen-width 300 
Screen width set to 300

```
]

---

.left-column[
 # basic usage
 ##run with config file (cont.)
]

.right-column[
```
{master}
lab@hermes-re0> show version | no-more 
Hostname: hermes-re0
Model: m320
JUNOS Base OS boot [12.3-20140210_dev_x_123_att.0]
......
JUNOS Routing Software Suite [12.3-20140210_dev_x_123_att.0]

{master}
lab@hermes-re0> show interfaces fxp0 terse 
Interface               Admin Link Proto    Local                 Remote
fxp0                    up    up
fxp0.0                  up    up   inet     172.19.161.51/24
                                            172.19.161.52/24

{master}
lab@hermes-re0> show version | no-more 
Hostname: alecto-re1
Model: m320
JUNOS Base OS boot [12.3-20140210_dev_x_123_att.0]
......
JUNOS Routing Software Suite [12.3-20140210_dev_x_123_att.0]

{master}
lab@alecto-re1> show interfaces fxp0 terse 
Interface               Admin Link Proto    Local                 Remote
fxp0                    up    up
fxp0.0                  up    up   inet     172.19.161.100/24
                                            172.19.161.102/24
```
]

---


.left-column[
 # basic usage
 ## log files
]

.right-column[
## check the generated log files
* one seperate log file (named from router name) for each router involved in the config file
* new logs will be appended to existing log file
* `log1_YYYYMMDD-HHMMSS.txt` record all interactions
* everytime the script was executed, a new  interaction log (named from
  runtime) will be generated
* everything after issue was detected will be recorded in another log file: `log2_YYYYMMDD-HHMMSS.txt`
```
pings@svl-jtac-tool02:~/temp1$ ls -l
total 72
8764 May  4 17:26 alecto.log    #<------one seperate log file 
4404 May  4 17:26 hermes.log    #<------for each router
 111 May  4 17:21 issuechecker_example1_single.conf
 158 May  4 17:21 issuechecker_example2_multi.conf
 296 May  4 17:21 issuechecker_example3_check.conf
 898 May  4 17:21 issuechecker_example4_replicate.conf
1421 May  4 17:21 issuechecker_example5_replicate_options.conf
1493 May  4 17:21 issuechecker_example6_replicate_collect.conf
1910 May  4 17:21 issuechecker_example7_monitor_change.conf
 659 May  4 17:21 issuechecker_example8_dataexport.conf
2377 May  4 17:22 log1_20140504-172258.txt #<--one log file each 
4751 May  4 17:22 log1_20140504-172323.txt #<--time the script
6962 May  4 17:26 log1_20140504-172351.txt #<--was executed
  51 May  4 17:48 log2_20140504-174839.txt #<--logs after "issue"
```
]

---

class: center, middle, inverse
template: inverse
##usage cases examples

---

layout: false
.left-column[
 # Usage case
 ## 1. single router, info collection
]

.right-column[

### goal: send cmds to one router
* login to one router
* sending command just ONE time
* exit

### config:
`pre_test(ROUTERNAME)` : cmds listed in this array will be sent just one time

config file: issuechecker_single.conf:
```
set pre_test(alecto) {"show version | no-more" "show interfaces fxp0 terse"}
```

or, a better looking format:

```
set pre_test(alecto) {                  
    "show version | no-more" 
    "show interfaces fxp0 terse"
}
```

]

---

.left-column[
 # Usage case
 ## 2. multiple routers, info collection
]

.right-column[
## goal: send commands to multiple routers
* login to multiple routers :hermes and alecto
* send commands to each every routers
* do it just one time

config file: issuechecker_multi.conf:
```
set pre_test(alecto) {
    "show version | no-more" "show interfaces fxp0 terse"
}
set pre_test(hermes)  {
    "show chassis hardware | no-more" "show chassis fpc pic-status"
}
#or, just borrow hermes's cmds if same cmds need to be sent
#set pre_test(hermes) $pre_test(alecto)
```
log files generated:

```
-rw-rw-r--  1 ping ping   51 May  5 19:15 log2_20140505-191500.txt
-rw-rw-r--  1 ping ping 5453 May  5 19:15 log1_20140505-191500.txt
-rw-rw-r--  1 ping ping   51 May  5 19:14 log2_20140505-191427.txt
-rw-rw-r--  1 ping ping 5453 May  5 19:14 log1_20140505-191427.txt
-rw-rw-r-- 1 ping ping   523435 May  3 19:17 alecto.log
-rw-rw-r-- 1 ping ping   238882 May  3 19:17 hermes.log
```
]

---

.left-column[
 # Usage case
 ## 3. multiple iterations - networks monitoring
]

.right-column[
### goal: send commands multiple times (in a loop)
* login to multiple routers :hermes and alecto
* send commands to each every routers
* repeat it over and over (for $maxrounds time)

### config:
* `check(ROUTERNAME)`: cmds listed in this array will be executed `$maxrounds` times, with `$check_intv` interval

config file: `issuechecker_check.conf`:
```
set debug 0
set pre_test(alecto) {
    "show version | no-more" 
    "show interfaces fxp0 terse"
}
set pre_test(hermes) $pre_test(alecto)

#this array "check" will be executed from within a loop!
set check(alecto) {
    "show interfaces ge-1/3/0.601 extensive | match pps"
    "show interfaces ge-1/3/0.602 extensive | match pps"
}
```

]


---

.left-column[
 # Usage case
 ## 4. issues replication
]

.right-column[

## goal: monitor data **value** from specific cmds
* login to multiple routers :hermes and alecto
* send commands to each every routers
* user to define what will be treated as "an issue" (most tricky part of the config)
* "check" (detect) if the issue got hit
* repeat it over and over ($maxrounds time)

config file: `issuechecker_replicate.conf`
```
set pre_test(alecto) {
    "show version | no-more" 
    "show interfaces fxp0 terse"
}
set pre_test(hermes) $pre_test(alecto)

set check(alecto) {
    "show interfaces ge-1/3/0.601 extensive | match pps"
    "show vpls connections instance 13979:333601"
}
set check(hermes) {
    "show interfaces ge-1/2/2.601 extensive | match pps"
    "show vpls connections instance 13979:333601"
}
```

]

---

.left-column[
 # Usage case
 ## 4. issues repli. (cont.)
]

.right-column[

### **user defined tcl code snippet** to define the issue(s):
* `check`\_`code`\_`alecto`\_`1`:`code` defined in this var will apply to the output of the `1`st cmd in `check` array sent to router
  `alecto` - in this case `show interfaces ge-1/3/0.601 extensive | match pps`
* a regex `Input  packets:\s+(\d+)\s+(\d+) pps` was used to match
  a line like:`Input  packets:     13143623       1 pps`
* once found a match, both counters will be captured and saved in 2 vars
  `packets` and `pps`
* if `pps` is 0 (no traffic), return 1 as a flag of "the issue"

```
#(continue..)
#issue definition code:
set check_code_alecto_1 {       #<------
    #match from any line of the output
    set does_match [                                    \
        regexp { Input  packets:\s+(\d+)\s+(\d+) pps }  \
            $cout_line -> packets pps                   \
    ]
    if {($does_match)} {
        if {$pps == 0} {
            myputs "pps 0, no traffic, the issue appears!"
            return 1
        }
    }
}
```
]

---

.left-column[
 # Usage case
 ## 5. options
]

.right-column[


some commonly used options to control(fine tune) the behavior of the script :

config `issuechecker_replicate_options.conf`
```
#print more info about how the script is running (def 1)
set debug 0  #0(quiet), 1(default:brief), 2(verbose), 3(extensive,for debug)
set logfile "log1_pr12345.txt" ;#log file name, optional
#log file that record all info AFTER issue detected, optional
set logfile_issue "log2_pr12345_$runtime.txt" 
set maxfilesize 100000000     ;#max size of each log file(in Bytes) before get gzipped
set log_dir "~/att-jtac-lab-logs"
set check_intv 10             ;#interval between each round check
#set maxrounds 20000          ;#max rounds to check
#set maxrounds_captured 10    ;#max rounds to capture the issue
...same as previous example...
```

logs generated based on above config:
```
ping@ubuntu1404:~/att-jtac-lab-logs$ ls -lct
 1 ping ping    11878 May  5 20:05 log1_pr12345.txt
 1 ping ping  3658 May  5 20:06 log2_pr12345_20140505-200633.txt
 1 ping ping  3658 May  5 20:06 log2_pr12345_20140505-200627.txt
 ......
 1 ping ping  3658 May  5 20:06 log2_pr12345_20140505-200558.txt
 1 ping ping  3658 May  5 20:05 log2_pr12345_20140505-200552.txt
 1 ping ping  3658 May  5 20:05 log2_pr12345_20140505-200546.txt
 1 ping ping  3658 May  5 20:05 log2_pr12345_20140505-200540.txt
```
]

---

.left-column[
 # Usage case
 ## 5. options (cont.)
]

.right-column[

```
...(conti.)...
set login_script attp 
```

### this script currently support to work on both att lab router and jtac lab routers , by setting `login_script` option:
* attp - internal login script: login att router with ping's att account
* attse - internal login script: login att routers with "attse" account
* attjtac - internal login script: login att routers with shared "jtac" account
* attx - user defined external login script
* jtaclab - (default) internal login script: login to jtac lab routers

]

---

.left-column[
 # Usage case
 ## 6. work on att lab routers
]

.right-column[

### goal: send commands to att lab routers
* login to 2 ATT lab routers :pe12 and pe13
* send commands to both routers
* repeat it over and over (for `$maxrounds` times and with `$check_intv`
  seconds interval)

config file `issuechecker_attrouters.conf`:
```
set debug 0              ;#debug level: 1(brief), 3(verbose)
set login_script attjtac ;#login att router with an internal script "attjac"
set logfile "log1_973222_$runtime.txt"
set logfile_issue "log2_973222_$runtime.txt"
set check_intv 5              
set routers {pe12 pe13}       
set check(pe12) [ list        \
  "show vpls connections instance vpls:1501 remote-site 13 | no-more"    \
  "show interfaces xe-0/1/2.2100 extensive | no-more"                    \
  "show configuration apply-groups"                                      \
  {request pfe execute target fpc0 command "show jnh 0 exception terse"} \
  {request pfe execute target fpc4 command "show jnh 0 exception terse"} \
]
set check(pe13) [ list \
  "show vpls connections instance vpls:1501 remote-site 12 | no-more"    \
  "show interfaces xe-0/1/2.2100 extensive | no-more"                    \
  "show configuration apply-groups"                                      \
  {request pfe execute target fpc0 command "show jnh 0 exception terse"} \
  {request pfe execute target fpc4 command "show jnh 0 exception terse"} \
]

```
]

---

.left-column[
 # Usage case
 ## 7. monitor change
]

.right-column[

### **user defined** issue definition code:
* use same regrex as example5, but this time search from both .red[**current**]
  and .red[**previous**] output of same cmd
* in this case: presumption is we "don't trust" the traffic rate reported in `pps`, instead we
  calculate from the 2 run of the same show command and calculate
  "manually", from the packets delta( `packet_now - packet_prev`) and time
  interval(`time now - time_prev`)

config file: `issuechecker_monitor_change.conf`:
```
set check_code_alecto_1 {
    set does_match1 [regexp {Input  packets:\s+(\d+)\s+(\d+) pps}    \
        $cout_line -> packets_now pps                       \
    ]
    set does_match2 [regexp {Input  packets:\s+(\d+)\s+(\d+) pps}    \
        $cout_line_prev -> packets_prev pps_prev        \
    ]
    set rate_expected 6
    if {($does_match1==1) && ($does_match2==1)} {
        set rate_calc [expr ($packets_now - $packets_prev) / ($time_now - $time_prev)]
        set rate_diff_with_expected [expr {abs($rate_calc - $rate_expected)}]
        if { $rate_diff_with_expected >= 5} {
            myputs "issue appears! rate changed too much!"
            return 1       ;#return 1 to indicate issue detection!
        }
    }
}
```

]

---

.left-column[
 # Usage case
 ## 7. network audit
]

.right-column[

###goal:

* export the captured traffic data into a file
* if issue (no traffic) appears , flag the issue and return

config file: `issuechecker_monitor_change.conf`
```
#.. same as prevoius ..
#define the issue:
set check_code_alecto_1 {
    #match from any line of the output
    set does_match [                                    \
        regexp { Input  packets:\s+(\d+)\s+(\d+) pps }  \
            $cout_line -> packets pps                   \
    ]

    if {($does_match)} {

        #export data to a file, in csv format
        set dataformat {"%s,%s"}   #<------use csv as data format
        set data "$packets $pps"   #<------data to export 
        set datafile "test.csv"    #<------file name

        if {$pps == 0} {
            myputs "pps 0, no traffic, the issue appears!"
            return 1
        }
    }
}
```

]

---

.left-column[
 # Usage case
 ## 7. network audit (continue..)
]

.right-column[

###exported data: test.csv
```
rtr,timestamp(UTC),packets,pps
==============================
alecto,1397955020,11090109,0
alecto,1397955032,11090111,0
alecto,1397955043,11090112,0
alecto,1397955055,11090114,0
alecto,1397955067,11090115,0
alecto,1397955079,11090116,0
alecto,1397955091,11090118,0
alecto,1397955103,11090119,0
alecto,1397955115,11090120,0
```
]

---

.left-column[
 # Usage case
 ## 9. monitoring intermittent issue
]

.right-column[

###goal:

* if issue appears, take action1:
  * collect more extensive info , backup logs , etc.
  * email notification: "issue appears!"
  * `collect`: cmds list in this array will be executed only **AFTER the
  issue was detected**

* otherwise, take action2 before next iteration:
  * config change , GRES , etc..
  * `test`: cmds list in this array will be executed only **if the issue didn't
  appear**

]

---

.left-column[
 # Usage case
 ## 9. monitoring intermittent issue (conti.)
]

.right-column[

config file: `issuechecker_replicate_info.conf`
```
...same as issuechecker_replicate.conf, plus...
#if issue got replicated, action1: collect more info and backup log
set collect(alecto) [ list 				        \
    "show interfaces ge-1/3/0.601 extensive | no-more"          \
    "file copy /var/log/messages messages-issue"                \
    "start shell pfe network"                                   \
    "show syslog messages"                                      \
    "exit"                                                      \
] 

#otherwise (issue not appear), action2: rollback config and re-test
set test(alecto) [ list                         \
    "configure private"                         \
    "rollback 1"                                \
    "show | compare | last 40 | no-more"        \
    "exit"                                      \
]
set test(hermes) $test(alecto)

```
]


---


.left-column[
 # Usage case
 ## 10. alternating test
]

.right-column[

## goal: run different cmds in each round
* `test1` ~ `test10`: cmds list in these arrays will be executed alternatively
  and execlusively in each iteration
* run `test1` in 1st round, `test2` in 2nd round, ...`test4` in 4th round, 
     `test1` in 5th round , `test2` in 6th round... and so on
* if any of these exist, `test` array will be ignored/skipped

```
set test1(alecto) [ list           \
    "configure private"         \
    "rollback 1" "show | compare | last 40 | no-more" \
    "commit"                    \
    "exit"                      \
]

set test2(hermes) $test1(alecto)
set test3(alecto) $test1(alecto)
set test4(hermes) $test1(alecto)
```
]

---

.left-column[
 # Usage case
 ## more complex conditions
 ### 
]

.right-column[

* issues might depend on different result from multiple commands - logical operations

```
set flag_check_method 1 ;#default, condition matched in any single cmd flag a hit to an issue
```

.t.b.c
]

---

name: last-page
template: inverse

    </textarea>
    <script src="http://gnab.github.com/remark/downloads/remark-0.6.0.min.js" type="text/javascript"></script>
    <script type="text/javascript">
      var hljs = remark.highlighter.engine;
    </script>
    <script src="remark.language.js" type="text/javascript"></script>
    <script type="text/javascript">
      var slideshow = remark.create({
          highlightStyle: 'monokai',
          highlightLanguage: 'remark'
        }) ;
    </script>
    <script type="text/javascript">
      var _gaq = _gaq || [];
      _gaq.push(['_setAccount', 'UA-44561333-1']);
      _gaq.push(['_trackPageview']);

      (function() {
        var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
        ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
        var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
      })();
    </script>
  </body>
</html>

