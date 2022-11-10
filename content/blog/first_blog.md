---
title: "First Blog - Pup"
date: 2022-11-09T16:44:09+05:30
tags: ['personal', 'blog']
---

## What I learned today

Today I came across a fantastic tool called [pup](https://github.com/ericchiang/pup).

From github:
### Pup is "*a command line tool for processing HTML. It reads from stdin, prints to stdout, and allows the user to filter parts of the page using CSS selectors.*"

It is basically a html parser, and makes web scraping from websites dead simple.

## What I did

I used pup in a simple script, which just fetches all the links on a website, and gives you a list 
to choose one, and then opens it up in a browser

![Gif](/get-links.gif)
## Tools used
+ dmenu 
+ grep 
+ curl 
+ pup 
+ brave (any browser)

## Walkthrough

So first lets get a website, I'll use [mine](https://kshitijaucharmal.github.io/main), and curl it

```toml
curl -sL https://kshitijaucharmal.github.io/main
```

Now pass that in pup with the --color flag. This just makes it look better

```toml
curl -sL https://kshitijaucharmal.github.io/main | pup --color
```

We want all the links now, so as you might know, links in html are in a tag "\<a>" and in the attribute **href**.
```toml
curl -sL https://kshitijaucharmal.github.io/main | pup --color 'a attr{href}'
```
## Output
```toml
#main-content
/
/main
/blog
/
/main/
/tags/personal/
#what-this-website-is-about
https://gohugo.io/
#my-youtube-channel
https://youtube.com/@artificialcode
#online-projects
https://kshitijaucharmal.github.io/gridworld
https://kshitijaucharmal.github.io/NEAT-JS
https://narutotheboss.itch.io/bishop-challenge
#passion-projects-on-github--gitlab
https://github.com/kshitijaucharmal/2048
https://github.com/kshitijaucharmal/WaveFunctionCollapse
https://github.com/kshitijaucharmal/gridworld
https://github.com/kshitijaucharmal/GridWorld-Processing
https://github.com/kshitijaucharmal/NEAT-JS
https://github.com/kshitijaucharmal/NEAT-Algorithm
https://github.com/kshitijaucharmal/bishop-challenge
https://github.com/kshitijaucharmal/Reverse-Shell
https://github.com/PlumPeach
https://github.com/kshitijaucharmal/Genetic-Sentences
https://github.com/kshitijaucharmal/KMeans-Visualization
https://github.com/kshitijaucharmal/Lorenz-Equation
https://github.com/kshitijaucharmal/Flocking
https://github.com/kshitijaucharmal/Boids
https://www.facebook.com/sharer/sharer.php?u=https://kshitijaucharmal.github.io/main/&amp;quote=Kshitij%27s%20website
https://twitter.com/intent/tweet/?url=https://kshitijaucharmal.github.io/main/&amp;text=Kshitij%27s%20website
https://pinterest.com/pin/create/bookmarklet/?url=https://kshitijaucharmal.github.io/main/&amp;description=Kshitij%27s%20website
https://reddit.com/submit/?url=https://kshitijaucharmal.github.io/main/&amp;resubmit=true&amp;title=Kshitij%27s%20website
mailto:?body=https://kshitijaucharmal.github.io/main/&amp;subject=Kshitij%27s%20website
#the-top
https://gohugo.io/
https://git.io/hugo-congo
```

Lets grep out the lines starting with http to just get the links and pipe it to dmenu

```toml
curl -sL https://kshitijaucharmal.github.io/main | pup --color 'a attr{href}' | grep '^http' | dmenu -i -l 10
```
 Now you can store it in a variable and ask brave to open it!!

```toml
brave $(curl -sL https://kshitijaucharmal.github.io/main | pup --color 'a attr{href}' | grep '^http' | dmenu -i -l 10)
```

Thats it.

## Finished [Script](https://gist.github.com/kshitijaucharmal/3f8beecb1b65bbb12ca0507895d10d1f)
