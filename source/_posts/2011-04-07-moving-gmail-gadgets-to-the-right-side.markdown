--- 
layout: post
title: Moving Gmail Gadgets to the Right Side
wordpress_url: http://timbroder.com/?p=900
date: 2011-04-07 14:56:39 -04:00
comments: true
tags: 
- gmail
- remember the milk
- css
---
I started using Remember the Milk recently but didn't want the <a href="http://www.rememberthemilk.com/services/gmail/gadget/" target="_blank">gmail gadget</a> to be so far down on the left hand side of my screen. There is no built in way to move gadgets to the right hand side with the exception of chat (labels used to do this but was removed in favor of drag in drop back in late 2009).

<a href="/images/wp-content/uploads/2011/04/gmail_right_widgets.png"><img class="size-full wp-image-901 alignleft" title="gmail_right_widgets" src="/images/wp-content/uploads/2011/04/gmail_right_widgets.png" alt="" width="513" height="455" /></a>

&nbsp;

If you don't have anything in the right hand column, <em>enable Right-Side Chat</em> from Gmail Labs. We are going to add in some custom css to gmail so install either <a href="https://chrome.google.com/extensions/detail/pabfempgigicdjjlccdgnbmeggkbjdhd" target="_blank">Stylist </a>for Chrome or <a href="https://addons.mozilla.org/en-US/firefox/addon/stylish/" target="_blank">Stylish</a> for Firefox.

Add the following style:

``` css
div.TZ:nth-child(8) {
    position:absolute !important;
    right:0px;
    top:165px;
    width:164px;
}```


In chrome you can also restrict the domain to mail.google.com.  For me, the Remember the Milk gadget was the 8th child.  Play with this until it looks right for you. You may also have to play with the "top" element depending on how much room your chat gadget takes up
