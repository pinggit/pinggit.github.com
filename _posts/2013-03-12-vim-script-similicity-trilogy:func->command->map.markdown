---
layout: post
title: "vim script similicity trilogy:func->command->map"
published: true
created:  2013 Mar 12
tags: [vim]
categories: [tech]
---

vim's similicity

function: program the complex editing task within a function  
command:  use a simple user-defined command to call the function  
map:      simplify the user command with a few key stroke (normal less than 3)  


    function! CopyNonFolded() range  	"function w/ range
    let lnum= a:firstline 			"record start of range
    let buffer=[]  				"init a var to store text
    while lnum <= a:lastline  		"start from 1st line in the range
         if (foldclosed(lnum) == -1)  	"if not in fold
             let buffer += getline(lnum, lnum) "store that literal line
             let lnum += 1  		"check next line
         else  				"otherwise (step on a fold)
             let buffer += [ foldtextresult(lnum) ] "just store that 'displayed' text
             let lnum = foldclosedend(lnum) + 1 "and increase lnum to the last line 
         endif  				"of the fold,+1 (go out of curr fold)
    endwhile 

    "1) open a buffer, append the list into the buffer
    "top new  				"open a new buff at top
    "set bt=nofile  				"buftype: not a file (no use?)
    "call append(".",buffer)  		"append(put) what we got in the buffer
    "0d_  					"delete curr line(same as dd)
    "2) ping: put the list into register directly
    let @"=join(buffer,"\n") . "\n"

    endfu 

    com! -range=% CopyFolds :<line1>,<line2>call CopyNonFolded() 
    "ping, visual map
    vn "" :CopyFolds<CR>




