---
id: 461
title: Using my VIM config in Windows (gVim)
date: 2014-02-03T21:27:23+00:00

layout: single
classes: wide
guid: http://gregwoods.co.uk/?p=461
permalink: /2014/02/using-my-vim-config-in-windows-gvim/
categories: programming sysadmin
---
This continues from my last post, and is mostly a reminder to myself!

My .vimrc file, created for VIM on the RaspberryPi, is also usable on gVim in Windows. It's the same 2 steps, fetch using Git, and make a symlink (yes you can do that on Windows too)

Open an elevated command prompt (run as administrator)

<pre>cd \users\greg
git clone https://github.com/GregWoods/.vim.git vimfiles
mklink _vimrc vimfiles\.vimrc</pre>

Job done!

### Update:

Older versions of Windows (such as Windows Server 2003) so not have the mklink command.  
Also needed to add an environment variable $HOME

In the case of Windows Server 2003, I set up a user environment variable in System Properties -> Advanced -> Environment Variables -> User Variables  
Variable: $HOME Value: %USERPROFILE%  
Requires log off / login  
Then create the link (it's a hardlink rather than the softlink which mklink creates. For explanation, see <a title="overview to understanding hard links, junction points and symbolic links in windows" href="http://comptb.cects.com/overview-to-understanding-hard-links-junction-points-and-symbolic-links-in-windows/" target="_blank">overview-to-understanding-hard-links-junction-points-and-symbolic-links-in-windows</a> )

<pre>fsutil hardlinks create _vimrc vimfiles\.vimrc</pre>