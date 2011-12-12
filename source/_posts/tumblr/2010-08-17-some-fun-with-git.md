---
layout: post
comments: true
title: Some fun with git
categories:
- git
- source code control
- awesome
---
Found a neat trick today while trying to figure out something in git:

I had a folder in my project which i wanted to be ignored and not tracked by git, the folder was called `site`, so my gitignore file had the following line:

```
site/*
```

Although today i realised there was a subfolder called `javascripts` which i wanted to track, but still ignore the rest of `site`. Instead of manually setting ignore for each of the folders and files within site i googled around a bit and came up with this:

```
site/*
!site/javascripts
```

This ignores all of the files and subfolders in `site` except for javascripts.

I love git :) Also I wasn’t sure if the author of this post was kidding, or serious ? [http://stackoverflow.com/questions/767147/how-do-i-tell-git-to-ignore-gitignore](http://stackoverflow.com/questions/767147/how-do-i-tell-git-to-ignore-gitignore)
