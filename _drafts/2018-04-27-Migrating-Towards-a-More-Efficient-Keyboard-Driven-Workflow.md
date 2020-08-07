---
layout: post
title: Migrating Towards a More Efficient Keyboard Driven Workflow 
author: Nikolai Shields
date:  2018-04-27 14:39:47
categories: [Workflow]
tags: [git, bspwm, tiling, window manager, wm]
---

If your like me, then you appreciate simplicity and efficiency.
In recent months I find myself not only annoyed, but in some instances, distracted by the features of the window managers I come in contact with, most notably gnome.
I surmise that there is a fair bit of conatct switching going on as I traverse multiple windows across multiple monitors and workspaces,
and have found that this opens up the possibility to become distracted.

I have spent some time using tiling window managers in the past, and became fairly proficient with Awesome, i3, Openbox, and Bspwm to name a few.
However I was unable to make a definitive switch, as I have yet to be able to reach a configuration that has a contiguous feel, not to mention a clean way of managing network and vpn connections.
So I find myself feeling unhappily bound to gnome...

No more I say!

Since switching my dotfile management to an aliased git repo ([see my prior post](https://nikolaishields.com/2018/How-I-Manage-My-Dotfiles/)),
I've found that making the inevitable switch to a new workflow has been much less stressful, as I can develop my files and create separate branches for other peoples configurations that I would like to test out.

Which gets us to the point of this post...
making the switch to a tiling window manager can be daunting, especially when you want things to work a certain way.
So I propose, if you've seen the posts on [r/unixporn](https://www.reddit.com/r/unixporn/) and feel inspired by their creativity and simplicity give the following a try : 

Find a post with someones dotfiles you like and give them a read, 
then create a new branch with the following command :

```bash
config branch Nikzt-dots
config checkout Nikzt-dots
git clone https://github.com/Nikzt/dotfiles.git
```

Then just move everything into place, delete the stuff you dont want to use, and run login to your new environment.
If you don't like it then drop the changes, delete the branch.
If you like some stuff, commit the parts your like and merge them into your another branch with your own files.

Anyway I hope this helps at least one person out there.

-N
