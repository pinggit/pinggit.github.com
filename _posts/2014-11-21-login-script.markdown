---
layout: post
title: "a generic login script: crtc"
published: true
created:  2014 Nov 21 02:28:16 PM
tags: [tcl, expect, script]
categories: [tech]

---

TABLE OF CONTENT

* auto-gen TOC:
{:toc}

- - -

info in this blog was obsolete since the crtc script has been updated,
documented in [another doc ](http://www-in.juniper.net/~pings/myblog/docs/scripts/crtc.html).

# introduction

Old topic: There were no good ways to interact with a remote host/router from within a
shell script...expect script might be the best in this field.

Tthe goal of implementing this script is to automate the login process to ANY
remote (even local) devices , (junos, cisco, linux server, erx, ...), with
whatever existing tools avaiable in the local machine (ssh, telnet,ftp, rcp,
sftp, your own scripts, etc) . there is really no presumption/limitation about
what protocols the login was based, Telnet/SSH are the most commonly used
protocols though.

something like the "secureCRT", but in command line mode. so it is much
smaller/agiler and may become more useful.

one major benefit of using a script (command line) is that, it is much easier to be
integrated into other tools, being it a perl/shell/python/tcl script, or
even another instance of the same script.

this small script currently supports most of the features I could expected from
other commercial tools dealing with interactive sessions (e.g. secureCRT).
I'll extend it whenever I feel other useful features/options can be added.

# run the script

## the script: just one file
Written in pure basic expect code, this script requires no dependencies to any
external libs/files. It (should) just runs on any platforms with standard
tcl/expect tool installed.

the very basic usage:

    /homes/pings/bin/crtc HOST

just 1 single file in server svl-jtac-tool02: 

    [pings@svl-jtac-tool02 ~]$
    [pings@svl-jtac-tool02 ~]$ cd bin
    [pings@svl-jtac-tool02 ~/bin]$ ls -l | grep -E "crtc$"   #<------
    -rwxr-xr-x   1 pings  others    5802 Nov 21 10:48 crtc

it already has the login data of Juniper JTAC routers configured, so without
any extra configuration, it can be used to login any JTAC routers (mgmt and
console).

## config file
an extra config file is needed if:
* you might want to maintain your own server database
* you might prefer to change the options to control the login behavior

a config file template can be copied from below location:

        [pings@svl-jtac-tool02 ~]$ pwd
        /homes/pings
        [pings@svl-jtac-tool02 ~]$ ls -l | grep crtc.conf
        -rw-r--r--   1 pings  others      12045 Nov 21 10:58 crtc.conf     #<------

## install to your own folder

copy the 2 files to your home:

    yourserver#cd
    (yourhome)#cp -r /homes/pings/crtc.conf ~/
    (yourhome)#cp -r /homes/pings/bin/crtc ~/
    (yourhome)#chmod 755 crtc

optionally: change the `PATH` and make the system to be able to location this
script when executed

    (yourhome)#export PATH=$PATH:~

## add your own data
to add the login info of your own remote devices that your are going to login
with this script, edit the crtc.conf file (with vi, vim, whatever editor) 

    vim ~/crtc.conf

add your own server entries and login data:

    set login_info(myserver)       [list  \
        "$"        "ssh bob@123.1.1.1"    \
        "Password:"    "mypass"           \
        "$"            "date"             \
    ]

run the script from your home:

    #crtc myserver

see more usage examples see below.


# usage examples

## options list

    ping@ubuntu1404:~$ crtc -h                                                
    Usage:/home/ping/bin/crtc [OPTIONS] session
           OPTIONS:
             -A               :auto-paging (no-more)
             -d/U             :print debug info
             -c "show version | no-more"
             -C <config file|NONE> :read config file
             -e ">" -s "show version | no-more"
             -h               :help
             -i <SECONDS>     :interval
             -k/K             :exit session also exit script
             -l               :list configured hosts
             -m               :monitoring mode,keep sending cmds
             -n <count>       :send command <count> time(s)
             -o/O             :login only (ignore all provided cmds)
             -p/P             :persist mode(todo)
             -q/Q             :quick mode: quit after done
             -r <SECONDS>     :reconnect interval
             -u/U             :hidden mode (hide login steps)
             -v               :version info
          KEYS:
             <c-z>            :run the session in background
             !e               :edit config file
             !l               :print configured hosts
             !L               :peek the log file
          SPECIAL CMDS:
             GRES             :Junos GRES request
             SLEEP <SECONDS>  :sleep some seconds before sending next command

there is one rule: the session name must be the last parameter

## login to juniper lab devices

config :

    set login_info(alecto)       [list               \
        "$"        "telnet alecto.$domain_suffix"    \
        "login: "      "lab"                        \
        "Password:"    "herndon1"                   \
        ">"            "set cli screen-width 300"   \
        ">"            "set cli timestamp"          \
    ]

login:

    ping@ubuntu1404:~/bin$ crtc alecto                                   
    current log file ~/att-lab-logs/alecto.log                            
    telnet alecto.jtac-east.jnpr.net                                      
    ping@ubuntu1404:~/bin$ telnet alecto.jtac-east.jnpr.net               
    Trying 172.19.161.100...                                              
    Connected to alecto.jtac-east.jnpr.net.                               
    Escape character is '^]'.                                             
                                                                          
    alecto-re0 (ttyp0)                                                    
                                                                          
    login: lab                                                            
    Password:                                                             
                                                                          
    --- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC 
    At least one package installed on this device has limited support.    
    Run 'file show /etc/notices/unsupported.txt' for details.             
    {master}                                                              
    lab@alecto-re0> set cli screen-width 300                              
    Screen width set to 300                                               
                                                                          
    {master}                                                              
    lab@alecto-re0> set cli timestamp                                     
                                                                          
    Nov 21 12:31:01                                                       
    CLI timestamp set to: %b %d %T                                        
                                                                          
    {master}                                                              
    lab@alecto-re0>                                                       

## login to any router in a group "jtac" 

all routers under a group share the same login steps

config:

     set domain_suffix_con jtac-west.jnpr.net
     set domain_suffix jtac-east.jnpr.net

     #define a new category "jtac" for all jtac devices
     set login_info($session@jtac)       [list               \
         "$"        "telnet $host.$domain_suffix"    \
         "login: "      "lab"                        \
         "Password:"    "herndon1"                   \
         ">"            "set cli screen-width 300"   \
         ">"            "set cli timestamp"          \
     ]

login:

    ping@ubuntu1404:~/bin$ crtc tintin@jtac                 
    spawn /bin/bash                                          
    current log file ~/att-lab-logs/tintin.log               
    telnet tintin.jtac-east.jnpr.net                         
    ping@ubuntu1404:~/bin$ telnet tintin.jtac-east.jnpr.net  
    Trying 172.19.161.18...                                  
    Connected to tintin.jtac-east.jnpr.net.                  
    Escape character is '^]'.                                
     Warning Notice                                          
                                                             
    Please contact Pratima or Brian before making any changes
                                                             
    tintin-re0 (ttyp0)                                       

## login to console of juniper device

config:

the trick is to load the hostmap data provided by lab admin, the data defines
which terminal server and port number that is going to be used when login the
console of a specific router (via a fake hostname:xxx-rex-con).  the tcl
`regexp` command is used to extract these info out of the mapping.

    #juniper jtac lab: map session name to terminal server data
    array set hostmap {\
        ......
        eros-re0-con                        b6tsb17:7015    \
        eros-re1-con                        b6tsb17:7016    \
        alecto-re0-con                      b6tsb17:7021    \
        alecto-re1-con                      b6tsb17:7022    \
        rams-re0-con                        b6tsa26:7023    \
        bills-re0-con                       b6tsa26:7024    \
        bears-re0-con                       b6tsb09:7013    \
        chargers-re0-con                    b6tsb09:7014    \
        ......
    }

    #domains
    set domain_suffix_con jtac-west.jnpr.net
    set domain_suffix jtac-east.jnpr.net

    #parse the terminal server data, 
    #for console:extract terminal server name and port number
    #otherwise use telnet to login
    if [regexp {(\w+):(\d+)} $host -> terminal_server port] {
        set login_string "telnet $terminal_server.$domain_suffix_con $port"
    } else {
        set login_string "telnet $host.$domain_suffix"
    }

    #define a new category "jtac" for all jtac devices
    set login_info($session@jtac)       [list           \
        "$"        "$login_string"                      \
        "login: "      "lab"                            \
        "Password:"    "herndon1"                       \
        ">"            "set cli screen-width 300"       \
        ">"            "set cli timestamp"              \
    ]

login:

    ping@ubuntu1404:~$ crtc alecto-re0-con@jtac                             
    current log file ~/att-lab-logs/b6tsb17:7021.log                        
    telnet b6tsb17.jtac-west.jnpr.net 7021                                  
    ping@ubuntu1404:~$ telnet b6tsb17.jtac-west.jnpr.net 7021               
    Trying 172.22.194.102...                                                
    Connected to b6tsb17.jtac-west.jnpr.net.                                
    Escape character is '^]'.                                               
                                                                            
    Type the hot key to suspend the connection: <CTRL>Z                     
                                                                            
                                                                            
    alecto-re0 (ttyd0)                                                      
                                                                            
    login: lab                                                              
    Password:                                                               
                                                                            
    --- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC   
    {backup}                                                                
    lab@alecto-re0> set cli screen-width 300                                
    Screen width set to 300                                                 
                                                                            
    {backup}                                                                
    lab@alecto-re0> set cli timestamp                                       
                                                                            
    Nov 24 08:09:27                                                         
    CLI timestamp set to: %b %d %T                                          
                                                                            
    {backup}                                                                
    lab@alecto-re0> it's all yours now!:)                                   
                                                                            
    Nov 24 08:09:28                                                         
                                                                            
    {backup}                                                                
    lab@alecto-re0>                                                         

to logout, `exit` won't kick yourself out, press `ctrl-]` and then type `quit`

    {backup}            
    lab@alecto-re0> exit
    Nov 24 08:10:05     
                        
                        
    alecto-re0 (ttyd0)  
                        
    login:              
    telnet> quit        
    Connection closed.  

## login to ATT qfx switches

config:

    set login_info(qfx11@att)       [list           \
        "$"        "ssh svl-jtac-tool02"            \
        "$"         "ssh jtac@12.40.233.51"         \
        "assword:"  "321jtac"                       \
        "Enter Option:"     "11"                    \
        "assword:"  "321jtac"                       \
        ">"         "set cli screen-width 300"      \
        ">"         "set cli timestamp"             \
    ]

    login:

    ping@ubuntu1404:~/bin$ crtc qfx11@att                                        
    current log file ~/att-lab-logs/qfx11.log                                     
    ssh svl-jtac-tool02                                                           
    ssh jtac@12.40.233.51                                                         
    ping@ubuntu1404:~/bin$ ssh svl-jtac-tool02                                    
    Last login: Fri Nov 21 10:20:35 2014 from 172.25.163.165                      
    Copyright (c) 1980, 1983, 1986, 1988, 1990, 1991, 1993, 1994                  
            The Regents of the University of California.  All rights reserved.    
                                                                                  
    FreeBSD 7.4-RELEASE (PAE) #0: Tue Jul 23 08:43:51 PDT 2013                    
                                                                                  
    ******************************************************************************
    **                                                                          **
    **      Hostname:               svl-jtac-tool02.juniper.net                 **
    **      IP Address:             172.17.31.81                                **
    **      Internet Address:       66.129.239.20                               **
    **      Operating System:       FreeBSD 7.4-RELEASE                         **
    **                                                                          **
    ******************************************************************************
    For operational availability issues, contact helpdesk.                        
    For functional enhancement requests, contact jboyle                           
    ******************************************************************************
    JTAC Shell Servers:  svl-jtac-tool01, svl-jtac-tool02, wfd-jtac-tool01        
    ******************************************************************************
                                                                                  
    ** Saturday Nov 22 12:00p,                                                    
      Proactive reboot planned to clean up stray processes after filer issues     
    ssh jtac@12.40.233.51                                                         
    [pings@svl-jtac-tool02 ~]$ ssh jtac@12.40.233.51                              
    Warning: Permanently added '12.40.233.51' (DSA) to the list of known hosts.   
    jtac@12.40.233.51's password:                                                 
    Last login: Fri Nov 21 12:27:08 2014 from 66.129.239.20                       
    #               For Authorized Use Only                                       
    #                                                                             
    # All of activities on this system are monitored. Anyone using this system    
    # expressly consents to such monitoring and is advised                        
    # that if such monitoring reveals possible evidence of criminal activity,     
    # system personnel may provide the evidence of such monitoring to law         
    # enforcement officals and may be executed to the fullest extent of law       
    #                                                                             
    #                                                                             
                 0.  EXIT                                                         
    1.  lzncce01            2.  lzncce02                                          
    3.  localhost           4.  lznsun02                                          
    5.  lzncce03            6.  lzncce04                                          
    7.  lzncce05            8.  lzncce10                                          
    9.  mtpnjtax100         10. mtanjtax100                                       
    11. mttnjtax100         12. ngects01                                          
    13. ngemfc3             14. ngomfc3                                           
    15. ngemfc5             16. ngomfc2                                           
    17. lzncce06            18. lzncce07                                          
    19. lzncce08            20. ngomfa1                                           
    21. ngomfa2             22. ngemfc11                                          
    23. mtinjlsic03           24. cipcce1                                         
    25. ngecce2             26. cipcce2                                           
    27. ngemfc4               28. ngomfa3                                         
    29. ngomfa4               30. ngOpac4                                         
    31. ngemfc9             32. mtinj003ts                                        
    33. ngemfc10              34. RouteServer                                     
    35. ngecce3             36. ngemfc6                                           
    38. ngemfc7             38. ngemfc8                                           
    39. mtinj00001cce9        40. mtinj00002cce9                                  
    41. mtenj00001cce9        42.mtenj00002cce9                                   
    43. mtpnj00001cce9        44.mtpnj00002cce9                                   
    45. mtanj00001cce9                                                            
    Enter Option: 11                                                              
                          Warning Notice                                          
                                                                                  
    This system is restricted solely to AT&T authorized users                     
    for legitimate business purpose only. The actual or attempted                 
    unauthorized access, use or modification of this system is                    
    strictly prohibited by AT&T. Unauthorized users are subject to                
    Company disciplinary proceedings and/or criminal and civil       
    penalities under state, federal or other applicable domestic and 
    foreign laws. The use of this system may be monitored and        
    recorded for administrative and security reasons. Anyone         
    accessing this system expressly consents to such monitoring      
    and is advised that if monitoring reveals possible evidence of   
    criminal activity, AT&T may provide the evidence of such         
    activity to law enforcement officials.All users must comply with 
    AT&T company policies regarding the protection of AT&T           
    information assets.;                                             
            For Tier Support send email to dl-cce@att.com            
    Password:                                                        
    --- JUNOS 13.2X51-D30_vjunos.50 built 2014-11-21 03:45:16 UTC    
    {master:0}                                                       
    jtac@mttnjtax101> set cli screen-width 300                       
    Screen width set to 300                                          
                                                                     
    {master:0}                                                       
    jtac@mttnjtax101> set cli timestamp                              
    Nov 22 02:18:05                                                  
    CLI timestamp set to: %b %d %T                                   
                                                                     
    {master:0}                                                       
    jtac@mttnjtax101>                                                

## send extra commands on successful login

`-c "CMDS"` option(can use multiple times):

    ping@ubuntu1404:~/bin$ crtc -c "show version | no-more" -c "show system uptime" alecto
    current log file ~/att-lab-logs/alecto.log                                     
    telnet alecto.jtac-east.jnpr.net                                               
    ping@ubuntu1404:~/bin$ telnet alecto.jtac-east.jnpr.net                        
    Trying 172.19.161.100...                                                       
    Connected to alecto.jtac-east.jnpr.net.                                        
    Escape character is '^]'.                                                      
                                                                                   
    alecto-re0 (ttyp0)                                                             
                                                                                   
    login: lab                                                                     
    Password:                                                                      
                                                                                   
    --- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC          
    At least one package installed on this device has limited support.             
    Run 'file show /etc/notices/unsupported.txt' for details.                      
    {master}                                                                       
    lab@alecto-re0> set cli screen-width 300                                       
    Screen width set to 300                                                        
                                                                                   
    {master}                                                                       
    lab@alecto-re0> set cli timestamp                                              
                                                                                   
    Nov 21 12:44:18                                                                
    CLI timestamp set to: %b %d %T                                                 
                                                                                   
    {master}                                                                       
    lab@alecto-re0> show version | no-more                                         
    Nov 21 12:44:18                                                                
    Hostname: alecto-re0                                                           
    Model: m320                                                                    
    JUNOS Base OS boot [12.3-20140210_dev_x_123_att.0]                             
    JUNOS Base OS Software Suite [12.3-20140210_dev_x_123_att.0]           
    JUNOS Packet Forwarding Engine Support (M320) [12.3-20140210_dev_x_123_att.0]  
    ...
                                                                                   
    {master}                                                                       
    lab@alecto-re0> show system uptime                                 
    Nov 21 12:49:35                                                    
    Current time: 2014-11-21 12:49:35 EST                              
    System booted: 2014-08-24 17:55:36 EDT (12w4d 19:53 ago)           
    Protocols started: 2014-08-24 17:56:49 EDT (12w4d 19:52 ago)       
    Last configured: 2014-10-23 17:00:25 EDT (4w0d 20:49 ago) by lab   
    12:49PM  up 88 days, 19:54, 1 user, load averages: 0.22, 0.14, 0.09
                                                                       
    {master}                                                           
    lab@alecto-re0>                                                    

    ping@ubuntu1404:~/bin$ crtc -c "show version | no-more" -c "show system uptime" -H -n 3 -i 5 -q alecto@jtac | grep -i
    "current time"
    current log file ~/att-lab-logs/alecto.log
    Current time: 2014-11-21 11:03:19 EST
    Current time: 2014-11-21 11:03:24 EST
    Current time: 2014-11-21 11:03:29 EST
    ping@ubuntu1404:~/bin$


## hide login details

`-H option`:

    ping@ubuntu1404:~/bin$ crtc -c "show version | no-more" -H alecto                                
    current log file ~/att-lab-logs/alecto.log                                                        
    set cli timestamp                                                                                 
                                                                                                      
    Nov 21 12:46:48                                                                                   
    CLI timestamp set to: %b %d %T                                                                    
                                                                                                      
    {master}                                                                                          
    lab@alecto-re0> show version | no-more                                                            
    Nov 21 12:46:49                                                                                   
    Hostname: alecto-re0                                                                              
    Model: m320                                                                                       
    JUNOS Base OS boot [12.3-20140210_dev_x_123_att.0]                                                
    JUNOS Base OS Software Suite [12.3-20140210_dev_x_123_att.0]                                      
    JUNOS 64-bit Kernel Software Suite [12.3-20140210_dev_x_123_att.0]                                


## "quick" mode: login, send cmds, and exit

`-q option`:

this is useful for quick test in shell script: login to a router, grab the data, then exit

    ping@ubuntu1404:~/bin$ crtc -c "show system uptime" -H -q alecto     
    current log file ~/att-lab-logs/alecto.log                            
    set cli timestamp                                                     
                                                                          
    Nov 21 12:52:29                                                       
    CLI timestamp set to: %b %d %T                                        
                                                                          
    {master}                                                              
    lab@alecto-re0> show system uptime                                    
    Nov 21 12:52:29                                                       
    Current time: 2014-11-21 12:52:29 EST                                 
    System booted: 2014-08-24 17:55:36 EDT (12w4d 19:56 ago)              
    Protocols started: 2014-08-24 17:56:49 EDT (12w4d 19:55 ago)          
    Last configured: 2014-10-23 17:00:25 EDT (4w0d 20:52 ago) by lab      
    12:52PM  up 88 days, 19:57, 1 user, load averages: 0.02, 0.09, 0.08   
                                                                          
    {master}                                                              
    lab@alecto-re0> [Fri Nov 21 12:51:56 EST 2014::..bye!:)..]            

