---
layout: post
title: "vim automatic filetype detection and setup based on file properties"
published: true
created:  2013 May 17 02:32:39 PM
tags: [vim]
categories: [tech]
---

vim is powerful, but vimL is surely a hard script to learn.
the balance is, do you want more power or more simplicity? ("BOTH" is not an
option :) )

let me throw some code here:

    au BufRead,BufNew,BufAdd *.asciidoc,README,TODO,CHANGELOG,NOTES setfiletype=asciidoc
    au BufRead,BufNew,BufAdd *.txt call s:FTasciidoc(AsciidocChecklines)
    au BufRead,BufNew,BufAdd *.log call s:FTlog()

it's all about vim filetype setup (then you have syntax highlight , fold,
file-specific keybindings, ... whatever, all of the VIM magics ). and most of the
complexity comes from the "auto-detection" techniques. ideally what I want are:

* if you are sure what filetype you need, "hard code" it based on the file extention
* otherwise, "look into" the file content to decide
  * if the .txt file "looks like" an asciidoc, set it to asciidoc filetype
  * if the .log file "looks like" a junose or junos log file, we have to narrow it
    down to tell whether it's 
    * a config file (mostly just a "show config" ) or 
    * a troubleshooting log file (full of "show xxx") -- based on the nature, we can
      apply different syntax (highlighting for config use different rules than
      highlighting system logs)

* when doing this , also consider the file size - a huge text file severely
  slow down the VIM performance (jump,search,change,update,etc) if equiped
  with syntax magic.

* if it doesn't look like known specific types, just set it to txt or whatever ...

