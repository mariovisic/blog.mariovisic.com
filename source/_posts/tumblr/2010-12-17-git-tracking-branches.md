---
layout: post
title: Git Tracking Branches
categories:
- git
- version control
---
Sometimes when I create a new branch it doesnt push to remote just by using
`git push`. I need to specifically run `git push origin [branch-name]
I found this which sets the branch to track to its upstream.
git branch --track
