---
title: Angular 2 CLI - Port Hog
permalink: /2016/09/14/angular-2-cli-port-hog//
layout: post
bigimg:
  - /assets/images/angular-superpower-photo-1.jpg
comments: true
---

I'm running lots of Angular 2 using the CLI on OSX (and loving it).

I have one small issue...

Often after stopping the app, when re-running it I get

'Port 4200 is already in use.'

Here is a little linux magic for you:

```
lsof -t -i tcp:4200 | xargs kill -9 | ng serve
```

This will find the process using port 4200, kill it, then re-serve your application.

(Posted for my FireBootCamp students that are having this issue.)