"code speaks louder than words", here it is:

    "ping
    "this file merged some content detection files
    " (2013-05-17) move fsize check into the autocmd function call 
    " (otherwise won't work if prior to the function code)
    "
    "define a global var knob, to enable/disable debug info on asciidoc file detection
    "
    if !exists("MyAsciidocDebug")
        let MyAsciidocDebug = 0
    endif

    if !exists("MyJelDebug")
        let MyJelDebug = 0
    endif

    if !exists("AsciidocChecklines")
      let AsciidocChecklines = 10
    endif

    if !exists("JecCheckLines")
      let JecCheckLines = 200
    endif

    if !exists("JecCheckLineLength")
      let JecCheckLineLength = 100
    endif

    if !exists("AsciidocCheckLineLength")
      let AsciidocCheckLineLength= 50
    endif

    let s:largefilesize = 1000000

    "w/o BufRead works for $vim file.txt, but not for :tab file.txt. that need BufNew, 
    au BufRead,BufNew,BufAdd *.asciidoc,README,TODO,CHANGELOG,NOTES setfiletype=asciidoc
    au BufRead,BufNew,BufAdd *.txt call s:FTasciidoc(AsciidocChecklines)
    au BufRead,BufNew,BufAdd *.log call s:FTlog()


    " This function checks for a valid AsciiDoc document title after first
    " skipping any leading comments.
    function! s:FTasciidoc(checklines)

      let s:fsize = getfsize(expand('%%:p')) "get current file size

    " ping: add another check, set asciidoc if there is a "= ABC" preceded with a blank line
      let n = 1                         "starting from 1st line

      if g:MyAsciidocDebug | echom 'asciidoc scan partI: check ^= xx in first '.a:checklines." lines" | endif

      while n <= a:checklines           "checking 1st 10 lines
        let line = getline(n)           "get a line
        let n = n + 1                   "increase number# earlier to make sure it get increased

        if g:MyAsciidocDebug | echom 'get a line:" ' . line . '" at number ' . (n-1) | endif
        if len(line) > g:AsciidocCheckLineLength   "skip pattern search if too long
          if g:MyAsciidocDebug | echom "line " . (n-1) . "is too long to be a heading, skip" | endif
          continue                      
        endif                     

        if line =~ '^=\+\s\S\+'         "if exact one space bet = and text(make it strict)
          if getline(n-2) =~ '^\s*$'    "and an empty line exist right before this line
            if (s:fsize <= s:largefilesize)
              if g:MyAsciidocDebug | echom "asciidoc mark ^= xxx found in 10lines, not a huge file,ft set to asciidoc2..." | endif
              set filetype=asciidoc2
              "return after successfully set
              return                    
            else
              if g:MyAsciidocDebug | echom "asciidoc mark ^= xxx found in 10lines, a huge file(over 2M!),ft set to asciidoc" | endif
              set filetype=asciidoc
              "return after successfully set
              return                    
            endif
            return                      
          else
            if g:MyAsciidocDebug | echom "asciidoc mark = ^xxx found, but no empty line ahead, ft not set to asciidoc" | endif
          endif
        else
        endif
      endwhile                          

      if g:MyAsciidocDebug | echom "asciidoc mark not found in first " . a:checklines . "lines, don't set ft" | endif
      if g:MyAsciidocDebug | echom 'asciidoc scan partI finished' | endif




      " otherwise,
      " scan the file line by line, skipping all comment blocks and comment lines
      " for a title/header text
      if g:MyAsciidocDebug | echom 'asciidoc scan partII: check text and dashes in first '.a:checklines." lines" | endif
      let in_comment_block = 0
      let n = 1                         "starting from 1st line

      while n < a:checklines            " 

        let line = getline(n)           "get a line
        if g:MyAsciidocDebug | echom 'get a line:" ' . line . '" at number ' . (n-1) | endif

        if len(line) > g:AsciidocCheckLineLength   "skip pattern search if too long
          if g:MyAsciidocDebug | echom "line " . n . "is too long to be a heading, skip" | endif
            let n = n + 1
          continue                      
        endif                     

        let n = n + 1                   "anchor move to next line
        if line =~ '^/\{4,}$'           "if '////..', then it's a comment block
          if ! in_comment_block         "if haven't seen it before
            if g:MyAsciidocDebug | echom "looks we found first comment in comment block" | endif
            let in_comment_block = 1    "mark it as block start
          else                          "otherwise,
            if g:MyAsciidocDebug | echom "looks we found 2nd comment in comment block" | endif
            let in_comment_block = 0    "mark it as block end
          endif
          continue                      "go check next line
        else
            if g:MyAsciidocDebug | echom "not a comment block" | endif
        endif                           "in either case

        if in_comment_block             "if we are still in block
          if g:MyAsciidocDebug | echom "we are still in a comment block,continue" | endif
          continue                      "move on
        endif

        if line !~ '\(^//\)\|\(^\s*$\)' "if we find sth else (means out of block)
          if g:MyAsciidocDebug | echom "found sth else other than a comment block mark/empty line,break" | endif
          break                         "meaning it's neither '//' nor blank line,break the loop
        endif                           "as this point we got some texts that

      endwhile                          "we assume to be a title or header

      "the title/header texts must be more than 3CH
      if line !~ '.\{3,}'               "if the line is too short (<3)
        if g:MyAsciidocDebug | echom "line " . (n-1) . "is too short and not looks like a heading line, skip" | endif
        return                          
      endif

      "there must be a '---' or '===' line under the text,also need >3 CH
      let len = len(line)               "now check 'next' line, get length & content
      let line = getline(n)             "see line 23(n=n+1) for why it's next line
      if line !~ '[-=]\{3,}'            "if there are no 3 or more '-' or '='
        if g:MyAsciidocDebug | echom "no 3 or more contineous -/= found under the above text,return" | endif
        return                         
      endif

      "the length difference of text and mark line in the header/title must less than 3
      if len < len(line) - 3 || len > len(line) + 3
        if g:MyAsciidocDebug | echom "length diff bet text and -/= under it is bigger than 3,return" | endif
        return
      endif

      "if such a title/head is found, then it's an asciidoc
      "setfiletype asciidoc

      "ping, add fsize check...
      if (s:fsize <= s:largefilesize)
        set filetype=asciidoc2      
        if g:MyAsciidocDebug | echom "asciidoc mark2 found & file is small, set ft asciidoc2" | endif
      else
        set filetype=asciidoc
        if g:MyAsciidocDebug | echom "asciidoc mark2 found & file is big, set ft asciidoc" | endif
      endif

      if g:MyAsciidocDebug | echom 'asciidoc scan partII finished' | endif

    endfunction


    function! s:FTlog()

    " ping: (2013-05-17) add file check
      let s:largefilesize = 1000000
      let s:fsize = getfsize(expand('%%:p')) "get current file size

      if (s:fsize <= s:largefilesize)

          let n = 1                         "starting from 1st line
          let endline = line('$')
          if g:MyJelDebug | echom "max line number is" endline | endif
          while n < g:JecCheckLines         "checking some lines from 1st line

              let line = getline(n)           "get a line

              if g:MyJelDebug 
                echom "get a line" line
                echom "looking for show config in the line..."
              endif

              if len(line) > g:JecCheckLineLength              "skip pattern search if too long
                let n = n + 1                 "very efficient/time saving!
                continue                      
              endif                     

              if line =~ '\S\S\+[^\]]\{0,45}\S[#>%]\s*show config'      "searching 'show config'
                  let ratio = (endline - n) * 100 / endline               "if match, check how much its output occupy the file
                  if ratio >= 60                "if 'show config' capture is alot
                      set filetype=jec            "set ft to jec(junos e config)
                      if g:MyJelDebug
                        echom "show config detected, set ft to jec" 
                      endif
                      return                      
                  else                          "otherwise if no much output, 
                      if g:MyJelDebug             "don't set jec
                        echom "show config detected but no much output, set ft to jel" 
                      endif
                      set filetype=jel
                      return
                  endif

              else                            "or if no show config detected,don't set

              endif

              let n = n + 1                   "otherwise check next line

          endwhile                          

          if g:MyJelDebug | echom "no show config detected, set ft to jel" | endif
          set filetype=jel

      else
        echom "file too large (current size:" . s:fsize . " Bytes > maxsize for ft check " . s:largefilesize . " Bytes!) , won't set ft"
      endif

    endfunction

    " vim: et sw=2 ts=2 sts=2:
