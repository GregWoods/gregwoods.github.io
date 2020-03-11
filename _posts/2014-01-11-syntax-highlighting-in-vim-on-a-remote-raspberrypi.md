---
id: 447
title: Syntax highlighting in VIM on a remote RaspberryPi
date: 2014-01-11T16:55:59+00:00
author: Greg Woods
layout: single
classes: wide
guid: http://gregwoods.co.uk/?p=447
permalink: /2014/01/syntax-highlighting-in-vim-on-a-remote-raspberrypi/
categories:
  - Linux
  - RaspberryPi
---
To VIM or not to VIM. The decades old text editor inspires avid devotion or utter hatred. I fell into the latter camp.

However, now that I&#8217;m experimenting with the Raspberry Pi for some hardware projects, it&#8217;s obvious I need something with more features than the nano editor. VIM pretty universal, will run in a terminal, or a non-GUI linux, and is undeniably fast editing once the steep learning curve is overcome.

So here are some of notes on VIM &#8211; particularly,setting up syntax highlighting with a nice colour scheme &#8211; a first step in making VIM palatable to my GUI insticts.

## Colour Schemes

If I&#8217;d spent half the time learning VIM as I&#8217;d spent trying to customise the colours, I&#8217;d be a VIM Jedi already.

### Good Schemes

<http://www.vimninjas.com/2012/08/26/10-vim-color-schemes-you-need-to-own/>

I particularly like <a title="solarized color scheme" href="http://ethanschoonover.com/solarized" target="_blank">solarized</a>

## On Windows (Putty)

If you want any chance of getting the genuine Solarized colors working in VIM through Putty, the colours in Putty must be changed.

The easiest way to do this is with [this reg file which sets up some sensible defaults for Putty](https://github.com/jblaine/solarized-and-modern-putty "Putty defaults"), including the solarized dark colours

You will need to recreate any existing sessions to get the new defaults

## On The Raspberry Pi

Connect and login using Putty. Your shell session will already have the new colour scheme

<pre>sudo apt-get install vim
cd ~
mkdir .vim
cd .vim
mkdir colors
wget <a href="https://raw.github.com/altercation/vim-colors-solarized/master/colors/solarized.vim">https://raw.github.com/altercation/vim-colors-solarized/master/colors/solarized.vim
</a>vim
:e $HOME/.vimrc
i     (insert mode)</pre>

<pre style="padding-left: 30px;"><span style="font-family: Consolas, Monaco, monospace; font-size: 12px; line-height: 18px;">syntax enable
</span>set background=dark
colorscheme solarized</pre>

<pre>:wq!      (save and close)</pre>

Now to add my VIM config to source control, we copy it to the .vim folder and symlink it first

<pre>cd ~
mv .vimrc .vim/.vimrc
ln -s .vim/.vimrc .vimrc
cd .vim
git init
ls -la         (shows hidden files)

Configure GIT</pre>

<pre>git config --global user.name "your full name"
git config --local user.name "your full name"
git config --global user.email "your email id"
git config --local user.email "your email id"
git config -l</pre>

still in the ~/.vim folder&#8230;

<pre>git add .
git commit -m "Initial commit of my vim configuration"</pre>

<pre>git remote add origin https://github.com/GregWoods/.vim

//had to do a git pull first
git pull https://github.com/GregWoods/.vim</pre>

<pre>git push origin master</pre>

&nbsp;

My VIMconfiguration is now on github.

### To install my Vim Config onto a new server&#8230;

    cd ~
    git clone https://github.com/GregWoods/.vim.git .vim
    ln -s .vim/.vimrc .vimrc

     

&nbsp;