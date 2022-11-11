---
title: "Automating the blog making process"
date: 2022-11-11T10:17:33+05:30
tags: ['blog']
---

## The problem

Whenever I need to make a blog, i need to go in the hugo directory, make a new file
with *hugo new <name of file>*, and also update the repo after that.

I want a script that makes a blog every day (just a file in the blogs folder) and then 
gives the name and the title of the date.

## The Script

```toml
#!/bin/sh

hugo_project=$1
today_date=`date | cut -d' ' -f1-4 | tr ' ' '-'`
cd $hugo_project
hugo new blog/$today_date.md 2> /dev/null || notify-send "Blog Exists" "Exiting" && exit
git add content/blog/$today_date.md
git commit -m "Added Blog file for Date $today_date"
git push origin main

hugo
hugo -D

cd public
git add -A
git commit -m "Added Blog for date $today_date to website"
git push origin master

notify-send "Added New Blog" "Successfully Done"
```

## How it works

+ So the the script is pretty simple, it first takes the hugo
repo path from the user, and gets the date from the simple
date command.

+ Then it goes to the directory, makes a new file, and sends
a notify-send to check if the file exists already. If it does,
it exits out of the loop.

+ Then the git commands just add and commit and push the new file

+ Then hugo makes the project (hugo -D)

+ Then I go in the public directory which is my 
actual website, and add everything hugo has added, 
commit and push.

+ And yeah, sends a notify-send to let me know its done

**Run this as a cron job every day at 10, and I got a 
blog Automating script!!**
