---
layout: post
title: "How I Manage My Dotfiles"
author: Nikolai Shields
date:  2018-03-20 21:34:26
categories: [dotfiles]
tags: [dotfiles, git]
---

For awhile now I've been using about 3 machines every day for school, work and leisure computing.
This has led me down the path of diverging configurations and left me wanting a simple and extensible way for managing my dotfiles across these machines.
There are many tools out there that manage dotfiles, and many different ways to get the job done, be it symlink farmers, or repositories, or a hybrid solutions.
Bottom line is there are many different ways to skin this cat, and I needed a solution that would do the following :

1. manage and version my files
2. easily deploy my files
3. syncronize my files between machines (as I mentioned divergence being a problem earlier)
4. not many dependancies/esoteric bits of code (easily understood and well documented implementaitions)
5. manage different configurations for different machines in an easy way

With these stipulations in mind I went searching for solutions and ultimately settled on a clever comment by StreakyCobra in their post on [HackerNews](https://news.ycombinator.com/item?id=11070797),
and gained greater insight and respect for its simplicity with [this](https://developer.atlassian.com/blog/2016/02/best-way-to-store-dotfiles-git-bare-repo/) tutorial by Nicola Paolucci from Atlasssian.

By using a bare git repository in your home directory you can check-in all the files for your configuration with familiar commmands and tools, as its just a git repo :

````bash
config [ add, rm, etc ] file
config [ push, pull ]
````

The alias makes it all just feel right.

Additionally, since its a git repo, I have branches created for classes of machine and individual machines if need be. 
At present I have 4 branches in use :

+ desktop
+ laptop
+ server
+ dev

As you can imagine the laptop is configured for my Thinkpad x230, which has some keyboard remappings and disabled trackpad stuff.

Desktop is for my desktop, and server is used for my non-graphical systems.
I use my dev branch for testing new configurations.

Pretty simple and sleak, highly recommend reading StreakyCobra's original comment and trying the tutorial from Nicola, and a thanks to each of them for posting what they did.
As stumbling on it has changed my computing expirience for the better.

-N
