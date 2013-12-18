---
layout: post
title: "rm , trash-cli , vim backup files, and others"
published: true
created:  2013 Apr 04 03:28:34 PM
tags: [rm]
categories: [tech]
---

## the trouble from `rm`
it takes a long time to download the core file from 2013-0404-0651.
but annoyingly it comes with a `.dmp2` , so I quickly changed the name like this:

    ping@640g-laptop:/mnt/public_html/casedata/2013-0404-0651$ ls -l
    total 88980
    -rwxr--r-- 1 ping 935 90930520 Apr  4 14:45 LM-10_21_04_04_2013_17_03.dmp2
    ping@640g-laptop:/mnt/public_html/casedata/2013-0404-0651$
    ping@640g-laptop:/mnt/public_html/casedata/2013-0404-0651$
    ping@640g-laptop:/mnt/public_html/casedata/2013-0404-0651$ rm LM-10_21_04_04_2013_17_03.dmp2 LM-10_21_04_04_2013_17_03.dmp
    rm: cannot remove `LM-10_21_04_04_2013_17_03.dmp': No such file or directory
    ping@640g-laptop:/mnt/public_html/casedata/2013-0404-0651$ ls -l
    total 0

I think I should slow down some (or go for a beer for now)...

now I hope I won't be that quick to even blindly pressing y & then hitting return...

    alias rm='rm -i'



## (2013-05-16) another incident

it looks i just cautiously bypassed the fragile wall that i
set up to prevent another incident...

    $ ls -lct
    total 2536
    -rwxr-x--- 1 ping ping 214584 May 16 11:58 pair1-resize-jpg.pdf
    -rwxr-x--- 1 ping ping 275735 May 16 11:46 pair1.jpg
    -rwxr-x--- 1 ping ping 326791 May 15 19:38 pair1-resize.pdf
    -rwxr-x--- 1 ping ping 517941 May 15 18:12 pair2.pdf
    -rwxr-x--- 1 ping ping 595350 May 15 18:12 pair1.pdf
    -rwxr-x--- 1 ping ping    891 May 15 18:12 temp.sh
    -rwxr-x--- 1 ping ping    890 May 15 18:12 temp.sh~
    -rwxr-x--- 1 ping ping 146232 May 15 15:19 pg_0005.pdf
    -rwxr-x--- 1 ping ping 126196 May 15 15:19 pg_0003.pdf
    -rwxr-x--- 1 ping ping 130720 May 15 15:19 pg_0002.pdf
    -rwxr-x--- 1 ping ping 239406 May 15 15:19 pg_0001.pdf
    test$ find ./ -newercc pg_0005.pdf -exec rm -rf {} \;
    rm: cannot remove directory: `.'
    $ convert pair1.pdf -geometry 612x792 -quality 100 pair1-resize.pdf
    convert: unable to open image `pair1.pdf':  @ error/blob.c/OpenBlob/2587.
    convert: missing an image filename `pair1-resize.pdf' @ error/convert.c/ConvertImageCommand/3011.
    test$ 

I was testing some pdf related work here. I setup this folder for
testing purpose. `pg_000x.pdf` files are files that I need to work on (basically I
need to merge/split/rotate/combine pdf files and make a book), they were copied
into this test folder first. all other files were generated based on these 4
files, except temp.sh, which is a small shell script I wrote to process all
input files in a batch mode.
firstly I was satisfied with my quick cleaning command here: `find` all files
that is newer (in terms of change time here - technically not only file content,
but essentially the inode ) than a specified file. then just remove all of them.
but problem is that this time I somehow decided to use the `-rf` version of
it...  and among those files that I really wanted to remove, I also permanently
removed the small shell script that I still need...

now I lost it. what are the options I have now? 

* recover from HD? no
  [way](http://gergap.wordpress.com/2008/07/18/how-ext3grep-can-save-you-hours-of-work/)

* recover from VIM backup?

  since the deletion was time-based, even all hidden files that VIM
  generated to track the file content change were removed. otherwise I can recover
  the file via the backup files.

* recover from VCS/dropbox ?

  I didn't put this temporary folder file into git track, nor in dropbox (lesson
  learned - better create temporary folders under dropbox)

* ignore the event, re-create the file from scratch!

I think my best option is the last one. so if I can't recover from this tragic
event,  maybe I can try to secure the future more -- I need to stay away from rm
(especially `-rf`)further...

## solution1
here is some quick script I got from the Internet

    #!/bin/sh
    # trashit
    #put this in .bashrc:
    # alias rm='~/bin/trashit'
    #
    # original script
    #    http://www.macosxhints.com/article.php?story=20030217172653485
    #    author: Shane Celis <shane (at) gnufoo (dot) org>
    #
    # Sun, 20-May-2007; 06:47:22 
    #    minor changes...

    if [ $# -eq 0 ]; then
            echo "usage: trashit <files...>" >&2
            exit 2;
    fi

    for file in "$@"; do
        # get just file name 
        destfile="`basename \"$file\"`"
        suffix='';
        i=0;

        # If that file already exists, change the name
        while [ -e "$HOME/.local/share/Trash/${destfile}${suffix}" ]; do
                suffix="-$i";
                i=`expr $i + 1`
        done
        mv -vi "$file" "$HOME/.local/share/Trash/${destfile}${suffix}"
    done

it works. but the problem is , if my filename contains spaces it still has an
issue.

## solution2

then I found the [trash-cli](https://github.com/andreafrancia/trash-cli)
project , which was commented as a "much better tool" in this case. even better
I found my laptop already have it installed.

    ping@640g-laptop:~/temp-transfer$ touch a.txt
    ping@640g-laptop:~/temp-transfer$ trash-put a.txt
    ping@640g-laptop:~/temp-transfer$ touch a.txt
    ping@640g-laptop:~/temp-transfer$ trash-put a.txt
    ping@640g-laptop:~/temp-transfer$ touch a.txt
    ping@640g-laptop:~/temp-transfer$ trash-put a.txt

    ~/.local/share/Trash/files$ ls -lct | head
    total 211964
    -rw-rw-r-- 1 ping ping        0 May 16 12:40 a.txt_2
    -rw-rw-r-- 1 ping ping        0 May 16 12:39 a.txt_1
    -rw-rw-r-- 1 ping ping     7589 May 16 12:39 a.txt

way to go! will use `trash-cli` for a while ( `rm -rf` as
the last resort still) and see...

## solution3

I always believe that VIM is a (at least "half-baked" if not perfect) VCS by
itself. that said, so if I set vim backup files in a different folder, then even
afer I removed the source file in a folder, its backup files should still be
maintained intact , right? so here is the magic workaround from another angel:

    set dir       = ./.vim-swap//
    set backupdir = ./.vim-backup//
    set undodir   = ./.vim-undo//

more talk about the issue in [this book](http://web.mit.edu/~simsong/www/ugh.pdf)