## keep sending cmds in a loop ("monitoring" mode)

`-n N -i INTERVAL` options:

this is useful to monitor some specific cmds for some iterations

    ping@ubuntu1404:~/bin$ crtc -c "show system alarm" -n 3 -i 5 -q alecto  
    current log file ~/att-lab-logs/alecto.log                               
    telnet alecto.jtac-east.jnpr.net                                         
    ping@ubuntu1404:~/bin$ telnet alecto.jtac-east.jnpr.net                  
    Trying 172.19.161.100...                                                 
    Connected to alecto.jtac-east.jnpr.net.                                  
    Escape character is '^]'.                                                
                                                                             
    alecto-re0 (ttyp0)                                                       
                                                                             
    login: lab                                                               
    Password:                                                                
                                                                             
    --- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC    
    At least one package installed on this device has limited support.       
    Run 'file show /etc/notices/unsupported.txt' for details.                
    {master}                                                                 
    lab@alecto-re0> set cli screen-width 300                                 
    Screen width set to 300                                                  
                                                                             
    {master}                                                                 
    lab@alecto-re0> set cli timestamp                                        
                                                                             
    Nov 21 12:56:14                                                          
    CLI timestamp set to: %b %d %T                                           
                                                                             
    {master}                                                                 
    lab@alecto-re0> show system alarm                                        
    Nov 21 12:56:14s                                                         
    3 alarms currently active                                                
    Alarm time               Class  Description                              
    2014-08-24 17:57:54 EDT  Major  FPC 4 PIC 0 Failure                      
    2014-08-24 17:56:51 EDT  Minor  PEM 1 Absent                             
    2014-08-24 17:56:51 EDT  Minor  PEM 0 Absent                             
                                                                             
    {master}                                                                 
    lab@alecto-re0> show system alarm                                        
    Nov 21 12:56:19s                                                         
    3 alarms currently active                                                
    Alarm time               Class  Description                              
    2014-08-24 17:57:54 EDT  Major  FPC 4 PIC 0 Failure                      
    2014-08-24 17:56:51 EDT  Minor  PEM 1 Absent                             
    2014-08-24 17:56:51 EDT  Minor  PEM 0 Absent                             
                                                                             
    {master}                                                                 
    lab@alecto-re0> show system alarm                                        
    Nov 21 12:56:24s                                                         
    3 alarms currently active                                                
    Alarm time               Class  Description                              
    2014-08-24 17:57:54 EDT  Major  FPC 4 PIC 0 Failure                      
    2014-08-24 17:56:51 EDT  Minor  PEM 1 Absent                             
    2014-08-24 17:56:51 EDT  Minor  PEM 0 Absent                             
                                                                             
    {master}                                                                 
    lab@alecto-re0> [Fri Nov 21 12:55:56 EST 2014::..bye!:)..]               

