---
date: "2019-05-26T20:14:59+08:00"
publishdate: "2019-05-27+08:00"
lastmod: "2019-05-27+08:00"
draft: false
title: "Mapping keys in vim"
tags: ["vim", "blog"]
series: ["My vim journey"]
categories: ["Tools"]
img: "images/blog/2019-05/cover.jpg"
toc: true
summary: "Things started when Apple started using touch bar on MacBook. Admittedly, touch bar is good, but as a vimer, I found it really inconvenient to switch between normal mode and insert mode. One day, I could not bear it, so I decided to make some changes."
---



Things started when Apple started using `touch bar` on MacBook. Admittedly, touch bar is good, but as a vimer, I found it really inconvenient to switch between `normal` mode and `insert` mode. One day, I could not bear it, so I decided to make some changes. 

Vim has a nick name "Text editor of the Gods", so there are a lot of things you can do about vim. You can customize your vim to make it easier to use, also more powerful.

So I decided to use `map` in Vimscript. Mapping is a very useful feature of Vimscript, and the magic of mapping is that mapping keys lets you tell Vim: 

> When I press these pattern, I want vim to do this perticular stuff rather than whatever vim would normally do.

You can treat is as a shortcut. And you can map keys in `normal` mode,  `insert` mode and other modes.

So, for example, look at this Vimscript below:

```shell
:map - dd
```

When you put this line in your `.vimrc` file and `source .vimrc` to make the `.vimrc` work. You are telling vim that the next time, in `normal` mode, when I press "-", the vim will do exactly what you do with pressing three characters `dd`. So the vim will delete that line.

