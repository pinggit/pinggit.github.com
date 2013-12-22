---
layout: post
title: "a shortcut/quick way to write a complicated vim map without bothering function call!"
published: true
tags: vim
categories: tech
---


"(2013-02-26) 
"a shortcut/quick way to do a complicated map but bypassing function calls

    map ,ct :
        \if g:colors_name == 'default' <Bar>
            \:colorscheme koehler <Bar>
        \elseif g:colors_name == 'koehler' <Bar>
            \:colorscheme molokai <Bar>
        \else <Bar>
            \:colorscheme default <Bar>
        \endif <Bar>
        \<CR>
