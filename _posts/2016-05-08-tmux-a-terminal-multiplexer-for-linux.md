---
id: 15
title: Tmux A Terminal Multiplexer For Linux
date: 2016-05-08T15:08:59+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=15
permalink: /index.php/computers/linux/tmux-a-terminal-multiplexer-for-linux/
post_icon:
  - linux.png
categories:
  - Linux
tags:
  - terminal
---
Tmux lets you manage terminal space by dividing screen in to multiple panes and windows. In this way, one doesn&#8217;t need to have a different tool for having new tabs and split screens.

It lets you switch easily between several programs in one terminal, detach them (they keep running in the background) and reattach them to a different terminal. I am trying to configure and get comfortable with it. Will post more on this soon.

<span style="color: #3366ff;"><a style="color: #3366ff;" href="https://tmux.github.io/">https://tmux.github.io/</a></span>

I have been using this since almost 7 months and I should say that, I do not need any other program for having multiple tabs or splitting screens. Tmux becomes much more powerful and user friendly after one has customized it for their own tastes in terms of short cut keys. Here are some most common short cuts or commands used together with tmux.

<https://blog.vishdaily.com/index.php/tutorials/terminal-commands/#tmux>

### **Tmuxinator &#8211;** Another little tool assisting windows and panes creation

<https://github.com/tmuxinator/tmuxinator/>

With tmuxinator one can define how many windows and different panes in those windows one wants via a tmuxinator template YML file. This is similay a YML formatted template in which one can define the windows they want and different panes they wanted. This is useful, if one works in a standard environment where they have to open same kind of locations all the time and navigate between them.

In addition to tmux installing tmuxinator, will drastically improves the way one can create panes or windows. Here is my sample configuration. This creates 3 windows called local, localplay and sshplay, In which local window is splitted to 6 panes with starting paths mentioned.

After defining this daily.yml template, just run _mux daily_ to open tmux session with the windows and panes created as defined in the template.

```bash
##> vim ~/.tmuxinator/daily.yml

name: vishdaily-workspace
root: ~/

# Specifies (by index) which pane of the specified window will be selected on project startup. If not set, the first pane is used.
startup_pane: 1

windows:
  - general:
        layout: tiled
        panes:
         - cd ~/songs && clear
         - cd ~/daily_scripts && clear
         - cd ~/remote_dir && clear
         - cd ~/ftp && clear
         - cd ~/Downloads && clear
         - cd ~/temp/ && clear
  - ftp: cd ~ && clear
  - ssh:
        layout: tiled
        panes:
         - cd ~ && clear
         - cd ~ && clear
         - cd ~ && clear
         - cd ~ && clear

```

### Customizing Tmux Shortcuts / Configuring Tmux Look & Feel

If one wants to **change the default shortcuts**, this can be achieved by editing ~/.tmux.conf file. My sample conf file looks like this.

Here mainly, I am using character | for vertical split and &#8211; for horizontal split. Using arrows keys for navigating between panes. At the end customizing how the window and pane information should be displayed.

```bash
# remap prefix from 'C-b' to 'C-a'

#unbind C-b
#set-option -g prefix C-a
#bind-key C-a send-prefix

# split panes using | and -
bind | split-window -h
bind - split-window -v
unbind '"'
unbind %


# switch panes using Alt-arrow without prefix (Meta) key is often Alt

bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D


# Enable mouse mode (tmux 2.1 and above)
set -g mouse off


# don't rename windows automatically
set-option -g allow-rename off

# start window numbering at 1
set -g base-index 1

# start pane numbering at 1
set -g pane-base-index 1

# I customized a tmux theme pack acoording to my tastes provided by https://github.com/jimeh/tmux-themepack
source-file "${HOME}/linux-configs/tmux/tmux-themepack/powerline/block/green-vish.tmuxtheme"



```

&nbsp;