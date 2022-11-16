---
title: "Newsboat is Awesome!!"
date: 2022-11-15T07:33:37+05:30
tags: ['blog']
---

## What is Newsboat
I Recently came across a program called [newsboat](https://wiki.archlinux.org/title/Newsboat)
, which is an rss feed reader.
For those who do not know, rss feeds are updates posted to any website and you can subscribe to them
to know what is up.
It also works on reddit sites, and youtube (tho youtube limits to the latest 15 videos upoaded)

This means you can use it as a newreader to keep track of everything you want,
right from the command line!!

## Getting Started
+ First, install newsboat, its available as an arch package, but also probably exists on apt.
+ make a new directory in $HOME called .newsboat, and make two new files in it, *config* and *urls*
+ The *config* file contains the config for newsboat (the colors and bindings and macros)
+ The *urls* file is just a list of urls that you want to subscribe to.

## The config file
By default, the bindings dont allow for vim keys, and also the colors are whack on my terminal.
The macros can make your life so much easier, but I haven't quite figured it out yet.

### Example config file:
```toml
# ~/.newsboat/config

# general settings
auto-reload yes
max-items 50

# externel browser
browser "/usr/bin/brave"
macro m set browser "/usr/local/bin/mpv %u"; open-in-browser ; set browser "/usr/local/bin/w3m %u"
macro l set browser "/usr/local/bin/firefox %u"; open-in-browser ; set browser "/usr/local/bin/w3m %u"

# unbind keys
# unbind-key ENTER
unbind-key j
unbind-key k
unbind-key J
unbind-key K

# bind keys - vim style
bind-key j down
bind-key k up
# bind-key j next articlelist
# bind-key k prev articlelist
bind-key J next-feed articlelist
bind-key K prev-feed articlelist
bind-key G end
bind-key g home
bind-key d pagedown
bind-key u pageup
bind-key l open
bind-key h quit
bind-key a toggle-article-read
bind-key n next-unread
bind-key N prev-unread
bind-key D pb-download
bind-key U show-urls
bind-key x pb-delete

color listnormal cyan default
color listfocus black yellow standout bold
color listnormal_unread blue default
color listfocus_unread yellow default bold
color info red black bold
color article white default bold

# Macros
# macro y set browser "mpv %u" ; open-in-browser ; set browser "elinks %u"
macro y set browser "youtube-dl -q -f %u"; open-in-browser ; set browser "elinks %u"

highlight all "---.*---" yellow
highlight feedlist ".*(0/0))" black
highlight article "(^Feed:.*|^Title:.*|^Author:.*)" cyan default bold
highlight article "(^Link:.*|^Date:.*)" default default
highlight article "https?://[^ ]+" green default
highlight article "^(Title):.*$" blue default
highlight article "\\[[0-9][0-9]*\\]" magenta default bold
highlight article "\\[image\\ [0-9]+\\]" green default bold
highlight article "\\[embedded flash: [0-9][0-9]*\\]" green default bold
highlight article ":.*\\(link\\)$" cyan default
highlight article ":.*\\(image\\)$" blue default
highlight article ":.*\\(embedded flash\\)$" magenta default
```
## The urls file
The urls file just contains all the urls/rss feeds you want
to subscribe to.

### Example urls file
```toml
--WEBSITES--
https://kshitijaucharmal.github.io/index.xml
https://lukesmith.xyz/index.xml
https://www.reddit.com/r/unixporn/new.rss

--YOUTUBE--
https://www.youtube.com/feeds/videos.xml?channel_id=UCmtyQOKKmrMVaKuRXz02jbQ
https://www.youtube.com/feeds/videos.xml?channel_id=UC0e3QhIYukixgh5VVpKHH9Q
```

(You can make sections with **--SECTION--**)

## Getting rss feed urls from websites

Some websites make this very easy, for example, you can
add *index.xml* to the end of [my website](https://kshitijaucharmal.github.io/index.xml)
and add that url to the urls file.

### From Youtube
+ Open the youtube channel you want to subscribe to
+ View Its source (Ctrl+u on brave)
+ Search for *channel_id=* and the second result will be the url you need

### From reddit
+ Go to the subreddit you want to subscribe to.
+ You can choose the new tab to subscribe to the new posts
+ Then go to the url bar, remove the last / and add *.rss* to the end.
+ That is the url you need.
