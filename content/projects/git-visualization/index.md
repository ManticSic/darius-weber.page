---
title: 'Git Visualization'
author: 'Darius Weber'
date: 2023-12-23
image: /projects/git-visualization/thumbnail.jpg
tags:
  - data visualization
  - git
  - git scm
  - version control
badges:
  - data visualization
  - git
  - git scm
  - version control
links: [ { url: https://github.com/ManticSic/git-history-visualization, icon: fab fa-github } ]
socialShare: false
toc: false
---

I'm new in writing blog posts or articles, but for me, there always has to be at least one picture accompanying such an article to liven it up a bit.

After finishing the content of my first blog post  [The Evolution of Git][1] I started to search for a picture or at least some inspirations to spruce it up.
Because the article was about Git, I thought it would be a great idea to have something with the Git logo or a branch visualization, but unfortunately, I didn't find anything I liked. I started to use generative AIs to generate something, but in the end, I was not satisfied with the results - and I gave up (for now).

A few days later I found a [data visualization of Jeff Palmer][1], which I though looked very interesting. I didn't knew at what I'm looking, but I liked it. By reading his blog post I learned that the graphic visualizes the history of the Git SCM repository and I started to think about it.

Coincidentally, I had one additional day off (extended weekend, woohoo!) and no plans. It was a long time, since I programmed in my spare time, so I decided to find a way to replicate his work (simply coping it wouldn't be fun).

First I searched for engines, frameworks or something like that, which only needs to get some data and voilà! I'm not in data visualization and everything I found looked like a deep hole and I only had three days: So I decided to do everything by myself.

The first decision was whether I use python (which should be very suitable) or something else. It's not that I can't program in Python, but I would have to set up my computer for this first, that's why I choosed C# (yes, TypeScript would be also a valid choice, but no).

In C# it is very easy to draw images (at least on Windows). And after finding a way to calculate and visualize an archimedean spiral, it was pretty easy. I spent most of the time with tweaking the sizes of the borders and circles, the order of layers and rotating the whole spiral. But it was fun!

I decided to only generate the spiral and adding everything else with Gimp. I'm pretty happy with the result:

![Visualization of the Git SCM repository](/projects/git-visualization/history-of-git-repository.jpg)

[1]: /blog/the-evolution-of-git/
[2]: https://jpalmer.dev/2021/03/visualizing-the-change-history-of-the-git-repository/
