---
layout: post
title: "7 tips to attain peace of mind (markdown)"
published: true
created:  2013 May 16 08:45:35 AM
tags: [english]
categories: 
    - life
    - mind
---

</style>
<script type="text/javascript">
/*<![CDATA[*/
var asciidoc = {  // Namespace.

/////////////////////////////////////////////////////////////////////
// Table Of Contents generator
/////////////////////////////////////////////////////////////////////

/* Author: Mihai Bazon, September 2002
 * http://students.infoiasi.ro/~mishoo
 *
 * Table Of Content generator
 * Version: 0.4
 *
 * Feel free to use this script under the terms of the GNU General Public
 * License, as long as you do not remove or alter this notice.
 */

 /* modified by Troy D. Hanson, September 2006. License: GPL */
 /* modified by Stuart Rackham, 2006, 2009. License: GPL */

// toclevels = 1..4.
toc: function (toclevels) {

  function getText(el) {
    var text = "";
    for (var i = el.firstChild; i != null; i = i.nextSibling) {
      if (i.nodeType == 3 /* Node.TEXT_NODE */) // IE doesn't speak constants.
        text += i.data;
      else if (i.firstChild != null)
        text += getText(i);
    }
    return text;
  }

  function TocEntry(el, text, toclevel) {
    this.element = el;
    this.text = text;
    this.toclevel = toclevel;
  }

  function tocEntries(el, toclevels) {
    var result = new Array;
    var re = new RegExp('[hH]([1-'+(toclevels+1)+'])');
    // Function that scans the DOM tree for header elements (the DOM2
    // nodeIterator API would be a better technique but not supported by all
    // browsers).
    var iterate = function (el) {
      for (var i = el.firstChild; i != null; i = i.nextSibling) {
        if (i.nodeType == 1 /* Node.ELEMENT_NODE */) {
          var mo = re.exec(i.tagName);
          if (mo && (i.getAttribute("class") || i.getAttribute("className")) != "float") {
            result[result.length] = new TocEntry(i, getText(i), mo[1]-1);
          }
          iterate(i);
        }
      }
    }
    iterate(el);
    return result;
  }

  var toc = document.getElementById("toc");
  if (!toc) {
    return;
  }

  // Delete existing TOC entries in case we're reloading the TOC.
  var tocEntriesToRemove = [];
  var i;
  for (i = 0; i < toc.childNodes.length; i++) {
    var entry = toc.childNodes[i];
    if (entry.nodeName.toLowerCase() == 'div'
     && entry.getAttribute("class")
     && entry.getAttribute("class").match(/^toclevel/))
      tocEntriesToRemove.push(entry);
  }
  for (i = 0; i < tocEntriesToRemove.length; i++) {
    toc.removeChild(tocEntriesToRemove[i]);
  }

  // Rebuild TOC entries.
  var entries = tocEntries(document.getElementById("content"), toclevels);
  for (var i = 0; i < entries.length; ++i) {
    var entry = entries[i];
    if (entry.element.id == "")
      entry.element.id = "_toc_" + i;
    var a = document.createElement("a");
    a.href = "#" + entry.element.id;
    a.appendChild(document.createTextNode(entry.text));
    var div = document.createElement("div");
    div.appendChild(a);
    div.className = "toclevel" + entry.toclevel;
    toc.appendChild(div);
  }
  if (entries.length == 0)
    toc.parentNode.removeChild(toc);
},


/////////////////////////////////////////////////////////////////////
// Footnotes generator
/////////////////////////////////////////////////////////////////////

/* Based on footnote generation code from:
 * http://www.brandspankingnew.net/archive/2005/07/format_footnote.html
 */

footnotes: function () {
  // Delete existing footnote entries in case we're reloading the footnodes.
  var i;
  var noteholder = document.getElementById("footnotes");
  if (!noteholder) {
    return;
  }
  var entriesToRemove = [];
  for (i = 0; i < noteholder.childNodes.length; i++) {
    var entry = noteholder.childNodes[i];
    if (entry.nodeName.toLowerCase() == 'div' && entry.getAttribute("class") == "footnote")
      entriesToRemove.push(entry);
  }
  for (i = 0; i < entriesToRemove.length; i++) {
    noteholder.removeChild(entriesToRemove[i]);
  }

  // Rebuild footnote entries.
  var cont = document.getElementById("content");
  var spans = cont.getElementsByTagName("span");
  var refs = {};
  var n = 0;
  for (i=0; i<spans.length; i++) {
    if (spans[i].className == "footnote") {
      n++;
      var note = spans[i].getAttribute("data-note");
      if (!note) {
        // Use [\s\S] in place of . so multi-line matches work.
        // Because JavaScript has no s (dotall) regex flag.
        note = spans[i].innerHTML.match(/\s*\[([\s\S]*)]\s*/)[1];
        spans[i].innerHTML =
          "[<a id='_footnoteref_" + n + "' href='#_footnote_" + n +
          "' title='View footnote' class='footnote'>" + n + "</a>]";
        spans[i].setAttribute("data-note", note);
      }
      noteholder.innerHTML +=
        "<div class='footnote' id='_footnote_" + n + "'>" +
        "<a href='#_footnoteref_" + n + "' title='Return to text'>" +
        n + "</a>. " + note + "</div>";
      var id =spans[i].getAttribute("id");
      if (id != null) refs["#"+id] = n;
    }
  }
  if (n == 0)
    noteholder.parentNode.removeChild(noteholder);
  else {
    // Process footnoterefs.
    for (i=0; i<spans.length; i++) {
      if (spans[i].className == "footnoteref") {
        var href = spans[i].getElementsByTagName("a")[0].getAttribute("href");
        href = href.match(/#.*/)[0];  // Because IE return full URL.
        n = refs[href];
        spans[i].innerHTML =
          "[<a href='#_footnote_" + n +
          "' title='View footnote' class='footnote'>" + n + "</a>]";
      }
    }
  }
},

install: function(toclevels) {
  var timerId;

  function reinstall() {
    asciidoc.footnotes();
    if (toclevels) {
      asciidoc.toc(toclevels);
    }
  }

  function reinstallAndRemoveTimer() {
    clearInterval(timerId);
    reinstall();
  }

  timerId = setInterval(reinstall, 500);
  if (document.addEventListener)
    document.addEventListener("DOMContentLoaded", reinstallAndRemoveTimer, false);
  else
    window.onload = reinstallAndRemoveTimer;
}

}
asciidoc.install();
/*]]>*/
</script>


## 7 Tips to Attain Peace of Mind

[有道学堂](http://xue.youdao.com/article.z?id=-7514447938861046657&keyfrom=PopWindow&abtest=1)

<!--
>    ifdef::basebackend-html[[subs="quotes"]]  
>    ifdef::basebackend-html[....]  
-->

>When you were child you had a pure mind; the mind  
>which was free from worries and anxieties. As the       ['wʌri],ʌ非常短，非[ɑ:]  
>time passed, you were influenced by several  
>social, personal, `familial` and official crises,       [fә'miljәl],not `familiar`  
>such as financial complications, broken                 a. 家族的, 家庭的  
>relationship, lack of trust, joblessness, failure         
>in business, loss of respect and so on. When the  
>mind is stressful, the associated germs of              [dʒә:m]n. 细菌, 种子  
>negativity, jealousy and pessimism `add fuel to`        ['pesimizm]n.悲观情绪  
>fire ,and hence your pure mind becomes impure.             
>These impurities,if taken out,can bring back the          
>mental purity,hence real spirit of joy of  
>childhood can be `attained` up to an adequate level.    [ә'tein]达到['ædikwәt]  
>Of course you cannot fix all of your problem at  
>once,but you can train your mind to develop the  
>skills,which can help either bypass or overcome  
>the depressed and `tragic` situations so as to give     ['trædʒik]  
>you a big time relaxation,while you focus on the        a. 悲惨的, 悲剧的  
>solution to your problems. Below are some  
>techniques which can be used to `combat` the peace      ['kɒmbæt] n. 争斗, 战斗  
>stealing triggers:  

<!--
>      
>    ifdef::basebackend-html[....]  
-->

# Mind your own business.   
  
   Yes, please mind your own business. When you start  
   being concerned about things which are not related  
   to you, you `lose your grip` on your thought process      [grip] n. 紧握, 控制  
   which often results in negativity disturbing the  
   mental peace.  Basically, your mind starts  
   wandering here and there. As you know that a  
   non-focused mind is evil's workshop hence the  
   germs of negativity and jealousy gain more  
   strength. So next time an unnecessary thought  
   comes to your mind, think whether this is really  
   something you should be worrying for? If not, `shun`      [ʃʌn]  
   `it` right away and focus on something positive,          vt. 避开, 规避, 避免  
   practical and `fruitful`.  
     
   ifdef::basebackend-html[....]  
  
# Surround yourself in positive people.   
      
   ifdef::basebackend-html[[subs="quotes"]]  
   ifdef::basebackend-html[....]  
     
   Ignore negative comments and stay away from  
   negative souls. When someone is negative, he  
   spreads negativity and you get affected.  
   Permanently staying with such people will have  
   long term impact on your character so think about  
   your `company`.  
     
   ifdef::basebackend-html[....]  
     
   NOTE: a real life joke: once we were travelling  
   with our Indian neighbors and we were sharing a  
   car. I was asked : "ping, do you like your  
   company?", and immediately I said "No ~ ~ !". Then  
   I felt people are becoming quiet! All of a sudden  
   I realized my neighbor means "themselves", not my  
   work!  
      
3. Don't think about others too much.   
      
    ifdef::basebackend-html[[subs="quotes"]]  
    ifdef::basebackend-html[....]  
      
    Remember the great quote: small minds discuss  
    people; Average minds discuss events; Higher minds      [i'vent],not ['i:vent]  
    discuss ideas and Great minds act in silence.  
    Don't allow your brain to compare yourself to  
    others as this is an insult to yourself.  Don't be      ['insʌlt]n.侮辱,损害  
    Jealous; it's a heart killing disease, get rid of  
    it as soon as possible. When you are jealous you  
    focus on finding faults in others even if they  
    don't have. This `poisons your soul` and steals the  
    mental peace.  
      
    ifdef::basebackend-html[....]  
      
4. You can't keep everyone happy.   
      
    ifdef::basebackend-html[[subs="quotes"]]  
    ifdef::basebackend-html[....]  
      
    Don't be `over sensitive`. Be natural and genuine in    ['dʒenjuin]  
    what you do. Be positive, constructive and ethical      a.真实的, 诚恳的  
    in your `deeds` and then don't really care too much     ['eθikәl]a.伦理的,  
    about others. Be aware, don't apply this formula        [di:d] 此处为“行为”  
    to too closed relations.  Develop trust to                
    establish powerful relationships.  
      
    ifdef::basebackend-html[....]  
      
5. Control your `mood swings` as it is an indication  
    of unstable personality.   
      
    ifdef::basebackend-html[[subs="quotes"]]  
    ifdef::basebackend-html[....]  
      
    Do it by not being over sensitive to others. Stop  
    being reactive and implosive.  `Stay calm`.             [ɪm'plosɪv]内爆型  
      
6. Ignore your thoughts about being unlucky.   
      
    Bad luck happens to everyone.  It's not your fault  
    at all. Time whether good or bad, passes quickly.  
    Develop the power of not looking back into your  
    past.  Believe in the power of Now. Believe in  
    your skills. Work hard and have faith in God; you  
    will get what you have `been entitled for`. Be  
    patient and see what God has planned for you.  
    Patience and consistency in your deeds is the key  
    to success.  
      
    ifdef::basebackend-html[....]  
      
7. Simplicity in your character and living style  
    can overcome the stress and improve your `happiness  
    index`.   
          
    ifdef::basebackend-html[[subs="quotes"]]  
    ifdef::basebackend-html[....]  
      
    Don't be socially sensitive and start following  
    every single trend your social circle is  
    following.  
      
    With these recommendations, I believe you can  
    bring major changes in your life style hence  
    attain back your mental peace. What are your  
    recommendations in gaining mental peace?  
      
    ifdef::basebackend-html[....]  

