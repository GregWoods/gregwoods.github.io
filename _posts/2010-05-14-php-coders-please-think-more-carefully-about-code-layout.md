---
id: 75
title: 'PHP Coders  - Please Think More Carefully About Code Layout'
date: 2010-05-14T08:30:12+00:00

layout: single

guid: http://gregwoods.co.uk/?p=75
permalink: /2010/05/php-coders-please-think-more-carefully-about-code-layout/
categories:
  - Programming
---
I've only recently started to use PHP again, but have coded a lot of classic ASP over the last few years, and both platforms share the same potential annoyances in code layout. Both languages were designed for the easy intermingling of server side code and html. Whilst I like this ease, it can result in spagetti code. My top tip is to make a decision. Your page is either:

  1. Almost entirely server side code with some html. In his case, replace most of your inline php tags with print commands. More code, but easier to read
  2. An html template with a scattering of simple, server-side placeholder variables. In this case, don't put any logic in the inline php, move it elsewhere

My second gripe is around indenting, and placement of php tags.  Here's a php code fragment from the WordPress Codex:

<pre>&lt;?php $my_query = new WP_Query('category_name=featured&#038;posts_per_page=1');
while ($my_query-&gt;have_posts()) : $my_query-&gt;the_post();
    $do_not_duplicate = $post-&gt;ID; ?&gt;
Html block here
&lt;?php endwhile; ?&gt;
</pre>

I find the above pretty nasty. The sample below is my preferred formatting. I have:

  1. Given priority to the server-side code for indenting. Everything between the while and endwhile is indented one tab, even the code outside of the php tags
  2. Made it clear when we switch between server-side and client-side code, but putting the opening and closing php tags on their own line. It will be easier to read context switches between server-side and html code

<pre>&lt;?php 
$my_query = new WP_Query('category_name=featured&posts_per_page=1');
while ($my_query-&gt;have_posts()) :
    $my_query-&gt;the_post();
    $do_not_duplicate = $post-&gt;ID;
    ?&gt;
    Html block here
    &lt;?php
endwhile;
?&gt;
</pre>

My formatting may be more lines of code, but it is easier to see what is going on.