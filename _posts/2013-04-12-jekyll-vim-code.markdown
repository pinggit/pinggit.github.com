---
layout: post
title: "vim shortcut keys for blog composition and publishing"
created:  2013 Apr 11 10:25:25 PM
tags: 
    - jekyll
    - vim
categories: 
    - tech
published: true
---

I like the [jekyll](https://github.com/mojombo/jekyll)-way of blogging, it gives
me almost all what I desired for blogging. The essential here (at least for me)
is simplicity (or "minimalism") - simply editing blog content as a pure text
file with your whatever favorite pure text editor , and uploading the blog file with
whatever file synchrozation technique, that's it.

but still, there are some last pieces of annoying work to do here, if you use it
in a daily base:

* what if, you want to publish a block of marked/selected texts from your editor
  (like the "visually selected text" in vim), as a blog post?

* there is no official **asciidoc** support (yet), but **markdown** is kind of a
  poor markup language. So how to also publish a selected range of
  asciidoc-formatted texts, into a blog post (I do this for those
  heavy/long/serious articles)?

* how to make the file synchronization (git/ftp/scp/rsync/whatever) even simpler
 -say, with one or two key strokes?

plus, a vimer typically prefer to have all things done , **without leaving vim**
-that is to compact all external commands to be executed, into a few keystroke shortcut
maps...

here is some final(targetted) quick keystrokes, each accomplishing one task:

    ",ji            select blog id: 1 or 2
    ",js            compose a new post from scratch/start (no pre-selected content)
                    in a new buffer(no tab) call: ->CMD:JekyllPost->FUNC:JekyllPost
                    visual mode, call: JekyllPostRange<CR>
    ",jp            compose a new post with current (selected or whole) content
                    in a new tab, call: JekyllPostRange<CR>
                    nn: use whole current file as content of new post (in new tab)
                    vn: use selected text as content of new post(in new tab)
    ",ja            publish asciidoc blog to jekyll, normal or visual mode
    ",jA            publish asciidoc blog to jekyll, normal mode only, support
                    user command-line selection
    ",jg            jekyll git external commands
    ",jl            list all existing posts for current blog. call :JekyllList<CR>
    ",jt            jekyll theme selector

    "some not-oftenly-used keys
    ",jP            :quick push (don't wait user input) and review
    ",jd            append discus code in the file
    ",jb            :JekyllBuild<CR>
    ",jy            prefix yaml header in the file

I find myself use ,ji ,jl ,ja and ,jg most of the time.

that is:

1. to compose a new post from scratch, press ,js

2. to start a new post from a range of selected text, just visual select them and press ,jp
   same keys for the whole texts

3. same as 2, but mainly for asciidoc users, so it's a lot heavier. The selected text
   must be in asciidoc format.  press ,ja will guide the user through a few
   Q-n-As (each with default answer prompted).  These will end up with all
   required parameters feed into asciidoc engine and get the final doc (html,
   html5) , generated. the source text will also be saved in a seperate
   accompanying file as a backup (but won't get published by default).  same
   keystroke also works for whole texts, if no texts were selected (no range).

4. if the blog looks OK, press ,jg to get it published. Depending on which blog
   it belongs to, this keystroke will call different file sync technique to get the
   work done:

   - for blog1 , which is my public blog, call git commands sequence to
   **push** the source files to github site, which , will be responsible for the
   site generation

   - for blog2, which is my work blog , runing on an internal web/ssh server, without a git
   server (like github) deployed : 

        * first generate whole site into a local folder using my local jekyll engine

        * then call rsync to make sure all files will be synchronized to the server

5. to switch between 2 sites, prss ',ji'. all posts will be saved into the
   corresponding blog folders repectively.

and here is the vim script codes:

    "jekyll--- 
    "

    "(optional)turn off all additional backup files
    nn ,nf <esc>:set nobackup<CR>:set noudf<CR>:set noswf<CR>

    "set nobackup noudf noswf

    "yaml highlight 
    "this doesn't work
    "function! Jekyll()
    "    execute "autocmd BufNewFile,BufRead " . g:jekyll_path . "/* syn match jekyllYamlFrontmatter /\\%^---\\_.\\{-}---$/ contains=@Spell"
    "endf

    "this works
    function! JekyllY()
        unlet b:current_syntax
        syntax include @Yaml syntax/yaml.vim
        syntax region yamlFrontmatter start=/\%^---$/ end=/^---$/ keepend contains=@Yaml,@Spell
        let b:current_syntax='markdown'
    endf

    nmap ,jy :call JekyllY()<CR>,nf

    "vars and maps 
    "ping: 
    if !exists('g:jekyll_post_created')
      let g:jekyll_post_created = "%Y %b %d %X"
    endif

    "constant: blog1
    if !exists('g:jekyll_path')
        let g:jekyll_path="~/mytest-project/jekyll-site/pinggit.github.com"
        "let g:jekyll_post_suffix = "textile" 
        "let g:jekyll_post_published = "false"
    endif

    "constant: blog2
    if !exists('g:jekyll_path2')
        let g:jekyll_path2="~/mytest-project/jekyll-site/blog.clone"
        let g:jekyll_path2="~/mytest-project/jekyll-site/juniperblog"
    endif

    "save the path change
    if !exists('g:jekyll_currentpath')
        let g:jekyll_currentpath=g:jekyll_path
    endif

    if !exists('g:jekyll_title')
      let g:jekyll_title = "dummy"
    endif

    if !exists('g:jekyll_title_pattern')
      let g:jekyll_title_pattern = "[ '\"]"
    endif

    if !exists('g:jekyll_post_suffix')
      let g:jekyll_post_suffix = "markdown"
    endif

    if !exists('g:jekyll_prompt_tags')
      let g:jekyll_prompt_tags = "life"
    endif

    if !exists('g:jekyll_prompt_categories')
      let g:jekyll_prompt_categories = "life"
    endif

    if !exists('g:jekyll_asciidoc_insertyaml')
        "turn off yaml, currently page looks ugly after enabling this
        let g:jekyll_asciidoc_insertyaml = 1
    endif

    if !exists('g:jekyll_template')
      let g:jekyll_template = [""]
    endif

    if !exists('g:jekyll_post_published')
      let g:jekyll_post_published = "false"
    endif

    if !exists('g:jekyll_upload')
      let g:jekyll_upload= "github"
    endif

    if !exists('g:jekyll_blogid')
      let g:jekyll_blogid= 1
    endif

    if !exists('g:jekyll_disqus_template')
        let g:jekyll_disqus_template="~/mytest-project/jekyll-site/pinggit.github.com/disqus-template.txt"
    endif

    nn        ,jb  :JekyllBuild<CR>
    nn        ,js  :JekyllPost<CR>
    map       ,jp  :JekyllPostRange<CR>
    nn        ,jl  :JekyllList<CR>
    nn <expr> ,jL  RangerChooser(g:jekyll_path . "/_posts") <bar> sleep 3

    "checkout and post
    "com! -nargs=1 JPost execute '!rake post title=<q-args>' | e YOUR_FILE


    "Asciidoc to Jekyll--- 

    function s:esctitle(str)
      let str = a:str
      let str = tolower(str)
      let str = substitute(str, g:jekyll_title_pattern, '-', 'g')
      let str = substitute(str, '\(--\)\+', '-', 'g')
      let str = substitute(str, '\(^-\|-$\)', '', 'g')
      return str
    endfunction


    function JekyllTemplate() "
        "always build template per current data:
        "if g:jekyll_template == ''
        let tags = input("use previous tag? [" . 
            \g:jekyll_prompt_tags . 
            \"](y/NEW TAG):",'y')
        if tags == 'y'
            let tags = g:jekyll_prompt_tags "try, save it
        else
            if tags != ''
                let g:jekyll_prompt_tags=tags
            endif
        endif

        let categories = input("use previous categories? [" . 
            \g:jekyll_prompt_categories . 
            \"](y/NEW CATEGORIES):" , 'y')
        if categories == 'y'
            let categories = g:jekyll_prompt_categories "try, save it
        else
            if categories != ''
                let g:jekyll_prompt_categories=categories
            endif
        endif

        let created = g:jekyll_post_created

        if created == "epoch"
            let created = localtime() 
        elseif created != ""
            let created = strftime(created)
        endif

        "let template = ["---", "layout: post", "title: \"" . g:jekyll_title . "\"", "published: " . published]
        let template = ["---", "layout: post", "title: \"" . g:jekyll_title . "\""]
        if created != ""
          call add(template, "created:  "  . created)
        endif
        if tags != ""
          call add(template, "tags: [" . tags . "]")
        endif
        if categories != ""
          call add(template, "categories: [" . categories . "]")
        endif

        let published = g:jekyll_post_published
        call add(template, "published: " . published )
        call extend(template,["---", ""])

        return template
    endf

    "(02/20/2013) publish a asciidoc-generated html blog
    "function! A2J(leveloffset, title)
    function! JekyllPrefixYamlHeader() "
        let template=JekyllTemplate()
        let err1 = append(0, template)
    endf

    map ,jy :call JekyllPrefixYamlHeader()<CR>

    function! JekyllAppendDisqus() "
        let template4disqus=g:jekyll_disqus_template
        exec "normal Go\<CR>\<CR>\<esc>"
        exec "read" . template4disqus
    endf

    map ,jd :call JekyllAppendDisqus()<CR>

    function! A2J(...) range "

        "initialization
        let os=-1
        let title=g:jekyll_title
        "not sure if better than html backend
        let format="html"
        let toc="-a toc2"

        let g:lasttab = tabpagenr()

        "ping:yank the selected texts
        exe a:firstline . "," . a:lastline . "yank"

        "if 1st params is not given (provided 0 params), ask for it
        if a:0 == 0

            let os=input("use default offset?" . '[' . os . ']' . "(y/0/-1/-2/-3/..):",'y')
            if os == 'y'
                let os = -1
            endif
        "if 1 param is given, use it as offset
        else
            let os=a:1
        endif

        "if 2nd param is not given, ask for it
        if a:0 <= 1 
            let title=input("want to use previous/default title?" . 
                \'[' . g:jekyll_title . ']' . "(y/NEW TITLE):" ,
                \'y')
            if title=='y'
                let title=g:jekyll_title
            else
                if title != ""
                    let g:jekyll_title = title
                endif
            endif

        else
            let title=a:2
            let g:jekyll_title = title
        endif

        "if 3rd param is not given, ask for it
        if a:0 <= 2
            let supported_backend="1-html,2-html5,3-blogger"
            let format_number=input("use the current asciidoc backend format?" . 
                \'[' . format . ']' . 
                \supported_backend . ':', 'y')
            if format_number==1
                let format="html"
            elseif format_number==2
                let format_number="html5"
            elseif format_number==3
                let format="blogger"
            else
            endif

        elseif a:0 == 3
            let format=a:3
        else
            echo "too much parameters: max is 3"
        endif

        let toc=input("want to use toc?[0:no-toc,1:toc,2:toc2]" , "2")
        if toc=='0'
            let toc=''
        elseif toc=='1'
            let toc='-a toc'
        elseif toc=='2'
            let toc='-a toc2'
        else
        endif

        if title == ''
          let title = input("Post title (better) not be empty: ")
          if title != ''
              let g:jekyll_title = title
          endif
        endif

        if title != ''
            let g:jekyll_title = title
            let file_name = strftime("%Y-%m-%d-") . 
               \s:esctitle(title)

            "exe "tabedit " . g:jekyll_path . "/_posts/" . file_name

    "       let path=input("use default/previous path?" . '[' . g:jekyll_path . ']' . "(y/<NEW PATH>):",'y')
    "       if path=='y'
    "           let path=g:jekyll_path
    "       else
    "           if path != ''
    "               let g:jekyll_path=path
    "           endif
    "       endif

            let path=input("use default/previous path?" . '[' . g:jekyll_path . ']' . "(y/n):",'y')
            if path=='y'
                let g:jekyll_blogid=1
                let path=g:jekyll_path
            elseif path=='n'
                let path=input("use default/previous path?" . '[' . g:jekyll_path2 . ']' . "(y/<NEW PATH>):",'y')
                if path=='y'
                    let path=g:jekyll_path2
                    let g:jekyll_blogid=2
                    let g:jekyll_upload='rsync'
                endif
                let g:jekyll_currentpath=path
            endif

            let full_name = path . "/_posts/" . file_name . "." . "html"
            "let g:AsciidocCmd = ":0,\$w !asciidoc 
            let g:AsciidocCmd = ':' . a:firstline . ',' . a:lastline . 
                \"w !asciidoc 
                \-a numbered " . toc . " " . "
                \-a toclevels=4 
                \-a iconsdir=/home/ping/bin/asciidoc-8.6.8/images/icons 
                \-a icons -a data-uri -a showcomments 
                \-a max-width=85em -a theme=volnitsky 
                \-o " . full_name . " " . "
                \-a leveloffset=" . os . "@" . " " . "
                \-b " . format . " - "

                "\-o " . "'" . full_name . "'" . " " . "

            echo "\nthe following CLI will be executed\n" g:AsciidocCmd

            let isSure=input("are you sure?(y/n):",'y')
            if isSure == 'y'
                exec g:AsciidocCmd

                "save the original selected texts and prepend with yaml
                let full_name_asciidoc = path . "/_posts/" . file_name . "." . "txt"
                exe "tabnew " . full_name_asciidoc
                call JekyllPrefixYamlHeader()
                exe "normal! p"
                "call JekyllAppendDisqus()
                exec "wq!"

                "try: insert template(yaml front end) in html file
                exe "tabnew " . full_name
                exe "normal u"

                "prepend yaml in HTML. since yaml insertion in asciidoc generated
                "html make it looks ugly, make it optional
                if g:jekyll_asciidoc_insertyaml
                    call JekyllPrefixYamlHeader()
                endif

                "append disqus code in HTML
                "let err2 = append(line('$'), "# THE END")
                "call JekyllAppendDisqus()

                "save the new webpage and quit ,then go back to original tab
                "exec "wq!"
                "exec "tabn " . g:lasttab
                
            else
                "this doesn't work to user cmd. good for expr map
                return g:AsciidocCmd

            endif
        endif
    endf

    "todo: 
        "gmail thread: vim script: repeat(\<left>)
        "need to archive same with ,ja, when user say no, pop cmds but no exec..
        "it looks this is not possible (or sth I don't know)
    "command! -nargs=* A2J :call A2J(<f-args>)
    com! -range=% -nargs=* A2J :<line1>,<line2>call A2J(<f-args>)

    "map <expr> ,ja ':' . A2J(-1, "new_post") . repeat("\<left>", 24)
    "no need ':' since the func will return a ':'
    "support:               the option of presenting CLIes for user selection
    "don't support:         don't work for visual range
    "nmap <expr> ,jA A2J(-1) . repeat("\<left>", 24)
    nmap <expr> ,jA A2J(-1) . "\<c-b>" . repeat("\<delete>",3)

    "support:               all non-range or range
    "don't support:         returning CLIes for user selection
    map ,ja :A2J


    "JekyllGit 

    "this works, but too ugly
    "nn ,gg :!git add -A .;git commit -m "msg: ";git push origin master"
    "            \<left><left><left><left><left><left><left>
    "            \<left><left><left><left><left><left><left>
    "            \<left><left><left><left><left><left><left>
    "            \<left><left><left><left><left>

    "this is much better
    "todo: need to save original path and restore after git finished
    "select right folder, lcd into it, then pop up git commands for user's selection
    "let g:jekyll_currentpath=g:jekyll_path
    function! JekyllGit(commitmsg)
        let current_blogid=input("is current blog ID " . g:jekyll_blogid. '? (y/n/newID)' , 'y')
        if current_blogid=='y'
            let current_blogid=g:jekyll_blogid
        endif

        if current_blogid=='n'
            if g:jekyll_blogid==1
                let current_blogid=2
            elseif g:jekyll_blogid==2
                let current_blogid=1
            else
            endif
        endif

        if current_blogid==1
            let g:jekyll_upload='github'
            let current_path=g:jekyll_path
        elseif current_blogid==2
            let g:jekyll_upload='rsync'                 "set proper upload method
            let current_path=g:jekyll_path2
        else
        endif

        let g:jekyll_blogid=current_blogid

        "this doesn't work
        ":lcd current_path
        "this works
        let original_path=getcwd()
        exec "lcd" . current_path
        echo "original path" . '[' . original_path . ']' . "is saved." "\n"
        echo "lcd into new path" . '[' . current_path . ']' . "\n"

        let commitmsg=a:commitmsg

        let commitmsg = input ("use last msg[" . g:jekyll_title . "]?[y/NEW TITLE]:" , 'y')
        if commitmsg == 'y'
            let commitmsg = g:jekyll_title
        else
            let g:jekyll_title = commitmsg
        endif

        if g:jekyll_blogid==1
            let generate='sleep 1'
            let upload="git push origin master"
        elseif g:jekyll_blogid==2
            let generate='jekyll --safe --no-auto'

            "todo: -a is a bit slow, --size-only is faster?
            let upload="
            \rsync --delete -vqrlczP " . 
            \current_path . 
            \"/_site/ pings@svl-jtac-tool01:public_html/myblog/"
        else
            let upload="git push origin master"
        endif

        let GitCmd="!
            \git add -A .;
            \git commit -m \"" . 
            \commitmsg . "\";" . generate . ";" . upload . '&'
            "\repeat("\<left>", 30)

        "return to original path
        "exec "lcd" . original_path

        "there must be at least one ':' in returned cmds!
        return ":" . GitCmd
    endf

    "command! -nargs=* JekyllGit call JekyllGit(<q-args>)
    command! -nargs=* JekyllGit exec JekyllGit(<q-args>)
    nn <expr> ,jg JekyllGit(g:jekyll_title) . repeat("\<left>", 24)

    func JekyllThemeToggle()
        let supported_themes="\n  1-twitter\n  2-holligan\n  3-the-minimum\n  4-the-program\n  5-dinky\n  6-mark-reid\n  7-tom\n"
        let theme=input("use which theme?" . "\n[" . supported_themes . "]\n" . "(1/2/3/..):",'1')
        if theme==1
            let theme="twitter"
        elseif theme==2
            let theme="hooligan"
        elseif theme==3
            let theme="the-minimum"
        elseif theme==4
            let theme="the-program"
        elseif theme==5
            let theme="dinky"
        elseif theme==6
            let theme="mark-reid"
        elseif theme==7
            let theme="tom"
        else
        endif

        let theme_change_cmd=":!rake theme:switch name=\"" . theme . "\""
        return theme_change_cmd

    endf
    nn <expr> ,jt JekyllThemeToggle()

    "quick publish the post (git push + w3m review)
    "pending issues:
    "  don't know how to prompt&wait for user input
    map ,jP :
         \exec JekyllGit("g:jekyll_title") . repeat("\<left>", 24) <Bar>
         \!w3m http://pinggit.github.com
         \<CR>

    function! JekyllSetBlogID(blogid) "
        let g:jekyll_blogid=a:blogid
        if g:jekyll_blogid==1
            let g:jekyll_currentpath=g:jekyll_path
            let g:jekyll_upload="github"
        elseif g:jekyll_blogid==2
            let g:jekyll_currentpath=g:jekyll_path2
            let g:jekyll_upload="rsync"
        else
        endif
        exec "lcd" . g:jekyll_currentpath
    endf

    nn ,ji :call JekyllSetBlogID(1)