this can be shortened by -m option, the cmds will be sent endless time, with
whatever interval configured in the config file. default interval is 0, meaning
to send as fast as the router can response.

    set interval 0

login:

    ping@ubuntu1404:~/bin$ crtc -c "show system alarm" -m -H alecto    
    current log file ~/att-lab-logs/alecto.log                          
    set cli timestamp                                                   
                                                                        
    Nov 21 13:01:17                                                     
    CLI timestamp set to: %b %d %T                                      
                                                                        
    {master}                                                            
    lab@alecto-re0> show system alarm                                   
    Nov 21 13:01:18s                                                    
    3 alarms currently active                                           
    Alarm time               Class  Description                         
    2014-08-24 17:57:54 EDT  Major  FPC 4 PIC 0 Failure                 
    2014-08-24 17:56:51 EDT  Minor  PEM 1 Absent                        
    2014-08-24 17:56:51 EDT  Minor  PEM 0 Absent                        
                                                                        
    {master}                                                            
    lab@alecto-re0> show system alarm                                   
    Nov 21 13:01:18s                                                    
    3 alarms currently active                                           
    Alarm time               Class  Description                         
    2014-08-24 17:57:54 EDT  Major  FPC 4 PIC 0 Failure                 
    2014-08-24 17:56:51 EDT  Minor  PEM 1 Absent                        
    2014-08-24 17:56:51 EDT  Minor  PEM 0 Absent                        
                                                                        
    {master}                                                            
    lab@alecto-re0> show system alarm                                   
    Nov 21 13:01:18s                                                    
    3 alarms currently active                                           
    Alarm time               Class  Description                         
    2014-08-24 17:57:54 EDT  Major  FPC 4 PIC 0 Failure                 
    2014-08-24 17:56:51 EDT  Minor  PEM 1 Absent                        
    2014-08-24 17:56:51 EDT  Minor  PEM 0 Absent                        
                                                                        


## everything together

in a shell script, you might want to get realtime output data of some command.
and then contiue to parse the collected data.
unless you are scripting directly within the router (.e.g. Junos shell mode)
this involves at least the following steps:

* login to the router
* send one or more commands
* repeat it 3 times, with 5s interval between each iteration
* collected the output for your analysis 
* trim other texts (e.g the text of the login procedures)
* then disconnect once above done 

here is how things can be done with this tool, one-liner:

    ping@ubuntu1404:~/bin$ crtc -c "show system alarm" -c "show system uptime" -n 3 -i 5 -q -H alecto 
    current log file ~/att-lab-logs/alecto.log                                                         
    set cli timestamp                                                                                  
                                                                                                       
    Nov 21 13:04:17                                                                                    
    CLI timestamp set to: %b %d %T                                                                     
                                                                                                       
    {master}                                                                                           
    lab@alecto-re0> show system alarm                                                                  
    Nov 21 13:04:17s                                                                                   
    3 alarms currently active                                                                          
    Alarm time               Class  Description                                                        
    2014-08-24 17:57:54 EDT  Major  FPC 4 PIC 0 Failure                                                
    2014-08-24 17:56:51 EDT  Minor  PEM 1 Absent                                                       
    2014-08-24 17:56:51 EDT  Minor  PEM 0 Absent                                                       
                                                                                                       
    {master}                                                                                           
    lab@alecto-re0> show system uptime                                                                 
    Nov 21 13:04:17                                                                                    
    Current time: 2014-11-21 13:04:17 EST                                                              
    System booted: 2014-08-24 17:55:36 EDT (12w4d 20:08 ago)                                           
    Protocols started: 2014-08-24 17:56:49 EDT (12w4d 20:07 ago)                                       
    Last configured: 2014-10-23 17:00:25 EDT (4w0d 21:03 ago) by lab                                   
     1:04PM  up 88 days, 20:09, 1 user, load averages: 0.00, 0.07, 0.07                                
                                                                                                       
    {master}                                                                                           
    lab@alecto-re0> show system alarm                                                                  
    Nov 21 13:04:22s                                                                                   
    3 alarms currently active                                                                          
    Alarm time               Class  Description                                                        
    2014-08-24 17:57:54 EDT  Major  FPC 4 PIC 0 Failure                                                
    2014-08-24 17:56:51 EDT  Minor  PEM 1 Absent                                                       
    2014-08-24 17:56:51 EDT  Minor  PEM 0 Absent                                                       
                                                                                                       
    {master}                                                                                           
    lab@alecto-re0> show system uptime                                                                 
    Nov 21 13:04:22                                                                                    
    Current time: 2014-11-21 13:04:22 EST                                                              
    System booted: 2014-08-24 17:55:36 EDT (12w4d 20:08 ago)                                           
    Protocols started: 2014-08-24 17:56:49 EDT (12w4d 20:07 ago)                                       
    Last configured: 2014-10-23 17:00:25 EDT (4w0d 21:03 ago) by lab                                   
     1:04PM  up 88 days, 20:09, 1 user, load averages: 0.00, 0.07, 0.07                                
                                                                                                       
    {master}                                                                                           
    lab@alecto-re0> show system alarm                                                                  
    Nov 21 13:04:27s                                                                                   
    3 alarms currently active                                                                          
    Alarm time               Class  Description                                                        
    2014-08-24 17:57:54 EDT  Major  FPC 4 PIC 0 Failure                                                
    2014-08-24 17:56:51 EDT  Minor  PEM 1 Absent                                                       
    2014-08-24 17:56:51 EDT  Minor  PEM 0 Absent                                                       
                                                                                                       
    {master}                                                                                           
    lab@alecto-re0> show system uptime                                                                 
    Nov 21 13:04:27                                                                                    
    Current time: 2014-11-21 13:04:27 EST                                                              
    System booted: 2014-08-24 17:55:36 EDT (12w4d 20:08 ago)                                           
    Protocols started: 2014-08-24 17:56:49 EDT (12w4d 20:07 ago)                                       
    Last configured: 2014-10-23 17:00:25 EDT (4w0d 21:04 ago) by lab                                   
     1:04PM  up 88 days, 20:09, 1 user, load averages: 0.00, 0.07, 0.07                                
                                                                                                       
    {master}                                                                                           
    lab@alecto-re0> [Fri Nov 21 13:03:59 EST 2014::..bye!:)..]                                         

## special "commands"

### `GRES` command (Junos platform specific)

to request GRES to a dual-RE Junos device, simply use the `GRES` command:

    crtc -c GRES alecto                                                   

an example:

    ping@ubuntu1404:~$ crtc -c GRES alecto                                                   
    current log file ~/att-lab-logs/alecto.log                                               
    telnet alecto.jtac-east.jnpr.net                                                         
    ping@ubuntu1404:~$ telnet alecto.jtac-east.jnpr.net                                      
    Trying 172.19.161.100...                                                                 
    Connected to alecto.jtac-east.jnpr.net.                                                  
    Escape character is '^]'.                                                                
                                                                                             
    alecto-re1 (ttyp0)                                                                       
                                                                                             
    login: lab                                                                               
    Password:                                                                                
                                                                                             
    --- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC                    
    {master}                                                                                 
    lab@alecto-re1> set cli screen-width 300                                                 
    Screen width set to 300                                                                  
                                                                                             
    {master}                                                                                 
    lab@alecto-re1> set cli timestamp                                                        
                                                                                             
    Nov 23 01:21:42                                                                          
    CLI timestamp set to: %b %d %T                                                           
                                                                                             
    {master}                                                                                 
    lab@alecto-re1>                                                                          
    Nov 23 01:21:42                                                                          
                                                                                             
    {master}                                                                                 
    lab@alecto-re1> request chassis routing-engine master switch                             
    Nov 23 01:21:42                                                                          
    Toggle mastership between routing engines ? [yes,no] (no) yes                            
    Nov 23 01:21:43                                                                          
                                                                                             
    Resolving mastership...                                                                  
    Complete. The other routing engine becomes the master.                                   
                                                                                             
    {backup}                                                                                 
    lab@alecto-re1> [Sun Nov 23 01:21:09 EST 2014::..[great! will exit current session...]..]
    exit                                                                                     
    Nov 23 01:21:43                                                                          
    Connection closed by foreign host.                                                       
    [Sun Nov 23 01:21:09 EST 2014::..will reconnect in 30s..]                                
    ping@ubuntu1404:~$ telnet alecto.jtac-east.jnpr.net                                      
    Trying 172.19.161.100...                                                                 
    Connected to alecto.jtac-east.jnpr.net.                                                  
    Escape character is '^]'.                                                                
                                                                                             
    alecto-re0 (ttyp0)                                                                       
                                                                                             
    login: lab                                                                               
    Password:                                                                                
                                                                                             
    --- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC                    
    {master}                                                                                 
    lab@alecto-re0> set cli screen-width 300                                                 
    Screen width set to 300                                                                  

