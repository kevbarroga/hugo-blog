---
title: "Migrating to Netlify"
date: 2018-01-03
tags: ["netlify", "hugo", "web", "development"]
draft: false
---

## Introduction

Just recently migrated my self-hosted site to [netlify].
Site was hosted on an old raspberry pi which I used as a low powered development system for small projects.
It was getting tedious to push commits to GitHub, ssh into the pi, pull down changes,
then finally run my custom hugo build script to generate the static files and reload nginx.

I discovered netlify on hugo's [hosting and development] section.
The process was pretty simple, instructions were clear and easy to follow.

Will be updating this post with detailed instructions soon...

These pages will still be self-hosted until I am able to migrate them:  
[My repository of the JavaScript 30 course from Wes Bos][js30]  
[Playing with D3.js][d3]  
[Simple todo list from [expalmer]][todo]

[netlify]: https://www.netlify.com/
[hosting and development]: https://gohugo.io/hosting-and-deployment/hosting-on-netlify/
[js30]: https://www.kbarro.ga/js30/
[d3]: https://www.kbarro.ga/d3/
[todo]: https://www.kbarro.ga/todo-list/
[expalmer]: https://github.com/expalmer/todo-list-vanilla-js