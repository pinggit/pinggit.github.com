---
layout: post
title: "bad work flow, bad day"
published: true
created:  2013 Dec 22 03:07:05 PM
tags: [work]
categories: [work]

---

initial `issue0`: there are some chinese charactors in my PR update and need to
be corrected

simple like that , right?

OK. now the war started...

oh that's an issue of my linux locale , so I need to :
* just remove the chinese chars , manually, and update PR. done. and fix the
  generic linux locale issue later on.
* why don't correct my linux locale issue (`issue#1`)? that's sth brought
  troubles from time to time...

without thinking, picked 2).

that's still fine, maybe good choice .... --- only if it can be fixed in
not-long-time...

how to fix issue#1 then?

* I ssh into the linux and couldn't find a solution in short time , via CLI
  (`issue#2`)
* I think I know how to fix it in GUI (there are some menus about language
  settings)

now, how to get login into the GUI (`issue#3`)?

I checked my notes and quickly found krfb , So I started it. now I need a
vncviewer client...

go downloaded it, found a cool plugin named "vncviewer for chrome". 

get it downloaded and installed...looks cool. launched it and attemped
connecting to my linux box, no response...

now, is my krfb doing the right work (`issue#4`)?

check `netstat` to look at if the right port got listened...again with help of
my notes...  gee...it's not krfb, its actually another thing named
sino-blabal-vnc that is actullay listenning port 5900...what the thell.  let me
kill it! but still no luck...

ok, let me forget about krfb and check vnc. I tested with both vnc4server and
vncserver, no luck.  when I check port, they seem only listen to port 5901 on
tcpv6? what's goinging on (`issue#5`)?

let's forget about these crabs and get back to the rocket solid CLI...

some researches on the locale file `/etc/default/locale` shows that if I
comment out the line containing "zh..."(meaning chinese font) I'll be
fine...did that, but doesn't work still...

while struggling all of these without a "quick"(or even "slow") resolution, I'm
thinking to get help from peoples...some irssi channels are blinking in
my screen status bar...great. let me post my question on a vim/linux group...
bingo!  someone send some smart ideas and my issue got solved like a charm!

at the same time I realized my VIM display issue also got fixed. great!

then we talked about the vim colorscheme. we exchanged ideas and even
screencaptures of different colorscheme.  the annoying thing is that it's not
just a matter of taste of colorscheme , the final look are actually affacted by
multiple things, including the setup of the terminal that we use to start ssh,
`background` setting doesn't change things much. then I realied my colorscheme
toggling code doen't actually work `(#issue6`)-- it worked on 1st hit and stop
working on the 2nd keystroke -- sheet (I'm a polite person)..

googling and researching again, how come it worked before but not now? I
remember I even had a [jekyll blog
post](http://www-in.juniper.net/~pings/myblog/2013/02/26/a-shortcut-quick-way-to-write-a-complicated-map-without-bothering-function-call/)
mentioning how convenient it is to have
a complicted map without boring a funciton call.. after quickly checking that
post, it was initially working and I later expanded it a couple of more lines
to support more colorscheme toggling..  finally I realized there is one small
mistake in the new code,which broke it. it's all about the vim `<Bar>` magic...

then I corrected everything, 

* verified it 
* updated the old blog post

But the thing is, when I was verifing it in one of my relatively long source
file, I noticed the `taglist` of that tcl/exect script still jumped into the
source file on a enter hit, while my expectation was to make it still locate
the source location, but just don't jump "into" the source file and always
remains where it was (coz then I have to manually jump back to taglist file to
keep navigating) -- this was an old issue that I initially didn't have a good
resolution (`issue#7`).  but hold on ... I realized recently I saw a gmail
discussion to my [recent
post](https://groups.google.com/forum/#!topic/vim_use/Ttk4KYb15Z4) that
provided a solution: use `autocomd` to define a new behavior to `<CR>`(enter),
which just can do exactly what I was thinking -- and it works well for
`quickfix` window! Then why don't simply apply the same idea for `taglist`?

However, I added similar code for taglist and quickly tested it...it doesn't work!

it looks that my final `<CR>` map was still overided by `taglist`
plugin at the last, that is after my `.vimrc` was called. then I checked the
order of VIM script executions, etc. and I think I need a good way to delay my
`autocmd` code in `vimrc`, and have them to be executed the last after
everything else done...

Actually the `p` command under taglist window just do exactly what I wanted,
but my as a generic question still I need to know how to define a new map :

* in .vimrc
* specific to a ft and a local buffer
* able to overide all other plugins/scripts, but just overide in the scope of a
  local buffer/ft.

So what's the next? ...

wait wait... 3+ hours passed... what is my initial issue#0 that made me seat down
to work in a relaxing [rainy
weekend](http://www.google.com/imgres?sa=X&espv=210&es_sm=93&biw=1280&bih=581&tbm=isch&tbnid=4SwWAQ67z-03eM:&imgrefurl=http://8o-clock.deviantart.com/art/rainy-day-please-stay-146885906&docid=a_7uw0szMOr_5M&imgurl=http://fc08.deviantart.net/fs42/i/2009/146/a/a/rainy_days_by_Ronaaa.jpg&w=800&h=526&ei=Rli3Uu7cFMiokQexjIH4AQ&zoom=1&ved=1t:3588,r:78,s:0,i:324&iact=rc&page=5&tbnh=168&tbnw=277&start=65&ndsp=16&tx=182&ty=84),
while I usually was peacefully reading Buddha,
Jesus, sima-guang, dickens , García Márquez , Salinger and Yasunari Kawabata?
how come I ended up with 7 more issues to work on ? the worst part is, I've
been crazily worked for a while and what's the done job?

this is a full 瞎折腾. I really need to stop this kind of `hell of
troubleshooting circle`. focus on one issue a time , prioritize, get the
initial issue#0 resloved and don't go too far beyond at one time.  that's it.