there is a tricky part in Junos GRES - if you do it too frequent, say, do it
again in less than 4m after the previous execution, the router will reject the
request with a message. The tool can handle this well:

    ping@ubuntu1404:~$ crtc -c GRES alecto                                                                 
    current log file ~/att-lab-logs/alecto.log                                                             
    telnet alecto.jtac-east.jnpr.net                                                                       
    ping@ubuntu1404:~$ telnet alecto.jtac-east.jnpr.net                                                    
    Trying 172.19.161.100...                                                                               
    Connected to alecto.jtac-east.jnpr.net.                                                                
    Escape character is '^]'.                                                                              
                                                                                                           
    alecto-re0 (ttyp0)                                                                                     
                                                                                                           
    login: lab                                                                                             
    Password:                                                                                              
                                                                                                           
    --- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC                                  
    {master}                                                                                               
    lab@alecto-re0> set cli screen-width 300                                                               
    Screen width set to 300                                                                                
                                                                                                           
    {master}                                                                                               
    lab@alecto-re0> set cli timestamp                                                                      
                                                                                                           
    Nov 23 01:36:24                                                                                        
    CLI timestamp set to: %b %d %T                                                                         
                                                                                                           
    {master}                                                                                               
    lab@alecto-re0>                                                                                        
    Nov 23 01:36:24                                                                                        
                                                                                                           
    {master}                                                                                               
    lab@alecto-re0> request chassis routing-engine master switch                                           
    Nov 23 01:36:25                                                                                        
    Toggle mastership between routing engines ? [yes,no] (no) yes                                          
    Nov 23 01:36:26                                                                                        
                                                                                                           
    Command aborted. Not ready for mastership switch, try after 221 secs.                                       #<------
                                                                                                           
    {master}                                                                                               
    lab@alecto-re0> [Sun Nov 23 01:35:52 EST 2014::..[script:ops! sorry...will redo 221s later then...]..]      #<------
    Nov 23 01:42:50                                                                            
                                                                                               
    {master}                                                                                   
    lab@alecto-re0> request chassis routing-engine master switch                                                #<------
    Nov 23 01:42:50                                                                            
    Toggle mastership between routing engines ? [yes,no] (no) yes                              
    Nov 23 01:42:51                                                                            
                                                                                               
    Resolving mastership...                                                                    
    Complete. The other routing engine becomes the master.                                     
                                                                                               
    {backup}                                                                                   
    lab@alecto-re0> [Sun Nov 23 01:42:18 EST 2014::..[great! will exit current session...]..]  
    exit                                                                                       
    Nov 23 01:42:51                                                                            
    Connection closed by foreign host.                                                         
    [Sun Nov 23 01:42:18 EST 2014::..will reconnect in 30s..]                                  
    ping@ubuntu1404:~$ telnet alecto.jtac-east.jnpr.net                                        
    Trying 172.19.161.100...                                                                   
    Connected to alecto.jtac-east.jnpr.net.                                                    
    Escape character is '^]'.                                                                  
                                                                                               
    alecto-re1 (ttyp0)                                                                         
                                                                                               
    login: lab                                                                                 
    Password:                                                                                  
                                                                                               
    --- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC                      
    {master}                                                                                   
    lab@alecto-re1> set cli screen-width 300                                                   
    Screen width set to 300                                                                    
                                                                                               
    {master}                                                                                   
    lab@alecto-re1> set cli timestamp                                                          
                                                                                               
    Nov 23 01:43:24                                                                            
    CLI timestamp set to: %b %d %T                                                             
                                                                                               
    {master}                                                                                   
    lab@alecto-re1> [Sun Nov 23 01:42:50 EST 2014::..it's all yours now!:)..]                  
                                                                                               
    Nov 23 01:43:24                                                                            
                                                                                               
    {master}                                                                                   
    lab@alecto-re1>                                                                            
### SLEEP command (platform-independent)

## use this tool in a shell script

file: printver.sh

    ver=`crtc -H -q -c "show version | no-more" $1 | grep -i "base os boot" | awk '{print \$5}'`
    echo "router $1 is running software versoin: $ver"

run the shell script:

    ping@ubuntu1404:~/bin$ printver.sh alecto@jtac
    router alecto@jtac is running software versoin: [12.3-20140210_dev_x_123_att.0]

    ping@ubuntu1404:~/bin$ printver.sh tintin@jtac
    router alecto@jtac is running software versoin:  [12.3R3-S4.7]

### run your junos shell script form a server(without modification)

just rename the script name to 'cli', and that's it.


## "persist" mode

if use `-p` (or `set persist_mode 1`), the login will be a little bit
"persistent" - it won't be kicked off easily as usual:

    telnet> quit                                                             
    Connection closed.                                                       
                                                                             
    will reconnect in 30s                                                    
    ping@ubuntu1404:~$ telnet b6tsb17.jtac-west.jnpr.net 7021                
    Trying 172.22.194.102...                                                 
    Connected to b6tsb17.jtac-west.jnpr.net.                                 
    Escape character is '^]'.                                                
                                                                             
    Type the hot key to suspend the connection: <CTRL>Z                      
                                                                             
                                                                             
    alecto-re0 (ttyd0)                                                       
                                                                             
    login: lab                                                               
    Password:                                                                
                                                                             
    --- JUNOS 12.3-20140210_dev_x_123_att.0 built 2014-02-10 20:40:15 UTC    
    {backup}                                                                 
    lab@alecto-re0> set cli screen-width 300                                 
    Screen width set to 300                                                  
                                                                             
    {backup}                                                                 
    lab@alecto-re0> set cli timestamp                                        
                                                                             
    Nov 24 08:10:40                                                          
    CLI timestamp set to: %b %d %T                                           
                                                                             
at this time, there is no easy way to kick off the session.  one way is to
press the `ctrl-z` keybind supported by this script to send a hangup signal.
this will move it running background. It can then be killed (by sending a
SIGKILL signal) as a process.

    {backup}                                                                 
    lab@alecto-re0> c-z was pressed, move this session background!           
                                                                             
    [1]+  Stopped                 crtc alecto-re0-con@jtac                   
    ping@ubuntu1404:~$ kill -9 %1                                            
                                                                             
    [1]+  Stopped                 crtc alecto-re0-con@jtac                   
    ping@ubuntu1404:~$                                                       
    [1]+  Killed                  crtc alecto-re0-con@jtac                   
    ping@ubuntu1404:~$                                                       

## misc options

* `-v`:     version
* `-l`:     print all currently configured hosts
* `-h`:     some help document (todo)


## keybind

`C-Z`     suspend current login session, make it running in background.


    {master}                                                                  
    lab@alecto-re0> set cli screen-width 300                                  
    Screen width set to 300                                                   
                                                                              
    {master}                                                                  
    lab@alecto-re0> set cli timestamp                                         
                                                                              
    Nov 22 12:51:05                                                           
    CLI timestamp set to: %b %d %T                                            
                                                                              
    {master}                                                                  
    lab@alecto-re0> [Sat Nov 22 12:50:33 EST 2014::..c-z was pressed!..]      
                                                                              
    [1]+  Stopped                 crtc alecto@jtac                           
    ping@ubuntu1404:~$ ^C                                                     

to continue, fg it to run in the front.

    ping@ubuntu1404:~$ fg      
    crtc alecto@jtac          
                               
    Nov 22 12:52:55            
                               
    {master}                   
    lab@alecto-re0>            

`!l`      list currently configured hosts

`!e`      edit config file


## todo

* to support a pre-defined "stateful" cmd sequence
* to provide a menu, easier host selection
* to support compact options
* to provide a tuturial or a man page
* github, license , etc
